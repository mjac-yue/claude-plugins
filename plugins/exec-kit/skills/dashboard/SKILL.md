---
name: dashboard
description: Generate a self-contained HTML project hub from all project documents — a single file named [project-name].html with a status landing page, rendered documentation, embedded wireframes, and open task tracking. Regenerates completely on each run; markdown files remain the source of truth. Run at any point to get a current, shareable view of the project.
disable-model-invocation: true
---

Generate the project dashboard for: $ARGUMENTS

> **Learning note — Project Dashboard**
> As a project accumulates documents across PM, design, and dev phases, the documentation becomes hard to navigate — files scattered across folders, status invisible unless you open each one, nothing that gives a stakeholder a quick read on where things stand. The dashboard solves this by generating a single self-contained HTML file from all current project documents. It's not a second source of truth — the markdown files are always authoritative. The HTML is a rendered, navigable view you can open in any browser, share with a stakeholder, or review before a meeting. Run it again at any checkpoint to get a fresh, fully current version.

Display the learning note above verbatim to the user before proceeding.

---

## Step 1: Find the project

Locate the project `CLAUDE.md`:
1. Check the current working directory
2. If not found, check one level up (in case you're inside a project subfolder)
3. If still not found and `$ARGUMENTS` was provided, check if it's a path to a project directory

Extract from `CLAUDE.md`:
- **Project name** — the `# Heading` at the top of the file
- **Project slug** — derive from the heading (lowercase, hyphens, no special characters)
- **Description** — the `> **[description]**` line under the heading
- **Project context** — Problem, Primary user, Builder, Started date
- **Output paths table** — all skill → file path mappings with Status and Last updated
- **Project status table** — if present

If no `CLAUDE.md` is found, ask the user for the project directory path before proceeding.

---

## Step 2: Read all project documents

Read every file listed in the Output paths table that exists on disk. For each file:
- Record the file path, its Status from the output paths table, and its Last updated date
- Read the full file content
- Determine if the file has real content or is just a placeholder (a placeholder is a file whose body contains only a heading line and/or the text "Run `/[skill]`..." — no substantive content)
- Flag placeholder files — they will show a "Not yet generated" state in the dashboard rather than empty content

Also read these files if they exist, regardless of the output paths table:
- `questions.md` — open questions and decisions log
- `pm/premortem.md` — premortem findings (top risks for the landing page)
- `design/wireframes/wireframe.html` — the interactive wireframe to embed

---

## Step 3: Convert markdown to HTML

For each non-placeholder document, convert its markdown content to HTML. Apply these conversions:

| Markdown | HTML |
|----------|------|
| `# Heading` | `<h1>` |
| `## Heading` | `<h2>` |
| `### Heading` | `<h3>` |
| `#### Heading` | `<h4>` |
| `**bold**` | `<strong>` |
| `*italic*` | `<em>` |
| `` `inline code` `` | `<code>` |
| ` ```code block``` ` | `<pre><code>` |
| `- item` / `* item` | `<ul><li>` |
| `1. item` | `<ol><li>` |
| `> blockquote` | `<blockquote>` |
| `---` | `<hr>` |
| `[text](url)` | `<a href="url">text</a>` |
| Markdown table | `<table>` with `<thead>` and `<tbody>` |
| Blank line between paragraphs | `<p>` |
| ` ```mermaid ``` ` blocks | Replace with a `<div class="mermaid-note">` containing the diagram description as a code block — do not attempt to render Mermaid diagrams |

Strip the frontmatter (YAML `---` block at the top) before converting. Strip the first `# [Title]` / status / last-updated header block from each document — the dashboard renders these as section metadata, not as part of the content.

---

## Step 4: Generate the HTML file

Generate a single self-contained HTML file. All CSS must be in a `<style>` block in `<head>`. All JavaScript must be in a `<script>` block before `</body>`. No external CDN links, no external file references.

### Visual design

Use this design system throughout:

**Palette:**
- Background: `#f8f9fa`
- Sidebar background: `#1a1a2e`
- Sidebar text: `#e0e0e0`
- Sidebar active: `#4f8ef7` (highlight)
- Card background: `#ffffff`
- Text primary: `#1a1a2e`
- Text secondary: `#6c757d`
- Border: `#e9ecef`
- Accent blue: `#4f8ef7`

**Status badge colours:**
- Done: `#198754` background, white text
- In progress: `#0d6efd` background, white text
- Not started: `#6c757d` background, white text
- Active: `#0d6efd` background, white text
- Skipped: `#6c757d` background, white text, `text-decoration: line-through`

**Typography:**
- Font stack: `-apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif`
- Base size: 15px, line-height 1.6
- Headings: `#1a1a2e`, weight 600
- Code: `'SF Mono', 'Monaco', 'Courier New', monospace`, size 13px, background `#f1f3f5`, padding `2px 6px`, border-radius `3px`
- Code blocks: background `#f1f3f5`, padding `16px`, border-left `3px solid #4f8ef7`
- Blockquotes: border-left `3px solid #4f8ef7`, background `#f0f5ff`, padding `12px 16px`
- Tables: full width, `border-collapse: collapse`, header background `#f1f3f5`, alternating row background `#f8f9fa`

### Layout

```
┌──────────────────────────────────────────────────────────┐
│ Sidebar (240px fixed) │ Main content area (flex 1)       │
│                       │                                  │
│ [Project Name]        │ [Section content]                │
│ [Progress: X/Y done]  │                                  │
│                       │                                  │
│ ● Overview            │                                  │
│                       │                                  │
│ Project               │                                  │
│   Project Status      │                                  │
│   Questions Log       │                                  │
│   Project Risks       │                                  │
│                       │                                  │
│ PM                    │                                  │
│   Brief               │                                  │
│   PRD                 │                                  │
│   ...                 │                                  │
│                       │                                  │
│ Design                │                                  │
│   UX Brief            │                                  │
│   Wireframes          │                                  │
│   ...                 │                                  │
│                       │                                  │
│ Dev                   │                                  │
│   Tech Spec           │                                  │
│   ...                 │                                  │
└──────────────────────────────────────────────────────────┘
```

Sidebar is fixed, 240px wide, dark background. Main content scrolls independently. On screens under 768px, sidebar collapses to a hamburger menu.

### Sidebar content

```html
<nav id="sidebar">
  <div class="sidebar-header">
    <h2>[Project Name]</h2>
    <div class="progress-pill">[X] / [Y] done</div>
  </div>

  <ul class="nav-list">
    <li><a href="#" data-section="overview" class="nav-link active">Overview</a></li>

    <li class="nav-group-label">Project</li>
    <li><a href="#" data-section="project-status" class="nav-link">Project Status</a></li>
    <li><a href="#" data-section="questions" class="nav-link">Questions Log</a></li>
    <li><a href="#" data-section="risks" class="nav-link">Project Risks</a></li>

    <li class="nav-group-label">PM</li>
    <!-- One <li> per PM document that exists, with status dot -->
    <!-- Status dot: green=Done, blue=In Progress, grey=Not Started -->
    <!-- Only show documents that are in the output paths table -->

    <li class="nav-group-label">Design</li>
    <!-- Design documents -->

    <li class="nav-group-label">Dev</li>
    <!-- Dev documents -->
  </ul>
</nav>
```

Show a small coloured dot before each nav item: green for Done, blue for In Progress, grey for Not Started. Placeholder files show grey dot.

### Overview section (landing page)

This is the first section shown on load. It is a tactical project snapshot — not a document list. It contains:

**1. Project header**
- Project name (h1)
- Description
- Problem statement, Primary user, Builder type, Started date — displayed as a clean metadata grid

**2. Progress bar chart**
A horizontal stacked bar chart showing overall completion across all deliverables. Render as a pure CSS bar (no canvas/SVG required):

```html
<div class="progress-chart">
  <div class="progress-bar-track">
    <div class="bar-done"    style="width: [X]%"  title="Done: [N]"></div>
    <div class="bar-active"  style="width: [X]%"  title="In progress: [N]"></div>
    <div class="bar-pending" style="width: [X]%"  title="Not started: [N]"></div>
  </div>
  <div class="progress-legend">
    <span class="legend-done">● Done ([N])</span>
    <span class="legend-active">● In progress ([N])</span>
    <span class="legend-pending">● Not started ([N])</span>
  </div>
</div>
```

Below the bar, render a row of three stat chips (Done / In Progress / Not Started) as coloured counts.

**3. In progress**
A highlighted card (blue left border) listing every deliverable currently marked "In Progress". For each item show: deliverable name, phase (PM / Design / Dev), and last updated date. If nothing is in progress, show a muted "No items currently in progress."

**4. Next steps**
Infer the next 2–3 actionable steps based on what is Done vs. Not Started. For example: if PRD is Done but Tech Spec is Not Started, the next step is to run `/techspec`. Present as a short numbered list with the suggested slash command alongside each step.

**5. Issues & dependencies to resolve**
Aggregate the most urgent blockers from two sources:
- P0 and P1 open questions from `questions.md` — show question text, owner, and priority badge
- Top risks scoring 7–9 from `pm/premortem.md` — show failure mode and risk score badge (red)

Group under two sub-headings: **Open questions** and **Top risks**. If both are empty, show a green "No blockers identified" badge. If `questions.md` has no open items, omit the Open questions sub-section. If no premortem exists, show a muted note under Top risks: *"Run `/premortem` to surface failure risks."*

**6. Last generated timestamp**
Small footer line: *"Dashboard generated: [date and time]"*

---

### Project Status section

A standalone section (linked from the Project group in the nav). Render the full deliverable status table from the CLAUDE.md Project status table (or the output paths table if no status table exists). Columns: Deliverable, Status (badge), Last Updated. Group rows by phase (PM / Design / Dev) using `<tbody>` with a group header row.

### Questions Log section

A standalone section (linked from the Project group in the nav). Render all questions from `questions.md` — both open and resolved. Group by status (Open first, then Resolved). For open questions, apply the priority card treatment:
- P0 in a red-bordered card
- P1 in an amber-bordered card
- P2 in a grey card

For resolved questions, render as a simple flat list with a ~~strikethrough~~ style or muted colour.

If `questions.md` doesn't exist or has no content, show a placeholder state.

### Project Risks section

A standalone section (linked from the Project group in the nav). Render the full premortem risk table from `pm/premortem.md`. Show all failure modes with: Failure Mode, Category, Risk Score (coloured badge: 7–9 = red, 4–6 = amber, 1–3 = grey), and any mitigation notes.

If no premortem has been run, show a placeholder state with the note: *"Run `/premortem` to generate the risk log."*

### Document sections

For each document that exists and has real content:

```html
<section id="[doc-id]" class="doc-section" style="display:none">
  <div class="doc-header">
    <h1>[Document Title]</h1>
    <div class="doc-meta">
      <span class="badge badge-[status]">[Status]</span>
      <span class="doc-date">Last updated: [date]</span>
    </div>
  </div>
  <div class="doc-body">
    [Converted HTML content]
  </div>
</section>
```

For placeholder documents (not yet generated):

```html
<section id="[doc-id]" class="doc-section" style="display:none">
  <div class="doc-header">
    <h1>[Document Title]</h1>
    <span class="badge badge-not-started">Not started</span>
  </div>
  <div class="placeholder-state">
    <p>This document hasn't been generated yet.</p>
    <code>Run /[skill] to generate it</code>
  </div>
</section>
```

### Wireframe section

If `design/wireframes/wireframe.html` exists:

Read the full content of `design/wireframes/wireframe.html`. Embed it using an `<iframe>` with `srcdoc` attribute set to the full escaped HTML content. Set height to `600px`, width `100%`, border `1px solid #e9ecef`, border-radius `8px`.

```html
<section id="wireframe" class="doc-section" style="display:none">
  <div class="doc-header">
    <h1>Interactive Wireframe</h1>
    <span class="badge badge-done">Done</span>
  </div>
  <iframe srcdoc="[escaped wireframe HTML]"
          style="width:100%;height:600px;border:1px solid #e9ecef;border-radius:8px;"
          title="Interactive Wireframe"></iframe>
</section>
```

If the wireframe doesn't exist, show a placeholder state for this section.

### JavaScript

Minimal vanilla JS — section switching only:

```javascript
const links = document.querySelectorAll('.nav-link');
const sections = document.querySelectorAll('.doc-section, #overview-section');

links.forEach(link => {
  link.addEventListener('click', (e) => {
    e.preventDefault();
    const target = link.dataset.section;

    // Hide all sections
    sections.forEach(s => s.style.display = 'none');

    // Show target
    const el = document.getElementById(target + '-section') ||
                document.getElementById(target);
    if (el) el.style.display = 'block';

    // Update active link
    links.forEach(l => l.classList.remove('active'));
    link.classList.add('active');
  });
});

// Mobile sidebar toggle
const toggle = document.getElementById('sidebar-toggle');
const sidebar = document.getElementById('sidebar');
if (toggle) {
  toggle.addEventListener('click', () => sidebar.classList.toggle('open'));
}
```

---

## Step 5: Save the file

1. Derive the output filename: `[project-slug].html` — e.g. `retirement-investment-strategy.html`
2. Save to the **project root** (same directory as `CLAUDE.md`)
3. If the file already exists, overwrite it completely — this is a full regeneration
4. Confirm the file path written to the user

Output to the user:

```
Dashboard generated: [project-slug].html
[N] documents rendered, [N] placeholders, [N] open questions

Open [project-slug].html in any browser to view the project hub.
Run /dashboard again at any time to regenerate with current content.
```

---

## Step 6: Update CLAUDE.md

In the project `CLAUDE.md` output paths table, add or update a row for `/dashboard`:

```
| `/dashboard` | `[project-slug].html` | Done | [Today's date] |
```

If the row already exists, update the Status to Done and Last updated to today's date.
