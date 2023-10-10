I've already forgotten as this happened a day or two ago. I wanted to switch my domain loonison.com to a new Netlify app. The domain is on GoDaddy and the nameservers were pointing to Cloudflare. I thought that was weird. So I just changed them to Netlify. Now all my cloudflare DNS routes quit working. This makes sense. I don't know how the old Netlify site was resolving though... I assume there was a setting in cloudflare pointing it to the Netlify auto-generated URL. 

So this pushed me to just let that domain be for my utility web app and I'll use my other domain lkat.io ([[2023-09-05 Purchased New Domains - lkat.io and troykatris.com]]) to forward things on my private network until it becomes a formalized hobby project.

### Navigating Cloudflare Dashboard
I found where the mysterious DNS link to my tunnel was. It took me quite a while to find it... but probably user error compared to.

I think I should not care about Zero trust Applications, I should just care about the tunnels and their associated Routes. You get there by:
1. On the left click Access
2. Click Tunnels
3. Click your tunnel and then Configure
4. Click the "Public Hostname" tab

![[Pasted image 20230905160551.png]]