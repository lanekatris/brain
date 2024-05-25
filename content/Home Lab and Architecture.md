# Backup

I added a larger hard drive [here](https://memo.lkat.io/m/7ZteyK8SGWDWwxXWbfuFP3). With inspiration from [here](https://sive.rs/backup) , I want to support these use cases:
- Shared temp folder to easily copy to my machines
- Migrate away from Onedrive - have a full copy of OneDrive with `rclone` backup to Cloudflare R2 - So long term storage
- Backup my apps with `restic`

- [ ] Complete roadmap: [[Home Lab and Architecture#Image Management]]
- [ ] Create an easy script to invoke: `scp -r lane@server1:/bigboy/temp/* c:\temp\` (it would be nice to have an rsync version for linux, scp was for windows)

# Image Management

I want to migrate off of Onedrive and host my own image storage and hosting because:
- No monthly payment
- Get off facebook as a source of truth for images (I don't do this, but the wife does)
- Anonymous user upload - for trips we take, I'd like an easy way for users to upload images/videos

**Roadmap**
1. ✅ Host [Immich](https://immich.app/)
2. ✅ Expose and lock down via cloudflare tunnels
3. ✅ Setup tailscale to get my Immich phone app working, I don't see it is supported to go through Cloudflare auth
4. Figure out manual backup
	1. [x] Put all cloudflare r2 api keys in 1password ✅ 2024-04-24
	2. [x] Make a script that updates the 3 relevant folders here ✅ 2024-04-21
	3. [x] Immich db backup ✅ 2024-04-21
		1. `docker exec -it immich_postgres pg_dumpall --clean --if-exists --username=postgres | gzip > "/bigboy/immich/db_dumps/dump.sql.gz"`
5. Figure out manual restore
	1. [ ] Do a test for folders
	2. [ ] Do a test with DB
6. [ ] Test sharing with wife
	- This will be a new access group in cloudflare zero trust then I need to add the group to the policy exposing Immich
	- [ ] Why did she get an error the first time opening via messenger?
7. [ ] Test sharing with [[2024-03-22 Snowboard Trip - Steamboat Springs]] folks as an example
8. Get all images/videos from OneDrive
9. Load all media from OneDrive into immich
10. Automated backup
11. My phone auto backup
12. Phone auto backup for Wife
13. Kill OneDrive payment

# Overview

Maitenance to do mention: https://memo.lkat.io/m/7ZteyK8SGWDWwxXWbfuFP3


I'm not looking for a Home Lab in the traditional sense. I have a server, and I need to run some things. 

I want my projects to be cloud focused and running in the cloud as that is where I'm at in my engineering career. Although, there are tools that save my time, which is our most **important** asset, and they need to always be running. **I'm cheap**, so why not run an old desktop at home?



Exposing Services
TODO: cloudflare vs opening ports in router

### To Dos
- [x] Get docker-compose rolling for [[Noco DB]] ✅ 2023-07-26
- [ ] Update cloudflare worker
- [ ] Install n8n
- [x] Get Ansible cleaned up with `ranger` and maybe download my `monorepo` git repo? ✅ 2023-07-26

### Network Setup

TODO

I'm using https://nextdns.io/ for my DNS server and for AD blocking

TODO: How I use N8N to easily update my public IP. It literally took under a minute.

### Domains

https://noco.loonison.com
Used to host [[Noco DB]] along with its forms


### Design Decisions

> Why aren't you using Kubernetes?

I have before. Even with Argo CD. It was too much of a headache from a management perspective and a port forwarding perspective. Trying to **KISS**, so docker it is, easy peasy.

> Queries

I'm using Next.js and various small node apps to show data or generate markdown showing data

> Mutations

I'm using obsidian and `lkat` API to make changes to data or create files. This is done here so I don't need to worry about authentication on the website and I can stay in one app. Just trying to consolidate things. One could say that would be a website... Well it is really easy in my current workflow to pull down in Obsidian and invoke an action compared to using a website.