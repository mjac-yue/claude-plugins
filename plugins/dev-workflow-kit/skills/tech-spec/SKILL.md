---
name: tech-spec
description: Generate a technical specification from product requirements. Covers architecture, data models, system components, dependencies, and technical risks. Use before development planning begins.
disable-model-invocation: true
---

Generate a technical specification for: $ARGUMENTS

**Output standard — diagrams**: All documents are read in Obsidian. Use Mermaid syntax (` ```mermaid ` blocks) for all diagrams — `flowchart LR` for system context and component diagrams, `erDiagram` for data models, `sequenceDiagram` for API request flows.

**Output standard — tables**: Always include a blank line before any Markdown table. Obsidian requires this to render `|` syntax as a table rather than plain text.

Use the template in [tech-spec-template.md](tech-spec-template.md) as the structure.

Follow this process:
1. **Understand the requirements** — restate the product goal and key user stories in engineering terms. Flag any ambiguities that must be resolved before design is final.
2. **Identify solution options** — before committing to an approach, enumerate 2–4 distinct technical approaches that could satisfy the requirements:
   - For each option, describe the approach in 2–3 sentences
   - Evaluate it across: implementation complexity, performance, maintainability, time to deliver, and risk
   - **Include real cost estimates** — not just "Low/Medium/High". For each option, state the actual expected monthly or annual cost at the expected usage level (e.g., "$0/month on Vercel free tier", "$25/month for Supabase Pro", "$0.002/1K tokens for Claude API"). If cost is unknown, note it as TBD and flag it as a risk.
   - Note which constraints or trade-offs each option optimises for
   - Identify the option you recommend and state why clearly
   - Record rejected options and the reason they were ruled out — this prevents relitigating decisions later
3. **Incorporate the architectural design** — if `/arch-design` has been run or an `arch-reviewer` assessment exists, pull the key outputs into the Architecture section of the spec:
   - NFRs, architectural style, and ADRs from the design document
   - Component responsibilities, integration patterns, and cross-cutting concerns
   - If no architectural design exists yet, produce a concise architecture section covering: system context, components, integration patterns, and the most important cross-cutting concerns (auth, error handling, observability)
   - Note which systems are extended vs. built from scratch
4. **Design the data model**:
   - New entities and their fields, types, and constraints
   - Relationships between entities
   - Database schema changes (new tables, migrations, indexes)
5. **Specify key algorithms or business logic** — any non-trivial logic that needs to be spelled out before implementation
6. **Define APIs needed** — list endpoints or events this feature produces or consumes (detail via `/api-spec` if needed)
7. **Identify dependencies and costs**:
   - Internal: teams, services, or feature flags that must be ready first
   - External: third-party APIs, SDKs, or infrastructure — for each, state the pricing tier being assumed (free, pro, pay-as-you-go) and the estimated monthly cost at expected usage
   - Produce a **Cost Summary table** aggregating all external dependency costs: monthly estimate at launch volume and projected cost at 10× scale. Flag any component where cost scales with usage and could become significant.
8. **Assess technical risks**:
   - Performance: latency, throughput, or scale concerns
   - Security: auth, data exposure, input validation, rate limiting
   - Reliability: failure modes, retry logic, data consistency
9. **Estimate complexity** — rough T-shirt sizing (S/M/L/XL) per major component with rationale

Output a spec detailed enough for engineering to estimate and plan without needing further product clarification.

## Save output

After presenting the technical specification to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/tech-spec` and save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. In that same project `CLAUDE.md`, find the **Project status** table and set the **Status** column to **Done** for the row matching this deliverable
5. Confirm the file was written to the user
6. If no project `CLAUDE.md` exists, present the output for manual copying
