# User Stories: [Feature Name]

**Epic**: [Epic / Initiative Name]  
**Sprint**: [Sprint Number or Date]  
**Created**: [Date]  

> **Learning note — User Stories**
> - **Why**: Atomic units of product work — each story describes one capability from the user's perspective with explicit value
> - **Who uses it**: PM writes them; Engineers size and plan from them; QA uses acceptance criteria as test cases
> - **Key decisions**: Which stories are truly independent and user-testable; which are technical tasks in disguise
> - **Next step**: Stories feed into cycle planning; acceptance criteria become the definition of done in each sprint

---

## Summary
*One sentence describing what this feature enables.*

---

## Stories

> **Note — Story Structure**: Each part of the story format serves a purpose. "As a [persona]" prevents stories for internal convenience. "So that [benefit]" is the most important part — it explains *why*, which helps Engineers make trade-offs and helps PMs evaluate if a story is still needed if requirements change.

---

### Story 1: [Title]

**As a** [persona],  
**I want** [capability],  
**So that** [benefit/value].

**Priority**: P0 | P1 | P2  
**Complexity**: S | M | L | XL  
**Depends on**: [Story # or "none"]

#### Acceptance Criteria

> **Note — Acceptance Criteria**: Turn a user story into a testable commitment. Key discipline: every criterion must be testable by someone who wasn't in the room. If a criterion requires subjective judgment ("it looks good"), it's not specific enough.

> 💡 **Tip**: *[Your AI will flag any acceptance criteria that are ambiguous, untestable, or likely to cause disagreement between PM and QA during sign-off.]*

- **Given** [context], **When** [action], **Then** [expected result]
- **Given** [context], **When** [action], **Then** [expected result]
- **Given** [context], **When** [action], **Then** [expected result]

#### Edge Cases

> **Note — Edge Cases**: The scenarios that break features in production but don't appear in the happy path. Most common: empty states, error states, permission boundaries, and boundary conditions. Undocumented edge cases become bug reports post-launch.

- 
- 

#### Notes / Open Questions
- 

---

### Story 2: [Title]

*(repeat structure above)*

---

## Dependencies Map

> **Note — Dependencies Map**: Stories that depend on others create sequencing constraints. Key decision: does any dependency create a bottleneck on the critical path? If so, it should start first regardless of priority ranking.

```
Story 1 → Story 3 (Story 3 requires Story 1 to be complete)
Story 2 → Story 4
```

---

## Definition of Done (Global)

> **Note — Definition of Done**: The non-negotiable floor below which no story can be called complete. Analytics instrumentation is particularly important — a feature launched without tracking its success metrics can't be evaluated.

- [ ] Feature works as described in acceptance criteria
- [ ] Edge cases handled
- [ ] Analytics events instrumented
- [ ] Accessible (WCAG AA)
- [ ] Mobile-responsive (if applicable)
- [ ] Documentation updated
- [ ] QA sign-off
