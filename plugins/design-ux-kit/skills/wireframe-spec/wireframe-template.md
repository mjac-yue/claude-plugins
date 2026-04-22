# Wireframe Spec: [Feature / Flow Name]

**Author**: [Name]
**Date**: [Date]
**Status**: Draft | In Review | Approved
**Related UX Brief**: [Link]
**Related PRD**: [Link]

> **Learning note — Wireframe Specification**
> - **Why**: Design blueprint — describes every screen, flow, component, and state in structured text before any visual design begins
> - **Who uses it**: Designers align on scope before spending time on visuals; Engineers estimate complexity; PMs verify every P0 user story maps to a screen
> - **Key decisions**: Is every required screen and state covered? Are error paths as well-specified as happy paths?
> - **Next step**: Approved wireframe spec → design review → visual design → design handoff

---

## User Flow Overview

> **Note — User Flow Overview**: Maps the complete journey from entry to exit before any individual screen is specified. Most valuable part: the error path — error flows are where most UX problems live, and they're usually underspecified in early design.

*Numbered sequence of the complete flow from entry to exit.*

```
[Entry point] → [Step 1] → [Step 2] → [Step 3] → [Exit / Success state]
                                ↓
                         [Error path] → [Recovery]
```

**Entry points**: [How/where users arrive at this flow]
**Exit points**: [Successful completion, abandonment, error exit]

---

## Screen Inventory

> **Note — Screen Inventory**: The scope document for the design — names every distinct screen or state that needs to be designed. Most common omissions: edge case screens (empty states, error screens, permission-denied states). If a screen isn't on this list, it won't get designed.

| # | Screen Name | Purpose | Notes |
|---|------------|---------|-------|
| 1 | | | |
| 2 | | | |
| 3 | | | |

---

## Screen Specifications

> **Note — Screen Specifications**: Each screen spec is the reference document design and engineering both build from. Most important discipline: specify all states (not just the default) — empty, loading, error, and success states catch the most bugs in production.

---

### Screen 1: [Screen Name]

**Purpose**: [What the user is trying to accomplish on this screen]

**Layout Zones**:
- Header: [contents]
- Navigation: [contents]
- Primary content area: [contents]
- Secondary / sidebar: [contents]
- Footer: [contents]

**Component Inventory**:

| Component | Type | Label / Content | Data Source | Notes |
|-----------|------|----------------|-------------|-------|
| | Input / Button / Card / Label / etc. | | | |

**States**:

> **Note — States**: Every component can exist in multiple states, and failing to specify them is the most common source of post-launch UI bugs. Missing states become inconsistent UI patterns implemented without design guidance.

> 💡 **Tip**: *[Your AI will identify which states are most commonly missing for this type of screen and flag any that could cause usability problems for your target users.]*

- **Default**: [Description]
- **Loading**: [What appears while data fetches]
- **Empty state**: [What appears when there is no data]
- **Error state**: [Error message text, recovery action]
- **Success state**: [Confirmation message or transition]
- **Disabled**: [Which elements are disabled and when]

**Actions**:

| User Action | Result / Next Screen | Notes |
|-------------|---------------------|-------|
| Clicks [X] | Navigates to Screen [N] | |
| Submits form | Triggers [validation / API call / etc.] | |

**Interaction Behaviors**:
- [Field validation: when triggered, error message format]
- [Hover/focus states]
- [Keyboard shortcuts]

---

*(Repeat Screen Specification block for each screen)*

---

## Edge Cases & Branching Paths

> **Note — Edge Cases & Branching Paths**: The scenarios that appear in support tickets because the design didn't account for them. Most common: user has no data, session expires mid-flow, network error during submission. Undocumented edge cases become P1 bugs post-launch.

| Scenario | How it's handled |
|----------|----------------|
| User has no existing data | |
| Session expires mid-flow | |
| Network error during submission | |
| [Other edge case] | |

---

## Open Design Questions

> **Note — Open Design Questions**: Decisions that could change the spec — need input before visual design begins. A question still open when the spec is reviewed for approval is a signal the spec isn't ready to move forward.

| Question | Impact | Owner | Due |
|----------|--------|-------|-----|
| | | | |
