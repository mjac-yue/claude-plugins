# Cycle Plan: [Round / Cycle] [N] — [Start date] to [End date]

**Project**: [Project name]
**Project phase**: Phase A — PM + Design alignment | Phase B — Tech design | Phase C — Dev build
**Work unit type**: Iteration round (Phase A) | Review round (Phase B) | Sprint / Flow cycle (Phase C)
**Team**: [Names and roles]
**Release plan phase**: [Phase name]
**Build layer**: [Layer name — Phase C only; N/A for Phases A and B]
**Round / Cycle goal**: [One sentence — what does done look like at the end of this round or cycle?]

> **Learning note — Cycle Plan**
> - **Why**: The commitment the team makes at the start of each sprint — defines what will be worked on, in what order, and by whom
> - **Who uses it**: PM verifies work aligns with release plan priorities; Engineering sequences tasks and identifies dependencies before work starts; Stakeholders see what's expected next
> - **Key decisions**: What gets selected for this cycle; what gets explicitly deferred; does the total work fit within available capacity?
> - **Next step**: Cycle complete → retrospective → next cycle plan

---

## Capacity

> **Note — Capacity**: Prevents the most common cycle failure — committing to more work than the team can complete. Key discipline: the 20% buffer is not optional. If teams plan to 100% capacity, any interruption causes the plan to fail.

| Person | Available days | Commitments / absences | Effective capacity |
|--------|---------------|----------------------|-------------------|
| [Name 1] | | | |
| [Name 2] | | | |
| **Team total** | | | |

*Buffer: reserve ~20% for unplanned work, reviews, and coordination.*

---

## Layer Check

> **Note — Layer Check**: Prerequisite gate — verifies work selected for this cycle is buildable, meaning all work it depends on is complete. Selecting Layer 3 work before Layer 2 is stable is one of the most common causes of mid-sprint rework.

*Confirm the current build layer and that all prerequisites are met before selecting work.*

| Prerequisite for Layer [N] | Status |
|---------------------------|--------|
| [Layer N-1 item 1] | Complete / In progress / Blocked |
| [Layer N-1 item 2] | Complete / In progress / Blocked |

**Layer gate status**: Ready to proceed | Blocked — [what must be resolved first]

---

## Selected Work

> **Note — Selected Work**: The cycle's contract — defines what the team commits to completing by the end of the cycle. Items are listed in execution order, not priority order, to make dependencies explicit.

> 💡 **Tip**: *[Your AI will flag any selected items that may be under-estimated, have unresolved dependencies, or push the team over effective capacity.]*

*Items selected for this cycle, in execution order. All items must be from the current or completing layer.*

| # | Work item | Layer | Size | Owner | Depends on | Status |
|---|-----------|-------|------|-------|-----------|--------|
| 1 | | | S/M/L | | — | Not started |
| 2 | | | | | #1 | Not started |
| 3 | | | | | — | Not started |
| 4 | | | | | | Not started |

**Capacity check**: Estimated total [S/M/L total] vs [N] effective days available — [On track / Over capacity — consider descoping #N]

---

## Dependency Check

> **Note — Dependency Check**: Surfaces all within-cycle dependencies so the team can sequence work correctly. A dependency not complete when the dependent task needs to start becomes a blocker that typically costs more time to unblock than the original task takes to complete.

| Item | Depends on | Status | Risk if not resolved |
|------|-----------|--------|---------------------|
| | | Done / In progress / Not started | |

---

## Parallel Workstreams This Cycle

> **Note — Parallel Workstreams**: Allows two team members to work simultaneously on independent tasks, reducing total elapsed time. Key discipline: define the sync point before work begins. The most common mistake is not defining the sync point, leading to integration problems at the end of the cycle.

*For 2-person teams only. Skip this section for solo (Tier 1) projects.*

| [Person 1] | [Person 2] | Sync point |
|-----------|-----------|------------|
| | | |

---

## Deferred Items

> **Note — Deferred Items**: Documenting what was considered and deferred — with the reason — prevents the same items from being debated in every cycle planning session. Items deferred repeatedly may need a scope decision: cut permanently vs. explicitly scheduled.

| Item | Reason deferred | Target cycle |
|------|----------------|-------------|
| | Too large / Dependency not ready / Lower priority | Cycle [N+1] |

---

## Risks This Cycle

> **Note — Cycle Risks**: Specific threats to completing this cycle's work. Most common: a dependency task "in progress" that might not complete in time, a task with unclear requirements that may require additional PM input, and external dependencies outside the team's control. Mitigations should be concrete, not "monitor closely."

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| | H/M/L | H/M/L | |

---

## Definition of Done

> **Note — Definition of Done**: The bar below which work can't be called complete. Prevents the common failure mode of a cycle being "done" with 90% of items complete and 10% "mostly done" — incomplete items carry into the next cycle with unresolved issues.

This cycle is complete when:

- [ ] All selected items meet their acceptance criteria
- [ ] No P0 bugs introduced by cycle work
- [ ] All outputs saved to project folder
- [ ] Blockers escalated or resolved
- [ ] Next cycle's layer prerequisites assessed
