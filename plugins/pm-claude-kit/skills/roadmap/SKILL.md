---
name: roadmap
description: Generate a product roadmap for a team, product area, or time period. Use when the user wants to plan a roadmap, organize initiatives by timeframe, or communicate the strategic plan.
disable-model-invocation: true
---

Create a product roadmap for: $ARGUMENTS

**Output standard — tables**: All documents are read in Obsidian. Always include a blank line before any Markdown table — Obsidian requires this to render `|` syntax as a table rather than plain text.

Use the template in [roadmap-template.md](roadmap-template.md) as the structure.

Follow this process:
1. **Clarify framing** — if the input doesn't specify, ask: (a) time horizon (Now/Next/Later vs. specific quarters), (b) level of detail (theme-level or initiative-level), (c) audience (internal team vs. external stakeholders). If the input is detailed enough, proceed directly.
2. **Organize by themes** — group initiatives under 2-5 strategic themes rather than listing features randomly. Themes give the roadmap a narrative.
3. **Assign timeframes** — place each initiative in the right horizon. Be honest: if something is speculative, mark it as low confidence.
4. **Add status signals** — for active work, indicate status (Not Started / In Discovery / In Development / Shipped).
5. **Write the strategic narrative** — a brief "why this order" explanation that a VP or customer could read and understand the reasoning.
6. **Flag dependencies and risks** — note anything that could shift the plan.

Confidence levels:
- **High**: Committed, in plan, resources allocated
- **Medium**: Likely, but scope or timing may shift
- **Low**: Exploring, no commitment yet

Output a roadmap ready to drop into a planning doc or presentation. Include both the table view and the narrative section.

## Save output

After presenting the roadmap to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/roadmap` and save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. In that same project `CLAUDE.md`, find the **Project status** table and set the **Status** column to **Done** for the row matching this deliverable
5. Confirm the file was written to the user
6. If no project `CLAUDE.md` exists, present the output for manual copying
