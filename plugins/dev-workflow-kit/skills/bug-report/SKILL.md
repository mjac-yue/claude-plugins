---
name: bug-report
description: Structure a bug report with reproduction steps, severity, environment details, and expected vs. actual behavior. Use when filing a defect during development or QA.
disable-model-invocation: true
---

Create a bug report for: $ARGUMENTS

> **Learning note — Bug Report**
> A well-written bug report cuts investigation time in half. Reproduction steps, environment details, expected vs. actual behavior, and severity classification give the engineer everything they need to reproduce and fix the issue without back-and-forth. Vague bug reports — "it broke" or "the button doesn't work" — are one of the biggest sources of engineering inefficiency. The time invested in a clear, structured bug report is returned many times over in faster fixes and fewer misunderstandings.

Display the learning note above verbatim to the user before proceeding.

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

## Save output

After presenting the bug report to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/bug-report` and save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. In that same project `CLAUDE.md`, find the **Project status** table and set the **Status** column to **Done** for the row matching this deliverable
5. Confirm the file was written to the user
6. If no project `CLAUDE.md` exists, present the output for manual copying
