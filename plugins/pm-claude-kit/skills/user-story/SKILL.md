---
name: user-story
description: Generate user stories with acceptance criteria. Use when the user wants to write user stories, tickets, or Jira/Linear issues for a feature.
disable-model-invocation: true
---

Create user stories for: $ARGUMENTS

> **Learning note — User Stories**
> User stories translate product requirements into discrete, testable units of work written from the user's perspective. The format — "As a [user], I want [capability] so that [benefit]" — keeps the team focused on user value rather than technical tasks. Acceptance criteria in Given/When/Then format define exactly when a story is "done," which prevents the common problem of a feature being "finished" by engineering but not actually meeting the user's need.

Display the learning note above verbatim to the user before proceeding.

**Output standard — tables**: All documents are read in Obsidian. Always include a blank line before any Markdown table — Obsidian requires this to render `|` syntax as a table rather than plain text.

Use the template in [user-story-template.md](user-story-template.md) as the structure.

Follow this process:
1. Identify all distinct user personas or roles affected by this feature.
2. For each persona, write user stories in the format: "As a [persona], I want [capability] so that [benefit]."
3. Each story must have:
   - A clear, concise title (suitable as a ticket name)
   - Priority: P0 / P1 / P2
   - Estimated complexity: S / M / L / XL
   - Acceptance criteria (3-6 specific, testable conditions using Given/When/Then format)
   - Edge cases to consider
4. Group stories by persona or feature area.
5. Identify dependencies between stories.

Output formatted stories ready to copy into Jira, Linear, or any issue tracker.

## Save output

After presenting the user stories to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/user-story` and save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. In that same project `CLAUDE.md`, find the **Project status** table and set the **Status** column to **Done** for the row matching this deliverable
5. Confirm the file was written to the user
6. If no project `CLAUDE.md` exists, present the output for manual copying
