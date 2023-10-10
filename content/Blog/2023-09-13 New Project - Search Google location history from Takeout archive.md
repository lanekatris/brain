---
tags:
  - project
status: done
---
# Why?

I forget some places I've been. I wanted an easy way to search where I've been to know if I've been there.

Since Google location tracking has been running for years, that seems to be the best way to know where I've been.

Google exposes this data via their Takeout service so that's how I can get to the data!

# How?

I started researching some different data orchestration frameworks. I didn't want to write custom code every time. I started down this path here: [[Dagster and thinking on data]].

**So the plan is:**
1. Manual - Kick off Google Takeout
2. Manual - Open email, download zip
3. Kick off - Use Kestra to upload the zip to S3
4. Kick off - Use another Kestra flow to load the zip, parse, and load into Postgres
5. Software - Next.js web app does a `like` statement to search this location history and displays the results
6. Software - Auth0 as I don't want to expose where I've been to the world

**Not in scope:**
- S3 bucket creation via IaC or using Kestra. I'm not quite there yet, I want to re-use what I have, trying to keep things simple.
- IaC for my secrets to talk to AWS

# To Dos

- [x] Create job to upload my google takeout to s3 ✅ 2023-09-13
- [x] Create job to populate postgres from my google takeout ✅ 2023-09-14

# Nice to Haves

- [ ] Reference the zip from the other Kestra flow instead of hardcoding it in a different flow
- [ ] Use secrets in my flows instead of my api keys right then and there
- [ ] Need a way to back up configuration of the apps I'm running in Docker
- [ ] Expose it via cloudflare tunnels securely

# Issues

### Running Docker Compose

For Kestra to spawn runners it needs to be ran as root:
`sudo docker compose -f docker-compose.kestra.yml up`

But I was getting this error:
`Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?`

Weird, I can run it as my user though...

So I did a `sudo systemctl start docker` and now I'm good to go 🤷

# After Thoughts

I was really drawn into Kestra for it's UX 🤷‍♂️ 

I'm not going to break down in details comparing the tools I tried: [[Dagster and thinking on data]].

My main take away from Kestra is it is a glorified SSIS, using modern technologies with python, a great UX, containerized, and a single pane to see executions and logs. These are all really good qualities!

But I'm still having to write python on the side, test it, and paste it into my web IDE in Kestra. So I get the balance, on the fly editing and single pane of glass... 

> [!warning] From what I can tell, you can't reference other flows?

Why does this ^^ matter? I'm wanting to modularize my data, but with Kestra I can only get to what is in the same flow, unless you write to a database or S3 of course. I think Dagster's concept of DAGs is great, or maybe that was introduced with AirFlow, regardless; that level of abstraction is what I'm looking for. 

Plus, I think Dagster has a decent UI. So hopefully moving closer to code and having a nice orchestration engine with UI will meet my needs 🙏

**2023-09-14**

> While Dagster helps run Python functions reliably, the primary goal is to help teams define and build data assets in code.

I noticed the above quote when reading [Dagster vs Prefect](https://dagster.io/vs/dagster-vs-prefect). I think this sums up more of what I want, it's Python though. I want to define assets in code, so I have building blocks and they are first class assets to view and reference for any new projects.


Oh yeah, [this article](https://python.plainenglish.io/airflow-vs-prefect-vs-kestra-what-is-the-best-data-orchestration-platform-in-2023-899d849743cc) helped me realize how to deal with local files in Kestra.

2023-09-15

> [!success] Looks like you can [trigger flows](https://kestra.io/docs/flow-examples/trigger-flow) based off of other flows... their docs are pretty but I don't think it was clear. Regardless, this is a win! 

# Snippets

Before I had Kestra to upload a the zip, I used the AWS cli:

`aws s3 cp takeout-20230703T122719Z-001.zip s3://lkat/google-takeouts/takeout-20230703T122719Z-001.zip`