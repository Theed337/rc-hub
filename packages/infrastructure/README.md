# @rc-hub/infrastructure

**Clean Architecture — Infrastructure Layer (äußerste Schicht)**

## Enthält

- Prisma Repository Implementierungen
- Redis Cache Adapter
- External API Clients
- E-Mail, File Storage, etc.

## Regeln

- ✅ Implementiert Ports aus `@rc-hub/domain`
- ✅ Imports aus `@rc-hub/domain`, `@rc-hub/application`, `@rc-hub/database`

## Status

🔲 Implementierung ausstehend
