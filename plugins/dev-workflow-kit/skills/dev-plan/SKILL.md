---
name: dev-plan
description: Generate a development plan with task breakdown, estimates, dependencies, and sprint allocation. Use after a tech spec is approved to translate it into an actionable engineering plan.
disable-model-invocation: true
---

Generate a development plan for: $ARGUMENTS

> **Learning note — Development Plan**
> A development plan breaks a feature into discrete, sequenced tasks with estimates and dependencies. Without it, engineers often start on the wrong pieces (building UI before the API it depends on), block each other, or discover at the end that the work was larger than expected. The dev plan is the bridge between "what to build" (tech spec) and "how we'll build it in what order" — it makes engineering work predictable and surfaces sequencing problems before they become schedule problems.

Display the learning note above verbatim to the user before proceeding.

**Output standard — tables**: All documents are read in Obsidian. Always include a blank line before any Markdown table — Obsidian requires this to render `|` syntax as a table rather than plain text.

Use the template in [dev-plan-template.md](dev-plan-template.md) as the structure.

## Step 0: Read required inputs

All three of the following must be complete before the dev plan is written. Check for them in the project directory:

- **Tech spec** (`dev/tech-spec.md`) — includes the decided tech stack, data model, and component breakdown. Required.
- **Arch design** (`dev/arch-design.md`) — defines component boundaries, integration patterns, and the build sequencing constraints. Required. The dev plan task order must respect these dependencies.
- **API spec** (`dev/api-spec.md`) — defines endpoint tasks that must be implemented. Required if the feature has APIs. If API spec was skipped (no APIs), note this and proceed.
- **Design handoff** (`design/design-handoff.md`) — acceptance criteria per screen. Use to ensure every build task has a clear "done" condition linked to the design.

If the tech spec or arch design are missing, stop and ask the user to complete those phases first.

## Step 1–8: Produce the dev plan

Follow this process:
1. **Restate the goal and constraints** — what is being built, by when, and with what team size or resource constraints?
2. **Break down the work into tasks**. For each task:
   - Clear name and description
   - Engineering discipline (frontend, backend, infrastructure, data, etc.)
   - Estimate in story points or days (include reasoning for non-obvious estimates)
   - Dependencies (which other tasks must be complete first)
   - Owner role (which type of engineer should own this)
3. **Identify the critical path** — the sequence of dependent tasks that determines the earliest possible completion date. Use the arch design's component boundaries to determine what must be built before what.
4. **Flag blockers** — anything that must be resolved, decided, or procured before work can start (design assets, API keys, third-party contracts, platform decisions)
5. **Propose sprint allocation** — group tasks into sprints (1- or 2-week), accounting for dependencies and parallelism. Assume typical capacity (e.g., 70–80% for planned work, remainder for reviews and unplanned).
6. **Define milestones** — meaningful checkpoints (e.g., "API complete and tested", "feature flag off in staging") that signal progress
7. **Highlight risks to the plan** — what could cause a slip, and what's the mitigation or contingency?
8. **Definition of Done** — the specific conditions that mark the feature complete and ready for QA handoff

Output a plan ready to drop into a sprint planning doc or project tracker.

## Save output

After presenting the development plan to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/dev-plan` and save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. In that same project `CLAUDE.md`, find the **Project status** table and set the **Status** column to **Done** for the row matching this deliverable
5. Confirm the file was written to the user
6. If no project `CLAUDE.md` exists, present the output for manual copying
