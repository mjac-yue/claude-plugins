# PM Claude Kit

A Claude Code plugin for Product Managers. Provides slash command skills for common PM workflows and specialized AI agents for reviewing and researching product work.

## What's Included

### Skills (Slash Commands)

| Command | Description |
|---------|-------------|
| `/init [project name]` | Initialize a new project — creates the standard folder structure, placeholder files, and a `CLAUDE.md` that auto-saves skill outputs across sessions |
| `/pm [feature or problem]` | End-to-end PM workflow orchestrator — 7 phases from problem framing through rollout package, with checkpoints |
| `/brainstorm [challenge or problem]` | Structured product brainstorm — asks discovery questions first, then generates ideas across 7 angles with real-world examples, produces Mermaid concept maps and decision trees, and recommends best bet / bold move / quick win with alternatives |
| `/brief [feature description]` | One-page feature brief — lightweight alternative to a full PRD for smaller or experimental features |
| `/prd [feature description]` | Full Product Requirements Document with goals, requirements, success metrics, and risks |
| `/user-story [feature]` | User stories with Given/When/Then acceptance criteria, priority, and complexity |
| `/competitive-analysis [product/market]` | Competitive landscape from existing knowledge — positioning, gaps, and whitespace |
| `/prioritization [list of features]` | RICE, MoSCoW, and impact/effort prioritization for features or initiatives |
| `/okr [goal/team/quarter]` | OKRs with measurable key results, baselines, and data sources |
| `/roadmap [feature or initiative]` | Product roadmap by theme and timeframe (Now/Next/Later or quarterly) |
| `/meeting-notes [raw notes or description]` | Structure raw meeting notes into decisions, action items, and open questions |
| `/rollout [feature]` | Launch enablement package — audience summaries and user training materials |
| `/tech-stack [project description]` | Tech stack recommendation optimized for solo PM-builder — framework, database, hosting, cost estimate |

### Agents

| Agent | Description |
|-------|-------------|
| `prd-reviewer` | Reviews a PRD across 8 dimensions — flags critical gaps, weak metrics, and scope issues |
| `requirements-gap-finder` | Stress-tests specs for edge cases and implementation gaps before engineering handoff |
| `competitive-analyst` | Researches multiple competitors in parallel via live web search — produces comparison matrix and strategic insights |

Agents are invoked automatically by Claude when relevant, or you can ask directly: *"Use the prd-reviewer agent to review this PRD."*

---

## Installation

### Install from GitHub

```bash
# Register the marketplace (one-time setup)
claude plugin marketplace add github:mjac-yue/claude-plugins

# Install the plugin
claude plugin install pm-claude-kit
```

### Verify installation

```bash
claude plugin list
```

You should see `pm-claude-kit` listed. The skills will now be available as slash commands.

---

## Usage Examples

### Start a new project
```
/init notification-preferences
```
Creates `notification-preferences/` with a `CLAUDE.md` and placeholder files for every PM deliverable.

### Run the full PM workflow
```
/pm Build a notification preferences feature for mobile users
```

### Brainstorm solutions to a product problem
```
/brainstorm We're losing users at the onboarding step where they invite teammates
```

### Write a quick brief
```
/brief Add CSV export to the reporting dashboard
```

### Write a PRD
```
/prd In-app referral program — users can invite teammates and earn credits
```

### Create user stories
```
/user-story Notification preferences — users should control which emails they receive
```

### Process meeting notes
```
/meeting-notes Discussed Q3 roadmap. Sarah wants to prioritize mobile. John pushed back on timeline. We agreed to do discovery first. Sarah to run 5 user interviews by end of month.
```

### Competitive analysis
```
/competitive-analysis Project management tools in the SMB space — focus on task assignment and reporting
```

### Prioritize a backlog
```
/prioritization Dark mode, bulk export, SSO login, in-app notifications, API rate limiting, onboarding checklist
```

### Choose a tech stack
```
/tech-stack New web app — solo PM build with AI, need auth and a database, React preferred
```

### Review a PRD with the agent
```
Use the prd-reviewer agent to review this PRD
```

### Research competitors with live web search
```
Use the competitive-analyst agent to research Notion, Coda, and Confluence for the knowledge management space
```

---

## Recommended Companion Plugins

For the full product-to-production workflow, also install:

| Plugin | Purpose | Install |
|--------|---------|---------|
| **design-ux-kit** | UX briefs, wireframes, design reviews, usability tests | `claude plugin install design-ux-kit` |
| **dev-workflow-kit** | Tech specs, code review, security review, deployment guides | `claude plugin install dev-workflow-kit` |
| **GitHub MCP** | Track issues, PRs, and milestones | `claude mcp add github` |
| **pdf skill** | Read and extract from PDFs | `claude plugin install anthropic-skills:pdf` |
| **docx skill** | Create/edit Word documents | `claude plugin install anthropic-skills:docx` |
| **pptx skill** | Create presentations | `claude plugin install anthropic-skills:pptx` |

---

## Sharing with Your Team

1. Push this repo to your company GitHub
2. Team members install with: `claude plugin install github:your-org/claude-plugins`
3. Everyone gets the same commands and templates

---

## Customizing

### Modify a template
Templates live in each skill's folder (e.g., `skills/prd/prd-template.md`). Edit them to match your team's conventions.

### Add a new skill
1. Create `skills/your-skill/SKILL.md` following the existing pattern
2. Reinstall: `claude plugin uninstall pm-claude-kit && claude plugin install pm-claude-kit`

### Adjust agent behavior
Edit the relevant file in `agents/` (e.g., `agents/prd-reviewer.md`) to change review criteria or output format.
