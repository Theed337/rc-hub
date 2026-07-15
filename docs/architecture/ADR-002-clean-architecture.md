# ADR-002: Clean Architecture

**Status:** Akzeptiert  
**Datum:** 2026-07-14  
**Entscheider:** Lead Software Architect

## Kontext

RC Hub soll Enterprise-Niveau erreichen. Business-Logik darf nicht an Frameworks, Datenbanken oder UI gekoppelt sein.

## Entscheidung

Strikte **4-Schichten-Architektur** über dedizierte Packages:

```
┌─────────────────────────────────────────┐
│  Presentation (apps/*)                  │  ← Next.js, Routing, UI Composition
├─────────────────────────────────────────┤
│  Application (packages/application)       │  ← Use Cases, Orchestrierung
├─────────────────────────────────────────┤
│  Domain (packages/domain)               │  ← Entities, Value Objects, Ports
├─────────────────────────────────────────┤
│  Infrastructure (packages/infrastructure)│  ← Prisma, Redis, External APIs
└─────────────────────────────────────────┘
```

## SOLID-Mapping

| Prinzip | Umsetzung in RC Hub |
|---------|---------------------|
| **S** — Single Responsibility | Jedes Package hat genau eine Schicht-Verantwortung |
| **O** — Open/Closed | Neue Adapter in Infrastructure, Domain unverändert |
| **L** — Liskov Substitution | Port-Implementierungen austauschbar (z. B. In-Memory für Tests) |
| **I** — Interface Segregation | Kleine Repository-Ports pro Aggregate |
| **D** — Dependency Inversion | Application hängt von Domain-Ports ab, nicht von Prisma |

## Package-Verantwortlichkeiten

### `packages/domain`
- Entities & Aggregate Roots
- Value Objects
- Domain Events
- Repository-Interfaces (Ports)
- Domain Services (nur wenn domänenrelevant)

**Verboten:** Imports aus `infrastructure`, `apps`, Frameworks

### `packages/application`
- Use Case Interfaces & Implementierungen
- Input/Output DTOs
- Application Service Orchestrierung
- Transaction Boundaries

**Erlaubt:** Imports aus `domain`, `shared-kernel`  
**Verboten:** Imports aus `infrastructure`, `apps`

### `packages/infrastructure`
- Prisma Repository Implementierungen
- Redis Cache Adapter
- External API Clients
- E-Mail, Storage, etc.

**Erlaubt:** Imports aus `domain`, `application`, `database`, `shared-kernel`

### `packages/shared-kernel`
- `Result<T, E>` Typ
- Basis-Fehlerklassen (`DomainError`, `ApplicationError`)
- Gemeinsame Value Objects (z. B. `Email`, `Uuid`)

## Dependency Enforcement

→ TODO: `dependency-cruiser` oder ESLint `import/no-restricted-paths` Regeln in Phase 2

## Konsequenzen

- Jede neue Feature-Entwicklung beginnt in `domain` (Modell) → `application` (Use Case) → `infrastructure` (Adapter) → `apps` (Wiring)
- Tests: Domain & Application ohne Datenbank testbar
- Höherer Datei-/Package-Overhead — bewusst akzeptiert für Wartbarkeit

## TODO

- [ ] Dependency-Graph-Linting einrichten
- [ ] Test-Strategie pro Schicht dokumentieren (ADR-004)
