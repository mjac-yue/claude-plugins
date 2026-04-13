---
name: design
description: Full Design & UX workflow orchestrator — runs all phases from discovery through handoff, pausing for approval at each checkpoint. Use when starting a new design effort end-to-end.
disable-model-invocation: true
---

Run the full Design & UX workflow for: $ARGUMENTS

**Output standard — diagrams**: All documents are read in Obsidian. Use Mermaid syntax (` ```mermaid ` blocks) for every diagram — Obsidian renders these natively. Never use ASCII art for diagrams. Relevant types: `flowchart` (user flows, navigation maps), `sequenceDiagram` (interaction flows between user and system), `stateDiagram-v2` (screen states and transitions).

**Output standard — tables**: Always include a blank line before any Markdown table. Obsidian requires this to render `|` syntax as a table rather than plain text.

Work through each phase below sequentially. After completing each phase, present the output and ask the user: "Ready to continue to Phase [N+1], or would you like to revise anything?"

---

## Phase 0 — Project Profile

Before producing anything, establish the project tier. If a Project Profile Card was already produced by exec-kit's `/release` skill, accept it and skip this phase.

Otherwise ask: *"How would you describe the size of this project — Micro (days–2w), Small (2–6w), Medium (6–16w), or Large (16w+)?"*

Then apply the phase gating below:

| Tier | Default phases | Not default — add back if needed |
|------|---------------|----------------------------------|
| **Tier 1 (Micro)** | If there is a UI change: describe it in plain prose (2–3 sentences). No formal design output needed by default. | All phases |
| **Tier 2 (Small)** | Phase 1 (abbreviated UX brief), Phase 2 (key screens only), Phase 3 (HTML mockup for key screens — serves as handoff). | Phases 4, 5, 6 |
| **Tier 3 (Medium)** | Phases 1, 2, 3, 4, 6. Phase 5 (usability test) if genuine UX unknowns exist. | Phase 5 (usability test) |
| **Tier 4 (Large)** | All phases. | — |

**Step C — Skipped phase opt-in**

After establishing the tier, present the phases not included by default and ask:

*"Before we start — the following phases are skipped by default for your tier. Would you like to add any of them back in?"*

Present only the phases skipped for the established tier, using this description for each:

| Phase | What it adds | When to add it back |
|-------|-------------|---------------------|
| Phase 1 — UX Brief | Full brief with research recommendations, constraints, success criteria, and assumptions to validate | Complex user problem, multiple user types, or significant unknowns before design begins |
| Phase 2 — Wireframe Spec | Full IA and flow document: all screens, user flows, component inventory, edge cases | Need a written spec alongside or instead of HTML mockups |
| Phase 3 — HTML Mockup | Interactive HTML wireframes per screen with iteration rounds | Need a browser-viewable, shareable prototype before design review or handoff |
| Phase 4 — Design Review | Heuristic audit against Nielsen's 10 usability heuristics + WCAG 2.1 AA | Multiple screens or complex interactions worth auditing before handoff |
| Phase 5 — Usability Test Plan | Test script, participant criteria, task scenarios, and success metrics | Novel interactions, unclear user mental models, or high-risk flows that need validation |
| Phase 6 — Design Handoff | Full component inventory, interaction specs, and acceptance criteria per screen | Engineering team needs a formal written spec beyond the HTML mockup |

Accept any number of additions. Confirm: *"Got it — I'll include [X, Y] in addition to the defaults. Here's the updated phase list for this session: [list]."*

**Checkpoint 0**: Confirm tier and phase list before proceeding.

---

## Phase 1 — UX Brief — *Tier 2–4*

**Tier 2**: Abbreviated — cover design scope, target user (one sentence), goal, and the top two constraints. Skip research recommendations and success criteria table. Output as a short paragraph, not the full template.
**Tier 3–4**: Full output below.

Produce a UX brief following the process and template of the `/ux-brief` skill — apply the ux-brief-template.md structure and steps.

- Define the design scope, target users, goals, constraints, and success criteria
- Surface any assumptions that need validation before design begins
- Identify what user research (if any) is needed before proceeding

After presenting the brief, offer: *"Want me to run the `user-research-planner` agent? It will assess whether formal user research is feasible or produce a faster assumption validation plan if it isn't — recommended before committing to a design direction."*

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the UX brief to the file listed for `/ux-brief`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Checkpoint 1**: Get approval before moving to Phase 2.

---

## Phase 2 — Information Architecture & Flow — *Tier 2–4*

**Tier 2**: Key screens only — identify the 2–4 screens or states that are new or significantly changed. Describe each screen's layout, components, and interactions in plain text. This output also serves as the design handoff for Tier 2 — no separate Phase 5 needed.
**Tier 3–4**: Full wireframe specification below.

Produce a wireframe specification following the process and template of the `/wireframe-spec` skill, based on the approved UX brief — apply the wireframe-template.md structure and steps.

- Map the key screens, user flows, and navigation structure
- Define component inventory and interaction states for each screen
- Note any branching paths, error states, or edge cases

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the wireframe spec to the file listed for `/wireframe-spec`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Checkpoint 2**: Get approval before moving to Phase 3.

---

## Phase 3 — HTML Mockup & Iteration — *Tier 2–4*

**Tier 2**: Produce HTML for the 2–4 key screens from Phase 2. Run 1–2 iteration rounds. The approved HTML mockup serves as the design handoff for Tier 2 — no separate Phase 6 needed.
**Tier 3–4**: Full process below.

Produce an interactive HTML wireframe following the process of the `/wireframe-html` skill:

1. **Brainstorm design directions** — present 2–3 distinct layout/interaction directions (name, 2–3 sentence description, real-world example, key design assumption). Ask the user which direction to build before writing any HTML. If a `/brainstorm` has already been run and a direction was chosen, confirm it and proceed.

2. **Produce the HTML mockup** — single self-contained file (inline CSS + minimal vanilla JS). Cover all screens from the wireframe spec. Include a screen navigation bar, mobile/desktop viewport toggle, all states (default, error, empty, loading), and inline design annotations. Style as a clear wireframe (monochrome, placeholder boxes, placeholder text).

3. **Collect feedback** — present the HTML in a fenced code block. Ask specifically: layout fit for the user's context, missing screens or states, confusing flows, unmet PRD requirements.

4. **Iterate** — apply feedback and produce an updated file. List changes made before the code block. Keep a running changelog as HTML comments in `<head>`. After 3 rounds, recommend running the `ux-reviewer` agent before continuing.

5. **Surface PM document updates** — after the mockup is approved, identify discoveries (edge cases, ambiguous requirements, new constraints) that should flow back to product documents. State exactly which document to update and what to change. Ask the user before making edits.

*After user approves: Save the HTML file. If the project `CLAUDE.md` has an output path for `/wireframe-html`, save there — otherwise save as `design/wireframe.html`. Update the **Project status** table. Confirm the file path.*

**Checkpoint 3**: Get approval on the final mockup before moving to Phase 4.

---

## Phase 4 — Design Review — *Tier 3–4 only*

**Tier 1–2**: Not included by default — the HTML mockup from Phase 3 is sufficient for simple projects. Add back if needed.

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

## Phase 5 — Usability Test Plan — *Tier 4, or Tier 3 if UX unknowns exist*

**Tier 1–2**: Not included by default. Add back if needed.
**Tier 3**: Run only if there are genuine UX unknowns — novel interaction patterns, unclear user mental models, or significant deviation from existing conventions. Otherwise not included by default — note: *"Usability test not run — add back before v2 if user adoption is lower than expected."*

Produce a usability test plan following the process and template of the `/usability-test` skill — apply the usability-test-template.md structure and steps.

- Define test objectives, participant criteria, and task scenarios
- Specify success metrics and how results will be analyzed
- Include a discussion guide outline

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the usability test plan to the file listed for `/usability-test`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Checkpoint 5**: Get approval before moving to Phase 6.

---

## Phase 6 — Design Handoff — *Tier 3–4 only*

**Tier 1–2**: Not included by default — the HTML mockup from Phase 3 serves as the handoff for Tier 2. Tier 1 needs no handoff doc. Add back if needed.

Produce a design handoff spec following the process and template of the `/design-handoff` skill — apply the design-handoff-template.md structure and steps.

- Document every screen with component inventory, states, and interaction specs
- Reference the approved HTML mockup as the source of truth for states and interactions
- Define acceptance criteria engineering can verify
- List open questions and decisions deferred to implementation

After presenting the handoff spec, offer: *"Want me to run the `pm-design-reviewer` agent one final time against the complete handoff? It checks that every requirement is covered and the spec is specific enough for a developer to build without a sync meeting."*

*After presenting: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the design handoff to the file listed for `/design-handoff`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Checkpoint 6**: Present the complete handoff package. Confirm the design workflow is complete.
