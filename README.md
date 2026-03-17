# FUTURE_CS_03: API Security Risk Analysis

## Project Overview
This task involved performing a read-only API Security Risk Analysis on the **ReqRes.in** public API. The goal was to identify common vulnerabilities related to the OWASP API Security Top 10, focusing on authentication, header security, and information disclosure.

## Tools Used
* **Postman:** For API request testing and response analysis.
* **Browser DevTools:** For monitoring network traffic and header inspection.

## Methodology
- **Scope:** Public API Testing (https://reqres.in)
- **Approach:** Black-box, Read-only Audit
- **Focus:** Authentication flow, HTTP headers, and error handling logic.

## Risk Analysis Findings

| Vulnerability | Severity | Evidence | Remediation |
| :--- | :--- | :--- | :--- |
| **Information Disclosure** | Low | `Server: cloudflare` & `Via: heroku-router` revealed | Mask server headers to prevent fingerprinting. |
| **Missing Security Headers** | Medium | `Strict-Transport-Security (HSTS)` missing | Implement HSTS to force secure HTTPS connections. |
| **Verbose Error Handling** | Low | Internal URLs and hints in `403/401` JSON | Sanitize error responses to hide backend paths. |
| **Bot Protection (WAF)** | Informational | Postman (Web) blocked by Cloudflare | Indicates active Web Application Firewall (WAF). |

## Screenshots
* [Header Analysis - Fingerprinting 1](screenshots/API%20testing%20headers%201.png)
* [Header Analysis - Fingerprinting 2](screenshots/API%20testing%20headers%202.png)
* [Authentication Challenge - Error Logic](screenshots/03_authentication_challenge_error.png)

## Conclusion
The ReqRes API demonstrates strong perimeter defense via Cloudflare's WAF. However, backend misconfigurations regarding information disclosure and missing HSTS headers pose a risk for targeted exploitation. Hardening the response headers and sanitizing error output are recommended to improve the overall security posture.
