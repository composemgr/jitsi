## 👋 Welcome to jitsi 🚀

Self-hosted video conferencing with chat, whiteboard, and transcription

## 📋 Description

Self-hosted video conferencing with chat, whiteboard, and transcription

## 🚀 Services

- **web**: ghcr.io/jitsi/web:unstable
- **prosody**: ghcr.io/jitsi/prosody:unstable
- **jicofo**: ghcr.io/jitsi/jicofo:unstable
- **jvb**: ghcr.io/jitsi/jvb:unstable


## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/jitsi/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/jitsi" ~/.local/srv/docker/jitsi
cd ~/.local/srv/docker/jitsi
cp default.env .env
docker compose --env-file .env up -d
```

### Option 3: Using composemgr
```bash
composemgr install jitsi
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
APP_API_TOKEN=replace-with-a-random-app-id
APP_SECRET_KEY=replace-with-a-random-16-byte-hex-string
```

See `docker-compose.yaml` for complete list of configurable options.

### Environment Files

`default.env.sample` holds the full set of variables and is copied to `.env`
before starting the stack:

```bash
cp default.env .env
docker compose --env-file .env up -d
```

`app.env.sample` holds the app-specific overrides and is copied to `app.env`:

```bash
cp app.env.sample app.env
```

`composemgr up` applies `app.env` and `default.env` automatically. Raw
`docker compose` commands need `--env-file .env` to pick up the same values.

### Reverse Proxy

Three standalone compose files ship in this repo:

| File | Use |
|------|-----|
| `docker-compose.yaml` | Default, published on `172.17.0.1:64217` |
| `docker-compose.traefik.yaml` | Behind an existing external `traefik` network |
| `docker-compose.tunnel.yaml` | Behind an existing external `cloudflare` tunnel network |

```bash
docker compose -f docker-compose.traefik.yaml --env-file .env up -d
```

## 🌐 Access

- **Web Interface**: http://172.17.0.1:64217

## 📂 Volumes


- `./volumes/config/jitsi` - Web configuration
- `./volumes/config/jitsi/cron` - Cron configuration
- `./volumes/config/prosody` - Prosody XMPP configuration
- `./volumes/data/prosody` - Custom Prosody plugins
- `./volumes/config/jicofo` - Jicofo configuration
- `./volumes/config/jvb` - JVB configuration
- `./volumes/data/jitsi/transcripts` - Recording transcripts

## 🔐 Security

- Change all default passwords before deploying to production
- Use strong secrets for all authentication tokens
- Configure HTTPS using a reverse proxy (nginx, traefik, caddy)
- Regularly update Docker images for security patches
- Backup your data regularly

## 🔍 Logging

```shell
docker compose --env-file .env logs -f web
```

## 🛠️ Management

```bash
# Start services
docker compose --env-file .env up -d

# Stop services
docker compose --env-file .env down

# Update to latest images
docker compose --env-file .env pull && docker compose --env-file .env up -d

# View logs
docker compose --env-file .env logs -f

# Restart services
docker compose --env-file .env restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
