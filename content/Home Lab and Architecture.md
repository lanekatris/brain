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