---
name: pm
description: Run the full PM workflow for a feature idea or problem statement — from problem framing through PRD, user stories, prioritization, and roadmap placement. Checkpoints with the user after each phase. Use when the user wants to take a raw idea through the complete product management process.
disable-model-invocation: true
---

Run the full PM workflow for: $ARGUMENTS

> **Learning note — PM Workflow**
> Product management is the discipline of deciding *what* to build and *why* before anyone starts designing or coding. This workflow takes you from a raw idea through problem framing, competitive context, a full PRD, user stories, prioritization, and roadmap placement — so that when design and engineering start, they have a shared, specific target. Skipping these steps doesn't save time; it creates expensive rework when the team discovers misalignment after weeks of work.

Display the learning note above verbatim to the user before proceeding.

**Output standard — diagrams**: All documents are read in Obsidian. Use Mermaid syntax (` ```mermaid ` blocks) for every diagram — Obsidian renders these natively. Never use ASCII art for diagrams. Relevant types: `flowchart` (user journeys, process flows), `sequenceDiagram` (interaction flows), `graph` (relationships).

**Output standard — tables**: Always include a blank line before any Markdown table. Obsidian requires this to render `|` syntax as a table rather than plain text.

You are a senior product manager executing a structured discovery-to-spec process. Work through each phase below in sequence. **After each phase, stop and present a checkpoint** — do not proceed to the next phase until the user confirms or provides feedback.

---

**Navigation standard — applies at every checkpoint**

After presenting each phase output, always append a **What's next?** block before waiting for the user's response. Use this exact format:

> **What's next?** [Recommended next step — next phase name, or next workflow if this is the final phase]
>
> **Optionally run at this point:**
>
> | Skill / Agent | Plugin | What it does |
> |--------------|--------|-------------|
> | `name` | kit | One-line description |
>
> *Reply with the name of anything you'd like to run first, or say "continue" to proceed.*

If no optional skills or agents apply at a given phase, omit the table and just show the next step recommendation.

---

**Review-Iterate-Approve standard — applies at phases marked with a designated reviewer**

At any phase that designates a reviewer below, follow this loop automatically — do not skip it:

1. **Run the reviewer** — invoke the designated agent immediately after presenting the phase deliverable. Do not ask whether to run it; just run it.
2. **Present findings** — summarise critical gaps, high-priority issues, and recommendations from the reviewer's output. Group by severity (Critical / High / Medium).
3. **Ask what to update** — after the findings, always ask: *"What would you like to update based on this review? List the specific items you want changed, or say **'approved'** if you're satisfied and ready to move on."*
4. **Apply updates** — make the changes the user requests to the deliverable.
5. **Re-run the reviewer** — run the same reviewer again on the updated deliverable.
6. **Repeat** from step 2 until the user explicitly says **"approved"**.
7. **Only then** proceed to the next phase checkpoint and save the file.

---

**Phase lookup table — use this to populate the block at each checkpoint:**

| After this phase | Recommended next step | Optional to run |
|-----------------|----------------------|-----------------|
| Phase 1 — Product Brief | Phase 2 — Competitive Landscape (or brainstorm to refine brief) | `/brainstorm` skill *(pm-claude-kit)* — run if the solution direction is unclear or needs more exploration before committing to the PRD |
| Phase 2 — Competitive Landscape | Phase 3 — PRD Draft | `prd-reviewer` agent *(pm-claude-kit)* — critique competitive framing before writing the PRD; `competitive-analyst` agent *(pm-claude-kit)* — run live web research if quick scan was used |
| Phase 3 — PRD Draft | Phase 4 — User Stories | `prd-reviewer` agent *(pm-claude-kit)* — 8-dimension structured PRD critique; `requirements-gap-finder` agent *(pm-claude-kit)* — edge cases and missing requirements |
| Phase 4 — User Stories | Phase 5 — Prioritization | `requirements-gap-finder` agent *(pm-claude-kit)* — stress-test stories before scope is cut |
| Phase 5 — Prioritization | Phase 6 — Roadmap Placement | No additional agents at this point |
| Phase 6 — Roadmap Placement *(final)* | **Start design: run `/design [feature]`** | No additional agents at this point |

---

## Phase 1: Product Brief

The brief is the foundation of the entire PM workflow. It captures the problem description, proposed solution, users, success criteria, and scope boundary — everything needed to run a focused competitive analysis and write a sharp PRD.

Follow the process of the `/brief` skill:

1. **Write a sharp problem statement** — one to two sentences. What is the user struggling to do, and what is the cost of that struggle?
2. **Describe the proposed solution** — two to three sentences on what will be built. Stay at the "what", not the "how".
3. **Identify who benefits** — primary user and any secondary stakeholders. One line each.
4. **Define success criteria** — two to three measurable signals that confirm the feature is working. Prefer outcome metrics over output metrics.
5. **Draw the scope boundary** — what this brief does NOT include. Prevents scope creep from the first conversation.
6. **List key assumptions** — two to three beliefs about users, behavior, or context this brief depends on. Flag which carries the most risk if wrong.
7. **Surface open questions** — anything that must be answered before design or development starts.

If $ARGUMENTS already answers some of these, skip those questions and confirm your understanding.

---

**CHECKPOINT 1 / 6 — Product Brief**

Present the brief, then ask:

> Does this capture the problem and direction accurately? Reply **"continue"** to move to competitive analysis, or share feedback to revise.
>
> **Optional**: Run `/brainstorm` if the solution direction is unclear — brainstorm explores ideas broadly and can update this brief before we commit to a PRD. You can iterate brief → brainstorm → brief until the direction is solid.

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the brief to the file listed for `/brief`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Risk gate**: Before proceeding, identify any risks surfaced in this phase:
- Are there key assumptions that, if wrong, would change the entire direction?
- Are there external dependencies or unknowns that could block this feature?

Present any score 6+ risks (Likelihood × Impact, 1–3 scale) and ask: *"Do you want to address these risks before proceeding to competitive analysis, or continue and revisit them in the PRD?"*

---

## Phase 2: Competitive Landscape

With the problem framing confirmed, assess the competitive context.

First, ask the user:

> For the competitive analysis, I can either:
> - **(A) Quick scan** — directional summary from existing knowledge (faster, good for well-known markets)
> - **(B) Live research** — use the `competitive-analyst` agent to search and analyze each competitor in parallel (recommended for 3+ competitors or unfamiliar markets)
>
> Which would you prefer?

**If quick scan (A):** Produce inline:
1. **Who else solves this** — 3–5 direct or adjacent competitors/alternatives
2. **How they solve it** — one-line approach per competitor
3. **Gaps and whitespace** — what none of them do well
4. **Differentiation angle** — the specific bet we're making to win

**If live research (B):** Invoke the `competitive-analyst` agent with the focus area and competitor list derived from Phase 1. Present the agent's output at this checkpoint.

---

**CHECKPOINT 2 / 6 — Competitive Landscape**

Present the competitive landscape output, then ask:

> Does this match your understanding of the competitive space? Reply **"continue"** to move to PRD drafting, or share feedback to adjust.

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the competitive landscape output to the file listed for `/competitive-analysis`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Risk gate**: Before proceeding, identify any risks surfaced from the competitive analysis:
- Are there competitors with a significant advantage we haven't accounted for?
- Does the competitive landscape change the differentiation angle in the brief?

Present any score 6+ risks and ask: *"Do you want to address these before writing the PRD, or continue and incorporate them?"*

---

## Phase 3: PRD Draft

With the brief confirmed and competitive context in hand, write the PRD. Use the approved brief as the foundation — the problem statement, users, success criteria, and scope boundary should flow directly from it.

Use the structure from [prd-template.md](../prd/prd-template.md) — the same structure the `/prd` skill produces:
- TL;DR
- Problem Statement (refined from Phase 1)
- Goals & Success Metrics (with leading and lagging indicators)
- Target Users
- Solution Overview & User Journey
- Requirements (P0 / P1 / P2)
- Out of Scope
- Design & Technical Considerations
- Risks & Mitigations
- Dependencies
- Open Questions

Write it fully — no placeholder text. Make explicit any assumptions embedded in the requirements.

---

**CHECKPOINT 3 / 6 — PRD Draft** *(designated reviewer: `prd-reviewer`)*

Present the full PRD, then immediately run the **Review-Iterate-Approve loop**:

1. Run the `prd-reviewer` agent on the PRD just produced.
2. Present its findings (critical gaps, high-priority issues, recommendations).
3. Ask: *"What would you like to update based on this review? List specific items, or say **'approved'** to move on."*
4. Apply updates, re-run `prd-reviewer`, repeat until the user says **"approved"**.

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the output to the file listed for `/prd`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Risk gate**: Before proceeding, identify any risks surfaced in writing the PRD:
- Are there P0 requirements with unclear acceptance criteria or high implementation uncertainty?
- Are there dependencies on third-party services, teams, or decisions not yet made?
- Does the scope feel right — or has it expanded beyond the brief?

Present any score 6+ risks and ask: *"Do you want to address these before generating user stories, or continue and track them?"*

---

## Phase 4: User Stories

With the PRD confirmed, generate user stories.

For each major requirement or user flow:
1. Write stories in "As a [persona], I want [capability] so that [benefit]" format
2. Include priority (P0/P1/P2) and complexity (S/M/L/XL)
3. Write acceptance criteria in Given/When/Then format (3–5 per story)
4. Note edge cases per story
5. Flag dependencies between stories

Group stories by persona or feature area. Aim for completeness — these should be ready to create as tickets.

---

**CHECKPOINT 4 / 6 — User Stories** *(designated reviewer: `requirements-gap-finder`)*

Present the user stories, then immediately run the **Review-Iterate-Approve loop**:

1. Run the `requirements-gap-finder` agent on the user stories just produced.
2. Present its findings (missing edge cases, gaps, ambiguous acceptance criteria).
3. Ask: *"What would you like to update based on this review? List specific stories or criteria to change, or say **'approved'** to move on."*
4. Apply updates, re-run `requirements-gap-finder`, repeat until the user says **"approved"**.

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the user stories to the file listed for `/user-story`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Risk gate**: Before proceeding, identify any risks in the user story set:
- Are any P0 stories XL complexity with high uncertainty?
- Are there stories with unresolved dependencies between them?
- Are there edge cases that suggest the problem is larger than the brief assumed?

Present any score 6+ risks and ask: *"Do you want to address these before prioritization, or continue and reflect them in the RICE scores?"*

---

## Phase 5: Prioritization

With the stories confirmed, score and rank the work.

Produce:
1. **RICE scores** for the top-level initiatives or story groups (not every individual story):
   - Reach, Impact, Confidence, Effort, Score
2. **MoSCoW classification** for the requirements — Must / Should / Could / Won't
3. **Recommended phasing** — suggest a v1 scope vs. future phases based on scores
4. **Key trade-offs** — what's being left out of v1 and why

---

**CHECKPOINT 5 / 6 — Prioritization**

Present the prioritization output, then ask:

> Does this prioritization reflect your team's current constraints and goals? Reply **"continue"** to get roadmap placement, or adjust scores/scope before proceeding.

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the prioritization output to the file listed for `/prioritization`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Risk gate**: Before proceeding, review the v1 scope cut:
- Have any "Could" or "Won't" items created downstream dependencies that could block "Must" items?
- Is the v1 scope achievable within the team's capacity, or is it still over-committed?

Present any score 6+ risks and ask: *"Do you want to adjust the scope before roadmap placement, or continue with the current cut?"*

---

## Phase 6: Roadmap Placement

With prioritization confirmed, recommend where this fits on the roadmap.

Produce:
1. **Recommended horizon** — Now / Next / Later, with reasoning
2. **Suggested quarter** — if the user has indicated current planning cycle, slot it specifically
3. **Dependencies to resolve first** — what must happen before this can start
4. **Confidence level** — High / Medium / Low, with the key risks that affect it
5. **What this displaces or deprioritizes** — no roadmap addition is free; flag the trade-off

---

**CHECKPOINT 6 / 6 — Roadmap Placement**

Present the roadmap placement recommendation, then ask:

> Does this placement make sense given your current planning cycle? Reply **"continue"** to complete the PM workflow, or adjust before proceeding.

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the roadmap output to the file listed for `/roadmap`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Risk gate — PM phase summary**: Before handing off to design, produce a consolidated risk summary of all risks identified across Phases 1–6:

Present as a table:

| Risk | Category | Score | Mitigation status |
|------|----------|-------|------------------|
| [Risk] | Schedule / Scope / Assumption / Dependency | 1–9 | Addressed / Accepted / Open |

Flag any Open risks with score 6+. Ask: *"Are there any open risks you want to address before starting the design workflow, or are you comfortable proceeding?"*

Then deliver the final summary:

---

## Final Deliverable Summary

Output a clean summary package:

```
## [Feature Name] — PM Spec Package

**Status**: Ready for design
**Completed**: [Date]

### Documents Produced
- Product Brief
- Competitive Landscape
- PRD
- User Stories ([n] stories)
- Prioritization (RICE + MoSCoW)
- Roadmap Recommendation

### Open Risks Carried into Design
| Risk | Score | Status |
|------|-------|--------|
| [Risk] | [1–9] | Accepted / To address |

### Next Steps
1. Run `/design [feature]` — UX brief (referencing the brief + user stories), wireframes, and design handoff
2. [e.g., Validate top assumption: [assumption] by [method] before design begins]
3. [e.g., Any open risks to address before design starts]

### Top Open Questions
1.
2.
3.
```

Ask the user if they'd like any section exported as a separate document.
