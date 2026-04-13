---
name: ux-brief
description: Create a UX brief that defines the scope, target users, goals, constraints, and success criteria for a design effort. Use at the start of any design project to align the team before wireframing begins.
disable-model-invocation: true
---

Create a UX brief for: $ARGUMENTS

**Output standard — tables**: All documents are read in Obsidian. Always include a blank line before any Markdown table — Obsidian requires this to render `|` syntax as a table rather than plain text.

Use the template in [ux-brief-template.md](ux-brief-template.md) as the structure.

## Step 0: Read available PM inputs

Before writing anything, check for the following documents in the project directory (usually under `pm/`). Pull directly from these rather than asking the user to repeat what's already been decided:

- **Product brief** (`pm/brief.md`) — scope boundary, users, success criteria, and key assumptions from the PM workflow. Use this as the primary source of truth for design scope and users.
- **User stories** (`pm/user-stories.md`) — P0/P1/P2 stories with acceptance criteria. These define exactly what the design must enable users to do.
- **PRD** (`pm/prd.md`) — full requirements, out-of-scope items, risks. Reference if brief or stories are not yet available.

If none of these exist, ask the user to provide the feature description before proceeding.

## Step 1–7: Produce the UX brief

Follow this process, drawing from the PM inputs above:

1. **Define the design scope** — what experience or flow is being designed? Derive directly from the product brief's scope boundary. What is explicitly out of scope?
2. **Identify target users** — pull the primary and secondary users from the product brief. Expand with any additional context about their goals, context, and pain points relevant to design.
3. **Articulate design goals** — what should the user be able to do or feel after this experience? Map each design goal to one or more P0 user stories so design coverage can be verified later.
4. **List constraints** — platform, technical, accessibility, brand, timeline, or resource constraints that will shape design decisions.
5. **Define success criteria** — pull from the brief's success criteria and connect to design-specific signals (task completion rate, error rate, satisfaction score, etc.).
6. **Surface assumptions** — carry forward the highest-risk assumptions from the product brief, plus any new design-specific assumptions about user mental models, interaction patterns, or information architecture.
7. **Identify research gaps** — flag what we don't know that could materially affect design direction. Recommend whether user research is needed before proceeding.

Ask clarifying questions only for gaps not answered by the PM inputs. Output a brief ready to share with design, product, and engineering stakeholders.

## Save output

After presenting the UX brief to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/ux-brief` and save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. In that same project `CLAUDE.md`, find the **Project status** table and set the **Status** column to **Done** for the row matching this deliverable
5. Confirm the file was written to the user
6. If no project `CLAUDE.md` exists, present the output for manual copying
