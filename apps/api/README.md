# @rc-hub/api

Backend API — Schicht zwischen Apps und Application Layer.

## Verantwortung

- HTTP Endpoints (REST/GraphQL — TBD)
- Request Validation
- Auth Middleware
- Use Case Exposition

## Architektur-Regel

```
Route Handler → Application Use Case → Domain Port → Infrastructure Adapter
```

**Kein direkter Prisma-Zugriff in Route Handlers.**

## Port

`3002` (Entwicklung)

## Status

🔲 Scaffold ausstehend — wartet auf API-Strategie (ADR-003)
