# Code Review: [PR / Feature Name]

**Reviewer**: [Name]
**Date**: [Date]
**PR / Branch**: [Link]
**Author**: [Name]
**Related ticket**: [Link]

> **Learning note — Code Review**
> - **Why**: The primary quality gate before code reaches production — catches bugs, security issues, and design problems when they're cheapest to fix (in the PR, not in production)
> - **Who uses it**: Engineers learn from each other and maintain shared code ownership; Engineering leads ensure the codebase evolves consistently with architecture; PM sees the approve/request-changes verdict to assess feature readiness
> - **Key decisions**: What is the overall verdict? Which findings are blocking vs. suggestions vs. nits? Are there security or correctness issues that must fix before merge?
> - **Next step**: Author addresses blocking issues → re-review → approve → merge

---

## Summary

> **Note — Summary**: The overall verdict (Approve / Approve with comments / Request changes) is the most important output — it tells the author what action to take. Lead with the most important finding; a security issue belongs in the first sentence, not buried after readability notes.

**What this change does**: [One sentence]
**Scope**: [Files / components changed]
**Overall verdict**: Approve | Approve with comments | Request changes

**Summary**: [2–3 sentences on overall quality and the most important things to address]

> 💡 **Tip**: *[Your AI will identify the highest-risk findings in this PR given the components changed, the feature context, and the patterns in the existing codebase.]*

---

## Review Findings

> **Note — Review Findings**: Organized by category rather than file — makes it easier to assess overall quality across dimensions and prevents missing systemic issues that span multiple files. The most commonly skipped categories are Test Coverage and Error Handling, which produce more production incidents than correctness bugs.

*Severity: **Blocking** = must fix before merge | **Non-blocking** = should fix | **Nit** = optional*

### Correctness

> **Note — Correctness**: Catches logic errors, off-by-one mistakes, incorrect condition checks, and behavior diverging from requirements. Trace through edge cases — empty inputs, boundary values, concurrent access. A correctness finding caught in review is prevented quality debt.

| Severity | Location | Finding | Recommendation |
|----------|----------|---------|---------------|
| | `file.js:42` | | |

### Test Coverage

> **Note — Test Coverage**: Check that the happy path is exercised, edge cases are covered, and error states are tested. The most common gap is error state coverage — engineers write tests for what works, not for what should happen when the API is down.

| Severity | Location | Finding | Recommendation |
|----------|----------|---------|---------------|
| | | | |

**Coverage summary**:
- Happy path: Covered / Missing
- Edge cases: Covered / Missing
- Error states: Covered / Missing

### Error Handling

> **Note — Error Handling**: Check that external calls have timeouts, failed operations don't leave inconsistent state, and user-facing errors don't leak internal details. Common gaps: missing timeouts, swallowed exceptions, stack traces exposed to users.

| Severity | Location | Finding | Recommendation |
|----------|----------|---------|---------------|
| | | | |

### Security

> **Note — Security**: Security findings are always at minimum Non-blocking; a genuine vulnerability should be Blocking. The cost of a breach vastly exceeds the cost of a delayed launch. Check against OWASP Top 10 as a minimum baseline.

| Severity | Location | Finding | Recommendation |
|----------|----------|---------|---------------|
| | | | |

### Performance

> **Note — Performance**: Identify code that will be slow or expensive under production load. Most common issues: N+1 queries, missing pagination on list endpoints, synchronous calls to slow external APIs blocking the request thread.

| Severity | Location | Finding | Recommendation |
|----------|----------|---------|---------------|
| | | | |

### Readability & Maintainability

> **Note — Readability & Maintainability**: Ask: "Would a new team member understand this in six months without PR context?" The most important readability tool is naming — a well-named function eliminates the need for a comment.

| Severity | Location | Finding | Recommendation |
|----------|----------|---------|---------------|
| | | | |

### Comment Quality

| Severity | Location | Finding | Recommendation |
|----------|----------|---------|---------------|
| | | | |

### Patterns & Consistency

> **Note — Patterns & Consistency**: Ensure new code follows established codebase conventions — error handling patterns, naming, file organization. Inconsistent patterns accumulate into a codebase where every file works slightly differently, slowing new engineers and causing bugs.

| Severity | Location | Finding | Recommendation |
|----------|----------|---------|---------------|
| | | | |

---

## Blocking Issues (must fix before merge)

> **Note — Blocking Issues**: Each item should be specific enough to act on — a file:line reference and a recommended fix, not just a description of the problem. If a blocking issue requires a significant design change, a conversation may be more effective than a list item.

1. **[Issue]** — `[file:line]` — [Description and recommended fix]
2. 

## Non-Blocking Suggestions

1. **[Issue]** — `[file:line]` — [Description and recommendation]
2. 

## Nits

1. `[file:line]` — [Optional polish note]

---

## Checklist

> **Note — Checklist**: A completed checklist doesn't mean all boxes are checked — it means the reviewer explicitly considered each dimension and made a judgment call. The last three items reflect the codebase commenting standard for all new or modified files.

- [ ] Logic is correct and matches requirements
- [ ] All new behaviors have test coverage
- [ ] Error states are handled and surfaced appropriately
- [ ] No security vulnerabilities introduced
- [ ] No obvious performance regressions
- [ ] Code is readable and consistent with codebase patterns
- [ ] No dead code, debug logs, or unresolved TODOs
- [ ] Documentation updated (if public API or behavior changed)
- [ ] File-level comments present on all new/modified files
- [ ] All functions/methods have plain-English comments
- [ ] Non-obvious logic explained with inline comments
- [ ] All TODOs marked with `// TODO:` and a description
