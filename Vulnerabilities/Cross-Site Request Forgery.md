# 🛡️ Cross-Site Scripting (XSS) Vulnerability Report (CVSS Scored)

## 📁 Project

**OWASP Juice Shop – Security Assessment**

---

# 📝 Vulnerability Title

Cross-Site Scripting (XSS) – Improper Input Validation and Output Encoding

---

# 🎯 Asset / Application

**OWASP Juice Shop**

---

# 🧪 Testing Methodology

Cross-Site Scripting testing was performed manually using:

* Browser URL manipulation
* Payload injection techniques
* Browser Developer Tools
* **Burp Suite**

Testing focused on identifying whether user-controlled input is properly sanitized and encoded before being rendered in the browser.

---

# 📌 Executive Summary

During testing, the application was found vulnerable to **Cross-Site Scripting (XSS)**.

Malicious JavaScript payloads injected into the search functionality were executed successfully in the browser. The application failed to properly sanitize and encode user input before rendering it in the page response.

This vulnerability allows attackers to execute arbitrary JavaScript in the victim’s browser, potentially leading to session hijacking, credential theft, phishing attacks, and malicious redirection.

---

# 🚨 Vulnerability Details

## 🔍 Finding: Reflected Cross-Site Scripting (XSS)

### 📍 Vulnerable Endpoint

```http id="0qz9w1"
GET /#/search?q=
```

---

# 📌 Description

The application reflects user-controlled input directly into the webpage without proper sanitization or output encoding.

By injecting malicious JavaScript payloads into the search parameter, arbitrary scripts can be executed in the victim’s browser.

---

# 🧪 Proof of Concept (PoC)

## Step 1 — Navigate to Search Functionality

Open the OWASP Juice Shop application.

Use the search feature available in the application.

---

## Step 2 — Inject Malicious Payload

Enter the following payload into the search field or URL:

```html id="q7b2sm"
<img src="invalid" onerror="alert('XSS');">
```

---

## Step 3 — Observe Script Execution

The browser executes the injected JavaScript payload and displays a popup message:

```text id="f5x8pk"
XSS
```

---

# 📸 Result

* JavaScript payload executed successfully
* Browser popup displayed
* User input reflected without sanitization
* Application vulnerable to Reflected XSS

---

# 💥 Attack Vector

Attackers can craft malicious URLs containing JavaScript payloads and trick victims into opening them.

Example vulnerable request:

```http id="g3d0kt"
GET /#/search?q=<img src="invalid" onerror="alert('XSS');">
```

When the victim opens the malicious link, the injected script executes in the victim’s browser.

---

# ⚠️ Impact

Successful exploitation may allow attackers to:

* Execute arbitrary JavaScript
* Steal session tokens
* Hijack user sessions
* Perform phishing attacks
* Redirect users to malicious websites
* Access sensitive browser data

---

# 🎯 Attack Scenario

An attacker creates a malicious link containing a JavaScript payload and sends it to a victim through email, chat, or social media.

When the victim opens the link, the application reflects the payload into the webpage without proper sanitization, causing the script to execute in the browser.

The attacker may then steal session cookies, capture user input, or redirect the victim to malicious websites.

---

# 📊 CVSS v3.1 Scoring

## 🎯 Base Score: **8.8 (High)**

---

# 📌 CVSS Vector

```text id="j9w4md"
CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:C/C:H/I:H/A:L
```

---

# 📊 CVSS Breakdown

| Metric              | Value    | Description                     |
| ------------------- | -------- | ------------------------------- |
| Attack Vector       | Network  | Exploitable remotely            |
| Attack Complexity   | Low      | Easy payload injection          |
| Privileges Required | None     | No authentication required      |
| User Interaction    | Required | Victim must open malicious link |
| Scope               | Changed  | Client-side impact              |
| Confidentiality     | High     | Session/token theft possible    |
| Integrity           | High     | Malicious actions possible      |
| Availability        | Low      | Minor browser disruption        |

---

# 💼 Business Impact

If exploited in a production environment, this vulnerability may lead to:

🔴 Session hijacking
🔴 Credential theft
🔴 Phishing attacks
🔴 Malicious redirection
🔴 Unauthorized actions performed on behalf of users
🔴 Reputation damage

---

# 🛠️ Recommendations

## 🔹 Input Validation

* Validate all user input
* Reject malicious characters and scripts

---

## 🔹 Output Encoding

* Encode user-controlled data before rendering in HTML
* Prevent browser interpretation of scripts

---

## 🔹 Security Headers

Implement:

* Content-Security-Policy (CSP)
* X-XSS-Protection

---

## 🔹 Secure Development Practices

* Use secure templating frameworks
* Avoid directly rendering untrusted input
* Perform regular security testing

---

# 📚 References

## [OWASP Cross Site Scripting Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html?utm_source=chatgpt.com)

## [OWASP Top 10](https://owasp.org/www-project-top-ten/?utm_source=chatgpt.com)

## [PortSwigger Web Security Academy – XSS](https://portswigger.net/web-security/cross-site-scripting?utm_source=chatgpt.com)

---

# 🏁 Conclusion

The application is vulnerable to **Reflected Cross-Site Scripting (XSS)** due to improper input validation and output encoding.

Attackers can inject malicious JavaScript payloads into the application and execute scripts in the victim’s browser, potentially leading to session hijacking, credential theft, and phishing attacks.

Proper input sanitization, output encoding, and secure browser protections are essential to mitigate this vulnerability.

---

# 📈 Final Assessment

| Category        | Rating  |
| --------------- | ------- |
| Severity        | 🔴 HIGH |
| CVSS Score      | 8.8     |
| Exploitability  | Easy    |
| Business Impact | High    |
| Confidence      | High    |
