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
