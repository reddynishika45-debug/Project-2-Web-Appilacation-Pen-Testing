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

Additionally, the product review section allows **HTML content to be stored and rendered**, which results in **Stored HTML Injection**. However, JavaScript execution within stored reviews was not observed.

These vulnerabilities may allow attackers to perform phishing attacks, redirect users to malicious websites, or manipulate the webpage content.

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

## ⚠️ Impact

Successful exploitation of this vulnerability allows attackers to:

* Execute arbitrary JavaScript in victim browsers
* Redirect users to malicious websites
* Perform phishing attacks
* Manipulate webpage content

During testing, the following payload successfully redirected the browser to an external website:

```html
<img src=x onerror="window.location='https://testfire.net'">
```

This demonstrates the potential for phishing and malicious redirection attacks.

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

## ⚠️ Impact

Although JavaScript execution was not observed, attackers may still:

* Inject malicious HTML content
* Manipulate page appearance
* Conduct phishing or social engineering attacks
* Mislead users through malicious links or images

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

## 📊 CVSS Breakdown

| Metric              | Value    | Description                   |
| ------------------- | -------- | ----------------------------- |
| Attack Vector       | Network  | Exploitable remotely          |
| Attack Complexity   | Low      | Simple payload injection      |
| Privileges Required | None     | No authentication needed      |
| User Interaction    | Required | User must open malicious link |
| Scope               | Changed  | Affects client browser        |
| Confidentiality     | High     | Possible data exposure        |
| Integrity           | High     | Page manipulation possible    |
| Availability        | None     | No system disruption          |

---

# 💼 Business Impact

If exploited in a real-world environment, these vulnerabilities may result in:

### 🔴 Phishing Attacks

Attackers could redirect users to malicious websites and steal credentials.

### 🔴 Reputation Damage

Users may lose trust in the application if malicious content is displayed.

### 🔴 Social Engineering Attacks

Injected HTML content could mislead users into performing unintended actions.

### 🔴 Client-Side Data Manipulation

Attackers could alter webpage content displayed to users.

---

# 🛠️ Recommendations

To mitigate these vulnerabilities, the following security measures are recommended:

* Implement proper **input validation and sanitization**
* Encode user input before rendering in HTML
* Use **Content Security Policy (CSP)** to restrict script execution
* Disallow unsafe HTML tags in user input
* Implement **server-side input filtering**

---

# 📚 References

OWASP Cross-Site Scripting Prevention Cheat Sheet
[https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)

OWASP Top 10 – Injection
[https://owasp.org/www-project-top-ten/](https://owasp.org/www-project-top-ten/)

CWE-79: Cross-Site Scripting (XSS)
[https://cwe.mitre.org/data/definitions/79.html](https://cwe.mitre.org/data/definitions/79.html)

PortSwigger Web Security Academy – XSS
[https://portswigger.net/web-security/cross-site-scripting](https://portswigger.net/web-security/cross-site-scripting)

---

# 🏁 Conclusion

The application is vulnerable to **Reflected Cross-Site Scripting (XSS)** within the search functionality and **Stored HTML Injection** in the product review section. While JavaScript execution was not observed in stored reviews, reflected XSS allows attackers to execute malicious scripts in the browser.

Proper input validation, output encoding, and security headers should be implemented to mitigate these vulnerabilities.

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
