# Dev Workflow Kit

A Claude Code plugin for developers and PM-led builds. Provides slash command skills for the full development lifecycle — from architecture through deployment — plus specialized AI agents for technical review, security auditing, and test generation.

## What's Included

### Skills (Slash Commands)

| Command | Description |
|---------|-------------|
| `/dev [feature or requirement]` | Full Development workflow orchestrator — runs all phases from architecture through deployment, with checkpoints |
| `/arch-design [feature or system]` | Define architectural style, component boundaries, integration patterns, and ADRs |
| `/tech-spec [feature]` | Generate a complete technical specification with solution options, data model, and risk assessment |
| `/api-spec [API or feature]` | Define endpoints, request/response schemas, auth model, and error handling |
| `/dev-plan [feature]` | Break implementation into tasks with estimates, dependencies, and sprint allocation |
| `/test-plan [feature]` | Define test types, coverage targets, and key test cases (happy path, edge cases, error states) |
| `/code-review [PR or change description]` | Structured code review covering correctness, security, performance, and patterns |
| `/perf-review [feature or system]` | Validate against latency/throughput targets and identify bottlenecks |
| `/security-review [feature or codebase]` | OWASP Top 10 security audit with severity ratings |
| `/bug-report [bug description]` | Produce a structured bug report with reproduction steps, impact, and expected behavior |
| `/deployment [feature or app]` | Step-by-step deployment guide with pre-deploy checklist, smoke tests, and rollback plan |

### Agents

| Agent | Description |
|-------|-------------|
| `solution-analyst` | Researches technical approaches and libraries against your codebase, then recommends with evidence |
| `arch-reviewer` | Reviews architecture against quality attributes: performance, scalability, security, maintainability |
| `code-reviewer` | Reviews actual source files with specific line-level findings across all review dimensions |
| `security-reviewer` | OWASP-aligned security audit of actual source files with evidence-based findings |
| `tech-spec-reviewer` | Reviews a tech spec for completeness, engineering risks, and feasibility |
| `pm-tech-reviewer` | Translates technical decisions into plain language for PM review and approval |
| `test-case-generator` | Expands user stories and acceptance criteria into comprehensive test cases |
| `ai-opportunity-analyst` | Identifies where AI could add value in a product, with cost estimates and fit assessment |

Agents are invoked automatically by Claude when relevant, or you can ask directly: *"Use the code-reviewer agent to review this PR."*

---

## Installation

### Install from GitHub

```bash
claude plugin marketplace add github:mjac-yue/claude-plugins
claude plugin install dev-workflow-kit
```

### Verify installation

```bash
claude plugin list
```

You should see `dev-workflow-kit` listed. The skills will now be available as slash commands.

---

## Usage Examples

### Run the full dev workflow
```
/dev Add a bulk export feature — users download data as CSV; built by a solo PM with AI assistance
```

### Design the architecture
```
/arch-design Event notification system — fan-out to email, push, and in-app channels
```

### Write a tech spec
```
/tech-spec CSV export feature — async job queue, S3 storage, email delivery when ready
```

### Generate a dev plan
```
/dev-plan Based on the approved tech spec for the export feature
```

### Review a PR
```
/code-review PR #47 — adds the CSV export endpoint and job queue worker
```

### Security audit
```
/security-review The authentication and session management code in src/auth/
```

### Create a deployment guide
```
/deployment Export feature on Render with a Postgres database and S3 bucket
```

### Deep code review with line-level findings
```
Use the code-reviewer agent to review src/export/
```

### Review tech spec as a PM
```
Use the pm-tech-reviewer agent to review this tech spec
```

---

## Recommended Companion Plugins

For the full product-to-production workflow, also install:

| Plugin | Purpose | Install |
|--------|---------|---------|
| **pm-claude-kit** | PRDs, user stories, competitive analysis, roadmaps | `claude plugin install pm-claude-kit` |
| **design-ux-kit** | UX briefs, wireframes, design reviews, usability tests | `claude plugin install design-ux-kit` |
| **GitHub MCP** | Track issues, PRs, and milestones | `claude mcp add github` |

---

## Sharing with Your Team

1. Push this repo to your company GitHub
2. Team members install with: `claude plugin install github:your-org/claude-plugins`
3. Everyone gets the same commands and templates

---

## Customizing

### Modify a template
Templates live in each skill's folder (e.g., `skills/tech-spec/tech-spec-template.md`). Edit them to match your team's conventions.

### Add a new skill
1. Create `skills/your-skill/SKILL.md` following the existing pattern
2. Reinstall: `claude plugin uninstall dev-workflow-kit && claude plugin install dev-workflow-kit`

### Adjust agent behavior
Edit the relevant file in `agents/` (e.g., `agents/code-reviewer.md`) to change review criteria or output format.
