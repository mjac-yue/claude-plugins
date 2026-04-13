---
name: rollout
description: Generate a product rollout package — audience-specific product summaries and user training materials. Use when a feature or product is ready to launch and needs communication and enablement content. Run this AFTER design and development are complete, not during requirements or spec phases.
disable-model-invocation: true
---

Create a rollout package for: $ARGUMENTS

> **Timing**: This skill should be run at the end of the product development cycle — after design is signed off and development is complete. If requirements are still being written or design has not started, return to `/pm` or `/design` first.

**Output standard — tables**: All documents are read in Obsidian. Always include a blank line before any Markdown table — Obsidian requires this to render `|` syntax as a table rather than plain text.

Use the template in [rollout-template.md](rollout-template.md) as the structure.

Follow this process:

### Step 1: Clarify context
If not already clear from the input, ask:
1. Who are the **audiences**? (internal team, customers, executives, support staff — pick all that apply)
2. What is the **rollout scope**? (all users, beta group, specific segment, phased)
3. Is there a **PRD or feature description** to reference? If so, use it as the source of truth.

If sufficient context exists, proceed directly.

---

### Step 2: Product Summary (per audience)

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

### Step 3: User Training Materials

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
