# Usage notes

Common patterns used across all Workfront Fusion API endpoints. For more details view API reference for specific resources.

## Error Structure

All API errors follow RFC 7807 Problem Details format with `application/problem+json` content type.

**Structure:**

| Field | Type | Description |
|-------|------|-------------|
| `type` | string | Error type (e.g., "BadRequest", "Unauthorized", "Forbidden") |
| `status` | number | HTTP status code (400-599) |
| `title` | string | Human-readable error message |
| `report` | object | Contains `request-id`, `x-gw-ims-org-id`, and optional `errors` array |

**Example:**

```json
{
  "type": "BadRequest",
  "status": 400,
  "title": "Invalid request parameters",
  "report": {
    "request-id": "abc-123-def-456",
    "x-gw-ims-org-id": "1234567890ABCDEF@AdobeOrg",
    "errors": ["field must be a valid value"]
  }
}
```

## Search Query Structure

Filter resources using the `property` query parameter. Multiple filters are AND-ed together.

**Operators:**

| Operator | Description | Example |
|----------|-------------|---------|
| `==` | Equals | `property=status==active` |
| `!=` | Not equals | `property=status!=deleted` |
| `>` | Greater than | `property=createdAt>2025-01-01T00:00:00.000Z` |
| `>=` | Greater than or equal | `property=id>=1000` |
| `<` | Less than | `property=createdAt<2025-12-31T23:59:59.999Z` |
| `<=` | Less than or equal | `property=id<=100` |
| `~` | Case-insensitive regex | `property=name~test` |
| `field` | Field exists | `property=description` |
| `!field` | Field does not exist | `property=!description` |

**Example:**

```
GET /api/v3/resource?property=status==active&property=createdAt>=2025-01-01T00:00:00.000Z
```

## Pagination Structure

Cursor-based pagination with items, metadata, and navigation links.

**Request Parameters:**

| Parameter | Type | Description |
|-----------|------|-------------|
| `limit` | number | Max items per page (1-1000) |
| `start` | string | Paging cursor value from previous response |
| `orderby` | string | Sort field, prefix with `-` (desc) or `+` (asc) |

**Response Structure:**

```json
{
  "items": [...],
  "_page": {
    "orderby": "-createdAt",
    "start": "2025-12-09T11:39:34.834Z",
    "next": "2025-12-09T10:12:01.000Z",
    "property": ["status==active"],
    "count": 50
  },
  "_links": {
    "next": {
      "href": "/api/v3/resource?orderby=-createdAt&start=2025-12-09T10:12:01.000Z&limit=50"
    },
    "page": {
      "href": "/api/v3/resource{?orderby,limit,start,property}"
    }
  }
}
```

**Pagination Flow:**

1. Make initial request: `GET /api/v3/resource?orderby=-createdAt&limit=50`
2. Check if `_links.next` exists for more pages
3. Use `_page.next` value or `_links.next.href` for next request
4. When `_page.next` is `null`, you've reached the last page

**Notes:**
- `start` parameter type must match the `orderby` field type
- Timestamps must be ISO 8601 format (UTC)
- `orderby` is required when using `start` or `limit`
