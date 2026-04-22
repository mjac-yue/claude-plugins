# Performance Review: [Feature / System Name]

**Author**: [Name]
**Date**: [Date]
**Scope**: [What is being reviewed — feature, endpoint, service, query]
**Related ticket / PRD**: [Link]

> **Learning note — Performance Review**
> - **Why**: Evaluates whether a feature will meet latency, throughput, and availability requirements under real-world load — before users encounter problems
> - **Who uses it**: Engineers identify bottlenecks before launch; Engineering leads make go/no-go decisions; PM evaluates whether the feature meets product commitments (e.g., "search results appear in under 500ms")
> - **Key decisions**: Does the system meet its SLOs? What must be fixed before launch vs. monitored post-launch?
> - **Next step**: Fix-before-launch items resolved → re-review; fix-soon items tracked in backlog; monitoring thresholds set for watch items

---

## Performance Requirements

> **Note — Performance Requirements**: Percentile latency targets matter more than averages — a 50ms average but 5-second p99 is broken for 1% of users. The "Targets source" field matters — a PRD target is a product commitment; one from engineering judgment can be revised.

| Metric | Target | Current / Measured | Status |
|--------|--------|-------------------|--------|
| p50 latency | < ms | ms | Pass / Fail / Unknown |
| p95 latency | < ms | ms | Pass / Fail / Unknown |
| p99 latency | < ms | ms | Pass / Fail / Unknown |
| Throughput (RPS) | ≥ | | Pass / Fail / Unknown |
| Error rate under load | < % | % | Pass / Fail / Unknown |
| Availability / uptime | ≥ % | | Pass / Fail / Unknown |

**Targets source**: [PRD SLO / engineering decision / industry standard]

---

## Critical Path Analysis

> **Note — Critical Path Analysis**: Traces every step between request and response. The most common surprises are external API calls adding hundreds of milliseconds, and database queries fast on small datasets but slow as data grows.

> 💡 **Tip**: *[Your AI will identify which steps in your critical path are most likely to become bottlenecks given the expected load and data volumes for this specific feature.]*

*Every step from request entry to response, with estimated latency contribution.*

| Step | Type | Estimated latency | Notes |
|------|------|------------------|-------|
| [Auth middleware] | Compute | ~Xms | |
| [DB query: fetch user] | Database | ~Xms | Indexed on `user_id` |
| [External API call] | Network | ~Xms | p95 per vendor docs |
| [Response serialization] | Compute | ~Xms | |
| **Total** | | **~Xms** | |

**Bottlenecks identified**: [Which steps dominate latency?]

---

## Database & Query Analysis

> **Note — Database & Query Analysis**: A full table scan on a 10M-row table is catastrophic. The "Scale concern" field forces thinking beyond current data volume — a query fast with 10,000 rows may be unusably slow at 1,000,000.

| Query | Table | Index used? | Rows scanned | Notes |
|-------|-------|------------|--------------|-------|
| | | Yes / No / Unknown | | |

**N+1 risks**: [Describe any patterns where queries multiply with data size]

**Scale concern**: [How does query time grow as data volume grows? At what row count does it become problematic?]

---

## Caching Analysis

> **Note — Caching Analysis**: The most common caching mistakes are caching user-specific data globally (serving one user's data to another) and caching mutable state without invalidation. The stale data risk field is the most important for PMs to evaluate.

| Data | Read frequency | Change frequency | Cached? | TTL | Invalidation strategy |
|------|--------------|-----------------|---------|-----|----------------------|
| | | | Yes / No | | |

**Cache hit rate expectation**: [%]
**Stale data risk**: [Is there a scenario where stale cache data causes incorrect behavior?]

---

## External Dependency Analysis

> **Note — External Dependency Analysis**: External dependencies are the most unpredictable latency sources — outside the team's control and varying with their own load. An external call without a timeout can hang indefinitely; without a fallback, the entire feature becomes unavailable when the dependency goes down.

| Dependency | Called synchronously? | p50 / p95 latency | Timeout set? | Fallback if unavailable? |
|-----------|----------------------|------------------|-------------|--------------------------|
| | Yes / No | / ms | Yes / No | Yes / No — [describe] |

---

## Load & Concurrency

> **Note — Load & Concurrency**: Systems that look fast in single-user testing can become unresponsive under concurrent write load. Contention and locking risks are especially important for write-heavy workflows.

**Peak expected load**: [RPS or concurrent users]
**Shared resource constraints**:

| Resource | Limit | Behavior at limit |
|----------|-------|------------------|
| DB connection pool | [N connections] | Queue / error |
| External API rate limit | [N req/min] | 429 returned |
| [Other] | | |

**Contention / locking risks**: [Any shared state that serializes requests?]

---

## Frontend Performance (if applicable)

> **Note — Frontend Performance**: Core Web Vitals (TTI, LCP, CLS) correlate directly with user drop-off and conversion rates. Before/after columns allow the team to quantify the performance impact of a change and catch regressions before deployment.

| Metric | Before | After | Delta |
|--------|--------|-------|-------|
| Bundle size (gzipped) | KB | KB | |
| Time to Interactive | s | s | |
| Largest Contentful Paint | s | s | |
| Layout shifts (CLS) | | | |

---

## Load Test Results (if available)

> **Note — Load Test Results**: Empirical evidence of system behavior under sustained and peak load — validates or invalidates the performance requirements at the top of this document. "Notable findings" should explain anything unexpected.

**Tool**: [k6 / Locust / JMeter / etc.]
**Test scenario**: [Description — ramp-up, peak, duration]
**Date run**: [Date]

| Scenario | RPS | p50 | p95 | p99 | Error rate | Pass/Fail |
|----------|-----|-----|-----|-----|------------|----------|
| Baseline | | | | | | |
| Peak load | | | | | | |
| Spike | | | | | | |

**Notable findings**: [Anything unexpected in the results]

---

## Recommendations

> **Note — Recommendations**: Be specific — "add a composite index on (user_id, created_at) to reduce scan from 50K to 200 rows" is actionable; "optimize the query" is not. PM uses this section for go/no-go decisions.

> 💡 **Tip**: *[Your AI will prioritize recommendations by impact and identify which fixes will give the greatest latency improvement for the effort required.]*

### Fix before launch (blocks SLO)
1. **[Finding]** — [Impact] — **Fix**: [Specific action]

### Fix soon (degrades at scale)
1. **[Finding]** — [Impact] — **Fix**: [Specific action]

### Monitor (acceptable now, watch post-launch)
1. **[Finding]** — [What to alert on and at what threshold]

---

## Open Questions

> **Note — Open Questions**: Any question that would change a "Pass" to "Fail" or move a recommendation from "Monitor" to "Fix before launch" should be resolved before the review is finalized.

| Question | Owner | Due |
|----------|-------|-----|
| | | |
