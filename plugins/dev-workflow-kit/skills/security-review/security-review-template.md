# Security Review: [Feature / System Name]

**Reviewer**: [Name]
**Date**: [Date]
**Scope**: [What is being reviewed — feature, PR, API, service]
**Related ticket / PRD**: [Link]
**Environment reviewed**: [Code / design / both]

---

## Overall Assessment

**Risk level**: Critical | High | Medium | Low | Clear
**Verdict**: Block launch | Fix before launch | Fix post-launch with tracking | No action needed

**Summary**: [2–3 sentences on overall security posture and the most important findings]

---

## OWASP Top 10 Evaluation

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

| Question | Owner | Due |
|----------|-------|-----|
| | | |
