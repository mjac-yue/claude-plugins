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

Once confirmed, output a **Project Profile Card** — a compact reference the PM can pass to any other plugin orchestrator (`/pm`, `/design`, `/dev`) to set the default process level. Any step listed as "not default" can be added back at any time.

```
## Project Profile

**Project**: [Name]
**Tier**: [N — Micro / Small / Medium / Large]
**Team**: [N people]
**Methodology**: [Kanban / Scrum (cadence)]

### Cross-plugin defaults

| Plugin | Default | Not default — add back if needed |
|--------|---------|----------------------------------|
| pm-claude-kit | [skills included by default] | [skills not included by default] |
| design-ux-kit | [skills included by default] | [skills not included by default] |
| dev-workflow-kit | [skills included by default] | [skills not included by default] |
| exec-kit | [skills included by default] | [skills not included by default] |
```

Fill in the defaults based on the tier:

**Tier 1**:
- pm-claude-kit: one-sentence brief | `/prd`, `/competitive-analysis`, `/user-story`, `/prioritization`, `/roadmap`, `/rollout`
- design-ux-kit: informal description if UI changes | all skills
- dev-workflow-kit: inline task list + code | all planning and review docs
- exec-kit: task list + brief launch checklist | all other skills

**Tier 2**:
- pm-claude-kit: `/brief`, `/user-story` (2–3 key flows) | `/prd`, `/competitive-analysis`, `/prioritization`, `/roadmap`, `/rollout`
- design-ux-kit: `/ux-brief` (abbreviated), `/wireframe-spec` (key screens — doubles as handoff) | `/design-review`, `/usability-test`, `/design-handoff`
- dev-workflow-kit: `/dev-plan`, `/security-review` (if auth/data) | `/arch-design`, `/tech-spec`, `/api-spec`, `/perf-review`
- exec-kit: `/release-plan` (lightweight), `/cycle-plan`, `/standup`, `/retro` | risk register, `/status`, `/kickoff`

**Tier 3**:
- pm-claude-kit: `/prd`, `/user-story`, `/competitive-analysis`, `/prioritization` | `/roadmap`, `/rollout`
- design-ux-kit: `/ux-brief`, `/wireframe-spec`, `/design-review`, `/design-handoff` | `/usability-test`
- dev-workflow-kit: `/tech-spec`, `/dev-plan`, `/test-plan`, `/code-review`, `/security-review` | `/arch-design`, `/api-spec`, `/perf-review`
- exec-kit: `/release-plan` (full), `/cycle-plan`, `/standup`, `/retro`, `/status`, `/risk` (top 5) | nothing

**Tier 4**:
- All plugins: full workflow — everything included by default

*Pass the Project Profile Card as context when running `/pm`, `/design`, or `/dev`. Each orchestrator will use it as the starting point and will confirm before skipping anything — you can always ask to add a step back in.*

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
