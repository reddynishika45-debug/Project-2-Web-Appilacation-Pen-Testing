# 🔎 Burp Suite Reconnaissance & Crawling

This section documents the reconnaissance and application mapping performed using *Burp Suite* on the OWASP Juice Shop web application.

---

# 🎯 Objective

The goal of reconnaissance was to:

* Intercept HTTP requests and responses
* Discover application endpoints and APIs
* Identify input parameters used by the application
* Map the structure of the web application before vulnerability testing

---

# 🛠 Tool Used

* Burp Suite (Community Edition)

---

# ⚙️ Step 1: Configure Browser Proxy

Burp Suite was configured as a proxy to intercept traffic between the browser and the target application.

Proxy settings used:


IP Address: 127.0.0.1
Port: 8080


The browser proxy settings were updated to route all traffic through Burp Suite.

---

# ⚙️ Step 2: Enable Intercept Mode

Navigate to:


Proxy → Intercept


Enable interception by clicking:


Intercept ON


This allows Burp Suite to capture and analyze HTTP requests.

---

# ⚙️ Step 3: Access the Target Application

The OWASP Juice Shop application was opened in the browser:


http://localhost:3000


Burp Suite intercepted the requests between the browser and the server.

---

# ⚙️ Step 4: Browse and Crawl the Application

To map the application structure, different features of the website were explored, including:

* Login page
* Product search
* User account section
* Basket functionality
* Address management
* Feedback submission
* Reviews section

Each action generated HTTP requests captured by Burp Suite.

---

# ⚙️ Step 5: Analyze HTTP History

Navigate to:


Proxy → HTTP History


This section recorded all intercepted requests and responses.

Important requests identified included:


GET /
GET /#/home
POST /rest/user/login
GET /rest/products
GET /rest/products/search?q=apple
GET /rest/basket
GET /rest/user
GET /rest/address
GET /rest/delivery


These endpoints revealed the application's backend API structure.

---

# ⚙️ Step 6: Analyze Site Map

Navigate to:


Target → Site Map


The Site Map feature automatically organized discovered endpoints and resources.

This helped identify:

* API endpoints
* application directories
* parameters used in requests
* authentication-related requests

---

# ⚙️ Step 7: Identify Parameters

During analysis, several user input parameters were discovered.

Examples:


email
password
q (search parameter)
basketId
address
review


These parameters were later used during vulnerability testing such as SQL Injection and Cross-Site Scripting.

---

# 📸 Evidence Collected

The following screenshots were captured during reconnaissance:

* Burp Suite dashboard
* Proxy intercept enabled
* HTTP History showing captured requests
* Target site map
* Login request interception
* Product search request
* Basket API request
* Address management request
* Delivery endpoint request
* Reviews and feedback requests

---

# 🧠 Key Findings

The reconnaissance phase revealed:

* Multiple backend API endpoints
* Several user input parameters
* Authentication requests
* Data submission endpoints

These findings helped identify potential attack surfaces for further security testing.

---

# 🎯 Outcome

Burp Suite reconnaissance successfully mapped the application structure and identified critical endpoints and parameters used during later vulnerability exploitation.

This step was essential for performing structured web application penetration testing.
