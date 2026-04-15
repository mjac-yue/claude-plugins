---
name: brainstorm
description: Run a structured brainstorm for a product challenge — generates a wide range of ideas across multiple angles, clusters them into themes, evaluates the top options, and recommends next steps. Use when exploring solutions to a problem, generating feature ideas, or unlocking a decision that feels stuck.
disable-model-invocation: true
---

Run a product brainstorm for: $ARGUMENTS

> **Learning note — Product Brainstorm**
> The goal of brainstorming is to generate many options before converging on one — this is called divergent thinking. Research consistently shows that the best ideas rarely come from the first instinct; they emerge after pushing past the obvious solutions to explore adjacent, contrarian, and minimal approaches. The structured brainstorm you're about to run is designed to prevent anchoring on the first idea and to surface angles you'd otherwise miss before you commit to a direction.

Display the learning note above verbatim to the user before proceeding.

**Output standard — diagrams**: All documents are read in Obsidian. Use Mermaid syntax (` ```mermaid ` blocks) for all diagrams — Obsidian renders these natively. Use `flowchart TD` or `flowchart LR` for concept maps and decision trees, `sequenceDiagram` for user flows with back-and-forth steps.

**Output standard — tables**: Always include a blank line before any Markdown table — Obsidian requires this to render `|` syntax as a table rather than plain text.

Use the template in [brainstorm-template.md](brainstorm-template.md) as the structure.

Follow this process:

### Step 0: Discovery — ask before you brainstorm
**Always run this step first.** Read the input and identify what is unclear or under-specified. Ask 3–5 targeted questions to understand the problem well enough to generate relevant ideas. Present the questions as a numbered list and explicitly ask the user to answer them before you continue.

Good discovery questions dig into:
- **The user**: Who specifically is experiencing this problem? What are they trying to get done? What have they tried already?
- **The problem**: What does failure look like today? How often does it happen? What's the cost — to the user and to the business?
- **The constraint**: What is non-negotiable? What has already been ruled out and why?
- **The goal**: What does a good outcome look like in 3 months? Is this about retention, acquisition, revenue, efficiency — or something else?
- **The context**: Is there existing work — research, prior attempts, related features — that the brainstorm should build on or avoid repeating?

Do not proceed to Step 1 until the user has answered. If the input is already detailed enough to answer most of these, confirm your understanding and ask only the questions that remain genuinely open.

### Step 1: Frame the challenge
Using the discovery answers, sharpen the problem statement:
- Restate the challenge as a "How might we…" question — keeps framing open and generative
- Identify the primary user and what they are trying to achieve
- Note any hard constraints (technical, timeline, budget, regulatory) ideas must respect
- Note any soft constraints (brand, team preferences) ideas should consider but can challenge
- State the success condition: what does a winning idea need to achieve?

### Step 2: Diverge — generate ideas broadly with real-world examples
Generate at least 12 distinct ideas. Quantity matters — push past the obvious. For each angle, cite a real product, company, or pattern that demonstrates this approach in practice.

- **Conventional**: the standard industry approach — *example: how [established player in the space] solves this today*
- **Adjacent**: what works in a related domain that could be borrowed — *example: how [product from a different category] handles a structurally similar problem*
- **Contrarian**: what happens if you flip the core assumption entirely — *example: [product that removed a step everyone assumed was necessary]*
- **Minimal**: the simplest version that still solves the problem — *example: [product that succeeded with a dramatically stripped-down approach]*
- **Maximal**: the most ambitious version if resources were unlimited — *example: [product with the richest, most guided version of this experience]*
- **User-led**: what users already do as a workaround — *describe the workaround pattern and what it reveals about unmet need*
- **Technology-led**: what AI, APIs, or automation makes newly possible — *example: [product using this technology to solve a similar problem]*

Do not filter ideas at this stage. Unusual ideas are welcome — they often seed better ideas through combination.

### Step 3: Cluster into themes and map with a diagram
Group the ideas into 3–5 thematic clusters. Give each cluster a short, evocative name.

Produce a Mermaid diagram showing how the clusters relate — use `flowchart LR` to show the clusters as nodes and connect ideas that are adjacent, complementary, or in tension with each other. This visual helps identify which directions are genuinely different and which are variations of the same approach.

Identify:
- Which cluster is most conventional
- Which cluster is most novel
- Which cluster has the broadest range of options

### Step 4: Converge — evaluate the top ideas with a comparison table
Select the 4–6 most promising ideas (mix of safe and bold). Evaluate each across four dimensions using H / M / L scoring:

| Idea | User impact | Feasibility | Novelty | Speed to validate | Notes |
| ---- | ----------- | ----------- | ------- | ----------------- | ----- |
| [Idea A] | H / M / L | H / M / L | H / M / L | H / M / L | [key tradeoff] |

Then produce a second Mermaid diagram — a decision tree (`flowchart TD`) that maps which idea fits best given different conditions. For example: "If the team wants fast learning → [Quick win]. If differentiation is the priority → [Bold move]. If adoption is the risk → [Best bet]." This makes the recommendation logic transparent and helps the user choose based on their actual situation.

### Step 5: Recommend with alternatives
Identify the top 3 ideas to pursue:
- **Best bet**: highest overall score across the four dimensions — the default recommendation
- **Bold move**: highest novelty, worth exploring even if riskier — recommend when differentiation is the top priority
- **Quick win**: fastest to validate — recommend when the team needs early signal or is uncertain about the problem definition

For each:
- State one concrete next action
- Name the key assumption this idea depends on
- Name the most likely reason it fails, and how to de-risk it

Also list **ideas worth revisiting** — options that scored lower now but would become stronger if a specific constraint changed (e.g., "Idea X becomes viable if timeline extends past Q3" or "Idea Y becomes viable if the API partnership closes").

### Step 6: Surface what's missing
Call out any important angles not explored — constraints that limited the brainstorm, data gaps that would change the evaluation, stakeholders whose perspective was absent, or questions the user should answer before choosing a direction.

## Save output

After presenting the brainstorm to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table with a row for `/brainstorm`, save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. In that same project `CLAUDE.md`, find the **Project status** table and set the **Status** column to **Done** for the row matching this deliverable
5. Confirm the file was written to the user
6. If no output path is configured, present the output for manual copying and suggest saving it to `pm/brainstorm.md`
