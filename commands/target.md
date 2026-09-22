---
description: Create a role target (Team Theory scorecard) from a JD, intake call, or role context
argument-hint: "[role and company, or where to find the JD / intake call]"
---

> If you see unfamiliar placeholders or need to check which tools are connected, see [CONNECTORS.md](../CONNECTORS.md).

Create a role target — a Team Theory scorecard with the role's mission, outcomes and competencies — for the role described in $ARGUMENTS.

Before anything else, orient the user in 1–2 sentences: you'll pull any job description or intake call they point to, ground the target in Team Theory methodology, generate it, then offer to save it to their connected tools. Nothing is saved or shared until they say so.

Then follow the **role-target** skill:

1. Load the user's Team Theory preferences (`get_custom_instructions`).
2. Retrieve role context the user pointed to — the JD from `~~cloud storage`, `~~knowledge base` or `~~ATS`, the intake call from `~~meeting transcripts`, prior scorecards from `search_portfolio_knowledge`. If $ARGUMENTS is empty and nothing is attached, ask for the role, the company, and whether there's a JD or intake call.
3. Search `search_methodology_knowledge` for scorecard best practices for this role.
4. Generate the target with `generate_document` (`documentType: "scorecard"`) and render it verbatim.
5. Offer to push it to the connected destinations (`~~cloud storage`, `~~knowledge base`, `~~ATS`, `~~chat`).

If the Team Theory tools aren't available, stop and tell the user to connect the Team Theory MCP server (`https://app.teamtheory.ai/mcp`).
