---
name: prioritization
description: Prioritize a list of features, requests, or initiatives using RICE, MoSCoW, or impact/effort frameworks. Use when the user needs help ranking or triaging product work.
disable-model-invocation: true
---

Help prioritize: $ARGUMENTS

> **Learning note — Feature Prioritization**
> Every team has more ideas than time to build them. Prioritization frameworks like RICE (Reach × Impact × Confidence ÷ Effort) give you a structured, shareable way to make the "what first?" decision — based on evidence rather than whoever argues most loudly in the room. Good prioritization also means being explicit about what you're *not* doing, which is just as important as what you are, because it prevents scope creep and keeps the team focused on the highest-impact work.

Display the learning note above verbatim to the user before proceeding.

**Output standard — tables**: All documents are read in Obsidian. Always include a blank line before any Markdown table — Obsidian requires this to render `|` syntax as a table rather than plain text.

Use the template in [rice-template.md](rice-template.md) as the structure.

Follow this process:
1. **Identify the framework** — default to RICE unless the user specifies MoSCoW or impact/effort matrix.
2. For **RICE scoring**, score each item on:
   - **Reach**: How many users affected per quarter? (number)
   - **Impact**: How much does it move the needle per user? (3=massive, 2=high, 1=medium, 0.5=low, 0.25=minimal)
   - **Confidence**: How confident are you in your estimates? (100%/80%/50%)
   - **Effort**: Person-weeks of work (lower = better)
   - **RICE Score** = (Reach × Impact × Confidence) / Effort
3. For **MoSCoW**, categorize each item as Must Have / Should Have / Could Have / Won't Have with a one-line rationale.
4. For **Impact/Effort Matrix**, place items in four quadrants: Quick Wins / Big Bets / Fill-ins / Time Sinks.
5. Produce a ranked table with scores and a brief recommendation section explaining the top priorities and any notable trade-offs.

Ask the user which framework they prefer if not specified. Output a table suitable for sharing in a planning doc.

## Save output

After presenting the prioritization output to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/prioritization` and save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. In that same project `CLAUDE.md`, find the **Project status** table and set the **Status** column to **Done** for the row matching this deliverable
5. Confirm the file was written to the user
6. If no project `CLAUDE.md` exists, present the output for manual copying
