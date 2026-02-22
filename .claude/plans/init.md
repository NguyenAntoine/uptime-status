# Uptime Kuma Setup

Uptime Kuma is a lightweight self-hosted uptime monitoring solution that tracks the availability and response times of your services and websites.

## Docker Compose Configuration

```yaml
services:
  uptime-kuma:
    image: louislam/uptime-kuma:2
    container_name: uptime_kuma
    restart: always
    expose:
      - 3001
    volumes:
      - ./data:/app/data
    environment:
      - VIRTUAL_HOST=${VIRTUAL_HOST}
      - LETSENCRYPT_HOST=${LETSENCRYPT_HOST}
      - LETSENCRYPT_EMAIL=${LETSENCRYPT_EMAIL}
      - VIRTUAL_PORT=3001
    networks:
      - default
      - reverse-proxy

networks:
  reverse-proxy:
    external: true
```

## Setup Instructions

1. Copy the environment template:
   ```bash
   cp .env.dist .env
   ```

2. Edit `.env` and fill in:
   - `VIRTUAL_HOST`: Your domain (e.g., uptime.example.com)
   - `LETSENCRYPT_HOST`: Same as VIRTUAL_HOST
   - `LETSENCRYPT_EMAIL`: Your email for Let's Encrypt

3. Transfer to VPS:
   ```bash
   rsync -av /Users/antoine/Perso/uptime-status/ vps:/path/to/uptime-status/
   ```

4. On VPS, start the container:
   ```bash
   cd /path/to/uptime-status
   docker compose up -d
   ```

## Features
- Lightweight status page
- Monitor HTTP(s), TCP, DNS, Ping, and more
- SQLite database (no external DB needed)
- Web UI for configuration at `https://VIRTUAL_HOST`
