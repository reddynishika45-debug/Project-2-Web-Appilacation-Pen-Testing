---

# 🧪 OWASP Juice Shop Setup (Kali Linux)

This guide explains how to install and run **OWASP Juice Shop** on **Kali Linux** for security testing and vulnerability assessment practice.

---

# ⚙️ Step 1: Install Node.js

Update the system and install **Node.js** and **npm**.

```bash
sudo apt update
sudo apt install nodejs npm -y
```

---

# ✅ Step 2: Verify Installation

Check whether Node.js and npm are installed correctly.

```bash
node -v
npm -v
```

If both commands return version numbers, the installation is successful.

---

# 🚀 Step 3: Run OWASP Juice Shop

Run the application using:

```bash
npx juice-shop
```

After running the command, open the application in your browser:

```
http://localhost:3000
```

---

# ❌ Fix Common npm Error

Sometimes the following error appears:

```
No versions available for juice-shop
```

To fix it, run:

```bash
npm cache clean --force
npm config set registry https://registry.npmjs.org/
npx @owasp/juice-shop
```

---

# 🐳 Install Docker (Kali Linux)

You can also run **Juice Shop** using **Docker**.

### Install Docker

```bash
sudo apt update
sudo apt install docker.io -y
```

### Start and Enable Docker

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

### Verify Installation

```bash
docker --version
```

---

# 🐳 Install Podman (Alternative to Docker)

**Podman** is an alternative container tool that can run Juice Shop.

### Install Podman

```bash
sudo apt update
sudo apt install podman -y
```

### Verify Installation

```bash
podman --version
```

---

# 🐳 Run OWASP Juice Shop using Docker or Podman

### ❌ Common Mistake

```bash
docket.io/bkimminich/juice-shop
```

### ✅ Correct Command

```bash
podman run -d -p 3000:3000 docker.io/bkimminich/juice-shop
```

If port **3000 is already in use**, run:

```bash
podman run -d -p 4000:3000 docker.io/bkimminich/juice-shop
```

---

# 📦 Check Running Containers

```bash
podman ps
```

---

# 🌐 Access Juice Shop in Browser

Open the application in your browser:

```
http://localhost:3000
```

or

```
http://localhost:4000
```

---

# ⚠️ Important Notes

* Perform testing **only in controlled environments**
* Do **NOT test real websites**
* Use intentionally vulnerable applications like **Juice Shop** for learning
* Capture **screenshots for documentation and reporting**

---

# 🎯 Outcome

After completing these steps, **OWASP Juice Shop will run locally**, allowing you to perform:

* Penetration testing
* Vulnerability assessment
* Security research
* OWASP Top 10 practice

This setup provides a **safe environment for learning web application security testing**.

---

