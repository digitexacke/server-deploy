# 🚀 BWM-XMD Deploy Platform

This is a VPS-based deployment platform for automatically deploying BWM-XMD WhatsApp bots via a web interface.

---

## 📦 Features

- Web-based deployment
- Automatic git clone
- Auto config injection
- Auto npm install
- Auto PM2 process creation
- Multi-bot support
- Node 20 compatible

---

## 🖥 Requirements

- Ubuntu VPS
- Node 20 (via NVM recommended)
- PM2
- Build tools (sqlite3 / sharp support)

---

## ⚙️ VPS Setup

### 1️⃣ Update system

```bash
apt update && apt upgrade -y
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.nvm/nvm.sh
nvm install 20
nvm use 20
nvm alias default 20

node -v

Perfect 💪🔥
If it will be a **GitHub repo**, then we structure it cleanly and professionally.

You don’t just dump commands — you organize it like a real deployment project.

Below is your **proper GitHub-ready structure + README**.

---

# 📁 Recommended Repo Structure

Create a new repo, for example:

```
bwm-deploy-platform
```

Structure it like this:

```id="i0yqks"
bwm-deploy-platform/
│
├── README.md
├── package.json
├── server.js
├── public/
│   └── index.html
└── .gitignore
```

---

# 📄 1️⃣ README.md (Clean GitHub Version)

Paste this into `README.md`:

````markdown id="rmv9x1"
# 🚀 BWM-XMD Deploy Platform

This is a VPS-based deployment platform for automatically deploying BWM-XMD WhatsApp bots via a web interface.

---

## 📦 Features

- Web-based deployment
- Automatic git clone
- Auto config injection
- Auto npm install
- Auto PM2 process creation
- Multi-bot support
- Node 20 compatible

---

## 🖥 Requirements

- Ubuntu VPS
- Node 20 (via NVM recommended)
- PM2
- Build tools (sqlite3 / sharp support)

---

## ⚙️ VPS Setup

### 1️⃣ Update system

```bash
apt update && apt upgrade -y
````

### 2️⃣ Install NVM + Node 20

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.nvm/nvm.sh
nvm install 20
nvm use 20
nvm alias default 20
```

Verify:

```bash
node -v
```

### 3️⃣ Install Build Tools

```bash
apt install build-essential python3 make g++ -y
```

### 4️⃣ Install PM2

```bash
npm install -g pm2
```

---

## 🚀 Run Deploy Server

Clone this repo:

```bash
git clone https://github.com/YOUR_USERNAME/bwm-deploy-platform.git
cd bwm-deploy-platform
npm install
```

Start server:

```bash
pm2 start server.js --name deploy-server
pm2 save
```

---

## 🌍 Access Web Interface

```
http://YOUR_VPS_IP:5005
```

---

## 📊 PM2 Commands

List processes:

```bash
pm2 list
```

View logs:

```bash
pm2 logs BOT_NAME
```

Delete bot:

```bash
pm2 delete BOT_NAME
```

---

## 📁 Bot Directory

Bots are deployed inside:

```
/opt/botserver/bots/
```

Each bot runs as a separate PM2 process.

---

## 🔐 Security Notice

This version does NOT include authentication.
Add authentication before making public.

---

## 📌 Author

Built for production VPS bot hosting.

````

---

# 📄 2️⃣ server.js (Repo Version)

Use this clean version:

```js
const express = require("express");
const { exec } = require("child_process");
const fs = require("fs");
const path = require("path");

const app = express();

app.use(express.json());
app.use(express.static("public"));

const BASE_DIR = "/opt/botserver/bots";

if (!fs.existsSync(BASE_DIR)) {
    fs.mkdirSync(BASE_DIR, { recursive: true });
}

app.post("/deploy", (req, res) => {
    const { owner, session } = req.body;

    if (!owner || !session) {
        return res.status(400).json({ error: "Missing owner or session" });
    }

    const botId = "bot_" + Date.now();
    const botPath = path.join(BASE_DIR, botId);

    exec(`git clone https://github.com/Bwmxmd254/BWM-XMD-GO.git ${botPath}`, (err) => {
        if (err) return res.status(500).json({ error: "Clone failed" });

        const envContent = `
OWNER_NUMBER=${owner}
SESSION=${session}
`;

        fs.writeFileSync(path.join(botPath, "config.env"), envContent);

        exec(`cd ${botPath} && npm install && pm2 start index.js --name ${botId} --max-memory-restart 400M`, (err2) => {
            if (err2) return res.status(500).json({ error: "Deployment failed" });

            res.json({
                success: true,
                botName: botId
            });
        });
    });
});

app.listen(5005, () => {
    console.log("Deploy server running on port 5005");
});
````

---

# 📄 3️⃣ package.json (Deploy Platform)

```json
{
  "name": "bwm-deploy-platform",
  "version": "1.0.0",
  "description": "Web deployment platform for BWM-XMD bots",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.19.2"
  }
}
```

---

# 📄 4️⃣ public/index.html

```html
<!DOCTYPE html>
<html>
<head>
  <title>BWM Deploy</title>
</head>
<body>
  <h2>Deploy Your BWM Bot</h2>

  <input type="text" id="owner" placeholder="Owner Number"><br><br>
  <textarea id="session" placeholder="Paste Session ID"></textarea><br><br>
  <button onclick="deploy()">Deploy</button>

  <script>
    function deploy() {
      fetch("/deploy", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          owner: document.getElementById("owner").value,
          session: document.getElementById("session").value
        })
      })
      .then(res => res.json())
      .then(data => alert(JSON.stringify(data)))
      .catch(err => alert("Deployment error"));
    }
  </script>
</body>
</html>
```

---

# 📄 5️⃣ .gitignore

```
node_modules
.env
```

---

# 🚀 Push to GitHub

Inside repo:

```bash
git init
git add .
git commit -m "Initial commit - BWM deploy platform"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/bwm-deploy-platform.git
git push -u origin main
```
