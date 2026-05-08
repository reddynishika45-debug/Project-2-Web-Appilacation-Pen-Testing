# 🛡️ Final Web Application Penetration Testing Report

## OWASP Juice Shop Security Assessment

---

# 📌 Project Information

## Project Title

Web Application Penetration Testing – OWASP Juice Shop

## Assessment Type

Vulnerability Assessment and Penetration Testing (VAPT)

## Target Application

OWASP Juice Shop

## Testing Environment

Localhost Environment (127.0.0.1:3000)

## Testing Approach

Manual Web Application Penetration Testing

## Tools Used

* Burp Suite
* Kali Linux
* Browser Developer Tools
* Burp Repeater
* JWT Decoder (jwt.io)

---

# 👩‍💻 Team Members

* Nishika Reddy
* Soham Vishwanbar
* Riken Parmar
* Ravella Venkata Tarun
* Bhanumahesh

---

# 📖 Executive Summary

This project focused on performing Web Application Penetration Testing (VAPT) on the intentionally vulnerable application OWASP Juice Shop.

The objective of the assessment was to identify, analyze, and demonstrate common web application vulnerabilities aligned with the OWASP Top 10 security risks.

Testing was conducted manually using Burp Suite, browser developer tools, API analysis, and business logic testing techniques.

During the assessment, multiple vulnerabilities were identified, including:

* SQL Injection
* Cross-Site Scripting (XSS)
* Broken Authentication
* Sensitive Data Exposure
* Security Misconfiguration
* Broken Access Control
* Vulnerable and Outdated Components
* Security Logging and Monitoring Failures
* Insecure Design
* Cross-Site Request Forgery (CSRF)
* Server-Side Request Forgery (SSRF)

Several vulnerabilities demonstrated weaknesses in authentication mechanisms, input validation, session management, access control, and business logic implementation.

The identified vulnerabilities could allow attackers to:

* Access unauthorized data
* Hijack user sessions
* Execute malicious scripts
* Perform unauthorized actions
* Exploit insecure application workflows
* Gather sensitive internal application information

This assessment highlights the importance of secure development practices, proper input validation, secure session handling, regular patch management, and continuous security testing.

---

# 🎯 Objectives

The primary objectives of this penetration testing project were:

* Perform reconnaissance and application analysis
* Identify vulnerabilities in the web application
* Exploit vulnerabilities to create Proof of Concept (PoC)
* Analyze vulnerabilities using CVSS scoring
* Understand insecure application workflows
* Provide mitigation strategies and security recommendations
* Improve understanding of OWASP Top 10 vulnerabilities

---

# 🧪 Testing Methodology

The following methodology was used during testing:

## 1. Reconnaissance

* Application crawling using Burp Suite
* Endpoint discovery
* API identification
* Header analysis
* Technology stack identification

## 2. Vulnerability Identification

* Input validation testing
* Authentication testing
* Session management analysis
* Access control testing
* Business logic testing
* Error handling analysis

## 3. Exploitation

* Manual payload injection
* Request manipulation
* Parameter tampering
* Session replay testing
* API abuse testing

## 4. Documentation

* Capture screenshots
* Document Proof of Concept (PoC)
* Analyze impact
* Assign severity ratings
* Provide recommendations

---

# 🔎 Vulnerabilities Identified

| #  | Vulnerability                            | Severity |
| -- | ---------------------------------------- | -------- |
| 1  | SQL Injection (SQLi)                     | High     |
| 2  | Cross-Site Scripting (XSS)               | High     |
| 3  | Broken Authentication                    | High     |
| 4  | Sensitive Data Exposure                  | High     |
| 5  | Broken Access Control                    | High     |
| 6  | Security Misconfiguration                | Medium   |
| 7  | Vulnerable and Outdated Components       | Medium   |
| 8  | Security Logging and Monitoring Failures | Medium   |
| 9  | Insecure Design                          | Medium   |
| 10 | Cross-Site Request Forgery (CSRF)        | Medium   |
| 11 | Server-Side Request Forgery (SSRF)       | Medium   |

---

# 1) SQL Injection (SQLi)

## Description

SQL Injection vulnerabilities occur when user-controlled input is improperly handled within database queries.

During testing, injection-style payloads submitted through application input fields generated abnormal responses and database-related errors.

## Impact

* Unauthorized database access
* Exposure of sensitive information
* Authentication bypass
* Database manipulation

## Severity

High

## Recommendation

* Use prepared statements
* Implement parameterized queries
* Validate and sanitize user input
* Avoid exposing database errors

---

# 2) Cross-Site Scripting (XSS)

## Description

The application improperly validates user input, allowing JavaScript payloads to be injected into user-controllable fields.

Payloads such as:

```html
<script>alert(1)</script>
```

were accepted during testing.

## Impact

* Session hijacking
* Cookie theft
* Malicious script execution
* User impersonation

## Severity

High

## Recommendation

* Implement output encoding
* Sanitize user input
* Use Content Security Policy (CSP)
* Validate all input fields

---

# 3) Broken Authentication

## Description

The application lacks brute-force protection and fails to invalidate sessions properly after logout.

Testing revealed:

* Unlimited login attempts
* No CAPTCHA
* No account lockout
* Session token reuse after logout

## Impact

* Account takeover
* Session hijacking
* Unauthorized access

## Severity

High

## Recommendation

* Implement account lockout
* Add CAPTCHA protection
* Invalidate sessions after logout
* Implement MFA

---

# 4) Sensitive Data Exposure

## Description

Sensitive information including JWT tokens, personal information, and internal application details were exposed during testing.

JWT tokens stored in Local Storage were easily accessible and decodable.

## Impact

* Exposure of Personally Identifiable Information (PII)
* Session hijacking
* Information disclosure
* Account compromise

## Severity

High

## Recommendation

* Store tokens in HttpOnly cookies
* Encrypt sensitive data
* Minimize API response data
* Use secure error handling

---

# 5) Broken Access Control

## Description

Improper access restrictions allowed unauthorized access to application resources and APIs.

Direct access to endpoints revealed insufficient authorization checks.

## Impact

* Unauthorized data access
* Privilege escalation
* Exposure of restricted resources

## Severity

High

## Recommendation

* Enforce server-side authorization
* Validate user permissions
* Restrict access to sensitive endpoints

---

# 6) Security Misconfiguration

## Description

The application exposed internal error messages, missing security headers, and sensitive configuration information.

Issues identified included:

* Missing Content-Security-Policy
* Missing Strict-Transport-Security
* robots.txt information disclosure
* Improper error handling

## Impact

* Information disclosure
* Increased attack surface
* Assistance in further exploitation

## Severity

Medium

## Recommendation

* Disable verbose errors
* Add missing security headers
* Restrict sensitive information exposure

---

# 7) Vulnerable and Outdated Components

## Description

The application exposed framework and version information including Angular, Express, and Node.js components.

Publicly known vulnerabilities affecting similar frameworks were identified.

## Impact

* Targeted exploitation
* Known vulnerability abuse
* Increased security risk

## Severity

Medium

## Recommendation

* Regularly update dependencies
* Monitor vulnerability databases
* Avoid exposing version information

---

# 8) Security Logging and Monitoring Failures

## Description

Suspicious activities such as repeated login attempts, injection payloads, and malicious inputs were processed without visible monitoring or alerting.

## Impact

* Undetected attacks
* Delayed incident response
* Increased risk of prolonged compromise

## Severity

Medium

## Recommendation

* Implement centralized logging
* Monitor suspicious activities
* Configure security alerts

---

# 9) Insecure Design

## Description

The application demonstrated insecure business logic and improper workflow validation.

Findings included:

* Quantity manipulation
* Coupon workflow weaknesses
* Weak password policy
* Improper workflow validation
* Inconsistent input validation

## Impact

* Business logic abuse
* Unauthorized discounts
* Workflow manipulation
* Increased attack surface

## Severity

Medium

## Recommendation

* Implement secure workflow validation
* Enforce strict business logic controls
* Validate user actions server-side

---

# 10) Cross-Site Request Forgery (CSRF)

## Description

Sensitive application actions lacked anti-CSRF protections.

Requests could potentially be triggered from external malicious websites without proper validation.

## Impact

* Unauthorized user actions
* Account modification
* Unwanted transactions

## Severity

Medium

## Recommendation

* Implement CSRF tokens
* Validate Origin and Referer headers
* Use SameSite cookie attributes

---

# 11) Server-Side Request Forgery (SSRF)

## Description

The application exposed internal workflow information during order processing, payment handling, and checkout operations.

Sensitive information exposed included:

* Administrative information
* Payment details
* Address information
* Internal order workflow

## Impact

* Information disclosure
* Internal workflow exposure
* Assistance in further attacks

## Severity

Medium

## Recommendation

* Restrict internal resource exposure
* Validate server-side requests
* Limit sensitive information disclosure

---

# 📊 Overall Risk Analysis

The assessment identified multiple high-severity vulnerabilities affecting authentication, input validation, session management, and access control.

Several vulnerabilities could potentially allow attackers to:

* Access unauthorized data
* Perform account takeover
* Execute malicious scripts
* Exploit insecure workflows
* Hijack user sessions
* Gather sensitive information

The presence of insecure business logic and weak session handling significantly increases the application's attack surface.

---

# 🛠️ General Security Recommendations

## Authentication & Session Security

* Implement Multi-Factor Authentication (MFA)
* Enforce strong password policies
* Add account lockout mechanisms
* Invalidate sessions after logout

## Input Validation

* Sanitize user input
* Use prepared statements
* Implement output encoding
* Validate API parameters

## Secure Configuration

* Disable verbose error messages
* Add security headers
* Remove unnecessary information disclosure

## Monitoring & Logging

* Implement centralized logging
* Configure intrusion detection
* Monitor suspicious activities

## Dependency Security

* Regularly update frameworks
* Monitor CVE databases
* Use dependency scanning tools

## Business Logic Protection

* Validate workflows server-side
* Prevent parameter tampering
* Restrict unauthorized state changes

---

# 📚 References

* OWASP Top 10
* OWASP Testing Guide
* OWASP Authentication Cheat Sheet
* PortSwigger Web Security Academy
* CWE Database
* CVSS v3.1 Framework

---

# 🏁 Conclusion

This project successfully demonstrates practical Web Application Penetration Testing against OWASP Juice Shop using manual testing methodologies.

The assessment identified vulnerabilities aligned with the OWASP Top 10 security risks and demonstrated practical exploitation techniques using Burp Suite and manual request analysis.

The project highlights:

* Web application security testing
* Vulnerability discovery
* Business logic analysis
* Session management testing
* API security testing
* Risk analysis and reporting

The inclusion of attack scenarios, CVSS scoring, mitigation strategies, and detailed documentation significantly improves the overall quality of the project.

This assessment demonstrates strong foundational understanding of web application security concepts and practical penetration testing methodologies.

---

# 🎯 Key Learning Outcomes

* Understanding OWASP Top 10 vulnerabilities
* Hands-on use of Burp Suite
* API testing and request manipulation
* Session and authentication testing
* Business logic vulnerability testing
* Vulnerability documentation and reporting
* Security risk assessment using CVSS
* Importance of secure coding practices

---

# 📌 Final Verdict

The project demonstrates strong internship-level penetration testing skills and practical understanding of modern web application vulnerabilities.

The assessment methodology, structured reporting, vulnerability analysis, and professional documentation reflect good foundational cybersecurity knowledge and hands-on application security experience.
