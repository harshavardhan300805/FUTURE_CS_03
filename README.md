# FUTURE_CS_02 — Phishing Email Detection & Awareness System

**Cyber Security Track — Task 2 (2026) | Future Interns**

## Objective
Analyze email samples, identify phishing indicators, classify risk, explain the attack in simple language, and create practical phishing-awareness guidance.

## Scope
Four email samples supplied in the project archive were reviewed as static evidence. The assessment covered sender identity, Reply-To, subject, message content, visible links/actions, social-engineering indicators, and risk classification.

## Samples
1. Web Developer Internship application-status email — **Suspicious / High Risk**
2. ChatGPT — “4 new image styles to try” — **Safe***
3. Swiggy — “Your A/C XXXX1234 credited…” — **Safe***
4. Emergent — “Welcome to Emergent: Your Unfair Advantage” — **Safe***

\* Safe means no strong phishing indicators were identified in the supplied evidence. It does not guarantee authenticity.

## Key Finding
The internship email presents the strongest concern because it requests a one-time registration fee as part of an internship workflow and directs the recipient to a payment link. The presence of a Razorpay `rzp.io` payment URL is not, by itself, proof of maliciousness; the opportunity and sender should be independently verified before payment.

## Methodology
1. Preserve the supplied email evidence.
2. Inspect sender and Reply-To addresses.
3. Review subject and body for social-engineering indicators.
4. Identify visible URLs and requested actions.
5. Check for requests involving credentials, OTPs, money, or sensitive data.
6. Classify risk based only on documented evidence.
7. Record limitations where raw headers/body data are unavailable.
8. Produce an awareness guide for employees.

## Tools / Resources
- PDF/static email evidence supplied for the task
- Email/header analysis tools for future raw-header verification
- Browser/domain inspection without interacting with suspicious destinations
- CISA and Google phishing-awareness guidance
- PDF/documentation tools

## Important Limitation
The supplied files are rendered PDF captures rather than complete raw `.eml` files. SPF, DKIM, DMARC, full Received headers, DNS history, and destination behavior could not be independently verified for every sample. Classifications are therefore evidence-based and provisional where stated.

## Repository Structure
```text
FUTURE_CS_02/
├── README.md
├── Report/
│   └── Phishing_Detection_Awareness_Report.pdf
├── Analysis/
│   ├── email_analysis.csv
│   ├── analysis_notes.md
│   └── risk_matrix.md
└── Evidence/
    ├── Email_Samples/
    ├── Extracted_Text/
    └── SHA256SUMS.txt
```

## Awareness Rule
**STOP → CHECK THE SENDER → INSPECT THE LINK → VERIFY INDEPENDENTLY → REPORT IF SUSPICIOUS**

## Disclaimer
This repository is for cybersecurity education, analysis, and awareness purposes. No attempt was made to access or exploit any system or suspicious destination.
