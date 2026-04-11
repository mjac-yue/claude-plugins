---
name: cycle-plan
description: Plan a single work cycle (sprint or Kanban flow) from the backlog, scoped against the active release plan. Verifies the team is working from the correct build layer, checks dependencies, assesses capacity for a 1–2 person team, and identifies parallel workstreams. Use at the start of each sprint or at the weekly review to plan the next block of work.
disable-model-invocation: true
---

Plan a work cycle for: $ARGUMENTS

You are helping a small team (1–2 PMs) plan a focused, achievable work cycle. Every item selected must come from the correct layer in the release plan — do not pull work ahead of unresolved dependencies.

## Step 1: Establish context

Ask if not already provided:
1. *"Which cycle number is this, and what are the start and end dates?"*
2. *"Which phase and build layer of the release plan are we in?"*
3. *"What's the available capacity this cycle?"* — days per person, noting any absences or commitments
4. *"Are you working in sprints or flow?"*
   - For sprints: the cycle is time-boxed and the plan is locked at the start
   - For flow: the cycle is a planning horizon; items can be added if capacity opens

## Step 2: Check the layer gate

Before selecting any work, verify:
- What layer should this cycle be drawing from?
- Is the gate to that layer open? (Are all prerequisites from the previous layer complete?)
- If any prerequisites are incomplete: address those first — do not advance to the next layer until the current one is stable
- Flag any incomplete prerequisites explicitly: *"Layer [N] is not yet complete — [item] is still open. This cycle should finish [item] before starting Layer [N+1] work."*

## Step 3: Apply capacity

Calculate effective capacity:
- Take available days per person
- Apply a 20% buffer for unplanned work, reviews, and coordination
- Express work items in S/M/L sizing (S = ~1 day, M = ~2–3 days, L = ~4–5 days)
- Warn if the selected work exceeds effective capacity and suggest what to defer

## Step 4: Select and sequence work

From the backlog for the current layer:
- Select items that fit within capacity
- Sequence by dependency: items that other items depend on go first
- For each item, note what it depends on and whether that dependency is already resolved
- Flag any item with an unresolved dependency as a risk, not a commitment

## Step 5: Check for within-cycle dependencies

For each selected item:
- Does it depend on another item in this same cycle? Sequence it later.
- Does it depend on something not yet complete from a previous cycle? Flag as blocked — do not include until the blocker is resolved.
- Does it require an external input (design asset, third-party API, stakeholder decision)? Name the dependency and who owns it.

## Step 6: Assign work (2-person team)

Split work between the two people based on:
- Natural parallel workstreams (e.g., one on backend, one on design review or documentation)
- Avoiding both people being blocked by the same dependency
- Identifying a sync point where their work must merge or hand off

For a solo build: note which items must be done sequentially and flag any that represent a single-person bottleneck on the critical path.

## Step 7: Set the cycle goal

Write one sentence: what does "done" look like at the end of this cycle, expressed as a user-observable or system-verifiable outcome — not a list of tasks.

## Step 8: Confirm deferred items

List items that were considered but not included, with a brief reason (too large, dependency not ready, lower priority). This prevents the same conversation next cycle.

---

Use the structure from [cycle-plan-template.md](cycle-plan-template.md).
