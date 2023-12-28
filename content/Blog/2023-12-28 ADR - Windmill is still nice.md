---
tags:
  - adr
title: Windmill.dev is still a pleasure to work with
date: 2023-12-28
---
I recently wanted to get an email to remind me to take any notes about my climbing session.

I usually go indoor bouldering on Tuesday. 

I saw where you can [share](https://www.windmill.dev/docs/advanced/sharing_common_logic#deno-or-bun-relative-imports-for-sharing-common-logic) functions/logic, this is perfect for sending email.

So it is simple as this:
```
import {main as emailMe} from '/f/shared_v1/email_me.ts'

export async function main() {
	await emailMe("Climb Debrief", "You should jot down any climbing notes you may have.")
}
```

And set a schedule for Tuesdays at 9pm and I'm good to go 🎉

![[Pasted image 20231228090430.png]]

**Side Note**
I've been messing with Temporal, I could have done it there. I would need to build and copy my worker though. Since I don't have any need for *any local resource* on my dev machine I can run it in the cloud! It's so easy...