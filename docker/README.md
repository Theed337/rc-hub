# Docker — Local Infrastructure

Lokale Entwicklungsumgebung für PostgreSQL und Redis.

## Starten

```bash
docker compose -f docker/docker-compose.yml up -d
```

## Stoppen

```bash
docker compose -f docker/docker-compose.yml down
```

## Services

| Service | Port | Credentials |
|---------|------|-------------|
| PostgreSQL 16 | 5432 | `rchub` / `rchub` |
| Redis 7 | 6379 | — |

## Hinweis

Produktions-Deployment ist noch nicht definiert → siehe `docs/architecture/TODO.md`
