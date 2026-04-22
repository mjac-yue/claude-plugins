# Development Plan: [Feature Name]

**Author**: [Name]
**Date**: [Date]
**Status**: Draft | Approved
**Related Tech Spec**: [Link]
**Engineering Owner**: [Name]
**Team size**: [N engineers]
**Target completion**: [Date]

> **Learning note — Development Plan**
> - **Why**: Translates an approved tech spec into a concrete execution roadmap — tasks, dependencies, owners, and a realistic timeline
> - **Who uses it**: Engineers coordinate parallel work and avoid blockers; Engineering leads track delivery and surface risks; PM sets stakeholder expectations and assesses launch feasibility
> - **Key decisions**: What is the critical path? What must be resolved before work can start? Is the sprint allocation realistic given effective capacity?
> - **Next step**: Approved plan → sprint execution; blockers escalated before they become timeline threats

---

## Goal & Constraints

> **Note — Goal & Constraints**: The "success state" is product-facing (what will a user be able to do?) not technical (which components will be built?). A plan that ignores a hard deadline or understates team capacity is not a real plan.

**What we're building**: [One sentence]
**Success state**: [What does "done" look like from a product perspective?]

**Constraints**:
- Timeline: [Hard deadline or preferred date]
- Team: [Available engineers and disciplines]
- Dependencies: [Must-have inputs from other teams before starting]

---

## Task Breakdown

> **Note — Task Breakdown**: The "depends on" column is critical — it reveals the task sequencing that constrains the schedule and, combined with estimates, produces the critical path. Estimation notes capture reasoning behind non-obvious estimates for retrospective learning.

| # | Task | Discipline | Estimate | Depends on | Owner role | Notes |
|---|------|-----------|----------|-----------|------------|-------|
| 1 | | FE / BE / Infra / Data | [days or points] | — | | |
| 2 | | | | #1 | | |
| 3 | | | | — | | |

**Estimation notes**:
- [Any non-obvious estimate that needs explanation]

---

## Critical Path

> **Note — Critical Path**: The sequence of dependent tasks that determines the earliest possible completion date. Any task NOT on the critical path has "float" — it can slip by some amount without affecting the delivery date, useful for prioritization.

> 💡 **Tip**: *[Your AI will identify the critical path through your task breakdown and flag which tasks carry the highest schedule risk given their estimates and dependencies.]*

*The sequence of dependent tasks that determines earliest possible completion.*

```
Task 1 (3d) → Task 3 (2d) → Task 6 (1d) → QA (2d) → Done
```

**Critical path total**: [N days]

---

## Blockers (must resolve before work can start)

> **Note — Blockers**: A blocker not resolved before its due date should immediately trigger replanning — can the team start on non-blocked tasks while waiting? Does the timeline need to shift?

| Blocker | Owner | Due | Status |
|---------|-------|-----|--------|
| [Design assets needed] | | | |
| [API keys / credentials] | | | |
| [Platform / infra decision] | | | |

---

## Sprint Allocation

> **Note — Sprint Allocation**: Plan at 70% capacity — not 100%. Meetings, code review, debugging, and unexpected questions consume the rest. A plan at 100% is a plan that will slip.

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

> **Note — Milestones**: Each milestone has a specific, testable definition — "API complete + tested" means integration tests are passing, not that code has been written. Frontend can't build the UI until the API is complete and tested.

| Milestone | Target date | Definition |
|-----------|------------|------------|
| API complete + tested | | All endpoints functional, integration tests passing |
| Feature complete in staging | | All tasks done, feature flag on in staging |
| QA sign-off | | All acceptance criteria verified |
| Ready for release | | Rollback plan confirmed, monitoring in place |

---

## Risks to the Plan

> **Note — Risks to the Plan**: Specific threats to the delivery timeline, not general technical risks. For technical unknowns, schedule an explicit time-boxed spike in Sprint 1 rather than discovering mid-sprint that an unknown is blocking progress.

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| [Dependency slips] | H/M/L | H/M/L | |
| [Scope creep] | H/M/L | H/M/L | Strict change control via PRD owner |
| [Technical unknown] | H/M/L | H/M/L | Time-boxed spike in Sprint 1 |

---

## Definition of Done

> **Note — Definition of Done**: Prevents the "I finished the code but..." conversation. The most commonly missed items are analytics instrumentation (features ship without data to measure success) and rollback procedure (teams discover they can't roll back safely only after they need to).

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

> **Note — Open Questions**: By the time the dev plan is written, most technical questions should be resolved. Remaining questions are typically scope, team availability, or external dependencies — all need an owner and a deadline.

| Question | Owner | Due | Status |
|----------|-------|-----|--------|
| | | | |
