# Design UX Kit

A Claude Code plugin for designers and product teams. Provides slash command skills for common design and UX workflows, plus specialized AI agents for design critique and user research planning.

## What's Included

### Skills (Slash Commands)

| Command | Description |
|---------|-------------|
| `/design [brief or feature]` | Full Design & UX workflow orchestrator — runs all phases from UX brief through handoff, with checkpoints |
| `/brainstorm [design challenge]` | Structured design brainstorm — asks discovery questions first, then generates concepts across 7 angles with real-world examples, produces Mermaid direction maps and user flow diagrams, side-by-side experience descriptions, and recommends best bet / bold move / quick prototype with alternatives |
| `/ux-brief [feature or problem]` | Define design scope, target users, goals, constraints, and success criteria |
| `/wireframe-spec [feature or flow]` | Map key screens, user flows, navigation structure, and interaction states |
| `/wireframe-html [feature or wireframe spec]` | Produce an interactive HTML wireframe — brainstorms design directions first, generates a self-contained HTML file with inline CSS and vanilla JS, supports iterative feedback rounds, and surfaces discoveries that should update product documents (PRD, user stories) |
| `/design-review [design description]` | Heuristic review against Nielsen's 10 usability principles and WCAG 2.1 AA accessibility |
| `/usability-test [feature or flow]` | Generate a usability test plan with tasks, participant criteria, and discussion guide |
| `/design-handoff [feature]` | Produce a developer-ready handoff spec with component inventory, states, and acceptance criteria |

### Agents

| Agent | Description |
|-------|-------------|
| `ux-reviewer` | Deep structured audit against Nielsen's heuristics and WCAG 2.1 AA — designer perspective |
| `pm-design-reviewer` | Reviews a design against PM requirements — checks coverage, user flow completeness, and handoff readiness |
| `user-research-planner` | Plans a user research study — methodology, participant criteria, discussion guide, and analysis framework |

Agents are invoked automatically by Claude when relevant, or you can ask directly: *"Use the ux-reviewer agent to review this design."*

---

## Installation

### Install from GitHub

```bash
claude plugin marketplace add github:mjac-yue/claude-plugins
claude plugin install design-ux-kit
```

### Verify installation

```bash
claude plugin list
```

You should see `design-ux-kit` listed. The skills will now be available as slash commands.

---

## Usage Examples

### Run the full design workflow
```
/design Add a bulk export feature — users need to download their data as CSV
```

### Brainstorm design concepts before committing to a direction
```
/brainstorm How should users set up their notification preferences — mobile, multiple account types
```

### Produce an interactive HTML wireframe
```
/wireframe-html Notification preferences settings screen — see wireframe spec
```

### Write a UX brief
```
/ux-brief Notification preferences — users should control which emails they receive
```

### Create a wireframe spec
```
/wireframe-spec Onboarding flow for new users — 3 steps: account setup, invite team, first project
```

### Review a design for usability issues
```
/design-review The checkout flow described in this wireframe spec — focus on error states and form usability
```

### Plan a usability test
```
/usability-test The new dashboard — we want to know if users can find and use the filters
```

### Generate a developer handoff spec
```
/design-handoff The notification settings screen from the approved wireframe
```

### Deep design audit
Once you have a design open or described, ask:
```
Use the ux-reviewer agent to audit this design
```

### Check design coverage against PRD
```
Use the pm-design-reviewer agent to check this design handoff against the PRD
```

---

## Recommended Companion Plugins

For a full design + product workflow, also install:

| Plugin | Purpose | Install |
|--------|---------|---------|
| **pm-claude-kit** | PRDs, user stories, competitive analysis, roadmaps | `claude plugin install pm-claude-kit` |
| **dev-workflow-kit** | Tech specs, code review, deployment guides | `claude plugin install dev-workflow-kit` |
| **pdf skill** | Read and extract from design briefs in PDF | `claude plugin install anthropic-skills:pdf` |
| **pptx skill** | Create design presentations | `claude plugin install anthropic-skills:pptx` |

---

## Sharing with Your Team

1. Push this repo to your company GitHub
2. Team members install with: `claude plugin install github:your-org/claude-plugins`
3. Everyone gets the same commands and templates

---

## Customizing

### Modify a template
Templates live in each skill's folder (e.g., `skills/ux-brief/ux-brief-template.md`). Edit them to match your team's conventions.

### Add a new skill
1. Create `skills/your-skill/SKILL.md` following the existing pattern
2. Reinstall: `claude plugin uninstall design-ux-kit && claude plugin install design-ux-kit`

### Adjust agent behavior
Edit the relevant file in `agents/` (e.g., `agents/ux-reviewer.md`) to change review criteria or output format.
