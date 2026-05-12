---
name: premortem
description: Run a structured premortem — assume the project has already failed and work backwards to identify the most likely failure modes. Reads all available project documents, surfaces risks across requirements, design, technical, and execution dimensions, and maps each failure mode to a specific document fix. Use at any phase transition before committing to the next expensive stage of work.
disable-model-invocation: true
---

Run a premortem for: $ARGUMENTS

> **Learning note — Premortem**
> A premortem flips the risk question: instead of asking "what could go wrong?", you declare the project has already failed and ask "what happened?" This bypasses optimism bias — the tendency to underweight risks during active planning — because failure is no longer hypothetical. Teams that run premortems surface significantly more failure modes than standard risk checklists, and the problems they find are more specific and actionable because they're grounded in the actual decisions already made. Run one at any major phase transition, when the cost of changing course is still lower than the cost of proceeding on a flawed assumption.

Display the learning note above verbatim to the user before proceeding.

**Output standard — tables**: All documents are read in Obsidian. Always include a blank line before any Markdown table — Obsidian requires this to render `|` syntax as a table rather than plain text.

Use the template in [premortem-template.md](premortem-template.md) as the structure.

Follow this process:

---

## Step 1: Establish scope

Determine what phase or artifact the premortem is focused on. If `$ARGUMENTS` names a phase or artifact (e.g. "requirements", "design", "tech spec", "launch plan"), focus the failure analysis there. If no argument is given, infer scope from what documents exist:

- Only PM documents present → requirements & product fit premortem
- PM + design documents present → design & UX premortem
- PM + design + tech spec/dev plan present → technical & execution premortem
- Release plan or cycle plan present → launch & delivery premortem

Read all available project documents before proceeding:

| Document | Location | What to extract |
|----------|----------|-----------------|
| Feature brief | `pm/brief.md` | Scope, users, success criteria, key assumptions |
| PRD | `pm/prd.md` | Requirements (P0/P1/P2), goals, open questions |
| User stories | `pm/user-stories.md` | P0 flows and acceptance criteria |
| Wireframe spec | `design/wireframe-spec.md` | Screen inventory, flows, edge cases |
| Design handoff | `design/design-handoff.md` | Component specs, interactions, acceptance criteria |
| Tech spec | `dev/tech-spec.md` | Technical approach, risks, dependencies |
| Dev plan | `dev/dev-plan.md` | Task breakdown, estimates, critical path |
| Release plan | `execution/release-plan.md` | Milestones, go/no-go criteria, timeline |

Summarise which documents were found and confirm the premortem scope before proceeding. If no project documents are found, ask the user to describe what has been decided so far.

---

## Step 2: Write the failure narrative

Imagine it is 9–12 months from now. The project has failed — visibly, specifically, and in a way that is painful for the team. Write a 3–4 sentence narrative that:

- Names the actual product and users from the documents
- Describes what failure looks like from the outside (the feature was pulled / users aren't adopting the core flow / the launch was delayed 5 months and over budget / a critical bug shipped to production)
- Names one or two specific decisions already made in the documents that contributed to the failure
- Makes the scenario vivid enough that the team can actually inhabit it

The failure narrative should feel uncomfortably plausible — not a catastrophe, but the kind of quiet failure that actually happens.

---

## Step 3: Identify failure modes

Working backwards from the failure narrative, identify the most plausible failure modes. For each category below, generate 2–4 specific failure modes grounded in the actual documents — not generic risks. Every failure mode must trace back to a specific decision, gap, or assumption already in the project materials.

**Category 1 — Scope & Requirements**
What the team built didn't solve the problem, or the requirements were too vague to build correctly.
- Look for: vague acceptance criteria, requirements with no measurable success signal, scope that kept expanding, P0 stories with undefined edge cases.

**Category 2 — User & Market Fit**
Users don't value this, or the team misunderstood the problem they were solving.
- Look for: assumptions in the brief that have never been validated, thin user research, personas that don't reflect real behaviour, success criteria tied to output (shipped) rather than outcome (adopted).

**Category 3 — Design & Usability**
The UX failed users — the flow was too complex, the empty states were missing, the mobile experience was an afterthought.
- Look for: screens with no error or loading states, flows that assume the happy path, accessibility gaps, edge cases that are noted but not designed for.

**Category 4 — Technical & Architecture**
The implementation approach failed — performance, reliability, integration failures, or technical debt that blocked iteration.
- Look for: N+1 query risks, external service dependencies with no fallback, missing rate limiting, auth not specified on all endpoints, complexity that was underestimated.

**Category 5 — Planning & Execution**
The timeline collapsed, the team was under-resourced, or the work sequence created blockers.
- Look for: XL estimates with no breakdown, dependencies between tasks not sequenced correctly, no buffer, external dependencies that aren't owned, critical path that's a single thread.

**Category 6 — Assumptions & Unknowns**
The project was built on assumptions that turned out to be wrong, or open questions that were never resolved.
- Look for: key assumptions in the brief or PRD flagged as high-risk, open questions that are still open at this stage, TBD decisions in the tech spec.

For each failure mode, record:
- A one-sentence description of the failure
- Which specific document, decision, or gap enabled it
- The category it belongs to

---

## Step 4: Score and rank

Score each failure mode on two dimensions and calculate a risk score:

| Score | Likelihood | Impact |
|-------|-----------|--------|
| 3 | Very likely — the conditions for this failure already exist in the documents | Fatal or near-fatal — would end the project or require complete rework |
| 2 | Plausible — one or two things would need to go wrong | Significant — would cause a major delay, budget overrun, or user-facing regression |
| 1 | Possible — requires several things to align badly | Manageable — recoverable with extra effort |

Risk score = Likelihood × Impact (range: 1–9).

Present all failure modes ranked from highest to lowest risk score in a table.

---

## Step 5: Map top failure modes to document fixes

For the top 5 failure modes by risk score, specify the concrete fix:

- **Which document** to update (name the file path)
- **What specifically to add, change, or clarify** — not "improve the requirements" but "add a Given/When/Then acceptance criterion to User Story 3 covering the case where the API returns no results"
- **Owner** — PM / Designer / Engineer / All
- **Effort to fix** — S (under an hour) / M (a few hours) / L (requires a meeting or research)

---

## Step 6: Recommend immediate actions

Based on the top failure modes, recommend 2–4 actions to take before proceeding to the next phase. Order by urgency. For each action, state:
- What to do
- Which failure mode it mitigates
- What happens if it's skipped

Then ask:

> *"Which of these failure modes do you want to address now? I can make the document updates directly — just name the ones you want fixed."*

If the user identifies items to fix, apply the changes to the relevant files before saving the premortem output.

---

## Save output

After presenting the premortem:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/premortem` and save the output to that file path
3. If no `/premortem` row exists, save to `pm/premortem.md` in the project directory
4. If `pm/premortem.md` already exists (a previous premortem was run), **append** a new section with today's date and phase as a heading — do not overwrite the previous run
5. Confirm the file was written with a single line
6. If no project `CLAUDE.md` exists, present the output for manual copying
