---
name: usability-test
description: Create a usability test plan with participant criteria, task scenarios, success metrics, and a discussion guide. Use before finalizing a design to validate it with real users.
disable-model-invocation: true
---

Create a usability test plan for: $ARGUMENTS

> **Learning note — Usability Testing**
> Usability testing is how you find out whether your design actually works — before engineering invests weeks building it. Watching real users attempt real tasks reveals problems that internal reviews always miss: users interpret labels differently than the team did, find confusion in flows that seemed logical, and abandon tasks at points nobody anticipated. A structured test plan defines what you're testing, who you're testing with, and what results would trigger a redesign — so the test produces actionable decisions, not vague observations.

Display the learning note above verbatim to the user before proceeding.

**Output standard — tables**: All documents are read in Obsidian. Always include a blank line before any Markdown table — Obsidian requires this to render `|` syntax as a table rather than plain text.

Use the template in [usability-test-template.md](usability-test-template.md) as the structure.

Follow this process:
1. **Define test objectives** — what specific questions does this test need to answer? What decisions depend on the results? (max 3–5 objectives)
2. **Specify participant criteria**:
   - Primary persona characteristics (role, experience level, context)
   - Screener questions to qualify or disqualify participants
   - Recommended sample size (typically 5 per persona for qualitative; 20+ for quantitative)
3. **Design task scenarios**:
   - Write 3–7 realistic tasks that reflect actual user goals (not instructions to click buttons)
   - Frame tasks in the user's language, not product terminology
   - Include a starting state for each task
   - Define what "task complete" looks like
4. **Define success metrics** for each task:
   - Task completion rate (%)
   - Time on task
   - Error rate
   - Satisfaction rating (e.g., Single Ease Question, 1–7)
5. **Outline the discussion guide**:
   - Warm-up questions to understand user context
   - Think-aloud prompts to use during tasks
   - Post-task probes ("What did you expect to happen?")
   - Post-session debrief questions
6. **Specify analysis approach** — how will findings be synthesized? Affinity mapping, severity ratings, rainbow spreadsheet, etc.
7. **Define thresholds** — what results would trigger a redesign before launch?

Output a test plan ready to hand to a UX researcher or run a moderated session from.

## Save output

After presenting the usability test plan to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/usability-test` and save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. In that same project `CLAUDE.md`, find the **Project status** table and set the **Status** column to **Done** for the row matching this deliverable
5. Confirm the file was written to the user
6. If no project `CLAUDE.md` exists, present the output for manual copying
