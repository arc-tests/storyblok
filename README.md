# Local Volunteering page: Storyblok + Astro demo

A small demo answering a developer’s question: how fast can you get something real working with Storyblok, and does it play nicely with AI tools? Built with Astro, Storyblok and Storyblok’s MCP server.

The Astro components are in this repo, but the block definitions and page content live in my Storyblok space. With your own space and token, you won’t see this demo’s content unless you recreate the blocks and pages there. I can demo it live.

## What's in it

- Current blocks: `page`, `teaser`, `grid`, `feature`, `banner` and `button`. `banner` and `button` are new and `feature` gained a nested `button`.
- A Home page and three sample pages (`/volunteer`, `/get-help`, `/events`), linked from the homepage features. Content created through the MCP (see AI.md).
- Current nesting: `page → grid → feature → button` and `page → banner → button`.
- Visual Editor preview works and edits show after saving.

## Run it locally

1. Clone this repo.
2. Ensure you have Node 22.23.4+. If you're a mise user, `mise.toml` covers this in this project only. For nvm users do `nvm install 24 && nvm use 24`, otherwise install from nodejs.org.
3. Run `npm install`.
4. Create a `.env` file and copy the same structure as `.env.example`. 
5. Fill in `STORYBLOK_DELIVERY_API_TOKEN` with your space's **preview** token (found in `Settings → Access Tokens`) and `STORYBLOK_REGION` with your space's region (e.g. `eu`).
6. Run `npm run dev`. You may be asked for your machine's password to create a local HTTPS certificate, which the Visual Editor needs.
7. Check the output for final URL where the website runs locally. Most times it will be `https://localhost:4321`.

## Connect the Visual Editor

To render a preview of the local project in the Visual Editor, follow these steps:

1. In your space, navigate to **Settings > Visual Editor**.
2. Set the default environment to `https://localhost:4321/`.
3. Save.
4. Open the `home` story.
5. Click **Config**.
6. Type `/` in the **Real path**.

Note: This has been adapted from the starter's README. In my case, `storyblok create` set the preview URL automatically, so I didn’t need these steps. Due to time, I haven’t tested this step.

## Changes from the starter

The stylesheet was replaced with `global.css` which was generated with AI following a suggested colour palette. I have also changed some markup of the blocks to use semantic markup. This is mentioned in `AI.md`.

## What I'd do next
* Commit the block schema to the repo, so others can recreate the space.
* Test whether button links follow a renamed page.
* Keyboard and screen-reader testing, which the AI said it hadn’t done.
* Add a description field to the feature block, so the name stays a short heading and the long sentences move into the description.
* Include a navigation so that we can have a "back to home" link.

---

Roughly 2 hours of focused work, with some interruptions. Creating a separate GitHub account and SSH setup aren’t included.

Built from [Storyblok's official Quickstart using Astro](https://www.storyblok.com/technologies).





