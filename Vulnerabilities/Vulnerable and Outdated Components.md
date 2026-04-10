
---

# 🛡️ Vulnerable and Outdated Components Vulnerability Report (CVSS Scored)

## 📁 Project

*OWASP Juice Shop – Security Assessment*

---

## 📝 Vulnerability Title

*Vulnerable and Outdated Components*

---

## 🎯 Asset / Application

*OWASP Juice Shop*

---

## 🧪 Testing Methodology

Testing was performed manually using *browser developer tools* and *API analysis through Burp Suite* to identify the frameworks and components used by the application.

The identified components were then checked against *public vulnerability databases* to determine whether any known vulnerabilities exist for those technologies.

Testing focused on identifying:

* Application version disclosure
* Technology stack information leakage
* Usage of potentially outdated frameworks or dependencies

---

## 📌 Executive Summary

During security testing, the application was found to *disclose information about its underlying components and technologies*.

The application exposes details such as *application version, frontend framework, and backend technologies* through API responses and client-side resources.

Attackers can leverage this information to identify *outdated components* and search for *publicly disclosed vulnerabilities* affecting those frameworks.

If vulnerable versions are used, attackers may exploit them to perform *targeted attacks such as remote code execution, cross-site scripting, or denial of service*.

---

# 🚨 Vulnerability Details

---

# 🔍 Identified Components

During the analysis, the following components were identified:

| Component           | Technology |
| ------------------- | ---------- |
| Frontend Framework  | Angular    |
| Backend Framework   | Express    |
| Runtime Environment | Node.js    |
| Application         | Juice Shop |

These components form the *application’s technology stack*.

---

# 🔍 Information Disclosure – Application Components

## 📍 Vulnerable Endpoint

http
GET /rest/admin/application-version


---

## 📌 Description

The application exposes information about its *technology stack and version details*.

Attackers can use this information to:

* Identify outdated frameworks
* Search for publicly disclosed vulnerabilities
* Develop targeted attacks against known vulnerable components

Applications relying on outdated frameworks or dependencies may be exposed to security risks if *patches and updates are not applied regularly*.

---

# 🧪 Proof of Concept (PoC)

## Step 1 — Identify Application Version

Send the following request using *Burp Repeater*:

http
GET /rest/admin/application-version


The server responds with *application version information*.

---

## Step 2 — Identify Frontend Framework

Open *browser developer tools* and inspect loaded resources.

Search inside the bundled JavaScript file:


main.js


Observe references to:


Angular


This confirms that the application uses the *Angular frontend framework*.

---

## Step 3 — Identify Backend Framework

Search within the same JavaScript bundle for:


express


The presence of *Express* indicates that the backend framework is based on *Express running on Node.js*.

---

## Step 4 — Search for Known Vulnerabilities

The identified frameworks were searched in *public vulnerability databases* such as the *National Vulnerability Database (NVD)*.

Example vulnerabilities affecting similar frameworks include:

* *CVE-2022-25844* – Express.js Denial of Service vulnerability
* *CVE-2021-42306* – Angular framework related vulnerability

---

## 📸 Evidence

Evidence for this vulnerability has been documented in the *screenshots folder* of the repository.

Example evidence includes:

* Burp Repeater response showing *application version disclosure*
* Developer tools showing *Angular references inside main.js*
* JavaScript bundle search results showing *Express framework*
* CVE search results identifying *public vulnerabilities affecting similar frameworks*

---

# 💥 Attack Vector

Attackers can exploit this vulnerability by gathering information about the application's technology stack through exposed endpoints and client-side resources.

Example request used to identify application version:

http
GET /rest/admin/application-version


Once the application version and frameworks are identified, attackers can search *public vulnerability databases such as NVD or CVE repositories* to discover known vulnerabilities affecting those components.

This enables attackers to prepare *targeted exploits specifically designed for vulnerable framework versions*.

---

# ⚠ Impact

Disclosure of application components enables attackers to:

* Identify outdated software frameworks
* Search for known vulnerabilities affecting those components
* Develop targeted attacks using publicly available exploits

If vulnerable versions are present, attackers may exploit issues such as:

* Cross-Site Scripting (XSS)
* Remote Code Execution
* Denial of Service
* Authentication bypass

---

# 🎯 Attack Scenario

An attacker analyzing the application could inspect *client-side scripts and API responses* to identify the frameworks and technologies used by the application.

For example, the attacker may discover that the application uses *Angular and Express* along with a specific application version.

The attacker can then search *public vulnerability databases* for known security issues affecting these technologies.

If vulnerabilities exist in the identified versions, the attacker may exploit them to perform attacks such as:

* Remote code execution
* Cross-site scripting
* Authentication bypass
* Denial-of-service attacks

---

# 📊 CVSS v3.1 Scoring

## 🎯 Base Score

*5.3 (Medium)*

---

## 📌 CVSS Vector


CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:L/I:N/A:N


---

# 📊 CVSS Breakdown

| Metric              | Value     | Description                           |
| ------------------- | --------- | ------------------------------------- |
| Attack Vector       | Network   | Exploitable remotely                  |
| Attack Complexity   | Low       | Easily identifiable information       |
| Privileges Required | None      | No authentication required            |
| User Interaction    | None      | Attack can be performed automatically |
| Scope               | Unchanged | Impact limited to application         |
| Confidentiality     | Low       | Technology stack disclosure           |
| Integrity           | None      | No modification of data               |
| Availability        | None      | No service disruption                 |

---

# 💼 Business Impact

If exploited in a production environment, this vulnerability may lead to:

### 🔴 Targeted Attacks

Attackers can identify vulnerable frameworks and prepare targeted exploits.

### 🔴 Increased Attack Surface

Disclosure of internal technologies makes the system easier to analyze and attack.

### 🔴 Potential Exploitation of Known Vulnerabilities

If outdated components exist, attackers may exploit publicly disclosed vulnerabilities.

### 🔴 Reputation Damage

Security weaknesses may reduce user trust in the application.

---

# 🛠️ Recommendations

## 🔹 Dependency Management

* Regularly update all frameworks and dependencies
* Use automated *dependency vulnerability scanning tools*

Examples:

* npm audit
* Snyk
* OWASP Dependency Check

---

## 🔹 Reduce Information Disclosure

* Avoid exposing *application version information*
* Remove unnecessary *technology stack details from responses*

---

## 🔹 Security Monitoring

* Monitor vulnerability databases for newly discovered issues
* Apply *security patches and updates promptly*

---

# 📚 References

OWASP Top 10 – Vulnerable and Outdated Components
[https://owasp.org/www-project-top-ten/](https://owasp.org/www-project-top-ten/)

National Vulnerability Database (NVD)
[https://nvd.nist.gov/](https://nvd.nist.gov/)

OWASP Dependency Check
[https://owasp.org/www-project-dependency-check/](https://owasp.org/www-project-dependency-check/)

---

# 🏁 Conclusion

The application exposes *information about the frameworks and technologies used in its architecture*.

This disclosure allows attackers to identify potential vulnerabilities in *outdated components* and develop targeted exploits.

Maintaining *up-to-date dependencies* and restricting *technology disclosure* is essential to reduce the risk of exploitation.

---

# 📈 Final Assessment

| Category        | Rating |
| --------------- | ------ |
| Severity        | MEDIUM |
| CVSS Score      | 5.3    |
| Exploitability  | Easy   |
| Business Impact | Medium |
| Confidence      | High   |

---
---

