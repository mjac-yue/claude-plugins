---
name: run
description: Cycle execution orchestrator — runs the full cadence for a single work cycle: planning, daily standups, retrospective, and status report, with the next cycle plan at the end. Use to manage the day-to-day and end-of-cycle rhythm once a release plan is in place.
disable-model-invocation: true
---

Run the cycle execution workflow for: $ARGUMENTS

Work through the cycle phases below. Standup processing can be run multiple times within a cycle — just provide the day's updates. The retrospective and status report run at the end of the cycle.

---

## Phase 1 — Cycle Planning

At the start of each new cycle, produce a cycle plan following the process and template of the `/cycle-plan` skill:
- Confirm which build layer this cycle draws from and that all layer prerequisites are met
- Assess team capacity
- Select and sequence work items from the current layer
- Check all within-cycle dependencies
- Assign parallel workstreams if 2-person team
- Set the cycle goal

After presenting the plan, offer: *"Want me to run the `plan-reviewer` agent to check this cycle plan for over-commitment or dependency issues before you start?"*

**Checkpoint 1**: Get approval before the cycle begins.

---

## Phase 2 — Daily Standup (run each day)

Process standup updates following the process and template of the `/standup` skill:
- Accept free-text or bullet-point updates from each person
- Structure into: done, in progress, blocked
- Surface blockers and decisions needed immediately
- Assess cycle health — is the team on track?

This phase can be run multiple times. Each run processes one day's updates.

**No checkpoint** — standups are continuous. Flag anything requiring a cycle plan revision.

---

## Phase 3 — Retrospective (end of cycle)

Run a retrospective following the process and template of the `/retro` skill:
- Assess what was completed vs planned
- Surface what worked and what didn't
- Define one action item per person
- Define one process change to try next cycle
- Check whether the release plan is still on track

**Checkpoint 3**: Get approval before generating the status report.

---

## Phase 4 — Status Report (end of cycle)

Generate a stakeholder status report following the process and template of the `/status` skill:
- Set RAG status for schedule, scope, quality, and team
- Show progress against release plan phases and build layers
- Summarise what shipped this cycle and what's planned next
- Surface any open risks and decisions needed from stakeholders

**Checkpoint 4**: Present the end-of-cycle package.

---

## Phase 5 — Next Cycle Planning

Immediately roll into the next cycle plan following the process and template of the `/cycle-plan` skill:
- Carry over any incomplete items from this cycle with updated sizing
- Confirm the next build layer or continued work on the current layer
- Reassess capacity for the new cycle

---

## End-of-Cycle Summary

Output a clean handoff summary:

```
## [Project Name] — Cycle [N] Complete

**Cycle dates**: [Start] to [End]
**Cycle goal**: [Goal]
**Outcome**: Achieved / Partially achieved / Not achieved

### Completed
- [Item]
- [Item]

### Carried to Cycle [N+1]
- [Item] — [Reason]

### Release Plan Status
- Current phase: [Phase name]
- Current layer: Layer [N] — [Name]
- Launch target: [Date] — On track / At risk

### Cycle [N+1] Focus
Layer [N] — [Layer name] | [Cycle goal for next cycle]
```
