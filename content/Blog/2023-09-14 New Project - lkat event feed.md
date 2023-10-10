---
tags:
  - project
status: done
---
# Why?

I want to review the things I've done, with a focus of outdoorsy type things. *Adventures*. I want to essentially consolidate the things that I do from different sources. Udisc is the best for keeping track of disc golf rounds and Mountain Project is a de facto climbing app with a tick list. 

In my effort to keep things simple, I think its best to use the best easiest tool to record your data for the specific activity. Unless I can rewrite it easily in Obsidian... but that is unlikely. It's important that these tools **give you access** to your data.

I needed to choose a small amount of scope, so the smallest dataset I have is my tick list (unfortunately). So I'll go with that.

# How?

**Getting the Data**
Mountain Project allows a tick list download as CSV via a web request, which is great. 

**Running the sync automatically**
When I finished up [[2023-09-13 New Project - Search Google location history from Takeout archive]] I set up Kestra which is a data orchestration framework. This isn't exactly necessary, but I like the single pain of glass it gives, compared to cloud functions running at a set interval (I think this is a pain to monitor).

**Target**
Postgres on Neon.tech is my database of choice so I'll put it there.

**Keeping in Mind**
I'm debating if I want [[Noco DB]] to be able to edit values... sometimes I imagine I'll want a way to manually edit or add data. Not sure on this.

# To Dos

- [x] Create DDL in Kestra to create staging table ✅ 2023-09-15
- [x] Load csv data into table ✅ 2023-09-15
- [x] Create or verify feed schema (nocodb) ✅ 2023-09-15
- [x] Load data from staging table to feed schema ✅ 2023-09-15
- [x] Show feed via nextjs with icon for climbing ✅ 2023-09-15

# After Thoughts

My feed query doesn't support other types, and my types are willy nilly coming from SQL. But man, you can query and hack so quickly with server components. 

I was also pleased to learn that Kestra flows can be triggered by others: [[2023-09-13 New Project - Search Google location history from Takeout archive]].

So with that ^^, I'll probably refactor things to break them up a bit. Ideally, something like Dagster: where I have a flow serve up a data item of some sort, and then other flows listen and do work. An example would be load a CSV into a table, then another flow syncs between tables, that way they aren't coupled and they do less in each flow.