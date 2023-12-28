---
tags:
  - project
  - homeassistant
  - nfc
  - windmilldev
title: Home Assistant + NFC + Windmill.dev
date: 2023-12-17
---
> [!info] Goal
> I wanted to see how easy it would be to be able to scan a NFC chip and persist this to a DB for knowing when we put my son to bed or when you drive your car.

I didn't take it to the extent of writing to the DB, but what I did find is using Windmill.dev cloud hosted along with HomeAssistant's (HASS) NFC reading was **very easy**.

### TLDR

Don't mount `dbus` when running on a Ubuntu host.

### What Didn't Work

I was getting bluetooth errors and HASS wouldn't start up successfully??

- https://community.home-assistant.io/t/2022-9-causing-issues-with-my-bluetooth-and-devices/458398/30
- https://community.home-assistant.io/t/help-with-bluetooth-initialisation-after-most-recent-update/541278

> I'm assuming this was caused by mounting `dbus`, see below
### Steps I took

The [docker compose](https://www.home-assistant.io/installation/alternative/#docker-compose) in their docs didn't work for me:
```yaml
version: '3'
services:
  homeassistant:
    container_name: homeassistant
    image: "ghcr.io/home-assistant/home-assistant:stable"
    volumes:
      - /PATH_TO_YOUR_CONFIG:/config
      - /etc/localtime:/etc/localtime:ro
      - /run/dbus:/run/dbus:ro
    restart: unless-stopped
    privileged: true
    network_mode: host
```

So I after searching around and to make my life easier I went with this to get hosting working:
```yaml
volumes:  
  homeassistant:  
  
services:   
  homeassistant:  
    image: ghcr.io/home-assistant/home-assistant:stable  
    environment:  
      - TZ=US/Eastern  
    ports:  
      - 8123:8123  
    volumes:  
      - homeassistant:/config 
    restart: unless-stopped  
```

**A few things**

1. A volume isn't needed to my knowledge, I just used it in my shotgun approach trying to fix things and kept it
2. I thought it was a version issue for a while and pinned to a particular version, but that wasn't it, `stable` is fine
3. Hardcode TZ in my shotgun approach, probably not required, [list](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) of TZs
4. The privilege, networking, and port exposing just didn't work. I don't if or why these are required. I didn't look it up. My example is working fine for
5. Do **not** mount `dbus`, that was the root issue
6. The initial create account UI didn't work, the create button was disabled. You can [fix](https://community.home-assistant.io/t/home-assistant-create-account-greyed-out/436743/7) by editing the button html via dev tools
7. Had issues with the webhook format, firstly need to edit the `configuration.yaml` file:
		1. Get into the container `docker exec -it <YOUR_CONTAINER_NAME> bash`
		2. `vi configuration.yaml` (they put you in the config directory automatically, this is nice)
		3. Example config below
		4. Look at your container logs for errors, I noticed I was getting 415 errors and that helped me know I needed to set a header and format the body correctly

**Tangent**

I thought about [HASS cloud](https://www.nabucasa.com/pricing/) (nabu casa). When I go off wi-fi I'll need a solution to talk to my instance. I think the 2 easiest options are HASS cloud and Cloudflare tunnels ([[2023-09-06 Cloudflare Zero Trust Tunnel Setup]]). Since I was just exploring I didn't take it this far and test. It will be easy to test, I think, by sitting at my desk, scanning a NFC, and taking my phone off wi-fi to test over cellular

**Example webhook to Windmill**:
```yaml
default_config:
frontend:                                                                  
  themes: !include_dir_merge_named themes                                  
automation: !include automations.yaml                                      
script: !include scripts.yaml                                              
scene: !include scenes.yaml                                                
rest_command:                                                              
  windmill_troy_sleep:                                                     
    url: "https://app.windmill.dev/api/w/lkat/jobs/run_wait_result/p/u/lanekatris/troy_put_to_sleep?token=<YOUR_SECRET_TOKEN>&payload=e30%3D"       
    method: post                                                           
    headers:                                                               
      content-type: 'application/json'                                     
    payload: '{}' 
```

> [!Warning]
> I don't see a good way to see [existing webhooks](https://www.windmill.dev/docs/core_concepts/webhooks)? I don't know how to delete existing as well, I can't find the token I created either...


