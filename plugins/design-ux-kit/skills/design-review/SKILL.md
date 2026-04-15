---
name: design-review
description: Review a design, wireframe, or prototype against UX heuristics and accessibility guidelines. Use to catch usability problems before visual design or development begins.
disable-model-invocation: true
---

Review this design: $ARGUMENTS

> **Learning note — Design Review**
> A design review evaluates a wireframe or prototype against established usability principles and accessibility standards before engineering begins. Nielsen's 10 heuristics capture decades of research about what makes interfaces intuitive, and WCAG 2.1 AA defines the minimum accessibility bar for most products. Catching usability problems and accessibility violations at this stage — rather than after the product is built — is dramatically cheaper in both time and user trust. A finding in a design review takes minutes to fix; the same issue in production can take weeks.

**Output standard — tables**: All documents are read in Obsidian. Always include a blank line before any Markdown table — Obsidian requires this to render `|` syntax as a table rather than plain text.

Use the template in [design-review-template.md](design-review-template.md) as the structure.

Follow this process:
1. **Understand the context** — what is the user trying to accomplish? Who are they? What platform/device?
2. **Evaluate against Nielsen's 10 Usability Heuristics**:
   1. Visibility of system status
   2. Match between system and real world
   3. User control and freedom
   4. Consistency and standards
   5. Error prevention
   6. Recognition rather than recall
   7. Flexibility and efficiency of use
   8. Aesthetic and minimalist design
   9. Help users recognize, diagnose, and recover from errors
   10. Help and documentation
3. **Accessibility audit (WCAG 2.1 AA)**:
   - Color contrast ratios
   - Touch/click target sizes (minimum 44×44px)
   - Keyboard navigation and focus order
   - Screen reader compatibility (labels, roles, alt text)
   - Text sizing and readability
4. **Consistency check** — flag any deviations from established patterns, terminology, or design system components
5. **Missing states** — identify states that are unaddressed (error, empty, loading, edge cases)
6. **Friction points** — steps, clicks, or cognitive load that could be reduced

For each finding, assign a severity: **Critical** (blocks task completion) / **Major** (significantly degrades experience) / **Minor** (polish issue).

Produce a prioritized list of findings with specific, actionable recommendations.

## Save output

After presenting the design review to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/design-review` and save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. In that same project `CLAUDE.md`, find the **Project status** table and set the **Status** column to **Done** for the row matching this deliverable
5. Confirm the file was written to the user
6. If no project `CLAUDE.md` exists, present the output for manual copying
