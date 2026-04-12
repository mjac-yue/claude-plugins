---
name: api-spec
description: Generate an API specification — endpoints, request/response schemas, authentication, error handling, and versioning. Use when designing a new API or extending an existing one.
disable-model-invocation: true
---

Generate an API specification for: $ARGUMENTS

**Output standard — tables**: All documents are read in Obsidian. Always include a blank line before any Markdown table — Obsidian requires this to render `|` syntax as a table rather than plain text.

Use the template in [api-spec-template.md](api-spec-template.md) as the structure.

Follow this process:
1. **Define the API overview**:
   - Purpose: what does this API enable?
   - Base URL and version
   - Authentication method (API key, OAuth 2.0, JWT, session cookie, etc.)
   - Rate limiting and throttling rules
2. **List all endpoints**. For each endpoint, specify:
   - HTTP method and path (e.g., `POST /v1/orders`)
   - Description of what it does
   - **Request**: path params, query params, request body schema (field name, type, required/optional, constraints, example)
   - **Response**: status codes, response body schema, example response
   - **Errors**: all error codes this endpoint can return with description and recovery guidance
3. **Define shared schemas** — reusable data objects used across multiple endpoints
4. **Document error model** — global error response format, standard error codes, and what each means for the caller
5. **Specify authentication flow** — how a caller obtains credentials and includes them in requests
6. **Versioning strategy** — how breaking changes will be handled (header versioning, URL versioning, deprecation policy)
7. **Webhooks** (if applicable) — events emitted, payload schema, delivery guarantees, retry behavior
8. **Usage examples** — 2–3 end-to-end request/response examples showing the most common use cases

Use OpenAPI-compatible field names where possible. Flag any decisions that are still open (e.g., pagination style, field naming convention).

## Save output

After presenting the API specification to the user:
1. Check if a project `CLAUDE.md` exists in the current working directory or any parent directory
2. If it contains an **Output paths** table, find the row for `/api-spec` and save the output to that file path
3. Update the **Status** field to **Done** and **Last updated** to today's date at the top of the file
4. Confirm the file was written to the user
5. If no project `CLAUDE.md` exists, present the output for manual copying
