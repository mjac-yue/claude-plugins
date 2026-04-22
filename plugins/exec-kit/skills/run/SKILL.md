---
name: run
description: Full lifecycle execution orchestrator — manages work across all three project phases (PM+Design alignment, Tech Design, Dev build). Each phase has its own work unit and cadence. PM+Design runs iteration rounds until mutual sign-off. Tech Design runs constraint-resolution rounds until all three roles align. Dev runs sprint or Kanban cycles with daily standups, retrospectives, and status reports. Use to manage the day-to-day rhythm once a release plan is in place.
disable-model-invocation: true
---

Run the lifecycle execution workflow for: $ARGUMENTS

> **Learning note — Lifecycle Execution**
> The /run skill is the full lifecycle manager — it tracks where you are across phases, manages transitions between them, and ensures the right work happens in the right order. Product development is rarely linear: sessions are interrupted, decisions from one phase affect previous ones, and context gets lost between work sessions. The state file that /run maintains is what makes it possible to pick up exactly where you left off, without spending the first 20 minutes of each session reconstructing what was decided.

Display the learning note above verbatim to the user before proceeding.

**Output standard — file writing**: Write all deliverables directly to their output files. Do not print full document content to the terminal. At the end of each checkpoint, present a **Review before continuing** block listing every file written and what changed, so the user knows exactly what to open before approving. Format:

> **Review before continuing**
> - `[file path]` — [one line: what was written or updated]
> - `questions.md` — [N new questions added, e.g. "2 P0, 1 P1"] *(omit if none)*

**Questions gate standard — applies at every checkpoint throughout this skill**: Before completing any checkpoint, check `questions.md` for open questions:
- Any open **P0** question → stop; resolve with the user now, record the decision and date in `questions.md` (moving the row to Resolved Decisions), update every document listed in the "Affected docs" column, then continue
- Any open **P1** question → flag to user; must be resolved before the current phase can sign off
- **P2** questions → note and carry forward

**Logging questions**: Whenever a question is surfaced during this skill — in iteration updates, constraint reviews, standup blockers, or any other context — write it to `questions.md` immediately with: question text, priority (P0/P1/P2), phase raised, owner, and affected documents. Do not store questions only in the state file; the log is the single source of truth.

**Release plan update standard — applies throughout this skill**: The release plan file (path listed in the project `CLAUDE.md` output paths table, or `[project]-release-plan.md` by default) is the live source of truth for phase status, layer completion, actual dates, and scope. It must be written to — not just referenced — at each of the following events:

| Event | What to update in the release plan file |
|-------|----------------------------------------|
| Phase A sign-off (A3) | Mark PM Layer and Design Layer rows as Complete with actual date; mark all Phase A gate criteria as met |
| Tech stack agreed (B2) | Replace TBD placeholders in Layer 1 with confirmed hosting, database, auth, and CI/CD choices |
| Phase B sign-off (B3) | Mark Tech Design Layer as Complete with actual date; update any layer scope affected by constraint resolutions |
| Build layer complete (C3) | Mark completed work items and the layer row as Done with actual date; update planned vs. actual dates for the current position |
| End-of-cycle status (C4) | Update the overall timeline health — adjust future layer dates if this cycle slipped or completed early |
| Test gate passed (D1–D3) | Mark the corresponding QA & Launch layer sub-item as passed with the actual date |
| Project complete (D6) | Mark all remaining layers Done; record actual launch date against planned |

At each of these events, open the release plan file, make the specific updates, and confirm to the user which file was written. Never leave the release plan as a kickoff snapshot — every phase completion must be reflected in the file before the checkpoint is closed.

Work through the phases below. First determine which project phase is active, then apply the appropriate execution model. The work unit, standup format, and retro format all differ by phase.

---

**Navigation standard — applies at every phase transition**

At the completion of each major phase (A, B, C) and at the end of each cycle summary, always append a **What's next?** block. Use this exact format:

> **What's next?** [Recommended next step]
>
> **Optionally run at this point:**
>
> | Skill / Agent | Plugin | What it does |
> |--------------|--------|-------------|
> | `name` | kit | One-line description |
>
> *Reply with the name of anything you'd like to run, or say "continue" to proceed.*

If no optional skills or agents apply, omit the table and just show the next step recommendation.

**Phase transition lookup table — use this to populate the block:**

| At this transition | Recommended next step | Optional to run |
|-------------------|----------------------|-----------------|
| Phase A — Round Planning (A1) | Begin PM + Design work for this round | `requirements-gap-finder` agent *(pm-claude-kit)* — stress-test PRD before Design starts; `/prd` skill *(pm-claude-kit)* — generate or refine the PRD |
| Phase A — Sign-off (A3) | Phase B — Tech Design | `prd-reviewer` agent *(pm-claude-kit)* — final PRD critique before sign-off |
| Phase B — Round Planning (B1) | Begin Eng review for this round | `arch-reviewer` agent *(dev-workflow-kit)* — architecture quality audit; `pm-tech-reviewer` agent *(dev-workflow-kit)* — translate technical decisions for PM |
| Phase B — Sign-off (B3) | Phase C — Dev Build | `/tech-spec` skill *(dev-workflow-kit)* — formal tech spec if not yet produced; `/dev-plan` skill *(dev-workflow-kit)* — ordered build task list |
| Phase C — Cycle Planning (C1) | Begin development cycle | `plan-reviewer` agent *(exec-kit)* — check cycle plan for over-commitment and dependency issues |
| Phase C — Retrospective (C3) | Next cycle or Phase D | `blocker-coach` agent *(exec-kit)* — diagnose any unresolved blockers from this cycle |
| Phase C — All layers complete *(final)* | Phase D — Testing & Launch | `/risk` skill *(exec-kit)* — review open risks before entering testing |
| Phase D — D1 Automated Tests | Phase D — D2 PM Requirements Test | No additional agents at this point |
| Phase D — D2 PM Requirements Test | Phase D — D3 Design Conformance Test | No additional agents at this point |
| Phase D — D3 Design Conformance Test | Phase D — D4 Bug Triage | `code-reviewer` agent *(dev-workflow-kit)* — line-level review of bugs found |
| Phase D — D4 Bug Triage | Phase D — D5 Risk Clearance | `blocker-coach` agent *(exec-kit)* — diagnose any bugs blocking launch |
| Phase D — D5 Risk Clearance | Phase D — D6 Rollout | No additional agents at this point |
| Phase D — D6 Rollout *(final)* | **Project complete** | `/status` skill *(exec-kit)* — final stakeholder status report; `/retro` skill *(exec-kit)* — end-of-project retrospective |

---

## State File — Session Continuity

This skill writes and reads a persistent state file named `[project-name]-state.md` in the project folder. This file is the resume point for every new session.

**At the start of every session**: Before asking any questions, check whether `[project-name]-state.md` exists. If it does, read it and present a brief resume summary:

> *"Resuming [Project]. Currently in Phase [A/B/C], Round/Cycle [N]. [One sentence on what's open or in progress]. Ready to continue?"*

Confirm with the user before proceeding. If no state file exists, proceed with Phase 0 as normal.

**After every checkpoint**: Write or update `[project-name]-state.md` using the format below. Never skip this — it is what makes the next session possible.

### State file format

```markdown
# [Project Name] — Execution State
> Last updated: [Date] — [Checkpoint name, e.g. "Phase A Round 2 sign-off"]

## Current Position
**Phase**: A — PM+Design alignment | B — Tech design | C — Dev build
**Round / Cycle**: [N]
**Tier**: [N — name] | **Methodology**: [Kanban / Scrum]

---

## Phase A — PM + Design Alignment
**Status**: Not started | Round [N] in progress | ✓ Complete [Date]
**PM sign-off**: Pending | ✓ [Date]
**Designer sign-off**: Pending | ✓ [Date]

**Open questions** (carrying into next round):
- [Question] — Owner: [PM / Designer]

**PRD**: [file path or "not yet created"] — [initial draft / round N in progress / final]
**Design**: [file path or "not yet created"] — [not started / round N in progress / handoff ready]

---

## Phase B — Tech Design
**Status**: Not started | Round [N] in progress | ✓ Complete [Date]
**PM sign-off**: Pending | ✓ [Date]
**Designer sign-off**: Pending | ✓ [Date]
**Eng sign-off**: Pending | ✓ [Date]

**Open constraints**:
- [Constraint] — Owner: [PM / Designer / Eng]

---

## Phase C — Dev Build
**Status**: Not started | Cycle [N] in progress | ✓ Complete [Date]
**Current cycle**: [N] | **Current layer**: Layer [N] — [name]

**In progress**:
- [Item] — [Owner]

**Carried over**:
- [Item] — [Reason]

**Next cycle focus**: Layer [N] — [goal]

---

## Phase D — Testing & Launch
**Status**: Not started | In progress | ✓ Complete [Date]
**D1 — Automated tests**: Pending | ✓ Pass [Date] | ✗ Fail — [N bugs found]
**D2 — PM requirements test**: Pending | ✓ Pass [Date] | ✗ Fail — [N gaps found]
**D3 — Design conformance test**: Pending | ✓ Pass [Date] | ✗ Fail — [N discrepancies found]
**D4 — Bug triage**: Pending | In progress — [N P0] [N P1] [N P2] open | ✓ Complete [Date]
**D5 — Risk clearance**: Pending | ✓ Cleared [Date] | ✗ Hold — [blocking risk]
**D6 — Rollout**: Pending | ✓ Complete [Date]

**Open bugs**:
- [Bug] — P[0/1/2] — [Owner]

---

## Key Decisions
| Date | Phase | Decision |
|------|-------|----------|
| | | |

## Questions & Decisions Log
> Full log: `questions.md` — summary of open items below.

**Open P0 (blockers)**:
- (none) or [Question — Owner]

**Open P1 (must resolve before sign-off)**:
- (none) or [Question — Owner]

**Open P2 (carry forward)**:
- (none) or [Question — Owner]

## Artifacts

### Project
| Artifact | File | Status |
|----------|------|--------|
| Release plan | | Draft \| Active \| ✓ Complete [Date] |
| Risk register | | Not started \| Active \| ✓ Cleared [Date] |

### PM
| Artifact | File | Status |
|----------|------|--------|
| Brief | | Not started \| In progress \| ✓ Done [Date] |
| Competitive analysis | | Not started \| In progress \| ✓ Done [Date] |
| PRD | | Not started \| In progress \| ✓ Done [Date] |
| User stories | | Not started \| In progress \| ✓ Done [Date] |
| Prioritization | | Not started \| In progress \| ✓ Done [Date] |
| Roadmap | | Not started \| In progress \| ✓ Done [Date] |

### Design
| Artifact | File | Status |
|----------|------|--------|
| UX brief | | Not started \| In progress \| ✓ Done [Date] |
| Wireframe spec | | Not started \| In progress \| ✓ Done [Date] |
| HTML mockup | | Not started \| In progress \| ✓ Done [Date] |
| Design review | | Not started \| In progress \| ✓ Done [Date] |
| Usability test plan | | Not started \| N/A \| ✓ Done [Date] |
| Design handoff | | Not started \| In progress \| ✓ Done [Date] |

### Dev
| Artifact | File | Status |
|----------|------|--------|
| Arch design | | Not started \| In progress \| ✓ Done [Date] |
| Tech spec | | Not started \| In progress \| ✓ Done [Date] |
| API spec | | Not started \| N/A \| ✓ Done [Date] |
| Dev plan | | Not started \| In progress \| ✓ Done [Date] |
| QA test plan | | Not started \| In progress \| ✓ Done [Date] |
| Code review | | Not started \| In progress \| ✓ Done [Date] |
| Security review | | Not started \| In progress \| ✓ Done [Date] |
| Deployment guide | | Not started \| In progress \| ✓ Done [Date] |

---

## Document Sync Queue
> Artifacts flagged for review due to upstream changes. Remove each entry once the artifact has been reviewed and updated.

- (none)
```

---

## Phase 0 — Determine Current Project Phase

Ask if not already clear from the input:

*"Which phase is the project currently in?"*

> - **(A) PM + Design alignment** — PM and Design are iterating toward sign-off. No Eng resources engaged yet.
> - **(B) Tech design** — Eng is reviewing PM + Design outputs, identifying constraints. All three roles engaged.
> - **(C) Dev build** — PM + Design are signed off, Eng is building. Standups are daily, cycles are sprint or Kanban.
> - **(D) Testing & Launch** — Code is complete. Running automated tests, PM requirements test, design conformance test, bug triage, risk clearance, and rollout.

If the user provides standup updates or cycle context that makes the phase obvious, infer it rather than asking.

Once confirmed, ask:

**Optional feature opt-in**

*"A few optional quality checks are available throughout this workflow but off by default — would you like to enable any of them?"*

| Feature | What it does | Default |
|---------|-------------|---------|
| `requirements-gap-finder` at round start | Stress-tests the PRD for edge cases before Design starts each Phase A round | Off |
| `prd-reviewer` at Phase A sign-off | Structured critique of the PRD before PM and Designer sign off | Off |
| `plan-reviewer` at cycle start | Reviews each cycle plan for over-commitment and dependency issues before work begins | Off |
| `blocker-coach` on blockers | Diagnoses blockers surfaced in standups and produces structured unblocking options | Off |
| `/risk` at each phase transition | Runs a risk gate after each phase completes — surfaces new risks and asks whether to address before proceeding | Off |

Accept any selections. Note enabled features and invoke them automatically at the relevant checkpoints throughout the session — no need to ask again. Confirm: *"Got it — I'll run [X, Y] automatically at the relevant checkpoints. Let's continue."*

Jump to the relevant section below.

---

## Phase A — PM + Design Alignment

*Work unit: iteration round. Rounds continue until PM and Designer mutually sign off.*
*Roles: PM + Designer only. No Eng resources required.*

---

### A1 — Round Planning

At the start of each round, produce a round plan:

- Confirm which round number this is
- Review what's open from the previous round (open questions, unresolved PRD sections, screens that need work)
- Define the goal for this round: which PRD sections the PM will work on, which screens the Designer will work on
- Identify the key question or decision this round needs to resolve
- Set the sync point: when PM and Designer will compare outputs

After presenting the plan, offer: *"Want me to run the `requirements-gap-finder` agent to stress-test the current PRD before Design starts this round?"* (Requires pm-claude-kit to be installed.)

**Apply the Questions Gate** — check `questions.md` before confirming the round plan. Resolve any P0 questions now; flag P1 questions to the user; carry P2 forward. Update `questions.md` with any new questions surfaced during round planning.

**Checkpoint A1**: Confirm round scope before work begins.
**Write state**: Update `[project]-state.md` — current phase (A), round number, round scope (PRD sections / screens in scope), open P0/P1 questions summary (full log in `questions.md`).

---

### A2 — Iteration Update (run each round, can run mid-round)

Process updates from PM and Designer. Accept free-text or bullet-point input.

Structure into:

**PRD changes this round**
- What sections changed
- What decisions were made
- What is still open or flagged [TBC]

After summarising PRD changes, run the **downstream design impact check**: check the project `CLAUDE.md` status table for any design artifact that is no longer "Not started". For each one, the PRD changes may have invalidated assumptions it was built on. Flag affected artifacts and add them to the Document Sync Queue in `[project]-state.md`. Do not mark those artifacts as current until they have been reviewed and updated.

| Design artifact | If status is not "Not started" | Action |
|----------------|-------------------------------|--------|
| UX brief | Flag for update | Revisit problem framing and user goals against updated PRD |
| Wireframe spec | Flag for update | Revisit screen list and flows against updated requirements |
| HTML mockups | Flag for update | Revisit after wireframe spec is updated |
| Design review | Flag for update | Re-run once mockups are updated |
| Design handoff | Flag for update | Re-run once design review is complete |

**Design changes this round**
- What screens were created or revised
- What design decisions were made
- What screens are still open or need another pass

**Cross-discipline open questions**
- Questions from Design that require PM input
- Questions from PM that require Design input
- Decisions that need to be made before the next round can proceed

Write every question surfaced here to `questions.md` immediately — assign priority (P0 if it blocks the current round, P1 if it must resolve before sign-off, P2 otherwise), owner, and list every document that will need updating when it is resolved.

**Round health**
- Are PM and Design converging toward sign-off, or are new questions opening up?
- Is scope creeping? Flag if new requirements are being introduced mid-round.
- Suggest whether this round can close or needs to continue.

This phase can be run multiple times within a round. Each run processes one update cycle.

**Write state**: Update `[project]-state.md` — for each artifact flagged by the downstream design impact check, add an entry to the **Document Sync Queue** section (artifact name, date flagged, reason). Update the status of any PM or Design artifact that progressed this round (e.g., PRD from "Not started" to "In progress").

---

### A3 — Round Review and Sign-off Check

Run at the end of each round before deciding whether to start another:

**Apply the Questions Gate** — check `questions.md` before sign-off. All P0 questions must be resolved and affected documents updated. P1 questions block sign-off; they must be resolved here. Carry P2 forward.

**Phase A artifact completeness check** — before recommending sign-off, read the project `CLAUDE.md` and check the status of every required Phase A deliverable. Phase A is not complete until ALL of the following are Done:

| Workstream | Required artifact | Skill that produces it |
|------------|-------------------|----------------------|
| PM | Brief | `/brief` (done at kickoff) |
| PM | Competitive analysis | `/competitive-analysis` |
| PM | PRD | `/prd` — must have passed at least one `prd-reviewer` loop |
| PM | User stories | `/user-story` |
| PM | Prioritization | `/prioritization` |
| PM | Roadmap | `/roadmap` |
| Design | UX brief | `/ux-brief` |
| Design | Wireframe spec | `/wireframe-spec` |
| Design | HTML mockups | `/wireframe-html` |
| Design | Design review | `/design-review` |
| Design | Design handoff | `/design-handoff` |

For any artifact that is Not started or In progress: do not recommend sign-off. Instead, tell the user which artifact is missing and which skill to run next. Only once all rows show Done should sign-off be offered.

- Review all open questions from this round in `questions.md` — are any still unresolved?
- Assess PRD completeness independently of question resolution: are all P0 requirements defined with acceptance criteria? Has the PRD been through at least one `prd-reviewer` pass? Resolving open questions is necessary but not sufficient — the PM must explicitly confirm PRD quality meets the bar.
- Check for scope drift: did the round introduce new requirements that need to be scoped?

**Design → PM cascade check** — Before sign-off, review PM documents against the completed design artifacts. Design decisions frequently surface requirements gaps, scope adjustments, or new constraints that must flow back before the PM can meaningfully sign off. For each PM artifact that is not "Not started", check against the full set of completed design deliverables (UX brief, wireframe spec, HTML mockups, design review, design handoff):

| PM artifact | What to check |
|------------|---------------|
| PRD (`pm/prd.md`) | Do design decisions reveal missing, ambiguous, or conflicting requirements? |
| User stories (`pm/user-stories.md`) | Do new flows, edge cases, or states discovered in design need new or updated stories? |
| Brief (`pm/brief.md`) | Do design decisions affect stated scope, users, or success criteria? |

For each artifact with gaps, state exactly what needs updating and why. Apply PM document updates before sign-off. If no updates are needed, confirm explicitly: *"Design review found no changes required to PM documents."*

**Sign-off decision**:
- If all Phase A artifacts are Done AND the design → PM cascade check is complete (updates applied or confirmed none needed) AND all P0/P1 questions in `questions.md` are resolved AND the PM explicitly confirms PRD quality AND the Designer confirms design completeness → record sign-off and move to Phase B
- If any artifact is missing, or the cascade check has unresolved PM updates, or P0/P1 questions remain, or quality is not confirmed → identify exactly what is missing and direct the user to the appropriate skill before sign-off

Offer: *"Want me to run the `prd-reviewer` agent to check the PRD before you sign off?"* (Requires pm-claude-kit to be installed.)

**Update release plan**: Open the release plan file and mark the PM Layer and Design Layer rows as Complete with today's date. Mark all Phase A gate criteria as met. Confirm the file was written.

**Checkpoint A3**: Record sign-off or confirm what must be completed next.
**Write state**: Update `[project]-state.md` —
- Phase A status → ✓ Complete [Date]; PM sign-off ✓ [Date]; Designer sign-off ✓ [Date]
- Current Position → Phase B
- Artifacts table: mark every PM row (Brief, Competitive analysis, PRD, User stories, Prioritization, Roadmap) and every Design row (UX brief, Wireframe spec, HTML mockup, Design review, Usability test plan or N/A, Design handoff) as ✓ Done [Date] with the actual file path
- Clear any Document Sync Queue entries that were resolved during this sign-off
- Open P0/P1 questions summary → update to reflect all resolved

---

### A4 — Phase A Status

Summarise overall Phase A progress for stakeholders or the release plan:

```
## PM + Design Alignment — Status Update

**Project**: [Name]
**Round**: [N] of [estimated total]
**Status**: On track / Converging / Expanding (new questions opening)

### PRD status
- Sections complete: [N of N]
- Open items: [list]
- Last significant change: [what changed and why]

### Design status
- Screens complete: [N of N P0 screens]
- Open items: [list]
- Last significant change: [what changed and why]

### Open questions requiring resolution
[List — owner and target round]

### Sign-off status
PM: Signed off / Pending — [what's blocking]
Designer: Signed off / Pending — [what's blocking]

### Estimated rounds to completion
[N more rounds, or "ready for sign-off"]
```

---

### A5 — Next Round Planning

After sign-off or if continuing: roll into the next round plan following A1. Carry forward all unresolved questions with updated context.

---

## Phase B — Tech Design + Constraint Resolution

*Work unit: review round. Rounds continue until all three roles (PM, Designer, Eng) sign off.*
*Roles: All three engaged. Eng leads review; PM + Design respond to constraints.*

---

### B1 — Review Round Planning

At the start of each review round:

- Confirm which round number this is
- For Round 1: establish what Eng is reviewing (full PRD + design handoff, or specific components). Round 1 also includes tech stack determination — Eng proposes the hosting platform, database, auth system, CI/CD tooling, and any other foundational technical choices. These decisions unblock Layer 1 of the release plan, which was left TBD during initial planning.
- For subsequent rounds: review which constraints from the previous round are still open
- Define the goal for this round: which components Eng will review, which constraints PM/Design will respond to
- Set the sync point: when all three will review Eng's findings and PM/Design responses

**Apply the Questions Gate** — check `questions.md` before confirming the round plan. Resolve any P0 questions now; flag P1 questions; carry P2 forward. Write any new constraints or questions surfaced here to `questions.md`.

**Checkpoint B1**: Confirm round scope before work begins.
**Write state**: Update `[project]-state.md` — current phase (B), round number, components under review this round, open P0/P1 questions summary (full log in `questions.md`).

---

### B2 — Constraint Update (run each round)

Process updates from all three roles. Accept free-text or bullet-point input.

Structure into:

**Tech stack decisions (Round 1 only)**
- Proposed hosting platform: [what Eng recommends and why]
- Proposed database: [what Eng recommends and why]
- Proposed auth system: [what Eng recommends and why]
- Proposed CI/CD tooling: [what Eng recommends and why]
- Any other foundational technical choices: [e.g. language, framework, third-party services]

Once the tech stack is agreed, immediately open the release plan file and replace every TBD placeholder in Layer 1 with the confirmed choices. Do not defer this to B3 — the Layer 1 specifics must be in the file as soon as they are decided so the team can act on them. Confirm the file was written.

**Constraints identified by Eng**
- Technical constraint: [what the constraint is]
- Affected PRD section or design screen: [reference]
- Proposed resolution options: [what Eng suggests]
- Impact if unresolved: [what breaks or becomes infeasible]

**PM responses**
- PRD sections updated in response to constraints
- Scope decisions made (accept constraint / adjust requirement / defer feature)
- New requirements introduced by constraint resolution (flag these — they may need design work)

**Design responses**
- Screens updated in response to constraints
- Design decisions made to accommodate technical constraints
- Any new screens or flows introduced

**Cross-discipline open questions**
- Questions from Eng that need PM decisions
- Questions from Eng that need Design decisions
- Unresolved constraints requiring further investigation

Write every open question or unresolved constraint to `questions.md` immediately — assign priority (P0 if it blocks the round, P1 if it must resolve before Phase B sign-off, P2 otherwise), owner, and list all documents that will need updating when resolved.

**Round health**
- Are constraints being resolved, or are new ones being uncovered?
- Are PM/Design updates introducing scope that needs another Eng review?
- Suggest whether this round can close or needs to continue.

---

### B3 — Constraint Resolution Review and Sign-off Check

Run at the end of each review round:

**Apply the Questions Gate** — check `questions.md` before sign-off. All P0 questions must be resolved and affected documents updated. P1 questions block sign-off. Carry P2 forward.

- Review all open constraints and questions in `questions.md` — are any still unresolved?
- Confirm the tech stack is decided — hosting, database, auth, CI/CD. If not yet agreed, this is a blocker for Phase B completion.
- Confirm Layer 1 TBD placeholders were already replaced in the release plan file during B2. If not, do it now before proceeding.
- Check that all PRD and design updates are internally consistent.
- Confirm Eng has reviewed and accepted the latest design handoff.
- Check for scope changes: did constraint resolution add, remove, or resize any work items in the release plan layers? If yes, open the release plan file and update the affected layer rows before sign-off.

**Phase B artifact write** — Before sign-off, tech design decisions must be written to dev documents. These decisions exist only in the state file and conversation until this step runs. Check the project `CLAUDE.md` for an **Output paths** table to determine file locations; otherwise use the defaults below.

| Dev artifact | Default file | Required for sign-off |
|-------------|-------------|----------------------|
| Architecture design | `dev/arch-design.md` | Yes — produce using `/arch-design` skill if not yet written |
| Technical specification | `dev/tech-spec.md` | Yes — produce using `/tech-spec` skill if not yet written; must include the confirmed tech stack (hosting, database, auth, CI/CD), resolved constraints, and data model decisions |

For each artifact: if the file does not exist, produce it now using the relevant skill before proceeding. If it exists but predates constraint resolutions from this Phase B, update it to reflect the final agreed decisions. Update **Status** to **Done** and **Last updated** to today's date in the project `CLAUDE.md` status table for each file written. Confirm the file paths to the user.

**Sign-off decision**:
- If all constraints resolved AND Phase B artifacts are written to dev files AND all three parties are satisfied → record sign-off and move to Phase C
- If constraints remain, or dev artifacts are not yet written → identify exactly what is missing before sign-off can be granted

**Update release plan**: Open the release plan file and mark the Tech Design Layer row as Complete with today's date. Apply any scope changes from constraint resolution to the affected layer rows. Confirm the file was written.

**Checkpoint B3**: Record three-way sign-off or confirm next round scope.
**Write state**: Update `[project]-state.md` —
- Phase B status → ✓ Complete [Date]; PM sign-off ✓; Designer sign-off ✓; Eng sign-off ✓
- Current Position → Phase C
- Artifacts table Dev rows: Arch design → ✓ Done [Date] [file path]; Tech spec → ✓ Done [Date] [file path]; API spec → ✓ Done [Date] [file path] or N/A
- Clear Open constraints list (move resolved ones to Key Decisions)
- Open P0/P1 questions summary → update to reflect all resolved

---

### B4 — Phase B Status

```
## Tech Design — Status Update

**Project**: [Name]
**Round**: [N]
**Status**: Resolving / Converging / Blocked on [item]

### Constraints
- Total identified: [N]
- Resolved: [N]
- Open: [N — list below]

### Open constraints
| Constraint | Owner | Proposed resolution | Status |
|-----------|-------|--------------------|----|
| | PM / Designer / Eng | | Pending / In progress |

### Sign-off status
PM: Signed off / Pending
Designer: Signed off / Pending
Eng: Signed off / Pending

### Estimated rounds to completion
[N more rounds, or "ready for sign-off"]
```

---

## Phase C — Dev Build

*Work unit: sprint or Kanban cycle. Retros are end of cycle.*
*Roles: Eng-led. PM + Design available for questions, not actively producing.*

**Cadence by team size** — check the team size recorded in the state file before running C2 or C3:
- **Solo builder (team size = 1)**: lightweight daily focus check-in (C2) + cycle close (C3). No standup ceremony; no retrospective.
- **Project team (team size ≥ 2)**: daily standup (C2) + full retrospective (C3).

---

### C1 — Cycle Planning

At the start of each new cycle, produce a cycle plan following the process and template of the `/cycle-plan` skill:
- Confirm which build layer this cycle draws from and that all layer prerequisites are met
- Assess team capacity
- Select and sequence work items from the current layer
- Check all within-cycle dependencies
- Assign parallel workstreams if 2-person team
- Set the cycle goal

After presenting the plan, immediately run the **Review-Iterate-Approve loop** *(designated reviewer: `plan-reviewer`)*:

1. Run the `plan-reviewer` agent — checks for over-commitment, dependency issues, and incorrect build-layer sequencing.
2. Present its findings (critical issues, warnings).
3. Ask: *"What would you like to update based on this review? List specific items, or say **'approved'** to start the cycle."*
4. Apply updates, re-run `plan-reviewer`, repeat until the user says **"approved"**.

**Apply the Questions Gate** — check `questions.md` before starting the cycle. Resolve any P0 questions now; flag P1 questions; carry P2 forward. Write any new questions or blockers surfaced during cycle planning to `questions.md`.

**Checkpoint C1**: Get approval before the cycle begins.

**Persist the approved cycle plan** — after the user says "approved", save the full cycle plan using the approach that matches the team size recorded in the state file:

- **Solo builder (team size = 1)**: Add a `## Cycle [N] — Plan` section to `[project]-state.md` directly below the Phase C status block. Include: cycle goal, approved task table (with estimates and dependencies), day-by-day schedule, verification criteria, and any key decisions made during the plan-reviewer loop. This keeps everything in one file and avoids document sprawl for a solo builder.

- **Project team (team size ≥ 2)**: Write the full approved cycle plan to `dev/cycles/cycle-[N].md`. Include: cycle goal, approved task table, day-by-day schedule with assignees, verification criteria, key decisions from the plan-reviewer loop, and carried items with rationale. Update `[project]-state.md` to reference the file path. Create the `dev/cycles/` directory if it does not exist.

In both cases, the cycle plan is the approved version — include any changes made during the review-iterate loop, not the initial draft.

**Write state**: Update `[project]-state.md` — current phase (C), cycle number, current build layer, selected work items and owners, cycle goal, open P0/P1 questions summary. For any dev artifact that is being produced this cycle (e.g., dev plan, QA test plan), update its Artifacts table row from "Not started" to "In progress [Date]".

---

### C2 — Daily Check-in (Solo) / Standup (Team)

**Solo builder (team size = 1) — Daily Focus check-in:**

The solo daily check-in is a brief orient-and-focus prompt, not a standup ceremony. When the user checks in (any message indicating they're starting a work session or asking what to do next):

1. Look at the approved cycle plan (in `[project]-state.md`) and the current Status column in `dev/dev-plan.md`
2. Identify the next uncompleted task in the cycle sequence, respecting within-cycle dependencies
3. Present a one-line focus prompt:

   > *"Today: [task name and one-line description]. [N] tasks remain in this cycle ([N] days of work). On track / [N] days behind."*

4. Accept task completions: if the user reports one or more tasks as done, update `dev/dev-plan.md` Status column to `✓` for each completed task immediately. Do not wait for retro or cycle close to record completions.
5. If the user surfaces a blocker, flag it and offer to invoke the `blocker-coach` agent.

No structured "done / in progress / blocked" output required. No cycle health narrative. Keep it to one short exchange.

---

**Project team (team size ≥ 2) — Daily Standup:**

Process standup updates following the process and template of the `/standup` skill:
- Accept free-text or bullet-point updates from each person
- Structure into: done, in progress, blocked
- Surface blockers and decisions needed immediately
- Assess cycle health — is the team on track?

**Task tracking**: For each task reported as Done in today's standup, open `dev/dev-plan.md` and update its Status column to `✓`. This keeps the dev plan as the live day-to-day task tracker throughout the cycle. If the dev plan task table does not have a Status column, add one before updating.

---

This phase can be run multiple times per cycle. Each run processes one session's updates.

**No checkpoint** — check-ins and standups are continuous. Flag anything requiring a cycle plan revision.

---

### C3 — Cycle Close (Solo) / Retrospective (Team)

**Solo builder (team size = 1) — Cycle Close:**

The solo cycle close focuses entirely on completion accounting and document updates. Skip the retrospective ceremony (what worked / what didn't / action items / process change).

1. Ask: *"What was completed this cycle?"* Accept free-text, bullet list, or "everything."
2. For any task the user reports as completed that isn't already `✓` in `dev/dev-plan.md`, update its Status column now.
3. Note any tasks not completed with a brief reason (carried to next cycle, descoped, blocked).

**Update release plan**: Open the release plan file and apply the following updates:
- For each work item completed this cycle: tick the corresponding `[ ]` checkbox in the build sequence section of the release plan (the layer checklist — e.g., Layer 1 — Infrastructure, Layer 2 — Foundation)
- If a build layer is fully complete, mark the layer heading as `✓ Complete [Date]` and tick any remaining unchecked items in that layer's checklist
- For items carried over, add a note to their checklist entry indicating the expected cycle
- Do not rely on the state file for this; the release plan file must reflect actual completion status

**Apply the Questions Gate** — check `questions.md`. Resolve any P0 blockers before closing the cycle.

**Checkpoint C3**: Confirm the completion list before writing state.
**Write state**: Update `[project]-state.md` —
- Cycle summary block: tasks completed, tasks carried over with reasons, next cycle focus
- Artifacts table Dev rows: for every dev artifact completed this cycle, update its row to ✓ Done [Date] with file path
- Open P0/P1 questions summary

Present a brief cycle close summary — completed vs planned count, any carried items, next cycle focus. One short block, no narrative sections.

---

**Project team (team size ≥ 2) — Retrospective:**

Run a retrospective following the process and template of the `/retro` skill:
- Assess what was completed vs planned
- Surface what worked and what didn't
- Define one action item per person
- Define one process change to try next cycle

**Apply the Questions Gate** — check `questions.md` before closing the cycle. Any blockers surfaced in standups that were logged as P0 questions must be resolved before the retrospective can complete. Write any new questions surfaced during retro to `questions.md`.

**Update release plan**: Open the release plan file and apply the following updates based on the retrospective:
- For each work item completed this cycle: tick the corresponding `[ ]` checkbox in the build sequence section of the release plan (the layer checklist — e.g., Layer 1 — Infrastructure, Layer 2 — Foundation)
- If a build layer is fully complete, mark the layer heading as `✓ Complete [Date]` and tick any remaining unchecked items in that layer's checklist
- For items carried over, add a note to their checklist entry indicating the expected cycle
- Do not rely on the state file for this; the release plan file must reflect actual completion status

**Checkpoint C3**: Get approval before generating the status report.
**Write state**: Update `[project]-state.md` —
- Completed items and carried-over items with reasons; next cycle focus
- Artifacts table Dev rows: for every dev artifact completed this cycle (dev plan, QA test plan, code review, security review, deployment guide — whichever applies), update its row to ✓ Done [Date] with the actual file path. Do not leave rows as "In progress" once the artifact is written and approved.
- Open P0/P1 questions summary

---

### C4 — Status Report (end of cycle)

Generate a stakeholder status report following the process and template of the `/status` skill:
- Set RAG status for schedule, scope, quality, and team
- Show progress against release plan phases and build layers
- Summarise what shipped this cycle and what's planned next
- Surface any open risks and decisions needed from stakeholders

**Update release plan**: If this cycle completed early or slipped, open the release plan file and adjust the planned dates for future layers to reflect the revised timeline. The release plan dates must stay realistic — do not leave them as the original kickoff estimates if the project has moved. Confirm the file was written.

**Checkpoint C4**: Present the end-of-cycle package.
**Write state**: Update `[project]-state.md` — RAG status, release plan health, and any Key Decisions made this cycle.

---

### C5 — Next Cycle Planning

Immediately roll into the next cycle plan following the process and template of the `/cycle-plan` skill:
- Carry over any incomplete items from this cycle with updated sizing
- Confirm the next build layer or continued work on the current layer
- Reassess capacity for the new cycle

---

## End-of-Phase or End-of-Cycle Summary

Output a clean handoff summary scaled to the phase:

**For Phase A completion:**
```
## [Project Name] — PM + Design Alignment Complete

**Completed**: [Date]
**Rounds taken**: [N]
**PRD status**: Final — [N sections, N P0 requirements]
**Design status**: Final — [N P0 screens, handoff doc ready]
**Sign-off**: PM ✓ | Designer ✓

### Key decisions made during alignment
- [Decision and rationale]

### What goes to Tech Design
- PRD: [file/location]
- Design handoff: [file/location]
- Open assumptions to watch: [list]
```

**For Phase B completion:**
```
## [Project Name] — Tech Design Complete

**Completed**: [Date]
**Rounds taken**: [N]
**Constraints resolved**: [N of N]
**Sign-off**: PM ✓ | Designer ✓ | Eng ✓

### Key constraint resolutions
- [Constraint → how it was resolved]

### Scope changes from tech design
- [Any requirements added, removed, or adjusted]

### Dev ready
- Tech stack confirmed: [hosting platform, database, auth system, CI/CD tooling]
- Release plan Layer 1 updated: [confirm TBD placeholders have been replaced with confirmed choices]
- Arch design: [file/location]
- Tech spec: [file/location]
- First cycle: [what Layer 1 work looks like]
```

**For Phase C cycle completion:**
```
## [Project Name] — Cycle [N] Complete

**Cycle dates**: [Start] to [End]
**Cycle goal**: [Goal]
**Outcome**: Achieved / Partially achieved / Not achieved

### Completed
- [Item]

### Carried to Cycle [N+1]
- [Item] — [Reason]

### Release Plan Status
- Current phase: [Phase name]
- Current layer: Layer [N] — [Name]
- Launch target: [Date] — On track / At risk

### Cycle [N+1] Focus
Layer [N] — [Layer name] | [Cycle goal for next cycle]
```

---

## Phase D — Testing & Launch

*Work unit: testing sprint. PM, Designer, and Eng all active. Each test type produces pass/fail results and a bug list. Bugs are triaged and fixed in cycles before risk clearance is granted.*

---

### D1 — Automated Tests

Before any manual testing, run (or direct the builder to run) the automated test suite:
- Unit tests, integration tests, and e2e tests defined in the QA test plan (`dev/test-plan.md`)
- If no automated tests exist, note this and treat all coverage as manual in D2/D3

Produce a test run summary:
```
## Automated Test Run — [Date]

**Unit tests**: [N passed] / [N total] — [Pass / Fail]
**Integration tests**: [N passed] / [N total] — [Pass / Fail]
**E2E tests**: [N passed] / [N total] — [Pass / Fail]

### Failures
- [Test name] — [What failed] — [Likely cause]

### Coverage gaps
- [Any area not covered by automated tests that needs manual testing]
```

If any critical failures exist (P0 tests failing), stop and resolve before D2. Log bugs to the bug register.

**Apply the Questions Gate** — check `questions.md` before proceeding to D2. Resolve any P0 questions now and update affected documents.

**Update release plan**: Open the release plan file and mark the D1 — Automated Tests sub-item in the QA & Launch layer as passed (or failed with count of bugs found). Confirm the file was written.

**Checkpoint D1**: Confirm automated test results before proceeding.
**Write state**: Update Phase D — D1 status with pass/fail and number of bugs found.

---

### D2 — PM Requirements Test

The PM manually tests that every P0 user story and acceptance criterion from `pm/user-stories.md` is met by the built product.

Structure the test as a requirements coverage check:

For each P0 user story:
1. State the story and its acceptance criteria (Given/When/Then)
2. Step through the built feature and verify each criterion
3. Mark as: ✓ Pass | ✗ Fail — [what's wrong] | ⚠ Partial — [what's missing]

Produce a summary:
```
## PM Requirements Test — [Date]

**Stories tested**: [N]
**Pass**: [N] | **Fail**: [N] | **Partial**: [N]

### Failures / Gaps
- Story [ID]: [What's not working or missing]
  → Bug: [Brief description]

### P1/P2 items not in scope for v1
- [Confirm these are intentionally deferred]
```

Log all failures as bugs. Ask: *"Do you want to fix the failures before design conformance testing, or continue and address them all in D4 bug triage?"*

**Apply the Questions Gate** — check `questions.md` before proceeding to D3. Resolve any P0 questions and update affected documents.

**Update release plan**: Open the release plan file and mark the D2 — PM Requirements Test sub-item as passed or failed with gap count. Confirm the file was written.

**Checkpoint D2**: Confirm PM test results.
**Write state**: Update Phase D — D2 status with pass/fail and gaps found.

---

### D3 — Design Conformance Test

The PM or Designer verifies that the built product matches the approved design handoff (`design/design-handoff.md`).

For each screen in the design handoff:
1. Compare the built screen against the handoff spec
2. Check: layout zones, components present, labels, states (empty/loading/error/success), interactions, transitions, accessibility requirements
3. Mark as: ✓ Match | ✗ Discrepancy — [what's different] | N/A — [screen not yet built]

Produce a summary:
```
## Design Conformance Test — [Date]

**Screens tested**: [N]
**Match**: [N] | **Discrepancy**: [N] | **Not built**: [N]

### Discrepancies
- Screen: [Name]
  - [Component / state / interaction that doesn't match the design]
  → Severity: P0 (blocks launch) / P1 (fix soon) / P2 (polish)
  → Bug: [Brief description]
```

Log all discrepancies as bugs. Offer: *"Want me to run the `ux-reviewer` agent *(design-ux-kit)* on the built product to catch anything the conformance check missed?"*

**Apply the Questions Gate** — check `questions.md` before proceeding to D4. Resolve any P0 questions and update affected documents.

**Update release plan**: Open the release plan file and mark the D3 — Design Conformance Test sub-item as passed or failed with discrepancy count. Confirm the file was written.

**Checkpoint D3**: Confirm design conformance results.
**Write state**: Update Phase D — D3 status with discrepancies found.

---

### D4 — Bug Triage

Consolidate all bugs from D1 (automated test failures), D2 (PM requirements gaps), and D3 (design discrepancies) into a single triage table.

For each bug, assign:
- **Priority**: P0 (blocks launch — cannot ship), P1 (must fix before launch), P2 (fix soon after launch), P3 (backlog)
- **Owner**: who fixes it
- **Estimate**: S / M / L effort
- **Source**: D1 / D2 / D3

Present the triage table and the launch readiness summary:

```
## Bug Triage — [Date]

| # | Bug | Priority | Owner | Estimate | Source | Status |
|---|-----|----------|-------|----------|--------|--------|
| 1 | [Description] | P0 | [Owner] | S/M/L | D1/D2/D3 | Open |

### Summary
- P0 bugs (launch blockers): [N]
- P1 bugs (must fix): [N]
- P2 bugs (post-launch): [N]
- P3 bugs (backlog): [N]

### Estimated fix effort
- P0: [total estimate]
- P1: [total estimate]
```

If P0 bugs exist, run a fix cycle: the builder addresses P0s, then re-run the relevant test (D1/D2/D3) to confirm the fix. Repeat until no P0s remain.

Offer: *"Want me to invoke the `blocker-coach` agent on any P0 bug that's proving hard to fix?"*

**Apply the Questions Gate** — check `questions.md` before proceeding to D5. All P0 and P1 questions must be resolved before risk clearance begins.

**Checkpoint D4**: No P0 bugs open before proceeding. P1s must have an owner and a fix date.
**Write state**: Update Phase D — D4 status with open bug counts and fix progress.

---

### D5 — Risk Clearance

Run the `/risk` skill in Phase D clearance mode (Step 6 of the risk skill):

1. Read the full risk register (`[project]-risks.md`)
2. Review every Open or Accepted risk — was it addressed during D1/D2/D3 testing?
3. Confirm no new risks were surfaced during testing that aren't in the register
4. Produce the launch risk clearance report:

```
## Launch Risk Clearance — [Date]

### Open risks at launch
| Risk | Score | Status | Post-launch mitigation |
|------|-------|--------|----------------------|
| [Risk] | [1–9] | Accepted | [What we'll do if it triggers post-launch] |

### Launch recommendation
[Clear to launch / Hold — [what must be resolved]]
```

**Clearance gate**: Do not proceed to D6 if any score 6+ risk is Open with no mitigation or acceptance decision. Ask the user to resolve or explicitly accept each one.

**Apply the Questions Gate** — check `questions.md` before launch. No open P0 or P1 questions permitted at this stage. Any remaining P2 questions should be logged as post-launch follow-ups.

**Checkpoint D5**: Launch risk clearance sign-off.
**Write state**: Update Phase D — D5 status with clearance decision.

---

### D6 — Rollout

With all tests passed, bugs triaged, and risks cleared, invoke the `/rollout` skill from pm-claude-kit.

The rollout skill will produce the full launch package including:
- Project / product completion summary (features implemented, timelines, resulting risks)
- Audience-specific product summaries (internal team, customers, executives, support)
- User training materials (quick start guide, step-by-step instructions, FAQ, tips)

**Update release plan**: Open the release plan file and mark all remaining QA & Launch layer rows as Done with today's actual date. Record the actual launch date against the planned date in the timeline section. Mark the overall project as Complete. Confirm the file was written.

**Checkpoint D6**: Confirm the rollout package is complete.
**Write state**: Update `[project]-state.md` —
- Phase D status → ✓ Complete [Date]; D6 Rollout → ✓ Complete [Date]
- Current Position → Project complete
- Artifacts table Dev rows: Deployment guide → ✓ Done [Date] with file path (if not already marked)
- Artifacts table Project rows: Release plan → ✓ Complete [Date]; Risk register → ✓ Cleared [Date]
- Clear Document Sync Queue (should be empty at launch)
- Overall project status → ✓ Complete

---

## Phase D completion summary

```
## [Project Name] — Testing & Launch Complete

**Phase D dates**: [Start] to [End]
**Automated tests**: [N passed / N total]
**PM requirements**: [N passed / N total]
**Design conformance**: [N matched / N screens]
**Bugs fixed**: [N P0] [N P1] fixed | [N P2] deferred to post-launch
**Risk clearance**: ✓ Cleared — [N risks accepted with post-launch mitigations]

### Launch package
- Rollout doc: [file/location]
- Open post-launch risks: [list or "none"]
- Metrics to watch: [from the product brief's success criteria]

**Project status**: Complete ✓
```
