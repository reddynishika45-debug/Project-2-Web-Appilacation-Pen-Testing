
# Server-Side Request Forgery (SSRF) Report

## 📝 Vulnerability Title

Server-Side Request Forgery (SSRF)

---

## 🎯 Application

OWASP Juice Shop

---

## 🧪 Testing Methodology

Server-side request handling and internal application workflows were analyzed manually using Burp Suite and browser interaction. Various shopping, checkout, payment, and order-processing functionalities were tested to identify improper exposure of internal resources and sensitive workflow information.

---

## 📌 Description

Server-Side Request Forgery (SSRF) vulnerabilities occur when an application improperly handles server-side requests and exposes internal resources or backend workflow information.

During testing, the application exposed multiple sensitive internal details during the shopping and checkout workflow. Sensitive information such as administrative account details, delivery information, payment methods, order summaries, and pricing details were visible throughout the application workflow.

The application revealed:

- Administrative account information
- Product pricing and charges
- Address and delivery details
- Payment method information
- Internal order processing workflow
- Order summary details

Improper exposure of internal application workflows may assist attackers in understanding backend processing and identifying additional attack vectors.

---

## 🚀 Steps to Reproduce

### Step 1 — Login to the Application

Login using valid application credentials.

### Observation

The application allowed access to shopping and checkout workflows containing sensitive internal information.

---

### Step 2 — Add Products to Basket

Browse available products and add items to the shopping basket.

### Observation

The application exposed:

- Product information
- Item pricing
- Basket details
- Internal shopping workflow data

---

### Step 3 — Analyze Delivery Workflow

Proceed to the delivery section during checkout.

### Observation

The application displayed:

- Delivery address
- Shipping methods
- Delivery charges
- Internal order-processing information

---

### Step 4 — Analyze Payment Workflow

Continue to the payment section.

### Observation

The application exposed:

- Payment methods
- Card-related information
- Administrative details
- Internal payment workflow information

---

### Step 5 — Review Order Summary

Proceed to the order summary page.

### Observation

The application revealed:

- Administrative account details
- Address information
- Product pricing
- Delivery charges
- Payment information
- Internal order summary data

---

## 📸 Proof of Concept

Evidence collected during testing includes:

- Exposure of administrative information
- Visible address and payment details
- Product pricing and order charges
- Internal workflow and order-processing information
- Sensitive checkout and order summary data

Screenshots were captured during testing and stored in the screenshots folder.

---

## ⚠ Impact

Improper exposure of backend workflow information may allow attackers to:

- Gather sensitive administrative information
- Understand internal application logic
- Identify hidden resources or endpoints
- Analyze payment and order workflows
- Perform further attacks using exposed data

Potential impacts include:

- Information disclosure
- Increased attack surface
- Exposure of sensitive payment and address information
- Assistance in further exploitation attempts

---

## 🎯 Attack Scenario

An attacker could analyze exposed checkout and payment workflows to gather information about internal application processing, payment handling, administrative details, and order-management mechanisms.

This information may help attackers identify backend services, hidden endpoints, or additional vulnerabilities for further exploitation.

---

## 🌐 Attack Vector

The vulnerability can be exploited through normal application interaction during:

- Shopping workflow
- Checkout process
- Delivery configuration
- Payment processing
- Order summary handling

Attackers can observe sensitive internal information through exposed responses and improperly protected workflow data.

---

## 📊 CVSS Score

### CVSS v3.1 Base Score: 6.5 (Medium)

---

## 📈 CVSS Breakdown

| Metric | Value |
|---|---|
| Attack Vector (AV) | Network |
| Attack Complexity (AC) | Low |
| Privileges Required (PR) | Low |
| User Interaction (UI) | Required |
| Scope (S) | Unchanged |
| Confidentiality (C) | High |
| Integrity (I) | Low |
| Availability (A) | None |

---

## 💼 Business Impact

If exploited in a real-world application, this vulnerability could lead to:

- Exposure of sensitive customer information
- Leakage of payment and order-processing data
- Disclosure of internal application workflows
- Increased risk of targeted attacks
- Loss of customer trust
- Compliance and privacy risks

The exposed information may assist attackers in conducting further exploitation attempts against the application infrastructure.

---

## 📊 Severity

Medium because sensitive internal workflow information and backend processing details are exposed, increasing the risk of reconnaissance and further attacks.

---

## 🛠 Recommendations

To improve security and reduce SSRF-related risks:

- Validate and sanitize all server-side requests
- Restrict access to internal resources
- Avoid exposing backend workflow information
- Limit sensitive data exposure in responses
- Implement proper access-control checks
- Use secure error-handling mechanisms
- Monitor suspicious request activity
- Restrict unnecessary information disclosure during checkout workflows

---

## 🏁 Conclusion

The OWASP Juice Shop application exposes sensitive internal workflow information during shopping, payment, and order-processing operations. Administrative details, payment information, address data, and backend workflow responses were accessible during testing.

Proper request validation, secure access controls, and reduced information exposure are necessary to minimize SSRF-related risks and improve overall application security.

---

# ✅ Final Assessment

The SSRF-related findings demonstrate that the application exposes excessive internal workflow information during normal application usage. While full internal server compromise was not achieved, the exposed administrative, payment, and order-processing details significantly increase the application's attack surface.

The vulnerability highlights weaknesses in information handling, backend workflow exposure, and request validation mechanisms. Proper access control, secure response handling, and minimized information disclosure are necessary to strengthen the application's security posture.

---
```
