# Team Theory Plugin

A [Team Theory](https://teamtheory.ai) plugin for Claude Cowork and Claude Code.

Executive hires are made on instinct far more often than anyone admits. The role gets defined in a 30-minute intake call that lives in someone's notes, the job description is a recycled template, and the interview loop is four smart people asking the same "tell me about yourself" questions and comparing gut feels afterwards. The facets that actually predict success in the role get covered twice, or not at all.

Team Theory turns that into a system. This plugin pulls the role context you already have — job descriptions in Google Drive or Box, intake calls in Granola, Metaview or BrightHire, the job in Ashby or Workable — grounds it in Team Theory's hiring methodology, and produces the documents a disciplined search runs on: a role target that defines what success looks like, and an interview plan that splits the target across the panel so every facet is tested once, well.

## Features

### 1. Role Target
Defines the role before anyone meets a candidate. Pulls the job description or intake-call transcript you point to, searches Team Theory's methodology for scorecard best practices, and generates a target: the role's mission, the outcomes the hire must deliver, and the competencies that predict delivering them. Then offers to save it wherever your team works.

**Slash Command:** `/team-theory:target`

```
/team-theory:target
/team-theory:target CFO for a PE-backed industrial services company, intake call in Granola from Tuesday
```

### 2. Divide & Conquer Interview Plan
Gives each interviewer a distinct slice of the target. Asks how many interviewers are in the loop, who's in the candidate pool, what terminology the company uses, and which facets matter most; clusters the target's outcomes and competencies into themes, one per interviewer; writes behavioral questions for each from Team Theory's question bank; then validates the full set for quality, redundancy and coverage. The final plan includes a facet coverage map, one guide per interviewer with questions and follow-ups, and a scoring table. Then offers to push it to your ATS as one interview kit per interviewer.

**Slash Command:** `/team-theory:interview-plan`

```
/team-theory:interview-plan
/team-theory:interview-plan from the CFO target above, 4 interviewers
```

### Built-in question discipline
Every question is written to collect a story, not a rehearsed answer: 15 words or fewer, one question at a time, never naming the competency being tested, and never assuming the candidate has done the exact job before — so strong candidates stepping up aren't screened out by the wording.

## MCP Connectors

Only Team Theory is required. Everything else is optional: the workflows use whatever is connected and skip the rest. See [CONNECTORS.md](CONNECTORS.md) for categories and alternatives.

| Connector | URL | Purpose |
|-----------|-----|---------|
| **Team Theory** | `https://app.teamtheory.ai/mcp` | Required — hiring methodology, your org's prior documents, and document generation |
| **Granola** | `https://mcp.granola.ai/mcp` | Intake-call transcripts and meeting notes |
| **Metaview** | `https://mcp.metaview.ai/mcp` | Interview intelligence — intake and interview transcripts |
| **BrightHire** | `https://app.brighthire.ai/mcp/v1` | Interview intelligence — intake and interview transcripts |
| **Google Drive** | `https://drivemcp.googleapis.com/mcp/v1` | Job descriptions, role briefs; save targets and plans |
| **Box** | `https://mcp.box.com` | Job descriptions, role briefs; save targets and plans |
| **Notion** | `https://mcp.notion.com/mcp` | Role and company notes; save targets and plans |
| **Ashby** | `https://mcp.ashbyhq.com/mcp/v1` | ATS — job context; push interview kits |
| **Workable** | `https://mcp.workable.com/mcp` | ATS — job context; push interview kits |

### Native Integrations

These are native Claude integrations — no MCP connector install needed. They're available when the user connects them in Claude Desktop or Cowork.

| Integration | Purpose |
|-------------|---------|
| **Slack** | Share the target or plan with the hiring team |

## Quick Start

1. Install the plugin:
   - **Claude Code:** `/plugin marketplace add teamtheoryai/teamtheory-plugin`, then `/plugin install team-theory@team-theory`
   - **Cowork:** add this repository as a plugin
2. Sign in to Team Theory when prompted, and connect any optional platforms you use
3. Run `/team-theory:target` with the role, and point Claude at the JD or intake call if you have one
4. Run `/team-theory:interview-plan` to split the target across your interview panel
5. Say yes when Claude offers to push the plan to your ATS — nothing is pushed, posted or shared without your explicit yes

You can also just ask in plain words — "build a scorecard for the CFO role", "split the interviews across four people" — and the right workflow starts.

## File Structure

```
├── .claude-plugin/
│   ├── plugin.json                  # Plugin manifest
│   └── marketplace.json             # Lets this repo be added as a marketplace
├── .mcp.json                        # 9 MCP server connections
├── CONNECTORS.md                    # Connector categories and ~~placeholders
├── LICENSE
├── README.md
├── commands/
│   ├── target.md                    # /team-theory:target
│   └── interview-plan.md            # /team-theory:interview-plan
└── skills/
    ├── role-target/
    │   └── SKILL.md                 # Target (scorecard) workflow
    └── divide-and-conquer/
        └── SKILL.md                 # Divide & Conquer interview plan workflow
```

## Architecture

**Commands** are explicit user entry points. They orient the user and hand off to the matching skill.

**Skills** hold the workflow and the methodology guardrails. They also activate automatically when a request matches, without the slash command.

**Team Theory MCP** does the heavy lifting: `search_methodology_knowledge` grounds each step in Team Theory methodology, `search_portfolio_knowledge` finds the org's own prior documents, and `generate_document` produces the final target and plan. Claude never writes those documents freehand.

**Key design decisions:**
- Tool-agnostic — skills refer to connector categories (`~~ATS`, `~~meeting transcripts`…), so any tool in a category works
- Grounded, not generated — every document is built from retrieved methodology and your own sources
- Working steps stay quiet — clustering, drafting and validation happen in the background; the user sees the plan, not the scaffolding
- Drafts, not sends — nothing is pushed to an ATS, drive or channel without an explicit yes and a named destination

## License

[MIT](LICENSE)
