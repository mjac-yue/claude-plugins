---
name: code-review
description: Produce a structured code review checklist and findings for a pull request or code change. Covers correctness, test coverage, error handling, readability, and adherence to patterns. Use when preparing for or conducting a PR review.
disable-model-invocation: true
---

Conduct a code review for: $ARGUMENTS

> **Learning note — Code Review**
> Code review is the quality gate before code becomes part of the product. A structured review catches bugs, security vulnerabilities, and maintainability problems that the original author missed — because it's almost impossible to spot your own assumptions. Reviews are also how knowledge spreads: the reviewer learns about changes they'll need to maintain, and the author learns patterns from feedback. Bugs found in code review are orders of magnitude cheaper to fix than the same bugs found in production.

Use the template in [code-review-template.md](code-review-template.md) as the structure.

Follow this process:
1. **Understand the change** — what is this PR trying to accomplish? What is the stated scope? Read the description and linked ticket before evaluating the code.
2. **Correctness**:
   - Does the implementation match the requirements?
   - Are there logic errors, off-by-one mistakes, or incorrect conditionals?
   - Are race conditions or concurrency issues possible?
   - Is mutable state handled safely?
3. **Test coverage**:
   - Are new behaviors covered by tests?
   - Do tests cover happy path, edge cases, and error states?
   - Are the tests meaningful (do they actually verify behavior, not just execute code)?
   - Are any tests brittle or overly coupled to implementation details?
4. **Error handling**:
   - Are all failure modes handled explicitly?
   - Are errors surfaced to the caller or logged appropriately — not silently swallowed?
   - Are user-facing error messages helpful?
5. **Security**:
   - Is user input validated and sanitized?
   - Are there any obvious injection vectors (SQL, command, XSS)?
   - Is sensitive data (tokens, PII) handled correctly — not logged, not exposed?
   - Are authorization checks in place for every operation?
6. **Performance**:
   - Are there N+1 queries or unnecessary repeated computation?
   - Are expensive operations cached where appropriate?
   - Are database queries indexed?
7. **Readability & maintainability**:
   - Are names (variables, functions, classes) clear and consistent with the codebase?
   - Is there dead code, commented-out code, or TODOs that should be resolved?

8. **Comment quality** (required for PM-led builds):
   - Does every file have a file-level comment explaining its purpose and role in the system?
   - Does every function/method have a comment explaining what it does, its parameters, and return value in plain English?
   - Are non-obvious logic blocks explained with inline comments that describe *why*, not just *what*?
   - Are long files or functions divided into named sections with comment headers?
   - When a specific approach was chosen over an obvious alternative, is that choice noted?
   - Are all TODOs marked with `// TODO:` and a description?
   - Flag missing comments as **Non-blocking** issues — they don't break behavior but impede learning and future maintenance.
9. **Patterns & consistency**:
   - Does the code follow the established patterns in this codebase?
   - Are there better abstractions already available that should be used?
   - Does the change introduce unnecessary coupling or complexity?

For each finding, assign a severity:
- **Blocking**: Must fix before merge (correctness bug, security issue, missing critical test)
- **Non-blocking**: Should fix but can merge (style, minor improvement, suggestion, missing comments)
- **Nit**: Optional polish

Output a review ready to post as PR feedback.
