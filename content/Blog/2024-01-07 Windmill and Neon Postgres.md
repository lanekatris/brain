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

`prepared statement \"s7\" already exists`

On every **other** request to the API...

### Resolution
This GitHub [issue](https://github.com/prisma/prisma/issues/11643) was exactly it. I needed to use the non-pooler Neon connection URL. Once I changed to the different URL I was good to go.

### Random
The dedicated [script type for just Postgres](https://www.windmill.dev/docs/getting_started/scripts_quickstart/sql#postgresql-1) is great, no creating and closing a connection, just give it an input and a connection and your good to go.

If you try to call it via a webhook you have to provide db connection info... that seems odd. So if you do want to have a webhook in front of it you need to use a flow. So you'll call the webhook for the flow and the defaults in your flow will call this Postgres script as expected.