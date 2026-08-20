# Shlink Self-Hosted URL Shortener (Docker Stack for Portainer)

This repository contains the Docker Compose stack configuration for hosting [Shlink](https://shlink.io/) (URL shortener server) and [Shlink Web Client](https://github.com/shlinkio/shlink-web-client) (web dashboard interface).

---

## 🚀 Portainer Deployment Instructions

### Step 1: Deploy Stack in Portainer
1. Open your **Portainer Dashboard**.
2. Navigate to **Stacks** -> **Add Stack**.
3. Name your stack: `shlink`.
4. Build method: Select **Repository**.
5. Repository URL: `https://github.com/breeves3622/shlink-docker`.
6. Repository reference: `refs/heads/main`.
7. Compose path: `docker-compose.yml`.
8. Under **Environment variables**, specify your values:
   - `DEFAULT_DOMAIN` = `s.yourdomain.com`
   - `IS_HTTPS_ENABLED` = `true`
   - `REDIRECT_EXTRA_PATH_MODE` = `append`
   - `SHLINK_PORT` = `9080`
   - `WEB_CLIENT_PORT` = `9081`
9. Click **Deploy the stack**.

---

## 🔑 Step 2: Generate an API Key for Shlink

To connect the Web Dashboard to your Shlink server, you need an API Key.

1. In Portainer, go to **Containers** -> click on the `shlink` container.
2. Click **Console** (or **Exec Console**).
3. Run command: `/bin/sh` or `/bin/bash`.
4. Execute the API key generation command:
   ```bash
   shlink api-key:generate
   ```
5. Copy the generated API Key output.

---

## 🌐 Step 3: Connect Shlink Web Client

1. Open your browser and go to `http://<YOUR_SERVER_IP>:9081`.
2. Click **Add a server**.
3. Fill in the server details:
   - **Name:** `My Shlink Server`
   - **URL:** `https://s.yourdomain.com`
   - **API Key:** Paste the API key generated in Step 2.
4. Click **Create server**.

---

## 📊 Ports & Persistence

| Service | Port | Description |
| :--- | :--- | :--- |
| **Shlink Server** | `9080` | Core shortener engine & REST API |
| **Shlink Web UI** | `9081` | Web administration dashboard |

Data is stored in the persistent volume `shlink_data` inside SQLite.
