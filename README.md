# Team Theory plugin

Hiring workflows for Claude, grounded in Team Theory methodology and your own documents, transcripts and ATS.

| Command | What it does |
|---|---|
| `/target` | Builds a role target (scorecard: mission, outcomes, competencies) from a JD, an intake call, or whatever context you give it, then offers to save it to your connected tools. |
| `/interview-plan` | Builds a Divide & Conquer interview plan from a target: one thematic cluster per interviewer, validated behavioral questions with follow-ups, then offers to push it to your ATS. |

In Claude Code the commands are namespaced: `/teamtheory:target`, `/teamtheory:interview-plan`. Both also trigger from plain requests ("build a scorecard for the CFO role", "split the interviews across four people").

## Install

Claude Code:

```
/plugin marketplace add teamtheoryai/teamtheory-plugin
/plugin install teamtheory@teamtheory
```

The plugin pre-configures the Team Theory MCP server (`https://mcp.teamtheory.ai/mcp`) plus optional connectors; sign in to each when prompted.

## Connectors

Only Team Theory is required. Transcripts (Granola, Metaview, BrightHire), cloud storage (Google Drive, Box), knowledge base (Notion) and ATS (Ashby, Workable) are optional: the workflows use whatever is connected and skip the rest. See [CONNECTORS.md](CONNECTORS.md) for the categories, alternatives, and what each is used for.

Nothing is pushed, posted or shared without your explicit yes.

## Layout

```
.claude-plugin/plugin.json        plugin manifest
.claude-plugin/marketplace.json   lets this repo be added as a marketplace
.mcp.json                         MCP servers (Team Theory + optional connectors)
CONNECTORS.md                     connector categories and ~~placeholders
skills/target/SKILL.md            /target
skills/interview-plan/SKILL.md    /interview-plan
```
