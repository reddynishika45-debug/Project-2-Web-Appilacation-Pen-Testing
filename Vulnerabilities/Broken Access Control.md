
---

# 🔓 Broken Access Control — IDOR Vulnerability Report

## 📁 Project

OWASP Juice Shop – Security Assessment

---

## 🚨 Severity

**Medium**

## 📊 CVSS Score

**6.5 (Medium)**

## 📌 CVSS Vector

```
CVSS:3.1/AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:N/A:N
```

---

## 📝 Vulnerability Title

Broken Access Control – Insecure Direct Object Reference (IDOR)

---

## 🎯 Asset / Application

* Application: OWASP Juice Shop
* Endpoint: `/rest/basket/{id}`
* Environment: Localhost Testing
* Tool Used: Burp Suite

---

## 🧪 Testing Methodology

Manual penetration testing was performed using Burp Suite by intercepting authenticated requests and modifying object identifiers. Authorization validation was tested by:

* Parameter manipulation
* Horizontal privilege escalation testing
* Authorization token validation
* Resource ownership verification

---

## 📌 Executive Summary

The application fails to enforce proper authorization checks on user-specific resources. By modifying the basket ID in API requests, an authenticated user can access another user's basket information. This vulnerability leads to unauthorized data exposure and horizontal privilege escalation.

---

## 🚨 Vulnerability Details

### 🔍 Finding 1 — Basket ID Manipulation (Confirmed)

**Endpoint**

```
GET /rest/basket/{id}
```

### 🧪 Proof of Concept

**Step 1 — Original Request**

```
GET /rest/basket/1
Authorization: Bearer <user_token>
```

📸 Screenshot Placeholder

```
[Insert Burp Original Request Screenshot]
```

---

**Step 2 — Modified Request**

```
GET /rest/basket/2
Authorization: Bearer <user_token>
```

📸 Screenshot Placeholder

```
[Insert Burp Modified Request Screenshot]
```

---

**Step 3 — Server Response**

The server returned basket data belonging to another user.

📸 Screenshot Placeholder

```
[Insert Unauthorized Data Response Screenshot]
```

---

## 🎯 Attack Vector

* Attack Type: Remote
* Access Level: Authenticated User
* Complexity: Low
* User Interaction: Not Required
* Exploitation Method: Parameter Manipulation

---

## 💥 Attack Scenario

1. Attacker logs in as normal user
2. Intercepts basket request using Burp Suite
3. Modifies basket ID value
4. Sends modified request to server
5. Server returns another user's basket data

This demonstrates horizontal privilege escalation due to missing authorization checks.

---

## 💼 Business Impact

🔴 Unauthorized Data Exposure
User shopping activity may be disclosed

🔴 Privacy Violation
Sensitive user information exposed

🔴 Compliance Risk
Violation of data protection standards

🔴 Attack Chaining Possibility
Can be combined with other vulnerabilities

🔴 Loss of Customer Trust
Users lose confidence in application security

---

## 📊 Risk Rating

| Factor       | Rating |
| ------------ | ------ |
| Likelihood   | High   |
| Impact       | Medium |
| Overall Risk | Medium |

---

## 🧠 CVSS Breakdown

| Metric              | Value     |
| ------------------- | --------- |
| Attack Vector       | Network   |
| Attack Complexity   | Low       |
| Privileges Required | Low       |
| User Interaction    | None      |
| Scope               | Unchanged |
| Confidentiality     | High      |
| Integrity           | None      |
| Availability        | None      |

---

## 🔁 Bypass Attempt Summary

| Technique              | Result                       | Status          |
| ---------------------- | ---------------------------- | --------------- |
| Basket ID Manipulation | Unauthorized data returned   | ✅ Confirmed     |
| User ID Manipulation   | Different user data returned | ✅ Confirmed     |
| JWT Role Modification  | Invalid token error          | ⚠️ Blocked      |
| Token Replacement      | Request rejected             | ❌ Not Confirmed |

---

## 🛠️ Recommendations

* Implement server-side authorization checks
* Validate resource ownership before response
* Use indirect object references
* Implement role-based access control (RBAC)
* Return HTTP 403 for unauthorized access
* Avoid predictable resource identifiers

---

## 🧩 Remediation Example

**Vulnerable Code**

```javascript
SELECT * FROM basket WHERE id = request.id
```

**Secure Implementation**

```javascript
SELECT * FROM basket WHERE id = ? AND user_id = authenticated_user
```

---

## 🏷️ OWASP Mapping

OWASP Top 10: **A01:2021 – Broken Access Control**

---

## 📸 Evidence Screenshots

1. Original Request Screenshot
2. Modified Request Screenshot
3. Unauthorized Response Screenshot
4. Scoreboard Completion Screenshot

---

## 📚 References

OWASP Broken Access Control Cheat Sheet
[https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html)

OWASP Top 10 – Broken Access Control
[https://owasp.org/Top10/A01_2021-Broken_Access_Control/](https://owasp.org/Top10/A01_2021-Broken_Access_Control/)

CWE-284 Improper Access Control
[https://cwe.mitre.org/data/definitions/284.html](https://cwe.mitre.org/data/definitions/284.html)

PortSwigger Access Control Testing
[https://portswigger.net/web-security/access-control](https://portswigger.net/web-security/access-control)

NIST CVSS Calculator
[https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator)

---

## 🏁 Conclusion

The application is vulnerable to Broken Access Control via insecure direct object references. Authenticated users can access other users' data by modifying identifiers. Proper authorization checks must be implemented to prevent unauthorized access and data disclosure.
