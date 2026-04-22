# Usability Test Plan: [Feature / Flow Name]

**Author**: [Name]
**Date**: [Date]
**Design version**: [Link]
**Test type**: Moderated remote | Moderated in-person | Unmoderated remote
**Target test dates**: [Date range]

> **Learning note — Usability Test Plan**
> - **Why**: Answers questions internal review can't — do users understand the design, can they complete tasks, and where do they get confused?
> - **Who uses it**: PM makes scope and design decisions with user evidence; Designers fix specific UX problems before launch; Leadership reduces launch risk on high-stakes features
> - **Key decisions**: Which test findings require a redesign vs. confirm the design is ready to ship?
> - **Next step**: Test findings → prioritized design fixes → updated handoff or sign-off for launch

---

## Test Objectives

> **Note — Test Objectives**: Well-defined objectives make findings actionable. Each objective should map to a specific decision: "Can users find the filter?" tells the Designer whether to make it more discoverable. If no decision changes based on the findings, the test isn't worth running.

*What specific questions must this test answer? What decisions depend on the results?*

1. Can users successfully [complete primary task] without assistance?
2. Do users understand [key concept or label]?
3. Where do users hesitate or make errors in [specific flow]?

---

## Participant Criteria

> **Note — Participant Criteria**: Research with the wrong participants produces misleading findings. Key discipline: the "must not have" criteria are as important as the "must have" — participants with deep familiarity often compensate for usability problems that would block a real user.

**Number of participants**: [N per persona; typically 5 for qualitative]

### Primary Persona
- **Role / profile**: [e.g., marketing manager at a mid-size company]
- **Experience level**: [e.g., intermediate SaaS user; has used similar tools]
- **Must have**: [Screener criteria — required characteristics]
- **Must not have**: [Exclusion criteria]

### Secondary Persona (if applicable)
- **Role / profile**:
- **Must have**:

### Screener Questions

> **Note — Screener Questions**: Determine who gets invited — the filter between general population and participants who represent your target users. Accept/reject criteria must be defined before recruiting begins. Most common mistake: not screening for specific context of use.

1. [Question] → Accept if: [answer] / Reject if: [answer]
2. [Question] → Accept if: / Reject if:
3. [Question] → Accept if: / Reject if:

---

## Tasks & Scenarios

> **Note — Tasks & Scenarios**: Where the research produces its most important findings. Key discipline: write tasks as user goals in natural language ("find a way to export your data"), not as instructions ("click Export") — the latter tests whether users can follow instructions, not whether the design is intuitive.

*Write tasks as realistic goals in user language — not instructions to click buttons.*

---

### Task 1: [Task Name]

**Scenario**: *"Imagine you [context]. You want to [goal]. Please show me how you would do that."*

**Starting state**: [Screen or URL the participant starts from; any pre-loaded data]

**Task complete when**: [Observable behavior — what does success look like?]

**Success metrics**:
- Task completion rate target: [e.g., ≥80%]
- Time on task: [acceptable range]
- Single Ease Question (SEQ) target: [e.g., ≥5/7]

---

*(Repeat for each task, 3–7 total)*

---

## Discussion Guide

> **Note — Discussion Guide**: Structures the session so every participant covers the same ground — making findings comparable. Key technique: the think-aloud prompt is the most important research method in usability testing — narrating thoughts reveals the mental model, not just what users click.

### Warm-Up (5 min)
- Tell me a bit about your role and how you typically [relevant activity].
- How often do you [relevant behavior]?
- What tools do you currently use for [relevant task]?

### Think-Aloud Prompt (use throughout tasks)
*"As you work through this, please narrate what you're thinking and what you're looking for."*

### Per-Task Probes (use after each task)
- What did you expect to happen when you [action]?
- Was there anything confusing or surprising?
- How would you rate the ease of that task on a scale of 1–7, where 1 is very difficult and 7 is very easy?

### Post-Session Debrief (10 min)
- Overall, what stood out to you — positive or negative?
- Was there anything you expected to find that you couldn't?
- If you could change one thing about what you saw today, what would it be?

---

## Success Thresholds

> **Note — Success Thresholds**: Converts subjective observation into objective evaluation — defines before the sessions what result would trigger a redesign vs. confirm readiness to ship. Without thresholds defined upfront, teams argue about whether 60% task completion is "good enough" after the data is in.

> 💡 **Tip**: *[Your AI will suggest appropriate success thresholds based on your feature type, user sophistication level, and the stakes of the user flow being tested.]*

| Metric | Target | Trigger redesign if |
|--------|--------|-------------------|
| Task 1 completion rate | ≥ 80% | < 60% |
| Task 2 completion rate | ≥ 80% | < 60% |
| Average SEQ score | ≥ 5/7 | < 4/7 |
| Critical errors | 0 | Any P0 blocker found |

---

## Analysis Approach

> **Note — Analysis Approach**: Ensures findings are synthesized into actionable recommendations, not just interesting observations. Key principle: define the output format upfront — a 5-slide summary is often more useful than a 50-page report. Turnaround should be fast — insights lose value as memory fades.

- **Session notes**: [Observation sheet / rainbow spreadsheet / etc.]
- **Synthesis method**: [Affinity mapping / frequency count / severity grid]
- **Output**: [Findings report / presentation / Jira tickets]
- **Turnaround**: [Days after final session]

---

## Logistics

> **Note — Logistics**: Logistics failures delay research or produce unreliable results — wrong tool, broken prototype, inadequate incentive. Key rule: incentives commensurate with participants' time and expertise attract representative participants; under-incentivized research often doesn't.

| Item | Detail |
|------|--------|
| Recruiting source | [Panel / internal users / etc.] |
| Incentive | [Amount / type] |
| Tool | [Lookback / Maze / UserZoom / Zoom + screen share] |
| Prototype link | [Link] |
| Note-taker | [Name] |
| Observer policy | [Silent observers allowed? In which room/channel?] |
