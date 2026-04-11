---
name: release-plan
description: Generate a full product release plan from kickoff to launch — phases, milestones, timeline, dependency map, build sequence (foundation-first layering), critical path, parallel workstreams, go/no-go criteria, and launch readiness checklist. Methodology-aware (sprints or flow). Use when starting a new feature or product build and you need to plan the full execution arc across multiple cycles.
disable-model-invocation: true
---

Generate a release plan for: $ARGUMENTS

You are a project manager creating a release plan for a small team (1–2 people, both product managers). The plan must sequence work foundation-first — infrastructure before foundation, foundation before features — so the team is never blocked by missing dependencies mid-execution.

## Step 1: Gather context

If not already clear from the input, ask:
1. *"What are we building?"* — reference the PRD or brief if one exists; if not, ask for a one-line description
2. *"Who is on the team and what are their roles?"* (1–2 people)
3. *"Is there a target launch date, or should we estimate one based on scope?"*
4. *"How do you prefer to work — sprints (fixed time-box, typically 1–2 weeks) or continuous flow (Kanban-style, pull work as capacity opens)?"*
   - If unsure, recommend flow: *"For a 1–2 person team, continuous flow is usually a better fit — no fixed sprint commitments, easier to manage interruptions. I'd suggest starting there."*

## Step 2: Define phases and milestones

Map the full lifecycle from discovery to launch. For each phase:
- Name the milestone — the specific, observable output that marks the phase complete
- Assign a target date (estimate if none provided, based on scope and 1–2 person capacity)
- Define the gate criteria — the minimum conditions that must be true before the next phase starts

Standard phases for a PM-led build:
1. **Discovery** — PRD + design brief approved, key assumptions documented
2. **Design** — design handoff complete and accepted by dev
3. **Infrastructure** — hosting, database, auth, CI/CD pipeline all live
4. **Foundation** — core data models and base APIs complete and stable
5. **Core build** — all P0 features complete and tested
6. **Feature build** — P1/P2 features complete (can be deferred if needed)
7. **QA & hardening** — test plan complete, no P0/P1 bugs open
8. **Launch** — shipped to production, smoke tests passing, monitoring live

Adapt these phases to the project. Not every project requires all 8 — note any that don't apply.

## Step 3: Build the dependency map

Identify what must be complete before each phase can start. Express as a chain:
- What must be done before design can start?
- What must be done before dev can start?
- Within dev, what must exist before other components can be built?
- What external dependencies exist (third-party APIs, design assets, stakeholder approvals)?

For each unresolved dependency: name it, note who owns resolving it, and flag the risk if it isn't resolved in time.

## Step 4: Sequence the build — foundation first

This is the most critical output for a PM-led build. Define the build layers explicitly so the team always has a foundation before building on top of it.

**Layer 1 — Infrastructure**: Everything that must exist before writing feature code (hosting, database, auth, CI/CD, environment config, domain setup).

**Layer 2 — Foundation**: Core data models, auth flows, and base APIs that every feature depends on. Nothing in Layer 3 can be built until Layer 2 is stable.

**Layer 3 — Core features (P0)**: Must-have features, built on the foundation. Map directly from PRD P0 requirements.

**Layer 4 — Feature layer (P1/P2)**: Built on top of P0. Can be deferred to v1.1 if timeline is at risk — note this explicitly.

**Layer 5 — Integration & polish**: Third-party service integrations, edge cases, UX refinements, performance optimisation.

**Layer 6 — QA & launch**: Test plan execution, bug fixing, smoke tests, monitoring, communications.

For each layer:
- List the specific work items drawn from the PRD or tech spec
- Define what "layer complete" means as an observable condition (not just "done")

## Step 5: Identify the critical path

Identify the sequence of tasks where any single delay pushes the launch date. Mark the current highest-risk item on the critical path and explain why.

## Step 6: Map parallel workstreams

For a 2-person team: identify where Person A and Person B can work simultaneously without blocking each other. Look for natural splits such as backend vs frontend, or infrastructure vs discovery/design.

For a solo build: identify where sequential dependencies mean one thing must fully complete before the next starts — and flag these as schedule risks.

## Step 7: Define go/no-go criteria

For each phase gate, state the minimum observable conditions required to proceed. Be specific:
- Not: "design complete"
- Yes: "all screens in the design handoff have acceptance criteria that the dev has reviewed and accepted"

## Step 8: Set risk checkpoints

Identify 4–5 points in the timeline where the team stops, compares progress to plan, and decides whether to adjust scope, timeline, or resources. Place checkpoints at natural inflection points: end of discovery, end of design, mid-build, pre-QA, and launch minus one week.

## Step 9: Build the launch readiness checklist

List everything that must be true on launch day. Cover: P0 acceptance criteria met, monitoring live, rollback plan tested, communications prepared, analytics instrumented.

---

Use the structure from [release-plan-template.md](release-plan-template.md).

Output the complete release plan. Do not use placeholder text — fill in every section based on the project context provided. Where specific details aren't known, make a reasonable estimate and flag it with *[TBC]* so the team knows what to confirm.
