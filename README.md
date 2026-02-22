# Uptime Kuma

A lightweight self-hosted uptime monitoring solution that tracks the availability and response times of your services and websites.

## Features

- 🔍 Monitor HTTP(s), TCP, DNS, Ping, and more
- 📊 Beautiful status page
- 🗄️ SQLite database (no external DB needed)
- 🌐 Web UI for easy configuration
- 🔐 Self-hosted - your data stays with you

## Quick Start

1. Copy the environment template:
   ```bash
   cp .env.dist .env
   ```

2. Edit `.env` and fill in your configuration:
   - `VIRTUAL_HOST`: Your domain (e.g., uptime.example.com)
   - `LETSENCRYPT_HOST`: Same as VIRTUAL_HOST
   - `LETSENCRYPT_EMAIL`: Your email for Let's Encrypt certificates

3. Start the service:
   ```bash
   docker compose up -d
   ```

4. Access the web UI at `https://VIRTUAL_HOST` and create your admin account

## Updating

To update to the latest image:

```bash
./updateDockerImages.sh
```

## Architecture

- **Container**: `uptime_kuma` (port 3001)
- **Volumes**: `./data:/app/data` (SQLite database)
- **Network**: Connected to `reverse-proxy` network for HTTPS via nginx-proxy

## Configuration

See `.claude/plans/init.md` for full setup instructions and Docker Compose details.

## Links

- [Uptime Kuma GitHub](https://github.com/louislam/uptime-kuma)
- [Uptime Kuma Documentation](https://uptime.kuma.pet/)
