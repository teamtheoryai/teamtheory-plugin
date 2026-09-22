---
description: Build a Divide & Conquer interview plan from a scorecard, one thematic cluster per interviewer
argument-hint: "[role and company, or where to find the scorecard / target]"
---

> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](../CONNECTORS.md).

Build a Team Theory Divide & Conquer interview plan for the role described in $ARGUMENTS: the scorecard's outcomes and competencies split into thematic clusters, one per interviewer, each with validated behavioral questions and follow-ups.

Before anything else, orient the user in 1–2 sentences: you'll find the scorecard, ask a few setup questions, cluster the facets, write and validate the questions, generate the plan, then offer to push it to their ATS. Nothing is pushed until they say so.

Then follow the **divide-and-conquer** skill:

1. Load the user's Team Theory preferences (`get_custom_instructions`).
2. Retrieve the scorecard / target and company context — from this conversation, `~~cloud storage`, `~~knowledge base`, `~~ATS`, `~~meeting transcripts`, or `search_portfolio_knowledge`. If there is no scorecard, offer to run `/team-theory:target` first.
3. Ask the setup questions in one message: number of interviewers, candidate experience base, company terminology, facets to emphasize. Wait for the answers.
4. Create thematic clusters, grounded in `search_methodology_knowledge`.
5. Generate questions for each cluster from the methodology question bank (one `search_methodology_knowledge` call per cluster).
6. Validate the full set for quality, redundancy and coverage, grounded in `search_methodology_knowledge`.
7. Generate the final plan with `generate_document` (`documentType: "dc-validation"`) and render it verbatim.
8. Offer to push it to the connected `~~ATS`, one interview per cluster.

Steps 4–6 are working steps: tell the user one line per step, not the drafts. If the Team Theory tools aren't available, stop and tell the user to connect the Team Theory MCP server (`https://app.teamtheory.ai/mcp`).
