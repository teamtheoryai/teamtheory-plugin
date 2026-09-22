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

The plugin connects the Team Theory MCP server (`https://mcp.teamtheory.ai/mcp`); sign in with your Team Theory account when prompted.

## Optional connectors

The workflows use whichever of these are connected, and skip the rest:

- **Documents:** Egnyte, SharePoint / OneDrive, Google Drive, Dropbox
- **Intake-call transcripts:** Metaview, Granola
- **Destinations / ATS:** Ashby, Greenhouse, Lever, Notion, Slack, and the document tools above

Nothing is pushed, posted or shared without your explicit yes.

## Layout

```
.claude-plugin/plugin.json        plugin manifest
.claude-plugin/marketplace.json   lets this repo be added as a marketplace
.mcp.json                         Team Theory MCP server
skills/target/SKILL.md            /target
skills/interview-plan/SKILL.md    /interview-plan
```
