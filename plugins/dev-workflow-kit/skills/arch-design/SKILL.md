---
name: arch-design
description: Produce an architectural design for a feature or system — covering non-functional requirements, architectural style, component boundaries, integration patterns, cross-cutting concerns, and Architecture Decision Records (ADRs). Output is structured to populate the Architecture section of a technical specification.
disable-model-invocation: true
---

Produce an architectural design for: $ARGUMENTS

**Output standard — diagrams**: All documents are read in Obsidian. Use Mermaid syntax (` ```mermaid ` blocks) for all diagrams — `flowchart LR` for system context and component relationships, `sequenceDiagram` for integration flows, `erDiagram` for data ownership maps.

**Output standard — tables**: Always include a blank line before any Markdown table. Obsidian requires this to render `|` syntax as a table rather than plain text.

Use the template in [arch-design-template.md](arch-design-template.md) as the structure.

Follow this process:

1. **Define non-functional requirements (NFRs)**:
   - Performance: latency targets (p50/p95/p99), throughput (RPS), batch SLAs
   - Scalability: current load, growth projection, scale-out strategy
   - Availability: uptime target (99.9% / 99.99%), RTO, RPO
   - Security: authentication model, data sensitivity, compliance requirements
   - Maintainability: team size, expected change frequency, onboarding cost
   - Observability: logging, metrics, tracing requirements
   - Testability: what must be independently testable?
   These drive every architectural decision — state them before making any choices.

2. **Select an architectural style**:
   Evaluate which style best fits the NFRs and existing system. Common options:
   - **Monolith (modular)** — single deployable unit with clear internal modules; simplest operationally
   - **Layered / N-tier** — presentation, business logic, data layers; well-understood, easy to reason about
   - **Microservices** — independently deployable services; high operational complexity, good for independent scaling
   - **Event-driven** — services communicate via events/messages; decoupled, but harder to trace and debug
   - **CQRS + Event Sourcing** — separate read/write models; powerful for audit and replay, high complexity
   - **Hexagonal (ports & adapters)** — business logic isolated from infrastructure; excellent testability
   State the chosen style and why. Explicitly note styles that were considered and rejected.

3. **Define component boundaries**:
   - Identify the major components (services, modules, layers, or bounded contexts)
   - For each component: its single responsibility, what it owns, what it does not own
   - Define the contracts between components (APIs, events, shared data stores)
   - Flag any components that share mutable state — these are coupling risks

4. **Define integration patterns**:
   - How do components communicate? (synchronous REST/gRPC, async messaging, shared DB, file exchange)
   - What consistency model is used at each boundary? (strong, eventual, causal)
   - How are failures at integration points handled? (retry, circuit breaker, fallback, dead letter)
   - What is the data ownership model? (which component is the system of record for each entity)

5. **Address cross-cutting concerns**:
   - **Authentication & authorization**: where are identity and permissions enforced?
   - **Error handling**: how do errors propagate across component boundaries? What reaches the user?
   - **Caching**: where is caching applied and what is the invalidation strategy?
   - **Logging & tracing**: what is logged, at what level, and how are requests correlated across components?
   - **Configuration management**: how is environment-specific config injected?
   - **Feature flags**: how are in-flight features controlled without a deploy?

6. **Identify architectural risks**:
   - Single points of failure
   - Bottlenecks that limit horizontal scaling
   - Components with high coupling that resist change
   - Decisions that are hard to reverse (lock-in risks)

7. **Write Architecture Decision Records (ADRs)** for each significant architectural choice:
   - Context: what situation prompted the decision?
   - Decision: what was chosen?
   - Rationale: why?
   - Consequences: what does this make easier or harder?
   - Alternatives considered and why they were rejected

Output an architectural design ready to be incorporated into the Architecture section of a technical specification.

## Save output

After presenting the architectural design to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/arch-design` and save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. In that same project `CLAUDE.md`, find the **Project status** table and set the **Status** column to **Done** for the row matching this deliverable
5. Confirm the file was written to the user
6. If no project `CLAUDE.md` exists, present the output for manual copying
