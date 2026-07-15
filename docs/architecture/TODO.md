# Offene Architektur-Entscheidungen

> Keine Annahmen — jeder Punkt muss vor Implementierung geklärt werden.

## 🔴 Blockierend (vor erstem Feature)

### Domänenmodell
- [ ] **Was ist RC Hub?** — Beschreibung des Geschäftszwecks
- [ ] **Kern-Entities** — Welche Aggregate gibt es? (z. B. User, Project, Device, …)
- [ ] **Rollen & Permissions** — Welche User-Rollen existieren?

### API-Strategie {#api-strategie}
- [ ] Next.js Route Handlers vs. dedizierter Server (Hono/Elysia) vs. tRPC
- [ ] REST vs. GraphQL
- [ ] API-Versionierung

### Authentifizierung
- [ ] NextAuth Provider (Google, GitHub, Credentials, OIDC?)
- [ ] Session-Strategie (JWT vs. Database Sessions)
- [ ] Wie unterscheiden sich Web- vs. Admin-Sessions?

## 🟡 Wichtig (vor Production)

### Redis
- [ ] Einsatzzweck: Cache, Session Store, Rate Limiting, Job Queue?
- [ ] TTL-Strategien

### Datenbank
- [ ] Multi-Tenancy erforderlich?
- [ ] Soft-Delete vs. Hard-Delete
- [ ] Audit-Log Anforderungen

### Deployment
- [ ] Zielumgebung (Vercel, AWS, Azure, Self-Hosted?)
- [ ] Staging/Production-Umgebungen
- [ ] Secrets Management

### 3D / Animation (Website)
- [ ] Welche Seiten nutzen Three.js / R3F?
- [ ] Performance-Budget (Lighthouse Score Ziel)
- [ ] Fallback für Geräte ohne WebGL

## 🟢 Kann später geklärt werden

### Internationalisierung
- [ ] i18n erforderlich? Welche Sprachen?

### Observability
- [ ] Logging (Pino, Winston?)
- [ ] Monitoring (Sentry, Datadog?)
- [ ] Analytics

### Testing
- [ ] E2E-Framework (Playwright?)
- [ ] Coverage-Ziele

### CI/CD
- [ ] GitHub Actions Pipeline
- [ ] Turborepo Remote Cache Provider

---

**Nächster Schritt:** Domänenmodell & API-Strategie mit Stakeholder klären, dann Scaffold der Apps.
