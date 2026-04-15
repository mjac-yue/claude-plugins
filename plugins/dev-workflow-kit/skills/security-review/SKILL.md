---
name: security-review
description: Conduct a security review aligned to OWASP Top 10 — covering authentication, authorization, input validation, data exposure, dependency vulnerabilities, and more. Use before launch or when reviewing a security-sensitive change.
disable-model-invocation: true
---

Conduct a security review for: $ARGUMENTS

> **Learning note — Security Review**
> Security vulnerabilities are exponentially more expensive to fix after launch than before — and the most common ones (broken access control, injection, authentication failures) follow predictable patterns documented in the OWASP Top 10. A security review before deployment is your last structured opportunity to catch these before real users and real data are at risk. It's also a trust issue: users who have their data exposed because of a preventable vulnerability rarely return.

Use the template in [security-review-template.md](security-review-template.md) as the structure.

Follow this process, evaluating each OWASP Top 10 category plus additional checks:

1. **A01 — Broken Access Control**:
   - Are authorization checks present on every operation that modifies or reads sensitive data?
   - Can a user access or modify another user's data (IDOR — Insecure Direct Object Reference)?
   - Are privilege levels enforced server-side, not just client-side?
   - Is the principle of least privilege applied to service accounts and API keys?

2. **A02 — Cryptographic Failures**:
   - Is sensitive data (PII, credentials, tokens) encrypted at rest and in transit?
   - Are weak or deprecated algorithms in use (MD5, SHA-1, DES)?
   - Are secrets stored in environment variables or a secrets manager — never hardcoded or in version control?
   - Is TLS enforced (no HTTP fallback)?

3. **A03 — Injection**:
   - Is all user input parameterized or sanitized before use in SQL, commands, LDAP, or XML?
   - Are ORM methods used correctly (no raw query string interpolation)?
   - Is output encoded to prevent XSS (HTML, JavaScript, URL context)?

4. **A04 — Insecure Design**:
   - Are there threat model gaps — functionality that was designed without considering abuse cases?
   - Are rate limits and anti-automation controls in place for sensitive operations (login, password reset, payment)?

5. **A05 — Security Misconfiguration**:
   - Are default credentials, sample data, or debug endpoints removed?
   - Are error messages safe (no stack traces, internal paths, or system info to end users)?
   - Are security headers set (CSP, HSTS, X-Frame-Options, etc.)?
   - Are unnecessary features, endpoints, or permissions disabled?

6. **A06 — Vulnerable & Outdated Components**:
   - Are dependencies up to date?
   - Are there known CVEs in any dependency versions in use?
   - Is there a process to receive and act on vulnerability alerts?

7. **A07 — Authentication Failures**:
   - Are session tokens sufficiently random and invalidated on logout?
   - Is there brute-force protection on authentication endpoints?
   - Are password reset flows secure (short-lived tokens, one-time use)?
   - Is MFA available for sensitive operations?

8. **A08 — Software & Data Integrity Failures**:
   - Is there integrity verification for any code, plugins, or data loaded from external sources?
   - Are CI/CD pipelines protected against unauthorized modification?

9. **A09 — Security Logging & Monitoring**:
   - Are authentication events, access control failures, and input validation failures logged?
   - Are logs free of sensitive data (passwords, tokens, PII)?
   - Are alerts configured for anomalous patterns?

10. **A10 — Server-Side Request Forgery (SSRF)**:
    - If the feature fetches URLs or resources based on user input, is the destination validated against an allowlist?

**Additional checks**:
- **API security**: Are all endpoints authenticated? Are response bodies free of over-exposed fields?
- **File upload** (if applicable): Are file types validated? Are uploads stored outside the web root?
- **Third-party integrations**: Are webhook payloads verified? Are API keys scoped to minimum permissions?

For each finding, assign:
- **Critical**: Immediate risk of data breach, account takeover, or privilege escalation — block launch
- **High**: Significant risk under reasonably foreseeable attack — fix before launch
- **Medium**: Risk exists but requires specific conditions — fix soon after launch
- **Low**: Defense-in-depth improvement — track in backlog

Output a security review with findings, evidence, and concrete remediation steps.
