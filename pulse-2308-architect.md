# Pulse 2308 — Technical Architect

## Debate: C — Offline-Capable vs Offline-First (D81)

**Counter-Assumption:** That "offline-capable" (optimistic UI + retry queue + AsyncStorage) is sufficient for French artisans working in basements, rural sites, and concrete buildings.

---

## Core Argument

The current decision inverts the actual problem. "Offline-capable" means: when the artisan loses signal in a basement, entries go into a retry queue. When connectivity returns, the queue processes. That is not offline-first. That is offline-*tolerant* at best, and offline-*deferred* at worst.

Consider the failure mode. A façadier arrives at a rural renovation site. No signal. He logs 4 hours of labor against three tasks, adds notes, attaches a photo of the wall condition. He leaves the site. Three hours later, connectivity returns. The retry queue fires. Except — his phone died at hour 2 (this happens constantly on site). Or he was in a train tunnel (French TER has massive coverage gaps). Or the Supabase client crashed during sync (unhandled, unrecoverable without manual intervention). What happens to that data? It's gone. Or worse — it's ambiguous. Did it sync? Did it not? There's no deterministic answer without building a full conflict-resolution layer, which D81 explicitly deferred.

The architects seem to treat "offline-capable" as a comfort word — the app can handle being offline briefly. But for this user and this use case, offline is not the exception. It's the default working condition. These artisans spend 40% of their working hours in environments where 4G simply does not reach — basements, interior renovation floors, rural perimeters, steel-framed buildings. Designing for the 60% connected case and hoping the retry queue handles the 40% is not a product strategy. It's a hope.

Furthermore, the decision conflates "optimistic UI" (UI responds instantly assuming success) with "offline persistence" (data survives the offline period). These are orthogonal concerns. You can have optimistic UI with local persistence (WatermelonDB). You can have optimistic UI without it (current design). The retry queue adds complexity without solving the core issue: what happens when the retry never happens?

If job logging is Sprint 1 non-negotiable, and job logging happens on job sites where connectivity is the exception, then "offline-capable" is a feature that fails precisely where the user most depends on it. We would be shipping a feature that looks functional in the office and fails in the field.

## Verdict

Deferring WatermelonDB/expo-sqlite to v1.2 is the wrong call if job logging is a Sprint 1 deliverable. The architecture should include local SQLite persistence in Sprint 0 — not as a nice-to-have, but as the foundational layer that makes job logging actually work. The retry queue should be a sync reliability mechanism, not the primary offline data survival strategy. Either job logging works offline in Sprint 1, or it shouldn't be in Sprint 1.

**Status:** REOPENED — added to debate-log as Debate 127
