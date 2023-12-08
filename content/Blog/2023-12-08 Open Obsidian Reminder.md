---
title: Open Obsidian Reminder Email
date: 2023-12-08
---
# TLDR
1) Using Pulumi I schedule a cloud function at 7AM
2) This cloud function sends an email to open Obsidian
3) The contents of the email points to my website which has a deep "a href" link
4) I click that and it opens obsidian! 

> It is a few click I know, but hey, I'm reminded 🤷

# Process
So, I wanted to set a reminder to open Obsidian since I use it for my reminders, to-do tasks, and brain dumps. Sometimes, I forget, especially during vacations or when I'm deeply focused at work. I might overlook opening it, and occasionally, I have time-sensitive tasks. My idea was to send an email at 7:00 AM, which is before or when I usually wake up, with a deep link to Obsidian. This is somewhat similar to my 8:00 PM reminder to log any outdoor activities. The purpose of this is to remind me to open the app.

I noticed that AWS SNS doesn't handle HTML... at all, and I don't want to deal with domains with AWS SES. Then, I remembered that Charm Bracelet has a "pop" command that makes sending emails super easy. They use Resend, so I signed up for it, and it was a quick process. I thought I would implement it in my cloud function. During our first deployment, things didn't go smoothly, and I encountered the error "Headers is not defined."

A quick search revealed that there's no fetch in this runtime. I looked up recent documentation, and it seems they use a raw HTTP request using fetch, so I'll go with that.

I really dislike dealing with fetch issues; it's frustrating. So, I'm switching to Axios because Axios always works... every time.

Now, the HTML "a" isn't getting rendered. Apparently, you can't put custom protocol links in emails, which makes sense from a security perspective. However, it's a bit of a pain, and now I need a middleman, perhaps my loonison.com or in markdown on lanekatris.com. It's a barrier of entry, dealing with this brain thing, as I can't easily preview my script copies, which I then upload via Git.

It wasn't that bad adding something to my brain. I quickly added it to Obsidian, ran the scripts, opened a new prompt, changed the directory, and ran the script. The build was pretty quick using Hugo, under 2 minutes. I had to think about where the script was, but this is beside the point. The issue is how I invoke updating the cloud brain. I also have to update the email to point to this new redirector on my site. Let's see what happens.

I finally figured out how to run a function via the AWS CLI, and that is pretty nice. Not having to go to the UI just feels better.

And things work!