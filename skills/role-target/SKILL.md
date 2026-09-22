---
name: role-target
description: Create a role target (Team Theory scorecard) — Mission, Outcomes, Competencies — from a job description, intake-call transcript, or whatever role context the user has. Use when the user runs /team-theory:target, says "create a target", "build a scorecard", "define the role", or shares a JD / intake call and wants the role defined.
user-invocable: false
---

# Role target (scorecard)

> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](../../CONNECTORS.md).

A **target** is a Team Theory scorecard: the role's mission, the outcomes (key results) the hire must deliver, and the competencies that predict delivering them. Team Theory generates the final document — never write the scorecard yourself.

Tool names below are the Team Theory MCP tools (`search_methodology_knowledge`, `generate_document`, `get_custom_instructions`, `search_portfolio_knowledge`). Your client may prefix them (e.g. `mcp__team-theory__…`). If the Team Theory tools are not available, stop and tell the user to connect the Team Theory MCP server (`https://app.teamtheory.ai/mcp`).

## Step 0 — Preferences

Call `get_custom_instructions` and honor any preferences it returns (tone, language, formatting) in every later step and in the `context` you pass to `generate_document`.

## Step 1 — Gather role context (only if the user pointed to it)

If the user named or attached a job description, role brief, or intake call — in the request or the conversation — retrieve it from whichever connected tools are available:

- **Documents** (JD, role brief, org chart, board memo): `~~cloud storage`, `~~knowledge base`, or the job posting in `~~ATS`.
- **Intake-call transcripts** (hiring manager / investor intake): `~~meeting transcripts`.
- **The org's own library**: `search_portfolio_knowledge` for prior scorecards or JDs for the same company or role.

Rules:
- Only search sources that are actually connected. Don't list or apologize for the ones that aren't.
- If the user gave no pointer and nothing is attached, ask once: role title, company, and whether there's a JD or intake call to pull from. If they have none, proceed with what they tell you.
- If a search returns several candidates (e.g. three intake calls for "CFO"), confirm the right one with the user before using it.
- Distill what you retrieve into a tight brief: role, company, stage/ownership (e.g. PE-backed, portco), reporting line, team size, mandate, 12–36 month outcomes, must-haves, known risks, and key quotes from the intake call. Do not forward raw transcripts or whole documents.

## Step 2 — Ground in scorecard methodology

Call `search_methodology_knowledge` for scorecard best practices, specific to the role, e.g.:

- `"scorecard mission outcomes competencies for [role]"`
- `"key results for [role] in a PE-backed [industry] company"` (when relevant)

Pick the 2–5 most relevant excerpts. Summarize any that are long.

## Step 3 — Generate the target

Call `generate_document` with:

- `documentType`: `"scorecard"`
- `context`: the distilled brief from Step 1 plus the user's preferences from Step 0.
- `knowledgeBaseChunks`: the excerpts from Step 2 (and any relevant `search_portfolio_knowledge` excerpts).

Render the returned document exactly as the tool instructs (as a document/artifact, verbatim). Do not paste, summarize, or rewrite it in chat.

## Step 4 — Offer to push it elsewhere

Look at which destinations are connected: `~~cloud storage`, `~~knowledge base`, `~~ATS` (attach to the job), `~~chat`. Offer the connected ones only, in one short question, e.g. "Want me to save this to Google Drive or post it to the #cfo-search Slack channel?"

- Never push, post, or share without an explicit yes and a named destination.
- After pushing, reply with the link or location.
- If nothing suitable is connected, skip this step silently.

## Output format & nuances

<!-- TODO: to be defined. -->
