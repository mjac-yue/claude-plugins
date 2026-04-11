# PM Claude Kit

A Claude Code plugin for Product Managers. Provides slash command skills for common PM workflows and specialized AI agents for reviewing product specs.

## What's Included

### Skills (Slash Commands)

| Command | Description |
|---------|-------------|
| `/prd [feature description]` | Generate a complete PRD from a brief or detailed description |
| `/user-story [feature]` | Create user stories with acceptance criteria in Given/When/Then format |
| `/meeting-notes [raw notes or description]` | Structure meeting notes with decisions and action items |
| `/competitive-analysis [product/market]` | Produce a structured competitive analysis with comparison matrix |
| `/okr [goal/team/quarter]` | Draft OKRs with measurable key results and grading guidance |
| `/prioritization [list of features]` | Prioritize using RICE, MoSCoW, or impact/effort matrix |

### Agents

| Agent | Description |
|-------|-------------|
| `prd-reviewer` | Reviews a PRD for completeness, clarity, weak metrics, and missing scope |
| `requirements-gap-finder` | Stress-tests specs for edge cases and implementation gaps before engineering handoff |

Agents are invoked automatically by Claude when relevant, or you can ask Claude directly: *"Use the prd-reviewer agent to review this PRD."*

---

## Installation

### Option 1: Install from local path (recommended for teams)

Clone or download this repo, then run in Claude Code:

```
/plugin install /path/to/pm-claude-kit
```

### Option 2: Install from GitHub (once published)

```
/plugin install github:your-org/pm-claude-kit
```

### Verify installation

```
/plugin list
```

You should see `pm-claude-kit` listed. The skills will now be available as slash commands.

---

## Usage Examples

### Write a PRD
```
/prd Add a bulk export feature that lets users download their data as CSV
```

### Create user stories
```
/user-story Notification preferences — users should be able to control which emails they receive
```

### Process meeting notes
```
/meeting-notes Discussed Q3 roadmap. Sarah wants to prioritize mobile. John pushed back on timeline. We agreed to do discovery first. Sarah to run 5 user interviews by end of month.
```

### Competitive analysis
```
/competitive-analysis Project management tools in the SMB space — focus on task assignment and reporting features
```

### Prioritize a backlog
```
/prioritization Dark mode, bulk export, SSO login, in-app notifications, API rate limiting, onboarding checklist
```

### Review a PRD
Once you have a PRD open or pasted, ask:
```
Use the prd-reviewer agent to review this PRD
```

### Find spec gaps before engineering handoff
```
Use the requirements-gap-finder agent on this spec: [paste spec]
```

---

## Recommended Companion Plugins & MCPs

For a full PM setup, also consider installing:

| Tool | Purpose | Install |
|------|---------|---------|
| **GitHub MCP** | Track issues, PRs, and milestones | `claude mcp add github` |
| **Linear MCP** | Manage Linear issues and cycles | `/plugin install linear` |
| **Slack MCP** | Post updates to Slack channels | `/plugin install slack` |
| **pdf skill** | Read and extract from PDFs | `/plugin install anthropic-skills:pdf` |
| **docx skill** | Create/edit Word documents | `/plugin install anthropic-skills:docx` |
| **pptx skill** | Create presentations | `/plugin install anthropic-skills:pptx` |

---

## Sharing with Your Team

1. Push this repo to your company GitHub
2. Team members install with: `/plugin install github:your-org/pm-claude-kit`
3. Everyone gets the same commands and templates

---

## Customizing

### Modify a template
Templates live in each skill's folder (e.g., `skills/prd/prd-template.md`). Edit them to match your team's conventions.

### Add a new skill
1. Create `skills/your-skill/SKILL.md` following the existing pattern
2. Reload: `/plugin reload pm-claude-kit`

### Adjust agent behavior
Edit `agents/prd-reviewer.md` or `agents/requirements-gap-finder.md` to change the review criteria to match your team's standards.
