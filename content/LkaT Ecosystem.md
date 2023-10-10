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

**Data:**
- Postgres - https://neon.tech/

Miscellaneous:
- [[Projects]]
- climb.rest
- [[Disc Golf Course Map Overlay]]

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


