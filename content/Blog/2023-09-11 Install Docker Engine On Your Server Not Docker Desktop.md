I was playing with [Kestra](https://kestra.io/) as I investigated some data orchestration frameworks. 

Their `docker-compose` in their getting started was error-ing out for me on my Ubuntu server with syntax errors. I check and was running an older Docker version: `20.x`. 

So I thought I'll just install what they recommended: [Docker Desktop](https://docs.docker.com/desktop/install/ubuntu/). 

After installing I got this error as Kestra needs root privileges (I think) to spawn other containers to do work via `docker.sock`:
```
Error response from daemon: driver failed programming external connectivity on endpoint homelab-kestra-1 (35ac5e6f0948606533f8daa03a653e5c8ee79f615c329969bcf2dcee0468c1ec): fork/exec /usr/bin/rootlesskit-docker-proxy: no such file or directory
```

I thought I had done this before, passing in `docker.sock`... How did this work before?

I should have just installed [Docker Engine](https://docs.docker.com/engine/install/ubuntu/) on my server (after uninstalling Docker Desktop); and I did; and now I'm good to go 👏

# Random

I was playing with [AirByte](https://airbyte.com/) and noticed it was running after I rebooted. I had no idea where the docker-compose was that I had fired it up with was. 

Just inspect it:
[Get docker-compose.yml file location from running container? - Stack Overflow](https://stackoverflow.com/questions/42108163/get-docker-compose-yml-file-location-from-running-container)

And that told me where 💪