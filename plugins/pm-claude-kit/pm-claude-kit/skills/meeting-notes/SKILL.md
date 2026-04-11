---
name: meeting-notes
description: Structure raw meeting notes into a clean summary with decisions and action items. Use when the user wants to process or write up meeting notes.
disable-model-invocation: true
---

Process these meeting notes: $ARGUMENTS

Use the template in [meeting-template.md](meeting-template.md) as the structure.

Follow this process:
1. Extract and clearly label:
   - **Attendees** (if mentioned)
   - **Context / Background** — why this meeting happened
   - **Key Discussion Points** — the 3-5 most important things discussed
   - **Decisions Made** — explicit decisions with rationale (not just what was discussed)
   - **Action Items** — each must have: owner, specific action, due date (if mentioned)
   - **Open Questions** — unresolved items that need follow-up
   - **Next Steps / Next Meeting**
2. Be precise: "team will look into X" is not an action item. Convert vague statements into specific, owned tasks.
3. If input is raw/messy notes, clean them up while preserving meaning.
4. If input is a meeting description (not notes), draft a template ready to fill in during the meeting.

Output clean markdown suitable for sharing in Slack, Confluence, or email.
