# PostHog hobby stack for Dokploy

Official PostHog hobby compose, adapted so Traefik (Dokploy) terminates TLS.

- Caddy listens on `:80` inside the compose network and routes capture/flags/web.
- Host ports 80/443 and other public infrastructure ports are not published.
- Kafka/ClickHouse memory is capped for a shared 16GB VPS.
- Elasticsearch and Temporal UI are omitted.

Do not commit secrets. Put `POSTHOG_SECRET` and `ENCRYPTION_SALT_KEYS` in Dokploy env.
