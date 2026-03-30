# Debate 74: Sprint 0 — 5 Days Is Defensible With Scope Clarifications

**Role:** Technical Architect (Specialist)
**Date:** 2026-03-30
**Status:** COUNTER-CHALLENGE

---

## My Challenge Against the Current Resolution

**I challenge the implicit assumption in all three challenges: that "Sprint 0" means "deliver everything production-ready before any parallel work can begin."**

This conflates two distinct questions:
1. What must the backend deliver in Sprint 0? (Backend scope)
2. What must be production-ready before React Native integration begins? (Integration readiness)

**The 5-day estimate was never about shipping a production auth system. It was about delivering compliance foundations + API contract.** The challenges are attacking a strawman: a "2-3 day JWT" that no one proposed.

---

## Response to Challenge 1 — JWT Auth Is 2-3 Days

**CONCEDE:** The 0.5-1 day estimate is too optimistic IF the deliverable is "production auth with Keychain, refresh rotation, and secure storage."

**PUSH BACK:** This is not what Sprint 0 needs from JWT.

The Sprint 0 deliverable for the backend is "Fastify + Postgres compliance foundations." The mobile team's Sprint 0 parallel work is building the UI shell — they don't need a working auth system in Sprint 0; they need the **API contract** to build against.

The correct Sprint 0 JWT scope is:
- Define auth endpoints in OpenAPI (0.25 day): `POST /auth/login`, `POST /auth/refresh`, `POST /auth/logout`, `GET /auth/me`
- Implement stub handlers that return the correct JSON shapes (0.25 day)
- Issue JWTs using `@fastify/jwt` with correct TTLs (0.5 day — this is just config)
- Document the JWT payload schema, TTLs, and refresh token flow in the API spec

This is **contract-first API design**, not "build production auth." The Keychain, refresh queue, and token rotation are **Sprint 1 deliverables** — precisely because the mobile team can't build the auth UI in Sprint 0 anyway (they're building the devis creation flow).

**Refined JWT estimate for Sprint 0: 0.5-1 day** (contract + stubs + `@fastify/jwt` config)
**Actual JWT cost deferred to Sprint 1: 1.5-2 days** (Keychain, refresh queue, logout, rotation)

This is not a 2-3 day gap. This is correct scoping: Sprint 0 defines what auth will look like; Sprint 1 builds it.

**However:** I concede the 5-day estimate did not make this distinction explicit. The debate log should clarify: JWT in Sprint 0 = contract + stubs, not production auth. Without this clarification, future implementers will default to "ship the full thing" and blow the timeline.

---

## Response to Challenge 2 — 8 Mentions Légales Combinations

**CONCEDE:** The 4-template math is wrong. 4 static files cannot cover 4 client types with correct legal text.

**PUSH BACK:** The 8-combination problem is a **Sprint 2 problem**, not a Sprint 0 problem.

Sprint 0 scope is **devis only**. Sprint 1 builds the client file + devis flow. Sprint 2 adds factures.

The client type × document type matrix produces 8 combinations, but:
- **Devis combinations needed in Sprint 0-1:** 4 (particulier/professionnel français/professionnel UE/professionnel hors-UE devis)
- **Facture combinations needed in Sprint 2:** 4 additional (particulier/professionnel français/professionnel UE/professionnel hors-UE facture)

The challenge states: "Devis mentions légales errors are less penal than factures — but the template system must be document-type-aware from Sprint 0 to avoid Sprint 1 retrofitting."

**This is incorrect.** A template system that renders devis correctly for 4 client types in Sprint 0 is not "wrong" — it's the correct scope. When Sprint 2 adds factures, the template engine already has client-type discrimination. Adding document-type (devis vs facture) discrimination at that point is not a retrofit — it's a natural feature addition on top of a working client-type system.

**The "must be document-type-aware from Sprint 0" argument assumes** that Sprint 1 builds both devis AND facture flows simultaneously. It does not. Sprint 1 is client file + devis only.

**Refined mentions légales estimate for Sprint 0:**
- 4 data-driven templates using Handlebars/Nunjucks (1 template per client type, not per document type)
- Conditional blocks for devis-specific vs facture-specific text
- Estimated: **0.5-0.75 days** (template engine setup + 4 client-type templates)

The "4 template files" framing in the debate log was too naive (static files approach). The correct implementation is a template engine with client-type conditionals, which was always the intent. This adds ~0.25 days over the original estimate.

**8-combination scope is legitimate for Sprint 2, not Sprint 0.**

---

## Response to Challenge 3 — Missing Devis Status Enum

**FULLY CONCEDE.** This is the strongest challenge.

The debate log says "Devis document model (minimal — no facture yet)." Without `devis.status`, Sprint 1 must:
1. Build the sending UI (requires `status = sent`)
2. Build client acceptance flow (requires `status = accepted/rejected`)
3. Build expiration logic (requires `status = expired`)
4. All while working around a missing status field

This is not "0.5-1 day of retrofit work" — this is "build the entire Sprint 1 feature set while simultaneously doing a migration." The integration risk is real: migrations during active development can break existing queries, require ORM updates, and introduce subtle bugs in status transition logic that only surface in production.

**The fix is trivial and the cost estimate in the challenge is wrong.**

Add to the Sprint 0 Devis schema:

```sql
ALTER TABLE devis ADD COLUMN status TEXT NOT NULL DEFAULT 'draft';
COMMENT ON COLUMN devis.status IS 'draft|sent|accepted|rejected|expired';
```

This is **30 minutes of schema work** in Sprint 0, not 0.5-1 days. The full status state machine (valid transitions, expiration cron job, etc.) can be Sprint 1 work. But the column must exist from Sprint 0 with a default, so no migration is needed when Sprint 1 starts building the status-aware UI.

**The challenge overestimates this cost by treating "add enum" as "build state machine."** Adding the column is 30 minutes. Building the state machine is Sprint 1's job.

---

## Revised Assessment

| Risk | Challenge claim | My assessment | Adjusted estimate |
|---|---|---|---|
| JWT auth | 2-3 days | Sprint 0 = contract + stubs (0.5-1d). Full auth = Sprint 1. | +0 days to Sprint 0 (clarification only) |
| Mentions légales | 4 templates wrong; 8 needed | Sprint 0 only needs 4 (devis only). Sprint 2 adds 4 (factures). Template engine adds ~0.25d. | +0.25 days |
| Devis status | Sprint 1 retrofit | Add `status TEXT DEFAULT 'draft'` in Sprint 0 (30 min). State machine = Sprint 1. | +0.1 days |

**Net adjustment to 5-day estimate: +0.35 days** — well within the original estimate with normal slack.

---

## The Assumption I Challenge

**I challenge the assumption that "production-ready" must be achieved before Sprint 0 ends.**

The Sprint 0 definition from the debate log is: "Fastify + Postgres compliance foundations, client.type + mentions légales + line item schema + TVA engine."

None of these deliverables require:
- Production auth (Keychain, refresh queue)
- Facture mentions légales (Sprint 2 scope)
- A complete Devis state machine (Sprint 1 feature)

The challenges conflate "shipping a production system" with "laying the right foundations." Sprint 0 is supposed to be foundations — schema, templates, TVA calculator. Not a finished product.

**If we demand production-ready auth before Sprint 0 ends, then Sprint 0 isn't a foundations sprint — it's a full MVP sprint wearing a foundations costume.**

---

## Resolution

**Option B — Defend 5 days with rebuttals and clarifications:**

Sprint 0 remains **5 days**, with these explicit scope clarifications:

**Day 1:** `client.type` enum (4 values) + mentions légales template engine (4 client-type templates with Handlebars/Nunjucks, devis-only)

**Day 2:** Line item schema (`ligne_devis` with TVA rate field) + TVA arrondi commercial calculator

**Day 3:** Devis document model + `devis.status TEXT DEFAULT 'draft'` (no state machine yet; Sprint 1 adds transitions)

**Days 4-5:** Fastify REST API scaffold
- `POST /auth/login` (stub returning correct shape; full auth in Sprint 1)
- `POST /auth/refresh` (stub)
- `POST /auth/logout` (stub)
- `GET /auth/me` (stub)
- Full `@fastify/jwt` configured with correct TTLs (config only, not the client-side Keychain work)
- CRUD endpoints: `POST/GET /clients`, `POST/GET/PATCH /devis`, `POST/GET/PATCH /devis/:id/lignes`
- Database migrations (all Sprint 0 tables)

**What Sprint 0 does NOT include (deferred to Sprint 1):**
- `react-native-keychain` / `expo-secure-store` integration
- Refresh token rotation
- Token revocation list
- Auth request queue with mutex
- Full state machine for `devis.status`

**The 5-day estimate is defensible** because the three challenges attack strawmen: production-ready auth, 8-combination scope, and a full state machine. None of these are Sprint 0 deliverables.

**The debate log should be updated to explicitly scope Sprint 0 vs Sprint 1 auth**, because without that clarification, an implementer will attempt to ship production auth in Sprint 0 and fail.

---

## Verdict

**Debate 74: Sprint 0 5-day estimate is DEFENSIBLE** with the following conditions:

1. JWT Sprint 0 scope = contract + stubs + `@fastify/jwt` config. Full auth = Sprint 1. Must be documented.
2. Mentions légales = 4 templates (devis × client type). 8 combinations = Sprint 2 scope.
3. `devis.status TEXT DEFAULT 'draft'` added in Sprint 0 schema (30 min). State machine = Sprint 1.

**No timeline extension required.** The challenges overestimate the Sprint 0 scope by borrowing from Sprint 1 and Sprint 2 requirements.

**If the team chooses to implement production auth in Sprint 0 anyway** (e.g., because mobile integration is blocked without it), then the estimate becomes **6 days**: 5 days as planned + 1 day for Keychain, refresh queue, and logout handler. But this is a product decision, not a technical requirement.

**Recommended debate log update to D71/D73 resolution:**
```
| D73 | Sprint 0 timeline | CONTESTED — Technical Architect defends 5 days with clarifications: 
JWT = contract+stubs (Sprint 1 = full auth). Mentions légales = 4 templates, devis-only (8 = Sprint 2). 
Devis status = 30-min schema addition in Sprint 0. State machine = Sprint 1. |
```
