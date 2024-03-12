---
title: Containerizing a NX.dev NEXT.js app
date: 2024-03-11
---
# Background

I wanted to play around with self hosting my next.js app in my home lab as I wanted to make it act more like a dynamic site compared to static. I want to be able to kick off temporal workflows, and I haven't decided the best way to make these things talk to each other while keeping deployments as easy as possible.

# TLDR

- Add the npm packages to containerize your app, mentioned below
- [Add](https://github.com/lanekatris/monorepo/blob/main/.github/workflows/web-docker.yml) a Github Action
- [Docker compose](https://github.com/lanekatris/monorepo/blob/779db1dc0965400edf0d59ce9d99c913636a4f8d/infrastructure/homelab/docker-compose.yml#L5-L12) to run your app

# Thought Process

> Does Next.js support dockerization, they would have to?

https://nextjs.org/docs/app/building-your-application/deploying#docker-image

> Oh wait, I'm in a NX.dev monorepo, things aren't this simple. How to do it the NX.dev way?

https://dev.to/sebastiandg7/nx-nextjs-docker-the-nx-way-containerizing-our-application-1mi7

> This looks like a lot of work... oh wait, the packages referenced in this article look pretty solid: `@nx-tools/nx-container`, let's look into these docs compared to all these hack changes this article is talking about

https://github.com/gperdomor/nx-tools/blob/main/packages/nx-container/README.md#setting-up-the-container-pluginte

> [!info] Side Quest 1
> I was trying to prevent caching of my discs in Next.js, or at least refresh it more often. I ended up with `export const dynamic = 'force-dynamic` from [here](https://stackoverflow.com/questions/76936730/how-to-disable-the-cache-data-and-update-every-time-client-visit-the-page-in-nex). More docs [here](https://nextjs.org/docs/app/building-your-application/caching)

> And look, they have a section for Github Actions:

https://github.com/gperdomor/nx-tools/blob/main/packages/nx-container/docs/ci/github-actions.md

> I added a GitHub action with a few changes [here](https://github.com/lanekatris/monorepo/blob/main/.github/workflows/web-docker.yml). Don't forget to add secrets if needed and map them via environment variables in the yaml. Also, `INPUT_GITHUB_TOKEN` is required

> [!info] Side Quest 2
> I see my `npm` cache is found and used, although the `npm install` still takes a bit to run, although it still is fast relatively to a real install. Docs [here](https://github.com/actions/setup-node)

> I did need to specify my Docker image tag to correctly match Docker Hub [here](https://github.com/lanekatris/monorepo/blob/main/software/js/packages/web/project.json#L56) and I chose to automatically push to Docker [here](https://github.com/lanekatris/monorepo/blob/main/software/js/packages/web/project.json#L53) 

I can now run the app with a simple docker compose on my server [here](https://github.com/lanekatris/monorepo/blob/779db1dc0965400edf0d59ce9d99c913636a4f8d/infrastructure/homelab/docker-compose.yml#L5-L12)

