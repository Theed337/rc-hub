# RC Hub

Enterprise-Plattform — Monorepo auf Basis von **Clean Architecture** und **SOLID**.

## Status

🟡 **Phase: Projektstruktur** — Architektur definiert, Implementierung folgt.

## Apps

| App | Pfad | Zweck |
|-----|------|-------|
| Website | `apps/web` | Öffentliche Web-Präsenz (Next.js 15) |
| Admin Dashboard | `apps/admin` | Internes Verwaltungs-Frontend (Next.js 15) |
| API | `apps/api` | Backend-API-Schicht |

## Packages

| Package | Pfad | Schicht |
|---------|------|---------|
| Domain | `packages/domain` | Entities, Value Objects, Ports |
| Application | `packages/application` | Use Cases, Application Services |
| Infrastructure | `packages/infrastructure` | Adapter (Prisma, Redis, externe APIs) |
| Shared Kernel | `packages/shared-kernel` | Gemeinsame Primitives, Fehlertypen |
| Database | `packages/database` | Prisma Schema & Migrations |
| Auth | `packages/auth` | NextAuth-Konfiguration & Session-Logik |
| UI | `packages/ui` | Geteilte React-Komponenten |
| Config | `packages/config-*` | ESLint, TypeScript, Tailwind Presets |

## Dokumentation

→ [`docs/architecture/README.md`](docs/architecture/README.md)

## Voraussetzungen

- Node.js ≥ 20
- pnpm ≥ 9
- Docker & Docker Compose

## Schnellstart (nach Implementierung)

```bash
pnpm install
docker compose -f docker/docker-compose.yml up -d
pnpm dev
```
