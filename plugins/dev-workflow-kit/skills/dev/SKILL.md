---
name: dev
description: Full Development workflow orchestrator — runs all phases from technical design through QA sign-off, pausing for approval at each checkpoint. Use when translating product requirements into an engineering-ready plan.
disable-model-invocation: true
---

Run the full Development workflow for: $ARGUMENTS

Work through each phase below sequentially. After completing each phase, present the output and ask the user: "Ready to continue to Phase [N+1], or would you like to revise anything?"

---

## Phase 0 — Solo Builder Complexity Check

Before any technical design begins, assess whether the scope is appropriate for the build context.

Ask the user:
> *"Who will be building this — a solo PM-led build with AI assistance, a small team, or a larger engineering team?"*

**If solo PM-led build**: Apply the following constraints throughout all phases:
- Prefer a **monolith** over microservices — one deployable unit is easier to build, debug, and maintain alone
- Prefer **managed services** over self-hosted — avoid database ops, auth servers, or infrastructure management
- Prefer **proven frameworks** with strong conventions over flexible but complex alternatives
- Flag any proposed component with XL complexity — these are high risk without dedicated engineering support
- Flag any approach that requires on-call readiness or significant operational expertise

Surface this check at Checkpoint 1 — if the proposed architecture violates any of these constraints, flag it explicitly and recommend a simpler alternative before proceeding.

**Coding standard — applies to all code produced in this workflow**:

All code generated in Phases 1–8 must be written with learning in mind. The builder is a PM with some coding experience who uses AI assistance and needs to understand what was built, not just run it. Apply these commenting rules to every code file produced:

- **File-level comment**: Every file starts with a 2–4 line comment explaining what this file does and how it fits into the overall system
- **Function/method comments**: Every function gets a comment explaining: what it does, what each parameter means, and what it returns — in plain English, not jargon
- **Logic comments**: Any block of code that isn't immediately obvious gets an inline comment explaining *why* it works that way, not just *what* it does (e.g., "// Sort descending so the most recent item appears first" not "// sort array")
- **Section breaks**: Use comments to divide long functions or files into named sections (e.g., `// --- Validate input ---`, `// --- Query database ---`, `// --- Format response ---`)
- **"Why not" comments**: When a specific approach was chosen over an obvious alternative, note it briefly (e.g., "// Using a Map here instead of an array for O(1) lookup — list can grow large")
- **TODO comments**: Any placeholder or deferred implementation is marked `// TODO: [description]` so nothing is silently incomplete

These comments exist to help the builder understand the codebase as it grows, not just to document for others. Write them as if explaining to a smart non-engineer who will read this code to learn from it.

---

## Phase 1 — Solution Analysis & Technical Specification

Start by offering: *"Would you like me to run the `solution-analyst` agent first? It reads your codebase and researches options before committing to a design — recommended when the right technical approach is not yet clear."*

If the user proceeds with solution analysis, run the `solution-analyst` agent to:
- Read the existing codebase to understand stack, patterns, and constraints
- Research 2–4 distinct technical approaches with real-world evidence
- Produce a structured options comparison and a clear recommendation

Once an approach is agreed, produce an architectural design by running the `/arch-design` skill:
- Define NFRs that every downstream decision must satisfy
- Select and justify the architectural style
- Define component boundaries, integration patterns, and cross-cutting concerns
- Write ADRs for each significant architectural choice

After presenting the architectural design, offer: *"Want me to run the `arch-reviewer` agent to audit the architecture against quality attributes (performance, scalability, availability, security, maintainability, testability, evolvability)?"*

Incorporate the approved architectural design into the technical specification by running the `/tech-spec` skill:
- Carry the chosen option from the solution analysis into the Solution Options section
- Define data models, system components, and key dependencies
- Identify technical risks and constraints upfront

After presenting the architectural design, also offer: *"Want me to run the `ai-opportunity-analyst` agent to identify where AI could add value in this product — including cost estimates and a fit assessment for each opportunity?"* The agent's output populates the AI Opportunities section of the tech spec.

After presenting the tech spec, offer two options:
- *"Want me to run the `tech-spec-reviewer` agent to check for gaps and engineering risks? (Engineering perspective — completeness, performance, reliability)"*
- *"Want me to run the `pm-tech-reviewer` agent for a PM-readable summary of what was decided and why, with complexity and risk translated into product terms?"*

If this is a solo PM-led build, always offer `pm-tech-reviewer` — it is the primary approval review for this context.

**Solo builder complexity check**: Before checkpoint, confirm the proposed architecture satisfies the Phase 0 constraints. If any component is flagged — microservices, self-hosted infrastructure, XL complexity estimates — explicitly note this and present a simpler alternative side-by-side before asking for approval.

**Checkpoint 1**: Get approval before moving to Phase 2.

---

## Phase 2 — API Specification (if applicable)

If the feature involves APIs, produce an API spec by running the `/api-spec` skill.

- Define endpoints, request/response schemas, auth model, and error handling
- Specify versioning strategy and backwards-compatibility constraints
- Note any third-party integrations or webhooks

If no APIs are involved, skip this phase and note that it was skipped.

**Checkpoint 2**: Get approval before moving to Phase 3.

---

## Phase 3 — Development Plan

Produce a development plan by running the `/dev-plan` skill, based on the approved tech spec.

- Break the implementation into tasks with estimates and dependencies
- Propose sprint allocation and sequencing
- Surface any blockers that must be resolved before development can start

**Checkpoint 3**: Get approval before moving to Phase 4.

---

## Phase 4 — QA & Test Plan

Produce a QA test plan by running the `/test-plan` skill.

- Define test types (unit, integration, e2e, manual) and coverage targets
- Generate key test cases covering happy path, edge cases, and error states
- Define acceptance criteria and sign-off conditions

After presenting the test plan, offer: *"Want me to run the `test-case-generator` agent to expand test cases from your user stories?"*

**Checkpoint 4**: Get approval before moving to Phase 5.

---

## Phase 5 — Code Review

Conduct a structured code review by running the `/code-review` skill.

- Review correctness, test coverage, error handling, readability, and pattern consistency
- Flag blocking issues that must be resolved before merge
- Flag non-blocking suggestions and nits separately

After presenting findings, offer: *"Want me to run the `code-reviewer` agent to review actual source files with specific line-level findings?"*

**Checkpoint 5**: Get approval before moving to Phase 6.

---

## Phase 6 — Performance Review

Conduct a performance review by running the `/perf-review` skill.

- Validate against defined latency and throughput targets
- Identify bottlenecks on the critical path (DB queries, external calls, caching gaps)
- Summarize load test results if available and flag any SLO violations

**Checkpoint 6**: Get approval before moving to Phase 7.

---

## Phase 7 — Security Review

Conduct a security review by running the `/security-review` skill, aligned to OWASP Top 10.

- Audit authentication, authorization, input validation, data exposure, and dependency risks
- Assign severity to each finding (Critical / High / Medium / Low)
- Block launch on any Critical finding

After presenting findings, offer: *"Want me to run the `security-reviewer` agent to audit actual source files for specific, line-level vulnerabilities?"*

**Checkpoint 7**: Get approval before moving to Phase 8.

---

## Phase 8 — Deployment

With development complete and all reviews signed off, produce a deployment guide by running the `/deployment` skill.

- Recommend a hosting platform appropriate for the tech stack and build context
- Build the pre-deployment checklist: environment variables, secrets, database provisioning, third-party service setup
- Write step-by-step deploy instructions specific to the chosen platform
- Define a smoke test checklist to verify the deploy is working
- Cover domain and DNS setup if a custom domain is needed
- Define the rollback plan
- Set up minimum viable monitoring: error tracking and uptime alerts

**Checkpoint 8**: Present the complete deployment guide. Confirm the full dev workflow is complete.

---

## Final Deliverable Summary

Output a clean summary:

```
## [Feature Name] — Dev Package

**Status**: Ready to deploy
**Completed**: [Date]

### Documents Produced
- Solution Analysis (if run)
- Architectural Design
- Technical Specification
- API Specification (if applicable)
- Development Plan
- QA Test Plan
- Code Review findings
- Performance Review findings
- Security Review findings
- Deployment Guide

### Open Items Before Launch
1. [Any unresolved findings from reviews]
2. [Any TBDs from the tech spec]
3. [Any smoke test items that need manual verification]
```
