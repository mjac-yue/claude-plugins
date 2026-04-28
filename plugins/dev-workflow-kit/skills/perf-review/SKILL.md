---
name: perf-review
description: Conduct a performance review for a feature or system — covering latency targets, load test results, query analysis, caching, and bottleneck identification. Use before launch or when a performance issue is suspected.
disable-model-invocation: true
---

Conduct a performance review for: $ARGUMENTS

> **Learning note — Performance Review**
> Performance problems are often invisible until they're catastrophic — queries that are fast with 100 rows become unusably slow with 100,000, and latency that's imperceptible with 10 users becomes frustrating at 1,000. A structured performance review identifies bottlenecks on the critical path, missing database indexes, and scale risks before users encounter them. Many performance fixes are cheap at design time and expensive after launch — especially database schema decisions that require migrations on production data.

Display the learning note above verbatim to the user before proceeding.

Use the template in [perf-review-template.md](perf-review-template.md) as the structure.

Follow this process:
1. **Define performance requirements** — what are the stated latency, throughput, and availability targets? If none exist, propose reasonable targets based on the feature type (interactive UI, batch job, API, etc.).
2. **Identify the critical path** — trace the request or operation from start to finish. List every step that adds latency (DB queries, external API calls, computation, serialization, network hops).
3. **Database & query analysis**:
   - Are queries hitting indexes?
   - Are there N+1 query patterns?
   - What is the expected data volume, and how does query time scale with it?
   - Are there missing indexes for common query patterns?
4. **Caching analysis**:
   - What data is read frequently and changes infrequently — should it be cached?
   - What is the cache hit rate expectation?
   - What is the cache invalidation strategy, and does it risk stale data?
5. **External dependencies**:
   - Which external services are called synchronously in the critical path?
   - What are their p50/p95/p99 latencies?
   - What happens to user experience when they are slow or unavailable?
6. **Load & concurrency**:
   - What is the expected requests-per-second at peak?
   - Are there shared resources (DB connections, rate-limited APIs) that become bottlenecks under load?
   - Are there locking or contention issues?
7. **Frontend performance** (if applicable):
   - Bundle size impact
   - Time to interactive effect
   - Render performance (reflows, expensive re-renders)
8. **Load test results** (if available) — summarize results, compare to targets, flag any SLO violations.
9. **Recommendations** — prioritize by impact. Distinguish between: fix before launch (blocks SLO) / fix soon (degrades at scale) / monitor (acceptable now, watch).

Output a performance review with findings ranked by impact and concrete next steps.

## Save output

After presenting the performance review to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/perf-review` and save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. In that same project `CLAUDE.md`, find the **Project status** table and set the **Status** column to **Done** for the row matching this deliverable
5. Confirm the file was written to the user
6. If no project `CLAUDE.md` exists, present the output for manual copying
