
# 1️⃣ SQL Injection Vulnerability Report

## 📝 Vulnerability Title

**SQL Injection (Error-Based & Input Validation Weakness)**

---

## 🎯 Application

OWASP Juice Shop

---

## 🧰 Tool Used

* Burp Suite

---

## 🧪 Testing Methodology

Testing was performed manually using **Burp Suite** by intercepting HTTP requests and injecting SQL payloads into user-controlled input fields.

The application responses were analyzed to determine whether user input was properly validated before being processed by the database.

---

## 📌 Description

SQL Injection occurs when **user input is improperly validated and directly included in SQL queries**, allowing attackers to manipulate database operations.

During testing, the **search functionality** was found to process user input without proper sanitization.

Multiple SQL payloads were injected into the search parameter, which resulted in **database error responses and unexpected query behavior**, confirming the presence of a SQL Injection vulnerability.

---

## 🔍 Vulnerable Endpoint

```
/rest/products/search?q=
```

**Parameter**

```
q
```

---

## 🚀 Steps to Reproduce

### Step 1 — Intercept Request

1. Open the application.
2. Perform a product search.
3. Intercept the request using Burp Suite Proxy.
4. Send the intercepted request to **Burp Repeater**.

---

### Step 2 — Test SQL Payloads

#### Payload 1 — Error-Based Injection

```
apple'
```

**Result**

* Application returned a **database error**.
* Example response:

```
SQLite error: incomplete input
```

---

#### Payload 2 — SQL Comment Injection

```
apple--
```

**Result**

* Request processed successfully.
* Server returned:

```
HTTP/1.1 200 OK
```

---

#### Payload 3 — Multiple Quote Injection

```
apple''
```

**Result**

* Request accepted by the server.
* Server returned:

```
HTTP/1.1 200 OK
```

* No input validation was applied.

---

## 📸 Proof of Concept

Evidence collected during testing includes:

* Screenshot showing **database error after injecting `'`**
* Screenshot showing **successful request using SQL comment operator `--`**
* Screenshot showing **application accepting multiple quotes `''`**

These observations confirm **improper input handling and lack of input sanitization**.

---

## ⚠️ Impact

If exploited, SQL Injection may allow attackers to:

* Retrieve sensitive data from the database
* Bypass authentication mechanisms
* Modify or delete application data
* Execute unauthorized database queries
* Gain unauthorized access to internal system data

---

## 💼 Business Impact

Successful exploitation of SQL Injection could result in:

* Exposure of **customer data**
* Unauthorized modification of **application records**
* Potential **financial loss**
* **Reputation damage** for the organization
* Increased risk of **full database compromise**

---

## 🎯 Attack Scenario

An attacker could manipulate the search functionality by injecting SQL syntax into the `q` parameter of the endpoint:

```
/rest/products/search
```

During testing, payloads such as:

```
apple'
--
apple''
```

caused changes in query behavior and generated database errors.

A skilled attacker could craft more advanced payloads to extract sensitive database information, bypass authentication mechanisms, or manipulate stored data.

---

## 📊 Severity

**Severity Level:** High

**CVSS v3.1 Score:** 9.8 (Critical)

**CVSS Vector**

```
AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
```

This vulnerability is considered critical because it allows attackers to interact directly with the backend database through malicious input.

---

## 🛠️ Recommendations

To mitigate SQL Injection vulnerabilities, the following measures are recommended:

* Use **prepared statements / parameterized queries**
* Implement **strict input validation and sanitization**
* Avoid exposing **database error messages**
* Use **ORM frameworks** for safer database interaction
* Apply the **principle of least privilege** for database accounts
* Implement **Web Application Firewall (WAF)** protections

---

## 🏁 Conclusion

The application is vulnerable to **SQL Injection** due to improper handling of user input in the search functionality.

The presence of database error messages and acceptance of SQL control characters confirms **insufficient input validation**, making the application susceptible to injection attacks.

Proper input validation, secure query handling, and improved error management are required to mitigate this vulnerability.

---
