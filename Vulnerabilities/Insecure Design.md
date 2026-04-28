---
# 🛡️ Insecure Design Vulnerability Report (CVSS Scored)

## 📁 Project

**OWASP Juice Shop – Security Assessment**

---

## 📝 Vulnerability Title

Insecure Design – Business Logic Flaws & Improper Validation in Checkout Workflow

---

## 🎯 Asset / Application

**OWASP Juice Shop**

---

## 🧪 Testing Methodology

Security testing was conducted using **manual testing techniques** and **Burp Suite**.

Critical application workflows such as **checkout, authentication, and input handling** were intercepted and manipulated to evaluate how the application enforces business logic and validates user-controlled data.

Testing focused on identifying weaknesses such as:

* Improper business logic validation
* Lack of server-side input validation
* Workflow bypass vulnerabilities
* Weak security policy enforcement

---

## 📌 Executive Summary

During security testing, the application was found to have multiple **Insecure Design vulnerabilities**.

The most critical issue identified is a **checkout workflow validation bypass**, where the application processes orders successfully even when critical parameters such as coupon data, address ID, payment ID, and delivery method ID are invalid or missing.

Additionally, the application demonstrates weak input validation, improper error handling, and poor enforcement of password policies.

These issues indicate a lack of secure design principles and significantly increase the risk of **fraudulent transactions, application instability, and exploitation of business logic flaws**.

---

# 🚨 Vulnerability Details

---

## 🔍 Finding 1: Checkout Workflow Validation Bypass (High Impact)

### 📍 Vulnerable Endpoint

`POST /api/Orders`

---

### 📌 Description

The application fails to validate critical parameters during the checkout process. Manipulated or invalid values for key fields are accepted by the server, and orders are successfully processed.

This indicates a lack of proper server-side validation and weak enforcement of business logic.

---

### 🧪 Proof of Concept (PoC)

#### Step 1 — Capture Checkout Request

* Perform a normal checkout process
* Intercept request using **Burp Suite**

---

#### Step 2 — Modify Request Parameters

Test the following manipulations:

* Invalid coupon:

```
"coupon": "INVALID123"
```

* Invalid address ID:

```
"addressId": 9999
```

* Invalid payment ID:

```
"paymentId": 999
```

* Invalid delivery method:

```
"deliveryMethodId": -1
```

* Remove required fields (e.g., paymentId)

---

#### Step 3 — Replay Request

Send the modified request using Burp Repeater.

---

### 📸 Result

* Server responds with **200 OK**
* Order is successfully processed despite invalid or missing data

---

### 💥 Attack Vector

Attackers can intercept checkout requests and modify critical parameters before sending them to the server.

Because the application does not enforce strict validation, attackers can submit manipulated requests to bypass normal application workflow and process unauthorized transactions.

---

### ⚠️ Impact

If exploited, attackers may:

* Perform unauthorized or fraudulent transactions
* Bypass payment validation
* Manipulate order details
* Exploit business logic flaws
* Cause data inconsistency

---

### 🎯 Attack Scenario

An attacker intercepts a legitimate checkout request using **Burp Suite** and modifies parameters such as payment ID, address ID, or coupon values.

The manipulated request is accepted by the server without validation, allowing the attacker to place orders with invalid or unauthorized data.

---

---

## 🔍 Finding 2: Improper Quantity Handling & Error Management

### 📍 Vulnerable Endpoint

`POST /api/BasketItems`

---

### 📌 Description

The application does not properly validate product quantity values, resulting in inconsistent behavior and server errors.

---

### 🧪 Proof of Concept (PoC)

* Negative quantity → **500 Internal Server Error**
* Zero quantity → **500 Internal Server Error**
* Extremely large quantity → inconsistent responses

---

### 📸 Result

* Application crashes or behaves inconsistently
* Improper error handling observed

---

### 💥 Attack Vector

Attackers can send crafted requests with invalid quantity values to trigger server errors or disrupt application behavior.

---

### ⚠️ Impact

* Application instability
* Potential Denial of Service (DoS)
* Backend logic exposure

---

### 🎯 Attack Scenario

An attacker manipulates product quantity values to trigger server errors, potentially causing instability or exploiting backend weaknesses.

---

---

## 🔍 Finding 3: Weak Password Policy

### 📍 Vulnerable Endpoint

`POST /api/Users`

---

### 📌 Description

The application allows weak passwords without enforcing complexity or strength requirements.

---

### 🧪 Proof of Concept (PoC)

* Register account with weak passwords such as:

  * `123`
  * `password`

---

### 📸 Result

* Weak passwords accepted without restriction

---

### 💥 Attack Vector

Attackers can exploit weak password policies to perform brute-force or credential stuffing attacks.

---

### ⚠️ Impact

* Increased risk of account compromise
* Weak authentication security

---

### 🎯 Attack Scenario

An attacker uses commonly used passwords to gain unauthorized access to user accounts due to lack of password strength enforcement.

---

---

## 🔍 Finding 4: Improper Handling of Unauthorized Fields

### 📍 Vulnerable Endpoint

`PUT /api/Users`

---

### 📌 Description

The application fails to properly validate and handle unauthorized input fields. When restricted fields such as user roles are modified, the application responds with an internal server error instead of safely rejecting the request.

---

### 🧪 Proof of Concept (PoC)

* Modify request:

```
"role": "admin"
```

* Send request via **Burp Suite**

---

### 📸 Result

* Server responds with **500 Internal Server Error**

---

### 💥 Attack Vector

Attackers can manipulate request payloads to include unauthorized fields, potentially causing server instability or identifying backend weaknesses.

---

### ⚠️ Impact

* Backend instability
* Poor input validation
* Increased attack surface

---

### 🎯 Attack Scenario

An attacker injects unauthorized parameters into API requests, causing the application to crash or behave unexpectedly, revealing weaknesses in backend validation logic.

---

# 📊 CVSS v3.1 Scoring

## 🎯 Base Score: **9.0 (High)**

---

## 📌 CVSS Vector

`CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:L`

---

## 📊 CVSS Breakdown

| Metric              | Value     | Description                      |
| ------------------- | --------- | -------------------------------- |
| Attack Vector       | Network   | Exploitable remotely             |
| Attack Complexity   | Low       | Easy to exploit                  |
| Privileges Required | None      | No authentication needed         |
| User Interaction    | None      | No user involvement              |
| Scope               | Unchanged | Limited to application           |
| Confidentiality     | High      | Sensitive data exposure possible |
| Integrity           | High      | Data manipulation possible       |
| Availability        | Low       | Possible service disruption      |

---

# 💼 Business Impact

If exploited in a production environment, these vulnerabilities may lead to:

🔴 Fraudulent Transactions
🔴 Unauthorized Order Placement
🔴 Data Integrity Issues
🔴 Account Compromise
🔴 Application Instability
🔴 Reputation Damage

---

# 🛠️ Recommendations

## 🔹 Secure Design Improvements

* Enforce strict server-side validation for all inputs
* Validate ownership of resources (address, payment, etc.)
* Reject invalid or missing parameters
* Implement proper workflow validation

## 🔹 Input Validation

* Validate numeric ranges and formats
* Use allowlists for accepted values
* Sanitize all user inputs

## 🔹 Authentication & Policy

* Enforce strong password policies
* Implement password complexity requirements

## 🔹 Error Handling

* Avoid exposing internal server errors
* Return generic error messages
* Implement centralized error handling

---

# 🏁 Conclusion

The application demonstrates multiple **Insecure Design vulnerabilities**, primarily due to improper validation of business logic and lack of secure workflow enforcement.

The most critical issue allows attackers to bypass the checkout process and perform unauthorized transactions with invalid data.

Implementing secure design principles, strict validation, and proper error handling is essential to mitigate these risks.

---

# 📈 Final Assessment

| Category        | Rating  |
| --------------- | ------- |
| Severity        | 🔴 HIGH |
| CVSS Score      | 9.0     |
| Exploitability  | Easy    |
| Business Impact | High    |
| Confidence      | High    |
