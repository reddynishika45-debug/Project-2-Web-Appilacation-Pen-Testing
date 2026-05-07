# 💻 System Requirements

This section describes the hardware, software, and environment requirements used for performing Web Application Penetration Testing on OWASP Juice Shop.

---

# 🖥️ Hardware Requirements

| Component | Requirement |
|---|---|
| Processor | Intel i3 / Ryzen 3 or higher |
| RAM | Minimum 4 GB (8 GB Recommended) |
| Storage | Minimum 20 GB Free Space |
| Internet Connection | Required for package installation |
| Virtualization Support | Recommended for Kali Linux VM |

---

# 🐧 Operating System Requirements

The project was tested primarily on:

| Operating System | Version |
|---|---|
| Kali Linux | Latest Stable Version |
| Windows | Windows 10 / 11 (Optional) |
| Ubuntu | 20.04+ (Optional) |

---

# 🛠️ Software Requirements

| Software / Tool | Purpose |
|---|---|
| OWASP Juice Shop | Vulnerable Web Application |
| Burp Suite Community Edition | Web Application Testing |
| Node.js | Running Juice Shop |
| npm | Package Management |
| Docker / Podman | Containerized Deployment |
| Web Browser | Application Testing |
| Visual Studio Code | Documentation & File Editing |

---

# 📦 Required Packages

## Node.js & npm

Install using:

```bash
sudo apt update
sudo apt install nodejs npm -y
````

---

## Docker

Install Docker:

```bash
sudo apt install docker.io -y
```

---

## Podman

Install Podman:

```bash
sudo apt install podman -y
```

---

# 🌐 Network Requirements

| Requirement      | Description             |
| ---------------- | ----------------------- |
| Localhost Access | Required for Juice Shop |
| Open Ports       | Port 3000 / 4000        |
| Browser Access   | Required for testing    |

---

# 🔐 Security Testing Environment

The testing environment should:

* Be isolated from production systems
* Use intentionally vulnerable applications only
* Avoid testing real-world targets without authorization

---

# ⚙️ Recommended Browser Extensions

| Extension  | Purpose                   |
| ---------- | ------------------------- |
| FoxyProxy  | Proxy Management          |
| Wappalyzer | Technology Identification |

---

# 📂 Tools Used During Testing

| Tool             | Usage                                 |
| ---------------- | ------------------------------------- |
| Burp Suite       | Request interception and manipulation |
| Browser DevTools | Client-side analysis                  |
| Kali Linux       | Security testing platform             |
| JWT.io           | JWT token analysis                    |
| curl             | API testing                           |

---

# 🚀 Supported Deployment Methods

OWASP Juice Shop can be deployed using:

* Node.js
* Docker
* Podman

---

# 🎯 Outcome

After configuring the above requirements, the environment will be ready for:

* Web Application Penetration Testing
* Vulnerability Assessment
* OWASP Top 10 Testing
* Security Research and Learning

```
