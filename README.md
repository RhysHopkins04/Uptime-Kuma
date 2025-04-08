# Uptime Kuma Deployment (Traefik + Cloudflare DNS)

This repository contains a Docker Compose setup for deploying [Uptime Kuma](https://github.com/louislam/uptime-kuma) behind a [Traefik](https://doc.traefik.io/traefik/) reverse proxy, using **Cloudflare DNS-01** for automatic SSL via Let's Encrypt.

---

## 🌐 Features

- 🕵️‍♂️ Uptime Kuma monitoring
- 🔐 Automatic HTTPS via Cloudflare DNS-01 challenge
- 🛡️ Traefik reverse proxy (v2)
- 🔧 Easily customizable domain from `.env`
- 📦 Docker Compose based

---

## 📁 Folder Structure

```
Uptime-Kuma/
├── docker-compose.yml         # Main stack config
├── .env                       # Environment secrets/config (Ensure you do not commit one with valid values)
├── letsencrypt/               # SSL cert storage for Traefik
│   └── acme.json              # Let's Encrypt cert data
├── data/                      # Uptime Kuma data
└── README.md                  # You're reading it!
```

---

## ⚙️ Prerequisites

- Docker
- Docker Compose
- A domain managed by Cloudflare
- A **Cloudflare API Token** with:
  - `Zone → DNS → Edit` permissions
  - Scoped to your domain

---

## 🔐 Setup SSL Certificate (Cloudflare)

1. Go to [Cloudflare API Tokens](https://dash.cloudflare.com/profile/api-tokens)
2. Create a token with:
   - **Permissions**: `Zone → DNS → Edit`
   - **Zone Resources**: your domain
3. Copy the token and paste it into `.env`

---

## 🛠️ Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/RhysHopkins04/Uptime-Kuma.git
cd Uptime-Kuma
```

### 2. Edit `.env` File

> Replace `your-cloudflare-token` with your Cloudflare API Token created earlier.
> Replace `status.yourdomain.com` with your desired monitoring subdomain.

### 3. Prepare SSL Storage

```bash
mkdir -p letsencrypt
touch letsencrypt/acme.json
chmod 600 letsencrypt/acme.json
```

### 4. Run the Stack

```bash
docker compose up -d
```

---

### ✅ Visit Uptime Kuma

Once containers are up and SSL is issued, access your monitoring dashboard:

```
https://status.yourdomain.com
```

---

### 🔔 Optional: Setup Discord Webhook Alerts

1. Go to Kuma dashboard → Notifications
2. Add new → Discord
3. Paste in your Discord webhook URL
4. Set alert types (up/down/etc.)
5. Save!

---

### 🧩 Expanding

You can easily:

- Monitor multiple game servers/nodes
- Add additional status pages
- Create custom alerts (Telegram, Email, Webhooks, etc.)
- Expose a public status page for your community

---

### 🧼 Cleaning Up

To stop and remove everything:

```bash
docker compose down
```

---

### 📌 Notes

- This stack assumes you're using Cloudflare as your DNS provider.
- Make sure the domain `status.yourdomain.com` has an A record in Cloudflare pointing to your panel server IP, **with proxy enabled (orange cloud)**.
- The Let's Encrypt DNS challenge will handle cert generation and renewal via API.

---

### 🙋 Need Help?

If you're stuck or want to expand this setup with auto-posting to Discord, status embeds, or multi-node dashboards — feel free to reach out or open an issue. However the official support for Uptime Kuma can be found here: [Kuma Support](https://uptimekuma.org/)
