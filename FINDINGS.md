# Findings from using AI

I recorded these as voice notes while doing the exercise, talking through my confusion with Claude chat as a rubber duck. I then used Claude to pull out the notes that fit this part of the brief. The findings and conclusions are mine.

## The MCP setup steps were in the wrong order

The MCP setup steps were in the wrong order, and the permissions step was unclear.

**Assistant**: using Claude in VS Code, while connecting the MCP.

**Produced**: `run /mcp` as step 1 and `reload` as step 4, with `grant permissions` as a separate step.

**Noticed**: Claude listed `run /mcp` first and `reload` last. But `/mcp` showed an empty list until I reloaded VS Code, because the session started before the server was added. The reload needs to come first.

"Grant only the permissions and spaces this project needs": Claude said this, citing Storyblok's docs. It's sensible advice but confusing for a newcomer. When you're just starting, you don't know what the project needs yet, and in my case the space was created for me by the CLI rather than chosen by me.

It turns out the permissions and the choice of space are on the same screen as the sign-in, which only appears once you start signing in. The steps read like three separate actions when it's really one screen.

**What could have stopped it**: the output should be updated to reflect this order of events. Reload the client after adding the server, and that space and permissions are chosen on the OAuth screen. Perhaps, some [documentation update](https://www.storyblok.com/docs/tooling/mcp-server/setup) could also fix this.

For example (from my voice notes):
1. Reload VS Code (or start a new session) so Claude Code picks up the new server.
2. Run /mcp and select Storyblok.
3. A browser window opens asking you to sign in to Storyblok. On that same screen, you choose which space to connect and which permissions to grant.
4. Run /mcp again and check Storyblok shows as connected.

## It changed my space without a plan or approval 

**Assistant**: the MCP-connected assistant

**Produced**: For the banner prompt it showed no plan at all. For the CTA change, it showed a plan but carried on without waiting for approval. Changes, including schema changes always carried on without need for approval.

**Noticed**: afterwards I asked the session whether I approved anything. Then I checked Storyblok’s own skill file and it says step 5 “Confirm — once”.

**What would have stopped it**: [the guidance already exists in the skill](https://github.com/storyblok/agent-plugin/blob/main/skills/storyblok-model-content/SKILL.md). The AI read it second-hand, through a sub-agent, and didn’t apply it. The starter’s AGENTS.md could state the rule directly (“show a plan and wait for approval before writing through the MCP”). Whether installing the plugin would have enforced it is an open question. 

## Whole sentences went into the feature’s name field 

**Assistant**: the MCP-connected assistant, writing sample content.

**Produced**: `feature` names like “Need a lift to one of our events? Our volunteer drivers can pick you up.” Once I asked for feature titles to render as headings, these became very long `<h2>`s.

**Noticed**: reviewing the rendered HTML for quick accessibility checks.

**What would have stopped it**: the content model itself. The starter’s `feature` block has only a name field, so the AI had nowhere else to put the text, and didn’t flag it. A `description` field, or a hint on the `name` field, a short description or a character limit, might have given the AI and editors the right signal.
