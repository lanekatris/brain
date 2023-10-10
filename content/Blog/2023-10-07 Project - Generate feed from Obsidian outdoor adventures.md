# Background 

Currently, at https://loonison.com/, I have my feed. 

This is what I envision as an aggregate from various sources. I just like the single pane of glass to see activity. It can help remind me of what I've done, and if I want to reference something I can browse over it quickly. 

Having a feed also gives a bit of *temporal context*. I can see that I listened to a podcast on Tuesday and also see I went to the climbing gym. I know that I'll usually see a podcast around this time or near a climbing session because I have a 45 minute drive there and listen to music or podcasts along the way.

It is super basic right now:

![[Pasted image 20231007144058.png]]

I **don't** want to worry about historical data. I tried to import activity ([[Google Location Parsing Project]]) from my Google History but I'm not sure if that juice is worth the squeeze. 

Somewhat related; what I think is quite successful was this project: [[2023-09-13 New Project - Search Google location history from Takeout archive]]. Being able to know if I've been somewhere is something that happens somewhat often, and this solves it quite well in my opinion. 

I do want a way to know when I visited somewhere, or how many times I've been there. Since I take unique places my location history project doesn't have this level of granularity. This will be a different project, hopefully won't take too long to add or build.

# Overview

> I want to sync the adventures I record as files in Obsidian to my feed in Postgres.

I want to automate this but for now here are some directions to remind me:
#### Directions

1) Copy files to S3 bucket:
`aws s3 sync --delete C:\Users\looni\OneDrive\Documents\vault1 s3://lkat/obsidian-vault`

2) Verify files were copied to bucket:
`aws s3 ls --summarize --human-readable --recursive s3://lkat/obsidian-vault`

For this project, these are really the files to verify are copied:
`aws s3 ls lkat/obsidian-vault/Adventures --recursive --human-readable`

3) Kick off a new Kestra sync to take the files from S3 and insert records into Postgres and then copy those to the feed:
http://server1.local:8090/ui/executions/dev/feedGenerateFromObsidianAdventures/1pWW2pksvyReQL3soT3kxe

4) If changes aren't visible kick off a Netlify build. I'm still not sure on the magic it is doing on caching or if the page is treated as dynamic or not:
https://app.netlify.com/sites/mellow-sunburst-a1d9d3/deploys