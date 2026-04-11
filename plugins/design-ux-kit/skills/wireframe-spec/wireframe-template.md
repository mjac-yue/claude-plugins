# Wireframe Spec: [Feature / Flow Name]

**Author**: [Name]
**Date**: [Date]
**Status**: Draft | In Review | Approved
**Related UX Brief**: [Link]
**Related PRD**: [Link]

---

## User Flow Overview

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

| # | Screen Name | Purpose | Notes |
|---|------------|---------|-------|
| 1 | | | |
| 2 | | | |
| 3 | | | |

---

## Screen Specifications

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

| Scenario | How it's handled |
|----------|----------------|
| User has no existing data | |
| Session expires mid-flow | |
| Network error during submission | |
| [Other edge case] | |

---

## Open Design Questions

| Question | Impact | Owner | Due |
|----------|--------|-------|-----|
| | | | |
