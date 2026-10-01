# 🔐 Cyber Security Task 3 – API Security Risk Analysis

## 📌 Project Overview

This project was completed as part of the **Future Interns Cyber Security Internship – Task 3 (2026)**.

The objective of this task was to perform a **read-only API Security Risk Analysis** on a public/test API, identify common API security risks, assess authentication and access-control considerations, inspect API responses and headers, and provide practical remediation recommendations.

The assessment was performed using **Postman** against the **JSONPlaceholder** test API.

---

## 🎯 Objectives

The assessment focused on:

- Analyzing a public/test API
- Reviewing API endpoints and responses
- Assessing authentication requirements
- Assessing access-control considerations
- Reviewing API response data
- Inspecting HTTP response headers
- Considering rate-limiting controls
- Identifying security risks
- Classifying risk severity
- Explaining potential business impact
- Providing remediation recommendations

The assessment was performed using a **safe, read-only methodology**.

---

## 🌐 API Tested

**API:** JSONPlaceholder

**Base URL:**  
https://jsonplaceholder.typicode.com/

JSONPlaceholder is a public fake REST API designed for testing, learning, and prototyping.

No private or production API was tested.

---

## 🛠️ Tools Used

### Postman

Used for:

- Sending API requests
- Inspecting HTTP status codes
- Reviewing JSON responses
- Checking authentication settings
- Inspecting HTTP response headers

### OWASP API Security

Used as a reference for common API security risks and security concepts.

---

## 🔍 Scope

### In Scope

The following read-only endpoints were tested:

```text
GET /posts
GET /users
GET /users/1
GET /posts/1/comments
GET /users/9999
```

The assessment also included:

- Authentication inspection
- Access-control assessment
- Response-data inspection
- HTTP-header inspection
- Security-risk analysis
- Risk classification
- Remediation recommendations

### Out of Scope

The following activities were **not performed**:

- Exploitation
- Authentication bypass
- Credential attacks
- Token attacks
- Denial-of-service testing
- Flooding or high-volume requests
- Destructive API operations
- Private API testing
- Production API testing
- Intrusive injection testing

---

## 🧪 Methodology

The assessment followed these steps:

1. Selected JSONPlaceholder as a safe public test API.
2. Reviewed the available API endpoints.
3. Sent read-only GET requests using Postman.
4. Inspected HTTP status codes and JSON responses.
5. Checked authentication requirements.
6. Inspected HTTP response headers.
7. Performed a basic access-control observation.
8. Reviewed potential API security risks.
9. Classified the observations.
10. Prepared remediation recommendations.

---

## 📊 Endpoints Tested

| # | Method | Endpoint | Result |
|---|---|---|---|
| 1 | GET | `/posts` | 200 OK |
| 2 | GET | `/users` | 200 OK |
| 3 | GET | `/users/1` | 200 OK |
| 4 | GET | `/posts/1/comments` | 200 OK |
| 5 | GET | `/users/9999` | 404 Not Found |

---

## 🔐 Authentication Assessment

The `/users/1` endpoint was tested without providing an API key, session token, or authentication credentials.

The Postman request used:

```text
Authorization: No Auth
```

The endpoint returned:

```text
200 OK
```

### Assessment

The endpoint is publicly accessible without authentication.

Because JSONPlaceholder is intentionally designed as a public test API, this behavior is treated as an expected characteristic of the test environment rather than a confirmed production vulnerability.

### Production Recommendation

A production API containing sensitive or private information should:

- Require authentication
- Validate credentials server-side
- Use secure authentication tokens
- Apply appropriate token expiration and rotation
- Protect sensitive endpoints from unauthenticated access

---

## 🔒 Access-Control Assessment

The following endpoint was tested:

```text
GET /users/1
```

A second read-only request was made using:

```text
GET /users/9999
```

The API returned:

```text
404 Not Found
```

This demonstrates how the API handles a nonexistent object identifier.

However, this **does not prove that object-level authorization is secure**.

JSONPlaceholder does not provide authenticated users or private resources, so a complete test of whether one authenticated user could access another user's private resource could not be performed.

### Conclusion

**No Broken Object Level Authorization vulnerability is claimed.**

### Production Recommendation

A real SaaS API should:

- Authenticate the requesting user
- Check the user's permissions
- Verify ownership or access rights
- Perform authorization server-side
- Deny unauthorized object access

---

## 📦 Data Exposure Assessment

The `/users` and `/users/1` responses return multiple user-related properties, including:

- ID
- Name
- Username
- Email
- Address
- Geographic information

Because JSONPlaceholder uses fake test data and is intentionally public, this was treated as a **data-exposure observation rather than a confirmed sensitive-data vulnerability**.

### Production Recommendation

Production APIs should:

- Return only required fields
- Minimize sensitive information
- Apply authorization before returning protected properties
- Separate public and private information where appropriate

---

## 🧱 HTTP Header Assessment

HTTP response headers were inspected using Postman.

Headers observed included:

- `Content-Type`
- `Access-Control-Allow-Credentials`
- `Cache-Control`
- `Content-Encoding`
- `ETag`
- `Expires`
- `Pragma`

No exploitation of CORS, caching, or other configuration behavior was performed.

### Production Recommendation

Production APIs should regularly review:

- HTTPS configuration
- CORS policies
- Cache-control settings
- Content-Type handling
- Security-related HTTP headers
- Unnecessary information disclosure

---

## 🚦 Rate Limiting

No high-volume or stress testing was performed because the assessment was intentionally read-only and non-intrusive.

Therefore, the effectiveness of rate limiting could not be confirmed.

### Production Recommendation

Production APIs should implement:

- Request-rate limits
- Per-user or per-token controls
- Request-size limits
- Monitoring
- Alerting
- Throttling

---

## 🧪 Input Validation

No confirmed input-validation vulnerability was identified.

The assessment remained read-only and did not perform intrusive injection or malformed-input testing.

### Production Recommendation

Production APIs should validate:

- Data types
- Input formats
- Input length
- Allowed values
- Request size
- Required fields

---

## ⚠️ Risk Summary

| ID | Area | Observation | Severity |
|---|---|---|---|
| API-01 | Authentication | Public endpoint does not require authentication | Low / Informational |
| API-02 | Data Exposure | Multiple user-related properties returned | Low |
| API-03 | Authorization | Full object-level authorization could not be tested | Not Assessed |
| API-04 | Rate Limiting | No stress testing performed | Not Assessed |
| API-05 | Headers | HTTP response headers inspected | Informational |
| API-06 | HTTPS | Requests performed over HTTPS | Positive |

**No High or Medium severity vulnerability was confirmed during this limited read-only assessment.**

---

## 💼 Business Impact

In a real production API, insufficient authentication, authorization, or data minimization could potentially result in:

- Unauthorized information disclosure
- Privacy concerns
- Compliance issues
- API abuse
- Increased infrastructure costs
- Loss of customer trust
- Reputational damage

These are potential production scenarios and were **not confirmed impacts of JSONPlaceholder**.

---

## 🛠️ Remediation Recommendations

1. Implement strong authentication for protected endpoints.
2. Enforce object-level authorization.
3. Minimize API response data.
4. Protect sensitive properties.
5. Implement appropriate rate limiting.
6. Review CORS configuration.
7. Review HTTP security headers and caching.
8. Maintain an accurate API inventory.
9. Monitor API activity and unusual behavior.
10. Perform regular authorized security testing.

---

## 📚 OWASP API Security Mapping

| OWASP Category | Assessment |
|---|---|
| API1:2023 Broken Object Level Authorization | Not conclusively assessed |
| API2:2023 Broken Authentication | Public test API; authentication not required |
| API3:2023 Broken Object Property Level Authorization | Data exposure considered; no confirmed vulnerability |
| API4:2023 Unrestricted Resource Consumption | Not assessed through stress testing |
| API5:2023 Broken Function Level Authorization | Not assessed |
| API6:2023 Sensitive Business Flows | Not applicable |
| API7:2023 Server Side Request Forgery | Not tested |
| API8:2023 Security Misconfiguration | Basic response configuration reviewed |
| API9:2023 Improper Inventory Management | Documented endpoints reviewed |
| API10:2023 Unsafe Consumption of APIs | Not assessed |

---

## 📸 Evidence

The `screenshots` folder contains the Postman evidence collected during the assessment:

```text
screenshots/
│
├── 01-posts-response.png
├── 02-users-response.png
├── 03-user-response.png
├── 04-comments-response.png
├── 05-response-headers.png
├── authentication-assessment.png
└── 06-access-control-test.png
```

### Evidence includes:

1. `/posts` API response
2. `/users` API response
3. `/users/1` API response
4. `/posts/1/comments` API response
5. HTTP response headers
6. Authentication assessment
7. Access-control test

---

## 📁 Repository Structure

```text
cyber-security-task-3-api-security/
│
├── README.md
│
├── report/
│   └── API-Security-Risk-Analysis-Task-3.pdf
│
└── screenshots/
    ├── 01-posts-response.png
    ├── 02-users-response.png
    ├── 03-user-response.png
    ├── 04-comments-response.png
    ├── 05-response-headers.png
    ├── authentication-assessment.png
    └── 06-access-control-test.png
```

---

## ⚖️ Ethics and Responsible Testing

This project was conducted for educational purposes using a public test API.

Only read-only requests were performed.

No:

- Exploitation
- Authentication bypass
- Credential attacks
- Denial-of-service testing
- Flooding
- Destructive operations
- Private API testing

were performed.

The assessment focuses on identifying security risks and recommending defensive improvements rather than exploiting systems.

---

## 📄 Report

The complete API Security Risk Analysis report is available at:

```text
report/API-Security-Risk-Analysis-Task-3.pdf
```

The report contains:

- Executive Summary
- Objective
- Scope
- Methodology
- API testing results
- Authentication assessment
- Access-control assessment
- Data exposure assessment
- Header analysis
- Risk classification
- Business impact
- Remediation recommendations
- OWASP mapping
- Limitations
- Screenshot evidence

---

## 📚 References

- JSONPlaceholder: https://jsonplaceholder.typicode.com/
- OWASP API Security Project: https://owasp.org/projects/api-security-project
- OWASP API Security Top 10: https://owasp.org/API-Security/
- Future Interns – Cyber Security Task 3

---

## 👨‍💻 Author

**Harsha Vardhan**

Cyber Security Internship – Future Interns  
**Task 3: API Security Risk Analysis**

---

⭐ This project demonstrates practical experience with API testing, security analysis, authentication assessment, access-control considerations, HTTP response inspection, risk classification, and professional security documentation.
