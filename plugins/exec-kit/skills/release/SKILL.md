---
name: release
description: Full release orchestrator — runs the complete project setup sequence from kickoff through release plan, risk register, and first cycle plan, pausing for approval at each step. Use when kicking off a new product or feature build to produce the full execution package before development begins.
disable-model-invocation: true
---

Run the full release setup for: $ARGUMENTS

Work through each phase below sequentially. After completing each phase, present the output and ask: "Ready to continue to the next step, or would you like to revise anything?"

---

## Phase 0 — Methodology Choice

Before anything else, ask:

> *"Do you prefer to work in sprints (fixed time-box, typically 1–2 weeks) or continuous flow (pull work as capacity opens, Kanban-style)?*
>
> For a 1–2 person team, I'd suggest **continuous flow** — no fixed sprint commitments, easier to handle interruptions, simpler to run. But sprints work well if you like a defined rhythm and regular retrospectives. Which fits better?"*

Confirm the choice and carry it through all subsequent phases.

**Checkpoint 0**: Confirm methodology before proceeding.

---

## Phase 1 — Project Kickoff

Produce a kickoff document following the process and template of the `/kickoff` skill:
- Define what's being built, why now, and what success looks like
- Set explicit scope boundaries (in scope, out of scope, deferred to v1.1)
- Define team roles and decision authority
- Set the working rhythm based on the methodology choice from Phase 0
- Define communication norms and where decisions are logged
- Set up the project folder structure

**Checkpoint 1**: Get approval before proceeding to the release plan.

---

## Phase 2 — Release Plan

Produce a release plan following the process and template of the `/release-plan` skill:
- Define phases and milestones with target dates
- Build the dependency map — what blocks what
- Sequence the build foundation-first across 6 layers (infrastructure → foundation → core → features → integration → launch)
- Identify the critical path and parallel workstreams
- Define go/no-go criteria for each phase gate
- Set risk checkpoints at key inflection points
- Build the launch readiness checklist

After presenting the release plan, offer: *"Want me to run the `plan-reviewer` agent to check the plan for over-commitment, missing dependencies, or build-order issues before we proceed?"*

**Checkpoint 2**: Get approval before proceeding to the risk register.

---

## Phase 3 — Risk Register

Produce an initial risk register following the process and template of the `/risk` skill:
- Systematically identify risks across schedule, scope, technical, resource, and external categories
- Score each risk (likelihood × impact)
- Define mitigations for all risks scoring 3+
- Flag any unmitigated high risks for immediate attention

**Checkpoint 3**: Get approval before proceeding to the first cycle plan.

---

## Phase 4 — First Cycle Plan

Produce the first cycle plan following the process and template of the `/cycle-plan` skill:
- Confirm which build layer the first cycle draws from (typically Layer 1 — Infrastructure)
- Assess capacity for the cycle
- Select and sequence work items
- Check all dependencies
- Set the cycle goal

**Checkpoint 4**: Present the complete release setup package.

---

## Final Deliverable Summary

Output a clean summary:

```
## [Project Name] — Release Setup Package

**Status**: Ready to execute
**Completed**: [Date]
**Methodology**: Sprints | Flow (Kanban)
**Target launch**: [Date]

### Documents Produced
- Project Kickoff
- Release Plan (phases, milestones, build sequence, dependency map)
- Risk Register ([N] risks identified, [N] high-priority)
- Cycle 1 Plan (Layer 1 — Infrastructure)

### First Three Actions
1. [Most important thing to do first]
2. [Second most important thing]
3. [Third most important thing]

### Top Risks to Watch
1. [Risk] — [Mitigation]
2. [Risk] — [Mitigation]
```
