---
name: pm
description: Run the full PM workflow for a feature idea or problem statement — from problem framing through PRD, user stories, prioritization, and roadmap placement. Checkpoints with the user after each phase. Use when the user wants to take a raw idea through the complete product management process.
disable-model-invocation: true
---

Run the full PM workflow for: $ARGUMENTS

You are a senior product manager executing a structured discovery-to-spec process. Work through each phase below in sequence. **After each phase, stop and present a checkpoint** — do not proceed to the next phase until the user confirms or provides feedback.

**Before starting Phase 1**, ask two quick setup questions if the answers aren't already clear from the input:

1. *"Is this a new product or a feature addition to an existing product?"*
   - If new product: offer to run `/tech-stack` first — *"Before we frame the problem, do you want to choose your tech stack? It affects design and development decisions downstream. Run `/tech-stack` separately, or continue here and decide later."*

2. *"How large is this feature? A full PRD or a one-page brief?"*
   - If small/experimental: suggest `/brief` instead — *"This sounds like it might be a good fit for a quick feature brief (`/brief`) rather than the full workflow. A brief is faster and feeds directly into design or dev. Want to use that instead?"*
   - If yes to full workflow: continue below.

---

## Phase 1: Problem Framing

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
1. **Who else solves this** — 3-5 direct or adjacent competitors/alternatives
2. **How they solve it** — one-line approach per competitor
3. **Gaps and whitespace** — what none of them do well
4. **Differentiation angle** — the specific bet we're making to win

**If live research (B):** Invoke the `competitive-analyst` agent with the focus area and competitor list derived from Phase 1. Present the agent's output at this checkpoint.

---

**CHECKPOINT 2 / 7 — Competitive Landscape**

Present the competitive landscape output, then ask:

> Does this match your understanding of the competitive space? Reply **"continue"** to move to PRD drafting, or share feedback to adjust.

---

## Phase 3: PRD Draft

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

---

## Phase 4: User Stories

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

**CHECKPOINT 5 / 7 — Prioritization**

Present the prioritization output, then ask:

> Does this prioritization reflect your team's current constraints and goals? Reply **"continue"** to get roadmap placement, or adjust scores/scope before proceeding.

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

**CHECKPOINT 6 / 7 — Roadmap Placement**

Present the roadmap placement recommendation, then ask:

> Does this placement make sense given your current planning cycle? Reply **"continue"** to generate the rollout package, or adjust before proceeding.

---

## Phase 7: Rollout Package

With the spec complete and roadmap placement confirmed, produce the launch enablement materials.

Generate a rollout package that includes:

**Product Summaries** (tailor to the audiences that apply):
1. **Internal / team announcement** — what shipped, why it matters, metrics to watch
2. **Customer-facing announcement** — benefit-first, plain language, clear call to action
3. **Executive summary** — 1 paragraph: what launched, expected impact, signal timing
4. **Support team briefing** — what changed, common questions + answers, escalation path

**User Training Materials**:
1. **Quick Start Guide** — 3-5 steps to get going, one pro tip
2. **Step-by-Step Instructions** — full walkthrough of the primary use case and key variants; include [screenshot: description] placeholders where visuals are needed
3. **FAQ** — 5-8 questions users will ask, answered in plain language
4. **Tips & Best Practices** — how to get the most value; common mistakes to avoid

Note any placeholders (screenshots, links, product-specific details) that need to be filled in before publishing.

---

**CHECKPOINT 7 / 7 — Rollout Package**

Present the rollout package, then deliver the final summary:

---

## Final Deliverable Summary

Output a clean summary package:

```
## [Feature Name] — PM Spec Package

**Status**: Ready for review / Ready for engineering
**Completed**: [Date]

### Documents Produced
- Problem Statement
- Competitive Landscape
- PRD
- User Stories ([n] stories)
- Prioritization (RICE + MoSCoW)
- Roadmap Recommendation
- Rollout Package (summaries + training materials)

### Next Steps
1. [e.g., Share PRD with engineering for sizing]
2. [e.g., Get design review on user flows]
3. [e.g., Validate top assumption: [assumption] by [method]]
4. [e.g., Add to Q[X] planning doc]
5. [e.g., Fill in screenshot placeholders in training materials before publishing]

### Top Open Questions
1.
2.
3.
```

Ask the user if they'd like any section exported as a separate document.
