# Appendix – API (Expanded)

## Conventions
- Base: `https://<site>/.netlify/functions`
- Headers: `Content-Type: application/json`
- Auth: admin endpoints protected (token/session) – details in Admin doc

## Endpoints

### POST /api/applications
Creates a new application.

Request
```json
{
  "companyName": "ABC Manufacturing",
  "regNo": "123-45-67890",
  "industry": "Electronics",
  "contact": {"name": "John Kim", "email": "john@example.com", "phone": "+82-2-1234-5678"},
  "iso": ["ISO 9001", "ISO 14001"],
  "employeeCount": 250,
  "sites": 3,
  "scope": "Electronic component manufacturing",
  "language": "en"
}
```
Response (201)
```json
{ "id": "app_2025_00123", "status": "created" }
```

### GET /api/applications?query=abc&limit=20&page=1
Search/paginate applications.

Response (200)
```json
{ "items": [{ "id": "app_...", "companyName": "ABC Manufacturing", "status": "Pending" }], "page": 1, "total": 94 }
```

### POST /api/quotations/:id
Generate a quotation DOCX for an application id.

Response (200)
- Content-Type: `application/vnd.openxmlformats-officedocument.wordprocessingml.document`
- Body: binary stream (download)

### GET /api/reports/:id
Generate a company sales report (HTML).

Response (200)
- Content-Type: `text/html`
- Body: HTML string (new tab)

## Error Model
```json
{ "error": { "code": "VALIDATION_ERROR", "message": "email invalid", "details": {"field": "contact.email"} } }
```

### Error Codes
- `VALIDATION_ERROR` (400)
- `NOT_FOUND` (404)
- `RATE_LIMITED` (429)
- `INTERNAL_ERROR` (500)

## Rate Limiting
- Quotation/report generation: per-admin daily caps; headers `X-RateLimit-Remaining`, `Retry-After`

## Idempotency
- For create endpoints, clients may send `Idempotency-Key` header to prevent duplicates.
