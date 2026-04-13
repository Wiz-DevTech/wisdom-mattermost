# wisdom-mattermost

Self-hosted team communication for **Wisdom Ignited Business Trust**.
Replaces Slack. Live at **https://chat.wisdomignited.com**

**Server:** Hetzner Cloud `ciphernex-node-1` — `37.27.214.143`

---

## First-Time Setup

```bash
# 1. SSH into Hetzner
ssh -i ciphernex-hetzner root@37.27.214.143

# 2. Clone repo
git clone https://github.com/Wiz-DevTech/wisdom-mattermost.git /opt/wisdom-mattermost
cd /opt/wisdom-mattermost

# 3. Create env file
cp .env.template .env
nano .env   # set MM_DB_PASSWORD and MM_ADMIN_PASSWORD

# 4. Create shared Docker network (if not exists)
docker network create wisdom-ops-net 2>/dev/null || true

# 5. Start
docker compose up -d

# 6. Add DNS record (from Codespace)
bash scripts/add-dns.sh
```

## After First Login

1. Visit **https://chat.wisdomignited.com** — complete setup wizard
2. Create channels: `#ciphernex` `#entities` `#deploys` `#ops`
3. Go to **Main Menu → Integrations → Incoming Webhooks**
4. Create one webhook per channel — copy URLs into `wisdom-notify` `.env`

## Required GitHub Secret

| Secret | Value |
|---|---|
| `SERVER_SSH_KEY` | `ciphernex-hetzner` ED25519 private key |
