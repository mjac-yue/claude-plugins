---
name: dev
description: Full Development workflow orchestrator — runs all phases from technical design through QA sign-off, pausing for approval at each checkpoint. Use when translating product requirements into an engineering-ready plan.
disable-model-invocation: true
---

Run the full Development workflow for: $ARGUMENTS

**Output standard — diagrams**: All documents are read in Obsidian. Use Mermaid syntax (` ```mermaid ` blocks) for every diagram — Obsidian renders these natively. Never use ASCII art for diagrams. Relevant types: `flowchart` (system context, component diagrams, data flows), `erDiagram` (data models), `sequenceDiagram` (API request flows), `classDiagram` (code structure), `graph` (dependency graphs).

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
| Phase 1 — Tech Spec | Phase 2 — API Spec (if API-first) or Phase 3 — Dev Plan | `tech-spec-reviewer` agent *(dev-workflow-kit)* — completeness and engineering risks; `pm-tech-reviewer` agent *(dev-workflow-kit)* — PM-readable summary and complexity flags; `arch-reviewer` agent *(dev-workflow-kit)* — quality attribute audit; `ai-opportunity-analyst` agent *(dev-workflow-kit)* — where AI adds value in this product |
| Phase 2 — API Spec | Phase 3 — Dev Plan | No additional agents at this point |
| Phase 3 — Dev Plan | Phase 4 — AI Build *(optional)* or Phase 5 — QA | `builder` agent *(dev-workflow-kit)* — implement the code layer by layer now (invokes Phase 4); `solution-analyst` agent *(dev-workflow-kit)* — if any technical approach is still undecided |
| Phase 4 — AI Build | Phase 5 — QA or Phase 6 — Code Review | `code-reviewer` agent *(dev-workflow-kit)* — immediate review of the files just built |
| Phase 5 — QA Test Plan | Phase 6 — Code Review | `test-case-generator` agent *(dev-workflow-kit)* — expand test cases from user stories |
| Phase 6 — Code Review | Phase 7 — Performance Review (if SLOs defined) or Phase 8 — Security | `code-reviewer` agent *(dev-workflow-kit)* — line-level findings on actual source files |
| Phase 7 — Performance Review | Phase 8 — Security Review | No additional agents at this point |
| Phase 8 — Security Review | Phase 9 — Deployment | `security-reviewer` agent *(dev-workflow-kit)* — OWASP audit of actual source files |
| Phase 9 — Deployment *(final)* | **Launch package: run `/rollout [feature]`** *(pm-claude-kit)* | exec-kit `/run [project]` — start the live delivery and execution cycle |

---

## Phase 0 — Project Profile & Builder Context

Before any technical design begins, establish three things: project tier, build context, and which optional phases to include.

**Step A — Project tier**

If a Project Profile Card was already produced by exec-kit's `/release` skill, accept it and skip this step.

Otherwise ask: *"How would you describe the size of this project — Micro (days–2w), Small (2–6w), Medium (6–16w), or Large (16w+)?"*

Apply phase gating based on the tier:

| Tier | Default phases | Not default — add back if needed |
|------|---------------|----------------------------------|
| **Tier 1 (Micro)** | Ordered task list + 5-item launch checklist. Write code with the commenting standard below. Phase 4 (AI Build) if requested. Phase 9 (abbreviated deploy checklist). | Phases 1, 2, 3, 5, 6, 7, 8 |
| **Tier 2 (Small)** | Phase 3 (abbreviated dev plan), Phase 6 (abbreviated code review checklist), Phase 8 (security check if auth or user data involved), Phase 9 (abbreviated deployment guide). | Phases 1, 2, 4 (AI Build), 5, 7 |
| **Tier 3 (Medium)** | Phases 1 (tech spec; arch design if novel architecture), 3, 5, 6, 8, 9. Phase 7 (perf review) if performance SLOs are defined. | Phase 2 (API spec) unless API-first; Phase 4 (AI Build); Phase 7 if no SLOs |
| **Tier 4 (Large)** | All phases. | — |

**Step B — Builder context**

Ask:
> *"Who will be building this — a solo PM-led build with AI assistance, a small team, or a larger engineering team?"*

**If solo PM-led build**: Apply the following constraints throughout all phases:
- Prefer a **monolith** over microservices — one deployable unit is easier to build, debug, and maintain alone
- Prefer **managed services** over self-hosted — avoid database ops, auth servers, or infrastructure management
- Prefer **proven frameworks** with strong conventions over flexible but complex alternatives
- Flag any proposed component with XL complexity — these are high risk without dedicated engineering support
- Flag any approach that requires on-call readiness or significant operational expertise

Surface this check at Checkpoint 1 — if the proposed architecture violates any of these constraints, flag it explicitly and recommend a simpler alternative before proceeding.

**Step C — Skipped phase opt-in**

After establishing the tier and builder context, present the phases that are not included by default and ask:

*"Before we start — the following phases are skipped by default for your tier. Would you like to add any of them back in?"*

Present only the phases that are skipped for the established tier. Use this description for each:

| Phase | What it adds | When to add it back |
|-------|-------------|---------------------|
| Phase 1 — Solution Analysis & Tech Spec | Formal architecture document, solution options comparison, ADRs | You have 2+ technical approaches to evaluate, or the architecture is novel |
| Phase 2 — API Specification | Full API contract with endpoints, schemas, auth model | Your feature includes API endpoints that other systems will consume |
| Phase 4 — AI Build | Claude writes the code layer by layer following the dev plan | You want Claude to implement the feature, not just plan it |
| Phase 5 — QA & Test Plan | Full test case suite with unit, integration, and e2e coverage | You want structured QA before launch, not just a manual checklist |
| Phase 7 — Performance Review | Validates against latency and throughput SLOs | You have defined performance targets (e.g. p95 < 200ms) |

Accept any number of additions. Update the phase list for this session before proceeding. Confirm: *"Got it — I'll include [X, Y, Z] in addition to the defaults. Here's the updated phase list for this session: [list]."*

**Coding standard — applies to all code produced in this workflow**:

All code generated in Phases 1–9 must be written with learning in mind. The builder is a PM with some coding experience who uses AI assistance and needs to understand what was built, not just run it. Apply these commenting rules to every code file produced:

- **File-level comment**: Every file starts with a 2–4 line comment explaining what this file does and how it fits into the overall system
- **Function/method comments**: Every function gets a comment explaining: what it does, what each parameter means, and what it returns — in plain English, not jargon
- **Logic comments**: Any block of code that isn't immediately obvious gets an inline comment explaining *why* it works that way, not just *what* it does (e.g., "// Sort descending so the most recent item appears first" not "// sort array")
- **Section breaks**: Use comments to divide long functions or files into named sections (e.g., `// --- Validate input ---`, `// --- Query database ---`, `// --- Format response ---`)
- **"Why not" comments**: When a specific approach was chosen over an obvious alternative, note it briefly (e.g., "// Using a Map here instead of an array for O(1) lookup — list can grow large")
- **TODO comments**: Any placeholder or deferred implementation is marked `// TODO: [description]` so nothing is silently incomplete

These comments exist to help the builder understand the codebase as it grows, not just to document for others. Write them as if explaining to a smart non-engineer who will read this code to learn from it.

**Checkpoint 0**: Confirm tier, builder context, and final phase list before proceeding.

---

## Phase 1 — Solution Analysis & Technical Specification — *Tier 3–4 only*

**Tier 1**: Not included by default — write code directly using the build-order task list from Phase 0. Add back if needed.
**Tier 2**: Not included by default. If there is a meaningful architectural decision (e.g., choosing between two approaches), note it in one paragraph with the rationale before moving to Phase 3. No formal tech spec or arch design doc needed by default. Add back if needed.
**Tier 3**: Run tech spec only — skip arch design unless the feature introduces a novel architectural pattern. Abbreviate solution options to two alternatives maximum.

Start by offering: *"Would you like me to run the `solution-analyst` agent first? It reads your codebase and researches options before committing to a design — recommended when the right technical approach is not yet clear."*

If the user proceeds with solution analysis, run the `solution-analyst` agent to:
- Read the existing codebase to understand stack, patterns, and constraints
- Research 2–4 distinct technical approaches with real-world evidence
- Produce a structured options comparison and a clear recommendation

Once an approach is agreed, produce an architectural design following the process and template of the `/arch-design` skill:
- Define NFRs that every downstream decision must satisfy
- Select and justify the architectural style
- Define component boundaries, integration patterns, and cross-cutting concerns
- Write ADRs for each significant architectural choice

After presenting the architectural design, offer: *"Want me to run the `arch-reviewer` agent to audit the architecture against quality attributes (performance, scalability, availability, security, maintainability, testability, evolvability)?"*

Incorporate the approved architectural design into the technical specification following the process and template of the `/tech-spec` skill:
- Carry the chosen option from the solution analysis into the Solution Options section
- Define data models, system components, and key dependencies
- Identify technical risks and constraints upfront

After presenting the architectural design, also offer: *"Want me to run the `ai-opportunity-analyst` agent to identify where AI could add value in this product — including cost estimates and a fit assessment for each opportunity?"* The agent's output populates the AI Opportunities section of the tech spec.

After presenting the tech spec, offer two options:
- *"Want me to run the `tech-spec-reviewer` agent to check for gaps and engineering risks? (Engineering perspective — completeness, performance, reliability)"*
- *"Want me to run the `pm-tech-reviewer` agent for a PM-readable summary of what was decided and why, with complexity and risk translated into product terms?"*

If this is a solo PM-led build, always offer `pm-tech-reviewer` — it is the primary approval review for this context.

**Solo builder complexity check**: Before checkpoint, confirm the proposed architecture satisfies the Phase 0 constraints. If any component is flagged — microservices, self-hosted infrastructure, XL complexity estimates — explicitly note this and present a simpler alternative side-by-side before asking for approval.

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the arch design to the file listed for `/arch-design` and the tech spec to the file listed for `/tech-spec`. Update **Status** to **Done** and **Last updated** to today's date for each. Confirm the files were written.*

**Checkpoint 1**: Get approval before moving to Phase 2.

---

## Phase 2 — API Specification — *Tier 3–4, or Tier 2 if API-first*

**Tier 1**: Not included by default. Add back if needed.
**Tier 2**: Run only if the entire feature is an API (no UI). If the API is incidental to a UI feature, document endpoint signatures inline in the dev plan instead.

If the feature involves APIs, produce an API spec following the process and template of the `/api-spec` skill.

- Define endpoints, request/response schemas, auth model, and error handling
- Specify versioning strategy and backwards-compatibility constraints
- Note any third-party integrations or webhooks

If no APIs are involved, skip this phase and note that it was skipped.

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the API spec to the file listed for `/api-spec`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Checkpoint 2**: Get approval before moving to Phase 3.

---

## Phase 3 — Development Plan — *Tier 2–4*

**Tier 1**: Not included by default — the task list from Phase 0 is sufficient. Add back if needed.
**Tier 2**: Abbreviated — produce an ordered task list with S/M/L sizing and build-layer grouping. No sprint allocation table, no blocker analysis section.
**Tier 3–4**: Full dev plan below.

Produce a development plan following the process and template of the `/dev-plan` skill, based on the approved tech spec.

- Break the implementation into tasks with estimates and dependencies
- Propose sprint allocation and sequencing
- Surface any blockers that must be resolved before development can start

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the dev plan to the file listed for `/dev-plan`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Checkpoint 3**: Get approval before moving to Phase 4.

---

## Phase 4 — AI Build — *Optional, all tiers*

**All tiers**: Not included by default. Add back when you want Claude to implement the feature, not just plan it. Recommended for solo PM-led builds using AI coding assistance.

This phase hands off the approved dev plan to the `builder` agent, which implements the code layer by layer, pauses after each layer for review, and applies the full commenting standard throughout.

Offer: *"Want me to run the `builder` agent to implement this? It will work through the dev plan layer by layer, pause after each layer for your review, and write all code with full comments so you can understand what was built."*

If the user accepts, invoke the `builder` agent with the following context:
- The approved dev plan (location in project directory)
- The feature brief (location in project directory)
- The wireframe spec if it exists (location in project directory)
- The builder context from Phase 0 (solo PM-led, team size, constraints)

The `builder` agent will:
1. Read all context files before writing any code
2. Work through build layers in the order defined in the dev plan
3. Pause after each layer and present a summary of files created/modified
4. Apply the Phase 0 commenting standard to every file
5. Respect all solo builder constraints (monolith, managed services, proven frameworks)
6. Flag any task that is significantly more complex than the dev plan estimated

When the builder agent completes, present the build summary (files created, TODOs remaining, any deviations from the plan) and confirm readiness for Phase 5 (QA) and Phase 6 (Code Review).

**Checkpoint 4**: Confirm build is complete and code is ready for review before moving to Phase 5.

---

## Phase 5 — QA & Test Plan — *Tier 3–4 only*

**Tier 1**: Not included by default. Note the two or three things to manually verify before shipping, inline. Add back if needed.
**Tier 2**: Formal test plan not included by default. Instead, list 4–6 specific things to verify before launch — happy path, the most likely error state, and one edge case. Inline, not a separate document. Add back the full plan if needed.

Produce a QA test plan following the process and template of the `/test-plan` skill.

- Define test types (unit, integration, e2e, manual) and coverage targets
- Generate key test cases covering happy path, edge cases, and error states
- Define acceptance criteria and sign-off conditions

After presenting the test plan, offer: *"Want me to run the `test-case-generator` agent to expand test cases from your user stories?"*

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the test plan to the file listed for `/test-plan`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Checkpoint 5**: Get approval before moving to Phase 6.

---

## Phase 6 — Code Review — *Tier 2–4*

**Tier 1**: Formal review not included by default. Apply the commenting standard from Phase 0 as you write — that's the quality check. Add back if needed.
**Tier 2**: Abbreviated checklist only — correctness, error handling, security (if auth/data), no dead code. One pass, no formal findings document.
**Tier 3–4**: Full code review below.

Conduct a structured code review following the process and template of the `/code-review` skill.

- Review correctness, test coverage, error handling, readability, and pattern consistency
- Flag blocking issues that must be resolved before merge
- Flag non-blocking suggestions and nits separately

After presenting findings, offer: *"Want me to run the `code-reviewer` agent to review actual source files with specific line-level findings?"*

**Checkpoint 6**: Get approval before moving to Phase 7.

---

## Phase 7 — Performance Review — *Tier 3–4, only if performance SLOs are defined*

**Tier 1–2**: Not included by default. Add back if needed.
**Tier 3**: Run only if performance SLOs are explicitly defined in the tech spec (e.g., p95 latency < 200ms). If no SLOs exist: note any obvious performance risks inline (e.g., unbounded queries, missing indexes) and skip the formal review.

Conduct a performance review following the process and template of the `/perf-review` skill.

- Validate against defined latency and throughput targets
- Identify bottlenecks on the critical path (DB queries, external calls, caching gaps)
- Summarize load test results if available and flag any SLO violations

**Checkpoint 7**: Get approval before moving to Phase 8.

---

## Phase 8 — Security Review — *Tier 2–4, conditional on risk*

**Tier 1**: Not included by default unless the change touches authentication, authorisation, or user data — if it does, run the abbreviated Tier 2 check below. Add back for any change involving auth or sensitive data.
**Tier 2**: Abbreviated — check four things only: (1) is user input validated? (2) are auth checks in place? (3) is sensitive data not logged or exposed? (4) are dependencies up to date? Flag any issue, skip the formal findings document.
**Tier 3–4**: Full security review below.

Conduct a security review following the process and template of the `/security-review` skill, aligned to OWASP Top 10.

- Audit authentication, authorization, input validation, data exposure, and dependency risks
- Assign severity to each finding (Critical / High / Medium / Low)
- Block launch on any Critical finding

After presenting findings, offer: *"Want me to run the `security-reviewer` agent to audit actual source files for specific, line-level vulnerabilities?"*

**Checkpoint 8**: Get approval before moving to Phase 9.

---

## Phase 9 — Deployment — *All tiers, depth scales*

**Tier 1**: 5-step deploy checklist only — the specific commands to run, one smoke test, done.
**Tier 2**: Abbreviated deployment guide — platform-specific steps, environment variables to set, smoke test checklist (5–8 items), rollback in one sentence.
**Tier 3–4**: Full deployment guide below.

With development complete and all reviews signed off, produce a deployment guide following the process and template of the `/deployment` skill.

- Recommend a hosting platform appropriate for the tech stack and build context
- Build the pre-deployment checklist: environment variables, secrets, database provisioning, third-party service setup
- Write step-by-step deploy instructions specific to the chosen platform
- Define a smoke test checklist to verify the deploy is working
- Cover domain and DNS setup if a custom domain is needed
- Define the rollback plan
- Set up minimum viable monitoring: error tracking and uptime alerts

*After presenting: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the deployment guide to the file listed for `/deployment`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Checkpoint 9**: Present the complete deployment guide. Confirm the full dev workflow is complete.

---

## Final Deliverable Summary

Output a clean summary scaled to the tier:

```
## [Feature Name] — Dev Package

**Status**: Ready to deploy
**Tier**: [N — Micro / Small / Medium / Large]
**Completed**: [Date]

### Documents Produced
[List only what was actually produced for this tier]

### Code Built
[If Phase 4 AI Build was run: list key files and layers completed. Otherwise: "Not run — build manually using the dev plan."]

### Open Items Before Launch
1. [Any unresolved findings or TBDs]
2.
3.
```
