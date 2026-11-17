# Express Frontend - Jenkins CI/CD Pipeline

This repository contains the **Node.js/Express** frontend service for the **TuteDude DevOps** Jenkins CI/CD assignment. It runs on an **AWS EC2 (Ubuntu 24.04)** instance managed by **systemd**, with automated deployments triggered via **GitHub Webhooks** and **Jenkins**.

## 📌 Overview & Endpoints
* **Port:** `3000`
* **Process Manager:** `systemd` (`express-app.service`)
* **Deployment Directory:** `/opt/express-app`
* **Endpoints:**
  * `GET /` — Renders the Express frontend landing page (`Jenkins CI/CD Deployment`).
  * `GET /health` — Health check endpoint (`{"status": "healthy", "application": "Express", "port": "3000"}`).

---

## 🛠️ Tech Stack
* **Runtime & Framework:** Node.js v18, Express.js
* **CI/CD & Infrastructure:** Jenkins, GitHub Webhooks, AWS EC2, systemd

---

## ⚙️ CI/CD Pipeline Workflow (`Jenkinsfile`)
1. **Checkout SCM:** Pulls the latest code from `https://github.com` when triggered by a GitHub webhook.
2. **Install Dependencies:** Runs `npm install` to install required Node packages.
3. **Deploy to Production:** Executes `/usr/local/bin/deploy-express` via `NOPASSWD` sudo rules to sync files to `/opt/express-app`, assign ownership to the `deploy` user, install production dependencies (`npm install --omit=dev`), and restart `express-app.service`.

---

## 🚀 Local Setup & Execution

### 1. Clone the Repository
```bash
git clone https://github.com
cd express-frontend
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Start the Server
```bash
PORT=3000 node app.js
```
Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## 📂 Repository Structure
```text
express-frontend/
├── app.js              # Express web server and health check routes
├── package.json        # Node.js project metadata and dependencies
├── Jenkinsfile         # Declarative Jenkins CI/CD pipeline script
└── README.md           # Project and pipeline documentation
```
