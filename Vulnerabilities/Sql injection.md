
---

# 1️⃣ SQL Injection Vulnerability

**Severity:** Critical
**CVSS Score:** 9.8
**CWE:** CWE-89 — Improper Neutralization of Special Elements used in an SQL Command

---

## 📌 Summary

A SQL Injection vulnerability was identified in the application’s product search functionality. Improper handling of user input allows SQL control characters to influence backend query behavior, leading to database error disclosure and potential query manipulation.

However, further testing indicates that certain payloads are being partially blocked or rejected, suggesting the presence of filtering or security controls rather than full exploitation prevention.

---

## 🎯 Application

OWASP Juice Shop

---

## 🧰 Tools Used

* Burp Suite
* Manual Testing

---

## 🧪 Testing Methodology

The vulnerability was analyzed using **Burp Suite Proxy and Repeater** by intercepting and modifying HTTP requests.

User input in the search parameter was manipulated with SQL payloads to observe:

* Backend query behavior
* Error responses
* Input validation mechanisms
* Boolean condition handling

---

## 📌 Vulnerable Endpoint

```
/rest/products/search?q=
```

**Parameter:**

```
q
```

---

## 📌 Description

SQL Injection occurs when user input is directly embedded into SQL queries without proper sanitization or parameterization.

During testing, the search functionality showed inconsistent behavior when processing SQL-related input. Certain payloads triggered database errors, confirming partial SQL injection behavior.

However, boolean-based injection attempts were blocked or rejected, indicating the presence of filtering or request validation mechanisms.

---

## 🚀 Steps to Reproduce

### Step 1 — Intercept Request

1. Open application
2. Perform product search
3. Capture request using Burp Suite Proxy
4. Send request to Burp Repeater

---

### Step 2 — Error-Based Injection Test

#### Payload:

```
apple'
```

**Response:**

```
SQLite error: incomplete input
```

---

### Step 3 — Boolean-Based Injection Test

#### Payload (TRUE condition):

```
apple' OR '1'='1
```

#### Payload (FALSE condition):

```
apple' OR '1'='2
```

**Response for both:**

```
HTTP 400 Bad Request
```

---

## 🚨 🧪 Bypass Attempts & Observations (NEW – IMPORTANT)

To further validate SQL injection behavior, multiple bypass techniques were tested.

### 🔹 1. Boolean-Based Conditions

Payloads tested:

```
apple' OR '1'='1
apple' OR '1'='2
```

**Observation:**
Both payloads resulted in:

```
400 Bad Request
```

✔ Indicates request rejection before query execution OR strict input filtering.

---

### 🔹 2. SQL Comment-Based Injection

```
apple--
```

**Result:**

```
200 OK
```

✔ Suggests partial acceptance of SQL special characters without immediate blocking.

---

### 🔹 3. Quote Escaping Variants

```
apple''
```

**Result:**

```
200 OK
```

✔ Indicates inconsistent input handling.

---

### 🔹 4. Error-Based Injection

```
apple'
```

**Result:**

```
SQLite error: incomplete input
```

✔ Confirms backend SQL parsing is influenced by user input.

---

### 📌 Key Observation Summary

* Error-based SQL injection behavior is observable
* Boolean-based payloads are blocked or rejected
* Inconsistent filtering suggests partial mitigation rather than complete protection
* Backend likely applies input filtering or request validation mechanisms

---

## 📸 Proof of Concept (PoC)

The vulnerability was confirmed by injecting SQL control characters into the search parameter.

Example payload:

```
apple'
```

This resulted in the following database error:

```
SQLite error: incomplete input
```

Additionally, comment-based and quote-based payloads altered response behavior, confirming SQL query interaction with user input.

---

## 📸 Evidence

Proof-of-concept screenshots demonstrating:

* SQL error responses
* Burp Suite request interception
* Payload testing results

are stored in the project repository under the evidence directory.

---

## ⚠️ Impact

If fully exploitable, SQL Injection may allow attackers to:

* Access sensitive database records
* Bypass authentication mechanisms
* Modify or delete data
* Execute unauthorized SQL queries
* Compromise backend systems

---

## 💼 Business Impact

Exploitation may lead to:

* Exposure of customer and product data
* Loss of data integrity
* Financial loss due to data breaches
* Regulatory compliance violations
* Reputation damage

---

## 🎯 Attack Scenario

An attacker intercepts the search request and manipulates the `q` parameter with SQL payloads.

Depending on backend filtering strength, the attacker may:

* Trigger database errors (confirmed)
* Attempt boolean-based inference (currently blocked)
* Explore further bypass techniques

This indicates a potential attack surface that may be exploitable under different input conditions or encoding variations.

---

## 📊 Severity Assessment

**Severity:** Critical

**CVSS v3.1 Score:** 9.8

```
AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
```

---

## 🛠️ Recommendations

* Use **parameterized queries (prepared statements)**
* Implement strict **input validation & sanitization**
* Avoid exposing raw database errors
* Apply **ORM frameworks**
* Use least privilege database accounts
* Strengthen WAF rules without blocking legitimate inputs incorrectly
* Implement centralized secure query handling layer

---

## 🏁 Conclusion

The application shows **partial SQL injection behavior**, primarily through error-based responses. However, boolean-based payloads are currently blocked or filtered, indicating partial mitigation.

This suggests the application is **not fully secure against SQL injection**, but instead relies on inconsistent input filtering mechanisms that may still be bypassed.

---

## 📚 References

* OWASP Top 10
* CWE-89: SQL Injection
* [https://owasp.org/www-project-top-ten/](https://owasp.org/www-project-top-ten/)
* [https://cwe.mitre.org/data/definitions/89.html](https://cwe.mitre.org/data/definitions/89.html)

---

