---
name: retro
description: Run a retrospective adapted to the current project phase. For Phase A (PM+Design alignment), reviews whether the round resolved its open questions and whether PM and Design are ready to sign off or need another round. For Phase B (Tech Design), reviews whether constraints are resolved and all three roles are aligned. For Phase C (Dev build), runs a lightweight sprint or cycle retrospective. Use at the end of each round or cycle.
disable-model-invocation: true
---

Run a retrospective for: $ARGUMENTS

> **Learning note — Retrospective**
> Retrospectives are how teams improve over time rather than repeating the same patterns. By reflecting on what worked and what didn't at the end of each round or cycle — not just at the end of the project — small improvements compound into significant gains. The key is specificity: "communication was good" isn't actionable, but "writing decisions in the shared doc prevented a 3-way email thread" is. This skill adapts the format to the current project phase because the questions worth asking are different at each stage.

Display the learning note above verbatim to the user before proceeding.

The format depends on the current project phase. Ask if not already clear: *"Which phase is the project in — (A) PM + Design alignment, (B) Tech design, or (C) Dev build?"*

---

## Phase A — Round Review (PM + Design alignment)

*Lightweight — 15 minutes. Goal: determine whether this round resolved its questions, and decide to sign off or plan the next round.*

**Step A1: Gather round data**

Ask if not already provided:
1. *"What was the round goal?"*
2. *"Which PRD sections changed and what decisions were made?"*
3. *"Which screens were created or revised?"*
4. *"Are there any open questions still unresolved from this round?"*
5. *"Are PM and Designer ready to sign off, or does another round need to happen?"*

**Step A2: Assess convergence**

- Are open questions being resolved, or are new ones opening at the same rate?
- Did the round introduce any scope changes that affect the release plan timeline?
- If multiple rounds have passed: is there a pattern in what keeps staying open? Flag if so.

**Step A3: Sign-off decision**

**If ready to sign off**:
- Confirm both PM and Designer explicitly agree the PRD is final and all P0 screens are covered
- Note the sign-off in the release plan (Alignment Rounds table)
- Output: *"Phase A complete — ready for Tech Design (Phase B)"*
- **Write state**: Update `[project]-state.md` — Phase A status ✓ with sign-off dates, clear open questions list, set Current Position to Phase B Round 1.

**If another round is needed**:
- List exactly what remains open
- Confirm that the next round has a specific, bounded goal (not "keep working on the PRD")
- Warn if this is round 3+: consider whether scope needs to be cut to reach sign-off
- **Write state**: Update `[project]-state.md` — remaining open questions with owners, updated round number.

**Step A4: One process change**

Pick one small thing to do differently in the next round. Keep it testable.

---

## Phase B — Constraint Resolution Review (Tech Design)

*Lightweight — 15 minutes. Goal: determine whether all constraints are resolved and all three roles are aligned.*

**Step B1: Gather round data**

Ask if not already provided:
1. *"How many constraints were identified in total? How many are resolved?"*
2. *"What constraints are still open?"*
3. *"Did constraint resolution require any PRD or design changes? Are those changes complete?"*
4. *"Are PM, Designer, and Eng ready to sign off?"*

**Step B2: Assess resolution completeness**

- For each open constraint: is it blocked on a decision, more Eng investigation, or PM/Design output?
- Did constraint resolution introduce new requirements that aren't yet in the release plan?
- If so: flag scope impact before proceeding

**Step B3: Sign-off decision**

**If all three are aligned**:
- Confirm Eng accepts the final design handoff
- Confirm all PRD and design updates from constraint resolution are complete
- Note the three-way sign-off in the release plan (Tech Design Rounds table)
- Output: *"Phase B complete — ready for Dev build (Phase C)"*
- **Write state**: Update `[project]-state.md` — Phase B status ✓ with sign-off dates, clear open constraints list, set Current Position to Phase C Cycle 1.

**If another round is needed**:
- List what remains open with owners and target resolution round
- Confirm the next round has a specific goal
- **Write state**: Update `[project]-state.md` — remaining open constraints with owners, updated round number.

**Step B4: One process change**

Pick one small thing to do differently in the next round.

---

## Phase C — Dev Cycle Retrospective

*Lightweight — 15 minutes. Goal: honest reflection and one concrete change.*

**Step C1: Gather cycle data**

Ask if not already provided:
1. *"What was the cycle goal?"*
2. *"Which items were completed? Which were carried over?"*
3. *"What worked well this cycle?"*
4. *"What didn't work or slowed you down?"*
5. *"Is the release plan still on track?"*

**Step C2: Assess completion honestly**

- Calculate completion rate: items done vs items planned
- For carried-over items: identify why each wasn't completed (underestimated, blocked, deprioritised, out of scope)
- Flag a pattern if the same type of issue has caused carry-overs across multiple cycles

**Step C3: Structure what worked and what didn't**

- Group related points together
- Keep each point specific — not "communication was good" but "writing decisions in the shared doc prevented a 3-way email thread"

**Step C4: Define one action item per person**

One action per person, maximum. Must be specific and completable within the next cycle. Assign to a named person.

**Step C5: Identify one process change**

The single highest-value change to try next cycle. Small and testable.

**Step C6: Check the release plan**

- Is the team on track for the target launch date?
- Does any issue suggest a scope change, timeline adjustment, or resource constraint?
- What layer does the next cycle draw from?

**Write state**: Update `[project]-state.md` — completed items, carried-over items with reasons, next cycle number and layer focus, release plan health. If used standalone (outside `/run`), also update Key Decisions with any significant choices made this cycle.

---

Use the structure from [retro-template.md](retro-template.md).

## Save output

After presenting the retrospective:
1. **Write state** per the Write state instructions in the phase above — this is the primary persistence mechanism
2. Additionally, check if a project `CLAUDE.md` exists in the current working directory or any parent directory
3. If it contains an **Output paths** table, find the row for `/retro` (or a `retro-[N].md` pattern) and save the retrospective document to that path
4. If no output path is configured for `/retro`, save to `execution/retro-[cycle-number].md` in the project directory (e.g., `execution/retro-01.md`)
5. Confirm the file was written to the user
6. If no project directory exists, present the output for manual copying
