# QA Test Plan: [Feature Name]

**Author**: [Name]
**Date**: [Date]
**Status**: Draft | In Review | Approved
**Related PRD**: [Link]
**Related Tech Spec**: [Link]
**QA Owner**: [Name]
**Target test dates**: [Date range]

> **Learning note — QA Test Plan**
> - **Why**: Defines what will be tested, how, and by whom — ensures systematic coverage of all behaviors, not just the happy path
> - **Who uses it**: QA engineers write and execute it; Engineers understand the division between unit/integration tests (theirs) and end-to-end/exploratory (QA's); PM makes informed release readiness decisions
> - **Key decisions**: Are all acceptance criteria covered by test cases? What is the sign-off threshold? Which existing features need regression testing?
> - **Next step**: QA sign-off when all acceptance criteria met → PM release decision

---

## Scope

> **Note — Scope**: The "out of scope" justification is as important as what's excluded — "not tested because it's unchanged" is acceptable; "not tested because we don't have time" should trigger a readiness conversation. Quality risks shape where to focus depth.

**In scope**: [What is being tested]

**Out of scope**: [What is explicitly not being tested and why]

**Quality risks** (what we're most concerned about):
- 
- 

---

## Test Types & Coverage Targets

> **Note — Test Types & Coverage Targets**: Different test types catch different defects at different costs. Performance and security tests are often omitted from test plans — their presence here ensures they're planned, not discovered as missing after launch.

| Test type | Coverage target | Tool / framework | Owner |
|-----------|---------------|-----------------|-------|
| Unit tests | ≥[X]% for new/modified modules | [Jest / pytest / etc.] | Dev |
| Integration tests | All service boundaries | [Framework] | Dev |
| End-to-end tests | [N] critical user journeys | [Playwright / Cypress / etc.] | QA |
| Manual / exploratory | Edge cases, visual, UX | — | QA |
| Performance tests | [Latency / load targets] | [k6 / Locust / etc.] | Dev / Infra |
| Security tests | [Auth, input validation, exposure] | [OWASP ZAP / manual] | Security / Dev |

---

## Test Cases

> **Note — Test Cases**: Write test cases from the user's perspective (what should this experience be?) not the implementation perspective — user-perspective tests catch the bugs that unit tests miss.

### Happy Path

> **Note — Happy Path**: The minimum viable test coverage — a feature that doesn't pass its happy path tests should not be released regardless of other considerations. Each test case must be specific enough to execute without ambiguity.

| # | Test case | Preconditions | Steps | Expected result | Type |
|---|-----------|--------------|-------|----------------|------|
| TC-1 | [Name] | [Setup / test data] | 1. [Step] 2. [Step] | [What happens] | e2e |
| TC-2 | | | | | |

### Edge Cases

> **Note — Edge Cases**: Most production bugs hide here. Most commonly missed: empty states (user with no records), boundary conditions (exactly at max value), and concurrent operations (two requests for the same resource simultaneously).

| # | Test case | Preconditions | Steps | Expected result | Type |
|---|-----------|--------------|-------|----------------|------|
| TC-10 | [Boundary condition] | | | | |
| TC-11 | [Empty/null input] | | | | |

### Error States

> **Note — Error States**: Verify the system fails gracefully — users see a helpful message rather than a crash or data corruption. The most important error states: external service unavailable, invalid input at submission, auth token expired mid-session, concurrent modification by two users.

> 💡 **Tip**: *[Your AI will identify the most likely error states to test given the external dependencies and data flows in this specific feature.]*

| # | Test case | Preconditions | Steps | Expected result | Type |
|---|-----------|--------------|-------|----------------|------|
| TC-20 | [API returns 500] | | | Friendly error shown, no data loss | Manual |
| TC-21 | [Network timeout] | | | Retry prompt displayed | Manual |

### Security

> **Note — Security**: Must be run against a real environment — security vulnerabilities are often in the integration between components, not the components themselves. The three listed are the minimum baseline; features handling sensitive data need additional cases.

| # | Test case | Expected result | Type |
|---|-----------|----------------|------|
| TC-30 | Unauthenticated request to protected endpoint | HTTP 401 returned | Integration |
| TC-31 | SQL injection in [field] | Input sanitized, no DB error | Integration |
| TC-32 | XSS in [field] | Script tags stripped/escaped | Integration |

---

## Test Environment Requirements

> **Note — Test Environment Requirements**: Tests run against an incorrect environment produce unreliable results. The most common gaps are missing test data and live external services (tests trigger real charges or real emails that pollute production data).

| Requirement | Detail |
|-------------|--------|
| Environment | [Staging / feature branch / dedicated QA env] |
| Feature flag | [Flag name] = `true` |
| Test data | [Seeded accounts, fixture data, or API stubs needed] |
| External services | [Mocked / sandboxed / live?] |
| Credentials | [Where to find test account credentials] |

---

## Acceptance Criteria

> **Note — Acceptance Criteria**: Each criterion should be verifiable by any team member — not "performance is acceptable" but "p95 latency < 500ms under 100 concurrent users." The most important criterion is "no P0 bugs open" — a feature with a known critical bug should never ship.

> 💡 **Tip**: *[Your AI will flag which acceptance criteria are at highest risk of not being met given the current test results and open bugs for this feature.]*

*QA sign-off requires all of these to be true.*

- [ ] All P0 user journeys complete without error
- [ ] All TC-1 through TC-[N] happy path cases pass
- [ ] No P0 bugs open; P1 bugs reviewed and accepted or fixed
- [ ] Performance: [p95 latency < Xms under Y concurrent users]
- [ ] No new WCAG 2.1 AA violations introduced
- [ ] Analytics events fire correctly for [key actions]
- [ ] Rollback tested and confirmed functional

---

## Regression Scope

> **Note — Regression Scope**: A regression in a core feature is often more impactful than a bug in the new feature. The most commonly missed regression areas are shared infrastructure (schema changes affecting multiple features) and authentication flows (session handling changes affecting all authenticated experiences).

*Existing features that could be affected and must be re-verified.*

| Area | Risk | Test cases to re-run |
|------|------|---------------------|
| [Related feature] | [Why it could regress] | [TC list or test suite name] |

---

## Bug Triage & Sign-Off

> **Note — Bug Triage & Sign-Off**: The release decision is ultimately a product judgment — PM is typically the sign-off owner. The escalation path is critical; it defines who makes the call when PM and Engineering lead disagree about a bug's severity.

**Bug severity definitions**:
- **P0**: Blocks sign-off. Must fix before release.
- **P1**: Must fix before release or accepted with documented risk.
- **P2**: Should fix; can ship with plan to address.
- **P3**: Nice to fix; tracked in backlog.

**Sign-off owner**: [Name]
**Sign-off criteria**: Zero P0s open; all acceptance criteria met; P1s resolved or accepted.
**Escalation path**: [Who to contact if blocking issues arise]
