# 🔐 Web Application Penetration Testing – OWASP Juice Shop

---

## 👩‍💻 Team Members

* Nishika Reddy
* Soham Vishwanbar
* Riken Parmar
* Ravella Venkata Tarun
* Bhanumahesh

---

## 📌 Project Overview

This project focuses on performing **Web Application Penetration Testing (VAPT)** on the intentionally vulnerable application **OWASP Juice Shop**.

The objective was to identify, analyze, and demonstrate common web application vulnerabilities based on the **OWASP Top 10** security risks.

Testing was conducted on:

* **Localhost Target:** `127.0.0.1:3000`
* **Application:** OWASP Juice Shop

The assessment included reconnaissance, vulnerability discovery, exploitation, and mitigation recommendations.

---

## 🎯 Objectives

* Perform reconnaissance and application crawling
* Identify vulnerabilities in the web application
* Exploit vulnerabilities to create Proof of Concept (PoC)
* Analyze vulnerability severity using CVSS
* Provide mitigation strategies and security recommendations

---

## 🛠️ Tools Used

* **Burp Suite** – Web proxy, interception, and vulnerability testing
* **Kali Linux** – Security testing environment
* **Browser Developer Tools** – Application analysis and debugging

---

## 🔎 Testing Methodology

1. Application reconnaissance and crawling using Burp Suite
2. Identification of endpoints, parameters, and APIs
3. Manual vulnerability testing based on OWASP Top 10
4. Exploitation of identified vulnerabilities
5. Documentation of Proof of Concept (PoC)
6. Risk analysis using CVSS scoring
7. Security recommendations and mitigation strategies

---

## ⚠️ Vulnerabilities Identified

The following vulnerabilities were identified during the assessment:

* SQL Injection
* Cross-Site Scripting (XSS)
* Broken Authentication
* Broken Access Control
* Security Misconfiguration
* Vulnerable and Outdated Components
* Security Logging and Monitoring Failures

---

## 📊 Vulnerability Severity Summary

| Vulnerability                          | Severity  |
| -------------------------------------- | --------- |
| SQL Injection                          | 🔴 High   |
| Cross-Site Scripting (XSS)             | 🔴 High   |
| Broken Authentication                  | 🔴 High   |
| Broken Access Control                  | 🔴 High   |
| Security Misconfiguration              | 🟡 Medium |
| Vulnerable and Outdated Components     | 🟡 Medium |
| Security Logging & Monitoring Failures | 🟡 Medium |

---

## 🧪 Example Attack Scenarios

### SQL Injection

Injection payloads were tested in the search functionality which resulted in database error responses indicating possible SQL injection vulnerability.

### Cross-Site Scripting (XSS)

User input fields such as reviews accepted JavaScript payloads demonstrating insufficient input validation.

### Broken Access Control

Unauthorized API endpoints were accessed directly, indicating improper access restrictions.

### Security Misconfiguration

Missing security headers and exposed API endpoints were discovered during testing.

---

## 📂 Project Structure

```
Web-Application-Penetration-Testing-OWASP-Juice-Shop/
│
├── installation/
│   ├── juice-shop-installation.md
│   └── screenshots/
│       └── installation-steps/
│
├── reconnaissance/
│   └── burp-recon-crawling.md
│
├── vulnerabilities/
│   ├── sql-injection.md
│   ├── broken-authentication.md
│   ├── cross-site-scripting-xss.md
│   ├── sensitive-data-exposure.md
│   ├── security-misconfiguration.md
│   ├── broken-access-control.md
│   ├── vulnerable-outdated-components.md
│   ├── security-logging-monitoring-failures.md
│   ├── insecure-design.md
│   ├── csrf-cross-site-request-forgery.md
│   └── ssrf-server-side-request-forgery.md
│
├── screenshots/
│   ├── reconnaissance/
│   ├── sql-injection/
│   ├── broken-authentication/
│   ├── cross-site-scripting-xss/
│   ├── sensitive-data-exposure/
│   ├── security-misconfiguration/
│   ├── broken-access-control/
│   ├── vulnerable-outdated-components/
│   ├── security-logging-monitoring-failures/
│   ├── insecure-design/
│   ├── csrf-cross-site-request-forgery/
│   └── ssrf-server-side-request-forgery/
│
├── reports/
│   └── final-vapt-report.pdf
│
├── mitigation/
│   └── recommendations.md
│
└── README.md
```

---

## 🛡️ Mitigation Strategies

### 🔴 High Severity

* Implement prepared statements to prevent SQL Injection
* Sanitize and validate user inputs to prevent XSS
* Implement strong authentication mechanisms
* Enforce proper access control checks on all endpoints

### 🟡 Medium Severity

* Configure proper security headers
* Update vulnerable frameworks and dependencies
* Implement centralized logging and monitoring
* Avoid exposing sensitive application information

---

## 🛠️ Security Recommendations

* Implement **secure coding practices**
* Apply **regular security patch updates**
* Enforce **strong authentication policies**
* Implement **input validation and output encoding**
* Enable **security logging and monitoring**
* Conduct **regular penetration testing**

---

## 📊 Risk Analysis

The application is vulnerable to several **high-severity web vulnerabilities** including injection and access control issues.

These vulnerabilities could allow attackers to:

* Access unauthorized data
* Execute malicious scripts
* Bypass authentication controls
* Compromise application integrity

---

## ✅ Conclusion

This project demonstrates the process of performing **web application penetration testing** using industry-standard tools and methodologies.

By identifying vulnerabilities based on the OWASP Top 10 and providing mitigation strategies, the project highlights the importance of proactive security testing to improve the overall security posture of web applications.

---

## 🎯 Key Learning

* Practical experience in web application penetration testing
* Understanding of OWASP Top 10 vulnerabilities
* Hands-on use of Burp Suite for security testing
* Identification and exploitation of web vulnerabilities
* Importance of secure development practices

---
