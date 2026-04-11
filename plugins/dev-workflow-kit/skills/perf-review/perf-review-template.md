# Performance Review: [Feature / System Name]

**Author**: [Name]
**Date**: [Date]
**Scope**: [What is being reviewed — feature, endpoint, service, query]
**Related ticket / PRD**: [Link]

---

## Performance Requirements

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

| Query | Table | Index used? | Rows scanned | Notes |
|-------|-------|------------|--------------|-------|
| | | Yes / No / Unknown | | |

**N+1 risks**: [Describe any patterns where queries multiply with data size]

**Scale concern**: [How does query time grow as data volume grows? At what row count does it become problematic?]

---

## Caching Analysis

| Data | Read frequency | Change frequency | Cached? | TTL | Invalidation strategy |
|------|--------------|-----------------|---------|-----|----------------------|
| | | | Yes / No | | |

**Cache hit rate expectation**: [%]
**Stale data risk**: [Is there a scenario where stale cache data causes incorrect behavior?]

---

## External Dependency Analysis

| Dependency | Called synchronously? | p50 / p95 latency | Timeout set? | Fallback if unavailable? |
|-----------|----------------------|------------------|-------------|--------------------------|
| | Yes / No | / ms | Yes / No | Yes / No — [describe] |

---

## Load & Concurrency

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

| Metric | Before | After | Delta |
|--------|--------|-------|-------|
| Bundle size (gzipped) | KB | KB | |
| Time to Interactive | s | s | |
| Largest Contentful Paint | s | s | |
| Layout shifts (CLS) | | | |

---

## Load Test Results (if available)

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

### Fix before launch (blocks SLO)
1. **[Finding]** — [Impact] — **Fix**: [Specific action]

### Fix soon (degrades at scale)
1. **[Finding]** — [Impact] — **Fix**: [Specific action]

### Monitor (acceptable now, watch post-launch)
1. **[Finding]** — [What to alert on and at what threshold]

---

## Open Questions

| Question | Owner | Due |
|----------|-------|-----|
| | | |
