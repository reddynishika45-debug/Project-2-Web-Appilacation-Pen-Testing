
# 🛡️ Security Logging and Monitoring Failures (CVSS Scored)

## 📁 Project

**OWASP Juice Shop – Security Assessment**

---

## 📝 Vulnerability Title

Security Logging and Monitoring Failures – Lack of Detection and Alerting for Suspicious Activities

---

## 🎯 Asset / Application

**OWASP Juice Shop**

---

## 🧪 Testing Methodology

Security logging and monitoring were evaluated using **manual testing techniques** and **Burp Suite**.

Various suspicious and malicious activities were performed to observe whether the application:

* Detects abnormal behavior
* Logs security events
* Triggers alerts or protective controls

Testing focused on identifying gaps in:

* Logging of authentication attempts
* Detection of malicious inputs
* Monitoring of unauthorized access attempts

---

## 📌 Executive Summary

During testing, the application was found to have insufficient **security logging and monitoring mechanisms**.

Multiple suspicious activities such as repeated failed login attempts, injection-style inputs, and malicious payload submissions were performed. The application processed these requests without triggering alerts, warnings, or defensive actions.

The absence of proper logging and monitoring significantly increases the risk of **undetected attacks, delayed incident response, and prolonged system compromise**.

---

# 🚨 Vulnerability Details

---

## 🔍 Finding 1: Lack of Monitoring for Repeated Failed Login Attempts

### 📍 Vulnerable Endpoint

`POST /rest/user/login`

---

### 📌 Description

The application does not detect or respond to repeated failed login attempts.

No security controls such as CAPTCHA, account lockout, or alerting mechanisms are triggered.

---

### 🧪 Proof of Concept (PoC)

#### Step 1 — Perform Multiple Login Attempts

Use credentials:

```id="k1m2lp"
Email: admin@juice-sh.op
Password: wrongpassword
```

Repeat the login request multiple times.

---

### 📸 Result

* Unlimited login attempts allowed
* No CAPTCHA triggered
* No alert or warning displayed

---

### 💥 Attack Vector

Attackers can automate repeated login attempts without detection, enabling brute-force or credential stuffing attacks.

---

### ⚠️ Impact

* Undetected brute-force attacks
* Increased risk of account compromise
* No visibility into authentication abuse

---

### 🎯 Attack Scenario

An attacker performs automated login attempts using password lists. Due to lack of monitoring and alerting, these attempts go unnoticed, allowing attackers to continue until valid credentials are discovered.

---

---

## 🔍 Finding 2: No Detection of Suspicious Input (Injection Attempts)

### 📍 Vulnerable Endpoint

`GET /rest/products/search?q=`

---

### 📌 Description

The application does not detect or flag suspicious input patterns such as injection-style payloads.

---

### 🧪 Proof of Concept (PoC)

Enter payloads such as:

```id="z3pl0k"
apple''
apple--
```

---

### 📸 Result

* Requests processed normally
* No alert or monitoring response

---

### 💥 Attack Vector

Attackers can send malicious payloads to test for injection vulnerabilities without being detected.

---

### ⚠️ Impact

* Undetected injection attempts
* Increased risk of exploitation
* Lack of visibility into malicious activity

---

### 🎯 Attack Scenario

An attacker tests various injection payloads to identify vulnerabilities. Without monitoring or alerts, these activities remain undetected, allowing further exploitation.

---

---

## 🔍 Finding 3: No Monitoring of Malicious Script Input

### 📍 Vulnerable Endpoint

`POST /api/Reviews`

---

### 📌 Description

The application accepts malicious script payloads without triggering any monitoring or alerting mechanism.

---

### 🧪 Proof of Concept (PoC)

Submit payload:

```id="a7mn2q"
<script>alert(1)</script>
```

---

### 📸 Result

* Payload accepted and stored
* No alert or warning generated

---

### 💥 Attack Vector

Attackers can inject malicious scripts into input fields without detection.

---

### ⚠️ Impact

* Undetected Cross-Site Scripting (XSS) attempts
* Increased risk of client-side attacks
* No visibility into malicious payload submissions

---

### 🎯 Attack Scenario

An attacker injects malicious scripts into application inputs. Due to lack of monitoring, these activities are not detected, allowing exploitation of users.

---

---

## 🔍 Finding 4: Lack of Monitoring for Unauthorized Endpoint Access

### 📍 Vulnerable Endpoint

`GET /rest/admin/application-version`

---

### 📌 Description

The application does not detect or log attempts to access sensitive or administrative endpoints.

---

### 🧪 Proof of Concept (PoC)

Send request:

```id="w9fpl3"
GET /rest/admin/application-version
```

---

### 📸 Result

* Endpoint responds normally
* No alert or monitoring response

---

### 💥 Attack Vector

Attackers can probe sensitive endpoints without being detected.

---

### ⚠️ Impact

* Exposure of internal application information
* Undetected reconnaissance activities
* Increased attack surface

---

### 🎯 Attack Scenario

An attacker scans and accesses internal endpoints to gather information about the application. Without monitoring, these reconnaissance activities remain undetected.

---

# 📊 CVSS v3.1 Scoring

## 🎯 Base Score: **6.5 (Medium)**

---

## 📌 CVSS Vector

`CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:L/A:N`

---

## 📊 CVSS Breakdown

| Metric              | Value     | Description                |
| ------------------- | --------- | -------------------------- |
| Attack Vector       | Network   | Exploitable remotely       |
| Attack Complexity   | Low       | Easy to perform            |
| Privileges Required | None      | No authentication required |
| User Interaction    | None      | No user involvement        |
| Scope               | Unchanged | Limited to application     |
| Confidentiality     | Low       | Limited data exposure      |
| Integrity           | Low       | Limited impact             |
| Availability        | None      | No service disruption      |

---

# 💼 Business Impact

If exploited in a production environment, these vulnerabilities may lead to:

🔴 Undetected malicious activities
🔴 Delayed incident response
🔴 Increased risk of prolonged compromise
🔴 Lack of forensic visibility
🔴 Reduced ability to respond to attacks

---

# 🛠️ Recommendations

## 🔹 Logging Improvements

* Log all authentication attempts (success & failure)
* Record suspicious inputs and abnormal behavior
* Log access to sensitive endpoints

## 🔹 Monitoring & Alerting

* Implement alerting for repeated failed login attempts
* Detect and flag injection patterns
* Monitor unusual API activity

## 🔹 Security Controls

* Deploy intrusion detection systems (IDS)
* Use anomaly detection mechanisms
* Implement centralized logging (SIEM)

## 🔹 Operational Practices

* Regularly review logs
* Perform continuous monitoring
* Establish incident response procedures

---

# 🏁 Conclusion

The application lacks effective **security logging and monitoring mechanisms**, allowing malicious activities to go undetected.

Without proper logging, attackers can perform brute-force attacks, injection attempts, and reconnaissance activities without triggering alerts, significantly increasing the risk of undetected security breaches.

Implementing robust logging, monitoring, and alerting mechanisms is essential to improve the application's security posture.

---

# 📈 Final Assessment

| Category        | Rating    |
| --------------- | --------- |
| Severity        | 🟡 MEDIUM |
| CVSS Score      | 6.5       |
| Exploitability  | Easy      |
| Business Impact | Medium    |
| Confidence      | High      |
