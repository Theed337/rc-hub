# ADR-001: Monorepo-Strategie

**Status:** Akzeptiert  
**Datum:** 2026-07-14  
**Entscheider:** Lead Software Architect

## Kontext

RC Hub besteht aus mehreren Apps (Website, Admin, API) und geteilten Packages. Enterprise-Anforderungen verlangen konsistente Tooling, geteilte Typen und reproduzierbare Builds.

## Entscheidung

Wir nutzen ein **Turborepo-Monorepo** mit **pnpm Workspaces**.

```
rc-hub/
├── apps/          # Deployable Applications
├── packages/      # Shared Libraries (Clean Architecture Layers)
├── docker/        # Local Infrastructure
└── docs/          # Architecture & Decisions
```

### Begründung

| Kriterium | Turborepo + pnpm |
|-----------|------------------|
| Build-Caching | Remote & lokal, task-basiert |
| Workspace-Isolation | Strikte `package.json`-Grenzen |
| Dependency-Deduplizierung | pnpm content-addressable store |
| Enterprise-Erfahrung | Breit eingesetzt (Vercel, große Teams) |

### Package-Namenskonvention

```
@rc-hub/<name>
```

Beispiele: `@rc-hub/web`, `@rc-hub/domain`, `@rc-hub/ui`

## Konsequenzen

### Positiv
- Einheitliche TypeScript-, ESLint- und Tailwind-Konfiguration über `packages/config-*`
- Geteilte Domain-Logik ohne Duplikation
- Parallele CI-Builds pro betroffenem Package (Turborepo `--filter`)

### Negativ
- Höhere initiale Komplexität gegenüber Single-Repo
- Team muss Workspace-Konventionen einhalten

## Alternativen (verworfen)

| Alternative | Grund der Ablehnung |
|-------------|---------------------|
| Multi-Repo | Geteilte Typen/Domain erfordern Versionierung & Publishing — Overhead |
| Nx | Gleichwertig, Turborepo enger mit Next.js/Vercel-Ökosystem |
| npm Workspaces | pnpm schneller, striktere Dependency-Isolation |

## TODO

- [ ] CI/CD-Pipeline definieren (GitHub Actions?)
- [ ] Remote Turborepo Cache konfigurieren
