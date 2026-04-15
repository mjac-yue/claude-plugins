---
name: competitive-analysis
description: Create a structured competitive analysis using existing knowledge — no live web search. Best for quick framing, known markets, or when feeding into a larger workflow. For live research across 3+ competitors in parallel, use the competitive-analyst agent instead.
disable-model-invocation: true
---

Create a competitive analysis for: $ARGUMENTS

> **Learning note — Competitive Analysis**
> Understanding the competitive landscape before you design or build tells you what's already been tried, what users are already accustomed to, and where genuine whitespace exists. It also helps you avoid building something that already exists — or missing a simple positioning angle that would make your product stand out. You don't need to outperform every competitor on every dimension; you need to be better than alternatives on the dimensions that matter most to your target user.

Display the learning note above verbatim to the user before proceeding.

**Output standard — tables**: All documents are read in Obsidian. Always include a blank line before any Markdown table — Obsidian requires this to render `|` syntax as a table rather than plain text.

Use the template in [competitive-template.md](competitive-template.md) as the structure.

Follow this process:
1. Identify the key competitors or alternatives to analyze (ask if unclear).
2. For each competitor, assess:
   - **Positioning** — who they target, their key value prop
   - **Key Features** — what they offer relative to our focus area
   - **Strengths** — what they do well
   - **Weaknesses / Gaps** — where they fall short
   - **Pricing** — model and price points if known
   - **Market Position** — market share, traction signals, funding
3. Produce a comparison matrix for quick visual reference.
4. Synthesize findings into:
   - **Competitive Whitespace** — opportunities competitors aren't addressing
   - **Differentiation Opportunities** — where we can win
   - **Threats** — what we need to defend against
   - **Strategic Recommendations** — 3 concrete actions based on analysis

Use publicly known information. Flag any assumptions or gaps in your research.

## Save output

After presenting the competitive analysis to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/competitive-analysis` and save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. In that same project `CLAUDE.md`, find the **Project status** table and set the **Status** column to **Done** for the row matching this deliverable
5. Confirm the file was written to the user
6. If no project `CLAUDE.md` exists, present the output for manual copying
