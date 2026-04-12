---
name: cycle-plan
description: Plan a single work unit scoped to the active project phase. For Phase A (PM+Design alignment), plans an iteration round. For Phase B (Tech Design), plans a constraint-resolution round. For Phase C (Dev build), plans a sprint or Kanban cycle. Adapts depth to project tier. Use at the start of each round or cycle.
disable-model-invocation: true
---

Plan a work unit for: $ARGUMENTS

You are helping a small team plan focused, achievable work. The format depends on the current project phase.

## Step 0: Confirm project phase and tier

Ask if not already clear:

*"Which phase is the project in — (A) PM + Design alignment, (B) Tech design, or (C) Dev build?"*

If not already known, also ask: *"What tier is this project — Micro (days–2 weeks), Small (2–6 weeks), Medium (6–16 weeks), or Large (16+ weeks)?"*

Then route to the appropriate section below.

---

## Phase A — Iteration Round Plan (PM + Design alignment)

*Plan one iteration round: which PRD sections PM will work on, which screens Designer will work on, what question this round resolves.*

**Tier 1**: List what the PM will write and what design work (if any) will happen. One goal sentence.

**Tier 2–4**:

**Step A1: Confirm round context**
- Which round number is this?
- What open questions or unresolved items are carried forward from the previous round?
- Is this the first round? If so, what is the current state of the PRD (draft / not started)?

**Step A2: Set round scope**
- Which PRD sections will PM draft or revise this round?
- Which screens will Designer create or revise?
- What is the one key question this round must resolve before the next round can start?

**Step A3: Assign parallel work**
- PM and Designer work in parallel — identify the split and the sync point
- Neither should wait for the other to finish before starting; the sync point is where they compare outputs

**Step A4: Set the round goal**
- One sentence: what does a successful round look like?
- Observable condition for "round complete" — e.g., *"PM has updated sections 3–5, Designer has revised the onboarding flow, and the question about notification preferences is resolved."*

**Step A5: Confirm deferred items**
- What was considered for this round but pushed to the next? Why?

Offer: *"Want me to run the `requirements-gap-finder` agent to stress-test the current PRD before Design starts this round?"*

**Write state** (standalone use only — skip if running within `/run`): Update `[project]-state.md` — round number, round scope (PRD sections / screens in scope), open questions carried forward.

---

## Phase B — Constraint Resolution Round Plan (Tech Design)

*Plan one review round: which components Eng will review, which constraints PM/Design will respond to.*

**Tier 1–2**: Single session — Eng flags blockers, PM/Design resolve. List the components to review and the expected outputs. No formal round structure needed.

**Tier 3–4**:

**Step B1: Confirm round context**
- Which round number is this?
- What open constraints are carried forward from the previous round?
- For Round 1: confirm Eng has the PRD and design handoff

**Step B2: Set round scope**
- Which components, features, or systems will Eng review this round?
- Which open constraints will PM/Design respond to?
- Any constraints requiring further Eng investigation before PM/Design can respond?

**Step B3: Assign parallel work**
- Eng reviews can run in parallel with PM/Design responses to previous-round constraints
- Identify the sync point: when all three will review findings and responses together

**Step B4: Set the round goal**
- What does a successful round look like?
- How many open constraints should be resolved by end of round?

**Write state** (standalone use only — skip if running within `/run`): Update `[project]-state.md` — round number, components under review, open constraints carried forward.

---

## Phase C — Dev Cycle Plan (Dev build)

*Plan a sprint or Kanban cycle from the release plan backlog.*

Apply the appropriate depth:
- **Tier 1 (Micro)**: Produce a simple ordered task list with a one-sentence goal. Skip all formal steps below.
- **Tier 2 (Small)**: Run Steps C1–C4 and C7–C8 only. Skip Steps C5 and C6.
- **Tier 3–4 (Medium/Large)**: Run all steps.

**Step C1: Establish context**

Ask if not already provided:
1. *"Which cycle number is this, and what are the start and end dates?"*
2. *"Which build layer of the release plan are we in?"*
3. *"What's the available capacity this cycle?"* — days per person, noting any absences or commitments
4. *"How many people are contributing?"* — confirm or recommend methodology:
   - **1–2 people**: default to **Kanban** — weekly planning horizon, items can be added as capacity opens
   - **3–5 people**: **Scrum with 1-week sprints** — time-boxed, locked backlog
   - **5+ people**: **Scrum with 2-week sprints** — full sprint rhythm

If methodology is already established from the release plan, apply it consistently.

**Step C2: Check the layer gate**

Before selecting any work, verify:
- What layer should this cycle draw from?
- Is the gate to that layer open? (Are all prerequisites from the previous layer complete?)
- If any prerequisites are incomplete: address those first — do not advance to the next layer until the current one is stable

**Step C3: Apply capacity**

Calculate effective capacity:
- Take available days per person
- Apply a 20% buffer for unplanned work, reviews, and coordination
- Express work items in S/M/L sizing (S = ~1 day, M = ~2–3 days, L = ~4–5 days)
- Warn if selected work exceeds effective capacity and suggest what to defer

**Step C4: Select and sequence work**

From the backlog for the current layer:
- Select items that fit within capacity
- Sequence by dependency: items that other items depend on go first
- Flag any item with an unresolved dependency as a risk, not a commitment

**Step C5: Check for within-cycle dependencies**

For each selected item:
- Does it depend on another item in this same cycle? Sequence it later.
- Does it depend on something not yet complete from a previous cycle? Flag as blocked.
- Does it require an external input (design asset, third-party API, stakeholder decision)? Name it.

**Step C6: Assign work (2-person team) [Tier 3–4 only]**

Split work between two people based on natural parallel workstreams. Identify a sync point where work must merge.

**Tier 2**: Only call out parallel work if genuinely non-obvious. Skip the table.

**Step C7: Set the cycle goal**

One sentence: what does "done" look like at the end of this cycle, expressed as a user-observable or system-verifiable outcome.

**Step C8: Confirm deferred items**

List items considered but not included, with a brief reason. This prevents the same conversation next cycle.

**Write state** (standalone use only — skip if running within `/run`): Update `[project]-state.md` — cycle number, current build layer, selected work items and owners, cycle goal, deferred items.

---

**Phase C only**: Use the structure from [cycle-plan-template.md](cycle-plan-template.md). The template is designed for dev cycles — it includes Layer Check, Selected Work, and Definition of Done sections that are not applicable to Phases A or B.

For Phases A and B: use the structured output defined in the Phase A and Phase B steps above. No template needed.
