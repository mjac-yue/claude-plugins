---
name: dev
description: Full Development workflow orchestrator — runs all phases from technical design through deployment, pausing for approval at each checkpoint. Use when translating product requirements into an engineering-ready plan and implementation.
disable-model-invocation: true
---

Run the full Development workflow for: $ARGUMENTS

> **Learning note — Development Workflow**
> The development workflow is a structured sequence from technical design through deployment. Each phase has a specific purpose: the tech spec defines the approach, the dev plan sequences the work, code review validates the implementation, and the deployment guide moves it safely to production. This sequence exists because the most expensive mistakes happen when decisions are made in the wrong order — architecture decisions made during coding instead of before, security reviews done after a vulnerability is already in production. The workflow forces the right conversations at the right times.

Display the learning note above verbatim to the user before proceeding.

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

---

**Review-Iterate-Approve standard — applies at phases marked with a designated reviewer**

At any phase that designates a reviewer below, follow this loop automatically — do not skip it:

1. **Run the reviewer** — invoke the designated agent immediately after presenting the phase deliverable. Do not ask whether to run it; just run it.
2. **Present findings** — summarise critical gaps, high-priority issues, and recommendations from the reviewer's output. Group by severity (Critical / High / Medium / Low).
3. **Ask what to update** — after the findings, always ask: *"What would you like to update based on this review? List the specific items you want changed, or say **'approved'** if you're satisfied and ready to move on."*
4. **Apply updates** — make the changes the user requests to the deliverable.
5. **Re-run the reviewer** — run the same reviewer again on the updated deliverable.
6. **Repeat** from step 2 until the user explicitly says **"approved"**.
7. **Only then** proceed to the next phase checkpoint and save the file.

---

**Phase lookup table — use this to populate the block at each checkpoint:**

| After this phase | Recommended next step | Optional to run |
|-----------------|----------------------|-----------------|
| Phase 1 — Solution Analysis & Tech Spec | Phase 2 — API Spec (if API-first) or Phase 3 — Dev Plan | `tech-spec-reviewer` agent *(dev-workflow-kit)* — completeness and engineering risks; `pm-tech-reviewer` agent *(dev-workflow-kit)* — PM-readable summary and complexity flags; `arch-reviewer` agent *(dev-workflow-kit)* — quality attribute audit |
| Phase 2 — API Spec | Phase 3 — Dev Plan | No additional agents at this point |
| Phase 3 — Dev Plan | Phase 4 — AI Build *(optional)* or Phase 5 — QA | `builder` agent *(dev-workflow-kit)* — implement the code layer by layer now (invokes Phase 4); `/premortem` skill *(exec-kit)* — assume the build has already failed and surface technical and execution risks before the first line of code is written |
| Phase 4 — AI Build | Phase 5 — QA or Phase 6 — Code Review | `code-reviewer` agent *(dev-workflow-kit)* — immediate review of the files just built |
| Phase 5 — QA Test Plan | Phase 6 — Code Review | `test-case-generator` agent *(dev-workflow-kit)* — expand test cases from user stories |
| Phase 6 — Code Review | Phase 7 — Performance Review (if SLOs defined) or Phase 8 — Security | `code-reviewer` agent *(dev-workflow-kit)* — line-level findings on actual source files |
| Phase 7 — Performance Review | Phase 8 — Security Review | No additional agents at this point |
| Phase 8 — Security Review | Phase 9 — Deployment | `security-reviewer` agent *(dev-workflow-kit)* — OWASP audit of actual source files |
| Phase 9 — Deployment *(final)* | **Phase D testing: run `/run [project]`** *(exec-kit)* | exec-kit `/status` — stakeholder status report before launch |

---

## Phase 0 — Prerequisites & Builder Context

### Prerequisites check

Before any build begins, confirm the local environment matches what the tech stack requires.

**Read the tech spec first.** Check `dev/tech-spec.md` (or equivalent) for the decided stack — language, runtime, framework, hosting platform, and any CLI tools. If a Local Development Setup section exists in the tech spec, use that as the source of truth for what to check.

**If no tech spec exists yet** (running `/dev` before Phase 1 is complete): skip the prerequisites check and note — *"Prerequisites will be confirmed once the tech spec is complete and the stack is decided."*

**If the tech spec exists**, derive the checklist from it:
- Identify every runtime, CLI tool, and account the stack requires
- Ask the user to run the relevant check commands and confirm each one
- For anything missing, provide the install command specific to the decided stack
- Once all checks pass, confirm the verified versions and note that they should be recorded in the tech spec's Local Development Setup section

Common patterns by stack (use only what applies):

| If the stack includes… | Check | Minimum |
|------------------------|-------|---------|
| Node.js / React / Vite / Next.js | `node --version` | 18.x+ |
| Python backend or serverless | `python3 --version` | 3.11+ |
| Git (all projects) | `git --version` | Any recent |
| Vercel deployment | `vercel --version` | Latest |
| Docker | `docker --version` | 20.x+ |
| Ruby on Rails | `ruby --version` | 3.x+ |
| Go | `go version` | 1.21+ |

Do not present tools that aren't part of the decided stack. A React + Vercel project does not need a Docker check. A Python Flask project does not need a Node.js check.

### Builder context

Ask:
> *"Who will be building this — a solo PM-led build with AI assistance, a small team, or a larger engineering team?"*

**If solo PM-led build**: Apply the following constraints throughout all phases:
- Prefer a **monolith** over microservices — one deployable unit is easier to build, debug, and maintain alone
- Prefer **managed services** over self-hosted — avoid database ops, auth servers, or infrastructure management
- Prefer **proven frameworks** with strong conventions over flexible but complex alternatives
- Flag any proposed component with XL complexity — these are high risk without dedicated engineering support
- Flag any approach that requires on-call readiness or significant operational expertise

Surface this check at Checkpoint 1 — if the proposed architecture violates any of these constraints, flag it explicitly and recommend a simpler alternative before proceeding.

**Coding standard — applies to all code produced in this workflow**:

All code generated in Phases 1–9 must be written with learning in mind. The builder is a PM with some coding experience who uses AI assistance and needs to understand what was built, not just run it. Apply these commenting rules to every code file produced:

- **File-level comment**: Every file starts with a 2–4 line comment explaining what this file does and how it fits into the overall system
- **Function/method comments**: Every function gets a comment explaining: what it does, what each parameter means, and what it returns — in plain English, not jargon
- **Logic comments**: Any block of code that isn't immediately obvious gets an inline comment explaining *why* it works that way, not just *what* it does
- **Section breaks**: Use comments to divide long functions or files into named sections (e.g., `// --- Validate input ---`, `// --- Query database ---`)
- **"Why not" comments**: When a specific approach was chosen over an obvious alternative, note it briefly
- **TODO comments**: Any placeholder or deferred implementation is marked `// TODO: [description]` so nothing is silently incomplete

**Checkpoint 0**: Confirm builder context before proceeding.

---

## Phase 1 — Solution Analysis & Technical Specification

### Step 1a: Read design outputs

Before any technical analysis, check for completed design deliverables in the project directory. These are required inputs for the solution analysis and tech spec:

- **Design handoff** (`design/design-handoff.md`) — screen inventory, components, states, interactions, acceptance criteria. This defines exactly what must be built.
- **Wireframe spec** (`design/wireframe-spec.md`) — user flows, screen structure, edge cases. Use this to understand scope and interaction complexity.
- **UX brief** (`design/ux-brief.md`) — design constraints that may affect technical choices (platform, accessibility, performance).

If the design handoff does not exist, ask: *"Has the design workflow been completed? The tech spec should reference the approved design so technical choices account for what's being built."*

### Step 1b: Tech stack determination

The tech stack must be established before the tech spec is written. Check if it was already decided in Phase B of `/run` (look for it in the state file or `dev/tech-spec.md`).

If the tech stack has not been decided, determine it now:
- **Hosting platform** — Vercel, Netlify, AWS, Railway, Fly.io, etc. with rationale
- **Database** — Postgres, SQLite, Supabase, PlanetScale, etc.
- **Auth system** — Clerk, Auth0, NextAuth, Supabase Auth, etc.
- **Frontend framework** — Next.js, React + Vite, SvelteKit, etc.
- **Backend approach** — API routes (monolith), separate backend, serverless functions
- **CI/CD tooling** — GitHub Actions, Vercel auto-deploy, etc.
- **Key third-party services** — any external APIs, payments, email, etc.

For a solo PM-led build, prefer managed services and proven frameworks. Recommend the simplest stack that handles the design requirements.

Document the tech stack in the tech spec and confirm with the user before proceeding.

### Step 1c: Solution analysis

Offer: *"Would you like me to run the `solution-analyst` agent first? It reads your codebase and researches options before committing to a technical design — recommended when the right approach is not yet clear."*

If the user proceeds with solution analysis, run the `solution-analyst` agent with:
- The design handoff and wireframe spec as context for what must be built
- The existing codebase to understand stack and patterns
- The decided tech stack as a constraint

Research 2–4 distinct technical approaches with real-world evidence. Produce a structured options comparison and a clear recommendation.

### Step 1d: Architecture design

Once an approach is agreed, produce an architectural design following the process and template of the `/arch-design` skill:
- Define NFRs that every downstream decision must satisfy
- Select and justify the architectural style (referencing the decided tech stack)
- Define component boundaries, integration patterns, and cross-cutting concerns
- Write ADRs for each significant architectural choice

After presenting the architectural design, offer: *"Want me to run the `arch-reviewer` agent to audit the architecture against quality attributes (performance, scalability, availability, security, maintainability, testability, evolvability)?"*

### Step 1e: Technical specification

Incorporate the approved architectural design and tech stack into the technical specification following the process and template of the `/tech-spec` skill:
- Carry the chosen option from the solution analysis into the Solution Options section
- Include the decided tech stack prominently (hosting, database, auth, framework, CI/CD)
- Reference the design handoff for data model requirements and API surface
- Define data models, system components, and key dependencies
- Identify technical risks and constraints upfront

After presenting the tech spec, immediately run the **Review-Iterate-Approve loop** *(designated reviewer: `tech-spec-reviewer`)*:

1. Run the `tech-spec-reviewer` agent on the tech spec just produced — checks for completeness, engineering risks, missing components, and underspecified logic.
2. Present its findings (critical gaps, high-risk areas, underspecified sections), grouped by severity.
3. Ask: *"What would you like to update based on this review? List specific sections or decisions to revise, or say **'approved'** to move on."*
4. Apply updates, re-run `tech-spec-reviewer`, repeat until the user says **"approved"**.

After the loop, separately offer:
- *"Want me to run the `pm-tech-reviewer` agent for a PM-readable summary of what was decided and why?"* (Always offer for solo PM-led builds — it is the primary comprehension check for this context.)
- *"Want me to run the `ai-opportunity-analyst` agent to identify where AI could add value in this product?"*

**Solo builder complexity check**: Before checkpoint, confirm the proposed architecture satisfies the Phase 0 constraints. If any component is flagged — microservices, self-hosted infrastructure, XL complexity estimates — explicitly note this and present a simpler alternative side-by-side before asking for approval.

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the arch design to the file listed for `/arch-design` and the tech spec to the file listed for `/tech-spec`. Update **Status** to **Done** and **Last updated** to today's date for each. Confirm the files were written.*

**Checkpoint 1**: Get approval before moving to Phase 2.

---

## Phase 2 — API Specification

*Run if the feature involves APIs consumed by other systems. If no APIs are involved, skip this phase and note that it was skipped.*

If the feature involves APIs, produce an API spec following the process and template of the `/api-spec` skill.

- Define endpoints, request/response schemas, auth model, and error handling
- Specify versioning strategy and backwards-compatibility constraints
- Note any third-party integrations or webhooks

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the API spec to the file listed for `/api-spec`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Checkpoint 2**: Get approval before moving to Phase 3.

---

## Phase 3 — Development Plan

Produce a development plan following the process and template of the `/dev-plan` skill. This phase requires all three of the following to be complete before starting:
- ✅ Tech spec approved (Phase 1) — defines what to build and the architecture
- ✅ Arch design approved (Phase 1) — defines component boundaries and sequencing constraints
- ✅ API spec approved or skipped (Phase 2) — defines the API surface tasks must implement

If any of these are incomplete, do not start the dev plan — return to the relevant phase first.

- Break the implementation into tasks with estimates and dependencies (reference the arch design for component sequencing)
- Reference the design handoff for acceptance criteria per task — each build task should map to one or more screens or interactions in the design
- Propose sprint allocation and sequencing
- Surface any blockers that must be resolved before development can start

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the dev plan to the file listed for `/dev-plan`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Checkpoint 3**: Get approval before moving to Phase 4.

---

## Phase 4 — AI Build

*This phase is optional. Offer it — do not run it automatically.*

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

## Phase 5 — QA & Test Plan

Produce a QA test plan following the process and template of the `/test-plan` skill.

- Define test types (unit, integration, e2e, manual) and coverage targets
- Generate key test cases covering happy path, edge cases, and error states
- Define acceptance criteria and sign-off conditions

After presenting the test plan, offer: *"Want me to run the `test-case-generator` agent to expand test cases from your user stories?"*

*After user approves: Check for a project `CLAUDE.md` in the current or parent directory. If it contains an **Output paths** table, save the test plan to the file listed for `/test-plan`. Update **Status** to **Done** and **Last updated** to today's date. Confirm the file was written.*

**Checkpoint 5**: Get approval before moving to Phase 6.

---

## Phase 6 — Code Review

Conduct a structured code review following the process and template of the `/code-review` skill.

- Review correctness, test coverage, error handling, readability, and pattern consistency
- Flag blocking issues that must be resolved before merge
- Flag non-blocking suggestions and nits separately

After presenting findings, immediately run the **Review-Iterate-Approve loop** *(designated reviewer: `code-reviewer`)*:

1. Run the `code-reviewer` agent on the actual source files — line-level findings on correctness, test coverage, error handling, security, and pattern consistency.
2. Present its findings, distinguishing **blocking issues** (must fix before merge) from **non-blocking suggestions**.
3. Ask: *"What would you like to update based on this review? List specific files or issues to address, or say **'approved'** if all blockers are resolved."*
4. Apply updates, re-run `code-reviewer`, repeat until the user says **"approved"**.

**Checkpoint 6**: Get approval before moving to Phase 7.

---

## Phase 7 — Performance Review

*Run if performance SLOs are explicitly defined in the tech spec (e.g., p95 latency < 200ms). If no SLOs exist: note any obvious performance risks inline (e.g., unbounded queries, missing indexes) and skip the formal review.*

Conduct a performance review following the process and template of the `/perf-review` skill.

- Validate against defined latency and throughput targets
- Identify bottlenecks on the critical path (DB queries, external calls, caching gaps)
- Summarize load test results if available and flag any SLO violations

**Checkpoint 7**: Get approval before moving to Phase 8.

---

## Phase 8 — Security Review

Conduct a security review following the process and template of the `/security-review` skill, aligned to OWASP Top 10.

- Audit authentication, authorization, input validation, data exposure, and dependency risks
- Assign severity to each finding (Critical / High / Medium / Low)
- Block launch on any Critical finding

After presenting findings, immediately run the **Review-Iterate-Approve loop** *(designated reviewer: `security-reviewer`)*:

1. Run the `security-reviewer` agent on actual source files — OWASP Top 10 audit with specific, line-level vulnerability findings.
2. Present its findings with severity (Critical / High / Medium / Low). Note: **Critical findings block launch** — they must be resolved before the loop can end.
3. Ask: *"What would you like to update based on this review? List specific vulnerabilities or files to fix, or say **'approved'** once all Critical and High findings are resolved."*
4. Apply fixes, re-run `security-reviewer`, repeat until the user says **"approved"**. Do not accept approval while any Critical finding remains open.

**Checkpoint 8**: Get approval before moving to Phase 9.

---

## Phase 9 — Deployment

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

Output a clean summary package:

```
## [Feature Name] — Dev Package

**Status**: Ready to deploy
**Completed**: [Date]

### Documents Produced
- Architecture Design
- Technical Specification
- API Specification (if run)
- Development Plan
- QA Test Plan
- Code Review Findings
- Performance Review (if run)
- Security Review
- Deployment Guide

### Code Built
[If Phase 4 AI Build was run: list key files and layers completed. Otherwise: "Not run — build manually using the dev plan."]

### Open Items Before Phase D Testing
1. [Any unresolved findings from code review, perf review, or security review]
2. [Any TODO comments in code that must be addressed before testing]
3. [Any design acceptance criteria not yet implemented]

### Next Step
Run `/run [project]` to begin Phase D — automated tests, PM requirements test, design conformance test, bug triage, risk clearance, and rollout.
```

After presenting the summary, prompt the user: *"Run `/dev-workflow-kit:log [one-line summary]` to record this in the work log — e.g. `/dev-workflow-kit:log Completed full dev workflow for [feature name]`"*

## Save output

After presenting the final deliverable summary:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, confirm each dev artifact (arch-design, tech-spec, api-spec, dev-plan, test-plan, deployment) has been saved to its listed file path during the relevant phase checkpoint — each is saved inline at approval, so this is a confirmation step
3. Update the **Status** field to **Done** and **Last updated** to today's date for any dev artifact not yet updated
4. Confirm to the user which files are written and current
5. If no project `CLAUDE.md` exists, note that outputs were presented inline and should be saved manually
