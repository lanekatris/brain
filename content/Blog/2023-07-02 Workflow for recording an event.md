# Use Case

> I want to easily record when I use the Blackstone grill

# Calendar Steps
1. Create folder in Obsidian: `Events\Blackstone`
2. Install **Full Calendar** community plugin
3. Choose **Full Note**, choose the directory created above, choose a color
4. Hit **save** (easy to forget)

# QuickAdd Steps
1. Type name, choose Template, add choice
2. Click the gear
3. Choose a template (it's required) choose filename format like this: `{{DATE:}} {{name}}` (This is so it prompts you for the name otherwise there isn't a name and that is screwy)
4. Choose the folder you want to create the note in

Your template needs to look like this to show up in the calendar correctly:
(You can name the template whatever)
```
---
title: {{name}}
allDay: true
date: {{date}}
completed: null
---
```

# Pinned Commands
This is for the **Command Palette**

(This is an Obsidian provided plugin)

> These 3 entry points are the most common for my needs

# Why all the trouble?

I have a bad habit of over engineering. I don't want to have to write a SPA, API, authentication for that API, write to database, show results; all to simply capture that I used my grill. 

Making data entry easy is the important part. So I try to make that happen with Obsidian. I can parse these files and sync to a database if I want, but I don't need to worry about that. Hurdle number one is easy data entry.

