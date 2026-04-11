# Development Plan: [Feature Name]

**Author**: [Name]
**Date**: [Date]
**Status**: Draft | Approved
**Related Tech Spec**: [Link]
**Engineering Owner**: [Name]
**Team size**: [N engineers]
**Target completion**: [Date]

---

## Goal & Constraints

**What we're building**: [One sentence]
**Success state**: [What does "done" look like from a product perspective?]

**Constraints**:
- Timeline: [Hard deadline or preferred date]
- Team: [Available engineers and disciplines]
- Dependencies: [Must-have inputs from other teams before starting]

---

## Task Breakdown

| # | Task | Discipline | Estimate | Depends on | Owner role | Notes |
|---|------|-----------|----------|-----------|------------|-------|
| 1 | | FE / BE / Infra / Data | [days or points] | — | | |
| 2 | | | | #1 | | |
| 3 | | | | — | | |

**Estimation notes**:
- [Any non-obvious estimate that needs explanation]

---

## Critical Path

*The sequence of dependent tasks that determines earliest possible completion.*

```
Task 1 (3d) → Task 3 (2d) → Task 6 (1d) → QA (2d) → Done
```

**Critical path total**: [N days]

---

## Blockers (must resolve before work can start)

| Blocker | Owner | Due | Status |
|---------|-------|-----|--------|
| [Design assets needed] | | | |
| [API keys / credentials] | | | |
| [Platform / infra decision] | | | |

---

## Sprint Allocation

*Assumes [N]-day sprints at [X]% planned capacity.*

### Sprint 1: [Goal / Theme]

| Task | Assignee | Est. |
|------|----------|------|
| | | |

**Sprint outcome**: [What will be true at the end of this sprint?]

### Sprint 2: [Goal / Theme]

| Task | Assignee | Est. |
|------|----------|------|
| | | |

**Sprint outcome**:

---

*(Add sprints as needed)*

---

## Milestones

| Milestone | Target date | Definition |
|-----------|------------|------------|
| API complete + tested | | All endpoints functional, integration tests passing |
| Feature complete in staging | | All tasks done, feature flag on in staging |
| QA sign-off | | All acceptance criteria verified |
| Ready for release | | Rollback plan confirmed, monitoring in place |

---

## Risks to the Plan

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| [Dependency slips] | H/M/L | H/M/L | |
| [Scope creep] | H/M/L | H/M/L | Strict change control via PRD owner |
| [Technical unknown] | H/M/L | H/M/L | Time-boxed spike in Sprint 1 |

---

## Definition of Done

The feature is complete when **all** of the following are true:

- [ ] All tasks marked complete and code merged to main
- [ ] Unit + integration tests passing at ≥[X]% coverage
- [ ] QA sign-off documented
- [ ] No open P0 or P1 bugs
- [ ] Analytics events instrumented and verified
- [ ] Feature flag configured for controlled rollout
- [ ] Rollback procedure documented and tested
- [ ] Documentation updated (API docs, runbook, changelog)

---

## Open Questions

| Question | Owner | Due | Status |
|----------|-------|-----|--------|
| | | | |
