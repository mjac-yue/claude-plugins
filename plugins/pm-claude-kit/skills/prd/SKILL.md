---
name: prd
description: Generate a Product Requirements Document (PRD) for a feature or product. Use when the user wants to write a PRD, spec, or requirements document.
disable-model-invocation: true
---

Write a Product Requirements Document (PRD) for: $ARGUMENTS

Use the template in [prd-template.md](prd-template.md) as the structure.

Follow this process:
1. If the user's input is brief, ask 2-3 clarifying questions before writing (target audience, key problem, success metric). If the input is detailed, proceed directly.
2. Fill every section of the template with specific, concrete content — no placeholder text.
3. For the "Out of Scope" section, think carefully about what related things this feature does NOT include.
4. For success metrics, always propose at least one leading indicator and one lagging indicator.
5. Flag any open questions or assumptions made in a final "Open Questions" section.

Output the completed PRD as a markdown document ready to share or save.
