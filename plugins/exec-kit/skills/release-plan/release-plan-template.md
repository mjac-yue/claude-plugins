# Release Plan: [Project Name]

**Author**: [Name]
**Date**: [Date]
**Target launch**: [Date]
**Status**: Draft | Active | Shipped
**Methodology**: Sprints | Flow (Kanban)
**Team**: [Names and roles]
**Related PRD**: [Link]

> **Learning note — Release Plan**
> - **Why**: Master schedule that sequences all project work from discovery through launch — surfaces dependency conflicts before they become blockers
> - **Who uses it**: PM manages dependencies and protects launch date; Engineering plans sprint capacity; Stakeholders see when to expect the product
> - **Key decisions**: Which phases have buffer; which dependencies are on the critical path; when to call a scope cut vs. a timeline slip
> - **Next step**: Approved release plan → kickoff complete; updated at every phase transition and cycle close

---

## Project Overview

> **Note — Project Overview**: Gives any stakeholder the context to evaluate the plan. Key field: "success definition" — if the team can't agree on it at the start, discovery isn't complete and execution shouldn't begin.

**What we're building**: [One sentence]
**Why now**: [Strategic reason or deadline]
**Success definition**: [How we'll know this shipped successfully — tie to PRD metrics]

---

## Phases & Milestones

> **Note — Phases & Milestones**: Top-level schedule — every phase, owner, target date, and gate criteria. Key column: gate criteria — concrete conditions that determine when a phase is complete, not subjective assessment. "PM and Designer mutually sign off" is a gate criterion; "looks good" is not.

> 💡 **Tip**: *[Your AI will highlight which phases carry the most schedule risk given your team size, dependencies, and feature complexity.]*

| Phase | Milestone | Owner | Target date | Status | Gate criteria |
|-------|-----------|-------|-------------|--------|---------------|
| A. PM + Design alignment | PM + Design signed off | PM + Designer | | Not started | PRD finalized, all screens covered, PM and Designer mutually sign off |
| B. Tech design | All three aligned, handoff accepted | Eng + PM + Designer | | Not started | Constraints resolved, PRD and design updated, Eng accepts handoff |
| 1. Infrastructure | Environment live | | | Not started | Deploy pipeline working, auth + DB accessible |
| 2. Foundation | Core data models + base APIs complete | | | Not started | End-to-end auth flow working, CRUD on core entities |
| 3. Core build | All P0 features complete | | | Not started | P0 acceptance criteria met, no blocking bugs |
| 4. Feature build | P1/P2 features complete | | | Not started | QA sign-off on all P1 items |
| 5. QA & hardening | All tests passing | | | Not started | Test plan complete, zero P0/P1 bugs open |
| 6. Launch | Shipped to production | | | Not started | Smoke tests pass, monitoring live, rollback ready |

---

## Alignment Rounds — Phase A (PM + Design)

> **Note — Phase A Alignment Rounds**: Iterative PM → Design → feedback loop. The number of rounds is variable. Key discipline: sign-off gate prevents moving to Engineering prematurely, when changes cost hours of Designer time rather than days of Engineering time.

*Each round is one pass of the PM → Design → feedback loop. Rounds continue until mutual sign-off.*

| Round | PM changes | Design changes | Open questions | Status |
|-------|-----------|----------------|----------------|--------|
| Round 1 | | | | In progress |
| Round 2 | | | | Pending |

**Sign-off status**: PM — Pending | Designer — Pending

**Phase A complete when**: PM and Designer both sign off with no open questions outstanding.

---

## Tech Design Rounds — Phase B

> **Note — Phase B Tech Design Rounds**: Engineering validates that PM + Design outputs are buildable within real system constraints. Key value: constraints found here are orders of magnitude cheaper to resolve than constraints discovered mid-build. Three-way sign-off gate ensures Engineering isn't starting with unresolved concerns.

| Round | Constraints identified | PRD updates needed | Design updates needed | Resolution status |
|-------|----------------------|-------------------|----------------------|------------------|
| Round 1 | | | | Pending |

**Sign-off status**: PM — Pending | Designer — Pending | Eng — Pending

**Phase B complete when**: All constraints resolved, all three parties sign off, Eng accepts design handoff.

---

## Dependency Map

> **Note — Dependency Map**: Visualizes the critical path — the sequence where any delay pushes the launch date. Key insight: feedback loops in Phases A and B are where the most time is saved by running tight, well-scoped rounds rather than open-ended iterations.

```mermaid
flowchart TD
    A([PM drafts PRD]) --> B([Design explores])
    B --> C{Open questions?}
    C -- Yes --> D([Feedback refines PRD])
    D --> E([PRD update refines design])
    E --> C
    C -- No --> F([PM + Design sign off ✓])
    F --> G([Eng tech design])
    G --> H{Constraints?}
    H -- Yes --> I([PM updates PRD\nDesign updates specs])
    I --> H
    H -- No --> J([All three aligned ✓])
    J --> K([Dev can start])
    K --> L([Infrastructure provisioned])
    L --> M([Foundation layer])
    M --> N([Core features P0])
    N --> O([Feature layer P1/P2])
    O --> P([QA & hardening])
    P --> Q([🚀 Launch])
```

### Unresolved Dependencies

| Dependency | Blocked work | Owner | Due | Status |
|-----------|-------------|-------|-----|--------|
| | | | | |

---

## Build Sequence

> **Note — Build Sequence**: Orders development work so each layer is stable before the next begins — prevents building feature code on top of an unstable foundation, which leads to expensive rewrites. Key insight: PM uses layer structure to understand what can be descoped if timelines slip (P2 in Layer 4 can often be deferred; foundation work in Layer 2 cannot).

*Work must be completed in layer order. Do not start a layer until the previous layer is stable.*

---

### PM Layer — Discovery & Requirements

> **Note — PM Layer**: Where requirements are shaped before any design or engineering investment. Key principle: a rushed PM layer produces a vague PRD that Design and Engineering can't execute against, leading to expensive corrections later.

- [ ] Problem framing and assumptions documented
- [ ] Competitive landscape assessed
- [ ] PRD drafted — problem, goals, user stories, P0/P1/P2 requirements
- [ ] Success metrics defined
- [ ] Scope boundaries set (in scope / out of scope / deferred)
- [ ] RICE or MoSCoW prioritization complete

**PM Layer complete when**: Initial PRD is ready for Design to start exploring — not finalized, ready for first round.

---

### Design Layer — Exploration & Alignment

> **Note — Design Layer**: Runs iteratively with the PM layer until both parties agree the design is ready for Engineering to review. Key principle: every problem caught here saves 5–10× the effort in Engineering. The sign-off gate is two-way — PM signs off on design quality, Designer signs off on requirement completeness.

- [ ] UX brief produced (user goals, flows, constraints)
- [ ] Key screens wireframed (all P0 flows covered)
- [ ] Design feedback incorporated into PRD (per round)
- [ ] PRD updates incorporated into design (per round)
- [ ] All P0 screens with acceptance criteria
- [ ] Design review complete — usability, accessibility, edge cases
- [ ] Design handoff doc prepared

**Design Layer complete when**: PM and Designer mutually sign off — PRD is final, all screens covered, no open questions.

---

### Tech Design Layer — Constraint Resolution

> **Note — Tech Design Layer**: Engineering's first formal engagement with PM and Design outputs. Key value: prevents Engineering from starting development only to discover a key requirement is infeasible — one of the most expensive types of mid-sprint discovery.

- [ ] Eng reviews PRD and design handoff
- [ ] Technical constraints identified and documented
- [ ] Architecture or implementation approach proposed
- [ ] Constraint feedback incorporated into PRD (per round)
- [ ] Constraint feedback incorporated into design (per round)
- [ ] Eng accepts final design handoff
- [ ] Tech spec or dev plan drafted (if required by tier)

**Tech Design Layer complete when**: All constraints resolved, all three parties sign off, Eng is unblocked to start dev.

---

### Layer 1 — Infrastructure

> **Note — Layer 1 Infrastructure**: Foundation everything else runs on — no feature code should be written before the deploy pipeline is working, the database is accessible, and auth is configured. Specific technology choices are determined in Phase B and filled in after.

- [ ] Hosting environment provisioned — *[TBD in Phase B]*
- [ ] Database provisioned and accessible — *[TBD in Phase B]*
- [ ] Auth system configured — *[TBD in Phase B]*
- [ ] CI/CD pipeline working (commit → test → deploy) — *[TBD in Phase B]*
- [ ] Environment variables and secrets configured
- [ ] Domain and DNS set up (if applicable)
- [ ] Error tracking configured — *[TBD in Phase B]*

**Layer 1 complete when**: A commit to main deploys to production without manual steps.

---

### Layer 2 — Foundation

> **Note — Layer 2 Foundation**: Core data models, auth flows, and base APIs that all feature code builds on. Key discipline: starting feature code before the foundation is stable leads to expensive refactoring when the data model needs to change.

- [ ] [Entity 1] — data model + CRUD endpoints
- [ ] [Entity 2] — data model + CRUD endpoints
- [ ] Authentication — sign up, login, session management
- [ ] Authorization — roles and permissions model
- [ ] Base API structure and error handling conventions

**Layer 2 complete when**: A user can sign up, log in, and the core data models are readable and writable end-to-end.

---

### Layer 3 — Core Features (P0)

> **Note — Layer 3 Core Features**: The P0 requirements — the things without which the product doesn't solve the user problem. Key discipline: if a P0 feature is proving more complex than estimated, either extend the timeline or escalate the scope decision to the PM — don't quietly reduce quality.

- [ ] [Feature 1] — [one-line description]
- [ ] [Feature 2] — [one-line description]
- [ ] [Feature 3] — [one-line description]

**Layer 3 complete when**: All P0 acceptance criteria are met and verified.

---

### Layer 4 — Feature Layer (P1/P2)

> **Note — Layer 4 Features**: P1/P2 features add significant value but aren't launch-blocking — they can be deferred if timeline is at risk. Key discipline: resist shipping P1 features in a degraded state to hit the date — a partial feature often creates more support burden than deferring it entirely.

- [ ] [Feature 4] — [one-line description]
- [ ] [Feature 5] — [one-line description]

**Layer 4 complete when**: All P1 acceptance criteria met; P2 items assessed for inclusion or deferral.

---

### Layer 5 — Integration & Polish

> **Note — Layer 5 Integration & Polish**: Error states, empty states, and loading states live here — what users encounter when things don't go perfectly. Key insight: these often differentiate a product that gets recommended from one that generates support tickets.

- [ ] [Integration 1] — [service and purpose]
- [ ] Error states and empty states for all flows
- [ ] Loading states and feedback
- [ ] Performance optimisation (if SLO targets are at risk)

**Layer 5 complete when**: All integration acceptance criteria met, no unhandled error states.

---

### Layer 6 — QA & Launch

> **Note — Layer 6 QA & Launch**: Final gate before real users interact with the product. Key rule: a rollback plan that isn't tested before launch is not a rollback plan.

- [ ] Test plan execution complete
- [ ] All P0/P1 bugs resolved
- [ ] Smoke test checklist passing in production environment
- [ ] Monitoring and alerting live
- [ ] Rollback procedure documented and tested
- [ ] Launch communications prepared

---

## Critical Path

> **Note — Critical Path**: The sequence where any delay pushes the launch date. Key signal: the "highest current risk" field should be updated at every status report — if the answer is always "nothing," the critical path isn't being monitored carefully enough.

**Path**: Phase A sign-off → Phase B sign-off → [Layer 1] → [Layer 2] → [Layer 3] → Launch

**Highest current risk on critical path**: [What's most likely to slip and why]

---

## Parallel Workstreams

> **Note — Parallel Workstreams**: Reduce total elapsed time by enabling team members to work simultaneously on independent tasks. Key discipline: plan the sync point before the workstreams start, not after — integration problems discovered at merge are the most expensive type of rework.

| Phase / Cycle | [Person 1] | [Person 2] | Sync point |
|--------------|-----------|-----------|------------|
| Phase A (rounds) | PRD refinement | Screen exploration | End of each round |
| Phase B | PRD/design updates | Tech design review | Constraint resolution |
| Layer 1–2 | | | |

---

## Go / No-Go Criteria

> **Note — Go / No-Go Criteria**: Objective conditions that must be true before each phase transition. Key principle: a phase gate that passes on time but with criteria unmet almost always creates more delay downstream than simply waiting for readiness.

> 💡 **Tip**: *[Your AI will flag which gate criteria are most likely to be incomplete given your current project state and highlight where to focus to stay on track.]*

| Phase gate | Must be true to proceed |
|-----------|------------------------|
| PM Layer → Design starts | Initial PRD drafted; problem, goals, and P0 requirements clear enough for design to explore |
| Design Layer → Phase A complete | PM and Designer both sign off; PRD finalized; all P0 screens covered with acceptance criteria; no open questions |
| Phase A → Tech Design | PM + Design sign-off confirmed; design handoff doc prepared |
| Tech Design → Dev | All constraints resolved; all three sign off; Eng accepts handoff; tech spec complete (if required) |
| Infrastructure → Foundation | Deploy pipeline working end-to-end; no manual steps to ship |
| Foundation → Core build | Auth works end-to-end; core data models stable (no planned schema changes) |
| Core build → QA | All P0 acceptance criteria met; no P0 bugs open |
| QA → Launch | Test plan complete; zero P0/P1 bugs; rollback plan tested; monitoring live |

---

## Risk Checkpoints

> **Note — Risk Checkpoints**: Scheduled moments to proactively review what could go wrong. Key checkpoint: mid-build (halfway through Layer 3) — last moment to descope P1 features before they're partially built, which makes descoping more expensive.

| Checkpoint | When | What to review |
|-----------|------|---------------|
| After PM Layer | Before Design starts | Is the problem well-defined? Is scope realistic? Are key assumptions documented? |
| End of Phase A round 2+ | If iterations are continuing | Are PM and Design converging? Is scope creeping? Set a round limit if needed. |
| Phase A complete | Before Tech Design starts | Is the design handoff doc complete? Are all acceptance criteria written? |
| End of Phase B | Before dev starts | Are all constraints resolved? Is the scope still achievable in the timeline? Any P2 to cut? |
| Mid-build | Halfway through Layer 3 | Is velocity on track? Any features to descope or defer? |
| Pre-QA | Entering Layer 6 | Any unresolved P1 bugs that could block launch? |
| Launch minus 1 week | 7 days before target | Is every item on the launch readiness checklist green? |

---

## Launch Readiness Checklist

> **Note — Launch Readiness Checklist**: Final gate before launch. Most commonly skipped items that cause the most painful incidents: rollback procedure not tested, monitoring not configured, and analytics not instrumented.

**Product**
- [ ] All P0 acceptance criteria met and verified
- [ ] All P1 acceptance criteria met (or deferral documented)
- [ ] No open P0 or P1 bugs
- [ ] Smoke tests passing in production

**Infrastructure**
- [ ] Error tracking live (errors flowing to dashboard)
- [ ] Uptime monitoring configured
- [ ] Alerts set for SLO violations
- [ ] Rollback procedure documented and tested
- [ ] Backups configured (if applicable)

**Communications**
- [ ] Internal team announcement ready
- [ ] Customer-facing announcement ready (if applicable)
- [ ] Support team briefed with FAQ
- [ ] Stakeholders notified of launch date

**Analytics**
- [ ] Success metrics instrumented (from PRD)
- [ ] Baseline measurements captured for comparison

---

## Open Questions

> **Note — Open Questions**: Represent risks to the timeline — decisions that if resolved differently could change the plan. Questions open for more than one week without progress should be escalated — waiting is often a sign the wrong person owns the question.

| Question | Owner | Due | Status |
|----------|-------|-----|--------|
| | | | |
