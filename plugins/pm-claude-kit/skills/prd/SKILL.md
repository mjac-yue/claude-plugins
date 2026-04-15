---
name: prd
description: Generate a Product Requirements Document (PRD) for a feature or product. Use when the user wants to write a PRD, spec, or requirements document.
disable-model-invocation: true
---

Write a Product Requirements Document (PRD) for: $ARGUMENTS

> **Learning note — Product Requirements Document**
> A PRD is the primary communication artifact between product management and the rest of the team. It answers three core questions in one document: what problem are we solving, who has it, and what does a good solution look like? Without a PRD, engineers and designers make assumptions independently — and those assumptions often diverge. A well-written PRD doesn't constrain creativity; it focuses it so everyone is working toward the same outcome.

Display the learning note above verbatim to the user before proceeding.

**Output standard — diagrams**: All documents are read in Obsidian. Use Mermaid syntax (` ```mermaid ` blocks) for all diagrams — Obsidian renders these natively. Never use ASCII art or plain-text flow descriptions where a diagram would be clearer.

**Output standard — tables**: Always include a blank line before any Markdown table. Obsidian requires this to render `|` syntax as a table rather than plain text.

Use the template in [prd-template.md](prd-template.md) as the structure.

Follow this process:
1. If the user's input is brief, ask 2-3 clarifying questions before writing (target audience, key problem, success metric). If the input is detailed, proceed directly.
2. Fill every section of the template with specific, concrete content — no placeholder text.
3. For the "Out of Scope" section, think carefully about what related things this feature does NOT include.
4. For success metrics, always propose at least one leading indicator and one lagging indicator.
5. Flag any open questions or assumptions made in a final "Open Questions" section.

**Diagram instructions**:

- **User Journey / Flow**: Always produce a real Mermaid `flowchart TD` using the actual steps for this feature. If the journey has decision points or branching paths (e.g. new vs returning user, success vs error), show them as diamond nodes. If the journey is a back-and-forth interaction between user and system, use a `sequenceDiagram` instead.
- **Dependencies**: Always produce a real Mermaid `flowchart LR` showing actual teams, systems, and prerequisite work. Arrows point in the direction of dependency. Only include nodes that genuinely apply — don't pad with empty placeholders.

Output the completed PRD as a markdown document ready to share or save.

## Save output

After presenting the PRD to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/prd` and save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. In that same project `CLAUDE.md`, find the **Project status** table and set the **Status** column to **Done** for the row matching this deliverable
5. Confirm the file was written to the user
6. If no project `CLAUDE.md` exists, present the output for manual copying
