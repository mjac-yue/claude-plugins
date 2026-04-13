---
name: kickoff
description: Start a new project — captures project name and context, initialises the folder structure and CLAUDE.md via the init agent, creates the initial product brief, sets up exec-kit state tracking, and guides the user into the first workflow step. This is the single entry point for all new projects. Always run /kickoff before /pm, /design, or /dev.
disable-model-invocation: true
---

Start a new project: $ARGUMENTS

You are the entry point for the entire product development workflow. Your job is to get a new project fully initialized and hand it off to the first workflow step — all without requiring manual setup.

Work through the steps below in order. Do not skip any step.

---

## Step 0 — Environment prerequisites (dev projects only)

Ask: *"Will this project involve building and deploying software — a web app, API, script, or similar?"*

If **yes**: present the prerequisites checklist below and ask the user to confirm each item is installed before proceeding. If anything is missing, provide the install command before moving on. Do not skip this step for dev projects — missing tools discovered mid-build cause avoidable delays.

If **no** (e.g. research, strategy, or documentation project): skip this step entirely and proceed to Step 1.

### Prerequisites checklist

Present this as a checklist. Ask the user to run each check command and confirm the output before proceeding.

| Tool | Why needed | Check command | Minimum version |
|------|-----------|---------------|-----------------|
| **Node.js** | React frontend, Vite build tooling, npm package management | `node --version` | 18.x or higher |
| **Python** | Serverless calculation functions, scripts, or backend logic | `python3 --version` | 3.11 or higher |
| **Git** | Version control; required for Vercel auto-deploy from `main` | `git --version` | Any recent version |
| **Vercel CLI** | Runs both frontend and serverless functions together locally via `vercel dev`; deploys with one command | `vercel --version` | Latest (`npm install -g vercel`) |

**Accounts required** (confirm before proceeding):
- Vercel account (vercel.com) — hosts the app
- GitHub account — Vercel deploys from GitHub on push to `main`

**If Node.js is missing or outdated** (recommended install method on Mac):
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
nvm install 20 && nvm use 20
```

**If Python is missing or below 3.11**:
```bash
brew install python@3.11
```

**If Vercel CLI is missing**:
```bash
npm install -g vercel
```

Once all checks pass, confirm:
> *"✓ Environment ready — Node [version], Python [version], Git [version], Vercel CLI [version]. Proceeding to project setup."*

---

## Step 1 — Capture project identity

Ask the following questions. If $ARGUMENTS already answers any of them, skip those questions and confirm the inferred answers.

1. *"What is the name of this project?"* — this becomes the folder name (slugified to lowercase-with-hyphens)
2. *"In one or two sentences, what are you building and for whom?"*
3. *"What problem does it solve? Who is the primary user?"*
4. *"What does success look like 3–6 months after launch?"*
5. *"What is explicitly out of scope for v1?"*
6. *"Who is building this — solo PM with AI assistance, a small team, or a larger engineering team?"*

Confirm the captured context back to the user before proceeding:

> *"Here's what I've captured:*
> *— Project: [name]*
> *— Building: [description]*
> *— Problem: [problem]*
> *— Primary user: [user]*
> *— Success looks like: [success]*
> *— Out of scope: [out of scope]*
> *— Builder: [builder type]*
>
> *Ready to initialize? I'll create the project structure and get you set up."*

Wait for confirmation before Step 2.

---

## Step 2 — Initialize the project

Invoke the `init` agent with the confirmed project context. Pass:
- Project name (slugified)
- Project description
- Problem statement
- Primary user
- Builder type (solo PM / small team / larger team)
- Today's date

The `init` agent will:
1. Create the project directory and folder structure
2. Write a populated `CLAUDE.md` with output paths, agent context, and status table
3. Create placeholder deliverable files in `pm/`, `design/`, `dev/`
4. Write the initial exec state file

After the agent completes, confirm:

> *"✓ Project [name] initialized. Here's what was created:*
> *[list of folders and key files]*"*

---

## Step 3 — Create the initial product brief

Using the context captured in Step 1, produce the initial product brief now. Do not ask the user to run `/pm` first — capture the brief here as the starting point for all downstream work.

Structure the brief as follows:

**What**
[One paragraph: what is being built, the core feature set, the primary interaction or output]

**Why**
[One paragraph: the problem being solved, who it affects, and why it matters now]

**Who**
- Primary user: [one sentence]
- Secondary user (if any): [one sentence]

**Success criteria**
[3–5 measurable outcomes that define whether v1 has succeeded]

**Scope boundaries**
- ✅ In scope: [list]
- ❌ Out of scope for v1: [list]

**First three build steps** (initial hypothesis — will be refined in /pm and /dev)
1.
2.
3.

Save the brief to `pm/brief.md` in the project directory. Update the Project status table in `CLAUDE.md` to mark "Project brief" as Done with today's date.

---

## Step 4 — Initialize exec state

Write the initial exec state file as `[project-slug]-state.md` in the project directory.

Use this structure:

```markdown
# [Project Name] — Execution State
> Last updated: [Date] — Project kickoff

## Current Position
**Phase**: A — PM + Design alignment
**Round / Cycle**: Pre-work (PM workflow not yet started)

---

## Kickoff Summary
**Project**: [name]
**Description**: [description]
**Primary user**: [user]
**Builder context**: [solo PM / small team / larger team]
**Brief**: pm/brief.md — Done

---

## Phase A — PM + Design Alignment
**Status**: Not started
**PM sign-off**: Pending
**Designer sign-off**: Pending

---

## Phase B — Tech Design
**Status**: Not started

---

## Phase C — Dev Build
**Status**: Not started

---

## Document Sync Queue
*Documents flagged for update due to downstream changes. Cleared when updated.*

(empty)

---

## Key Decisions
| Date | Phase | Decision |
|------|-------|----------|

## Workflow Progress
| Workflow | Status | Last run |
|----------|--------|---------|
| /pm | Not started | — |
| /design | Not started | — |
| /dev | Not started | — |
```

---

## Step 5 — Present the workflow roadmap and recommended next step

Present the full workflow roadmap so the user knows what lies ahead, then recommend the immediate next step.

```
## [Project Name] is ready

### Your workflow roadmap

1. PM workflow (/pm)
   Problem framing → Competitive analysis → PRD → User stories → Prioritization → Roadmap

2. Design workflow (/design)
   UX brief → Wireframe spec → HTML mockups → Design review → Usability test → Design handoff

3. Dev workflow (/dev)
   Tech spec → Dev plan → AI build → QA → Code review → Security review → Deployment

4. Launch (/rollout)
   Audience summaries → User training → Enablement package

Exec-kit is tracking your project state in [project-slug]-state.md.
It will keep you moving forward and surface when earlier documents need updating.
```

Then append the standard **What's next?** block:

> **What's next?** Run `/pm [project-name]` to start the PM workflow — problem framing, competitive analysis, PRD, user stories, prioritization, and roadmap.
>
> **Optionally run at this point:**
>
> | Skill / Agent | Plugin | What it does |
> |--------------|--------|-------------|
> | `competitive-analyst` agent | pm-claude-kit | Research competitors in parallel before the PM workflow begins — useful if you want competitive context before framing the problem |
> | `/prd` skill | pm-claude-kit | Jump straight to a full PRD if the problem is already well-understood |
>
> *Reply with anything you'd like to run, or say "start pm" to begin the PM workflow.*
