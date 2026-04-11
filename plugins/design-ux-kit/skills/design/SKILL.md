---
name: design
description: Full Design & UX workflow orchestrator — runs all phases from discovery through handoff, pausing for approval at each checkpoint. Use when starting a new design effort end-to-end.
disable-model-invocation: true
---

Run the full Design & UX workflow for: $ARGUMENTS

Work through each phase below sequentially. After completing each phase, present the output and ask the user: "Ready to continue to Phase [N+1], or would you like to revise anything?"

---

## Phase 1 — UX Brief

Produce a UX brief by running the `/ux-brief` skill.

- Define the design scope, target users, goals, constraints, and success criteria
- Surface any assumptions that need validation before design begins
- Identify what user research (if any) is needed before proceeding

After presenting the brief, offer: *"Want me to run the `user-research-planner` agent? It will assess whether formal user research is feasible or produce a faster assumption validation plan if it isn't — recommended before committing to a design direction."*

**Checkpoint 1**: Get approval before moving to Phase 2.

---

## Phase 2 — Information Architecture & Flow

Produce a wireframe specification by running the `/wireframe-spec` skill, based on the approved UX brief.

- Map the key screens, user flows, and navigation structure
- Define component inventory and interaction states for each screen
- Note any branching paths, error states, or edge cases

**Checkpoint 2**: Get approval before moving to Phase 3.

---

## Phase 3 — Design Review

Run a heuristic design review by running the `/design-review` skill against the wireframe spec.

- Evaluate against Nielsen's 10 usability heuristics
- Flag accessibility concerns (WCAG 2.1 AA)
- Surface inconsistencies, friction points, and missing states

After presenting the review, offer two options:
- *"Want me to run the `ux-reviewer` agent for a deeper structured audit? (Designer perspective — heuristics, accessibility, missing states)"*
- *"Want me to run the `pm-design-reviewer` agent to check coverage against your PRD or brief? (PM perspective — requirements coverage, user flow completeness, handoff readiness)"*

**Checkpoint 3**: Get approval (and incorporate any revisions) before moving to Phase 4.

---

## Phase 4 — Usability Test Plan

Produce a usability test plan by running the `/usability-test` skill.

- Define test objectives, participant criteria, and task scenarios
- Specify success metrics and how results will be analyzed
- Include a discussion guide outline

**Checkpoint 4**: Get approval before moving to Phase 5.

---

## Phase 5 — Design Handoff

Produce a design handoff spec by running the `/design-handoff` skill.

- Document every screen with component inventory, states, and interaction specs
- Define acceptance criteria engineering can verify
- List open questions and decisions deferred to implementation

After presenting the handoff spec, offer: *"Want me to run the `pm-design-reviewer` agent one final time against the complete handoff? It checks that every requirement is covered and the spec is specific enough for a developer to build without a sync meeting."*

**Checkpoint 5**: Present the complete handoff package. Confirm the design workflow is complete.
