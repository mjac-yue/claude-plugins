# Claude Code Plugin Suite

A set of Claude Code plugins covering the full product development lifecycle — from product discovery through design, engineering, and deployment. Built for a **PM-led, AI-assisted workflow** where a product manager drives the process and uses AI to execute design and development tasks, reviewing outputs before each phase proceeds.

---

## Plugins

| Plugin | Orchestrator | Purpose |
|--------|-------------|---------|
| `pm-claude-kit` | `/pm` | Full PM workflow — discovery, PRD, user stories, prioritization, roadmap, rollout |
| `design-ux-kit` | `/design` | Full design workflow — UX brief, wireframes, design review, usability testing, handoff |
| `dev-workflow-kit` | `/dev` | Full dev workflow — architecture, tech spec, API spec, dev plan, QA, code/perf/security review, deployment |

Each plugin has a **workflow orchestrator** (runs all phases end-to-end with checkpoints) and a set of **standalone skills** you can run independently for individual tasks.

---

## pm-claude-kit

### Skills

| Skill | What it does |
|-------|-------------|
| `/init` | Initialize a new project — creates the standard folder structure, placeholder files, and a `CLAUDE.md` that auto-saves skill outputs across sessions |
| `/pm` | End-to-end PM workflow orchestrator — 7 phases from problem framing to rollout package |
| `/brief` | One-page feature brief — lightweight alternative to a full PRD for smaller features |
| `/prd` | Full Product Requirements Document with goals, requirements, success metrics, and risks |
| `/user-story` | User stories with Given/When/Then acceptance criteria, priority, and complexity |
| `/competitive-analysis` | Competitive landscape from existing knowledge — positioning, gaps, whitespace |
| `/prioritization` | RICE, MoSCoW, and impact/effort prioritization for features or initiatives |
| `/okr` | OKRs with measurable key results, baselines, and data sources |
| `/roadmap` | Product roadmap by theme and timeframe (Now/Next/Later or quarterly) |
| `/meeting-notes` | Structure raw meeting notes into decisions, action items, and open questions |
| `/rollout` | Launch enablement package — audience summaries and user training materials |
| `/tech-stack` | Tech stack recommendation optimized for solo PM-builder — framework, database, hosting, cost estimate |

### Agents

| Agent | What it does |
|-------|-------------|
| `prd-reviewer` | Reviews a PRD across 8 dimensions — flags critical gaps, weak metrics, scope issues |
| `requirements-gap-finder` | Stress-tests specs for edge cases and implementation gaps before engineering handoff |
| `competitive-analyst` | Researches multiple competitors in parallel via live web search — produces comparison matrix and strategic insights |

---

## design-ux-kit

### Skills

| Skill | What it does |
|-------|-------------|
| `/design` | End-to-end design workflow orchestrator — 5 phases from UX brief to dev handoff |
| `/ux-brief` | UX brief defining scope, target users, goals, constraints, and success criteria |
| `/wireframe-spec` | Wireframe specification — screens, user flows, components, states, and interactions in structured text |
| `/design-review` | Heuristic design review against Nielsen's 10 usability principles and WCAG 2.1 AA |
| `/usability-test` | Usability test plan with participant criteria, task scenarios, success metrics, and discussion guide |
| `/design-handoff` | Design handoff spec for engineering — components, states, interactions, and acceptance criteria |

### Agents

| Agent | What it does |
|-------|-------------|
| `ux-reviewer` | Structured UX audit against heuristics and accessibility guidelines — prioritized findings report |
| `user-research-planner` | Plans a user research study, or produces an assumption validation plan when formal research isn't feasible |
| `pm-design-reviewer` | Reviews design artifacts from a PM perspective — requirements coverage, user flow completeness, handoff readiness |

---

## dev-workflow-kit

### Skills

| Skill | What it does |
|-------|-------------|
| `/dev` | End-to-end dev workflow orchestrator — 8 phases from solution analysis to deployment |
| `/arch-design` | Architectural design — NFRs, architectural style, component boundaries, integration patterns, ADRs |
| `/tech-spec` | Technical specification — solution options, data model, components, dependencies, risk assessment |
| `/api-spec` | API specification — endpoints, request/response schemas, auth, error handling, versioning |
| `/dev-plan` | Development plan — task breakdown, estimates, dependencies, critical path, sprint allocation |
| `/test-plan` | QA test plan — test types, coverage targets, key test cases, acceptance criteria, sign-off process |
| `/code-review` | Structured code review checklist — correctness, test coverage, error handling, security, patterns |
| `/perf-review` | Performance review — latency targets, query analysis, caching, load test results, bottlenecks |
| `/security-review` | Security review aligned to OWASP Top 10 — findings with severity and remediation steps |
| `/bug-report` | Structured bug report — reproduction steps, severity, environment, expected vs. actual behavior |
| `/deployment` | Deployment guide — platform setup, environment config, database provisioning, smoke tests, rollback |

### Agents

| Agent | What it does |
|-------|-------------|
| `solution-analyst` | Reads the codebase and researches 2–4 technical options — produces structured comparison and recommendation |
| `arch-reviewer` | Reviews architecture against 8 quality attributes — reads actual code, not just documentation |
| `tech-spec-reviewer` | Reviews a tech spec for completeness, engineering risks, and feasibility across 10 dimensions |
| `pm-tech-reviewer` | Translates tech spec decisions into plain language — flags complexity risk, checks requirements coverage |
| `code-reviewer` | Reviews actual source files — specific line-level findings with blocking/non-blocking severity |
| `security-reviewer` | Audits actual code for OWASP Top 10 vulnerabilities — evidence-based findings with exploit scenarios |
| `test-case-generator` | Generates comprehensive test cases from user stories or acceptance criteria |
| `ai-opportunity-analyst` | Identifies where AI could add value in the product — evaluates fit, cost, and risk for each opportunity |

---

## Installation

### Install all three plugins

```bash
# Register the marketplace (one-time setup)
claude plugin marketplace add github:mjac-yue/claude-plugins

# Install each plugin
claude plugin install pm-claude-kit
claude plugin install design-ux-kit
claude plugin install dev-workflow-kit

# Verify
claude plugin list
```

### Install individual plugins

Install only the plugins relevant to your role:

```bash
# Product managers
claude plugin marketplace add github:mjac-yue/claude-plugins
claude plugin install pm-claude-kit

# Designers
claude plugin marketplace add github:mjac-yue/claude-plugins
claude plugin install design-ux-kit

# Engineers
claude plugin marketplace add github:mjac-yue/claude-plugins
claude plugin install dev-workflow-kit
```

---

## Usage

### Start a new project

```
/init notification-preferences
```

This creates `notification-preferences/` with a `CLAUDE.md` and placeholder files for every deliverable. Open that folder in Claude Code and all subsequent skill outputs will be saved to their corresponding files automatically.

### Run a full workflow end-to-end

```
/pm Build a notification preferences feature for mobile users
/design Notification preferences settings screen
/dev Implement notification preferences — see PRD and design handoff attached
```

### Run individual skills

```
/brief Add CSV export to the reporting dashboard
/prd In-app referral program
/tech-stack New web app — solo build, React preferred, need auth and a database
/bug-report Checkout button disabled after removing a promo code on Safari
/deployment Next.js app on Vercel with Supabase database
```

### Invoke agents directly

```
Use the prd-reviewer agent to review this PRD: [paste or file path]
Use the competitive-analyst agent to research Notion, Coda, and Confluence
Use the pm-tech-reviewer agent on this tech spec before I approve it
Use the code-reviewer agent to review the files in /src/api/orders
```

---

## Workflow overview

The three plugins map to the natural product development sequence. Outputs from each phase feed the next:

```
/pm  →  PRD + user stories
           ↓
       /design  →  wireframe spec + design handoff
                       ↓
                   /dev  →  tech spec + code + deployment
```

Each orchestrator pauses at checkpoints for review and approval before proceeding. Agents are offered at relevant points and can also be invoked directly at any time.

---

## Updating

When changes are made to the plugins, pull the latest and reinstall:

```bash
# Get the latest version
claude plugin uninstall pm-claude-kit && claude plugin install pm-claude-kit
claude plugin uninstall design-ux-kit && claude plugin install design-ux-kit
claude plugin uninstall dev-workflow-kit && claude plugin install dev-workflow-kit
```

---

## Repository structure

```
claude-plugins/
├── .claude-plugin/
│   └── marketplace.json          # Marketplace configuration
└── plugins/
    ├── pm-claude-kit/
    │   ├── .claude-plugin/
    │   │   └── plugin.json
    │   ├── skills/
    │   │   └── <skill-name>/
    │   │       ├── SKILL.md      # Skill prompt and configuration
    │   │       └── *-template.md # Output template
    │   └── agents/
    │       └── <agent-name>.md   # Agent instructions and configuration
    ├── design-ux-kit/
    │   └── [same structure]
    └── dev-workflow-kit/
        └── [same structure]
```
