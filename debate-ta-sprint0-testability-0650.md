# POSITION PAPER
## Topic: Sprint 0 Testability — Can a Beta User Actually Test by Day 6.5?
**Author:** Technical Architect
**Date:** 2026-03-31

## Executive Summary

Both the Growth Strategist (GS-Sprint0Timing-0559) and Product Strategist (PS-beta-validity-0630) debate whether 5 beta users can validate the app — but neither questions whether the app will exist in a testable state by day 6.5. The assumption that "Sprint 0 produces a testable artifact by day 6.5" is technically unsound. A Supabase-connected React Native app with a real schema, TVA calculator, sequential numbering, and mentions légales templates cannot be built, debugged, and smoke-tested in 6.5 days by a solo developer. The debate about whether beta users constitute "validation theater" is premature — the more fundamental problem is that there may be no artifact to validate at all.

## Section 1: The Technical Reality of 6.5 Days

The Sprint 0 scope, as currently planned, includes:

1. **Supabase project setup** — project creation, schema design, RLS policies, auth
2. **Expo/React Native project** — init, navigation, state management, API client
3. **Offline architecture** — expo-sqlite, documents table, draft semantics, sync logic
4. **Core business logic** — TVA calculator (20%/10%/5.5% rates), sequential invoice numbering
5. **Legal compliance** — mentions légales templates (French invoice legal requirements)
6. **Frontend happy path** — devis → facture → WhatsApp PDF flow
7. **Real device testing** — APK builds, testing on actual Android hardware

Each of these is a full day of work. Together, they constitute approximately 8-10 developer-days of effort. The 6.5-day sprint assumes all of this compresses cleanly through parallelization and optimistic estimates. It does not.

### Where Time Actually Goes

**Days 1-2: Infrastructure trap**
Supabase project creation, schema design, and RLS policy writing are sequential — you cannot write RLS policies before defining your schema. Expo project init, dependency installation, and auth flow are sequential — you cannot connect to Supabase before the project exists. The offline architecture (expo-sqlite, documents table, migration runner) is a 2-day minimum taskblock with internal dependencies that cannot be parallelized.

**Days 3-4: Business logic sinkhole**
The TVA calculator is not a simple multiplication. French VAT requires:
- Three rate tiers (20% normal, 10% reduced, 5.5% special)
- TVA intracommunautaire for EU B2B invoices
- Proper rounding rules (demi-centime)
- TVA calculation per line item, then aggregated

Sequential numbering requires coordination with the offline-first architecture — the same invoice number cannot be issued twice, even if a draft was created offline and confirmed later. This requires Supabase triggers or Edge Functions, which add complexity.

Mentions légales are not copy-paste templates. French law requires specific content: SIREN/SIRET, RCS registration, VAT intracommunautaire number, capital social, and director name. These must be real (or legally-safe fictional) values. Until Louis commits these to git, the feature cannot be completed.

**Days 5-6: Integration and testing hell**
The devis → facture → WhatsApp PDF flow is not a single screen. It spans:
- Client selection or creation
- Line item management (add/remove/edit)
- TVA calculation per item
- Total aggregation
- PDF generation
- WhatsApp share intent
- Each step requires error handling, loading states, and edge cases

Building this end-to-end, debugging on a real device (not emulator), and verifying no crashes is a 2-day task minimum.

**Day 6.5: The uncomfortable math**
If Days 1-6 are fully consumed by the above (and they will be, on a good day), day 6.5 is when the smoke test would theoretically begin. But day 6.5 is not a real day — it is the sprint boundary. The smoke test would begin as the sprint ends.

## Section 2: Why "Schema-First" is the Wrong Approach for This Timeline

The current Sprint 0 plan is schema-first: define the complete schema (TVA, sequential numbering, mentions légales, documents table), build the backend, then connect the frontend. This approach has a fundamental timing problem.

A schema-first approach requires:
1. Complete schema design before any code is written
2. All business rules finalized before any UI exists
3. Legal text committed before any invoice can be generated

In a 6.5-day sprint, schema-first means:
- Days 1-3: Schema and backend (nothing to show)
- Days 4-5: Fragmented frontend (partially connected)
- Days 5-6: Integration scramble (connecting what was built in pieces)
- Day 6.5: Hope that it works

### The Alternative: Happy Path First

A happy-path-first approach produces a testable artifact faster:
1. **Day 1:** Minimal Supabase schema (clients table only), Expo project with auth
2. **Day 2:** Devis creation screen (hardcoded TVA, sequential number from counter)
3. **Day 3:** WhatsApp share, PDF generation, client list
4. **Day 4:** Real device testing, bug fixes
5. **Day 5:** Beta users test the happy path — it works or it doesn't
6. **Day 6+:** Add TVA complexity, sequential numbering with proper locking, mentions légales

The happy-path-first approach answers the only question that matters in Sprint 0: **does the core flow work on a real device?**

## Core Position

**The assumption that Sprint 0 produces a testable artifact by day 6.5 is false.**

A schema-first approach with TVA calculator, sequential numbering, mentions légales templates, and offline-first architecture cannot compress into 6.5 days while producing a testable artifact. The "5 beta user smoke test" gate is not meaningful because the artifact it would test does not exist by day 6.5 under the current plan.

Both the Growth Strategist's "validation theater" critique and the Product Strategist's "smoke test" defense are debating the value of a test that cannot happen as scheduled. The prior question — whether the app will be buildable by day 6.5 — is answered: it will not be, if the current schema-first plan is followed.

## Resolution Proposal

**Option A: Shrink the Sprint 0 Artifact (Recommended)**
Restrict Sprint 0 to the minimum viable testable flow:
- Supabase: clients + devis tables only (no factures, no reminders, no documents table)
- TVA: hardcoded 20% for Sprint 0 (add tiered TVA post-Sprint 0)
- Sequential numbering: simple local counter (add proper locking post-Sprint 0)
- Mentions légales: placeholder text (e.g., "[Legal info to be added]")
- Offline: skip entirely for Sprint 0 (add post-Sprint 0)

This produces a testable devis → WhatsApp PDF flow by day 4-5, leaving day 5-6 for the smoke test with real beta users.

**Option B: Extend Sprint 0 to 10 Days**
If the full schema-first scope is non-negotiable (TVA tiers, sequential numbering with proper locking, mentions légales, offline-first), Sprint 0 must be 10 days. The 6.5-day estimate is not aggressive — it is impossible given the scope.

**Option C: Parallel Confirmation Gates**
Move all non-development tasks (mentions légales content from Louis, Supabase project creation) to pre-Sprint 0 blockers. Sprint 0 should not begin until:
1. Mentions légales real content committed to git
2. Supabase project created and accessible
3. Expo project initialized with basic auth connected to Supabase

This prevents Sprint 0 from being consumed by setup while development waits on Louis.

---

*End of Position Paper*