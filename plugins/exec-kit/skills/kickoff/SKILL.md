---
name: kickoff
description: Produce a project kickoff document — what we're building, scope boundaries, team roles, working rhythm, decision-making process, communication norms, and project folder structure. Use at the start of a new project to align the team before execution begins. Pairs with /release-plan for the full project launch package.
disable-model-invocation: true
---

Produce a project kickoff document for: $ARGUMENTS

You are helping a small team (1–2 PMs) get aligned before execution starts. A good kickoff document prevents the most common small-team failure modes: unclear scope, undefined decision ownership, and no shared understanding of how the work will run.

## Step 1: Gather context

Ask if not already provided:
1. *"What are we building?"* — reference the PRD or brief if one exists
2. *"Who is on the team and what are each person's responsibilities?"*
3. *"Is there a target launch date?"*
4. *"How do you prefer to work — sprints or continuous flow?"*
5. *"Who are the key stakeholders outside the team?"*

## Step 2: Define the project clearly

From the PRD (if available) or the input:
- Extract the problem statement in one sentence
- Summarise the solution in one sentence
- State the strategic reason or deadline driving the project now
- Define success in measurable terms — tie to PRD success metrics where possible

## Step 3: Set scope boundaries explicitly

A kickoff document without explicit out-of-scope items is incomplete. For every project:
- List what is explicitly in scope
- List what is explicitly out of scope (prevents scope creep conversations later)
- List any items deferred to v1.1 — these were considered but consciously excluded from v1

## Step 4: Define team roles and decision authority

For a 1–2 person team, decision authority is often unclear because everyone wears multiple hats. Be explicit:
- Who owns product scope decisions?
- Who owns technical approach decisions?
- Who decides to defer a feature when timeline is at risk?
- What gets escalated, and to whom?

## Step 5: Define the working rhythm

Make the methodology choice explicit and set expectations:
- Sprint or flow — and what that means in practice for this team
- Cadence: how often cycle plans are written, standups happen, status reports go out
- Where work items are tracked (project folder, linear, Jira, etc.)

## Step 6: Communication norms

Define where and how the team communicates, especially:
- How blockers are raised (async vs sync)
- Response time expectations
- Where decisions are logged (prevents "I thought we decided..." conversations)

## Step 7: Set up the project folder

Define the folder structure where all skill outputs will be saved. The structure should map to the full product development lifecycle so outputs from pm-claude-kit, design-ux-kit, dev-workflow-kit, and exec-kit all have a home.

Note: if using the `/init` skill from pm-claude-kit, this structure is created automatically.

---

Use the structure from [kickoff-template.md](kickoff-template.md).

Output the complete kickoff document. Do not use placeholder text — fill in every section based on the project context provided.
