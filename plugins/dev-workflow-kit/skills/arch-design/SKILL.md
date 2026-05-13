---
name: arch-design
description: Produce an architectural design for a feature or system — covering non-functional requirements, architectural style, component boundaries, integration patterns, cross-cutting concerns, and Architecture Decision Records (ADRs). Output is structured to populate the Architecture section of a technical specification.
disable-model-invocation: true
---

Produce an architectural design for: $ARGUMENTS

> **Learning note — Architectural Design**
> Architecture decisions are the hardest to change later. The choices made here — how components communicate, how data is structured, how the system scales — create structural constraints that persist for years. A formal architecture review forces you to consider non-functional requirements (performance, security, maintainability, testability) before they become production problems. The goal isn't to over-engineer; it's to make the important structural decisions explicitly, while the cost of changing them is still low.

Display the learning note above verbatim to the user before proceeding.

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

7. **Address AI architecture concerns** (skip this step entirely if no AI/ML components are in scope):

   > **Learning note — AI Architecture**
   > AI components introduce a new class of architectural concerns that traditional software design doesn't address. The core challenge: outputs are non-deterministic, latency is variable, costs scale with usage, and quality degrades in ways that are hard to detect without dedicated instrumentation. The architectural decisions made here — how prompts are managed, how outputs are evaluated, how fallbacks are designed — are as consequential as database and API design decisions. Making them explicitly during architecture review, rather than discovering them during production incidents, is the point.

   Display this learning note verbatim before working through AI architecture concerns.

   **a. Model serving layer**
   - What type of AI component? (LLM generation, classification, embeddings, RAG, recommendations, vision, speech)
   - API integration vs. self-hosted model — justify against latency, cost, data privacy, and team capability
   - Synchronous vs. asynchronous — when must the user wait for AI output vs. when can processing be deferred?
   - Caching strategy — which AI outputs are safe to cache and for how long? (Identical prompts on identical inputs are often cacheable)
   - Rate limit handling — how does the system behave when AI API rate limits are hit? (queue, degrade, error)

   **b. Prompt pipeline design**
   - Where are prompts defined: inline in code, external config files, or a prompt management service?
   - How are prompts versioned — how do you roll back a bad prompt in production without a full redeploy?
   - How is context assembled — what data is injected into the prompt, from where, and in what format?
   - Token budget — what is the maximum context window consumed per call, and how is overflow handled?
   - For RAG: retrieval strategy (dense, sparse, or hybrid), chunk size, overlap, and whether reranking is applied

   **c. Evaluation and quality monitoring**
   - What does "correct" output look like — is ground truth available for automated evaluation?
   - How will AI output quality be measured in development: human eval, LLM-as-judge, or reference-based metrics?
   - How will quality be monitored in production — what signals indicate degradation (error rate, latency, user feedback, quality score)?
   - What is the evaluation cadence: per-deploy, continuous, or triggered by quality signals?

   **d. Fallback and graceful degradation**
   - What happens when the AI API is unavailable or returns an error?
   - What happens when output quality falls below threshold (low confidence, content filter triggered, timeout)?
   - Is there a non-AI fallback path that preserves core functionality for users?

   **e. AI observability**
   - What is logged per AI call: prompt, completion, model version, latency, token count, estimated cost?
   - How are AI-related errors and quality signals surfaced to the team in real time?
   - How is cost tracked and attributed — per feature, per user, per session?
   - What alerts fire if cost or error rate exceeds threshold?

   Write ADRs for each significant AI architecture decision: model provider choice, RAG vs. no RAG, prompt management approach, evaluation strategy.

8. **Write Architecture Decision Records (ADRs)** for each significant architectural choice:
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
7. Prompt the user: *"Run `/dev-workflow-kit:log [one-line summary]` to record this in the work log — e.g. `/dev-workflow-kit:log Completed arch design for [feature name]`"*
