---
tags:
  - project
  - discgolf
status: done
---

# Why?

I want to populate my feed from udisc scorecards.

# How?

# To Dos

- [x] Upload to s3 ✅ 2023-09-16
- [x] download file, turn to json ✅ 2023-09-16
- [x] delete table ✅ 2023-09-16
- [x] create table ✅ 2023-09-16
- [x] load json data ✅ 2023-09-16
- [x] Populate feed ✅ 2023-09-16
- [x] Change how nextjs loads data ✅ 2023-09-16

# After Thoughts

This was insanely easy after the building blocks were in place:
- Example kestra flow
- Example sql to populate the feed
- Example sql to regenerate its part of the feed
- Easy way to upload a CSV
- Next.js already knows its DB connection string, I just changed the sql, changed the Typescript type, and I'm off to the races rendering the data