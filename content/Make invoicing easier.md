- [x] Test that kestra can send emails via SNS (Yes it can send after I gave IAM permissions) ✅ 2023-12-01
- [x] Get token ✅ 2023-12-01
- [x] Find last month's start and end date ✅ 2023-12-02
- [x] Export to pdf ✅ 2023-12-01
- [x] Send email with download link ✅ 2023-12-01
- [x] Create markdown invoice manually or automatically (I'll go with manually via Obsidian.md) ✅ 2023-12-02
- [x] Stupid Kestra, just use node and create the body to a file ✅ 2023-12-02

Mac daddy URL for pdf export: `https://api.track.toggl.com/reports/api/v3/workspace/2052847/summary/time_entries.pdf`


**Ideas**
1. I could have kestra do this every first of month and makes an easy downloadable pdf (could use kestra output state) and sends an email to tell me to handle it
2. I could have my golang cli do this



#### Findings

##### 2023-12-02
**Kestra**
I got furthest along with kestra. It wasn't that bad. I enjoy they already have a building block to download a file and to send a SNS email. The documentation wasn't the best which was the first bad part but I foudn another blueprint. So its lack of documentation shows its face but it's not terrible. 

My issue was finding last months start and end dates. What language to use? I literally just want some dates. So the meh documentation I saw with date functions but no good way to get this. When I ran Node code I could get the dates but I didn't know how to expose the variables because the docs about exposing were deprecated. I then gave up and thought this would be a good use case for windmill.

I will say the ease of use to expose downloaded files (from the files storage from an execution) is very useful. I imagine in Windmill all this has to be manually wired up. 

I finally go things working, it was a series of multiple documentation kestra pages to guide me along. I eventually created a file in the output director, then I do a `read` of that file in the next step and pass that along to the request handler. This is a good example of how working with YAML goes... you start interpolating and it is semi-simple, but it could blow up for more complex examples. It also shows that it is NOT possible (from what I found) to find last month's start and end date. So YAML is good for certain things and not so well for other simple use cases.

The new abstraction with Kestra with "scripts" that can be created in the "editor" which can be consumed in "flows" is very similar to Windmill and allows sharing between flows so somewhat DRYing things up.

**Windmill**
I haven't even gotten the file downloaded yet. I do enjoy the UX in it though. Although, I haven't been able to make good progress. It is defiantly more code oriented and orchestrating code, I want that sometimes but first I want building blocks.

**N8N**
I think about comparing and contrasting with n8n but it has been a while since I've used it. So i'm not sure what it excels at, but it does have a ton of integrations that are similar to kestra that are pretty nice to use.