---
name: design
description: Full Design & UX workflow orchestrator — runs all phases from UX brief through design handoff, pausing for approval at each checkpoint. Use when starting a new design effort end-to-end.
disable-model-invocation: true
---

Run the full Design & UX workflow for: $ARGUMENTS

**Output standard — diagrams**: All documents are read in Obsidian. Use Mermaid syntax (` ```mermaid ` blocks) for every diagram — Obsidian renders these natively. Never use ASCII art for diagrams. Relevant types: `flowchart` (user flows, navigation maps), `sequenceDiagram` (interaction flows between user and system), `stateDiagram-v2` (screen states and transitions).

**Output standard — tables**: Always include a blank line before any Markdown table. Obsidian requires this to render `|` syntax as a table rather than plain text.

Work through each phase below sequentially. After completing each phase, present the output and ask the user: "Ready to continue to Phase [N+1], or would you like to revise anything?"

---

**Navigation standard — applies at every checkpoint**

After presenting each phase output, always append a **What's next?** block before waiting for the user's response. Use this exact format:

> **What's next?** [Recommended next step — next phase name, or next workflow if this is the final phase]
>
> **Optionally run at this point:**
>
> | Skill / Agent | Plugin | What it does |
> |--------------|--------|-------------|
> | `name` | kit | One-line description |
>
> *Reply with the name of anything you'd like to run first, or say "continue" to proceed.*

If no optional skills or agents apply at a given phase, omit the table and just show the next step recommendation.

**Phase lookup table — use this to populate the block at each checkpoint:**

| After this phase | Recommended next step | Optional to run |
|-----------------|----------------------|-----------------|
| Phase 1 — UX Brief | Phase 2 — Wireframe Spec | No additional agents at this point — brief pulls directly from PM inputs |
| Phase 2 — Wireframe Spec | Phase 3 — HTML Mockup | `user-research-planner` agent *(design-ux-kit)* — validate open design questions before building mockups; `pm-design-reviewer` agent *(design-ux-kit)* — requirements coverage check on the spec |
| Phase 3 — HTML Mockup | Phase 4 — Design Review | `ux-reviewer` agent *(design-ux-kit)* — structured heuristic audit on the mockup |
| Phase 4 — Design Review | Phase 5 — Usability Test Plan (if UX unknowns) or Phase 6 — Design Handoff | `ux-reviewer` agent *(design-ux-kit)* — deeper structured audit; `pm-design-reviewer` agent *(design-ux-kit)* — PM-perspective requirements check |
| Phase 5 — Usability Test Plan | Phase 6 — Design Handoff | `user-research-planner` agent *(design-ux-kit)* — formal study if test uncovered deep unknowns |
| Phase 6 — Design Handoff *(final)* | **Start dev: run `/dev [feature]`** | `pm-design-reviewer` agent *(design-ux-kit)* — final requirements coverage check before dev handoff |

---

## Phase 1 — UX Brief

Produce a UX brief following the process and template of the `/ux-brief` skill — apply the ux-brief-template.md structure and steps.

**Before writing the brief, read the available PM inputs:**
- Check `pm/brief.md` for scope boundary, users, success criteria, and key assumptions
- Check `pm/user-stories.md` for P0/P1/P2 stories and acceptance criteria
- Check `pm/prd.md` if brief or stories are not available

Pull scope, users, and success criteria directly from these documents. Do not ask the user to re-enter what has already been decided. Map each design goal to one or more P0 user stories.

- Define the design scope (from product brief), target users (from product brief), goals, constraints, and success criteria
- Surface any new design-specific assumptions beyond those already in the product brief
- Identify research gaps — note these for the wireframe spec phase (user research decisions are made after the wireframe spec, not before)

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the UX brief to the file listed for `/ux-brief`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Checkpoint 1**: Get approval before moving to Phase 2.

---

## Phase 2 — Information Architecture & Flow

Produce a wireframe specification following the process and template of the `/wireframe-spec` skill, based on the approved UX brief — apply the wireframe-template.md structure and steps.

- Read `pm/user-stories.md` and map every P0 story to the screen(s) it requires — explicitly list this mapping so nothing is missed
- Map the key screens, user flows, and navigation structure
- Define component inventory and interaction states for each screen
- Note any branching paths, error states, or edge cases

After presenting the spec, offer: *"Want me to run the `user-research-planner` agent on this wireframe spec? It will assess whether any open design questions or assumptions need user validation before we build the HTML mockup. If it surfaces changes, we'll update the spec before moving to mockups."*

If the user accepts and research findings require design direction changes, update the wireframe spec before proceeding.

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the wireframe spec to the file listed for `/wireframe-spec`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Checkpoint 2**: Get approval before moving to Phase 3.

---

## Phase 3 — HTML Mockup & Iteration

Produce an interactive HTML wireframe following the process of the `/wireframe-html` skill:

1. **Brainstorm design directions** — present 2–3 distinct layout/interaction directions (name, 2–3 sentence description, real-world example, key design assumption). Ask the user which direction to build before writing any HTML. If a `/brainstorm` has already been run and a direction was chosen, confirm it and proceed.

2. **Produce the HTML mockup** — single self-contained file (inline CSS + minimal vanilla JS). Cover all screens from the wireframe spec. Include a screen navigation bar, mobile/desktop viewport toggle, all states (default, error, empty, loading), and inline design annotations. Style as a clear wireframe (monochrome, placeholder boxes, placeholder text).

3. **Collect feedback** — present the HTML in a fenced code block. Ask specifically: layout fit for the user's context, missing screens or states, confusing flows, unmet PRD requirements.

4. **Iterate** — apply feedback and produce an updated file. List changes made before the code block. Keep a running changelog as HTML comments in `<head>`. After 3 rounds, recommend running the `ux-reviewer` agent before continuing.

5. **Surface PM document updates** — after the mockup is approved, identify discoveries (edge cases, ambiguous requirements, new constraints) that should flow back to product documents. State exactly which document to update and what to change. Ask the user before making edits.

*After user approves: Save the HTML file. If the project `CLAUDE.md` has an output path for `/wireframe-html`, save there — otherwise save as `design/wireframe.html`. Update the **Project status** table. Confirm the file path.*

**Checkpoint 3**: Get approval on the final mockup before moving to Phase 4.

---

## Phase 4 — Design Review

Conduct a heuristic design review following the process and template of the `/design-review` skill, applied to the approved HTML mockup and wireframe spec — use the design-review-template.md structure.

- Evaluate against Nielsen's 10 usability heuristics
- Flag accessibility concerns (WCAG 2.1 AA)
- Surface inconsistencies, friction points, and missing states

After presenting the review, offer two options:
- *"Want me to run the `ux-reviewer` agent for a deeper structured audit? (Designer perspective — heuristics, accessibility, missing states)"*
- *"Want me to run the `pm-design-reviewer` agent to check coverage against your PRD or brief? (PM perspective — requirements coverage, user flow completeness, handoff readiness)"*

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the design review to the file listed for `/design-review`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Checkpoint 4**: Get approval (and incorporate any revisions) before moving to Phase 5.

---

## Phase 5 — Usability Test Plan

*Run if there are genuine UX unknowns — novel interaction patterns, unclear user mental models, or significant deviation from existing conventions. If no UX unknowns exist, note: "Usability test not run — add back before v2 if user adoption is lower than expected." and proceed to Phase 6.*

Produce a usability test plan following the process and template of the `/usability-test` skill — apply the usability-test-template.md structure and steps.

- Define test objectives, participant criteria, and task scenarios
- Specify success metrics and how results will be analyzed
- Include a discussion guide outline

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the usability test plan to the file listed for `/usability-test`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Checkpoint 5**: Get approval before moving to Phase 6.

---

## Phase 6 — Design Handoff

Produce a design handoff spec following the process and template of the `/design-handoff` skill — apply the design-handoff-template.md structure and steps.

- Document every screen with component inventory, states, and interaction specs
- Reference the approved HTML mockup as the source of truth for states and interactions
- Define acceptance criteria engineering can verify
- List open questions and decisions deferred to implementation

After presenting the handoff spec, offer: *"Want me to run the `pm-design-reviewer` agent one final time against the complete handoff? It checks that every requirement is covered and the spec is specific enough for a developer to build without a sync meeting."*

*After presenting: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the design handoff to the file listed for `/design-handoff`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Checkpoint 6**: Present the complete handoff package. Confirm the design workflow is complete.
