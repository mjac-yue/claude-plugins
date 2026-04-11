---
name: dev-plan
description: Generate a development plan with task breakdown, estimates, dependencies, and sprint allocation. Use after a tech spec is approved to translate it into an actionable engineering plan.
disable-model-invocation: true
---

Generate a development plan for: $ARGUMENTS

Use the template in [dev-plan-template.md](dev-plan-template.md) as the structure.

Follow this process:
1. **Restate the goal and constraints** — what is being built, by when, and with what team size or resource constraints?
2. **Break down the work into tasks**. For each task:
   - Clear name and description
   - Engineering discipline (frontend, backend, infrastructure, data, etc.)
   - Estimate in story points or days (include reasoning for non-obvious estimates)
   - Dependencies (which other tasks must be complete first)
   - Owner role (which type of engineer should own this)
3. **Identify the critical path** — the sequence of dependent tasks that determines the earliest possible completion date
4. **Flag blockers** — anything that must be resolved, decided, or procured before work can start (design assets, API keys, third-party contracts, platform decisions)
5. **Propose sprint allocation** — group tasks into sprints (1- or 2-week), accounting for dependencies and parallelism. Assume typical capacity (e.g., 70–80% for planned work, remainder for reviews and unplanned).
6. **Define milestones** — meaningful checkpoints (e.g., "API complete and tested", "feature flag off in staging") that signal progress
7. **Highlight risks to the plan** — what could cause a slip, and what's the mitigation or contingency?
8. **Definition of Done** — the specific conditions that mark the feature complete and ready for QA handoff

Output a plan ready to drop into a sprint planning doc or project tracker.
