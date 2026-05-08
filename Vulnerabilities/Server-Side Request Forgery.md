
# Server-Side Request Forgery (SSRF) Vulnerability Report

---

# 📝 Vulnerability Title

Server-Side Request Forgery (SSRF)

---

# 🎯 Application

OWASP Juice Shop

---

# 🧪 Testing Methodology

The application workflow and internal request handling mechanisms were analyzed manually using Burp Suite and browser-based interaction. Multiple application functionalities related to order processing, payment handling, address management, and administrative information exposure were reviewed to identify insecure server-side request behavior and unintended exposure of internal resources.

---

# 📌 Description

Server-Side Request Forgery (SSRF) occurs when an application fetches remote resources or processes internal requests without proper validation. Attackers may exploit such behavior to access internal systems, sensitive resources, or unintended application functionality.

During testing, multiple sensitive application components and internal resources were exposed throughout the order and payment workflow. The application revealed administrative information, internal order details, payment-related data, delivery information, and address-related information during request processing and order handling.

The application workflow exposed:

- Administrative account information
- Internal order summary details
- Payment processing information
- Address and delivery details
- Product and pricing information
- Backend workflow responses

These findings indicate insufficient validation and improper exposure of internal application resources during server-side processing.

---

# 🚀 Steps to Reproduce

## Step 1 — Access Login and Shopping Workflow

1. Open OWASP Juice Shop.
2. Login using available credentials.
3. Browse products and add items to the basket.

### Observation

The application exposes detailed product pricing and workflow information during the purchase process.

---

## Step 2 — Review Delivery Information

1. Proceed to checkout.
2. Navigate to the delivery section.

### Observation

The application reveals:

- Delivery methods
- Shipping charges
- Internal order flow
- Address-related information

---

## Step 3 — Analyze Payment Workflow

1. Continue to the payment section.
2. Observe available payment methods and processing details.

### Observation

The application exposes:

- Payment modes
- Payment-related identifiers
- Internal payment workflow details

---

## Step 4 — Review Order Summary

1. Continue to the order summary page.
2. Inspect displayed information.

### Observation

The application reveals:

- Administrative account information
- Order details
- Address information
- Product pricing
- Delivery charges
- Payment information
- Internal order processing details

---

# 📸 Proof of Concept (PoC)

Evidence collected during testing includes:

- Exposure of administrative account details
- Visible internal order summary information
- Address and delivery information disclosure
- Payment method exposure
- Product pricing and order flow exposure
- Backend workflow information disclosure

Screenshots of these findings were captured during testing and stored in the project screenshots folder.

---

# ⚠️ Impact

If internal request handling and server-side processing are not properly secured, attackers may gain access to sensitive application data and internal resources.

Potential impacts include:

- Exposure of sensitive administrative information
- Leakage of internal workflow logic
- Information disclosure aiding further attacks
- Exposure of payment and delivery information
- Increased attack surface for attackers
- Potential access to internal services or resources

---

# 🎯 Attack Scenario

An attacker could interact with application workflows and analyze exposed server-side responses to gather sensitive information about internal application processing. By leveraging improperly exposed order details, administrative information, and backend workflow responses, attackers may identify hidden endpoints, internal services, or sensitive resources for further exploitation.

---

# 📊 Severity

**Medium Severity**

Although direct server compromise was not achieved, the exposure of sensitive internal workflow information and improper handling of server-side requests increases the risk of information disclosure and further exploitation.

---

# 🛠 Recommendations

To mitigate SSRF and related information disclosure risks:

- Validate and sanitize all server-side requests
- Restrict access to internal resources
- Avoid exposing internal application details in responses
- Implement proper access control checks
- Use allowlists for outbound server requests
- Minimize exposure of payment and address information
- Implement secure error handling
- Monitor suspicious server-side request behavior

---

# 🏁 Conclusion

The OWASP Juice Shop application exposes sensitive workflow information and internal processing details during shopping, payment, and order handling operations. Improper exposure of administrative information, payment details, and backend workflow responses increases the risk of information disclosure and further attacks.

Proper request validation, secure access control, and minimal exposure of internal resources are essential to reduce SSRF-related risks.

---
```
