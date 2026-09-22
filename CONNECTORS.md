# Connectors

## How tool references work

Plugin files use `~~category` as a placeholder for whatever tool the user connects in that category. For example, `~~ATS` might mean Ashby, Workable, Greenhouse, or any other ATS with an MCP server.

Plugins are **tool-agnostic** — they describe workflows in terms of categories (ATS, meeting transcripts, cloud storage, etc.) rather than specific products. The `.mcp.json` pre-configures specific MCP servers, but any MCP server in that category works.

Only **Team Theory** is required. Every other category is optional: a workflow uses whatever is connected and skips the rest.

## Connectors for this plugin

| Category | Placeholder | Included servers | Other options |
|----------|-------------|-----------------|---------------|
| Team Theory (required) | `~~Team Theory` | Team Theory | — |
| Meeting transcripts | `~~meeting transcripts` | Granola, Metaview, BrightHire | Fireflies, Otter, Zoom, Gong |
| Cloud storage | `~~cloud storage` | Google Drive, Box | Egnyte, SharePoint / OneDrive, Dropbox |
| Knowledge base | `~~knowledge base` | Notion | Confluence, Coda |
| ATS | `~~ATS` | Ashby, Workable | Greenhouse, Lever, Workday Recruiting, SmartRecruiters |
| Chat | `~~chat` | — | Slack, Microsoft Teams |

## What each category is used for

| Placeholder | `/teamtheory:target` | `/teamtheory:interview-plan` |
|-------------|-----------|-------------------|
| `~~Team Theory` | Scorecard methodology (`search_methodology_knowledge`), the org's prior scorecards (`search_portfolio_knowledge`), and the scorecard itself (`generate_document`) | Clustering, question-bank and validation methodology (`search_methodology_knowledge`), and the final plan (`generate_document`) |
| `~~meeting transcripts` | Pull the intake call with the hiring manager or investor | Pull the intake call for company context and emphasis |
| `~~cloud storage` | Pull the job description or role brief; save the scorecard | Pull the scorecard; save the plan |
| `~~knowledge base` | Pull role or company notes; save the scorecard | Pull the scorecard; save the plan |
| `~~ATS` | Pull the job posting; attach the scorecard to the job | Push one interview (kit / stage) per cluster, with questions and scorecard attributes |
| `~~chat` | Share the scorecard with the hiring team | Share the plan with the interview panel |

Nothing is pushed, posted or shared without the user's explicit yes and a named destination.
