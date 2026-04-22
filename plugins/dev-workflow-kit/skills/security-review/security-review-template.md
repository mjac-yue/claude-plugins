# Security Review: [Feature / System Name]

**Reviewer**: [Name]
**Date**: [Date]
**Scope**: [What is being reviewed — feature, PR, API, service]
**Related ticket / PRD**: [Link]
**Environment reviewed**: [Code / design / both]

> **Learning note — Security Review**
> - **Why**: Systematically evaluates a feature for vulnerabilities before it reaches production — the last structural defense before code is exposed to real users and real attackers
> - **Who uses it**: Security engineers and senior engineers conduct it; Engineering leads use the verdict for launch decisions; PM understands security risks that could require scope changes
> - **Key decisions**: What is the overall risk level and verdict? Which findings are blocking launch? Are there Critical or High findings that cannot ship?
> - **Next step**: Critical and High findings remediated → re-review; Medium and Low tracked in backlog with plan

---

## Overall Assessment

> **Note — Overall Assessment**: The risk level and verdict are the two most important outputs. Features with "Block launch" verdicts need remediation before any production traffic. A "Clear" verdict means the reviewer looked and found no significant issues — not that the review was skipped.

**Risk level**: Critical | High | Medium | Low | Clear
**Verdict**: Block launch | Fix before launch | Fix post-launch with tracking | No action needed

**Summary**: [2–3 sentences on overall security posture and the most important findings]

---

## OWASP Top 10 Evaluation

> **Note — OWASP Top 10 Evaluation**: A "Pass" means the reviewer confirmed no vulnerability in that category — not that it was skipped. The most commonly found issues are A01 (Broken Access Control), A03 (Injection), and A07 (Authentication Failures). Any "Issue" finding should have a corresponding detailed finding below.

> 💡 **Tip**: *[Your AI will highlight which OWASP categories are most relevant to this specific feature type and flag which checks to examine most closely given the technology stack.]*

*Severity: **Critical** = immediate risk of breach/takeover | **High** = fix before launch | **Medium** = fix soon | **Low** = backlog*

| # | Category | Status | Severity | Finding |
|---|----------|--------|----------|---------|
| A01 | Broken Access Control | Pass / Issue / N/A | | |
| A02 | Cryptographic Failures | Pass / Issue / N/A | | |
| A03 | Injection | Pass / Issue / N/A | | |
| A04 | Insecure Design | Pass / Issue / N/A | | |
| A05 | Security Misconfiguration | Pass / Issue / N/A | | |
| A06 | Vulnerable & Outdated Components | Pass / Issue / N/A | | |
| A07 | Authentication Failures | Pass / Issue / N/A | | |
| A08 | Software & Data Integrity Failures | Pass / Issue / N/A | | |
| A09 | Security Logging & Monitoring | Pass / Issue / N/A | | |
| A10 | Server-Side Request Forgery | Pass / Issue / N/A | | |

---

## Additional Checks

> **Note — Additional Checks**: Cover vulnerability areas common in web applications that don't map cleanly to a single OWASP category. API endpoint authorization is the most frequently found gap — endpoints that exist but don't verify the authenticated user has permission to access the specific resource.

| Area | Status | Severity | Finding |
|------|--------|----------|---------|
| API endpoint authorization | Pass / Issue / N/A | | |
| Response body data exposure | Pass / Issue / N/A | | |
| File upload handling | Pass / Issue / N/A | | |
| Third-party webhook verification | Pass / Issue / N/A | | |
| Secrets management | Pass / Issue / N/A | | |
| Security headers | Pass / Issue / N/A | | |
| Rate limiting / anti-automation | Pass / Issue / N/A | | |

---

## Detailed Findings

> **Note — Detailed Findings**: The "Evidence" field is critical — a security finding without specific evidence can be disputed; evidence makes the finding undeniable and actionable. Remediation must be specific enough to implement: "use parameterized queries via `pg.query()` with `$1` placeholders" not "sanitize user input."

### Critical (block launch — immediate risk)

#### Finding 1: [Short title]
**Category**: [OWASP category or area]
**Location**: `[file:line or endpoint]`
**Description**: [What the vulnerability is and how it could be exploited]
**Evidence**: [Specific code snippet, request, or behavior demonstrating the issue]
**Impact**: [What an attacker could do if this is exploited]
**Remediation**: [Specific fix — code change, config change, or control to add]

---

### High (fix before launch)

#### Finding 1: [Short title]
**Category**:
**Location**:
**Description**:
**Impact**:
**Remediation**:

---

### Medium (fix soon after launch)

1. **[Title]** — `[location]` — [Description] — **Fix**: [Remediation]

---

### Low (track in backlog)

1. **[Title]** — `[location]` — [Description] — **Fix**: [Remediation]

---

## Security Checklist

> **Note — Security Checklist**: "Authorization checked server-side" deserves special emphasis — client-side authorization checks (hiding a button in the UI) are not security controls. A motivated attacker will call the API directly. Verify "no secrets in source code or logs" actively, not just assumed.

- [ ] All endpoints require authentication (or explicitly documented as public)
- [ ] Authorization checked server-side for every sensitive operation
- [ ] All user input parameterized / sanitized
- [ ] No secrets in source code or logs
- [ ] Sensitive data encrypted at rest and in transit
- [ ] Error messages safe (no stack traces to end users)
- [ ] Rate limiting on authentication and sensitive endpoints
- [ ] Dependencies scanned for known CVEs
- [ ] Security events logged (auth failures, access control failures)
- [ ] Logs free of PII and credentials

---

## Open Questions

> **Note — Open Questions**: An unresolved security question is not a deferred decision — it's an unknown risk. Do not launch a feature with Critical or High open security questions; treat them as findings at the highest severity of the possible outcomes.

| Question | Owner | Due |
|----------|-------|-----|
| | | |
