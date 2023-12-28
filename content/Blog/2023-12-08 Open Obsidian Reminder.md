---
title: Open Obsidian Reminder Email
date: 2023-12-08
---
# TLDR
1) Using Pulumi I schedule a cloud function at 7AM
2) This cloud function sends an email to open Obsidian
3) The contents of the email points to my website which has a deep "a href" link
4) I click that and it opens obsidian! 

> It is a few clicks I know, but hey, I'm reminded 🤷

[Web page](https://www.lanekatris.com/obsidian-links) with deep links

# Process
So, I wanted to set a reminder to open Obsidian since I use it for my reminders, to-do tasks, and brain dumps. Sometimes, I forget, especially during vacations or when I'm deeply focused at work. I might overlook opening it, and occasionally, I have time-sensitive tasks. My idea was to send an email at 7:00 AM, which is before or when I usually wake up, with a deep link to Obsidian. This is somewhat similar to my 8:00 PM reminder to log any outdoor activities. The purpose of this is to remind me to open the app.

I noticed that AWS SNS doesn't handle HTML... at all, and I don't want to deal with domains with AWS SES. Then, I remembered that Charm Bracelet has a "pop" command that makes sending emails super easy. They use Resend, so I signed up for it, and it was a quick process. I thought I would implement it in my cloud function. During our first deployment, things didn't go smoothly, and I encountered the error "Headers is not defined."

A quick search revealed that there's no fetch in this runtime. I looked up recent documentation, and it seems they use a raw HTTP request using fetch, so I'll go with that.

I really dislike dealing with fetch issues; it's frustrating. So, I'm switching to Axios because Axios always works... every time.

Now, the HTML "a" isn't getting rendered. Apparently, you can't put custom protocol links in emails, which makes sense from a security perspective. However, it's a bit of a pain, and now I need a middleman, perhaps my loonison.com or in markdown on lanekatris.com. It's a barrier of entry, dealing with this brain thing, as I can't easily preview my script copies, which I then upload via Git.

It wasn't that bad adding something to my brain. I quickly added it to Obsidian, ran the scripts, opened a new prompt, changed the directory, and ran the script. The build was pretty quick using Hugo, under 2 minutes. I had to think about where the script was, but this is beside the point. The issue is how I invoke updating the cloud brain. I also have to update the email to point to this new redirector on my site. Let's see what happens.

I finally figured out how to run a function via the AWS CLI, and that is pretty nice. Not having to go to the UI just feels better.

And things work!
# Tab Dump
* [Obsidian URI - Obsidian Help](https://help.obsidian.md/Concepts/Obsidian+URI)
* [find vault id obsdiainmd - Google Search](https://www.google.com/search?q=find+vault+id+obsdiainmd&rlz=1C1GCEA_enUS928US928&oq=find+vault+id+obsdiainmd&gs_lcrp=EgZjaHJvbWUyBggAEEUYOTIGCAEQRRhA0gEINDA0N2owajeoAgCwAgA&sourceid=chrome&ie=UTF-8)
* [Scheduling Serverless | Pulumi Blog](https://www.pulumi.com/blog/scheduling-serverless/)
* [utc to eastern time - Google Search](https://www.google.com/search?q=utc+to+eastern+time&rlz=1C1GCEA_enUS928US928&oq=utc+to+easter&gs_lcrp=EgZjaHJvbWUqBwgAEAAYgAQyBwgAEAAYgAQyBggBEEUYOTIHCAIQABiABDIHCAMQABiABDIHCAQQABiABDIHCAUQABiABDIHCAYQABiABDIHCAcQABiABDIHCAgQABiABDIHCAkQABiABNIBCDIxMDVqMGo3qAIAsAIA&sourceid=chrome&ie=UTF-8)
* [amazon sns - Sending html content in AWS SNS(Simple Notification Service) emails notifications - Stack Overflow](https://stackoverflow.com/questions/32241928/sending-html-content-in-aws-snssimple-notification-service-emails-notification)
* [Configuring AWS SES with Pulumi. Complete example on how to use Pulumi… | by Mauro | Medium](https://whattodevnow.medium.com/configuring-aws-ses-with-pulumi-4b25e2a9e230)
* [AWS Lambda - Resend](https://resend.com/docs/send-with-aws-lambda)
* [reactjs - 'ReferenceError: Headers is not defined' when using Headers in a server side rendered react project - Stack Overflow](https://stackoverflow.com/questions/57186018/referenceerror-headers-is-not-defined-when-using-headers-in-a-server-side-ren)
* [examples/testing-unit-ts/ec2tests.ts at 74db62a03d013c2854d2cf933c074ea0a3bbf69d · pulumi/examples](https://github.com/pulumi/examples/blob/74db62a03d013c2854d2cf933c074ea0a3bbf69d/testing-unit-ts/ec2tests.ts)
* [javascript - require('node-fetch') gives ERR\_REQUIRE\_ESM - Stack Overflow](https://stackoverflow.com/questions/69087292/requirenode-fetch-gives-err-require-esm)
* [invoke lambda cli - Google Search](https://www.google.com/search?q=invoke+lambda+cli&rlz=1C1GCEA_enUS928US928&oq=invoke+lambda+cli&gs_lcrp=EgZjaHJvbWUyBggAEEUYOTIICAEQABgWGB4yCAgCEAAYFhgeMggIAxAAGBYYHjIICAQQABgWGB4yCAgFEAAYFhgeMggIBhAAGBYYHjIICAcQABgWGB4yCAgIEAAYFhgeMggICRAAGBYYHtIBCDI4NjJqMGo3qAIAsAIA&sourceid=chrome&ie=UTF-8)
* [node-fetch/node-fetch at 2.x](https://github.com/node-fetch/node-fetch/tree/2.x#readme)