Project: [[Inbox Project in Obsidian]]

 I really like raindrop.io for bookmarks but I didn't want to use it for "read later". I also didn't want to use Chrome. I was OK with a non-mobile solution at the moment. 
 
 So I decided to add to my lkat api a REST endpoint that takes a URL and creates a file in the root of my Obsidian vault. The root of my vault signifies things that need cleaned up; or simply an "inbox". This way, once I'm done reading something I can just delete the file. I don't care about history of it. I also don't have to worry about syncing with a 3rd party  when I've read something or cleaning up a database.

 Who calls this API? A basic chrome extension. So with 2 clicks it adds the current tab to my Obsidian vault. Remember: KISS.
