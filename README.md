# PostHog hobby stack

Official PostHog hobby compose, adapted for a dedicated server at `hog.oryxbms.com`
(Timeweb `nl-1`, 8 vCPU / 16 GB / 160 GB NVMe).

- Caddy publishes `80`/`443`; set `CADDY_HOST=hog.oryxbms.com` in `.env` so it obtains the Let's Encrypt certificate.
- App images are pinned to local tags in `.env` (`POSTHOG_APP_TAG`, `POSTHOG_NODE_TAG`)
  so a restart never pulls a newer `latest` with unapplied migrations.
- Elasticsearch and Temporal UI are omitted.

## Deploy

```bash
cd /opt/posthog
git pull
docker compose up -d --remove-orphans
# Bind-mounted ClickHouse config/UDFs are re-read only on restart.
docker compose restart clickhouse
```

Do not commit secrets. `POSTHOG_SECRET` and `ENCRYPTION_SALT_KEYS` live only in
`/opt/posthog/.env` on the server; changing them breaks encrypted Postgres fields.
