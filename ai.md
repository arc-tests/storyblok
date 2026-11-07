# How I used AI

Tools: Claude Code in VS Code, connected to Storyblok's MCP server.

To connect the MCP, I used the quickstart prompt from Storyblok’s docs, adding ‘Connect to the following Storyblok MCP:’ at the start.

## Prompts that did the most work

### 1. Creating the banner block (using the MCP)

**My prompt**
> Create a new banner block that has an `<h2>`, allows a short paragraph and a call to action button which allows a custom label and url.

**What it did:** 
It read AGENTS.md and went to read Storyblok’s agent skills on GitHub. It didn’t install the plugin. It then listed the space’s existing blocks, created a `banner` block with `headline`, `text`, `cta_label` and `cta_link` fields, wrote `Banner.astro` and registered it in `astro.config.mjs`.

**What I checked:** 
I signed-in on the Storyblok web app and saw the banner in the Block Library. I noticed the CTA was two flat fields rather than a nested block, so my next prompt made it its own button block.

**Verdict:** 
This was my first prompt using the MCP. It changed my Storyblok space without showing me a plan first. Storyblok’s agent skill describes presenting a plan before any changes. Whether a direct request like mine should count as approval is a question I’d like to discuss.

### 2. Adding buttons to the homepage features

**My prompt**
> Update the features in the homepage to each use the new CTA button.

**What it did:** 
It added a cta field to the `feature` block and updated `Feature.astro` to render it. Each button needs a `label` and a `link`, and `Home` was the only page, so it stopped and asked me to choose: create stub pages, use placeholder URLs, or give it labels and URLs myself. I chose stub pages. It created three draft pages, re-read `Home` to make sure nothing had changed, then linked each feature’s button to its page.

**What I checked:** 
I clicked each button on the homepage and checked the three pages loaded. In Storyblok I saw the three new draft stories.

**Verdict:** 
I was pleased it anticipated this, as it was going to be my follow-up. Interestingly, it asked me about content (where links should go) but not about the schema change it had just made. 


### 3. The semantic HTML and theme prompt
**My prompt**
> Update the Astro components so the button, descriptions and nested blocks render using semantic HTML: feature titles as headings (not paragraphs), and the button as a link ensuring accessibility.
> Update the colour theme using the following colour scheme: #2d5972, #733e4a, #b25d62, #e5926b and #f7d5b5. Adjust accordingly to ensure accessibility.

**What it did:** 
It swapped the existing stylesheet (which is loaded from Storyblok's CDN) for a brand new one (`global.css`) so that the new theme lives in the repo. It computed contrast ratios for the palette to decide which colour pairs were safe for text. It took screenshots and tested for light and dark mode. It flagged that two of the suggested colours would fail contrast if used on light backgrounds so it used them only for decorative touches.

It also made changes to the HTML. For example, Grid is now a real list using `<ul>`/`<li>`, the buttons are a plain `<a>` and it uses `<h2>` where it makes sense.

**What I checked:** 
I inspected the rendered HTML. The structure was much better than the starter’s, where each feature was a `<section>` containing only a paragraph. But on the new pages, whole sentences now render as `<h2>`, because the feature block has no description field and the sample content put everything in the name. A full sentence isn’t a good heading for screen-reader users navigating by headings.

**Verdict:** 
I asked for descriptions, but the feature block had no description field. The AI didn’t add one, and its reply didn’t mention it. I was still happy with the styling: the contrast work was thorough.


## What I rewrote by hand, and why

### Content changed by hand
I've done some content changes using the Storyblok Visual Editor to test if editing in Storyblok updates the page. Changes include the Home headline and a feature title.

### Reviewed code
I didn’t rewrite any code by hand. I reviewed the semantic HTML and contrast choices and kept them. When I saw paragraphs instead of- eadings, I fixed by prompting rather than editing.

### What I'd do next
Add a description field to the feature block, so the name stays a short heading and the long sentences move into the description.

Include a navigation and easy "back to home" link.

### Extras done by hand instead of using AI
These are covered in the README.

* Creating the space
* Scaffolding with `storyblok create`
* Fixing the Node version. 

