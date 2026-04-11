---
name: standup
description: Process daily standup updates from 1–2 people into a structured summary — what's done, what's in progress, what's blocked, and what decisions are needed. Works from bullet-point or free-text input. Flags anything that needs cycle plan attention. Use daily or whenever the team needs a quick shared view of status.
disable-model-invocation: true
---

Process standup updates for: $ARGUMENTS

You are helping a small team (1–2 PMs) get clarity on daily status and surface anything that needs attention. Keep it concise — standups should take less than 5 minutes to read.

## Step 1: Parse the updates

Accept input in any format:
- Bullet points per person
- Free-text notes
- A mix of both

If input is ambiguous, organise it by person first, then by category (done / in progress / blocked).

## Step 2: Surface blockers immediately

For each blocker:
- Name what is blocked
- Identify what's causing the block (missing input, unresolved dependency, technical issue, decision needed)
- Suggest who needs to act and by when
- If a blocker has been present for more than 1 day, flag it as a recurring blocker that may need escalation

## Step 3: Flag decisions needed

Identify anything in the updates that requires a decision before work can continue. For each:
- State the decision clearly
- Note who has authority to make it (from the kickoff doc if available)
- Suggest a deadline — decisions that block same-day work should be flagged as urgent

## Step 4: Assess cycle health

Based on the updates, briefly assess:
- Is the cycle on track to meet its goal?
- Is any item running significantly longer than sized?
- Is the team likely to complete all selected work in the remaining cycle days?
- Should any item be flagged for cycle plan review (rescoped, deferred, or escalated)?

Keep this assessment to 1–2 sentences. Don't over-analyse — if it's clearly on track, just say so.

---

Use the structure from [standup-template.md](standup-template.md).
