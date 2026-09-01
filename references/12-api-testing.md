# WSTG-APIT — API Testing

| ID | Title | What it verifies |
|---|---|---|
| WSTG-APIT-00 | API Testing Overview (background, not a test) | — |
| WSTG-APIT-01 | API Reconnaissance | API surface is fully enumerated (OpenAPI/Swagger/GraphQL introspection, undocumented endpoints, versioned/shadow APIs) |
| WSTG-APIT-02 | API Broken Object Level Authorization | Endpoints that take an object ID enforce that the caller is authorized for *that specific* object (BOLA/IDOR at the API layer) |
| WSTG-APIT-03 | Testing for Excessive Data Exposure | Responses return only the fields the client needs, not entire internal objects the client-side then filters |
| WSTG-APIT-04 | API Broken Function Level Authorization | Admin/privileged endpoints/functions aren't reachable by lower-privileged callers who know or guess the route |
| WSTG-APIT-99 | Testing GraphQL | GraphQL-specific risks: introspection exposure in production, query depth/complexity limits, batching abuse, field-level authorization |

Note: several other WSTG categories apply equally to APIs (Authentication, Session/Token handling,
Input Validation, SSRF, Mass Assignment, Rate limiting under Business Logic) — for an API-only
target, walk this category plus the applicable tests from those, not this category alone.
