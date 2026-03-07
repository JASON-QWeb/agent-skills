# RESTful API Design

## Description
Guidelines and patterns for designing clean, consistent, and developer-friendly RESTful APIs.

## URL Structure
```
GET    /api/v1/users          # List users
GET    /api/v1/users/:id      # Get user
POST   /api/v1/users          # Create user
PUT    /api/v1/users/:id      # Update user
DELETE /api/v1/users/:id      # Delete user
```

## Response Format
```json
{
  "data": { "id": 1, "name": "Alice" },
  "meta": { "request_id": "abc-123" }
}
```

## Error Handling
```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid email format",
    "details": [
      { "field": "email", "message": "must be a valid email address" }
    ]
  }
}
```

## Pagination
```
GET /api/v1/users?page=2&per_page=20

Response headers:
X-Total-Count: 100
Link: <...?page=3>; rel="next", <...?page=1>; rel="prev"
```

## Best Practices
1. Use plural nouns for resources
2. Version your API
3. Use HTTP status codes correctly
4. Support filtering, sorting, pagination
5. Rate limit your endpoints
