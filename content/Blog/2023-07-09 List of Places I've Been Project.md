I got this working on 2023-07-09 by hacking things together.

![[Pasted image 20230709130830.png]]

# To Do
- [x] I want a list of places (maybe unique) that I've been that I can search against. This doesn't have to be fancy ✅ 2023-07-09

# How To
1. I'm using the [[Google Location Parsing Project]] and I commented out all the excludes
2. Queried SQL Lite with DataGrip: `select distinct name,address from tab1 order by name`
3. Exported the file manually: ![[Pasted image 20230709130309.png]]
4. Copied this file to my Obsidian vault and manually added a "date updated" snippet

> These are all hack/manual fixes but I don't imagine updating this frequently. I can always make this **really** reproducible when I want to spend the time on it.

> OmniSearch searches this out of the box, but unfortunately it only forwards you to the beginning of note instead of actually where it lives at in the file