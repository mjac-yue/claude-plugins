# Exec Kit

A Claude Code plugin for project execution. Covers the full delivery lifecycle for a 1–2 person PM-led team — from project kickoff through release planning, cycle execution, retrospectives, and stakeholder reporting. Methodology-aware: works with sprints or continuous flow (Kanban).

## What's Included

### Orchestrators

| Command | Description |
|---------|-------------|
| `/release [project or feature]` | Full release setup — kickoff, release plan, risk register, and first cycle plan with checkpoints |
| `/run [cycle details]` | Cycle execution — planning, daily standups, retrospective, status report, and next cycle plan |

### Skills (Slash Commands)

| Command | Description |
|---------|-------------|
| `/release-plan [project description]` | Full release plan — phases, milestones, foundation-first build sequence, dependency map, critical path, go/no-go criteria, and launch readiness checklist |
| `/cycle-plan [cycle details]` | Single cycle plan — work selection from correct build layer, capacity check, dependency validation, parallel workstreams |
| `/standup [updates from each person]` | Structure daily updates into done/in-progress/blocked, surface blockers and decisions needed |
| `/retro [cycle summary]` | Lightweight retrospective — what worked, what didn't, one action per person, one process change |
| `/status [project and cycle context]` | Stakeholder status report — RAG status, progress against release plan, risks, decisions needed |
| `/risk [project context]` | Risk register — identify, score (likelihood × impact), define mitigations and owners |
| `/kickoff [project description]` | Project kickoff doc — scope, team roles, decision authority, working rhythm, communication norms |

### Agents

| Agent | Description |
|-------|-------------|
| `plan-reviewer` | Reviews a release or cycle plan for over-commitment, missing dependencies, wrong build-layer sequencing, and feasibility for a 1–2 person team |
| `blocker-coach` | Diagnoses a blocker's root cause, generates unblocking options (resolve, workaround, descope, escalate), and drafts any communications needed |

Agents are invoked automatically by Claude when relevant, or you can ask directly: *"Use the plan-reviewer agent to check this release plan."*

---

## Installation

### Install from GitHub

```bash
claude plugin marketplace add github:mjac-yue/claude-plugins
claude plugin install exec-kit
```

### Verify installation

```bash
claude plugin list
```

---

## Usage Examples

### Start a new project end-to-end
```
/release Build a notification preferences feature — users control which emails they receive
```

### Run a cycle (planning through retro)
```
/run Cycle 3 — we're in Layer 3 core build, 2 people, 10 days available
```

### Generate the release plan only
```
/release-plan CSV export feature — async job queue, S3 storage, email delivery when ready
```

### Plan the next sprint or flow cycle
```
/cycle-plan Cycle 4, Layer 3 core build, Person A 4 days Person B 3 days, sprint
```

### Process today's standup
```
/standup Person A: finished auth endpoints, working on user profile API, no blockers. Person B: design handoff reviewed and accepted, starting on frontend component library, blocked on Figma access from engineering team.
```

### End-of-cycle retrospective
```
/retro Cycle 3 — completed 4 of 6 items, carried over 2. Auth took longer than sized. Parallel work between frontend and backend went well.
```

### Weekly status report
```
/status Week 5, building Layer 3, 2 of 5 P0 features complete, on track for end-of-month launch
```

### Review the release plan before starting
```
Use the plan-reviewer agent to review this release plan
```

### Diagnose a blocker
```
Use the blocker-coach agent — we're blocked on the payment integration because the third-party API sandbox isn't returning consistent responses and we can't test our implementation
```

---

## How It Fits in the Suite

```
pm-claude-kit     →  what to build (PRD, stories, roadmap)
exec-kit          →  how to execute it (release plan, cycles, standups, status)
design-ux-kit     →  design the solution
dev-workflow-kit  →  build and ship it
```

The `/release-plan` skill is designed to receive its inputs from pm-claude-kit outputs (PRD, user stories, RICE prioritisation) and feed its build sequence into dev-workflow-kit's `/dev-plan`.

---

## Methodology

The plugin recommends a methodology based on your team size — asked automatically at the start of `/release` and `/cycle-plan`.

| Team size | Default recommendation | Reason |
|-----------|----------------------|--------|
| **1–2 people** | **Kanban** | No sprint ceremony overhead; absorbs interruptions; WIP limits prevent context-switching; ship when done, not when sprint ends |
| **3–5 people** | **Scrum (1-week sprints)** | Structured cadence helps coordinate; short sprint keeps planning overhead low |
| **5+ people** | **Scrum (2-week sprints)** | Coordination cost at this size benefits from sprint rhythm and ceremonies |

You can override the recommendation — the plugin explains the trade-offs and confirms your choice before proceeding.

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
