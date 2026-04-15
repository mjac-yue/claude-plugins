---
name: init
description: Initialize a new product project — creates a standard folder structure with placeholder files for all PM, design, and dev deliverables, and a CLAUDE.md that tells Claude where to save outputs across sessions. Run this once at the start of any new product or feature project. Code is scaffolded separately when you run /tech-stack.
disable-model-invocation: true
---

Set up a new product project for: $ARGUMENTS

> **Learning note — Project Initialization**
> Good projects start with a clean folder structure and a shared understanding of where things live. The init skill creates that structure before any work begins, so every deliverable — from PM brief through design handoff to deployment guide — has a known home. When all tools and team members save to the same locations, you avoid the confusion of "which version is the latest?" — a surprisingly common source of lost work on small teams.

Display the learning note above verbatim to the user before proceeding.

Follow this process exactly:

## Step 1 — Clarify project details

If the project name is not clear from $ARGUMENTS, ask:
1. **Project name** — used as the folder name (use-kebab-case, e.g. `notification-preferences`)
2. **One-line description** — what this product or feature does
3. **Where to create it** — default is the current working directory; ask only if context suggests otherwise

Do not proceed until you have the project name and description.

## Step 2 — Create the folder structure

Use the Bash tool to create the following directories:

```bash
mkdir -p [project-name]/pm
mkdir -p [project-name]/design
mkdir -p [project-name]/dev
```

Note: The `src/` code directory is **not** created here. It is scaffolded by `/tech-stack` after the stack is approved, and will live at the project root alongside `pm/`, `design/`, and `dev/`.

## Step 3 — Create placeholder files

Use the Write tool to create each of the following files. Every placeholder file follows this format:

```
# [Document Title]

**Project**: [Project Name]
**Status**: Not started
**Last updated**: —

> Run `/[skill] [brief topic description]` to generate this document.
```

Create these files:

**pm/ folder:**
- `pm/brief.md` — "Feature Brief" — `/brief`
- `pm/prd.md` — "Product Requirements Document" — `/prd`
- `pm/user-stories.md` — "User Stories" — `/user-story`
- `pm/competitive-analysis.md` — "Competitive Analysis" — `/competitive-analysis`
- `pm/prioritization.md` — "Prioritization" — `/prioritization`
- `pm/roadmap.md` — "Roadmap" — `/roadmap`
- `pm/rollout.md` — "Rollout Package" — `/rollout`

**design/ folder:**
- `design/ux-brief.md` — "UX Brief" — `/ux-brief`
- `design/wireframe-spec.md` — "Wireframe Specification" — `/wireframe-spec`
- `design/design-review.md` — "Design Review" — `/design-review`
- `design/usability-test-plan.md` — "Usability Test Plan" — `/usability-test`
- `design/design-handoff.md` — "Design Handoff" — `/design-handoff`

**dev/ folder:**
- `dev/tech-stack.md` — "Tech Stack" — `/tech-stack`
- `dev/arch-design.md` — "Architectural Design" — `/arch-design`
- `dev/tech-spec.md` — "Technical Specification" — `/tech-spec`
- `dev/api-spec.md` — "API Specification" — `/api-spec`
- `dev/dev-plan.md` — "Development Plan" — `/dev-plan`
- `dev/test-plan.md` — "QA Test Plan" — `/test-plan`
- `dev/deployment.md` — "Deployment Guide" — `/deployment`

## Step 4 — Create the project CLAUDE.md

Use the Write tool to create `[project-name]/CLAUDE.md` using the template below.

Replace [Project Name], [project-name], and [one-line description] with the actual values provided.

---

```markdown
# [Project Name]

[One-line description]

---

## Project context

This is a PM-led, AI-assisted build. The product manager drives all phases and reviews AI-generated outputs before proceeding. Code is written with learning in mind — all files include file-level comments, function comments, and inline explanations of non-obvious logic.

---

## Project structure

```
[project-name]/
├── CLAUDE.md          ← you are here
├── pm/                ← PM deliverables (briefs, PRDs, user stories, roadmap, rollout)
├── design/            ← design deliverables (UX brief, wireframes, handoff)
├── dev/               ← dev documentation (tech spec, API spec, dev plan, test plan)
└── src/               ← application code (scaffolded by /tech-stack)
    ├── app/           ← pages and API routes
    ├── components/    ← reusable UI components
    ├── lib/           ← utilities and helpers
    ├── hooks/         ← custom hooks
    └── types/         ← type definitions
```

`dev/` is documentation only. All application code lives in `src/` (or the framework equivalent) at the project root.

---

## Output paths

When any skill generates output in this project, **save it to the corresponding file below** after presenting it to the user. Always confirm the file was written. Update the **Status** and **Last updated** fields at the top of the file.

| Skill | Save to |
|-------|---------|
| `/brief` | `pm/brief.md` |
| `/prd` | `pm/prd.md` |
| `/user-story` | `pm/user-stories.md` |
| `/competitive-analysis` | `pm/competitive-analysis.md` |
| `/prioritization` | `pm/prioritization.md` |
| `/roadmap` | `pm/roadmap.md` |
| `/rollout` | `pm/rollout.md` |
| `/ux-brief` | `design/ux-brief.md` |
| `/wireframe-spec` | `design/wireframe-spec.md` |
| `/design-review` | `design/design-review.md` |
| `/usability-test` | `design/usability-test-plan.md` |
| `/design-handoff` | `design/design-handoff.md` |
| `/tech-stack` | `dev/tech-stack.md` |
| `/arch-design` | `dev/arch-design.md` |
| `/tech-spec` | `dev/tech-spec.md` |
| `/api-spec` | `dev/api-spec.md` |
| `/dev-plan` | `dev/dev-plan.md` |
| `/test-plan` | `dev/test-plan.md` |
| `/deployment` | `dev/deployment.md` |

---

## Agent context paths

When agents need to find project documents or code, look here:

| Agent | Documents | Code |
|-------|-----------|------|
| `prd-reviewer` | `pm/prd.md` | — |
| `requirements-gap-finder` | `pm/prd.md`, `pm/user-stories.md` | — |
| `competitive-analyst` | `pm/competitive-analysis.md` | — |
| `pm-design-reviewer` | `pm/prd.md`, `pm/user-stories.md`, `design/design-handoff.md` | — |
| `ux-reviewer` | `design/wireframe-spec.md`, `design/design-handoff.md` | — |
| `user-research-planner` | `pm/prd.md`, `design/ux-brief.md` | — |
| `pm-tech-reviewer` | `pm/prd.md`, `dev/tech-spec.md` | — |
| `tech-spec-reviewer` | `pm/prd.md`, `dev/tech-spec.md`, `dev/arch-design.md` | — |
| `solution-analyst` | `pm/prd.md`, `dev/tech-spec.md` | `src/`, `package.json` |
| `arch-reviewer` | `dev/arch-design.md`, `dev/tech-spec.md` | `src/` |
| `code-reviewer` | `dev/tech-spec.md`, `pm/user-stories.md` | `src/` |
| `security-reviewer` | `dev/tech-spec.md`, `dev/api-spec.md` | `src/` |
| `test-case-generator` | `pm/user-stories.md`, `design/design-handoff.md` | `src/` |

*Code paths are populated after `/tech-stack` scaffolds the project. Update if your framework uses different conventions.*

---

## Project status

| Phase | Deliverable | Status |
|-------|------------|--------|
| Setup | Tech stack chosen | Not started |
| Setup | Code scaffold | Not started |
| PM | Feature Brief | Not started |
| PM | PRD | Not started |
| PM | User Stories | Not started |
| PM | Competitive Analysis | Not started |
| PM | Prioritization | Not started |
| PM | Roadmap | Not started |
| PM | Rollout Package | Not started |
| Design | UX Brief | Not started |
| Design | Wireframe Spec | Not started |
| Design | Design Review | Not started |
| Design | Usability Test Plan | Not started |
| Design | Design Handoff | Not started |
| Dev | Architectural Design | Not started |
| Dev | Tech Spec | Not started |
| Dev | API Spec | Not started |
| Dev | Dev Plan | Not started |
| Dev | QA Test Plan | Not started |
| Dev | Deployment Guide | Not started |

Update this table as deliverables are completed — change status to **In progress**, **Done**, or **Skipped**.
```

---

## Step 5 — Confirm and summarise

After creating all files, output:

```
## Project initialised: [Project Name]

📁 [project-name]/
├── CLAUDE.md
├── pm/          (7 deliverables)
├── design/      (5 deliverables)
└── dev/         (7 deliverables)

Code lives at the project root and is scaffolded when you choose your stack.

**Recommended next steps:**
1. Open the [project-name]/ folder in Claude Code
2. Run `/tech-stack [product description]` — chooses your stack and scaffolds src/
3. Run `/pm [feature description]` or `/brief [feature description]` to start the PM workflow

All skill outputs will be saved automatically to their corresponding files.
```
