---
name: kickoff
description: Start a new project — captures project name and context, initialises the folder structure and CLAUDE.md via the init agent, creates the initial product brief, sets up exec-kit state tracking, and guides the user into the first workflow step. This is the single entry point for all new projects. Always run /kickoff before /pm, /design, or /dev.
disable-model-invocation: true
---

Start a new project: $ARGUMENTS

> **Learning note — Project Kickoff**
> A strong project kickoff prevents the most common failure mode in product development: starting work before everyone agrees on what's being built, for whom, and what success looks like. By capturing project identity, creating the folder structure, and writing the initial brief before any PM, design, or engineering work begins, the kickoff ensures every subsequent step starts from a shared foundation. Projects that skip kickoff almost always discover critical misalignment later — when it's expensive to fix.

Display the learning note above verbatim to the user before proceeding.

You are the entry point for the entire product development workflow. Your job is to get a new project fully initialized and hand it off to the first workflow step — all without requiring manual setup.

Work through the steps below in order. Do not skip any step.

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

## Phase D — Testing & Launch
**Status**: Not started
**Automated tests**: Pending
**PM requirements test**: Pending
**Design conformance test**: Pending
**Bug triage**: Pending
**Risk clearance**: Pending
**Rollout**: Pending

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

Phase A — PM + Design Alignment (/pm → /design)
  Brief → Brainstorm (iterative) → Competitive analysis → PRD → User stories →
  Prioritization → Roadmap → UX brief → Wireframe spec → HTML mockups →
  Design review → Usability test → Design handoff

Phase B — Tech Design (/dev Phase 1–3)
  Tech stack → Solution analysis → Architecture → Tech spec → API spec → Dev plan

Phase C — Dev Build (/dev Phase 4–9)
  AI build → QA test plan → Code review → Performance review → Security review → Deployment

Phase D — Testing & Launch (/run Phase D)
  Automated tests → PM requirements test → Design conformance test →
  Bug triage cycle → Risk clearance gate → Rollout

Exec-kit is tracking your project state in [project-slug]-state.md.
Run /run [project] at the start of each session — it reads the state file and
picks up exactly where you left off.
```

Then append the standard **What's next?** block:

> **What's next?** Run `/run [project-name]` to begin Phase A — the `/run` skill will guide you through the full lifecycle from PM alignment through testing and launch.
>
> **Optionally run at this point:**
>
> | Skill / Agent | Plugin | What it does |
> |--------------|--------|-------------|
> | `competitive-analyst` agent | pm-claude-kit | Research competitors in parallel before PM work begins — useful if you want competitive context before framing the problem |
> | `/release-plan` skill | exec-kit | Generate a full release plan with phases, milestones, and build layers before starting work |
>
> *Reply with anything you'd like to run first, or say "start" to begin with `/run`.*

**Optional team document**: If the user is working with a team (not solo), offer to produce a kickoff document using the structure from [kickoff-template.md](kickoff-template.md) — covers team roles, working rhythm, decision-making authority, communication norms, and key dependencies. Save as `[project-slug]-kickoff.md` in the project root. This is separate from `CLAUDE.md` and is intended for sharing with collaborators.
