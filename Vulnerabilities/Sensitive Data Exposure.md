---

# 🛡️ Sensitive Data Exposure Vulnerability Report (CVSS Scored)

## 📁 Project

**OWASP Juice Shop – Security Assessment**

---

## 📝 Vulnerability Title

**Sensitive Data Exposure**

---

## 🎯 Asset / Application

**OWASP Juice Shop**

---

## 🧪 Testing Methodology

Security testing was performed using **manual testing techniques** and **Burp Suite** to analyze HTTP requests, authentication responses, and API endpoints.

The testing process focused on identifying:

* Exposure of sensitive user information in API responses
* Weak protection of authentication tokens
* Improper client-side storage of security tokens
* Disclosure of internal application information through error messages

---

## 📌 Executive Summary

During security testing, the application was found to expose **sensitive user data and authentication tokens** through API responses, client-side storage, and improperly protected JWT tokens.

Authentication tokens are encoded using **Base64 but not encrypted**, allowing attackers to decode them and retrieve sensitive information such as **email, user ID, and user roles**.

Additionally, certain API responses expose **Personally Identifiable Information (PII)** including full name, address, and contact information.

These weaknesses significantly increase the risk of **information disclosure, session hijacking, and potential account takeover**.

---

# 🚨 Vulnerability Details

---

# 🔍 Finding: Sensitive Data Exposure

## 📍 Example Endpoints

```http id="sde1"
POST /rest/user/login
```

```http id="sde2"
GET /api/Address/8
```

---

## 📌 Description

The application improperly exposes sensitive information through several mechanisms:

* JWT tokens are **Base64 encoded but not encrypted**
* API responses expose **personal user information**
* Internal error messages reveal **backend implementation details**
* Authentication tokens are stored in **browser local storage**

Because Base64 encoding is **not a secure encryption method**, attackers can easily decode the JWT payload and extract sensitive data without needing the secret key.

---

# 🧪 Proof of Concept (PoC)

## Step 1 — Capture Login Request

Login using valid credentials and intercept the request using **Burp Suite**.

```http id="sde3"
POST /rest/user/login
```

Observe that the request body contains:

* Email
* Password

---

## Step 2 — Extract JWT Token

Inspect the login response in **Burp Suite** and identify the **JWT token** returned by the server.

---

## Step 3 — Decode JWT Token

Copy the JWT token and decode it using an online JWT decoder.

The decoded payload reveals sensitive information such as:

* Email
* User ID
* User Role

---

## Step 4 — Analyze API Response

Send the following request:

```http id="sde4"
GET /api/Address/8
```

The response exposes sensitive information including:

* Full Name
* Mobile Number
* Address
* Zip Code
* City
* Country

---

## Step 5 — Test Unauthorized Access

Modify the request to access another resource:

```http id="sde5"
GET /api/Addresss/9
```

The server returns an **internal error message**, revealing backend application details.

---

## Step 6 — Check Client-Side Storage

Open **Browser Developer Tools → Application → Local Storage**.

Observe that the **JWT authentication token is stored in local storage**, making it accessible via JavaScript.

---

## 📸 Result

Evidence collected during testing includes:

* Burp Suite responses exposing authentication tokens
* Decoded JWT payload revealing sensitive user information
* API responses exposing PII
* Error messages revealing internal system details
* JWT token stored in browser local storage

Screenshots supporting this vulnerability are stored in the **screenshots folder of the repository**.

---

# 💥 Attack Vector

Attackers can exploit this vulnerability by intercepting authentication responses and decoding exposed JWT tokens.

Example request:

```http id="sde6"
POST /rest/user/login
```

Because JWT tokens are only **Base64 encoded**, attackers can easily decode them and retrieve sensitive information.

Additionally, if authentication tokens are stored in **local storage**, attackers can steal them using **Cross-Site Scripting (XSS)** or other client-side attacks.

This allows attackers to reuse the token and access authenticated endpoints.

---

# ⚠ Impact

Successful exploitation may lead to:

* Exposure of **Personally Identifiable Information (PII)**
* **Account takeover**
* **Session hijacking**
* Information leakage about internal system architecture
* Increased risk of targeted attacks and phishing

---

# 🎯 Attack Scenario

An attacker monitoring application responses could capture authentication tokens returned by the server.

Because the JWT token is only encoded and not encrypted, the attacker can decode it to retrieve sensitive user data such as email addresses and user roles.

If the token is stored in browser local storage, it could be stolen through a **Cross-Site Scripting attack**.

Using the stolen token, the attacker could impersonate the legitimate user and access protected resources, potentially exposing sensitive personal data or performing unauthorized actions.

---

# 📊 CVSS v3.1 Scoring

## 🎯 Base Score

**7.5 (High)**

---

## 📌 CVSS Vector

```
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N
```

---

# 📊 CVSS Breakdown

| Metric              | Value     | Description                    |
| ------------------- | --------- | ------------------------------ |
| Attack Vector       | Network   | Exploitable remotely           |
| Attack Complexity   | Low       | Easy to perform                |
| Privileges Required | None      | No prior authentication needed |
| User Interaction    | None      | Attack performed automatically |
| Scope               | Unchanged | Impact limited to application  |
| Confidentiality     | High      | Sensitive data exposure        |
| Integrity           | None      | No direct data modification    |
| Availability        | None      | No service disruption          |

---

# 💼 Business Impact

If exploited in a production environment, this vulnerability could lead to:

### 🔴 Data Privacy Violations

Exposure of sensitive personal information such as addresses and phone numbers.

### 🔴 Account Takeover

Attackers could impersonate legitimate users using stolen authentication tokens.

### 🔴 Regulatory Risks

Exposure of personal data could lead to **compliance violations** and legal penalties.

### 🔴 Reputation Damage

Loss of user trust due to improper protection of sensitive data.

---

# 🛠️ Recommendations

## 🔹 Secure Token Handling

* Avoid storing sensitive data inside JWT payloads
* Encrypt sensitive information where necessary
* Use **short token expiration times**

---

## 🔹 Secure Storage of Authentication Tokens

* Store authentication tokens in **HttpOnly cookies**
* Prevent JavaScript access to authentication tokens

---

## 🔹 Limit Sensitive Data Exposure

* Restrict API responses to **only necessary information**
* Avoid exposing internal system details in error messages

---

## 🔹 Implement Strong Security Controls

* Apply **proper input validation**
* Implement **secure access control checks**
* Protect against **Cross-Site Scripting (XSS)** attacks

---

# 📚 References

OWASP Top 10 – Sensitive Data Exposure
[https://owasp.org/www-project-top-ten/](https://owasp.org/www-project-top-ten/)

OWASP Cryptographic Storage Cheat Sheet
[https://cheatsheetseries.owasp.org/](https://cheatsheetseries.owasp.org/)

JWT Security Best Practices
[https://jwt.io](https://jwt.io)

---

# 🏁 Conclusion

The application exposes sensitive user data through **weak JWT handling, excessive API responses, client-side storage of tokens, and verbose error messages**.

These weaknesses allow attackers to retrieve sensitive user information and potentially hijack user sessions.

Implementing **secure token storage, minimal data exposure, and proper encryption mechanisms** is necessary to protect sensitive information and mitigate these risks.

---

# 📈 Final Assessment

| Category        | Rating |
| --------------- | ------ |
| Severity        | HIGH   |
| CVSS Score      | 7.5    |
| Exploitability  | Easy   |
| Business Impact | High   |
| Confidence      | High   |

---
If you want, I can also **review this Sensitive Data Exposure report like a mentor and give you its rating (just like I did for Broken Authentication)** — that will help ensure your **internship project scores high.**
