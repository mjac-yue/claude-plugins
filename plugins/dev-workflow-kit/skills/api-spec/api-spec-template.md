# API Specification: [API / Feature Name]

**Author**: [Name]
**Date**: [Date]
**Status**: Draft | In Review | Approved
**Related Tech Spec**: [Link]
**API version**: v[N]

> **Learning note — API Specification**
> - **Why**: The contract between teams that build an API and teams that consume it — changes after consumers build against it are breaking changes that require versioning
> - **Who uses it**: Backend engineers implement against it; frontend engineers and partners build integrations; QA designs integration tests from it
> - **Key decisions**: What constitutes a breaking change? How are credentials obtained and passed? What are the rate limits and error codes?
> - **Next step**: Approved spec → implementation; any post-approval changes require a versioning decision

---

## Overview

> **Note — Overview**: The "who are the consumers" answer shapes every design decision — a public API for third-party developers has different versioning, documentation, and stability requirements than an internal API consumed only by a frontend team.

**Purpose**: [What does this API enable? Who are the consumers?]
**Base URL**: `https://api.example.com/v1`
**Protocol**: REST / GraphQL / gRPC
**Data format**: JSON

---

## Authentication

> **Note — Authentication**: The "how to obtain credentials" and "how to include in requests" steps are the most important for consumer onboarding — missing or unclear instructions are the top source of integration support requests.

**Method**: [API Key / OAuth 2.0 / JWT / Session cookie]

**How to obtain credentials**:
1. 
2. 

**How to include in requests**:
```
Authorization: Bearer <token>
```

**Token expiry**: [Duration and refresh behavior]

---

## Rate Limiting

> **Note — Rate Limiting**: Consumers need to understand limits so they can design integrations to avoid hitting them (through caching, batching, or backoff). The "behavior when exceeded" column is critical — a 429 without a retry-after header will cause consumers to spin in a tight loop.

| Limit | Scope | Behavior when exceeded |
|-------|-------|----------------------|
| [N] requests/minute | Per API key | HTTP 429, retry-after header |

---

## Endpoints

> **Note — Endpoints**: Each endpoint block should be complete enough that a consumer can integrate without asking questions — every parameter type, required/optional status, constraint, and error code. The most common spec gaps are missing error codes and underspecified field constraints.

> 💡 **Tip**: *[Your AI will flag any endpoint design inconsistencies, missing error codes, or field constraints that could cause integration problems for consumers of this specific API.]*

---

### [Method] [Path]

**Description**: [What this endpoint does]

**Authentication required**: Yes / No

#### Request

**Path Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | string (UUID) | Yes | |

**Query Parameters**:

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `page` | integer | No | 1 | |
| `limit` | integer | No | 20 | Max 100 |

**Request Body**:

```json
{
  "field_name": "string",
  "count": 0,
  "nested": {
    "key": "value"
  }
}
```

| Field | Type | Required | Constraints | Description |
|-------|------|----------|-------------|-------------|
| `field_name` | string | Yes | Max 255 chars | |
| `count` | integer | No | Min 0 | |

#### Response

**Success — HTTP 200**:

```json
{
  "id": "uuid",
  "field_name": "string",
  "created_at": "2026-01-01T00:00:00Z"
}
```

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | |
| `created_at` | ISO 8601 string | UTC timestamp |

**Errors**:

| Status | Code | Message | When |
|--------|------|---------|------|
| 400 | `INVALID_REQUEST` | [Description] | Missing/invalid field |
| 401 | `UNAUTHORIZED` | [Description] | Bad or expired token |
| 403 | `FORBIDDEN` | [Description] | Insufficient permissions |
| 404 | `NOT_FOUND` | [Description] | Resource doesn't exist |
| 429 | `RATE_LIMITED` | [Description] | Too many requests |
| 500 | `INTERNAL_ERROR` | [Description] | Server error |

---

*(Repeat endpoint block for each endpoint)*

---

## Shared Schemas

> **Note — Shared Schemas**: A change to a shared schema is a breaking change to every endpoint that uses it — this is why versioning policy must be defined before the API is consumed externally.

### [SchemaName]

```json
{
  "id": "uuid",
  "name": "string",
  "status": "active | inactive"
}
```

| Field | Type | Description |
|-------|------|-------------|
| | | |

---

## Error Response Format

> **Note — Error Response Format**: A consistent error envelope allows consumers to write a single error-handling function that works for every API error. The `code` field is the most important — machine-readable codes allow consumers to handle specific failure modes rather than generic messages.

All errors return the same envelope:

```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable description",
    "details": {}
  }
}
```

---

## Versioning

> **Note — Versioning**: Engineers need a clear definition of breaking vs. non-breaking changes; consumers need a deprecation policy to plan migrations. URL versioning (`/v1/`) is simpler than header versioning — the deprecation timeline should be long enough for consumers to migrate (typically 3–6 months minimum for external APIs).

> 💡 **Tip**: *[Your AI will recommend an appropriate versioning strategy and deprecation timeline based on your consumer profile and the stability requirements of this specific API.]*

**Strategy**: [URL versioning (`/v1/`) / Header versioning]
**Deprecation policy**: [e.g., 6 months notice, deprecation header on sunset date]
**Current version**: v[N]
**Breaking change definition**: [What constitutes a breaking change]

---

## Webhooks (if applicable)

> **Note — Webhooks**: Three most important things to specify: delivery semantics (at-least-once means duplicates are possible and consumers must be idempotent), retry policy, and verification (consumers must validate HMAC signatures or accept spoofed events).

### [Event Name]

**Trigger**: [When this event fires]

**Payload**:
```json
{
  "event": "event.name",
  "timestamp": "2026-01-01T00:00:00Z",
  "data": {}
}
```

**Delivery**: [At-least-once / exactly-once]
**Retry policy**: [N retries over Y hours with exponential backoff]
**Verification**: [HMAC signature header name and algorithm]

---

## Usage Examples

> **Note — Usage Examples**: A concrete `curl` command with a real-looking request and response is more useful than the most thorough parameter table — consumers copy-paste them as starting points. If you can't write a concise example, the endpoint design may be too complex.

### Example 1: [Common use case]

**Request**:
```bash
curl -X POST https://api.example.com/v1/resource \
  -H "Authorization: Bearer <token>" \
  -H "Content-Type: application/json" \
  -d '{"field": "value"}'
```

**Response**:
```json
{
  "id": "abc-123",
  "field": "value"
}
```

---

## Open Questions

> **Note — Open Questions**: Every unresolved question here is a potential breaking change later if the wrong assumption is baked into consumer integrations. Resolve before implementation begins.

| Question | Owner | Due | Status |
|----------|-------|-----|--------|
| | | | |
