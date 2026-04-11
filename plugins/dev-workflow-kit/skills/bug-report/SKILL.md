---
name: bug-report
description: Structure a bug report with reproduction steps, severity, environment details, and expected vs. actual behavior. Use when filing a defect during development or QA.
disable-model-invocation: true
---

Create a bug report for: $ARGUMENTS

Use the template in [bug-report-template.md](bug-report-template.md) as the structure.

Follow this process:
1. **Write a clear title** — one sentence that uniquely identifies the bug. Format: "[Component] [What happens] when [condition]". Example: "Checkout button disabled after removing coupon code on mobile Safari."
2. **Assign severity**:
   - **P0 — Critical**: data loss, security vulnerability, service down, or complete blocker for a key user flow
   - **P1 — High**: major feature broken with no workaround
   - **P2 — Medium**: feature works but behavior is wrong or degraded; workaround exists
   - **P3 — Low**: cosmetic issue, minor inconsistency, or edge case with minimal user impact
3. **Document the environment**:
   - Browser/device/OS (if frontend)
   - App version or build number
   - Environment (production, staging, feature branch)
   - User account or test data used (anonymized if sensitive)
4. **Write step-by-step reproduction steps** — numbered, specific enough that anyone can reproduce from scratch. Start from a clean state.
5. **State expected behavior** — what should have happened?
6. **State actual behavior** — what happened instead? Include error messages, screenshots, or log excerpts verbatim.
7. **Note frequency** — always reproducible, intermittent (X% of attempts), or one-time?
8. **Identify possible cause** (optional) — if you have a hypothesis about the root cause, note it separately from the factual description.
9. **List related issues or PRs** — any known related bugs or recent changes that may be connected.

Output a bug report ready to file in a tracker (Linear, Jira, GitHub Issues, etc.).
