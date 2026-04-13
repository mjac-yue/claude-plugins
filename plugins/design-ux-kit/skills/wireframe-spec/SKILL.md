---
name: wireframe-spec
description: Generate a wireframe specification — describing screens, user flows, components, and interaction states in structured text. Use when you need a design blueprint before visual design or prototyping.
disable-model-invocation: true
---

Generate a wireframe specification for: $ARGUMENTS

**Output standard — tables**: All documents are read in Obsidian. Always include a blank line before any Markdown table — Obsidian requires this to render `|` syntax as a table rather than plain text.

Use the template in [wireframe-template.md](wireframe-template.md) as the structure.

Follow this process:
1. **Map the user flow** — identify the entry point, happy path, and exit points. Draw the flow as a numbered sequence of steps.
2. **Inventory the screens** — list every distinct screen or state required to complete the flow.
3. **Specify each screen**, including:
   - **Purpose** — what the user is trying to accomplish on this screen
   - **Layout zones** — header, nav, content area, sidebar, footer, modals
   - **Components** — every UI element present (inputs, buttons, labels, cards, tables, etc.) with their labels and placeholder content
   - **States** — empty state, loading state, error state, success state, disabled state (as applicable)
   - **Actions** — what the user can do and what happens next
4. **Define interaction behaviors** — hover, focus, validation, animation, transitions between screens
5. **Call out edge cases** — what happens if the user has no data, hits an error, or takes an unexpected path?
6. **Flag open design questions** — decisions that need stakeholder input before visual design begins

Use plain-language descriptions. This spec should be detailed enough that a designer can produce visuals and an engineer can estimate effort without further clarification.

## Save output

After presenting the wireframe specification to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/wireframe-spec` and save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. In that same project `CLAUDE.md`, find the **Project status** table and set the **Status** column to **Done** for the row matching this deliverable
5. Confirm the file was written to the user
6. If no project `CLAUDE.md` exists, present the output for manual copying
