---
name: standup
description: Process status updates adapted to the current project phase. For Phase A (PM+Design alignment), structures iteration updates — PRD changes, design changes, and open cross-discipline questions. For Phase B (Tech Design), structures constraint updates — what Eng found, what PM/Design need to respond to. For Phase C (Dev build), processes daily standup updates into done/in-progress/blocked. Use whenever the team needs a structured shared view of status.
disable-model-invocation: true
---

Process status updates for: $ARGUMENTS

The format depends on the current project phase. Ask if not already clear: *"Which phase is the project in — (A) PM + Design alignment, (B) Tech design, or (C) Dev build?"*

---

## Phase A — Iteration Update (PM + Design alignment)

*Not a daily standup. Run at the end of a work session or when PM and Designer have outputs to compare.*

Accept input in any format — bullet points, free text, or a mix.

**Step A1: Parse PM and Designer updates separately**

Structure each person's update into:
- What changed in their work (PRD sections updated / screens created or revised)
- What decisions were made
- What is still open or flagged [TBC]

**Step A2: Identify cross-discipline open questions**

These are the most important output of the iteration update:
- Questions from Design that require PM to clarify or decide on requirements
- Questions from PM that require Design to explore or confirm feasibility
- Any inconsistencies between the current PRD state and the current design state

For each open question:
- State it clearly
- Note who needs to respond
- Flag urgency: does this block the next round, or can it carry forward?

**Step A3: Check for scope drift**

Are new requirements being introduced mid-round that weren't in the original scope? If so:
- Name the new requirement
- Flag whether it changes the timeline or resourcing
- Recommend: absorb into current scope / defer to v1.1 / escalate for a scope decision

**Step A4: Assess alignment health**

Brief assessment (1–2 sentences):
- Are PM and Design converging? Are open questions getting resolved faster than new ones are opening?
- If new questions keep opening: suggest a scope boundary conversation before the next round

**Write state**: Update `[project]-state.md` — replace the open questions list with the current set (resolved questions removed, new questions added with owners).

---

## Phase B — Constraint Update (Tech Design)

*Run after Eng has reviewed PM/Design outputs, or when PM/Design have responded to constraints.*

**Step B1: Parse updates by role**

Structure each role's update:
- **Eng**: constraints identified, components reviewed, questions for PM or Design
- **PM**: PRD sections updated in response to constraints, scope decisions made
- **Designer**: screens updated in response to constraints, design decisions made

**Step B2: Surface open constraints**

For each constraint still open:
- Name the constraint
- What decision or change is needed to resolve it (PM decision / Design change / Eng investigation)
- Who owns the next action and by when
- Impact if not resolved: what can't proceed until this is closed

**Step B3: Flag scope changes**

Did constraint resolution introduce new requirements or remove existing ones? Name them and flag whether they need a release plan update.

**Step B4: Assess resolution health**

Are constraints being resolved, or is Eng uncovering new ones at the same rate? If the latter, surface this explicitly — the team may need to timebox the tech design phase or narrow scope.

**Write state**: Update `[project]-state.md` — replace the open constraints list with the current set (resolved constraints removed, new constraints added with owners).

---

## Phase C — Daily Standup (Dev build)

*Process daily updates from 1–2 people. Concise — should take less than 5 minutes to read.*
*No state file write — daily standups are too frequent. State is written at cycle-level checkpoints in `/run` and `/retro`.*

**Step C1: Parse updates**

Accept input in any format. Organise by person, then by category: done / in progress / blocked.

**Step C2: Surface blockers immediately**

For each blocker:
- Name what is blocked
- Identify the cause (missing input, unresolved dependency, technical issue, decision needed)
- Suggest who needs to act and by when
- If a blocker has persisted more than 1 day, flag it as recurring — may need escalation

**Step C3: Flag decisions needed**

For anything requiring a decision before work can continue:
- State the decision clearly
- Note who has authority to make it
- Suggest a deadline — same-day blockers are urgent

**Step C4: Assess cycle health**

1–2 sentences:
- Is the cycle on track to meet its goal?
- Is any item running significantly longer than sized?
- Should anything be flagged for cycle plan review (rescoped, deferred, or escalated)?

---

Use the structure from [standup-template.md](standup-template.md).
