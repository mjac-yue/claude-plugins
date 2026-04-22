# Risk Register: [Project Name]

**Author**: [Name]
**Last updated**: [Date]
**Review cadence**: [Weekly / At each risk checkpoint in release plan]

> **Learning note — Risk Register**
> - **Why**: Proactively tracks what could go wrong and what the mitigation plan is — before problems become incidents
> - **Who uses it**: PM maintains it; Engineering and Design contribute domain risks; stakeholders review high-severity items
> - **Key decisions**: Which risks need active mitigation vs. monitoring? Which exceed appetite thresholds and require escalation?
> - **Next step**: Reviewed at each release plan risk checkpoint; closed risks archived for retrospective learning

---

## Risk Summary

> **Note — Risk Summary**: An increasing trend signals more problems are being uncovered than resolved — a warning sign that may require scope, timeline, or resource changes.

| Severity | Count | Trend |
|----------|-------|-------|
| High (score 6–9) | | ↑ Increasing / → Stable / ↓ Decreasing |
| Medium (score 3–5) | | |
| Low (score 1–2) | | |

> 💡 **Tip**: *[Your AI will identify which risks are most likely to materialize given your current phase, team composition, and technical stack — and flag which mitigations need immediate action.]*

---

## Active Risks

> **Note — Active Risks**: Score 6+ requires active mitigation; 3–5 monitor; 1–2 log and review periodically. The "Residual risk" column shows what risk remains after mitigation — a High residual may mean the plan needs revisiting.

*Scored: Likelihood (1–3) × Impact (1–3) = Score. Prioritise score 6+ first.*

| ID | Risk | Category | Likelihood | Impact | Score | Owner | Mitigation | Residual risk | Review date | Status |
|----|------|----------|-----------|--------|-------|-------|-----------|--------------|------------|--------|
| R-01 | | Schedule / Scope / Tech / Resource / External | 1–3 | 1–3 | | | | Low / Medium / High | | Open |
| R-02 | | | | | | | | | | |
| R-03 | | | | | | | | | | |

**Scoring guide**:
- Likelihood: 1 = Unlikely, 2 = Possible, 3 = Likely
- Impact: 1 = Minor delay or rework, 2 = Phase slip or scope change, 3 = Launch blocked or major rework

---

## Risk Detail

> **Note — Risk Detail**: Prevention reduces probability; contingency is the response plan if it materializes anyway. "Monitor closely" is not a mitigation — "schedule a spike in Cycle 3 to test the integration" is.

### R-01: [Risk name]

**Description**: [What could go wrong and under what conditions]
**Category**: Schedule / Scope / Technical / Resource / External
**Likelihood**: [1–3] — [Reason]
**Impact**: [1–3] — [What happens if this risk materialises]
**Score**: [L × I]

**Mitigation plan**:
1. [Action to reduce likelihood]
2. [Action to reduce impact if it occurs]

**Contingency** (if risk materialises):
- [What we'll do]

**Owner**: [Name]
**Residual risk after mitigation**: Low / Medium / High
**Review date**: [Date]
**Status**: Open / Mitigated / Closed

---

*(Repeat R-0N block for each risk)*

---

## Closed Risks

> **Note — Closed Risks**: Preserved for decision history and retrospective learning — which mitigations worked, which didn't, and which risks weren't anticipated at all.

| ID | Risk | Closed date | Outcome |
|----|------|------------|---------|
| | | | Mitigated / Did not occur / Accepted |

---

## Risk Appetite

> **Note — Risk Appetite**: Sets escalation thresholds so engineers know when to manage autonomously vs. escalate — avoiding ad-hoc judgment calls under pressure.

*Agreed thresholds for this project.*

| Threshold | Decision |
|-----------|---------|
| Any score 9 | Immediate escalation to [stakeholder] |
| Score 6–8 | Weekly review, mitigation required within [N] days |
| Score 3–5 | Fortnightly review |
| Score 1–2 | Monitor, no active mitigation required |
