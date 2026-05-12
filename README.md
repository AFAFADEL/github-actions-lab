# github-actions-lab
# GitHub Actions Lab 🚀

This repository demonstrates Continuous Integration (CI) using GitHub Actions with:

- GitHub-hosted Runner
- Self-hosted Runner on AWS EC2
- Automated testing using Node.js and Jest

---

## 📌 Project Structure

```bash
github-actions-lab/
│── .github/
│   └── workflows/
│       └── ci.yml
│── app.js
│── app.test.js
│── package.json
│── README.md
```

---

# 🧪 Lab 1 — GitHub Hosted Runner

This workflow runs automatically on GitHub-hosted runners whenever code is pushed to the `main` branch.

## Workflow File

```yaml
name: Node.js CI

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 18

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test
```

## Features

✅ Runs on GitHub-hosted runners  
✅ Installs dependencies automatically  
✅ Executes automated tests using Jest  
✅ Triggered on every push to `main`

---

# ☁️ Lab 2 — Self-hosted Runner on AWS EC2

This lab demonstrates running GitHub Actions on an AWS EC2 Ubuntu instance instead of GitHub servers.

## EC2 Setup

### 1. Launch EC2 Instance

- Ubuntu 22.04 LTS
- Instance Type: `t2.micro`

### 2. Install Dependencies

```bash
sudo apt update
sudo apt install -y nodejs npm git curl
```

### 3. Configure Self-hosted Runner

From GitHub:

**Settings → Actions → Runners → New self-hosted runner**

Select:

```text
Linux → x64
```

Run the generated commands on EC2.

Example:

```bash
mkdir actions-runner && cd actions-runner

curl -o actions-runner-linux-x64.tar.gz -L <runner-url>

tar xzf ./actions-runner-linux-x64.tar.gz

./config.sh
```

### 4. Start Runner

Temporary mode:

```bash
./run.sh
```

Service mode (recommended):

```bash
sudo ./svc.sh install
sudo ./svc.sh start
```

Check status:

```bash
sudo ./svc.sh status
```

---

## Self-hosted Workflow File

```yaml
name: CI on Self-hosted Runner

on:
  push:
    branches: [main]

jobs:
  build-and-test:
    runs-on: self-hosted

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Show hostname
        run: hostname && uname -a

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test

      - name: Cleanup
        run: rm -rf node_modules
```

## Features

✅ Runs on AWS EC2 instance  
✅ Uses self-hosted GitHub runner  
✅ Displays EC2 hostname in logs  
✅ Removes node_modules after execution

---

# 🔍 Difference Between Lab 1 & Lab 2

| Feature | Lab 1 | Lab 2 |
|----------|--------|--------|
| Runner Type | GitHub-hosted | Self-hosted |
| Infrastructure | GitHub Servers | AWS EC2 |
| Configuration | Simple | Requires EC2 setup |
| `runs-on` | `ubuntu-latest` | `self-hosted` |

---

## 🛠️ Technologies Used

- GitHub Actions
- Node.js
- Jest
- AWS EC2
- Ubuntu 22.04
- Self-hosted Runner

---

## 📷 Expected Output

After pushing code:

- Workflow starts automatically
- Dependencies are installed
- Tests run successfully
- GitHub Actions shows green check mark ✅

---



<img width="2355" height="871" alt="image" src="https://github.com/user-attachments/assets/d966732b-0a7f-4b11-b768-737c21d4b1ff" />
<img width="1895" height="1101" alt="image" src="https://github.com/user-attachments/assets/38269f63-18fb-4574-bb15-89d7ae70185c" />
