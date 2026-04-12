---
name: release
description: Full release orchestrator — assesses team size and project complexity to determine the right level of process, then runs the appropriate setup sequence from kickoff through release plan, risk register, and first cycle plan. Adapts output depth and document count to the project tier — no over-engineering small work. Use when kicking off any new product or feature build.
disable-model-invocation: true
---

Run the full release setup for: $ARGUMENTS

**Output standard — diagrams**: All documents are read in Obsidian. Use Mermaid syntax (` ```mermaid ` blocks) for every diagram — Obsidian renders these natively. Never use ASCII art for diagrams. Supported diagram types: `flowchart` (dependency maps, workflows), `gantt` (timelines), `erDiagram` (data models), `sequenceDiagram` (flows), `graph` (component relationships).

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

Based on team size and scope, suggest a starting tier. The tier is a **recommendation, not a constraint** — the user can add back any step or document at any point.

**Tier 1 — Micro**
*Signals*: Scope (A), or scope (B) solo with clear requirements and no unknowns.
*Default*: Simple task list with build order and a brief launch checklist. Formal docs not included by default.

**Tier 2 — Small**
*Signals*: Scope (B), 1–2 people. Or scope (C) with very clear requirements and no technical unknowns.
*Default*: Lightweight release plan (phases + build sequence), one-paragraph kickoff summary. Dependency map, critical path, risk register not included by default.

**Tier 3 — Medium**
*Signals*: Scope (C), any team size. Or scope (D) with a small team and well-understood requirements.
*Default*: Full release plan, full kickoff, focused risk register (top 3–5 risks).

**Tier 4 — Large**
*Signals*: Scope (D), or any project with multiple teams, major unknowns, significant external dependencies, or real user or business risk.
*Default*: Full process — all documents, all sections, all checkpoints.

Present the suggested tier and methodology, then confirm with an explicit opt-in/opt-out:

> *"Based on what you've described, this looks like a **[Tier N — name]** project. My suggested default is [describe what's included]. For a team of [N], I'd recommend **[Kanban / Scrum]** [brief reason].*
>
> *The tier is just a starting point — you can add back any step or document at any time. Does this look right, or would you like to adjust the scope of what we produce?"*

---

**Methodology by team size** (apply within the confirmed tier):
- **1–2 people → Kanban** (default): no sprint overhead, absorbs interruptions, WIP limits, ship when done
- **3–5 people → Scrum, 1-week sprints**: structured cadence, shared commitment, low ceremony overhead
- **5+ people → Scrum, 2-week sprints**: coordination cost justifies full sprint rhythm

Once confirmed, output a **Project Profile Card** — a compact reference that establishes the scope of work for each phase exec will manage. Any step listed as "not default" can be added back at any time.

```
## Project Profile

**Project**: [Name]
**Tier**: [N — Micro / Small / Medium / Large]
**Team**: [N people — note PM, Designer, Eng roles]
**Methodology**: [Kanban / Scrum (cadence)]

### Phase defaults

| Phase | Default work | Not default — add back if needed |
|-------|-------------|----------------------------------|
| A — PM + Design alignment | [PM deliverables and design deliverables included by default] | [what's skipped for this tier] |
| B — Tech design | [tech design depth for this tier] | [what's skipped] |
| C — Dev build | [dev layers and process included] | [what's skipped] |
```

Fill in the defaults based on the tier:

**Tier 1**:
- Phase A: one-sentence brief + informal UI description if needed | PRD, competitive analysis, user stories, UX brief, wireframes
- Phase B: single async review session — Eng flags blockers | no formal tech spec
- Phase C: ordered task list + brief launch checklist | all formal dev docs

**Tier 2**:
- Phase A: abbreviated PRD, 2–3 key user stories, UX brief, wireframes for key screens | competitive analysis, full prioritization, usability testing
- Phase B: one review round — Eng flags constraints, PM/Design resolve | no formal tech spec
- Phase C: lightweight release plan, cycle plans, standups, retros | risk register, status reports, kickoff doc

**Tier 3**:
- Phase A: full PRD, user stories, competitive analysis, RICE prioritization, UX brief, wireframe spec, design review, design handoff | usability testing, rollout plan
- Phase B: full tech design rounds until all three aligned | formal tech spec (include if complexity warrants)
- Phase C: full release plan, cycle plans, standups, retros, status reports, risk register (top 5) | nothing

**Tier 4**:
- All phases: full workflow — everything included by default

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
- Build sequence (layers 1–6, with items per layer) — leave Layer 1 items as TBD categories; specific tech choices are made in Phase B
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

## Phase 4 — First Round Plan

The first work unit is always a **PM round** — the starting point for Phase A (PM + Design alignment). This is not a dev cycle plan.

**All tiers**: Produce a first round plan for Phase A:

**Tier 1**: A simple ordered task list — what the PM will write and what (if any) design work will happen. One goal sentence. No capacity table.

**Tier 2**: Abbreviated round plan — which PRD sections to draft, which screens to sketch, key questions to resolve. Estimate time for PM and Designer. Note the sync point.

**Tier 3–4**: Full round plan following Phase A1 of the `/run` skill — confirm what's open, set round scope for PM and Designer, identify the key question this round resolves, set the sync point. Offer to run the `requirements-gap-finder` agent before Design starts.

After presenting, note:
> *"When PM + Design sign off on Phase A, run `/run` to move into Tech Design (Phase B). When all three are aligned, run `/run` to kick off the dev build (Phase C)."*

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

---

## State File — Create Initial State

After presenting the final deliverable summary above, create `[project-name]-state.md` in the project folder. This is the resume point for all future sessions using `/run`, `/retro`, `/cycle-plan`, and `/standup`.

Populate it using the format defined in `/run`. Initial values:
- **Current Position**: Phase A, Round 1
- **Phase A status**: Round 1 in progress — PRD: initial draft (or "not yet started"), Design: not started
- **Phase B status**: Not started
- **Phase C status**: Not started
- **Artifacts**: Populate with the file paths of documents produced during this setup (kickoff doc, release plan, risk register)
- **Key Decisions**: Record any significant scope or tier decisions made during setup

Then note to the user:
> *"State file created at `[project-name]-state.md`. Start every future session by opening this file or telling Claude to read it — this is how work resumes across days and sessions."*
