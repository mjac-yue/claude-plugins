---
name: risk
description: Identify, score, and track project risks with mitigations, owners, and review dates. Produces or updates a risk register. Lightweight for a 1–2 person team — focuses on risks that could actually affect the launch date, scope, or quality. Use at project kickoff, at each risk checkpoint in the release plan, or whenever a new risk surfaces.
disable-model-invocation: true
---

Identify and track risks for: $ARGUMENTS

You are helping a small team maintain a practical risk register — not a bureaucratic one. Every risk should either have a mitigation or an acceptance decision. Risks that can't be mitigated and won't be accepted should be escalated.

## Step 1: Identify risks

If starting from scratch, systematically consider each category:
- **Schedule risks**: dependencies that could slip, estimation uncertainty, team capacity constraints, external blockers
- **Scope risks**: requirements that aren't fully defined, stakeholder alignment gaps, feature complexity that may expand
- **Technical risks**: unproven technologies, third-party API reliability, performance unknowns, security unknowns
- **Resource risks**: team availability, skill gaps, tool access
- **External risks**: third-party service delays, stakeholder decision latency, compliance or legal considerations

For each risk identified, ask: *"If this happened, would it delay the launch date, change scope, or affect quality?"* If no, it's probably not worth tracking.

## Step 2: Score each risk

Use a simple 1–3 × 1–3 matrix:
- **Likelihood**: 1 = Unlikely (has happened rarely or conditions are unfavourable), 2 = Possible (realistic given the project context), 3 = Likely (actively occurring or strong indicators present)
- **Impact**: 1 = Minor (small rework, < 1 week delay), 2 = Significant (phase slip, scope change), 3 = Severe (launch blocked, major rework required)
- **Score** = Likelihood × Impact (1–9)

Prioritise score 6+ for active mitigation. Score 3–5 for monitoring. Score 1–2 can be logged and checked at the next checkpoint.

## Step 3: Define mitigations

For each risk with score 3+:
- **Prevention**: what action reduces the likelihood of this risk occurring?
- **Contingency**: if it occurs anyway, what's the response plan?
- Assign an owner — the person responsible for executing the mitigation
- Set a review date — when to reassess the score

Avoid vague mitigations like "monitor closely". Be specific: *"Schedule API integration spike in Cycle 3 before committing to Layer 4 timeline."*

## Step 4: Flag unmitigated high risks

Any risk with score 6+ and no viable mitigation should be flagged for escalation or an explicit acceptance decision. Don't leave high risks in the register without an owner and a plan.

## Step 5: Update existing register (if provided)

If a risk register already exists:
- Update scores for risks where status has changed
- Close risks that have been resolved or are no longer relevant
- Add new risks identified since the last review
- Note the trend for the summary (increasing / stable / decreasing)

---

Use the structure from [risk-template.md](risk-template.md).
