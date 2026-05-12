---
name: design
description: Full Design & UX workflow orchestrator — runs all phases from UX brief through design handoff, pausing for approval at each checkpoint. Use when starting a new design effort end-to-end.
disable-model-invocation: true
---

Run the full Design & UX workflow for: $ARGUMENTS

> **Learning note — Design & UX Workflow**
> The design process bridges product intent and engineering reality. Before a single line of code is written, design makes the feature tangible — defining what each screen looks like, how users move between them, and what happens at each interaction state. A structured design process (brief → wireframes → review → handoff) prevents the failure mode of engineering building something that technically meets the spec but doesn't work for users. Each phase builds on the last, with checkpoints where you can course-correct while the cost of changing things is still low.

Display the learning note above verbatim to the user before proceeding.

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

---

**Review-Iterate-Approve standard — applies at phases marked with a designated reviewer**

At any phase that designates a reviewer below, follow this loop automatically — do not skip it:

1. **Run the reviewer** — invoke the designated agent immediately after presenting the phase deliverable. Do not ask whether to run it; just run it.
2. **Present findings** — summarise critical gaps, high-priority issues, and recommendations from the reviewer's output. Group by severity (Critical / High / Medium).
3. **Ask what to update** — after the findings, always ask: *"What would you like to update based on this review? List the specific items you want changed, or say **'approved'** if you're satisfied and ready to move on."*
4. **Apply updates** — make the changes the user requests to the deliverable.
5. **Re-run the reviewer** — run the same reviewer again on the updated deliverable.
6. **Repeat** from step 2 until the user explicitly says **"approved"**.
7. **Only then** proceed to the next phase checkpoint and save the file.

---

**Phase lookup table — use this to populate the block at each checkpoint:**

| After this phase | Recommended next step | Optional to run |
|-----------------|----------------------|-----------------|
| Phase 1 — UX Brief | Phase 2 — Wireframe Spec | `/brainstorm` skill *(design-ux-kit)* — run if the UX brief has surfaced multiple viable design directions before committing to screen architecture in the wireframe spec |
| Phase 2 — Wireframe Spec | Phase 3 — HTML Mockup | `user-research-planner` agent *(design-ux-kit)* — validate open design questions before building mockups; `pm-design-reviewer` agent *(design-ux-kit)* — requirements coverage check on the spec |
| Phase 3 — HTML Mockup | Phase 4 — Design Review | `ux-reviewer` agent *(design-ux-kit)* — structured heuristic audit on the mockup |
| Phase 4 — Design Review | Phase 5 — Usability Test Plan (if UX unknowns) or Phase 6 — Design Handoff | `ux-reviewer` agent *(design-ux-kit)* — deeper structured audit; `pm-design-reviewer` agent *(design-ux-kit)* — PM-perspective requirements check |
| Phase 5 — Usability Test Plan | Phase 6 — Design Handoff | `user-research-planner` agent *(design-ux-kit)* — formal study if test uncovered deep unknowns |
| Phase 6 — Design Handoff *(final)* | **Start dev: run `/dev [feature]`** | `pm-design-reviewer` agent *(design-ux-kit)* — final requirements coverage check before dev handoff; `/premortem` skill *(exec-kit)* — assume the project has already failed and surface design and UX risks before committing to the build; `/dashboard` skill *(exec-kit)* — regenerate the HTML project hub to include all design documents and the interactive wireframe |

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

> **Optional**: Run `/brainstorm` if the UX brief has surfaced multiple viable design directions — brainstorm explores layout, interaction, and navigation concepts with real-world examples and ranked recommendations before you commit to screen architecture in the wireframe spec. Phase 3 (HTML Mockup) includes a lighter direction check, but `/brainstorm` is more thorough and produces artefacts you can reference throughout the design phase.

---

## Phase 2 — Information Architecture & Flow

Produce a wireframe specification following the process and template of the `/wireframe-spec` skill, based on the approved UX brief — apply the wireframe-template.md structure and steps.

- Read `pm/user-stories.md` and map every P0 story to the screen(s) it requires — explicitly list this mapping so nothing is missed
- Map the key screens, user flows, and navigation structure
- Define component inventory and interaction states for each screen
- Note any branching paths, error states, or edge cases

After presenting the spec, immediately run the **Review-Iterate-Approve loop** *(designated reviewer: `pm-design-reviewer`)*:

1. Run the `pm-design-reviewer` agent on the wireframe spec just produced.
2. Present its findings (requirements coverage gaps, missing user flows, handoff readiness issues).
3. Ask: *"What would you like to update based on this review? List specific items, or say **'approved'** to move on."*
4. Apply updates, re-run `pm-design-reviewer`, repeat until the user says **"approved"**.

After the loop, separately offer: *"Want me to also run the `user-research-planner` agent to assess whether any open design questions need user validation before we build the HTML mockup?"* If the user accepts and findings require changes, update the wireframe spec before proceeding.

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

After presenting the review, immediately run the **Review-Iterate-Approve loop** *(designated reviewer: `ux-reviewer`)*:

1. Run the `ux-reviewer` agent on the HTML mockup and design review just produced — deep structured audit against Nielsen's 10 heuristics and WCAG 2.1 AA.
2. Present its findings (usability issues, accessibility gaps, missing states), grouped by severity.
3. Ask: *"What would you like to update based on this review? List specific screens, flows, or components to change, or say **'approved'** to move on."*
4. Apply updates to the HTML mockup (`design/wireframes/wireframe.html`) and wireframe spec (`design/wireframe-spec.md`) as needed.
5. **Upstream PM cascade** — after applying any design updates, check the project `CLAUDE.md` status table for PM artifacts that are no longer "Not started". Design changes can surface requirements gaps or scope adjustments that must flow back:

   | PM artifact | If status is not "Not started" | What to check |
   |------------|-------------------------------|---------------|
   | PRD (`pm/prd.md`) | Flag for review | Do design changes reveal missing, ambiguous, or conflicting requirements? |
   | User stories (`pm/user-stories.md`) | Flag for review | Do new flows, edge cases, or states need new or updated stories? |
   | Brief (`pm/brief.md`) | Flag for review | Do design changes affect stated scope, users, or success criteria? |

   Tell the user which PM artifacts are affected and what specifically needs updating. Apply PM document updates before proceeding. Add to the Document Sync Queue in the state file if one exists.

6. Re-run `ux-reviewer` on the updated artifacts, repeat from step 2 until the user says **"approved"**.

After the loop, separately offer: *"Want me to also run the `pm-design-reviewer` agent to confirm all PRD requirements are covered before handoff?"*

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

After presenting the handoff spec, immediately run the **Review-Iterate-Approve loop** *(designated reviewer: `pm-design-reviewer`)*:

1. Run the `pm-design-reviewer` agent on the complete handoff spec — checks every requirement is covered and the spec is specific enough for a developer to build without a sync meeting.
2. Present its findings (uncovered requirements, underspecified interactions, handoff gaps).
3. Ask: *"What would you like to update based on this review? List specific sections or screens to revise, or say **'approved'** to finalise the handoff."*
4. Apply updates, re-run `pm-design-reviewer`, repeat until the user says **"approved"**.

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the design handoff to the file listed for `/design-handoff`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Checkpoint 6**: Present the complete handoff package. Confirm the design workflow is complete.
