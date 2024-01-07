---
title: Windmill and Neon Postgres
date: 2024-01-07
tags:
  - windmilldev
  - neonpostgres
---
### Goal
I want to scan a little RFID tag with my phone and a row is created in Postgres.

### Technologies
- #homeassistant for phone RFID scanning to HTTP workflow
- #windmilldev as the authorized REST endpoint that talks to Postgres
- #neonpostgres as Postgres provider

### Issue
I noticed a weird error:
`# prepared statement \"s7\" already exists`
On every **other** request to the API...

### Resolution
This GitHub [issue](https://github.com/prisma/prisma/issues/11643) was exactly it. I needed to use the non-pooler Neon connection URL. Once I changed to the different URL I was good to go.