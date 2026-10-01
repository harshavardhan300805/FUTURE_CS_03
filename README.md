# 🔐 Cyber Security Task 3 – API Security Risk Analysis

## 📌 Overview

This project was completed as part of the **Future Interns Cyber Security Internship – Task 3 (2026)**.

The task involved performing a **read-only API Security Risk Analysis** using the **JSONPlaceholder** test API.

## 🎯 Objectives

- Analyze API endpoints
- Assess authentication and access control
- Inspect API responses and headers
- Identify potential security risks
- Suggest remediation measures

## 🛠️ Tools Used

- **Postman** – API testing and inspection
- **JSONPlaceholder** – Public test API
- **OWASP API Security Top 10** – Security reference

## 🔍 Scope

Tested read-only GET requests:

```text
GET /posts
GET /users
GET /users/1
GET /posts/1/comments
GET /users/9999
```

No exploitation, bypass attempts, flooding, or private/production API testing was performed.

## 📊 Assessment

The assessment covered:

- Authentication
- Access control
- Data exposure
- HTTP response headers
- Rate limiting considerations
- Input validation considerations

No High or Medium severity vulnerability was confirmed during the limited read-only assessment.

## 📁 Repository Structure

```text
├── README.md
├── report/
│   └── API-Security-Risk-Analysis-Task-3.pdf
└── screenshots/
    ├── 01-posts-response.png
    ├── 02-users-response.png
    ├── 03-user-response.png
    ├── 04-comments-response.png
    ├── 05-response-headers.png
    ├── authentication-assessment.png
    └── 06-access-control-test.png
```

## 📄 Detailed Report

The complete methodology, findings, screenshots, risk analysis, business impact, and remediation recommendations are available in:

**`report/API-Security-Risk-Analysis-Task-3.pdf`**

## ⚖️ Ethics

This assessment was conducted for educational purposes using a public test API and followed a read-only, non-intrusive approach.

## 👨‍💻 Author

**Harsha Vardhan**  
Future Interns – Cyber Security Internship 2026
