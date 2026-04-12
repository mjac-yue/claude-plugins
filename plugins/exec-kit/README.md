# Exec Kit

A Claude Code plugin for full-lifecycle project execution. Covers the entire delivery arc from initial PM discovery through design alignment, technical design, and dev build — for a 1–2 person PM-led team. Methodology-aware: works with sprints or continuous flow (Kanban).

## Three-Phase Lifecycle

Exec Kit owns the full project lifecycle across three phases. Each phase has its own work unit, cadence, and roles:

| Phase | Who | Work unit | Done when |
|-------|-----|-----------|-----------|
| **A — PM + Design alignment** | PM + Designer (no Eng) | Iteration round | PM and Designer mutually sign off — PRD final, all P0 screens covered |
| **B — Tech design** | All three (Eng leads) | Review round | All constraints resolved, all three sign off, Eng accepts handoff |
| **C — Dev build** | Eng (PM + Design available) | Sprint or Kanban cycle | All features shipped, launch checklist green |

Phases A and B are **iterative**, not linear handoffs. PM and Design feed back and forth across rounds until alignment is reached. Eng may send constraint feedback back to PM and Design in Phase B, triggering additional rounds before dev can start.

---

## What's Included

### Orchestrators

| Command | Description |
|---------|-------------|
| `/release [project or feature]` | Full lifecycle setup — project profile, kickoff, release plan, risk register, and first Phase A round plan. Creates the session state file. |
| `/run [phase and context]` | Execution orchestrator across all three phases. Reads state file at start of every session to resume seamlessly. Manages iteration rounds (A), constraint rounds (B), and daily cycles (C). |

### Skills (Slash Commands)

| Command | Description |
|---------|-------------|
| `/release-plan [project description]` | Full release plan spanning all phases — PM + Design alignment, tech design, and dev build layers. Foundation-first sequencing for dev. |
| `/cycle-plan [round or cycle details]` | Plan a single work unit for the active phase: iteration round (A), constraint round (B), or sprint/Kanban cycle (C). |
| `/standup [updates]` | Phase-aware status updates. Phases A+B: structures iteration updates — PRD changes, design changes, open questions/constraints. Phase C: daily done/in-progress/blocked standup. |
| `/retro [round or cycle summary]` | Phase-aware retrospective. Phases A+B: sign-off decision with convergence assessment. Phase C: lightweight cycle retro with one action per person and one process change. |
| `/status [project and cycle context]` | Stakeholder status report — RAG status, progress against release plan, risks, decisions needed. |
| `/risk [project context]` | Risk register — identify, score (likelihood × impact), define mitigations and owners. |
| `/kickoff [project description]` | Project kickoff doc — scope, team roles, decision authority, working rhythm, communication norms. |

### Agents

| Agent | Description |
|-------|-------------|
| `plan-reviewer` | Reviews a release or cycle plan for over-commitment, missing dependencies, wrong build-layer sequencing, and feasibility for a 1–2 person team. |
| `blocker-coach` | Diagnoses a blocker's root cause, generates unblocking options (resolve, workaround, descope, escalate), and drafts any communications needed. |

Agents are invoked automatically by Claude when relevant, or you can ask directly: *"Use the plan-reviewer agent to check this release plan."*

---

## Session Continuity

Exec Kit writes a persistent state file (`[project-name]-state.md`) to the project folder. This file is updated after every checkpoint and is the resume point for every new session.

**Starting a new session**: Claude reads the state file and presents a one-line summary of where the project is before doing anything. No re-explaining context.

**What the state file tracks**:
- Current phase (A/B/C) and round/cycle number
- All open questions (Phase A) or constraints (Phase B) with owners
- Sign-off status for each role
- In-progress and carried-over dev items (Phase C)
- Key decisions log
- Artifact file paths (PRD, design handoff, tech spec, release plan)

**Written by**: `/release` (creates it), `/run` (after every checkpoint), `/retro` (at sign-off decisions), `/cycle-plan` (standalone use), `/standup` (Phase A+B updates only).

---

## Installation

### Install from GitHub

```bash
claude plugin marketplace add mjac-yue/claude-plugins
claude plugin install exec-kit
```

### Verify installation

```bash
claude plugin list
```

---

## Usage Examples

### Kick off a new project end-to-end
```
/release Build a notification preferences feature — users control which emails they receive
```
*Produces: project profile, kickoff doc, release plan covering all three phases, risk register, first Phase A round plan, and the session state file.*

### Run Phase A — PM + Design alignment
```
/run Phase A, Round 1 — PM is drafting the notification preferences PRD, Designer starting exploration
```

### Process a Phase A iteration update
```
/standup PM: updated sections 3 and 4, open question on email frequency — need Design input. Designer: completed notification settings screen, two edge cases unresolved on mobile.
```

### Run Phase B — Tech design
```
/run Phase B, Round 1 — Eng reviewing PRD and design handoff for notification preferences
```

### End of Phase A — run the round review
```
/retro Phase A Round 2 — all screens complete, PRD final, PM and Designer ready to sign off
```

### Run a Phase C dev cycle
```
/run Cycle 3 — we're in Layer 3 core build, 2 people, 10 days available
```

### Process a daily dev standup
```
/standup Person A: finished auth endpoints, working on user profile API, no blockers. Person B: design handoff reviewed and accepted, starting on frontend component library, blocked on Figma access.
```

### End-of-cycle retrospective
```
/retro Cycle 3 — completed 4 of 6 items, carried over 2. Auth took longer than sized. Parallel work between frontend and backend went well.
```

### Weekly status report
```
/status Week 5, building Layer 3, 2 of 5 P0 features complete, on track for end-of-month launch
```

### Review a plan before starting
```
Use the plan-reviewer agent to review this release plan
```

### Diagnose a blocker
```
Use the blocker-coach agent — we're blocked on the payment integration because the third-party API sandbox isn't returning consistent responses
```

---

## How It Fits in the Suite

```
exec-kit          →  owns the full lifecycle (PM alignment → design alignment → dev build)
pm-claude-kit     →  PM craft tools invoked within Phase A (PRD, user stories, prioritization)
design-ux-kit     →  design craft tools invoked within Phase A/B (wireframes, UX review, handoff)
dev-workflow-kit  →  dev craft tools invoked within Phase C (tech spec, code review, security)
```

Exec Kit is the execution layer. The other plugins provide craft-level tools that are called from within exec's phases — not separate workflows that exec follows.

---

## Project Tiers — Process scales to project size

The plugin asks two questions before producing anything: team size and project scope. Together these determine the **project tier**, which controls how much process is applied across all three phases.

| Tier | Scope | Timeline | What gets produced |
|------|-------|----------|--------------------|
| **1 — Micro** | Single small change, clear scope | Days – 2 weeks | Ordered task list + brief launch checklist. No formal documents. |
| **2 — Small** | 1–3 features, few unknowns | 2–6 weeks | Lightweight release plan, abbreviated Phase A (single round), single Phase B session. |
| **3 — Medium** | Multi-feature, some unknowns | 6–16 weeks | Full release plan, full Phase A rounds, full Phase B, focused risk register (top 5 risks). |
| **4 — Large** | Full product, high complexity | 16+ weeks | Everything — full docs, all sections, exhaustive risk register, go/no-go criteria, risk checkpoints. |

You can override the suggested tier — the plugin explains what it's skipping and why, and confirms before proceeding.

---

## Methodology — Recommended by team size

Within the confirmed tier, methodology is recommended based on team size:

| Team size | Default recommendation | Reason |
|-----------|----------------------|--------|
| **1–2 people** | **Kanban** | No sprint ceremony overhead; absorbs interruptions; WIP limits prevent context-switching; ship when done, not when sprint ends |
| **3–5 people** | **Scrum (1-week sprints)** | Structured cadence helps coordinate; short sprint keeps planning overhead low |
| **5+ people** | **Scrum (2-week sprints)** | Coordination cost at this size benefits from full sprint rhythm |

**Kanban specifics for 1–2 person teams:**
- Cycle = weekly planning horizon (not a locked sprint)
- Items can be pulled in during the week if capacity opens
- WIP limit: max 2 items in progress at once per person
- Retrospective: end of each week or every 2 weeks — your call
- No sprint reviews — demo when features ship, not on a calendar

---

## Sharing with Your Team

1. Push this repo to your company GitHub
2. Team members install with: `claude plugin install github:your-org/claude-plugins`
3. Everyone gets the same commands and templates

---

## Customizing

### Modify a template
Templates live in each skill's folder (e.g., `skills/release-plan/release-plan-template.md`). Edit them to match your team's conventions.

### Add a new skill
1. Create `skills/your-skill/SKILL.md` following the existing pattern
2. Reinstall: `claude plugin uninstall exec-kit && claude plugin install exec-kit`
