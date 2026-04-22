# Tech Stack Recommendation: [Product Name]

**Date**: [Date]
**Product type**: [Web app / Mobile / API / Extension / CLI / Hybrid]
**Builder context**: PM-led, AI-assisted build
**Scale target**: [Launch estimate] → [12-month estimate]

> **Learning note — Tech Stack Recommendation**
> - **Why**: One of the most consequential product decisions — determines what's easy, hard, or impossible for years
> - **Who uses it**: Engineers own the recommendation; PM understands and approves trade-offs; Stakeholders evaluate operational costs
> - **Key decisions**: Does this stack fit the team's skills, the product's scale requirements, and the available budget?
> - **Next step**: Approved stack decision feeds into tech spec, dev plan, and deployment guide

---

## Recommended Stack

> **Note — Recommended Stack**: Gives everyone a quick view of the full technology picture. Key question: any technology without a documented alternative is a single-point-of-choice risk — what do we do if it doesn't work out?

| Layer | Recommendation | Alternative |
|-------|---------------|-------------|
| **Frontend** | | |
| **Backend** | | |
| **Database** | | |
| **Auth** | | |
| **File storage** | | |
| **Hosting** | | |
| **CI/CD** | | |

---

## Why This Stack

> **Note — Why This Stack**: Prevents this from being a list of technology names without justification. Key discipline: PM should be able to articulate the 3 key reasons this stack was chosen. If the rationale can't be explained simply, the decision may not be well-reasoned.

> 💡 **Tip**: *[Your AI will highlight any stack choices that seem mismatched with your stated scale targets or team context, and flag where the "why" needs strengthening.]*

[2–3 sentences on the core rationale — why this combination makes sense for this product type and builder context]

### Frontend: [Recommendation]
**Why**: [1–2 sentences]
**Alternative**: [Name] — use instead if [condition]

### Backend: [Recommendation]
**Why**: [1–2 sentences]
**Alternative**: [Name] — use instead if [condition]

### Database: [Recommendation]
**Why**: [1–2 sentences]
**Alternative**: [Name] — use instead if [condition]

### Auth: [Recommendation]
**Why**: [1–2 sentences — strongly prefer managed auth; note if DIY is ever appropriate]

### Hosting: [Recommendation]
**Why**: [1–2 sentences]
**Deployment model**: [How code goes from local to live — git push, CLI deploy, etc.]

---

## Key Third-Party Services

> **Note — Key Third-Party Services**: Where most hidden costs and vendor risks live. Key decision for each service: is the managed service worth the cost and dependency risk, or should this be built in-house? For early-stage products, managed services are almost always the right call.

| Purpose | Recommended service | Why |
|---------|-------------------|-----|
| Payments | | |
| Email (transactional) | | |
| Analytics | | |
| Error monitoring | | |
| [Other relevant] | | |

---

## Cost Estimate

> **Note — Cost Estimate**: Cost estimates are often missing, leading to budget surprises at growth. Key question: are there services where cost scales with usage in a way that could become unaffordable at 10× volume? Those deserve the most scrutiny.

> 💡 **Tip**: *[Your AI will flag any services with usage-based pricing that could surprise you at growth, and suggest where to negotiate committed pricing.]*

| Tier | Assumption | Estimated monthly cost |
|------|-----------|----------------------|
| Launch (0–500 users) | [Free tier + baseline services] | $[X] – $[Y] |
| Growth (500–5,000 users) | [Scaled services, database growth] | $[X] – $[Y] |

*Main cost drivers at growth: [e.g., database compute, auth MAUs, storage]*

---

## What to Avoid

> **Note — What to Avoid**: Naming what not to do is as valuable as naming what to do — prevents paths that seem attractive but have known problems. If a stakeholder requests something in this section, this gives Engineering a documented rationale for declining.

| Technology / Pattern | Why to avoid it |
|---------------------|----------------|
| | |

---

## Trade-offs Accepted

> **Note — Trade-offs Accepted**: Every technology choice involves trade-offs. Key discipline: intellectual honesty — if a trade-off is "this won't scale past 10,000 users," name it explicitly rather than implying "we'll revisit when needed."

- **[What you're giving up]** — [Why that's acceptable at this stage]
- **[What you're giving up]** — [Why that's acceptable at this stage]

---

## Starter Setup

> **Note — Starter Setup**: Reduces the gap between "tech stack approved" and "first line of code running." If setup takes more than 30 minutes for a new engineer, simplify or document more thoroughly.

Get a skeleton running locally in these steps:

```bash
# Step 1
[command]

# Step 2
[command]

# Step 3
[command]
```

**First thing to verify it works**: [Simple smoke test — what to check]

---

## Open Questions Before Committing

> **Note — Open Questions Before Committing**: Questions where the wrong answer would change the stack recommendation. Answer these before writing any production code — rebuilding a foundation layer because a compliance requirement was discovered mid-build is expensive.

1. [Any constraint that could change the recommendation if answered differently]
2. [e.g., "Do you have an existing domain and DNS provider?"]
3. [e.g., "Is there a compliance requirement (HIPAA, SOC 2, GDPR) that affects hosting region?"]
