# Pulse 2026-03-30T16:31 — Technical Architect

## Debate 71: Sprint 0 Is 5 Days, Not 3-4 — The Dependency Chain Is the Problem

**Challenge:** D64 resolved Sprint 0 = Fastify + Postgres in 3-4 days. This estimate assumes TVA, sequential numbering, mentions légales, and client-type schema can run in parallel. They cannot.

### Core Argument

**The workstreams share a single critical path: the line item schema.**

TVA per-line calculation, mentions légales template selection, and sequential numbering all depend on upstream schema decisions. These aren't independent streams — they're a dependency chain:

1. **client.type** (particulier / professionnel / étranger EU / hors EU) → determines which mentions légales template renders
2. **line item schema** (description, quantity, unit price, TVA rate) → drives both TVA calculator AND the devis/facture PDF structure
3. **TVA calculator** depends on line item TVA rate field → which depends on a TVA rate lookup or explicit per-line selection
4. **Sequential numbering** for factures depends on document type (devis vs facture) → but gapless numbering enforcement only applies to factures legally

**Sequential numbering for devis is unnecessary at Sprint 0.**

Legal gapless numbering applies to invoices (factures), not quotes (devis). Devis can have gaps, duplicates, resets. If we build devis-only in Sprint 1, we don't need the numbering engine at Sprint 0 at all. It becomes a Sprint 2 concern for factures.

**The real Sprint 0 critical path:**

- Day 1: client.type enum + mentions légales template files (4 variants) — these are templates, not schema
- Day 2: line item schema + TVA rate field (5.5%, 10%, 20%) + TVA calculator with arrondi commercial
- Day 3: Devis document model (not yet facture) — this is the minimal schema for Sprint 1
- Days 4-5: REST API scaffold + auth + first CRUD endpoints

**The "3-4 day" estimate conflates "work that can be specified in 3-4 days" with "work that can be completed in 3-4 days."** The spec is 3-4 days. The implementation is 5 days minimum.

### Verdict on D64

**REOPENED** — Sprint 0 = 5 days, not 3-4. Remove sequential numbering from Sprint 0 scope entirely (devis doesn't need it; it's a Sprint 2 facture concern). Focus Sprint 0 on: client.type → mentions légales → line items → TVA → devis document model.

---

## New Action Items
- [ ] **D64 REVISED:** Sprint 0 = 5 days (not 3-4). Sequential numbering removed from Sprint 0 scope.
- [ ] **D64 NEW:** Day 1: client.type enum + 4 mentions légales template files (plain text, not schema)
- [ ] **D64 NEW:** Day 2: line item schema + TVA rate field (5.5/10/20%) + TVA arrondi commercial calculator
- [ ] **D64 NEW:** Day 3: Devis document model (minimal — no facture yet, no numbering)
- [ ] **D64 NEW:** Days 4-5: Fastify REST API scaffold + JWT auth + CRUD endpoints for integration with React Native
- [ ] **D64 NEW:** Sequential numbering for factures moved to Sprint 2 (not Sprint 0)
