# Bug Report: [Title]

**Reporter**: [Name]
**Date**: [Date]
**Severity**: P0 Critical | P1 High | P2 Medium | P3 Low
**Status**: Open | In Progress | Resolved | Closed
**Assignee**: [Name]

> **Learning note — Bug Report**
> - **Why**: The communication channel between whoever finds a problem and whoever fixes it — quality of the report directly determines how quickly the bug gets fixed
> - **Who uses it**: QA, users, and engineers file them; PM triages severity and priority; Engineering leads spot patterns across reports
> - **Key decisions**: What is the correct severity based on user impact? Is this reproducible? What's the root cause hypothesis?
> - **Next step**: Triaged → assigned → reproduced → fixed → verified closed

---

## Title

> **Note — Title**: The pattern "[Component] [What happens] when [condition]" encodes where the bug is (routing), the symptom (triage), and under what conditions (reproduction). Good: "Checkout button stays disabled after removing coupon code on mobile Safari." Bad: "Checkout not working."

*[Component] [What happens] when [condition]*

> Example: "Checkout button stays disabled after removing coupon code on mobile Safari"

---

## Severity Rationale

> **Note — Severity Rationale**: Severity is based on user impact, not technical complexity — a minor cosmetic bug in a critical flow deserves higher severity than a complex bug affecting 0.01% of users.

> 💡 **Tip**: *[Your AI will assess the appropriate severity level given the affected user flow, workaround availability, and percentage of users impacted by this specific bug.]*

**Why this severity**:
- **P0** — Data loss / security issue / service down / complete blocker for key user flow
- **P1** — Major feature broken, no workaround available
- **P2** — Feature works but behavior is wrong or degraded; workaround exists
- **P3** — Cosmetic issue, minor inconsistency, or rare edge case

---

## Environment

> **Note — Environment**: Environment information determines reproducibility and helps narrow the root cause. The most common omission is the user account — many bugs are user-specific or data-specific. Anonymize real user data but preserve enough to reconstruct the scenario.

| Field | Value |
|-------|-------|
| App version / build | |
| Environment | Production / Staging / [Branch name] |
| Browser | [Chrome 123 / Safari 17 / Firefox 125] |
| OS | [macOS 14.4 / iOS 17 / Windows 11] |
| Device | [Desktop / iPhone 15 / etc.] |
| User account | [Anonymized ID or test account name] |
| Feature flag state | [Flag name] = [value] |

---

## Steps to Reproduce

> **Note — Steps to Reproduce**: Each step must be specific enough to follow without prior knowledge — "Navigate to [URL]" rather than "go to checkout." Start from a clean state to prevent environmental contamination from previous sessions.

*Start from a clean state. Be specific enough that anyone can reproduce.*

1. Navigate to [URL / screen]
2. [Action]
3. [Action]
4. Observe: [what happens]

**Frequency**: Always reproducible | Intermittent ([X]% of attempts) | One-time occurrence

---

## Expected Behavior

> **Note — Expected Behavior**: The baseline against which actual behavior is measured. Reference the source of truth — a PRD requirement, design spec, or documented behavior. This also serves as the acceptance criterion for the fix.

*What should have happened?*

> 

---

## Actual Behavior

> **Note — Actual Behavior**: Factual description only — verbatim error messages, exact UI state, specific data values. Quote error messages exactly rather than paraphrasing. Hypotheses about cause belong in the Possible Cause section, clearly labeled as speculation.

*What happened instead? Include exact error messages, screenshots, or log excerpts.*

> 

**Error message** (if any):
```
[Paste error text verbatim]
```

---

## Screenshots / Recording

> **Note — Screenshots / Recording**: A screenshot communicates in one second what takes a paragraph to describe. Console logs and network request logs from browser dev tools are invaluable for frontend bugs — they often show the exact API response or JS error.

*Attach or link screenshots, screen recordings, or console logs here.*

- 

---

## Possible Cause (optional)

> **Note — Possible Cause**: Clearly labeled as speculation, not fact. A wrong hypothesis labeled as such saves investigation time; one presented as fact sends engineers down the wrong path. If you don't have a hypothesis, leave this blank.

*If you have a hypothesis, note it here — clearly separated from the factual description above.*

> 

---

## Related Issues / PRs

> **Note — Related Issues / PRs**: The most valuable link is a PR that may have introduced the bug — it immediately gives the engineer the code change to investigate and the author to consult.

- [Link to related bug]
- [Link to PR that may have introduced this]

---

## Additional Context

> **Note — Additional Context**: Captures information that doesn't fit elsewhere but could be critical — a recent deploy, config change, or similar reports from multiple users. "Multiple users are reporting this" can elevate a P2 to a P1.

*Anything else that might be relevant — recent deploys, config changes, similar reports from users.*

> 
