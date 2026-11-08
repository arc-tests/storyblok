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

---

## Tutorial: Add a block to your Astro site with an AI assistant and Storyblok's MCP

This walkthrough takes you from nothing to an Astro site with a new, nested block, built by prompting an AI assistant connected to Storyblok's MCP server.

### Before you start

- A Storyblok account. Signing up first means you only have to log in when prompted later. You don't need to create a space at this point as the CLI creates one for you in step 1.
- Node.js 22.23.4 or newer.
- An editor or assistant that supports MCP. I used VS Code with the Claude Code extension.

### 1. Create the project

In the folder of your choice, install Storyblok's CLI, log in and create the project:

```sh
npm install -g storyblok
storyblok login
storyblok create
```

If you skip `storyblok login`, `create` will offer you to log you in there and then.

Choose Astro, then a path for your project. The CLI scaffolds the project, creates a space for it, fills in your `.env` and preview URL, and opens your new space in the browser. It then shows the next steps: `cd` into your project folder, `npm install` and `npm run dev`. The first run may ask for your computer's password: it's creating a local HTTPS certificate, which the Visual Editor needs.

At `https://localhost:4321` you should see a heading and three cards.

### 2. Connect your assistant to the MCP

Paste the quickstart prompt from Storyblok's MCP docs into your assistant:

> Fetch https://www.storyblok.com/docs/tooling/mcp-server/setup.md and follow the setup instructions for this client.

Once it confirms the server was added:

1. Reload your editor or start a new session, so the assistant picks up the new server.
2. Run `/mcp` and select Storyblok.
3. Sign in to Storyblok in the browser window that opens. On the same screen, choose the space the CLI created and grant permissions. For a simple demo you can tick them all. For real projects, review them.

### 3. Create a block

> Create a new banner block that has an `<h2>`, allows a short paragraph and a call to action button which allows a custom label and url.

The assistant looks at how the starter's blocks are set up, reads Storyblok's agent skills (the starter's `AGENTS.md` points it there), creates the block in your space and writes a matching `Banner.astro` component.

In your space's **Block Library**, on Storyblok's UI in your browser, open the banner. You'll see a headline, text, and a link and link label, all on the same level.

You won't see the banner on your site yet, and that's the key idea: the block's definition lives in Storyblok, its Astro component lives in your code, and nothing renders until a **story** (Storyblok's word for a page) uses it.

### 4. Nest a block

> Make the CTA its own button block so that it is nestable.

The assistant describes what it's about to do, creates a `button` block, and swaps the banner's two link fields for one field that only accepts a button. It first checks whether any story uses the banner, so no content is lost. None does yet.

Refresh the Block Library in your browser. The banner now holds a button, which is block nested inside.

### 5. Put it on a page

First, I gave the starter's three cards (feature blocks) a button each:

> Update the features in the homepage to each use the new CTA button.

Each `button` needs a link, and Home was the only page, so the assistant stopped and asked: create stub pages, use placeholder URLs, or take labels and URLs from me? I chose stub pages, and it created three drafts and linked each card's button to one.

Then I filled those pages:

> Create sample content for the three new pages just created and add to each a banner and a feature with realistic sample content.

Open a new page locally: the banner renders, nested button included.

### 6. Edit it in the Visual Editor

Open the page in Storyblok, change some text and press **Save**. The preview updates once you save, not as you type.






