---

# 🛡️ Cross-Site Scripting (XSS) & HTML Injection Vulnerability Report (CVSS Scored)

## 📁 Project

OWASP Juice Shop – Security Assessment

---

# 📝 Vulnerability Title

Reflected Cross-Site Scripting (XSS) & Stored HTML Injection

---

# 🎯 Asset / Application

OWASP Juice Shop

---

# 🧪 Testing Methodology

Manual penetration testing was performed by injecting HTML and JavaScript payloads into application input fields such as the search functionality and product review section. The application responses were analyzed to determine whether malicious scripts were executed or rendered within the browser.

Testing focused on identifying:

* Reflected Cross-Site Scripting (XSS)
* Stored Cross-Site Scripting (XSS)
* HTML Injection
* DOM-based XSS

---

# 📌 Executive Summary

During testing, the application was found to be vulnerable to **Reflected Cross-Site Scripting (XSS)** within the search functionality. This vulnerability allows attackers to inject malicious JavaScript code that executes in the user's browser.

Additionally, the product review section allows **HTML content to be stored and rendered**, resulting in **Stored HTML Injection**. However, JavaScript execution within stored reviews was not observed.

These vulnerabilities may allow attackers to manipulate webpage content, redirect users to malicious websites, or conduct phishing attacks.

---

# 🚨 Vulnerability Details

---

# 🔍 Finding 1: Reflected Cross-Site Scripting (CONFIRMED)

## 📍 Vulnerable Endpoint

```
#/search?q=
```

---

## 🧪 Proof of Concept (PoC)

### Step 1 — Inject Payload

Enter the following payload in the search field:

```html
<img src=x onerror=alert(1)>
```

---

### Step 2 — Observe Response

The browser executes the JavaScript payload via the `onerror` event, resulting in an alert popup.

---

## 📸 Result

* Payload is reflected in the application response
* Browser executes injected JavaScript
* Alert popup confirms successful script execution

---

## 💥 Attack Vector

* **Attack Vector:** Network (AV:N)
* Exploitable through user-controlled search parameter
* No authentication required
* Payload executes in victim's browser

---

## 🎯 Attack Scenario

An attacker could craft a malicious URL containing a Cross-Site Scripting payload and distribute it to victims through phishing emails, social media messages, or malicious advertisements.

Example malicious request:

```
http://target-site/#/search?q=<img src=x onerror=alert(1)>
```

When the victim clicks the link, the injected script executes within the browser context of the application. This allows the attacker to run arbitrary JavaScript in the victim's session.

For example, an attacker could modify the payload to redirect the victim to a phishing website:

```html
<img src=x onerror="window.location='https://testfire.net'">
```

This would automatically redirect users to a malicious page designed to steal login credentials or distribute malware.

---

## ⚠️ Impact

Successful exploitation of this vulnerability allows attackers to:

* Execute arbitrary JavaScript in victim browsers
* Redirect users to malicious websites
* Perform phishing attacks
* Manipulate webpage content

---

# 🔍 Finding 2: Stored HTML Injection (CONFIRMED)

## 📍 Vulnerable Location

```
Product Review Section
```

---

## 🧪 Proof of Concept (PoC)

### Step 1 — Submit Payload

Submit the following payload as a product review:

```html
<img src=x onerror=alert(1)>
```

---

### Step 2 — Refresh Page

After refreshing the page, the payload remains visible in the review section.

---

## 📸 Result

* HTML content is stored in the database
* Payload remains visible after page refresh
* JavaScript execution does **not occur**

---

## ⚠️ Technical Interpretation

The application allows **HTML content to be stored and rendered**, but JavaScript execution is restricted. This behavior indicates **Stored HTML Injection rather than Stored XSS**.

---

## 🎯 Attack Scenario

An attacker could submit a malicious HTML payload through the product review feature. Because the application stores and renders user-supplied HTML content, attackers may inject misleading or malicious content.

For example, an attacker could create a fake review containing a malicious link or image designed to trick users into visiting an external phishing website.

Example payload:

```html
<a href="https://malicious-site.com">Click here for a discount</a>
```

Users viewing the product reviews may trust the content and click the link, potentially exposing themselves to phishing attacks or malicious downloads.

---

# 🔍 DOM-Based XSS Testing

## Test Performed

The following payload was tested directly in the URL:

```
#/search?q=<img src=x onerror=alert(1)>
```

---

## Observation

* Application returned **"No results found"**
* No JavaScript execution occurred

---

## Conclusion

DOM-based XSS was tested but **not observed**.

---

# 📊 CVSS v3.1 Scoring

## 🎯 Reflected XSS Base Score: **8.2 (High)**

---

## 📌 CVSS Vector

```
CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:C/C:H/I:H/A:N
```

---

# 📊 CVSS Breakdown

| Metric              | Value    | Description                      |
| ------------------- | -------- | -------------------------------- |
| Attack Vector       | Network  | Exploitable remotely             |
| Attack Complexity   | Low      | Simple payload injection         |
| Privileges Required | None     | No authentication required       |
| User Interaction    | Required | Victim must click malicious link |
| Scope               | Changed  | Impacts client browser           |
| Confidentiality     | High     | Possible data exposure           |
| Integrity           | High     | Page manipulation possible       |
| Availability        | None     | No service disruption            |

---

# 💼 Business Impact

If exploited in a real-world environment, these vulnerabilities may lead to:

### 🔴 Phishing Attacks

Attackers may redirect users to malicious websites to steal credentials.

### 🔴 Reputation Damage

Users may lose trust in the platform if malicious content appears.

### 🔴 Social Engineering

Malicious HTML content could trick users into performing unintended actions.

### 🔴 Client-Side Manipulation

Attackers could modify content displayed in the browser.

---

# 🛠️ Recommendations

To mitigate these vulnerabilities, the following security controls should be implemented:

* Implement strict **input validation and sanitization**
* Apply **output encoding** before rendering user input
* Deploy **Content Security Policy (CSP)** headers
* Restrict unsafe HTML tags in user input
* Use secure libraries for input handling

---

# 📚 References

OWASP Cross-Site Scripting Prevention Cheat Sheet
[https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)

OWASP Top 10
[https://owasp.org/www-project-top-ten/](https://owasp.org/www-project-top-ten/)

CWE-79: Cross-Site Scripting
[https://cwe.mitre.org/data/definitions/79.html](https://cwe.mitre.org/data/definitions/79.html)

PortSwigger Web Security Academy – XSS
[https://portswigger.net/web-security/cross-site-scripting](https://portswigger.net/web-security/cross-site-scripting)

---

# 🏁 Conclusion

The application is vulnerable to **Reflected Cross-Site Scripting (XSS)** in the search functionality and **Stored HTML Injection** in the product review section. While stored reviews do not execute JavaScript, reflected XSS enables attackers to execute malicious scripts in the browser.

Implementing proper input validation, output encoding, and secure content handling is essential to mitigate these vulnerabilities.

---

# 📈 Final Assessment

| Category               | Rating      |
| ---------------------- | ----------- |
| Reflected XSS Severity | HIGH        |
| Stored HTML Injection  | MEDIUM      |
| CVSS Score             | 8.2         |
| Exploitability         | Easy        |
| Business Impact        | Medium–High |
| Confidence             | High        |

---
