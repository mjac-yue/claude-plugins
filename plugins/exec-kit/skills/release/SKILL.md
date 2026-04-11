---
name: release
description: Full release orchestrator — assesses team size and project complexity to determine the right level of process, then runs the appropriate setup sequence from kickoff through release plan, risk register, and first cycle plan. Adapts output depth and document count to the project tier — no over-engineering small work. Use when kicking off any new product or feature build.
disable-model-invocation: true
---

Run the full release setup for: $ARGUMENTS

Work through each phase below sequentially. After completing each phase, present the output and ask: "Ready to continue to the next step, or would you like to revise anything?"

---

## Phase 0 — Project Profile

Before producing anything, establish the project profile. Ask two questions:

**Question 1: Team size**

*"How many people are actively contributing to this project?"*

**Question 2: Project scope**

*"How would you describe the size of this project?"*

> - **(A) Micro** — a single small change, bug fix, or simple improvement. Timeline: days to ~2 weeks. Scope is clear and unlikely to change.
> - **(B) Small** — one to three features with reasonably clear requirements. Some unknowns, but nothing major. Timeline: 2–6 weeks.
> - **(C) Medium** — multiple features or a meaningful product area. Some technical unknowns, likely some design work, a few external dependencies. Timeline: 6–16 weeks.
> - **(D) Large** — a full product, significant feature set, or high complexity. Multiple phases, design + dev, external integrations, multiple stakeholders. Timeline: 16+ weeks.

*If unsure, describe what you're building and I'll suggest the right tier.*

---

### Deriving the Project Tier

Based on team size and scope, determine the project tier and declare it before proceeding:

**Tier 1 — Micro**
*Signals*: Scope (A), or scope (B) solo with clear requirements and no unknowns.
*What this means*: No formal documentation needed. Produce a simple task list with build order and a brief launch checklist. Skip kickoff doc, release plan, and risk register.

**Tier 2 — Small**
*Signals*: Scope (B), 1–2 people. Or scope (C) with very clear requirements and no technical unknowns.
*What this means*: Lightweight release plan (phases + build sequence only — no dependency map, no critical path analysis, no parallel workstream table). No formal risk register unless a specific concern exists. Kickoff is a one-paragraph summary, not a full doc.

**Tier 3 — Medium**
*Signals*: Scope (C), any team size. Or scope (D) with a small team and well-understood requirements.
*What this means*: Full release plan with all sections, but risk register covers only the top 3–5 risks rather than being exhaustive. Kickoff doc is full but can skip sections that don't apply.

**Tier 4 — Large**
*Signals*: Scope (D), or any project with multiple teams, major unknowns, significant external dependencies, or a launch with real user or business risk.
*What this means*: Full process — all documents, all sections, all checkpoints.

Present the determined tier and methodology recommendation, then confirm:

> *"Based on what you've described, this looks like a **[Tier N — name]** project. I'll produce [describe what's included and what's skipped]. For a team of [N], I'd recommend **[Kanban / Scrum]** [brief reason].*
>
> *Does that match your sense of the project, or should we adjust the tier?"*

---

**Methodology by team size** (apply within the confirmed tier):
- **1–2 people → Kanban** (default): no sprint overhead, absorbs interruptions, WIP limits, ship when done
- **3–5 people → Scrum, 1-week sprints**: structured cadence, shared commitment, low ceremony overhead
- **5+ people → Scrum, 2-week sprints**: coordination cost justifies full sprint rhythm

**Checkpoint 0**: Confirm project tier and methodology before proceeding.

---

## Phase 1 — Kickoff

**Tier 1**: Skip. Note the goal and success definition in one sentence at the top of the task list.

**Tier 2**: Produce a one-paragraph kickoff summary covering: what's being built, who's building it, target date, scope boundaries (in/out), and how the two people will coordinate. No formal document.

**Tier 3–4**: Produce a full kickoff document following the process and template of the `/kickoff` skill:
- Define what's being built, why now, and what success looks like
- Set explicit scope boundaries (in scope, out of scope, deferred to v1.1)
- Define team roles and decision authority
- Set the working rhythm based on the confirmed methodology
- Define communication norms and where decisions are logged
- Set up the project folder structure

**Checkpoint 1**: Get approval before proceeding to the release plan.

---

## Phase 2 — Release Plan

**Tier 1**: Skip the release plan. Produce instead:
- An ordered task list grouped by build layer (infrastructure first, then foundation, then features)
- A brief launch checklist (5–8 items: smoke test, no open bugs, monitoring on)
- Estimated total time

**Tier 2**: Produce a lightweight release plan covering:
- Phases and milestones with target dates
- Build sequence (layers 1–6, with items per layer)
- Key dependencies (prose, not a full map — only note dependencies that are genuinely at risk)
- Launch readiness checklist (abbreviated — 8–10 items)
- Skip: dependency map diagram, critical path analysis, parallel workstream table, go/no-go criteria table, risk checkpoints

**Tier 3–4**: Produce the full release plan following the process and template of the `/release-plan` skill:
- Define phases and milestones with target dates
- Build the full dependency map
- Sequence the build foundation-first across 6 layers
- Identify critical path and parallel workstreams
- Define go/no-go criteria for each phase gate
- Set risk checkpoints
- Build the complete launch readiness checklist

After presenting (Tier 3–4 only), offer: *"Want me to run the `plan-reviewer` agent to check the plan before we proceed?"*

**Checkpoint 2**: Get approval before proceeding to the risk register.

---

## Phase 3 — Risk Register

**Tier 1**: Skip entirely.

**Tier 2**: Skip unless a specific risk was surfaced during planning. If one was, note it in one line: risk, likelihood, mitigation, owner. No formal register.

**Tier 3**: Produce a focused risk register covering the top 3–5 risks only. Score each (likelihood × impact). Define mitigations for score 4+. Skip the full systematic category sweep.

**Tier 4**: Produce the full risk register following the process and template of the `/risk` skill — systematic review across all risk categories, scored, owned, with mitigations for all score 3+.

**Checkpoint 3**: Get approval before proceeding to the first cycle plan.

---

## Phase 4 — First Cycle Plan

**All tiers**: Produce a cycle plan appropriate to the tier and methodology:

**Tier 1**: A simple ordered task list for the week with one goal sentence. No capacity table, no formal template.

**Tier 2**: Abbreviated cycle plan — goal, items in priority order, estimated size, one dependency check. Skip capacity table and parallel workstream section if solo.

**Tier 3–4**: Full cycle plan following the process and template of the `/cycle-plan` skill — layer gate check, capacity, dependency validation, parallel workstreams, cycle goal.

**Checkpoint 4**: Present the complete setup package.

---

## Final Deliverable Summary

Output a summary scaled to the tier:

```
## [Project Name] — Release Setup ([Tier N — name])

**Status**: Ready to execute
**Completed**: [Date]
**Tier**: [N — Micro / Small / Medium / Large]
**Methodology**: Kanban | Scrum ([cadence])
**Team**: [N people]
**Target launch**: [Date]

### Documents Produced
[List only what was actually produced for this tier]

### First Three Actions
1. [Most important thing to do first]
2.
3.

### Risks to Watch
[Top 1–2 risks if Tier 2+, or "None identified" for Tier 1]
```
