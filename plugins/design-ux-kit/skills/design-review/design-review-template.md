# Design Review: [Feature / Screen Name]

**Reviewer**: [Name]
**Date**: [Date]
**Design version reviewed**: [Version / link]
**Platform**: [Web / iOS / Android / All]

> **Learning note — Design Review**
> - **Why**: Structured quality gate that catches usability and accessibility problems before code is written — when they're cheapest to fix
> - **Who uses it**: Designers pressure-test their own work; PMs verify the design meets UX brief success criteria; Engineers understand what QA will verify
> - **Key decisions**: Is the design approved to move to development, or does it need another iteration?
> - **Next step**: Approved → design handoff; Needs Rework → return to wireframe spec for specific screens

---

## Overall Assessment

> **Note — Overall Assessment**: Gives stakeholders a one-glance summary. Key decision: "Approved with Changes" means development can start while specific issues are addressed; "Needs Rework" returns specific screens to wireframe, not the full feature to start-over.

**Rating**: Approved | Approved with Changes | Needs Rework

**Summary**:
*2–3 sentences on the overall quality and the most important things to address.*

---

## Heuristic Evaluation

> **Note — Heuristic Evaluation**: Nielsen's 10 heuristics are a research-validated framework for identifying usability problems before user testing. Key discipline: structured evaluation against frameworks, not subjective feedback — "users won't know what happened after clicking Submit (Heuristic 1)" is a finding; "I don't like it" is not.

> 💡 **Tip**: *[Your AI will highlight which heuristics are most likely violated given your specific feature type and user context, so you know where to look hardest.]*

*Severity: **Critical** = blocks task completion | **Major** = significantly degrades experience | **Minor** = polish issue*

| # | Heuristic | Rating | Findings |
|---|-----------|--------|---------|
| 1 | Visibility of system status | Pass / Issue | |
| 2 | Match between system and real world | Pass / Issue | |
| 3 | User control and freedom | Pass / Issue | |
| 4 | Consistency and standards | Pass / Issue | |
| 5 | Error prevention | Pass / Issue | |
| 6 | Recognition rather than recall | Pass / Issue | |
| 7 | Flexibility and efficiency of use | Pass / Issue | |
| 8 | Aesthetic and minimalist design | Pass / Issue | |
| 9 | Error recovery | Pass / Issue | |
| 10 | Help and documentation | Pass / Issue | |

---

## Accessibility Audit (WCAG 2.1 AA)

> **Note — Accessibility Audit**: WCAG 2.1 AA compliance is both a legal requirement in many jurisdictions and a usability improvement for all users. Key principle: accessibility can't be added as a polish pass at the end — structural problems must be designed in from the start.

| Check | Status | Notes |
|-------|--------|-------|
| Color contrast (4.5:1 text, 3:1 UI) | Pass / Fail | |
| Touch/click target size (44×44px min) | Pass / Fail | |
| Keyboard navigation & focus order | Pass / Fail | |
| Focus indicators visible | Pass / Fail | |
| Screen reader labels (ARIA, alt text) | Pass / Fail | |
| Text resize to 200% without loss | Pass / Fail | |
| No content conveyed by color alone | Pass / Fail | |

---

## Consistency Check

> **Note — Consistency Check**: Users who learn a pattern in one part of the product expect it everywhere. Key decision: is a new pattern being introduced intentionally (needs to go into the design system) or accidentally (needs to be corrected)?

| Area | Status | Notes |
|------|--------|-------|
| Matches design system components | Pass / Issue | |
| Consistent terminology with rest of product | Pass / Issue | |
| Consistent interaction patterns | Pass / Issue | |
| Consistent iconography and imagery style | Pass / Issue | |

---

## Missing States

> **Note — Missing States**: Most common source of post-launch UI bugs. Every missing state listed here needs a design before development begins — otherwise Engineering implements their own version, creating inconsistent user experiences.

| State | Screen(s) | Notes |
|-------|-----------|-------|
| Empty state | | |
| Loading state | | |
| Error state | | |
| Success / confirmation | | |
| Edge cases | | |

---

## Prioritized Findings

> **Note — Prioritized Findings**: Severity ensures the most important problems are addressed first. Critical issues block launch; Major issues degrade experience significantly; Minor issues are polish items. PMs use this section for scope decisions: all Critical and Major issues should be fixed before development starts.

> 💡 **Tip**: *[Your AI will flag which findings are most likely to affect your key success metrics and which are safe to defer to a follow-up sprint given your timeline.]*

### Critical Issues (must fix before development)
1. **[Finding]** — [Screen/component] — [Why it matters] — [Recommended fix]

### Major Issues (should fix)
1. **[Finding]** — [Screen/component] — [Recommended fix]

### Minor Issues (nice to have)
1. **[Finding]** — [Screen/component] — [Recommended fix]

---

## Questions for the Designer

> **Note — Questions for the Designer**: Captures ambiguities and intentional choices that need clarification before findings are fully assessed. Some "issues" turn out to be intentional decisions the reviewer didn't understand; some questions reveal missing requirements that should go back to the PM.

1. 
2. 
3. 
