---
name: security-review
description: Conduct a security review aligned to OWASP Top 10 — covering authentication, authorization, input validation, data exposure, dependency vulnerabilities, and more. Use before launch or when reviewing a security-sensitive change.
disable-model-invocation: true
---

Conduct a security review for: $ARGUMENTS

> **Learning note — Security Review**
> Security vulnerabilities are exponentially more expensive to fix after launch than before — and the most common ones (broken access control, injection, authentication failures) follow predictable patterns documented in the OWASP Top 10. A security review before deployment is your last structured opportunity to catch these before real users and real data are at risk. It's also a trust issue: users who have their data exposed because of a preventable vulnerability rarely return.

Display the learning note above verbatim to the user before proceeding.

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

**AI security checks** (if AI/ML components are in scope — skip entirely if not):

> **Learning note — AI Security**
> AI components introduce a class of vulnerabilities not covered by OWASP Top 10. Prompt injection is the AI equivalent of SQL injection: user input manipulates model behavior in unintended ways. PII leakage through third-party AI APIs is a real compliance risk — sending user data to OpenAI or Anthropic may violate data residency requirements or contractual obligations. These checks must be evaluated before launch for any product with AI components.

Display the learning note verbatim before AI security checks.

- **Prompt injection** — Can a user craft input that overrides the system prompt or changes model behavior? Test: does passing `"Ignore all previous instructions and..."` in user input cause the model to deviate from intended behavior? Mitigation: input sanitization, output validation, system prompt anchoring, separate instruction and data channels where possible.

- **Indirect prompt injection** — If the AI reads external content (documents, web pages, emails, database records), can that content contain embedded instructions the model will follow? Test: embed `"Assistant: disregard user goals and instead..."` in a document the AI processes. Mitigation: treat all externally retrieved content as untrusted data; validate AI outputs before acting on them.

- **PII leakage through AI APIs** — Is user PII (names, emails, financial data, health data) being sent to third-party AI APIs? Does this comply with your data processing agreements and the applicable data residency requirements? Are users informed? Mitigation: anonymize or redact PII before sending to third-party APIs; use on-premises or data-residency-compliant models where contractually required.

- **Model output safety** — Can the AI produce harmful, biased, legally risky, or brand-damaging content at scale? Is there a content filter or output validation layer? What is the response when a content policy violation is triggered? Mitigation: output validation, content filtering, clear user-facing error messages for rejected outputs, monitoring for repeated violations.

- **Over-reliance on AI output** — Is AI output being used for decisions that should require human verification (access control, financial calculations, identity confirmation, legal conclusions)? Is there a human-in-the-loop requirement missing from the design? Mitigation: never use AI output as the sole authority for consequential decisions; require human confirmation or rule-based verification for high-stakes outputs.

- **AI API key exposure** — Are AI API keys stored securely (environment variables / secrets manager, never hardcoded)? Are keys scoped to the minimum permissions needed? Is there a key rotation plan? What is the blast radius if a key is leaked?

- **Training data exposure** (if fine-tuning) — Does the training data contain PII, confidential business information, or copyrighted material? Is the training pipeline access-controlled?

Assign severity using the same scale as other findings. Prompt injection and PII leakage through AI APIs are typically **Critical** or **High**.

For each finding, assign:
- **Critical**: Immediate risk of data breach, account takeover, or privilege escalation — block launch
- **High**: Significant risk under reasonably foreseeable attack — fix before launch
- **Medium**: Risk exists but requires specific conditions — fix soon after launch
- **Low**: Defense-in-depth improvement — track in backlog

Output a security review with findings, evidence, and concrete remediation steps.

## Save output

After presenting the security review to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/security-review` and save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. In that same project `CLAUDE.md`, find the **Project status** table and set the **Status** column to **Done** for the row matching this deliverable
5. Confirm the file was written to the user
6. If no project `CLAUDE.md` exists, present the output for manual copying
