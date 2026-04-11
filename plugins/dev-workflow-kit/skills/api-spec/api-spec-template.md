# API Specification: [API / Feature Name]

**Author**: [Name]
**Date**: [Date]
**Status**: Draft | In Review | Approved
**Related Tech Spec**: [Link]
**API version**: v[N]

---

## Overview

**Purpose**: [What does this API enable? Who are the consumers?]
**Base URL**: `https://api.example.com/v1`
**Protocol**: REST / GraphQL / gRPC
**Data format**: JSON

---

## Authentication

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

| Limit | Scope | Behavior when exceeded |
|-------|-------|----------------------|
| [N] requests/minute | Per API key | HTTP 429, retry-after header |

---

## Endpoints

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

**Strategy**: [URL versioning (`/v1/`) / Header versioning]
**Deprecation policy**: [e.g., 6 months notice, deprecation header on sunset date]
**Current version**: v[N]
**Breaking change definition**: [What constitutes a breaking change]

---

## Webhooks (if applicable)

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

| Question | Owner | Due | Status |
|----------|-------|-----|--------|
| | | | |
