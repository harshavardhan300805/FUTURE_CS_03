# Cyber Security Task 3 – API Security Risk Analysis

**Future Interns Cyber Security Internship 2026**
**Author:** Harsha Vardhan
**Target API:** [JSONPlaceholder](https://jsonplaceholder.typicode.com) (public demo API)
**Tool:** Postman
**Testing date:** 01 October 2026

---

## Overview

This repository contains a read-only security risk analysis of JSONPlaceholder, a free public REST API built for testing and prototyping. The assessment reviews authentication, access control, data exposure, HTTP response headers, rate limiting and input handling.

**Result: No High or Medium severity vulnerability was confirmed.** The observations are Informational or Low and mostly reflect that JSONPlaceholder is an intentionally open sandbox with synthetic data. They are documented because the same patterns would matter in a production API.

## Repository Contents

```
.
├── README.md
├── API_Security_Risk_Analysis_Report.docx   # full report
└── screenshots/                             # Postman evidence (Figures 1–7)
    ├── figure-1-posts.png
    ├── figure-2-users.png
    ├── figure-3-users-1.png
    ├── figure-4-posts-1-comments.png
    ├── figure-5-response-headers.png
    ├── figure-6-authentication-no-auth.png
    └── figure-7-access-control-users-9999-404.png
```

## Scope & Ethics

**In scope (GET requests only):**

- `/posts`
- `/users`
- `/users/1`
- `/posts/1/comments`
- `/users/9999` (non-existent resource test)

**Out of scope:** write operations (POST, PUT, PATCH, DELETE), load or denial-of-service testing, injection payloads, fuzzing, brute force, and any other system.

JSONPlaceholder is a public service meant for testing and learning. Testing was limited to a few read-only requests, used no credentials or real personal data, and did not try to disrupt the service. All data returned is synthetic.

## Tools Used

| Tool | Purpose |
|---|---|
| Postman | Sending requests, inspecting status codes, bodies, timings and headers, capturing screenshots |
| JSONPlaceholder | Target public REST API |
| OWASP API Security Top 10 (2023) | Framework used to map observations |

## Methodology

1. Defined scope and rules of engagement (read-only, public demo API).
2. Sent GET requests to the in-scope endpoints in Postman.
3. Recorded status code, response time and size for each request.
4. Reviewed response bodies for the type of data returned.
5. Tested authentication with the Authorization type set to **No Auth**.
6. Tested access-control behaviour with a non-existent user ID.
7. Inspected the response headers.
8. Mapped observations to OWASP API Security Top 10 (2023) and rated severity.

## Endpoints Tested

| Endpoint | Method | Status | Time | Size | Evidence |
|---|---|---|---|---|---|
| `/posts` | GET | 200 OK | 148 ms | 7.76 KB | Figure 1 |
| `/users` | GET | 200 OK | 406 ms | 2.67 KB | Figure 2 |
| `/users/1` | GET | 200 OK | 142 ms | 1.21 KB | Figure 3 |
| `/posts/1/comments` | GET | 200 OK | 141 ms | 1.52 KB | Figure 4 |
| `/users/1` (No Auth) | GET | 200 OK | 60 ms | 1.21 KB | Figure 6 |
| `/users/9999` | GET | 404 Not Found | 642 ms | 909 B | Figure 7 |

## Authentication & Access-Control Results

- **Authentication:** `GET /users/1` with **No Auth** returned `200 OK`. This is expected for a public demo API and is not treated as a vulnerability.
- **Access control:** `GET /users/9999` returned `404 Not Found` with an empty JSON object and no sensitive error detail.
- **BOLA limitation:** Full BOLA (Broken Object Level Authorization) testing was not possible because JSONPlaceholder has no authenticated or private users, so there is no ownership boundary to test.

## Key Observations

| ID | Observation | Severity | OWASP 2023 |
|---|---|---|---|
| R-01 | Endpoints accessible without authentication (expected for a demo API) | Informational | API2 |
| R-02 | Personal-data-like fields returned (name, email, address); synthetic data | Low | API3 |
| R-03 | `Access-Control-Allow-Credentials: true` observed; needs a full CORS review | Low | API8 |
| R-04 | No rate-limit indicators observed; rate limiting not actively tested | Informational | API4 |
| R-05 | Mixed caching directives (`max-age` with `Expires: -1` / `Pragma: no-cache`) | Informational | API8 |

No findings were inflated to increase the count. Severity reflects a public sandbox and would be re-evaluated for a production API handling real customer data.

## Evidence

| Figure | Description | File |
|---|---|---|
| 1 | `GET /posts` – 200 OK | [figure-1-posts.png](screenshots/figure-1-posts.png) |
| 2 | `GET /users` – 200 OK | [figure-2-users.png](screenshots/figure-2-users.png) |
| 3 | `GET /users/1` – 200 OK | [figure-3-users-1.png](screenshots/figure-3-users-1.png) |
| 4 | `GET /posts/1/comments` – 200 OK | [figure-4-posts-1-comments.png](screenshots/figure-4-posts-1-comments.png) |
| 5 | Response headers | [figure-5-response-headers.png](screenshots/figure-5-response-headers.png) |
| 6 | Authentication – No Auth | [figure-6-authentication-no-auth.png](screenshots/figure-6-authentication-no-auth.png) |
| 7 | Access control – `/users/9999` → 404 | [figure-7-access-control-users-9999-404.png](screenshots/figure-7-access-control-users-9999-404.png) |

## Remediation Highlights (for production APIs)

- Require authentication on every endpoint that returns non-public data.
- Enforce object-level and property-level authorization on the server.
- Return only the fields each client needs; avoid exposing email and address data by default.
- Restrict CORS to an explicit origin allow-list.
- Apply per-client rate limiting and return `429` with `Retry-After`.
- Add standard security headers and keep caching directives consistent.
- Keep error responses generic and validate inputs against a schema.

## Limitations

- JSONPlaceholder is a demo API with fake data and no authentication layer, so many controls could not be meaningfully tested.
- Full BOLA testing was not possible (no authenticated or private users).
- Testing was read-only and limited to a handful of GET requests.
- Only a subset of the 22 response headers was captured, so security headers were not fully assessed.
- Rate limiting, injection and fuzzing tests were not performed, in line with the ethical scope.
- Results reflect a single test session and may change over time.

## Full Report

Detailed findings, business impact, full remediation table, OWASP mapping and screenshots are in [API_Security_Risk_Analysis_Report.docx](API_Security_Risk_Analysis_Report.docx).

## References

- [JSONPlaceholder](https://jsonplaceholder.typicode.com)
- [Postman](https://www.postman.com)
- [OWASP API Security Top 10 – 2023](https://owasp.org/API-Security/editions/2023/en/0x11-t10/)
- [OWASP REST Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/REST_Security_Cheat_Sheet.html)

## Author

**Harsha Vardhan**
GitHub: [harshavardhan300805](https://github.com/harshavardhan300805)
LinkedIn: [harsha-vardhan300805](https://linkedin.com/in/harsha-vardhan300805)

*Completed as part of the Future Interns Cyber Security Internship 2026.*

> **Disclaimer:** Educational assessment of a public demo API using read-only requests. Only test systems you own or have permission to test.
