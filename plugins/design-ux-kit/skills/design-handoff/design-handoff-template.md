# Design Handoff: [Feature / Screen Name]

**Author**: [Name]
**Date**: [Date]
**Design file**: [Figma / Sketch / XD link]
**Status**: Ready for development | In progress | Needs design revision
**Related PRD**: [Link]
**Related Tech Spec**: [Link]

---

## Summary

*One paragraph: what this feature does, the user problem it solves, and key design decisions engineers need to understand before building.*

---

## Screen Inventory

| # | Screen / State Name | Description | Design file frame |
|---|---------------------|-------------|-------------------|
| 1 | | | |
| 2 | | | |

---

## Screen Specifications

---

### Screen 1: [Screen Name]

**Description**: [Purpose and user goal on this screen]

#### Components

| Component | Type | Label / Copy | Data | Notes |
|-----------|------|-------------|------|-------|
| | Button / Input / Card / etc. | | [API field or static] | |

#### States

| State | Trigger | Visual description | Notes |
|-------|---------|-------------------|-------|
| Default | Page load | | |
| Loading | On data fetch | Skeleton loader / spinner | |
| Empty | No data present | [Empty state copy and illustration] | |
| Error | [API error / validation fail] | [Error message copy] | |
| Success | [Action completed] | [Confirmation copy or transition] | |
| Disabled | [Condition] | [Which elements, opacity/style] | |

#### Interactions

| User action | Trigger condition | Result / transition | Animation |
|-------------|-----------------|---------------------|-----------|
| Click [button] | | Navigates to [screen] | [type, duration] |
| Submit form | | [API call / validation] | |

#### Responsive Behavior

| Breakpoint | Layout changes |
|-----------|---------------|
| Mobile (< 768px) | |
| Tablet (768–1024px) | |
| Desktop (> 1024px) | |

---

*(Repeat Screen Specification block for each screen)*

---

## Design System References

| Component | Status | Notes |
|-----------|--------|-------|
| [Button — Primary] | Existing | Use `btn-primary` token |
| [New component name] | New — needs build | Spec in design file frame [X] |

---

## Accessibility Requirements

| Requirement | Detail |
|------------|--------|
| Focus order | [Describe tab order for keyboard navigation] |
| ARIA roles | [Any custom roles needed beyond semantic HTML] |
| Alt text | [Images and icons that need descriptive text] |
| Color contrast | All text meets 4.5:1; UI elements meet 3:1 |
| Keyboard shortcuts | [Any shortcuts to implement] |
| Reduced motion | [How animations behave with prefers-reduced-motion] |

---

## Acceptance Criteria

*Engineering and QA verify each of these before sign-off.*

- [ ] [Criterion — specific, testable]
- [ ] [Criterion]
- [ ] [Criterion]
- [ ] All interactive elements are reachable and operable by keyboard
- [ ] No WCAG 2.1 AA violations
- [ ] Empty, loading, and error states render correctly
- [ ] Design matches across all specified breakpoints

---

## Assets

| Asset | Format | Location | Notes |
|-------|--------|----------|-------|
| [Icon name] | SVG | [Link / path] | |
| [Illustration] | PNG 2x | [Link / path] | |

---

## Open Questions & Deferred Decisions

| Question | Impact | Owner | Due |
|----------|--------|-------|-----|
| | | | |
