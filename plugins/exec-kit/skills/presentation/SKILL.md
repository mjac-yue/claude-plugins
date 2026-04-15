---
name: presentation
description: Create a presentation as a Marp markdown file. Produces a structured slide deck with proper Marp frontmatter, cover slide, agenda, content slides, and a closing slide. Use whenever a presentation, slide deck, or pitch deck needs to be created.
disable-model-invocation: true
---

Create a Marp presentation for: $ARGUMENTS

> **Learning note — Stakeholder Presentation**
> Stakeholder presentations are how product decisions get made, funded, and communicated. A well-structured deck ensures your analysis, proposal, or update is understood clearly — regardless of how complex the underlying work is. The most common mistake in presentations is leading with detail rather than conclusion: start with what you're asking the audience to understand or decide, then provide the supporting evidence. This skill uses Marp, a markdown-based presentation tool, so slides can be version-controlled and regenerated as easily as any other document.

**Output standard — Marp markdown**: All presentations are rendered with [Marp](https://marp.app/). The output must be a valid `.md` file with the Marp frontmatter block at the top. Every slide is separated by `---`. Use the template in [presentation-template.md](presentation-template.md) as the structural reference.

**Output standard — diagrams**: Use Mermaid syntax (` ```mermaid ` blocks) for any diagrams — `flowchart LR` for flows, `sequenceDiagram` for sequences, `erDiagram` for data models. Marp renders Mermaid natively.

Follow this process:

1. **Clarify the presentation brief** — before writing any slides, confirm:
   - **Audience**: who will see this (technical, executive, customer, mixed)?
   - **Goal**: inform, persuade, teach, or propose?
   - **Length**: how many slides is appropriate? (default to 8–12 for a focused deck)
   - If `$ARGUMENTS` provides sufficient context, proceed without asking.

2. **Draft the structure** — outline the slide titles and one-line purpose for each before writing content:
   - Cover + title
   - Agenda (for decks ≥ 6 slides)
   - Content slides grouped by theme
   - Summary / takeaways
   - Closing (questions, next steps, or call to action)

3. **Write the slides** — for each slide:
   - Use a single `#` heading as the slide title (Marp `headingDivider: 1` splits on `#`)
   - Keep text concise — max 5–6 bullet points per slide, one idea per bullet
   - Use `>` blockquotes for key takeaways or pull quotes
   - Use tables for comparisons (always add a blank line before the `|` syntax)
   - Use `<!-- _class: split -->` for two-column layouts
   - Use `<!-- _class: title -->` for the cover and closing slides
   - Add Mermaid diagrams where a visual would replace multiple bullets

4. **Tailor the Marp frontmatter** — choose appropriate values:
   - `theme`: `default`, `gaia`, or `uncover` (default is `default`)
   - `paginate: true` for all decks except single-slide title cards
   - `headingDivider: 1` so each `#` heading starts a new slide automatically
   - Add a `style` block for any custom CSS needed (font sizing, column layouts, header colours)

5. **Review for slide discipline**:
   - No slide should contain a wall of text — rewrite as bullets, a table, or a diagram
   - Each slide should communicate one clear idea
   - The deck should tell a logical story from cover to close

## Save output

After presenting the Marp markdown to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/presentation` and save the output to that file path with a `.md` extension
3. If no output path is configured, save the file as `presentation.md` in the current working directory (or a name derived from `$ARGUMENTS`, e.g., `q2-roadmap.md`)
4. Confirm the file path written so the user can open it in Marp or VS Code with the Marp extension
