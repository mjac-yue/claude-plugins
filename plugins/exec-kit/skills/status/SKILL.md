---
name: status
description: Generate a stakeholder status report showing progress against the release plan — phase completion, RAG status, what shipped this cycle, what's coming next, risks, and decisions needed. Use weekly or fortnightly to keep stakeholders informed without writing reports from scratch.
disable-model-invocation: true
---

Generate a status report for: $ARGUMENTS

> **Learning note — Stakeholder Status Report**
> Status reports keep decision-makers informed without requiring them to attend every meeting. A concise RAG status (Red/Amber/Green) with progress, risks, and decisions needed lets stakeholders do their job — unblocking resources, adjusting timelines, making scope trade-offs — at the right moments. The most important rule for status reports: be honest about yellow and red states. A status report that hides a problem doesn't help anyone; it just delays the conversation until the problem is worse.

Display the learning note above verbatim to the user before proceeding.

You are helping a PM produce a concise, honest stakeholder update. Good status reports surface problems early — a green report that hides a yellow reality helps nobody.

## Step 1: Gather context

Ask if not already provided:
1. *"What is the reporting period (cycle number and dates)?"*
2. *"Who is the audience?"* — internal team, leadership, external stakeholders
3. *"What is the overall status?"* — on track, at risk, or off track, and why
4. *"What was completed this cycle?"*
5. *"What is planned for next cycle?"*
6. *"Are there any open risks or issues?"*
7. *"Are any decisions needed from stakeholders?"*

## Step 2: Set RAG status honestly

Assess each dimension independently:
- **Schedule**: Is the team on track to hit the target launch date? Are any milestones at risk?
- **Scope**: Is the scope stable, or are there change requests, discoveries, or deferrals that have shifted it?
- **Quality**: Are there any known bugs, technical debt decisions, or test coverage gaps worth flagging?
- **Team**: Is capacity as planned? Any upcoming absences, dependencies on unavailable people, or resource constraints?

Use the traffic light honestly:
- 🟢 Green: on track, no action needed from stakeholders
- 🟡 Yellow: at risk, monitoring closely, may need support — say what help is needed
- 🔴 Red: off track, action required — say what specifically

## Step 3: Summarise progress against release plan

Show each phase with its target date and current status. Make it immediately clear which phases are complete, which are in progress, and which haven't started. Note the current build layer and how far through it the team is.

## Step 4: Surface decisions needed

Any item that requires a stakeholder decision before the team can proceed belongs in this section. Be specific about what the decision is, the options, and when it's needed. Don't bury it at the bottom.

## Step 5: Calibrate length to audience

- Leadership / external stakeholders: lead with the one-line summary and RAG, keep narrative brief
- Internal team: can include more detail on layer progress and specific blockers

The report should be readable in under 2 minutes.

---

Use the structure from [status-template.md](status-template.md).

## Save output

After presenting the status report:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/status` and save the report to that file path
3. If no output path is configured for `/status`, save to `execution/status-[date].md` in the project directory (e.g., `execution/status-2026-04-27.md`) — one file per reporting period
4. Update the **Status** field to **Done** and **Last updated** to today's date
5. Confirm the file was written to the user
6. If no project directory exists, present the output for manual copying
