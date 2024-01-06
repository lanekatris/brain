[Docker Hub for LK](https://hub.docker.com/repository/docker/loonison101/lk/tags?page=1&ordering=last_updated)

[[Recommender and trip planning for things to do]]
[[Climbing]]
[[Disc Golf Projects]]
[[Fitness Software and Projects]]
Travel - State park visited completion
I expose google history dataset
I expose state park dataset (probably want a simple dataset folder to house these things and you can choose what to load...)
Logging climbs - [[Climb Logger V3]]
(recording) climbs
searching where you've been with google history
infrastructure - tailscale or cloudflare tunnels [[2023-09-06 Cloudflare Zero Trust Tunnel Setup]]

I'm going to need calendar integration :/ 

as part of the location recommending - external things you need to do: turn on google takeout every 2 montsh for one year, then schedule a calendar thing to make a reminder for you https://takeout.google.com/settings/takeout 
calendar integration: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.googlecalendar/

fitness second brain - use a standing desk to force or limit your time on computers

Obsidian for:
- Note taking
- Digital Garden
- Blog

Main executables that wire up smaller utilities/projects:
- lkat (server)
- lk (client cli)

Potentially:
- [[Noco DB]]
- n8n
- [[Home Lab and Architecture]]
- Invoicing
- Climb recording
- IOT - Aquarium
- Raindrop.io
- Pluggable architecture
- gamification
- fitness goals

**Data:**
- Postgres - https://neon.tech/
- Kestra

Miscellaneous:
- [[Projects]]
- climb.rest
- [[Disc Golf Course Map Overlay]]
- [[2023-12-08 Open Obsidian Reminder]]

Charts
- Kibana
- Apache blah blah taht is like tableau

Considerations
1. Cloud needs to talk to your API publically or it talks to a shared resource like a db or a queue
2. Auth is needed in cloud or via cloud flare for private HIPAA things
#### Goals

> I'd like to be multi-tenant so I can start it for my son Troy (we could compare data and it would be good to see other's data)



#### Design Decisions

> Why create a server that Obsidian needs to call when you could create a macro or full fledged Obsidian extension?

**A few reasons**
- Keep obsidian macro/client super lightweight
- Ability to write code in any language by being an external web server
- Ability to consolidate a lot of utilities and functionality in `lkat` where as doing this in an obsidian extension wouldn't support this use case

> Why neon.tech and why Postgres?

I've iterated on this way too much, wasting my time and just abandoning things. I've tried Dynamo, Mongo, EventStore DB, etc. 

Postgres is just a swiss army knife, and supports unstructured data along with all the query support I need. I don't want to worry about backing up things so I'm using the cloud. This is free!

N8n, [[Noco DB]] can all talk to Postgres easily as well. So a way to make my projects and integrations **easy**.

I want to model off of how temporal and cobra cli host their product (grpc, golang, etc.)

# UI s
- Next JS
- Obsidian
- [[Noco DB]]
- CLI (LK)


# Built With
- [Joy UI](https://mui.com/joy-ui/getting-started/) by MUI

# LK

**2023-11-26**
- You need all caps when doing environment variables for viper to pick them up, oops I forgot. [Recommended Dockerfile](https://docs.docker.com/language/golang/build-images/)
- I recently allowed config file and env vars with [this](https://dev.to/techschoolguru/load-config-from-file-environment-variables-in-golang-with-viper-2j2d) and [this](https://articles.wesionary.team/environment-variable-configuration-in-your-golang-project-using-viper-4e8289ef664d)




# To Dos
- [ ] Destroy current pulumi stack under `software/infrastructure` and create a new `lkat` and pulumi/infrastrucutre folder to make things like... idk, resend api key or kestra IAM for S3?
- [ ] Need sql migrations
- [ ] Need pulumi to create at least SNS topic


> It's ok to have software that runs on your computer, like a file watcher that will upload to a server and notify you of the link... its ok!! some thingsa are cloud, some things run local, its ok...!