# Design Handoff: [Feature / Screen Name]

**Author**: [Name]
**Date**: [Date]
**Design file**: [Figma / Sketch / XD link]
**Status**: Ready for development | In progress | Needs design revision
**Related PRD**: [Link]
**Related Tech Spec**: [Link]

> **Learning note — Design Handoff**
> - **Why**: The bridge between design and engineering — enables Engineers to build accurately without a daily sync with the Designer
> - **Who uses it**: PM verifies acceptance criteria are testable before dev starts; QA uses acceptance criteria as test cases; Engineers build without interpretation
> - **Key decisions**: Is every component, state, interaction, and responsive behavior specified completely enough that an Engineer can build without asking questions?
> - **Next step**: Handoff accepted by Engineering → development begins → QA verifies against acceptance criteria

---

## Summary

> **Note — Summary**: Gives Engineers context for *why* the design looks the way it does. Without this, Engineers optimize for technical convenience rather than user outcomes. Key test: if an Engineer reads this summary and then makes a design decision, will they make the same decision the Designer would?

*One paragraph: what this feature does, the user problem it solves, and key design decisions engineers need to understand before building.*

---

## Screen Inventory

> **Note — Screen Inventory**: Complete list of everything that needs to be built — the scope document for the engineering sprint. Most commonly missing: edge case screens (empty state, permission-denied) and mobile-specific layouts that differ from desktop.

| # | Screen / State Name | Description | Design file frame |
|---|---------------------|-------------|-------------------|
| 1 | | | |
| 2 | | | |

---

## Screen Specifications

> **Note — Screen Specifications**: The contract between Design and Engineering for each screen. Key principle: the level of detail here determines how accurately the final implementation matches the design. More detail = fewer design-intent violations.

---

### Screen 1: [Screen Name]

**Description**: [Purpose and user goal on this screen]

#### Components

> **Note — Components**: Ensures every UI element is built as specified. Most important note: whether a component is from the existing design system (reuse) or is new (build from scratch and potentially add to the design system).

| Component | Type | Label / Copy | Data | Notes |
|-----------|------|-------------|------|-------|
| | Button / Input / Card / etc. | | [API field or static] | |

#### States

> **Note — States**: Most important part of the handoff — states are where implementation bugs live. Key discipline: Engineers frequently build the default state correctly and implement loading, empty, and error states inconsistently because they weren't specified.

> 💡 **Tip**: *[Your AI will flag which states are most likely to be overlooked for this type of screen and which have the highest risk of being implemented incorrectly without explicit specification.]*

| State | Trigger | Visual description | Notes |
|-------|---------|-------------------|-------|
| Default | Page load | | |
| Loading | On data fetch | Skeleton loader / spinner | |
| Empty | No data present | [Empty state copy and illustration] | |
| Error | [API error / validation fail] | [Error message copy] | |
| Success | [Action completed] | [Confirmation copy or transition] | |
| Disabled | [Condition] | [Which elements, opacity/style] | |

#### Interactions

> **Note — Interactions**: Most commonly under-specified aspect of handoffs. "Clicking a button navigates to the next screen" is insufficient — Engineers also need: is there a transition animation, does the button become disabled while in-flight, what happens if the action fails?

| User action | Trigger condition | Result / transition | Animation |
|-------------|-----------------|---------------------|-----------|
| Click [button] | | Navigates to [screen] | [type, duration] |
| Submit form | | [API call / validation] | |

#### Responsive Behavior

> **Note — Responsive Behavior**: Must be specified for every breakpoint where the layout changes. Most common responsive failure: assuming desktop layouts can be compressed to mobile without redesigning the information hierarchy.

| Breakpoint | Layout changes |
|-----------|---------------|
| Mobile (< 768px) | |
| Tablet (768–1024px) | |
| Desktop (> 1024px) | |

---

*(Repeat Screen Specification block for each screen)*

---

## Design System References

> **Note — Design System References**: Prevents Engineers from building custom implementations of components that already exist. Key note for PMs: "new component" items require additional Engineering time beyond the feature work itself.

| Component | Status | Notes |
|-----------|--------|-------|
| [Button — Primary] | Existing | Use `btn-primary` token |
| [New component name] | New — needs build | Spec in design file frame [X] |

---

## Accessibility Requirements

> **Note — Accessibility Requirements**: Ensures Engineers build an accessible implementation, not just a visually matching one. Most commonly forgotten: reduced motion specification for users with vestibular disorders.

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

> **Note — Acceptance Criteria**: Testable statements that define when the implementation correctly matches the design. Key discipline: each criterion should be specific enough that two people testing independently reach the same pass/fail. "The button looks correct" fails this test; "The Submit button is disabled until all required fields are filled" passes it.

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

> **Note — Assets**: Prevents Engineering from using placeholder or incorrect assets in the shipped product. If assets aren't ready before development starts, list what's expected and by when.

| Asset | Format | Location | Notes |
|-------|--------|----------|-------|
| [Icon name] | SVG | [Link / path] | |
| [Illustration] | PNG 2x | [Link / path] | |

---

## Open Questions & Deferred Decisions

> **Note — Open Questions**: Questions still open at handoff must be resolved before Engineering builds the affected component. Deferred decisions are design choices intentionally left to Engineering to implement. Questions not resolved within the first sprint become blockers or inconsistent design decisions made in isolation.

| Question | Impact | Owner | Due |
|----------|--------|-------|-----|
| | | | |
