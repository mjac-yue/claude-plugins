---
name: pm
description: Run the full PM workflow for a feature idea or problem statement — from problem framing through PRD, user stories, prioritization, and roadmap placement. Checkpoints with the user after each phase. Use when the user wants to take a raw idea through the complete product management process.
disable-model-invocation: true
---

Run the full PM workflow for: $ARGUMENTS

**Output standard — diagrams**: All documents are read in Obsidian. Use Mermaid syntax (` ```mermaid ` blocks) for every diagram — Obsidian renders these natively. Never use ASCII art for diagrams. Relevant types: `flowchart` (user journeys, process flows), `sequenceDiagram` (interaction flows), `graph` (relationships).

**Output standard — tables**: Always include a blank line before any Markdown table. Obsidian requires this to render `|` syntax as a table rather than plain text.

You are a senior product manager executing a structured discovery-to-spec process. Work through each phase below in sequence. **After each phase, stop and present a checkpoint** — do not proceed to the next phase until the user confirms or provides feedback.

---

## Phase 0 — Project Profile

Before producing anything, establish the project tier. If a Project Profile Card was already produced by exec-kit's `/release` skill, accept it and skip this phase.

Otherwise ask:

1. *"Is this a new product or a feature addition to an existing product?"*
   - If new product: offer to run `/tech-stack` first — *"Before we frame the problem, do you want to choose your tech stack? It affects design and development decisions downstream. Run `/tech-stack` separately, or continue here and decide later."*

2. *"How would you describe the size of this project?"*
   - **(A) Micro** — single small change, days to ~2 weeks, clear scope
   - **(B) Small** — 1–3 features, 2–6 weeks, few unknowns
   - **(C) Medium** — multi-feature, 6–16 weeks, some unknowns
   - **(D) Large** — full product, 16+ weeks, significant complexity

Derive the tier and declare it, then apply the phase gating below:

| Tier | Default phases | Not default — add back if needed |
|------|---------------|----------------------------------|
| **Tier 1 (Micro)** | Problem framing only (one paragraph). Produce a one-paragraph brief with scope, goal, and first action. | Phases 2–6 |
| **Tier 2 (Small)** | Phase 1 (abbreviated), Phase 4 (2–3 stories only). Run `/brief` instead of PRD. | Phases 2, 3, 5, 6 |
| **Tier 3 (Medium)** | Phases 1–5. Phase 6 (roadmap) if needed for stakeholder communication. | Phase 6 (roadmap) |
| **Tier 4 (Large)** | Phases 1–6. | — |

> **Note on Phase 7 — Rollout Package**: Rollout is intentionally excluded from the default `/pm` workflow. It belongs at the end of the product development cycle — after design and dev are complete and the product is ready to ship. Run `/rollout` separately at that point. Do not produce rollout materials as part of initial requirements and spec work.

**Step C — Skipped phase opt-in**

After establishing the tier, present the phases not included by default and ask:

*"Before we start — the following phases are skipped by default for your tier. Would you like to add any of them back in?"*

Present only the phases skipped for the established tier, using this description for each:

| Phase | What it adds | When to add it back |
|-------|-------------|---------------------|
| Phase 2 — Competitive Landscape | Structured analysis of competing products, approaches, and whitespace | Entering a new market, need to differentiate, or need stakeholder context on competition |
| Phase 3 — PRD (Full) | Full product requirements doc with goals, requirements, risks, and open questions | Need a formal spec for engineering handoff or stakeholder review instead of a brief |
| Phase 4 — User Stories | Complete story set with Given/When/Then acceptance criteria, priority, sizing, and edge cases | Need sprint-ready tickets before design begins |
| Phase 5 — Prioritization | RICE scores + MoSCoW classification with v1 scope recommendation and trade-offs | Have more requirements than capacity and need a defensible scope cut |
| Phase 6 — Roadmap Placement | Where this fits: Now/Next/Later, suggested quarter, dependencies, and what it displaces | Need to communicate placement to stakeholders or align with an existing planning cycle |

Accept any number of additions. Confirm: *"Got it — I'll include [X, Y] in addition to the defaults. Here's the updated phase list for this session: [list]."*

**Checkpoint 0**: Confirm tier and phase list before proceeding.

---

## Phase 1: Problem Framing — *All tiers*

**Tier 1**: One paragraph only — problem in one sentence, who it affects, and the proposed direction. No structure required. Then stop and output the brief directly.
**Tier 2**: Abbreviated — problem statement + assumptions only. Skip anti-problems and scale analysis.
**Tier 3–4**: Full output below.

Before writing anything, frame the problem properly.

Produce:
1. **Problem Statement** — "We've observed that [user/customer] struggles to [do X] because [root cause]. This results in [impact]. We believe that [proposed direction] could address this."
2. **Who is affected** — primary and secondary users, rough scale
3. **Why now** — what makes this worth solving in the current cycle (data, strategic fit, urgency)
4. **Assumptions** — list 3-5 key assumptions embedded in this framing that need validation
5. **Anti-problems** — what this is NOT about (scope boundary at the problem level)

---

**CHECKPOINT 1 / 7 — Problem Framing**

Present the problem framing output, then ask:

> Does this capture the problem accurately? Reply **"continue"** to move to competitive analysis, or share feedback to revise before proceeding.

*After user approves: Problem framing is incorporated into the brief (Phase 3) or PRD — no separate file save at this checkpoint.*

---

## Phase 2: Competitive Landscape — *Tier 3–4 only*

**Tier 1–2**: Not included by default. If competitive context is relevant for a Tier 2 project, note 1–2 alternatives in one line as part of the brief. Add back if needed.

With the problem framing confirmed, assess the competitive context.

First, ask the user:

> For the competitive analysis, I can either:
> - **(A) Quick scan** — directional summary from existing knowledge (faster, good for well-known markets)
> - **(B) Live research** — use the `competitive-analyst` agent to search and analyze each competitor in parallel (recommended for 3+ competitors or unfamiliar markets)
>
> Which would you prefer?

**If quick scan (A):** Produce inline:
1. **Who else solves this** — 3-5 direct or adjacent competitors/alternatives
2. **How they solve it** — one-line approach per competitor
3. **Gaps and whitespace** — what none of them do well
4. **Differentiation angle** — the specific bet we're making to win

**If live research (B):** Invoke the `competitive-analyst` agent with the focus area and competitor list derived from Phase 1. Present the agent's output at this checkpoint.

---

**CHECKPOINT 2 / 7 — Competitive Landscape**

Present the competitive landscape output, then ask:

> Does this match your understanding of the competitive space? Reply **"continue"** to move to PRD drafting, or share feedback to adjust.

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the competitive landscape output to the file listed for `/competitive-analysis`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

---

## Phase 3: PRD Draft — *Tier 3–4 only*

**Tier 1**: Not included by default — problem framing from Phase 1 is sufficient. Add back if needed.
**Tier 2**: Not included by default. Use `/brief` instead — produce a one-page feature brief covering: what, why, who, success criteria, scope boundaries, and first three build steps. Add back a full PRD if needed.

With the problem and context confirmed, write the PRD.

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

**CHECKPOINT 3 / 7 — PRD Draft**

Present the full PRD, then ask:

> Review the PRD above. Reply **"continue"** to generate user stories, or share specific sections to revise. You can also ask to run the `prd-reviewer` agent for a structured critique before proceeding.

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the output to the file listed for `/prd` (Tier 3–4) or `/brief` (Tier 2). Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

---

## Phase 4: User Stories — *Tier 2–4*

**Tier 1**: Not included by default. Add back if needed.
**Tier 2**: Write 2–3 stories for the primary user flow only. One acceptance criterion each (Given/When/Then). No edge cases, no complexity sizing beyond S/M/L.
**Tier 3–4**: Full output below.

With the PRD confirmed, generate user stories.

For each major requirement or user flow:
1. Write stories in "As a [persona], I want [capability] so that [benefit]" format
2. Include priority (P0/P1/P2) and complexity (S/M/L/XL)
3. Write acceptance criteria in Given/When/Then format (3-5 per story)
4. Note edge cases per story
5. Flag dependencies between stories

Group stories by persona or feature area. Aim for completeness — these should be ready to create as tickets.

---

**CHECKPOINT 4 / 7 — User Stories**

Present the user stories, then ask:

> Review the user stories above. Reply **"continue"** to move to prioritization, or identify stories to add, remove, or revise. You can also ask to run the `requirements-gap-finder` agent to check for edge cases.

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the user stories to the file listed for `/user-story`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

---

## Phase 5: Prioritization — *Tier 3–4 only*

**Tier 1–2**: Not included by default — scope is small enough that prioritization is implicit. Just note what's P0 vs. deferred in the brief or user stories. Add back if needed.

With the stories confirmed, score and rank the work.

Produce:
1. **RICE scores** for the top-level initiatives or story groups (not every individual story):
   - Reach, Impact, Confidence, Effort, Score
2. **MoSCoW classification** for the requirements — Must / Should / Could / Won't
3. **Recommended phasing** — suggest a v1 scope vs. future phases based on scores
4. **Key trade-offs** — what's being left out of v1 and why

---

**CHECKPOINT 5 / 7 — Prioritization**

Present the prioritization output, then ask:

> Does this prioritization reflect your team's current constraints and goals? Reply **"continue"** to get roadmap placement, or adjust scores/scope before proceeding.

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the prioritization output to the file listed for `/prioritization`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

---

## Phase 6: Roadmap Placement — *Tier 3–4, or Tier 3 only if explicitly requested*

**Tier 1–2**: Not included by default — work is scoped and ready to execute. Add back if stakeholder communication requires roadmap placement.
**Tier 3**: Run only if the team needs to communicate placement to stakeholders or integrate with an existing roadmap. Otherwise skip and note: *"Roadmap placement skipped — add to your roadmap at [Now/Next/Later] based on the prioritization output."*

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

Then deliver the final summary:

---

## Final Deliverable Summary

Output a clean summary package:

```
## [Feature Name] — PM Spec Package

**Status**: Ready for design
**Completed**: [Date]

### Documents Produced
[List only what was produced for this tier]
- Problem Statement
- Competitive Landscape (if run)
- PRD or Feature Brief
- User Stories ([n] stories)
- Prioritization (RICE + MoSCoW) (if run)
- Roadmap Recommendation (if run)

### Next Steps
1. Run `/design [feature]` — UX brief, wireframes, and design handoff
2. [e.g., Validate top assumption: [assumption] by [method] before design begins]
3. [e.g., Any other PM actions needed before design starts]

### Top Open Questions
1.
2.
3.
```

Ask the user if they'd like any section exported as a separate document.
