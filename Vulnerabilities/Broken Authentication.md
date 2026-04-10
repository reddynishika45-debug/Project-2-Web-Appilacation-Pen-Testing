---

# 🛡️ Broken Authentication Vulnerability Report (CVSS Scored)

## 📁 Project

**OWASP Juice Shop – Security Assessment**

---

## 📝 Vulnerability Title

**Broken Authentication – Lack of Brute-Force Protection & Improper Session Management**

---

## 🎯 Asset / Application

**OWASP Juice Shop**

---

## 🧪 Testing Methodology

Authentication security testing was conducted using **manual testing techniques** and **Burp Suite**. Login requests were intercepted and analyzed to evaluate how the application handles authentication attempts and session management.

Testing focused on identifying weaknesses such as:

* Lack of brute-force protection
* Improper session termination
* Session token reuse after logout

---

## 📌 Executive Summary

During security testing, the application was found to have multiple **Broken Authentication vulnerabilities**.

The login functionality does **not implement protective mechanisms against brute-force attacks**, allowing attackers to perform unlimited login attempts.

Additionally, the application **fails to properly invalidate user sessions after logout**. Previously issued authentication tokens remain valid and can still be used to access authenticated resources.

These issues significantly increase the risk of **account compromise, session hijacking, and unauthorized access**.

---

# 🚨 Vulnerability Details

---

# 🔍 Finding 1: Lack of Brute-Force Protection

## 📍 Vulnerable Endpoint

```
POST /rest/user/login
```

---

## 📌 Description

The application allows **unlimited authentication attempts** without implementing protective mechanisms such as:

* Account lockout
* CAPTCHA verification
* Request rate limiting

This allows attackers to repeatedly attempt different password combinations until valid credentials are discovered.

---

## 🧪 Proof of Concept (PoC)

### Step 1 — Navigate to Login Page

Open the login page of the application.

### Step 2 — Perform Multiple Login Attempts

Enter a valid email address such as:

```
admin@juice-sh.op
```

Attempt multiple incorrect passwords repeatedly.

### Step 3 — Observe Application Response

The application responds with the **same error message for every failed attempt** and does not trigger any security control such as **CAPTCHA or account lockout**.

---

## 📸 Result

* Unlimited login attempts allowed
* No CAPTCHA or rate limiting applied
* No account lockout triggered

---

## 💥 Attack Vector

Attackers can exploit this vulnerability remotely by sending repeated authentication requests to the login endpoint:

```
POST /rest/user/login
```

Because the application does **not enforce rate limiting or account lockout mechanisms**, attackers can automate login attempts using scripts or password lists.

This attack vector enables **automated brute-force attacks** where thousands of password combinations can be tested until valid credentials are discovered.

---

## ⚠️ Impact

If exploited successfully, attackers may:

* Gain unauthorized access to user accounts
* Perform credential brute-force attacks
* Compromise user data
* Conduct account takeover attacks

---

## 🎯 Attack Scenario

An attacker could automate login attempts using password dictionaries against the authentication endpoint.

Because the application does not enforce protections such as **rate limiting or account lockout**, the attacker can repeatedly attempt login requests until valid credentials are discovered.

Once valid credentials are obtained, the attacker can access the user account and perform actions such as:

* Viewing personal data
* Modifying account details
* Placing fraudulent orders

---

# 🔍 Finding 2: Session Not Invalidated After Logout

## 📍 Vulnerable Endpoint

```
GET /rest/user/whoami
```

---

## 📌 Description

The application **fails to properly invalidate session tokens when a user logs out**. A previously issued session token remains valid and can still be used to access authenticated endpoints.

This behavior indicates **improper session management**.

---

## 🧪 Proof of Concept (PoC)

### Step 1 — Login to the Application

Authenticate using valid credentials.

### Step 2 — Capture an Authenticated Request

Using **Burp Suite**, capture a request to:

```
GET /rest/user/whoami
```

Send the request to **Burp Repeater** and verify that user data is returned.

### Step 3 — Logout from the Application

Logout using the application interface.

### Step 4 — Replay the Captured Request

Replay the same request in **Burp Repeater**.

---

## 📸 Result

The response still returns **authenticated user information even after the user has logged out**.

This indicates that the **session token remains valid and has not been properly invalidated**.

---

## 💥 Attack Vector

Attackers can exploit this vulnerability by capturing or obtaining a **valid session token** and replaying it to access authenticated endpoints.

Example authenticated request:

```
GET /rest/user/whoami
```

If the session token is **not invalidated after logout**, attackers can reuse the token to maintain unauthorized access to the account.

---

## ⚠️ Impact

This vulnerability may lead to:

* Session hijacking
* Persistent unauthorized access
* Account takeover
* Exposure of sensitive user data

---

## 🎯 Attack Scenario

An attacker could intercept or obtain a **valid session token** using techniques such as:

* Network interception
* Cross-Site Scripting (XSS)

Even after the legitimate user logs out of the application, the attacker can reuse the captured token to access authenticated endpoints.

This allows the attacker to **impersonate the user and perform actions without needing the user's credentials**.

---

# 📊 CVSS v3.1 Scoring

## 🎯 Base Score

**8.1 (High)**

---

## 📌 CVSS Vector

```
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:N
```

---

## 📊 CVSS Breakdown

| Metric              | Value     | Description                      |
| ------------------- | --------- | -------------------------------- |
| Attack Vector       | Network   | Exploitable remotely             |
| Attack Complexity   | Low       | Simple automated attack          |
| Privileges Required | None      | No authentication required       |
| User Interaction    | None      | Attack performed automatically   |
| Scope               | Unchanged | Impact limited to application    |
| Confidentiality     | High      | Sensitive data exposure possible |
| Integrity           | High      | Account actions can be performed |
| Availability        | None      | No service disruption            |

---

# 💼 Business Impact

If exploited in a production environment, these vulnerabilities may lead to:

### 🔴 Account Takeover

Attackers could gain unauthorized access to user accounts.

### 🔴 Data Exposure

Sensitive personal information may be exposed.

### 🔴 Fraudulent Activity

Attackers could perform transactions or modify account details.

### 🔴 Reputation Damage

Security incidents could reduce user trust and damage the organization's reputation.

---

# 🛠️ Recommendations

## 🔹 Brute-Force Protection

* Implement **account lockout after multiple failed login attempts**
* Add **CAPTCHA verification after repeated failures**
* Apply **rate limiting on authentication endpoints**
* Implement **Multi-Factor Authentication (MFA)**

---

## 🔹 Session Management

* Invalidate **session tokens immediately upon logout**
* Implement **short session expiration time**
* Regenerate **session identifiers after authentication**
* Use secure cookie attributes such as **HttpOnly** and **Secure**

---

# 📚 References

* OWASP Authentication Cheat Sheet
  [https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html)

* OWASP Top 10
  [https://owasp.org/www-project-top-ten/](https://owasp.org/www-project-top-ten/)

* CWE-287: Improper Authentication
  [https://cwe.mitre.org/data/definitions/287.html](https://cwe.mitre.org/data/definitions/287.html)

* PortSwigger Web Security Academy – Authentication
  [https://portswigger.net/web-security/authentication](https://portswigger.net/web-security/authentication)

---

# 🏁 Conclusion

The application is vulnerable to **Broken Authentication** due to the absence of **brute-force protection mechanisms** and **improper session invalidation**.

These issues allow attackers to perform **automated credential attacks** and **reuse session tokens even after logout**, significantly increasing the risk of **unauthorized access and account compromise**.

Implementing stronger authentication controls and secure session management practices is essential to mitigate these vulnerabilities.

---

# 📈 Final Assessment

| Category        | Rating |
| --------------- | ------ |
| Severity        | HIGH   |
| CVSS Score      | 8.1    |
| Exploitability  | Easy   |
| Business Impact | High   |
| Confidence      | High   |

---
