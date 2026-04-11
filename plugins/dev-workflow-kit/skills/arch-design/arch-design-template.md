# Architectural Design: [Feature / System Name]

**Author**: [Name]
**Date**: [Date]
**Status**: Draft | In Review | Approved
**Related PRD**: [Link]
**Related Solution Analysis**: [Link]
**Engineering Owner**: [Name]

---

## Non-Functional Requirements (NFRs)

*These drive every architectural decision. State them before making choices.*

| NFR | Requirement | Measurement | Priority |
|-----|-------------|-------------|----------|
| **Performance** | p95 latency < [X]ms | [How measured] | Must / Should / Nice |
| **Throughput** | [X] RPS sustained | Load test | Must / Should / Nice |
| **Availability** | [99.9% / 99.99%] uptime | SLO dashboard | Must / Should / Nice |
| **RTO** | Recovery within [X] min | Failover drill | Must / Should / Nice |
| **RPO** | Max [X] min data loss | Backup test | Must / Should / Nice |
| **Scalability** | Support [X]× current load by [date] | Load test | Must / Should / Nice |
| **Security** | [Compliance standard / data classification] | Security review | Must / Should / Nice |
| **Maintainability** | [New engineer productive within X days] | — | Should |
| **Testability** | [Components testable in isolation] | Test suite | Must / Should |

---

## Architectural Style

**Chosen style**: [Monolith / Layered / Microservices / Event-driven / CQRS / Hexagonal / Hybrid]

**Rationale**: [Why this style fits the NFRs and the team's operational capability. Be specific — reference the NFRs above.]

**Styles considered and rejected**:

| Style | Reason rejected |
|-------|----------------|
| | |
| | |

---

## System Context

*Where this system or feature sits in the broader landscape.*

```
[External User] → [This System] → [Downstream System A]
[External System] ↗              ↘ [Downstream System B]
```

**External actors**: [Users, external systems, or services that interact with this system]
**Trust boundaries**: [Where authentication and authorization are enforced]

---

## Component Design

### Component Overview

| Component | Responsibility | Owns | Does NOT own |
|-----------|---------------|------|-------------|
| | [Single sentence] | [Data / logic it controls] | [Explicit exclusions] |
| | | | |

### Component Details

---

#### [Component Name]

**Responsibility**: [One sentence — what is the single job of this component?]

**Public interface** (contract with other components):
- Exposes: [API endpoints / events / data / files]
- Consumes: [APIs / events / data from other components]

**Internal structure** (if non-trivial):
- [Key sub-modules or layers within this component]

**Data owned**: [Which entities or stores this component is the system of record for]

**Scaling strategy**: [How this component scales — horizontal / vertical / stateless / stateful]

---

*(Repeat for each component)*

---

## Integration Patterns

| Integration | Components | Pattern | Consistency | Failure handling |
|-------------|-----------|---------|-------------|-----------------|
| [A → B] | [From] → [To] | Sync REST / Async event / gRPC / File | Strong / Eventual | Retry + DLQ / Circuit breaker / Fallback |
| | | | | |

### Data Ownership

*Which component is the system of record for each key entity.*

| Entity | Owner | Consumers | Notes |
|--------|-------|-----------|-------|
| | | | |

---

## Cross-Cutting Concerns

### Authentication & Authorization
- **Identity provider**: [Where identities are established]
- **Enforcement point**: [Which component(s) enforce authN and authZ]
- **Authorization model**: [RBAC / ABAC / ACL / policy-based]
- **Service-to-service auth**: [mTLS / JWT / API key / none]

### Error Handling
- **Propagation strategy**: [How errors cross component boundaries — rethrow, wrap, transform]
- **User-facing errors**: [What reaches the user and how it's formatted]
- **Internal errors**: [Logged and surfaced how]

### Caching
| Cache | Layer | What is cached | TTL | Invalidation strategy |
|-------|-------|---------------|-----|----------------------|
| | CDN / App / DB | | | |

### Logging & Observability
- **Correlation**: [How requests are traced across components — trace ID propagation]
- **Log levels**: [What is logged at DEBUG / INFO / WARN / ERROR]
- **Metrics**: [Key metrics exposed per component, SLO-relevant signals]
- **Alerting**: [What conditions trigger alerts and to whom]

### Configuration Management
- **Environment config**: [How env-specific values are injected — env vars, config service, secrets manager]
- **Feature flags**: [How in-progress features are controlled — flag service, config, code]

---

## Architectural Risks

| Risk | Quality attribute | Likelihood | Impact | Mitigation |
|------|------------------|-----------|--------|------------|
| Single point of failure: [describe] | Availability | H/M/L | H/M/L | |
| Bottleneck: [describe] | Performance / Scalability | H/M/L | H/M/L | |
| Tight coupling: [describe] | Maintainability | H/M/L | H/M/L | |
| Lock-in: [describe] | Evolvability | H/M/L | H/M/L | |

---

## Architecture Decision Records (ADRs)

---

### ADR-001: [Decision title]

**Status**: Proposed | Accepted | Deprecated | Superseded by ADR-[N]

**Context**: [What situation, constraint, or requirement prompted this decision?]

**Decision**: [What was decided?]

**Rationale**: [Why? Reference specific NFRs or constraints.]

**Consequences**:
- Positive: [What this makes easier]
- Negative: [What this makes harder or more expensive]

**Alternatives considered**:
| Alternative | Reason rejected |
|-------------|----------------|
| | |

---

### ADR-002: [Decision title]

**Status**:
**Context**:
**Decision**:
**Rationale**:
**Consequences**:
- Positive:
- Negative:

**Alternatives considered**:
| Alternative | Reason rejected |
|-------------|----------------|
| | |

---

*(Add ADRs for each significant architectural choice)*

---

## Open Questions

| Question | Impact on architecture | Owner | Due |
|----------|----------------------|-------|-----|
| | | | |
