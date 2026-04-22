# Project Kickoff: [Project Name]

**Date**: [Date]
**Author**: [Name]
**Team**: [Names and roles]
**Related PRD**: [Link]
**Related design brief**: [Link]

> **Learning note — Project Kickoff**
> - **Why**: Creates a shared starting point — everyone aligns on what's being built, why, and how the team will work together before any work begins
> - **Who uses it**: PM transfers context from discovery to delivery; Engineers understand scope and constraints; Designers understand timeline and working rhythm
> - **Key decisions**: Who decides scope changes, technical approach, and what gets escalated — teams that skip this answer these questions one at a time for weeks
> - **Next step**: Kickoff complete → release plan, which sequences this alignment into an execution schedule

---

## What We're Building

> **Note — What We're Building**: Shared one-glance answer to the most fundamental question. "Why now" is particularly important — if the team understands the strategic reason or deadline, they make better judgment calls when trade-offs arise mid-project.

**Problem**: [One sentence from the PRD problem statement]
**Solution**: [One sentence — what we're shipping]
**Why now**: [Strategic reason or deadline]

---

## Success Definition

> **Note — Success Definition**: Shared target that survives the inevitable scope and timeline pressures of delivery. Key discipline: "users are happy" is not a success definition; "30% of new users complete onboarding without contacting support" is.

**We will know this project succeeded when**:
1. [Metric or observable outcome from PRD success metrics]
2. [Metric or observable outcome]
3. [Metric or observable outcome]

**Launch definition**: [What "shipped" means — beta users, full rollout, internal only, etc.]

---

## Scope

> **Note — Scope**: Protects the team's capacity and the launch date. When scope creep happens (and it will), this section is the reference for what was agreed at the start. "Deferred to v1.1" acknowledges good ideas explicitly postponed — reducing the political cost of not including them now.

### In scope

-
-
-

### Out of scope

*Explicit boundaries to prevent scope creep.*

-
-
-

### Deferred to v1.1

-
-

---

## Team & Roles

> **Note — Team & Roles**: Prevents duplication and gaps. Key column: "Decision authority" — defines who makes the final call when there's disagreement, preventing circular discussions. Unclear lines cause small decisions to be escalated to stakeholders who shouldn't need to be involved.

| Person | Role | Responsibilities | Decision authority |
|--------|------|-----------------|-------------------|
| [Name 1] | [Title] | | |
| [Name 2] | [Title] | | |

---

## Working Rhythm

> **Note — Working Rhythm**: Defines operating cadence — how often the team checks in, how work is reviewed, how status is communicated. Key choice: async vs. synchronous standup. Async is better for distributed teams and solo builders. A consistent rhythm makes blockers visible faster than ad-hoc check-ins.

**Methodology**: Sprints ([N]-day) | Flow (Kanban)
**Cycle cadence**: [Weekly / fortnightly]
**Standup**: [Async written / Sync call] — [Time / frequency]
**Retrospective**: End of each cycle — [Format: Start/Stop/Continue]
**Status report**: [Weekly / fortnightly] to [audience]

---

## Decision Making

> **Note — Decision Making**: Prevents the team from relitigating the same choices repeatedly or escalating decisions that should be made at team level. Key question: what's the escalation path when there's disagreement and no one knows who should make the final call?

> 💡 **Tip**: *[Your AI will flag any decision-making ambiguities that are likely to cause friction given your team composition and project scope.]*

**Who decides product scope changes**: [Name]
**Who decides technical approach**: [Name]
**Who decides to defer a feature**: [Name] — with [Name]'s input
**Escalation path**: [What gets escalated and to whom]

**Decision log**: [Where decisions are recorded — e.g., project folder DECISIONS.md]

---

## Communication Norms

> **Note — Communication Norms**: Prevents mismatched expectations — one person expecting same-day Slack responses while another checks messages once a day. Key rule: document decisions made in any sync conversation — verbal agreements are invisible to team members who weren't present.

| Channel | Used for | Response expectation |
|---------|---------|---------------------|
| [Slack / Teams / etc.] | Day-to-day questions, blockers | [Same day / 4 hours] |
| [Email / async doc] | Status updates, decisions | [24 hours] |
| [Sync call] | Blockers that can't be resolved async | [As needed] |

---

## Key Dependencies & External Contacts

> **Note — Key Dependencies**: Most common source of unexpected delays. Key question for each dependency: what's the latest date we need this before it delays our launch? If the answer is "we needed it yesterday," escalate immediately.

| Dependency | Type | Contact | Notes |
|-----------|------|---------|-------|
| | Design asset / API / Stakeholder approval / Tool access | | |

---

## Project Folder Structure

> **Note — Project Folder Structure**: Ensures outputs from each workflow are saved consistently and found without asking. Correct setup at kickoff means zero time spent at the end of each phase asking "where did you save that?"

```
[project-name]/
├── CLAUDE.md              — auto-save instructions for Claude Code
├── discovery/
│   ├── prd.md
│   └── brief.md
├── design/
│   ├── ux-brief.md
│   ├── wireframe-spec.md
│   └── design-handoff.md
├── execution/
│   ├── release-plan.md
│   ├── risk-register.md
│   └── cycles/
│       ├── cycle-01.md
│       └── retro-01.md
├── dev/
│   ├── tech-spec.md
│   ├── api-spec.md
│   └── dev-plan.md
└── launch/
    ├── status-reports/
    └── rollout.md
```

---

## Open Questions at Kickoff

> **Note — Open Questions at Kickoff**: Normal — the kickoff identifies ambiguity, it doesn't resolve all of it. Every question needs an owner and a due date. The number of unresolved questions is a signal of how much discovery work remains before the team can execute with confidence.

| Question | Owner | Due |
|----------|-------|-----|
| | | |
