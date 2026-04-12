---
name: design-handoff
description: Generate a design handoff specification for engineering — component inventory, interaction specs, states, and acceptance criteria. Use to hand off a finalized design to developers.
disable-model-invocation: true
---

Generate a design handoff spec for: $ARGUMENTS

Use the template in [design-handoff-template.md](design-handoff-template.md) as the structure.

Follow this process:
1. **Summarize the design** — one paragraph describing the feature, the user problem it solves, and any key design decisions engineers need to understand.
2. **Screen inventory** — list every screen/state being handed off with a brief description of its purpose.
3. **For each screen**, document:
   - **Components** — every UI element, its label, placeholder text, and data source
   - **States** — all visual states (default, hover, focus, active, disabled, loading, empty, error, success)
   - **Interactions** — what happens on user actions (click, tap, swipe, keyboard shortcut)
   - **Transitions** — animation type, duration, and trigger for any motion between states or screens
   - **Responsive behavior** — how layout adapts across breakpoints
4. **Design system references** — which existing components, tokens, or styles are being reused vs. new
5. **Accessibility requirements** — ARIA roles, focus order, keyboard shortcuts, alt text, contrast specifications
6. **Acceptance criteria** — a testable checklist engineers and QA can use to verify the implementation matches the design
7. **Assets** — list of any icons, images, or illustrations needed and their sources
8. **Open questions** — decisions deferred to engineering, and anything that needs a follow-up before or during implementation

Output a spec detailed enough that engineering can build without a sync meeting.

## Save output

After presenting the design handoff spec to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/design-handoff` and save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. Confirm the file was written to the user
5. If no project `CLAUDE.md` exists, present the output for manual copying
