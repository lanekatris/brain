Will have visibility by utilizing [[Viewing Job Queue in Obsidian]]

### Needed Because
- Be an interface to obsidian's file system
- Supporting [[Inbox Project in Obsidian]]
- Supports offline (where personal machine is turned off)
- Supports **obsidian mobile** sending off invocations (since it can't call an api directly since the host PC isn't running)

### Possible Solutions
- Use SQS
- Use Postgres
- Could check if files exist in S3 and pull them (cloudflared exposes this api potentially to be called from the cloud)
- n8n
- I'm using hosted postgres, why don't I use it for rabbitmq?
- ~~Pubnub - Won't work as it doesn't really let messages sit around, it's not designed for that~~
- Raindrop

### Use Cases
- [x] From mobile we can ✅ 2023-07-28

### To Do
- [ ] Install n8n on server I guess with docker [[Home Lab and Architecture]]
- [x] Put in raindrop ✅ 2023-07-28
- [x] n8n pulls, writes, clears raindrop ✅ 2023-07-28
- [x] [[Inbox Project in Obsidian]] ✅ 2023-07-28
- [ ] How to handle those auth keys on mobile?
- [ ] sleepy time from mobile isn't working, change the name to invoke too