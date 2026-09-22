---
name: interview-plan
description: Build a Team Theory Divide & Conquer interview plan — split the scorecard's outcomes and competencies into thematic clusters, one per interviewer, with validated behavioral questions and follow-ups for each. Use when the user says "/interview-plan", "divide and conquer", "interview plan", "split the interviews across the panel", or wants interview guides for multiple interviewers from a scorecard or target.
argument-hint: "[role and company, or where to find the scorecard / target]"
---

# /interview-plan — Divide & Conquer interview plan

The user invoked this with: $ARGUMENTS

Divide & Conquer gives each interviewer a distinct slice of the scorecard, so the panel covers every facet once, with no two interviewers asking the same questions. Team Theory generates the final document — never write the plan document yourself.

Tool names below are the Team Theory MCP tools (`search_methodology_knowledge`, `generate_document`, `get_custom_instructions`, `search_portfolio_knowledge`). Your client may prefix them (e.g. `mcp__team-theory__…`). If the Team Theory tools are not available, stop and tell the user to connect the Team Theory MCP server (`https://mcp.teamtheory.ai/mcp`).

Steps 3–5 are working steps: do them in your own reasoning and tell the user only one line per step (e.g. "Creating thematic clusters from the scorecard."). Don't show cluster tables, drafts, or validation notes in chat.

## Step 0 — Preferences

Call `get_custom_instructions` and honor any preferences it returns in every later step and in the `context` you pass to `generate_document`.

## Step 1 — Retrieve the scorecard / target and company context

The plan is built on a scorecard (target). Find it, in this order:

1. **In the conversation** — a target from `/target` or a pasted scorecard.
2. **Where the user pointed** — documents in Egnyte, SharePoint / OneDrive, Google Drive, or Dropbox; intake-call transcripts in Metaview or Granola.
3. **The org's own library** — `search_portfolio_knowledge` for the role's scorecard.

Only search sources that are actually connected. If several candidates come back, confirm the right one with the user. If there is no scorecard anywhere, offer to run `/target` first — a plan without outcomes and competencies to cluster is guesswork.

Distill the scorecard into its facets — each Key Result (R1, R2…) and Competency (CC1, RC1…) with a one-line definition — plus a short company brief (stage, ownership, industry, team, what makes the role hard).

## Step 2 — Ask the setup questions

Ask these in one message, and skip any the user already answered:

1. **How many interviewers** (or interviews) are in the loop?
2. **Candidate experience base** — who is in the pool? (e.g. sitting CFOs vs. strong #2s stepping up; industry insiders vs. adjacent.) This decides how hard the non-incumbent guard bites.
3. **Company terminology** — internal words to use (e.g. "business units", "pods", "portcos").
4. **Facets to emphasize** — anything to weight more heavily or cover twice.

Wait for the answers before continuing.

## Step 3 — Create thematic clusters

Call `search_methodology_knowledge` for the clustering method and themes, e.g.:

- `"divide and conquer interview clustering scorecard facets into interviews"`
- `"interview themes for [role] competencies"`

Apply what it returns. The floor, whatever the search says:

- One cluster per interviewer; 2–4 facets per cluster; sizes roughly balanced.
- Every facet in at least one cluster, none in three or more. Emphasized facets may appear twice.
- Group by natural theme (people and influence, functional depth, strategy and judgment, execution, talent and team-building…). Cluster names are 3 words max.
- Warn the user if there are fewer than 2 interviewers (thin coverage) or more interviewers than half the facet count (too many interviews for too few facets).

## Step 4 — Generate questions for each cluster

Call `search_methodology_knowledge` for question-generation instructions once, then for question-bank examples **once per cluster**, e.g.:

- `"divide and conquer question generation rules behavioral interview"`
- `"[role] [cluster theme] interview questions"` — one per cluster.

Use the bank as inspiration, not templates. Draft 7–10 questions per cluster, each with 2–4 short follow-up bullets. The floor:

- Every question elicits a **story**, and the candidate can't guess the "good" answer from it (side-door framing).
- **≤15 words, one question, no second clause.** Trust the follow-ups.
- **Non-incumbent guard:** never assume they've done the exact thing ("In the most senior role you've held…", not "In your last CEO role…").
- **Never broadcast the scorecard:** no Key Result or Competency named in the question.
- Mix **Event** (positive before negative), **Attribute** (paired; first follow-up asks for an example) and **TORC** (get the first and last name first, then the 1–10 rating and "what would they improve" as follow-ups; place late).
- Use the company's terminology from Step 2; otherwise avoid structural jargon.
- Open each guide with an energizing, rapport-building question.

## Step 5 — Validate the full set

Call `search_methodology_knowledge` for the validation checklist, e.g. `"divide and conquer interview question validation quality redundancy coverage"`. Then review **all** clusters together, with fresh eyes:

- **Quality** — rewrite anything that fails the Step 4 floor.
- **Redundancy** — no two questions, in the same guide or across guides, likely to surface the same story. Merge or replace.
- **Coverage** — every facet is probed by at least one question in its cluster; every guide mixes question types and is sequenced well.

## Step 6 — Generate the final plan

Call `generate_document` with:

- `documentType`: `"dc-validation"` (the Divide & Conquer final-stage document: header, role overview, facet coverage map, one guide per interviewer with questions, follow-ups and a scoring table).
- `context`: the role and company brief, the setup answers from Step 2, the clusters (name, facets, goal), and **every validated question with its follow-ups**, plus the user's preferences. The generator formats what you pass; it should not have to invent questions.
- `knowledgeBaseChunks`: the 2–5 most useful methodology excerpts from Steps 3–5.

Render the returned document exactly as the tool instructs (as a document/artifact, verbatim). Do not paste, summarize, or rewrite it in chat.

## Step 7 — Offer to push to the ATS

Check which ATS or interview tools are connected (e.g. Ashby, Greenhouse, Lever, Workday, Metaview). Offer the connected ones in one short question, e.g. "Want me to add these as interview kits on the CFO job in Ashby, one per interviewer?"

- Never create or change anything in the ATS without an explicit yes and the specific job / interview stage confirmed.
- Map one cluster to one interview (kit / stage), questions and follow-ups included, and the facets as its scorecard attributes where the ATS supports it.
- After pushing, reply with links or locations. If a cluster couldn't be pushed, say which and why.
- If no ATS is connected, offer the other connected destinations (Drive, SharePoint, Notion, Slack…) instead, or skip silently if there are none.
