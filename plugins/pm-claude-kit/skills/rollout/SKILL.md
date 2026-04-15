---
name: rollout
description: Generate a product rollout package — audience-specific product summaries and user training materials. Use when a feature or product is ready to launch and needs communication and enablement content. Run this AFTER design and development are complete, not during requirements or spec phases.
disable-model-invocation: true
---

Create a rollout package for: $ARGUMENTS

> **Learning note — Product Rollout**
> A feature isn't complete when code ships — it's complete when users understand it and adopt it. The rollout package bridges the gap between "technically live" and "users getting value from it." Different audiences need different messages: customers want to know how their problem is solved, support teams need to know what changed and what questions to expect, and executives want to know the strategic impact. Getting these communications right is often what determines whether a technically good product actually succeeds in practice.

Display the learning note above verbatim to the user before proceeding.

> **Timing**: This skill should be run at the end of the product development cycle — after design is signed off and development is complete. If requirements are still being written or design has not started, return to `/pm` or `/design` first.

**Output standard — tables**: All documents are read in Obsidian. Always include a blank line before any Markdown table — Obsidian requires this to render `|` syntax as a table rather than plain text.

Use the template in [rollout-template.md](rollout-template.md) as the structure.

Follow this process:

### Step 0: Read project inputs

Before writing anything, check the project directory for:
- **Product brief** (`pm/brief.md`) — original scope, users, and success criteria
- **PRD** (`pm/prd.md`) — full requirements. Use as source of truth for what was planned
- **User stories** (`pm/user-stories.md`) — P0/P1/P2 feature list
- **Roadmap** (`pm/roadmap.md`) — planned horizon and timeline
- **Risk register** (`[project]-risks.md`) — open and accepted risks at launch
- **Phase D test results** (from exec-kit `/run` Phase D) — what was tested, what passed, what was deferred

Use these to produce the project completion summary in Step 1 and to ground all audience summaries in what was actually built (not just what was planned).

### Step 1: Project Completion Summary

Produce a project-level completion summary before any audience-specific content. This is the single source of truth for what shipped.

**What was built**
[2–3 sentences: what the product or feature does, the core user workflow, the primary benefit delivered]

**Features implemented (v1)**

| Feature | Priority | Status |
|---------|----------|--------|
| [Feature from user stories] | P0/P1 | ✓ Shipped / Deferred to v2 |

**What was deferred to v2**
[List any P1/P2 items cut from v1 scope and the reason]

**Timeline summary**
- Project started: [Date from kickoff]
- Phase A complete (PM + Design): [Date]
- Phase B complete (Tech Design): [Date]
- Phase C complete (Dev Build): [Date]
- Phase D complete (Testing): [Date]
- Launch date: [Date]

**Resulting risks at launch**
[Pull from Phase D risk clearance — any Accepted risks with post-launch mitigations. If none, state "No open risks at launch."]

| Risk | Score | Post-launch mitigation |
|------|-------|----------------------|
| [Risk] | [1–9] | [What happens if it triggers] |

**Success metrics to watch**
[Pull from the product brief or PRD success criteria — the 2–3 metrics that will tell us v1 succeeded]

---

### Step 2: Clarify rollout context
If not already clear from the input, ask:
1. Who are the **audiences**? (internal team, customers, executives, support staff — pick all that apply)
2. What is the **rollout scope**? (all users, beta group, specific segment, phased)

If sufficient context exists from the project inputs, proceed directly.

---

### Step 3: Product Summary (per audience)

Write a tailored summary for each relevant audience. Each version has a different focus:

**Internal / Team announcement**
- What shipped, what it does, why it matters
- What changed from the original plan (if anything)
- What to watch / metrics being tracked
- Who to contact with questions

**Customer-facing announcement**
- Written in plain language, benefit-first (not feature-first)
- Lead with the user problem it solves, not the technical capability
- Include what users can do now that they couldn't before
- Call to action (try it, learn more, etc.)
- Avoid internal jargon or technical detail

**Executive summary**
- 1 paragraph: what launched, strategic rationale, expected impact
- Key metric to watch and when to expect signal
- Any risks or open items post-launch

**Support team briefing**
- What changed from a user perspective
- Common questions users will ask + answers
- Known issues or limitations
- Escalation path for edge cases

---

### Step 4: User Training Materials

Produce practical, task-oriented training content. Structure it around what users need to **do**, not what the feature **is**.

**Quick Start Guide**
- 3-5 steps to get started with the feature
- Screenshot placeholders labeled [screenshot: describe what to show]
- One "pro tip" to highlight a non-obvious capability

**Step-by-Step Instructions**
- Full walkthrough of the primary use case
- Include decision points (if X, then Y)
- Cover the most common variant use cases
- Note prerequisites or setup required

**FAQ**
- 5-8 questions users are likely to ask
- Answers in plain language
- Flag anything that requires a support escalation

**Tips & Best Practices**
- 3-5 recommendations for getting the most value
- Common mistakes to avoid

---

### Output

Produce the full rollout package as a structured markdown document. Use clear section headers so each piece can be extracted and used independently (e.g., copy the customer announcement into an email, paste the FAQ into a help article).

Note any sections where real screenshots, links, or specific product details need to be filled in before publishing.

## Save output

After presenting the rollout package to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/rollout` and save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. In that same project `CLAUDE.md`, find the **Project status** table and set the **Status** column to **Done** for the row matching this deliverable
5. Confirm the file was written to the user
6. If no project `CLAUDE.md` exists, present the output for manual copying
