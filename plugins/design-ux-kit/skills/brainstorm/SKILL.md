---
name: brainstorm
description: Run a structured design brainstorm for a UX challenge — generates a wide range of concepts across multiple angles, clusters them into themes, evaluates the top options against design criteria, and recommends next steps. Use when exploring UX patterns, interaction concepts, or layout approaches before committing to a direction.
disable-model-invocation: true
---

Run a design brainstorm for: $ARGUMENTS

> **Learning note — Design Brainstorm**
> Before committing to a design direction, it's worth exploring multiple approaches. The design brainstorm generates concepts across different angles — conventional patterns, adjacent ideas from other domains, minimal approaches, accessibility-first constraints — to prevent anchoring too quickly on the first solution. The best design is often not the obvious one, and this brainstorm gives you a structured way to discover alternatives before you invest time building anything.

Display the learning note above verbatim to the user before proceeding.

**Output standard — diagrams**: All documents are read in Obsidian. Use Mermaid syntax (` ```mermaid ` blocks) for all diagrams — Obsidian renders these natively. Use `flowchart TD` for user flows and decision trees, `flowchart LR` for concept maps and direction comparisons, `sequenceDiagram` for back-and-forth interaction flows between user and system.

**Output standard — tables**: Always include a blank line before any Markdown table — Obsidian requires this to render `|` syntax as a table rather than plain text.

Use the template in [brainstorm-template.md](brainstorm-template.md) as the structure.

Follow this process:

### Step 0: Discovery — ask before you brainstorm
**Always run this step first.** Read the input and identify what is unclear or under-specified. Ask 3–5 targeted questions to understand the design challenge well enough to generate relevant concepts. Present them as a numbered list and explicitly ask the user to answer before you continue.

Good discovery questions dig into:
- **The user**: Who specifically is experiencing this? What are they trying to get done? What device and environment are they in? What is their emotional state during this task?
- **The friction**: What breaks down in the current experience? Where do users drop off, make errors, or express frustration?
- **The constraint**: What is non-negotiable — platform, design system components, accessibility requirements, technical limits?
- **The goal**: What does success look like — task completion rate, reduced errors, faster time-on-task, higher satisfaction? What metric will move?
- **The context**: Is there existing work — prior designs, user research, competitive references — that the brainstorm should build on or avoid repeating?

Do not proceed to Step 1 until the user has answered. If the input is already detailed enough to answer most of these, confirm your understanding and ask only the questions that remain genuinely open.

### Step 1: Frame the design challenge
Using the discovery answers, sharpen the problem statement:
- Restate the challenge as a "How might we…" question — keeps framing open and generative
- Identify the primary user, their goal, and the context in which they'll experience this design (device, environment, emotional state)
- Note any hard constraints (platform, accessibility requirements, existing design system, technical limitations)
- Note any soft constraints (brand tone, visual language, team familiarity) that concepts should consider but can challenge
- State the design success condition: what must the experience achieve for the user to feel it worked?

### Step 2: Diverge — generate concepts broadly with real-world examples
Generate at least 12 distinct design concepts or directions. Quantity matters — push past the first instinct. For each angle, cite a real product or pattern that demonstrates this approach.

- **Conventional**: the established UX pattern for this type of problem — *example: how [product] implements this pattern today*
- **Adjacent**: how a different product category (gaming, e-commerce, mobile OS, fintech) solves a structurally similar challenge — *example: [product] uses [pattern] for [analogous problem]*
- **Contrarian**: what if you inverted the typical flow or removed a step users expect? — *example: [product that eliminated a step everyone assumed was mandatory]*
- **Minimal**: the simplest interface that still achieves the user's goal — *example: [product that succeeded with a dramatically stripped-down approach]*
- **Maximal**: the most guided, richest experience if complexity were no obstacle — *example: [product with the most hands-on, instructive version of this experience]*
- **User-led**: what workarounds or mental models do users already bring to this task? — *describe the workaround and what it reveals about the real mental model*
- **Accessibility-first**: design for the most constrained user — often produces universally clearer solutions — *example: [pattern that became mainstream by starting from an accessibility-first constraint]*

Do not filter concepts at this stage. Rough, directional concepts are fine — they seed better ideas through combination.

### Step 3: Cluster into design directions and map with a diagram
Group the concepts into 3–5 design directions. Give each direction a short, evocative name (e.g., "Progressive Reveal", "Always Visible Scaffold", "Inline Guidance").

Produce a Mermaid diagram (`flowchart LR`) showing how the directions relate — connect directions that are adjacent, complementary, or in tension. This helps identify which directions are genuinely different and which are variations of the same approach.

Then produce a second Mermaid diagram showing the primary user flow for the most promising direction. Use `flowchart TD` for linear flows with decision points, or `sequenceDiagram` if the interaction involves significant back-and-forth between the user and the system. Keep it to the key steps — this is a concept-level sketch, not a full spec.

Identify:
- Which direction is most familiar to users
- Which direction is most differentiated
- Which direction is easiest to prototype quickly

### Step 4: Converge — evaluate the top concepts with a comparison table and alternatives
Select the 4–6 most promising concepts (mix of safe and bold). Evaluate each using H / M / L scoring:

| Concept | Usability | Accessibility | Feasibility | Distinctiveness | Testability | Notes |
| ------- | --------- | ------------- | ----------- | --------------- | ----------- | ----- |
| [Concept A] | H / M / L | H / M / L | H / M / L | H / M / L | H / M / L | [key tradeoff] |

For the top 2–3 concepts, produce a brief **side-by-side description** of what the experience looks and feels like for the user — written in plain language, not design jargon. This makes abstract directions concrete and helps stakeholders engage with them without seeing visuals.

### Step 5: Recommend with alternatives
Identify the top 3 directions to explore further:
- **Best bet**: strongest balance across usability, feasibility, and distinctiveness — the default recommendation
- **Bold move**: highest distinctiveness; worth exploring even if it challenges conventions — recommend when the experience needs to differentiate
- **Quick prototype**: fastest to mock up and test — recommend when the team needs user signal before committing

For each:
- State one concrete next action
- Name the key design assumption this direction depends on
- Name the most likely usability failure, and how to de-risk it with a prototype or test

Also list **directions worth revisiting** — options that scored lower now but would become stronger if a specific constraint changed (e.g., "Direction X becomes viable if the design system adds [component]" or "Direction Y becomes viable if user research confirms [behaviour]").

### Step 6: Surface what's missing
Call out any important angles not yet explored — missing user research that would change the evaluation, unclear requirements, platform constraints that need clarification, or questions the user should answer before choosing a direction to prototype.

## Save output

After presenting the brainstorm to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table with a row for `/brainstorm`, save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. In that same project `CLAUDE.md`, find the **Project status** table and set the **Status** column to **Done** for the row matching this deliverable
5. Confirm the file was written to the user
6. If no output path is configured, present the output for manual copying and suggest saving it to `design/brainstorm.md`
