---
title: Hosting my second brain
date: 2023-10-09
---
I started off with wanting to do a blog. Then I got inspiration from TODO's website and see the blog and second brain so I want to do both but i'll sart with PKM and see how it goes. 

# To Do

- [x] Move quartz to ~~monorepo~~ to `brain` repo ✅ 2023-10-09
- [x] Make name change ✅ 2023-10-11
- [x] Make lanekatris.com use quartz ✅ 2023-10-26
- [ ] Setup RSS with domain and 1000
- [ ] Change Frontmatter of all posts
- [ ] Migrate blog from deleted github to this new place


https://app.netlify.com/sites/steady-yeot-35aa96/overview

## Nice to haves

- [ ] https://steady-yeot-35aa96.netlify.app/tags/ a link to this
# Log

**2023-10-09**
I've been gaming of late with the colder rainy fall weather so I'm on windows. I had to upgrade Node.js.

So locally things look great. I definately want to make tweaks to the layout but that is for another day. 

Since I want to keep everything in Obsidian to author and link, I think I will copy over to the `Content` folder in Quartz. 

I don't have crazy secret things in my vault but there are sensitive finances and other personal items. So, I keep everything in a `Public` folder in my vault that I want to expose. I used this folder when I was using [Obsidian Publish](https://obsidian.md/publish). 

I'll just do the same, hopefully it's easy 😉 copy from `Public` -> `Content`. 

> [!info] Image Sizing / Compression
> I don't see natively a way that Quartz processes images. I think this is a battle for another day. I've always had this problem with the million frameworks I've tried. I suppose all but Medium.com or WriteFreely.com or Gatsby handled this for you.

I see where Netlify deprecated their Asset optimization: https://www.netlify.com/blog/2021/12/21/optimize-your-sites-with-post-processing-on-netlify/

I intentionally chose to fork the Quartz repo so I could get updates. I tried a Git Submodule but it seemed dirty.

 I wonder if Astro handles images out of the box? (yes it does)

I even looked up the Quartz Community Discord for image processing to no avail.

**2023-10-26**
(I will put images in ImageKit, I don't want to deal with other solutions)
(There may be a cool integration to auto expose my s3 to ImageKit)

- [ ] asdf

I need to do the following steps:
#### 1. ✅ Upload obsidian files to S3

This can be done with aws sync cli or a plugin to write to s3

#### 2. Commit files and push



3. (Netlify automatically gets kicked off and deploys the site)



2023-10-27

Ok, it's too much of a pain dealing with Kestra and github actions.

So I'll just run a copy script and upload to s3 manually and call it a day

**To Dos**
- [x] Copy files from obsidian/public folder to git ✅ 2023-10-27
- [x] git commit && git push ✅ 2023-10-27
- [x] script or program to make this easier ✅ 2023-10-27

(Just remember to keep images in imagekit and I think we are gravy 🤷)