# telegram-bot-api (Docker)

Unofficial Docker image of [Telegram Bot API Server](https://github.com/tdlib/telegram-bot-api),
referenced from [aiogram/telegram-bot-api](https://github.com/aiogram/telegram-bot-api).

Builds the upstream `tdlib/telegram-bot-api` source on a schedule and publishes
multi-arch images to the GitHub Container Registry (GHCR).

## Image

```
ghcr.io/bmw-ece-ntust/telegram-bot-api:latest
```

Supported architectures: `linux/amd64`, `linux/arm64`.

## Usage

```bash
docker run -d \
  -p 8081:8081 \
  --name=telegram-bot-api \
  --restart=always \
  -v telegram-bot-api-data:/var/lib/telegram-bot-api \
  -e TELEGRAM_API_ID=<api_id> \
  -e TELEGRAM_API_HASH=<api-hash> \
  ghcr.io/bmw-ece-ntust/telegram-bot-api:latest
```

Obtain `api-id` and `api-hash` from <https://my.telegram.org> as described in
<https://core.telegram.org/api/obtaining_api_id>.

## Configuration

| Variable | Default | Description |
|---|---|---|
| `TELEGRAM_API_ID` | — | Telegram API ID (required) |
| `TELEGRAM_API_HASH` | — | Telegram API hash (required) |
| `TELEGRAM_STAT` | `0` | Enable statistics endpoint on port 8082 |
| `TELEGRAM_VERBOSITY` | `1` | Log verbosity |
| `TELEGRAM_LOG_FILE` | — | Log file path (default: stdout/stderr) |
| `TELEGRAM_MAX_CONNECTIONS` | `1000` | Max open file descriptors |
| `TELEGRAM_LOCAL` | `0` | Allow local Bot API requests |
| `TELEGRAM_HTTP_IP_ADDRESS` | `0.0.0.0` | Listen IP |
| `TELEGRAM_HTTP_PORT` | `8081` | Listen port |
| `TELEGRAM_PROXY` | — | HTTP proxy for outgoing webhooks |

## Scheduled builds

GitHub Actions workflow rebuilds the image every weekday at **07:00 Asia/Taipei**
(`0 23 * * 0-4` UTC, i.e. Sun–Thu 23:00 UTC → Mon–Fri 07:00 UTC+8).

Only weekday runs; weekends skipped.

## Persistence

Server working dir: `/var/lib/telegram-bot-api`. Process runs as root.
