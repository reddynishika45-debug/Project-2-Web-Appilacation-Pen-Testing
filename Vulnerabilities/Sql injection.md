# 🛡️ SQL Injection Vulnerability Report (CVSS Scored)

## 📁 Project

OWASP Juice Shop – Security Assessment

---

# 📝 Vulnerability Title

SQL Injection (Error-Based with Partial Input Filtering Observed)

---

# 🎯 Asset / Application

OWASP Juice Shop

---

# 🧪 Testing Methodology

Manual penetration testing was performed using **Burp Suite** by injecting SQL payloads into application input fields and authentication parameters. Responses were analyzed based on:

* SQL error messages
* HTTP status codes
* Behavioral changes
* Input filtering / WAF responses

---

# 📌 Executive Summary

The application is vulnerable to **Error-Based SQL Injection**, confirmed through database error leakage when malformed input is injected. While some payloads are blocked (HTTP 400), backend SQL errors indicate insecure query handling.

This vulnerability may allow attackers to:

* Extract sensitive database information
* Manipulate authentication logic
* Perform unauthorized database queries

---

# 🚨 Vulnerability Details

---

## 🔍 Finding 1: Error-Based SQL Injection (CONFIRMED)

### 📍 Endpoint

```id="endpoint1"
/rest/products/search?q=
```

---

## 🧪 Proof of Concept (PoC)

### Step 1: Inject payload

```sql id="poc1"
apple'
```

### Step 2: Observe response

* SQL error returned in HTTP response
* Database query structure exposed

### 📸 Result

* Backend reveals SQL parsing error
* Confirms unsanitized input handling

---

## 💥 Attack Vector (CVSS Context)

* **Attack Vector:** Network (AV:N)
* Exploitable remotely via HTTP request
* No authentication required
* Direct injection via input parameter

---

## 💼 Business Impact

* Exposure of sensitive customer/product data
* Potential database compromise
* Regulatory compliance violations (GDPR / data protection laws)
* Reputational damage to organization
* Possible financial fraud if extended to user data

---

---

## 🔍 Finding 2: Boolean-Based SQL Injection (PARTIALLY BLOCKED)

### 📍 Payloads

```sql id="poc2"
' OR 1=1--
' OR 1=2--
```

### 📊 Observation

* HTTP 400 Bad Request returned
* No logical response difference observed

---

## 🔍 Finding 3: UNION-Based SQL Injection (BLOCKED)

### 📍 Payload

```sql id="poc3"
' UNION SELECT 1,2,3--
```

### 📊 Observation

* Request blocked (HTTP 400)
* No SQL execution observed

---

## 🔍 Finding 4: Time-Based Blind SQL Injection (NOT CONFIRMED)

### 📍 Payload

```sql id="poc4"
' OR IF(1=1, SLEEP(5), 0)--
```

### 📊 Observation

* No delay observed

---

## 🔍 Finding 5: Authentication Bypass Attempt (SQL ERROR OBSERVED)

### 📍 Payload

```sql id="poc5"
admin'--
```

### 📊 Observation

* SQLite error returned
* Indicates unsafe authentication query handling

---

# 📊 Bypass Attempts Summary

| Technique     | Payload        | Result       | Status           |
| ------------- | -------------- | ------------ | ---------------- |
| Error-Based   | `apple'`       | SQL error    | ✅ CONFIRMED      |
| Boolean-Based | `' OR 1=1--`   | 400 response | ⚠️ Blocked       |
| UNION-Based   | `UNION SELECT` | 400 response | ⚠️ Blocked       |
| Auth Bypass   | `admin'--`     | SQLite error | ⚠️ Partial issue |
| Time-Based    | `SLEEP(5)`     | No delay     | ❌ Not confirmed  |

---

# 📊 CVSS v3.1 Scoring

## 🎯 Base Score: **7.5 (High)**

---

## 📌 CVSS Vector

```id="cvss1"
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:L/A:N
```

---

## 📊 CVSS Breakdown

| Metric                   | Value     | Description                    |
| ------------------------ | --------- | ------------------------------ |
| Attack Vector (AV)       | Network   | Remote exploitation via HTTP   |
| Attack Complexity (AC)   | Low       | Simple payload injection       |
| Privileges Required (PR) | None      | No authentication needed       |
| User Interaction (UI)    | None      | No user action required        |
| Scope (S)                | Unchanged | Same application context       |
| Confidentiality (C)      | High      | Sensitive data exposure risk   |
| Integrity (I)            | Low       | Query manipulation possible    |
| Availability (A)         | None      | No service disruption observed |

---

# 💥 Attack Scenario

An attacker injects malicious SQL payloads into the application’s search parameter. During testing:

```sql id="attack1"
apple'
```

triggered a database error, confirming insecure SQL query handling.

### Possible real-world exploitation:

* Extract database schema
* Retrieve sensitive user data
* Combine with UNION-based payloads for data extraction
* Attempt authentication bypass

---

# 💼 Business Impact

If exploited in production, this vulnerability may lead to:

### 🔴 Data Breach

* Leakage of customer records and sensitive information

### 🔴 Financial Loss

* Fraud through compromised accounts
* Regulatory penalties (GDPR / compliance violations)

### 🔴 Reputation Damage

* Loss of customer trust
* Brand credibility impact

### 🔴 Operational Risk

* Database corruption or manipulation
* System instability under exploitation

---

# 🛠️ Recommendations

* Use **parameterized queries (prepared statements)**
* Avoid dynamic SQL string concatenation
* Implement strict input validation (whitelisting)
* Suppress database error messages in production
* Strengthen WAF rules for SQL meta-characters
* Enable logging and monitoring for injection attempts

---

# 📚 References

1. OWASP SQL Injection Prevention Cheat Sheet
   [https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)

2. OWASP Top 10 – Injection
   [https://owasp.org/www-project-top-ten/](https://owasp.org/www-project-top-ten/)

3. CWE-89: Improper Neutralization of Special Elements used in SQL Command ('SQL Injection')
   [https://cwe.mitre.org/data/definitions/89.html](https://cwe.mitre.org/data/definitions/89.html)

4. NIST CVSS v3.1 Specification Guide
   [https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator)

5. PortSwigger Web Security Academy – SQL Injection
   [https://portswigger.net/web-security/sql-injection](https://portswigger.net/web-security/sql-injection)

---

# 🏁 Conclusion

The application demonstrates a **High severity SQL Injection vulnerability** confirmed via error-based injection. Although some filtering exists, backend SQL errors indicate insecure query handling.

Immediate remediation is required to prevent data exposure and exploitation.

---
| Category               | Rating      |
| ---------------------- | ----------- |
| Reflected XSS Severity | HIGH        |
| Stored HTML Injection  | MEDIUM      |
| CVSS Score             | 8.2         |
| Exploitability         | Easy        |
| Business Impact        | Medium–High |
| Confidence             | High        |

---

