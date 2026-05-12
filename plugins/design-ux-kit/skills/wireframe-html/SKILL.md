---
name: wireframe-html
description: Produce an interactive HTML wireframe from a wireframe spec or design brief. Uses /brainstorm to explore design directions before committing to an implementation, then generates a self-contained HTML file with inline CSS and minimal JS. Supports iterative feedback rounds and surfaces any discoveries that require updating product documents (PRD, user stories, UX brief).
disable-model-invocation: true
---

Produce an HTML wireframe for: $ARGUMENTS

> **Learning note — Interactive HTML Wireframe**
> There's a category of problem that only appears when you actually interact with a design: flows that seem logical in a spec but feel confusing in motion, missing states that only become obvious when you hit an error, and layouts that break at a different screen size. An interactive HTML wireframe makes the design clickable and testable before any visual design or engineering work begins — it's the fastest way to surface these problems at the cheapest moment to fix them.

Display the learning note above verbatim to the user before proceeding.

**Output standard — HTML**: All HTML output must be a single self-contained file — inline CSS in a `<style>` block, inline JS in a `<script>` block, no external CDN or file dependencies. Use semantic HTML5 elements. Style as a clear wireframe: monochrome palette (white, light grey, mid grey, dark grey, black), placeholder images as grey `div` boxes with dimensions labeled inside, `[Placeholder text]` for content that will be real copy. The wireframe aesthetic should communicate structure and flow — not finished visual design.

**Output standard — responsiveness**: Every wireframe must include mobile and desktop layouts. Use a CSS class toggle or a `<select>` dropdown in the page to switch between viewports. Default to the mobile view.

**Output standard — interactivity**: Use minimal vanilla JS only. Acceptable interactions: tab/nav switching between screens, modal open/close, form validation state simulation (show error/success states on button click), accordion expand/collapse. Do not use frameworks or libraries.

Follow this process:

### Step 0: Check existing context

Before generating anything:
1. Check if a wireframe spec exists (in `design/wireframe-spec.md` or referenced in `CLAUDE.md`) — if so, read it and use it as the primary input
2. Check if a brainstorm has been run for this design challenge (in `design/brainstorm.md`) — if so, note the recommended direction
3. Check if a UX brief exists (`design/ux-brief.md`) — if so, extract the target user, goals, and constraints
4. Check if a PRD exists (`pm/prd.md`) — if so, note the requirements this mockup must satisfy

Summarise what you found before proceeding. If no wireframe spec exists, ask the user to describe the key screens and flows before continuing.

### Step 1: Brainstorm design directions

Before writing any HTML, present 2–3 distinct design directions for the user to choose from. For each direction:
- Give it a short evocative name (e.g., "Card-first", "Sidebar Nav", "Stepped Wizard")
- Describe in 2–3 sentences what the experience looks and feels like — the layout pattern, how the user moves through it, what's prominent
- Name a real product that uses a similar pattern (e.g., "Similar to how Stripe's dashboard organises secondary actions")
- State the key design assumption this direction makes about the user

Ask: *"Which direction should I build the HTML mockup from — or would you like to combine elements from more than one?"*

If a `/brainstorm` has already been run and a direction was chosen, confirm the direction and proceed directly to Step 2.

### Step 2: Produce the HTML wireframe

Build a single self-contained HTML file covering all key screens defined in the wireframe spec (or described by the user). Structure the file as follows:

**Page structure:**
- A top navigation bar listing all screens as clickable links — clicking switches the visible screen section
- A viewport toggle (Mobile / Desktop) that resizes the content area using CSS
- Each screen as a `<section>` with a clear heading and screen ID
- A persistent annotation panel (collapsible) showing design notes for the visible screen

**For each screen, implement:**
- All layout zones (header, nav, content, sidebar, footer, modals) as clearly labelled `div` blocks
- Every component listed in the wireframe spec — inputs, buttons, labels, cards, tables — with their correct labels and placeholder content
- All named states: show the default state in the main view; add a button or tab to toggle into error / empty / loading / success states
- Inline HTML comments (`<!-- comment -->`) explaining non-obvious layout or interaction decisions

**Annotations:**
- Add a `data-note` attribute to any element where a design decision was made that differs from the wireframe spec, or where an assumption was made
- The annotation panel reads these and lists them — this gives the reviewer context without cluttering the visual

### Step 3: Present and collect feedback

After producing the HTML:
1. Show the complete file in a fenced code block (` ```html `) so the user can copy and open it in a browser
2. Summarise what was built: screens covered, states implemented, key design decisions made
3. Ask for feedback using these specific prompts:
   - *"Does the layout feel right for the primary user's context (device, environment)?"*
   - *"Are there any screens, states, or edge cases missing?"*
   - *"Does anything feel confusing or counter-intuitive in the flow?"*
   - *"Are there any requirements from the PRD or user stories that aren't reflected here?"*

### Step 4: Iterate

Apply feedback and produce an updated HTML file. For each round:
- List the changes made at the top of the response before the code block
- Flag any changes that represent a significant direction shift (not just a polish fix) — offer to re-run the brainstorm for that component if needed
- Keep a running changelog as HTML comments in the `<head>` of the file:
  ```html
  <!-- Changelog:
    v1 — Initial mockup
    v2 — Moved nav to bottom on mobile per feedback; added empty state for no-data case
  -->
  ```

Continue iterating until the user approves the mockup. Maximum 3 rounds before recommending a `/design-review` to pressure-test the current state before continuing.

### Step 5: Surface PM document updates

After the mockup is approved, review the full iteration history and identify any discoveries that should flow back to product documents. For each finding, state:
- **What was discovered** — the specific design decision or edge case uncovered during mockup
- **Which document to update** — PRD, user stories, UX brief, or wireframe spec
- **The specific change** — exactly what to add, remove, or amend

Common triggers:
- A user flow that only became clear when visualised → update user stories with a new Given/When/Then
- A constraint discovered during mockup (e.g., mobile layout can't fit X) → update UX brief constraints
- A requirement that turned out to be ambiguous or conflicting → flag in PRD open questions
- An edge case surfaced that wasn't in the acceptance criteria → add to the relevant user story

Ask: *"Should I apply these updates to the product documents now?"* If yes, make the edits to the relevant files.

## Save output

After the mockup is approved:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table with a row for `/wireframe-html`, save the HTML file to that path
3. If no path is configured, save the file as `design/wireframes/wireframe.html`
4. In the project `CLAUDE.md`, find the **Project status** table and set the **Status** column to **Done** for the HTML Mockup row
5. Confirm the file path written to the user
