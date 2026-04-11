# QA Test Plan: [Feature Name]

**Author**: [Name]
**Date**: [Date]
**Status**: Draft | In Review | Approved
**Related PRD**: [Link]
**Related Tech Spec**: [Link]
**QA Owner**: [Name]
**Target test dates**: [Date range]

---

## Scope

**In scope**: [What is being tested]

**Out of scope**: [What is explicitly not being tested and why]

**Quality risks** (what we're most concerned about):
- 
- 

---

## Test Types & Coverage Targets

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

### Happy Path

| # | Test case | Preconditions | Steps | Expected result | Type |
|---|-----------|--------------|-------|----------------|------|
| TC-1 | [Name] | [Setup / test data] | 1. [Step] 2. [Step] | [What happens] | e2e |
| TC-2 | | | | | |

### Edge Cases

| # | Test case | Preconditions | Steps | Expected result | Type |
|---|-----------|--------------|-------|----------------|------|
| TC-10 | [Boundary condition] | | | | |
| TC-11 | [Empty/null input] | | | | |

### Error States

| # | Test case | Preconditions | Steps | Expected result | Type |
|---|-----------|--------------|-------|----------------|------|
| TC-20 | [API returns 500] | | | Friendly error shown, no data loss | Manual |
| TC-21 | [Network timeout] | | | Retry prompt displayed | Manual |

### Security

| # | Test case | Expected result | Type |
|---|-----------|----------------|------|
| TC-30 | Unauthenticated request to protected endpoint | HTTP 401 returned | Integration |
| TC-31 | SQL injection in [field] | Input sanitized, no DB error | Integration |
| TC-32 | XSS in [field] | Script tags stripped/escaped | Integration |

---

## Test Environment Requirements

| Requirement | Detail |
|-------------|--------|
| Environment | [Staging / feature branch / dedicated QA env] |
| Feature flag | [Flag name] = `true` |
| Test data | [Seeded accounts, fixture data, or API stubs needed] |
| External services | [Mocked / sandboxed / live?] |
| Credentials | [Where to find test account credentials] |

---

## Acceptance Criteria

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

*Existing features that could be affected and must be re-verified.*

| Area | Risk | Test cases to re-run |
|------|------|---------------------|
| [Related feature] | [Why it could regress] | [TC list or test suite name] |

---

## Bug Triage & Sign-Off

**Bug severity definitions**:
- **P0**: Blocks sign-off. Must fix before release.
- **P1**: Must fix before release or accepted with documented risk.
- **P2**: Should fix; can ship with plan to address.
- **P3**: Nice to fix; tracked in backlog.

**Sign-off owner**: [Name]
**Sign-off criteria**: Zero P0s open; all acceptance criteria met; P1s resolved or accepted.
**Escalation path**: [Who to contact if blocking issues arise]
