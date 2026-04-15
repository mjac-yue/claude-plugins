---
name: risk
description: Identify, score, and track project risks across all phases — PM, Design, Dev, and execution. Produces or updates a risk register with cross-phase coverage including scope, schedule, technical, resource, design, and project/exec risks. Run at kickoff, at each phase transition, after each workflow step, and in Phase D before rollout.
disable-model-invocation: true
---

Identify and track risks for: $ARGUMENTS

> **Learning note — Risk Management**
> Risk management is the discipline of thinking about what could go wrong before it does — and deciding in advance what you'll do about it. By identifying, scoring, and tracking risks across all phases (PM, design, technical, execution), you can mitigate the serious ones early when the cost is low, rather than managing them as incidents post-launch. The difference between a risk that was flagged and mitigated and one that wasn't is often the difference between a planned response and a crisis.

You are helping a small team maintain a practical cross-phase risk register — not a bureaucratic one. Risks are tracked from the first PM step through to launch. Every risk should either have a mitigation or an explicit acceptance decision.

---

## Step 1: Identify risks by category

Check the project directory for the latest deliverables (brief, PRD, user stories, wireframe spec, design handoff, tech spec, dev plan) and read them before identifying risks. Risks should be grounded in what's actually in those documents.

Systematically consider each category:

**PM risks** (surface during Phase A — PM workflow)
- Scope: requirements not fully defined, assumptions that are high-risk if wrong, unclear success criteria
- Alignment: stakeholder disagreements, unresolved open questions in the PRD
- Market: competitive threats identified in the competitive analysis not accounted for

**Design risks** (surface during Phase A — Design workflow)
- UX: novel interaction patterns with no validation, flows with unresolved edge cases
- Coverage: P0 user stories without a mapped screen, open design questions not yet resolved
- Accessibility: known WCAG gaps from the design review

**Technical risks** (surface during Phase B — Tech Design)
- Architecture: unproven technologies in the stack, third-party API reliability, XL complexity estimates
- Data: schema changes affecting production data, performance unknowns (unbounded queries, missing indexes)
- Security: auth gaps, input validation gaps, known OWASP exposure from the security review
- Integration: external dependencies whose timelines are outside the team's control

**Execution / project risks** (surface at kickoff and during /run)
- Schedule: dependencies that could slip, estimation uncertainty, team capacity constraints
- Resource: team availability, skill gaps, tool access, builder context (solo PM with limited eng bandwidth)
- External: third-party service delays, compliance requirements, legal considerations
- Decision latency: decisions needed from stakeholders that could block a phase transition

For each risk identified, ask: *"If this happened, would it delay the launch date, change scope, affect quality, or require rework of a completed phase?"* If no, it's probably not worth tracking.

---

## Step 2: Score each risk

Use a simple 1–3 × 1–3 matrix:
- **Likelihood**: 1 = Unlikely, 2 = Possible, 3 = Likely (actively occurring or strong indicators present)
- **Impact**: 1 = Minor (small rework, < 1 week delay), 2 = Significant (phase slip, scope change), 3 = Severe (launch blocked, major rework of a completed phase)
- **Score** = Likelihood × Impact (1–9)

Prioritise score 6+ for active mitigation. Score 3–5 for monitoring. Score 1–2 can be logged and checked at the next checkpoint.

---

## Step 3: Define mitigations

For each risk with score 3+:
- **Prevention**: what action reduces the likelihood of this risk occurring?
- **Contingency**: if it occurs anyway, what's the response plan?
- Assign an owner and a review date

Avoid vague mitigations like "monitor closely". Be specific: *"Schedule API integration spike in Cycle 3 before committing to Layer 4 timeline."*

---

## Step 4: Flag unmitigated high risks and ask to proceed

Any risk with score 6+ and no viable mitigation must be explicitly surfaced. Do not silently log it.

For each unmitigated score 6+ risk, present:
> **Risk**: [description]
> **Score**: [L × I = score] — [why this is high]
> **Status**: No mitigation identified
> **Recommended action**: [Descope / Defer / Escalate / Accept with rationale]

Then ask:
> *"Do you want to address [risk name] before proceeding, or accept it and continue? Reply with your decision for each flagged risk."*

Do not proceed to the next workflow step until the user has responded to each flagged risk.

---

## Step 5: Update existing register (if provided)

If a risk register already exists (`[project]-risks.md` or equivalent):
- Update scores for risks where status has changed
- Close risks that have been resolved (note the resolution)
- Add new risks identified since the last review
- Note the trend for the overall register (increasing / stable / decreasing)

---

## Step 6: Phase D — Pre-launch risk clearance

When called at the end of Phase D (before rollout), produce a **launch risk clearance report**:

1. **Review the full risk register** — show every risk that is still Open or Accepted (not Closed)
2. **For each open risk**, confirm:
   - Was it addressed during testing? (automated tests, PM test, design conformance test)
   - If not addressed, is it safe to launch with? What is the post-launch mitigation?
3. **Launch recommendation**:
   - **Clear to launch**: all score 6+ risks are closed or have explicit post-launch mitigations accepted by the team
   - **Hold**: one or more score 6+ risks are unaddressed and no mitigation is in place — list exactly what must be resolved
4. Present the clearance decision and ask for sign-off before rollout begins.

---

## Output format

Produce the risk register as a table, sorted by score descending:

| # | Risk | Category | L | I | Score | Status | Mitigation / Decision | Owner | Review date |
|---|------|----------|---|---|-------|--------|----------------------|-------|------------|
| 1 | [Risk] | PM / Design / Technical / Exec | 1–3 | 1–3 | 1–9 | Open / Mitigated / Accepted / Closed | [Specific action or acceptance rationale] | [Owner] | [Date] |

After the table, produce a one-paragraph **Risk Summary**:
- How many risks total, how many are score 6+, what the trend is
- The single biggest risk to the launch date and what's being done about it
- Whether the team is clear to proceed to the next phase or step

Save the register to `[project]-risks.md` if a project directory exists.
