---
name: test-run
description: Run a full project lifecycle walkthrough for a test product — generates every document the plugin suite produces (PM, Design, Tech Design, Execution) using realistic, initiative-specific content. Pauses after each phase for review before proceeding. Creates a self-contained project folder under ~/Documents/Projects/test-runs/. Does not produce code.
disable-model-invocation: true
---

You are running a full project lifecycle walkthrough for: **$ARGUMENTS**

Your job is to generate every document the plugin suite produces — across PM Discovery, Design, Tech Design, and Execution — using realistic, initiative-specific content. This is a controlled test: no code is produced, all outputs are written to disk, and a review pause occurs after each phase.

**Output standard**: Write all documents to disk before pausing. Do not print full document content to the terminal. At each phase pause, present a **Review before continuing** block listing every file written, then wait for the user to type `continue`.

---

## Setup — Create the project

**Step 1**: Derive a kebab-case slug from the product name in `$ARGUMENTS`. Example: "Mobile Expense Tracker" → `mobile-expense-tracker`.

**Step 2**: Create this directory structure. Default location is `~/Documents/Projects/test-runs/[slug]/`; if that path is not accessible (e.g., different OS or home directory), use the current working directory instead:

```
test-runs/[slug]/
├── CLAUDE.md
├── pm/
│   ├── brief.md
│   ├── competitive-analysis.md
│   ├── prd.md
│   ├── user-stories.md
│   └── prioritization.md
├── design/
│   ├── ux-brief.md
│   ├── wireframe-spec.md
│   └── design-handoff.md
├── dev/
│   ├── arch-design.md
│   ├── tech-spec.md
│   └── api-spec.md
└── execution/
    ├── release-plan.md
    ├── cycle-01.md
    ├── dev-plan.md
    └── retro-01.md
```

**Step 3**: Write `CLAUDE.md` to the project root with the project name, one-sentence description, and an output paths table mapping each file to its skill (matching the structure above). Mark all artifacts as "Not started" — the test run will update them as files are written.

**Step 4**: Confirm setup is complete, then announce Phase 1 is starting.

---

## Content rules — apply throughout all phases

- Generate realistic, specific content based on the product description — treat this as a real product with real users, real constraints, and real decisions. Generic placeholder text defeats the purpose of a test run.
- Every `💡 Tip` placeholder in the templates should be filled with a specific, initiative-relevant insight — not left as a placeholder.
- No code files. Only markdown documents.
- Use today's date for all dates. Set sprint and cycle dates relative to today. Set the target launch 12–14 weeks from today.
- File sizes: PM documents should be substantive (PRD: 400–600 words of content). Design and dev documents can be more concise but must be complete — no half-filled tables.

---

## Phase 1 — PM Discovery

Generate these 5 documents in `pm/`. Write each file to disk as it is completed.

### pm/brief.md
Product brief structured as:
- **What** — one paragraph describing what is being built and the core feature set
- **Why** — one paragraph on the problem being solved, who it affects, and why now
- **Who** — primary user (one sentence), secondary user if applicable
- **Success criteria** — 3–5 measurable outcomes that define whether v1 succeeded
- **Scope** — ✅ In scope / ❌ Out of scope for v1

### pm/competitive-analysis.md
Analysis of 3–4 realistic competitors in this space. For each competitor:
- One-paragraph overview and market position
- Key features table (5–6 features, ✓ / ✗ / partial)
- Pricing model
- Strengths (2–3 bullets) and weaknesses (2–3 bullets)

Close with: a comparison matrix across all competitors, and a "Where to win" synthesis identifying the specific gap this product can own.

### pm/prd.md
Full PRD using the prd-template structure:
- TL;DR (2–3 sentences)
- Problem statement (one paragraph with evidence of the problem)
- Goals (3–4 specific goals tied to the problem)
- User personas (2 personas — name, role, context, goals, pain points)
- Requirements: at least 4 P0, 3 P1, 2 P2 — each P0 with acceptance criteria
- Success metrics (3–4 measurable metrics tied to the goals)
- Scope boundaries (in scope / out of scope / explicitly deferred)
- Open questions (2–3 real open questions for this product)

### pm/user-stories.md
6–8 user stories covering the P0 flows. Each story:
- Title and persona
- Story: "As a [persona], I want to [action] so that [benefit]"
- Priority: P0 / P1 / P2
- Acceptance criteria: Given / When / Then (2–4 criteria per story)

### pm/prioritization.md
RICE scoring for the top 6–8 features from the PRD. Include:
- A scoring table: Feature, Reach (0–10), Impact (0–3), Confidence (%), Effort (weeks), RICE Score
- Scores should reflect realistic trade-offs — not all features score equally
- A recommendation section: top 3 to build first, with one sentence of rationale for each

After writing all 5 files, output:

> **Review before continuing — Phase 1: PM Discovery**
> - `pm/brief.md` — [one-line product summary]
> - `pm/competitive-analysis.md` — [N competitors, key gap: X]
> - `pm/prd.md` — [N P0 / N P1 / N P2 requirements, N personas]
> - `pm/user-stories.md` — [N stories across N P0 flows]
> - `pm/prioritization.md` — [top 3 features: X, Y, Z]
>
> Open the `pm/` folder to review. **Type `continue` to proceed to Phase 2 — Design.**

---

## Phase 2 — Design

Wait for user to type `continue`. Then generate these 3 documents in `design/`. Write each file to disk as it is completed.

*Note: The full /design orchestrator produces 6 deliverables. This test run generates the 3 primary handoff documents (UX brief, wireframe spec, design handoff). The brainstorm exploration, design review, and usability test plan are omitted for brevity — they would be generated by the /brainstorm, /design-review, and /usability-test skills in a real project.*

### design/ux-brief.md
UX brief using the ux-brief-template structure:
- Target users: 2 user profiles with role, context, primary goal, and the key pain point the design must resolve
- Key user journeys: 3–4 primary flows described as goal → steps → success state
- Design constraints: technical constraints (platform, performance), accessibility requirements, and business constraints
- What success looks like for the design (2–3 observable outcomes)
- Open questions: 3–4 real design questions that need resolution before wireframing can be finalised

### design/wireframe-spec.md
Text-based wireframe spec for the 3–4 P0 flows. For each screen:
- **Screen name and purpose** (one sentence)
- **Layout** — describe the visual hierarchy: header zone, main content zone, action zone. Use structured text, not images.
- **Components** — bulleted list of all visible elements: labels, buttons, input fields, navigation, data displays. Include placeholder dimensions or relative sizes where relevant.
- **States** — at minimum: default, loading, empty, error, success
- **Interactions** — what happens on each primary action (tap, click, submit)
- **Edge cases** — at least one per screen

### design/design-handoff.md
Design handoff document:
- Screen inventory table: screen name, purpose, states covered, route/URL
- Component specifications: list reused components (minimum 3), their properties, and variants
- Accessibility requirements: WCAG 2.1 AA conformance notes per screen
- Interaction specifications: key transitions and loading feedback patterns
- Acceptance criteria: per-screen pass/fail criteria for the engineer to verify against

After writing all 3 files, output:

> **Review before continuing — Phase 2: Design**
> - `design/ux-brief.md` — [N user journeys, N open design questions]
> - `design/wireframe-spec.md` — [N screens, N P0 flows]
> - `design/design-handoff.md` — [N screens in inventory, N components specified]
>
> Open the `design/` folder to review. **Type `continue` to proceed to Phase 3 — Tech Design.**

---

## Phase 3 — Tech Design

Wait for user to type `continue`. Then generate these 3 documents in `dev/`. Write each file to disk as it is completed.

### dev/arch-design.md
Architectural design using the arch-design-template structure:
- NFRs table: performance (p95 latency target), availability (uptime target), scalability (load target), security (data classification) — all with specific numbers, not ranges
- Chosen architectural style with one-paragraph rationale referencing the NFRs; include a "styles considered and rejected" table (2 alternatives)
- System context diagram in Mermaid: external users, this system, and downstream services
- Component design: 3–4 components with single-responsibility descriptions, what each owns, and what each does NOT own
- Integration patterns table: how components communicate, consistency model, and failure handling
- Cross-cutting concerns: auth enforcement point, error propagation strategy, caching approach, logging and observability
- Architectural risks table: 3–4 risks across the standard categories (SPOF, bottleneck, coupling, lock-in) with mitigations
- 2–3 ADRs for the significant decisions made (storage choice, auth model, communication pattern)

### dev/tech-spec.md
Technical specification using the tech-spec-template structure:
- Overview paragraph (what is being built, the product goal, approach chosen)
- Requirements summary table (top 5 P0 requirements restated in engineering terms)
- Solution options: 2–3 distinct approaches with evaluation matrices and actual monthly cost estimates (dollar amounts, not Low/Medium/High); include a Decision section with rationale and options ruled out
- Data model: 2–3 core entities with field tables and relationships
- Key business logic: 1–2 non-trivial rules or calculations with edge cases
- APIs index: top 5 endpoints (method, path, purpose, owner)
- Dependencies: internal and external, with a cost summary table (component, pricing model, launch cost, 10× scale cost)
- Technical risks: 4 risks across performance, security, data consistency, third-party reliability
- Complexity estimate: per-component sizing with total estimate and confidence level

### dev/api-spec.md
API specification using the api-spec-template structure:
- Overview: purpose, base URL, protocol, data format
- Authentication: method, how to obtain credentials, how to include in requests, token expiry
- Rate limiting table
- 4–5 endpoint blocks — each with:
  - Request: path params, query params (if any), request body with JSON example and field table
  - Response: success JSON example with field table
  - Errors: status codes, error codes, and when each occurs
- Shared schemas (1–2 reused data structures)
- Error response envelope
- Versioning policy

After writing all 3 files, output:

> **Review before continuing — Phase 3: Tech Design**
> - `dev/arch-design.md` — [architectural style chosen, N ADRs recorded]
> - `dev/tech-spec.md` — [chosen approach, est. $X/month at launch, N technical risks]
> - `dev/api-spec.md` — [N endpoints, auth method, N shared schemas]
>
> Open the `dev/` folder to review. **Type `continue` to proceed to Phase 4 — Execution Planning.**

---

## Phase 4 — Execution Planning

Wait for user to type `continue`. Then generate these 2 documents in `execution/`. Write each file to disk as it is completed.

### execution/release-plan.md
Release plan using the release-plan-template structure:
- Project overview: what is being built, why now, success definition
- Phases & milestones table: all phases (A PM+Design, B Tech Design, Layers 1–6) with specific target dates spaced 2–3 weeks apart from today, owners, statuses, and gate criteria
- Build sequence: populate all 6 layer checklists with product-specific items. Layer 1 (Infrastructure) and Layer 2 (Foundation) should have fully specific checklist items based on the tech stack chosen in Phase 3. Layers 3–6 can use the P0/P1 requirements from the PRD.
- Dependency map: the Mermaid flowchart (copy the template diagram — it applies universally)
- Go/no-go criteria table: all 8 phase gates with must-be-true conditions specific to this product
- Risk checkpoints table
- Launch readiness checklist: all sections populated with product-specific items
- Target launch date: 12–14 weeks from today

### execution/cycle-01.md
Cycle 1 plan using the cycle-plan-template structure. Cycle 1 covers Layer 1 — Infrastructure:
- Capacity table: 1–2 person team, 2-week cycle, with 20% buffer applied
- Layer check: prerequisites for Layer 1 (all pre-Layer-1 tasks — none should be blocked at this point)
- Selected work table: 4–6 infrastructure tasks specific to the tech stack chosen in Phase 3 (hosting setup, database provisioning, auth configuration, CI/CD pipeline, environment variables, error tracking)
- Dependency check table
- Deferred items: any Layer 1 items deferred to Cycle 2 with reasons
- Risks this cycle: 2–3 realistic risks for an infrastructure cycle
- Definition of done: all 5 standard items checked

After writing both files, output:

> **Review before continuing — Phase 4: Execution Planning**
> - `execution/release-plan.md` — [target launch: DATE, N phases mapped, N layer items]
> - `execution/cycle-01.md` — [N work items, Layer 1 Infrastructure, N-person team]
>
> Open the `execution/` folder to review. **Type `continue` to proceed to Phase 5 — First Development Cycle.**

---

## Phase 5 — First Development Cycle

Wait for user to type `continue`. Then generate these 2 documents in `execution/`. Write each file to disk as it is completed.

### execution/dev-plan.md
Development plan for Cycle 1 using the dev-plan-template structure:
- Goal & constraints: Cycle 1 goal (infrastructure live), timeline (2 weeks), team, dependencies
- Task breakdown: 6–8 tasks for the Layer 1 infrastructure work. Use realistic discipline (Infra/BE), day estimates, and dependencies. At least 2 tasks should depend on prior tasks to make the critical path non-trivial.
- Critical path: draw the dependency chain using the `Task 1 (Nd) → Task 2 (Nd) → ...` format with a total day count
- Blockers section: 1–2 realistic pre-start blockers (e.g., platform account access, API credentials)
- Sprint allocation: 2-week sprint at 70% capacity with tasks distributed across days
- Milestones: 3 checkpoints (infrastructure accessible, CI/CD live, smoke test passing)
- Risks: 3 risks with likelihoods, impacts, and mitigations
- Definition of done: all 8 standard items, tailored to infrastructure work

### execution/retro-01.md
End-of-Cycle-1 retrospective using the retro-template structure. Simulate a realistic outcome: 4 of 6 planned items completed, 2 carried over:
- Cycle summary: goal, outcome (Partially achieved), items completed (4 of 6)
- What worked: 2–3 specific practices that helped (e.g., "starting with environment config before CI/CD prevented a dependency block")
- What didn't work: 2 specific friction points with enough detail to be actionable (e.g., "database provisioning took 2 days longer than estimated because the free tier had connection limits we didn't discover until integration")
- Carried-over items table: 2 items with specific reasons (underestimated / dependency not ready) and actions (carry to Cycle 2 / descope)
- Action items: 1 action per person (or 2 for solo) with specific, completable actions and due dates
- One process change: specific change, the problem it solves, and how the team will know it worked
- Release plan check: on track / at risk with one-sentence explanation

After writing both files, output:

> **Review before continuing — Phase 5: First Development Cycle**
> - `execution/dev-plan.md` — [N tasks, critical path: X days, N milestones]
> - `execution/retro-01.md` — [4 of 6 items completed, key process change: X]

Then output the test run complete summary:

---

> ## Test run complete — [Product Name]
>
> All documents written to `~/Documents/Projects/test-runs/[slug]/`
>
> | Phase | Documents generated |
> |-------|---------------------|
> | 1 — PM Discovery | brief, competitive analysis, PRD, user stories, prioritization |
> | 2 — Design | UX brief, wireframe spec, design handoff |
> | 3 — Tech Design | arch design, tech spec, API spec |
> | 4 — Execution Planning | release plan, cycle 1 plan |
> | 5 — First Dev Cycle | dev plan, retro |
>
> **What to check**: Open a document from each phase and verify the content is realistic and initiative-specific — not generic. The `💡 Tip` sections should contain product-relevant insights, not placeholder text. The PRD requirements, tech stack decisions, and release plan dates should all be internally consistent across phases.
>
> To run another test product: `/test-run [new product description]`
