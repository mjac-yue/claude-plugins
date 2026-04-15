---
name: brief
description: Write a one-page feature brief — a lightweight alternative to a full PRD for smaller features, experiments, or spikes. Covers the problem, proposed solution, success criteria, and scope boundary. Output feeds directly into /ux-brief or /tech-spec without needing the full PM workflow.
disable-model-invocation: true
---

Write a feature brief for: $ARGUMENTS

> **Learning note — Feature Brief**
> A feature brief is the one-page alternative to a full PRD — it captures the essential problem, solution, and success criteria without requiring a full requirements process. Briefs are most useful early in discovery (before you've committed to an approach) and for smaller features where a full PRD would be overkill. The brief is typically the first document design and engineering read, so clarity here prevents questions and misalignment later.

Display the learning note above verbatim to the user before proceeding.

**Output standard — tables**: All documents are read in Obsidian. Always include a blank line before any Markdown table — Obsidian requires this to render `|` syntax as a table rather than plain text.

Use the template in [brief-template.md](brief-template.md) as the structure.

Follow this process:

1. **Write a sharp problem statement** — one to two sentences maximum. What is the user struggling to do, and what is the cost of that struggle? If you can't state the problem in two sentences, ask a clarifying question before proceeding.

2. **Describe the proposed solution** — two to three sentences on what will be built. Stay at the "what", not the "how". Avoid implementation detail.

3. **Identify who benefits** — primary user and any secondary stakeholders affected. One line each.

4. **Define success criteria** — two to three measurable signals that confirm the feature is working. Prefer outcome metrics (task completion rate, time saved, adoption) over output metrics (feature shipped, pages created).

5. **Draw the scope boundary** — explicitly state what this brief does NOT include. This prevents scope creep from the first conversation.

6. **List key assumptions** — the two to three beliefs about users, behavior, or context that this brief depends on. Flag which assumption carries the most risk if wrong.

7. **Surface open questions** — anything that must be answered before design or development starts. Assign an owner and urgency if known.

8. **Recommend next step** — based on the feature type and complexity, recommend which skill to run next:
   - Use `/ux-brief` if the feature has meaningful user-facing UX to design
   - Use `/tech-spec` if the implementation approach needs to be decided before design
   - Use `/prd` if this feature is large enough to warrant full requirements documentation
   - Use `/tech-stack` first if the product's technology choices haven't been made yet

Keep the entire brief to one page. If the feature is too complex to fit in one page, recommend running `/prd` instead.

## Save output

After presenting the brief to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/brief` and save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. In that same project `CLAUDE.md`, find the **Project status** table and set the **Status** column to **Done** for the row matching this deliverable
5. Confirm the file was written to the user
6. If no project `CLAUDE.md` exists, present the output for manual copying
