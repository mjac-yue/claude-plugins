---
name: release-plan
description: Generate a full product release plan from kickoff to launch — phases, milestones, timeline, dependency map, build sequence (foundation-first layering), critical path, parallel workstreams, go/no-go criteria, and launch readiness checklist. Methodology-aware (sprints or flow). Use when starting a new feature or product build and you need to plan the full execution arc across multiple cycles.
disable-model-invocation: true
---

Generate a release plan for: $ARGUMENTS

> **Learning note — Release Plan**
> A release plan is the master schedule that sequences all the work from first commit to launch. It identifies dependencies between workstreams (you can't build the UI before the API it needs), establishes go/no-go criteria, and gives the whole team a shared timeline to coordinate around. Without it, teams frequently discover at the last minute that two critical pieces of work were blocked on each other, or that a third-party dependency wasn't ready. The release plan doesn't prevent surprises — it surfaces them early enough to do something about them.

Display the learning note above verbatim to the user before proceeding.

**Output standard — diagrams**: All documents are read in Obsidian. Use Mermaid syntax (` ```mermaid ` blocks) for all diagrams. Use `flowchart TD` for dependency maps and build sequences, `gantt` for timelines if phase dates are known.

**Output standard — tables**: Always include a blank line before any Markdown table. Obsidian requires this to render `|` syntax as a table rather than plain text.

You are a project manager creating a release plan for a small team. The plan must sequence work foundation-first — infrastructure before foundation, foundation before features — so the team is never blocked by missing dependencies mid-execution.

## Step 0: Determine the project tier

If not already established (e.g., via the `/release` orchestrator), ask two questions before proceeding:

1. *"How many people are contributing to this project?"*
2. *"How would you describe the project size?"*
   - **(A) Micro** — single small change, days to ~2 weeks, clear scope
   - **(B) Small** — 1–3 features, 2–6 weeks, few unknowns
   - **(C) Medium** — multi-feature, 6–16 weeks, some unknowns
   - **(D) Large** — full product, 16+ weeks, significant complexity

Then declare the tier before proceeding:

| Tier | Scope | Plan depth |
|------|-------|-----------|
| **Tier 1 — Micro** | (A) | Ordered task list + brief launch checklist. Use this skill's output informally, not the full template. |
| **Tier 2 — Small** | (B) with 1–2 people | Phases + build sequence only. Skip dependency map, critical path, parallel workstreams, go/no-go table, risk checkpoints. |
| **Tier 3 — Medium** | (C) any size, or (D) small team | Full plan — all sections. |
| **Tier 4 — Large** | (D) with complexity, multiple phases, or stakeholder risk | Full plan — all sections, extra rigour on risks and go/no-go criteria. |

Apply only the steps below that correspond to the confirmed tier. Steps marked **[Tier 3–4 only]** or **[Tier 2+]** can be skipped for smaller projects.

## Step 1: Gather context

If not already clear from the input, ask:
1. *"What are we building?"* — reference the PRD or brief if one exists; if not, ask for a one-line description
2. *"Who is on the team and what are their roles?"*
3. *"Is there a target launch date, or should we estimate one based on scope?"*
4. *"What methodology are you using?"* — Kanban (default for 1–2 people) or Scrum (sprints)

## Step 2: Define phases and milestones

Map the full lifecycle from discovery to launch. For each phase:
- Name the milestone — the specific, observable output that marks the phase complete
- Assign a target date (estimate if none provided, based on scope and capacity)
- Define the gate criteria — the minimum conditions that must be true before the next phase starts

Standard phases for a PM-led build:

**Phase A — PM + Design alignment** *(iterative, no Eng)*
- PM drafts initial PRD → Design explores → Design feedback refines PRD → PRD update refines design → repeat
- This is not a linear handoff — it is a feedback loop. Rounds continue until PM and Designer mutually sign off.
- Gate: PM and Designer both sign off; PRD finalized; all P0 screens covered with acceptance criteria; no open questions.

**Phase B — Tech design + constraint resolution** *(iterative, all three roles)*
- Eng reviews PM + Design outputs → identifies technical constraints → PM updates PRD, Design updates specs → Eng confirms resolution → repeat if needed
- Gate: all three parties sign off; Eng accepts design handoff; tech spec complete (if required by tier).

**Dev phases** *(sequential, Eng-led; PM + Design available for questions)*
1. **Infrastructure** — hosting, database, auth, CI/CD pipeline all live
2. **Foundation** — core data models and base APIs complete and stable
3. **Core build** — all P0 features complete and tested
4. **Feature build** — P1/P2 features complete (can be deferred if needed)
5. **QA & hardening** — test plan complete, no P0/P1 bugs open
6. **Launch** — shipped to production, smoke tests passing, monitoring live

**Tier 2**: Phase A still applies but may be a single round with light design (UX brief + key screens). Phase B may be a single review session rather than multiple rounds. Dev phases: use only Infrastructure → Foundation → Core build → Launch if that's all that applies.

**Tier 3–4**: Model the full iterative nature of Phases A and B. Track rounds explicitly. Do not skip without noting why.

## Step 3: Build the dependency map [Tier 3–4 only]

Identify what must be complete before each phase can start. Express as a chain:
- What must be done before design can start?
- What must be done before dev can start?
- Within dev, what must exist before other components can be built?
- What external dependencies exist (third-party APIs, design assets, stakeholder approvals)?

For each unresolved dependency: name it, note who owns resolving it, and flag the risk if it isn't resolved in time.

**Tier 2**: Instead of a full dependency map, note in plain prose any dependency that is genuinely at risk — e.g., *"Third-party payment API access must be confirmed before Layer 3 can start."* Skip the rest.

## Step 4: Sequence the build — foundation first

Define the build layers explicitly so the team always has a foundation before building on top of it. The full sequence includes pre-dev layers for PM and design work.

**PM Layer — Discovery & requirements**: Problem framing, competitive landscape, PRD draft, user stories, prioritization. PM-led, no Eng or Design resources required. Complete when the initial PRD is ready for Design to start exploring.

**Design Layer — Exploration & alignment** *(iterative with PM)*: UX brief, wireframes, design review, handoff doc. Runs in rounds with PM until mutual sign-off. Complete when PM and Designer both sign off with no open questions.

**Tech Design Layer — Constraint resolution** *(iterative with all three)*: Eng reviews and identifies constraints, PM + Design respond, all three align. Complete when Eng accepts handoff and all constraints are resolved.

**Layer 1 — Infrastructure**: Everything that must exist before writing feature code — hosting, database, auth, CI/CD, environment config, domain setup. *The specific tech stack choices (hosting platform, database, auth system, CI/CD tooling) are not made here — they are determined in Phase B. In the initial release plan, list Layer 1 as a set of TBD categories. Fill in the specifics only after Phase B is complete and the tech stack is confirmed.*

**Layer 2 — Foundation**: Core data models, auth flows, and base APIs that every feature depends on. Nothing in Layer 3 can be built until Layer 2 is stable.

**Layer 3 — Core features (P0)**: Must-have features, built on the foundation. Map directly from PRD P0 requirements.

**Layer 4 — Feature layer (P1/P2)**: Built on top of P0. Can be deferred to v1.1 if timeline is at risk — note this explicitly.

**Layer 5 — Integration & polish**: Third-party service integrations, edge cases, UX refinements, performance optimisation.

**Layer 6 — QA & launch**: Test plan execution, bug fixing, smoke tests, monitoring, communications.

For each layer:
- List the specific work items drawn from the PRD or tech spec — except for Layer 1, which should list TBD categories until Phase B confirms the tech stack
- Define what "layer complete" means as an observable condition (not just "done")
- For PM and Design layers: track iteration rounds separately in the Alignment Rounds and Tech Design Rounds sections

## Step 5: Identify the critical path [Tier 3–4 only]

Identify the sequence of tasks where any single delay pushes the launch date. Mark the current highest-risk item on the critical path and explain why.

**Tier 2**: Skip the formal critical path. Instead, note in one sentence the single item most likely to slip the launch date and why.

## Step 6: Map parallel workstreams [Tier 3–4 only]

For a 2-person team: identify where Person A and Person B can work simultaneously without blocking each other. Look for natural splits such as backend vs frontend, or infrastructure vs discovery/design.

For a solo build: identify where sequential dependencies mean one thing must fully complete before the next starts — and flag these as schedule risks.

**Tier 2**: Skip the parallel workstream table. Only note if there is an obvious split worth calling out.

## Step 7: Define go/no-go criteria [Tier 3–4 only]

For each phase gate, state the minimum observable conditions required to proceed. Be specific:
- Not: "design complete"
- Yes: "all screens in the design handoff have acceptance criteria that the dev has reviewed and accepted"

**Tier 2**: Replace the full criteria table with a single go/no-go statement per phase: *"Start [Phase N] when: [one condition]."*

## Step 8: Set risk checkpoints [Tier 3–4 only]

Identify 4–5 points in the timeline where the team stops, compares progress to plan, and decides whether to adjust scope, timeline, or resources. Place checkpoints at natural inflection points: end of discovery, end of design, mid-build, pre-QA, and launch minus one week.

**Tier 2**: Set one mid-project check-in and a launch-minus-3-days check. That's enough for a small project.

## Step 9: Build the launch readiness checklist

**All tiers** — but scale the length to the project:

- **Tier 1**: 5–8 items (smoke test passes, no open P0 bugs, basic monitoring on)
- **Tier 2**: 8–12 items (add: error tracking, rollback known, key stakeholder notified)
- **Tier 3–4**: Full checklist — product, infrastructure, communications, analytics

Cover only what genuinely applies to this project. Don't include items that are meaningless at the project's scale.

---

**For Tier 2**: Use the release-plan-template.md structure but skip sections marked [Tier 3–4 only] — Dependency Map diagram, Critical Path, Parallel Workstreams table, Go/No-Go Criteria table, and Risk Checkpoints table. Replace each with a one-liner where relevant.

**For Tier 3–4**: Use the full structure from [release-plan-template.md](release-plan-template.md).

Output the complete plan. Do not use placeholder text — fill in every section based on the project context provided. Where specific details aren't known, make a reasonable estimate and flag it with *[TBC]* so the team knows what to confirm.

## Save output

After presenting the release plan to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/release-plan` and save the output to that file path; if no row exists, save to `execution/release-plan.md` in the project directory
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. Confirm the file was written to the user
5. If no project directory exists, present the output for manual copying
