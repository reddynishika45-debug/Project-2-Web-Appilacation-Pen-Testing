# 📚 OWASP Top 10 Vulnerabilities — Study Notes

## 📁 Project

**Web Application Penetration Testing – OWASP Juice Shop**

---

# 1️⃣ SQL Injection (SQLi)

## 📌 Definition

SQL Injection occurs when user-controlled input is inserted into SQL queries without proper validation or sanitization.

Attackers can manipulate database queries to access, modify, or delete data.

---

## 🎯 Common Causes

* Unsanitized user input
* Dynamic SQL queries
* Lack of prepared statements

---

## 💥 Impact

* Database compromise
* Unauthorized data access
* Authentication bypass
* Data deletion or modification

---

## 🧪 Example Payloads

```sql id="9znijq"
' OR 1=1--
```

```sql id="c3d9u2"
admin'--
```

---

## 🛠 Prevention

* Use prepared statements
* Parameterized queries
* Input validation
* Least privilege database access

---

# 2️⃣ Broken Authentication

## 📌 Definition

Broken Authentication occurs when authentication or session management mechanisms are improperly implemented.

Attackers can compromise passwords, session tokens, or bypass authentication controls.

---

## 🎯 Common Causes

* Weak passwords
* No account lockout
* Improper session management
* Predictable tokens

---

## 💥 Impact

* Account takeover
* Unauthorized access
* Session hijacking

---

## 🧪 Example Issues

* Unlimited login attempts
* Session token remains valid after logout

---

## 🛠 Prevention

* Multi-Factor Authentication (MFA)
* Rate limiting
* Secure session handling
* Strong password policy

---

# 3️⃣ Cross-Site Scripting (XSS)

## 📌 Definition

XSS occurs when malicious scripts are injected into web pages viewed by other users.

---

## 🎯 Types of XSS

* Stored XSS
* Reflected XSS
* DOM-Based XSS

---

## 💥 Impact

* Session hijacking
* Credential theft
* Malicious redirects

---

## 🧪 Example Payload

```html id="7rjlwm"
<script>alert(1)</script>
```

---

## 🛠 Prevention

* Output encoding
* Input sanitization
* Content Security Policy (CSP)

---

# 4️⃣ Sensitive Data Exposure

## 📌 Definition

Sensitive data exposure occurs when confidential information is improperly protected.

---

## 🎯 Exposed Data Examples

* JWT tokens
* Passwords
* Personal information
* API responses

---

## 💥 Impact

* Identity theft
* Account compromise
* Data leakage

---

## 🛠 Prevention

* Encrypt sensitive data
* Use HTTPS
* Secure token storage
* Minimal data exposure

---

# 5️⃣ Security Misconfiguration

## 📌 Definition

Security Misconfiguration occurs when applications or servers are improperly configured.

---

## 🎯 Examples

* Default configurations
* Verbose error messages
* Missing security headers
* Exposed directories

---

## 💥 Impact

* Information disclosure
* Increased attack surface

---

## 🛠 Prevention

* Secure default settings
* Disable debug information
* Implement security headers

---

# 6️⃣ Broken Access Control

## 📌 Definition

Broken Access Control occurs when users can access resources or perform actions outside their intended permissions.

---

## 🎯 Examples

* Accessing admin endpoints
* IDOR vulnerabilities
* Privilege escalation

---

## 💥 Impact

* Unauthorized data access
* Privilege abuse

---

## 🛠 Prevention

* Server-side authorization checks
* Principle of least privilege
* Role-based access control

---

# 7️⃣ Vulnerable and Outdated Components

## 📌 Definition

Applications using outdated frameworks or libraries may contain publicly known vulnerabilities.

---

## 🎯 Examples

* Old Angular versions
* Outdated Express.js components

---

## 💥 Impact

* Remote Code Execution
* XSS
* Authentication bypass

---

## 🛠 Prevention

* Regular dependency updates
* Vulnerability scanning
* Patch management

---

# 8️⃣ Security Logging and Monitoring Failures

## 📌 Definition

Applications fail to properly detect, log, or alert suspicious activities.

---

## 🎯 Examples

* No logging of failed logins
* No monitoring of attacks
* Missing alerts

---

## 💥 Impact

* Undetected attacks
* Delayed incident response

---

## 🛠 Prevention

* Centralized logging
* SIEM integration
* Real-time alerting

---

# 9️⃣ Insecure Design

## 📌 Definition

Insecure Design refers to flaws in business logic or application architecture caused by missing or weak security controls.

---

## 🎯 Examples

* Workflow bypass
* Weak password policy
* Improper validation

---

## 💥 Impact

* Fraudulent actions
* Business logic abuse
* Unauthorized transactions

---

## 🛠 Prevention

* Threat modeling
* Secure design principles
* Server-side validation

---

# 🔟 Cross-Site Request Forgery (CSRF)

## 📌 Definition

CSRF tricks authenticated users into performing unwanted actions on a web application.

---

## 🎯 Attack Method

A malicious website forces a victim’s browser to send unauthorized requests.

---

## 💥 Impact

* Unauthorized account actions
* Password changes
* Transactions without consent

---

## 🛠 Prevention

* CSRF tokens
* SameSite cookies
* Re-authentication for sensitive actions

---

# 1️⃣1️⃣ Server-Side Request Forgery (SSRF)

## 📌 Definition

SSRF occurs when an attacker tricks the server into making requests to internal or external systems.

---

## 🎯 Attack Targets

* Internal services
* Cloud metadata endpoints
* Internal APIs

---

## 💥 Impact

* Internal network exposure
* Sensitive data access
* Remote service interaction

---

## 🛠 Prevention

* URL validation
* Allowlist trusted domains
* Restrict outbound requests

---

# 🧠 Key Learning Points

✅ Understanding OWASP Top 10 vulnerabilities
✅ Practical penetration testing using **Burp Suite**
✅ Identifying web application weaknesses
✅ Analyzing attack vectors and impacts
✅ Applying mitigation strategies

---

# 🏁 Conclusion

The **OWASP Top 10** represents the most critical web application security risks.

Understanding these vulnerabilities helps security professionals identify weaknesses, perform secure testing, and improve application security through proper mitigation and secure development practices.
