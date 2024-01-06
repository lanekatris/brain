---
title: Cloudflare R2 Storage
date: 2023-10-16
---
# Background

I was thinking about the data hosting portion of my vision with the [[LkaT Ecosystem]]. 

As I switched to [[2023-10-16 Blog  Rewrite to Quartz]] life was made easy. I then thought about hosting a CSV file. I can't on Netlify. I'm not sure if this is allowed but it makes sense from their perspective: just hosting web resources for static sties. 

For one project: [[Disc Golf Projects]] I hosted on [Kaggle](https://www.kaggle.com/datasets/lanekatris/pdga-united-states-disc-golf-courses). I want to host first from my perspective. I know R2 is a cloud service but I want to have more control over data assets.

I also have some data files in [GitHub](https://github.com/lanekatris/monorepo/tree/main/data). This worked, but I felt bad even though they are small files.

# Just Do It

So that led me down the object storage path, which is the right thing. I'm hoping to consolidate downloads publically via one place. Also, these may get sizable so no need to abuse Netlify. 

$0 egress cost for R2! So I'll use this instead of S3 and not have to worry about things.

You have to add your credit card, this is not a problem.

> [!info] A caveat I noticed when you make a bucket public is that they don't recommend this for production and it isn't meant for production. I don't foresee any issue here

# To Dos

- [x] Assign custom domain to R2 bucket ✅ 2023-10-16
- [x] Get their CLI: Wrangler setup ✅ 2023-10-16

**Made it**: `storage.lkat.io`

# Upcoming

Now I need to write to R2 programmatically! 