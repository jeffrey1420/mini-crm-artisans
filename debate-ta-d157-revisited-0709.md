# Position Paper: TA-D157-Revisited

**Author:** Technical Architect  
**Date:** 2026-03-31 07:09 UTC  
**Challenge ID:** TA-D157-Revisited  
**Responds to:** Debate D157 (06:50 pulse) — "6.5 Days Is Insufficient for a Testable Artifact"

---

## Challenge Headline

**D157's diagnosis is correct. The conclusion is wrong.**

D157 correctly identifies that the current Sprint 0 plan — schema-first with TVA calculator, sequential numbering, mentions légales, offline architecture, and full devis→facture flow — cannot fit in 6.5 days and produce a testable artifact. But D157's proposed resolution ("shrink the artifact OR extend to 10 days") accepts the wrong premise. The problem is not the timeline. The problem is the plan's sequencing.

---

## Assumption Challenged

**D157 accepts that "schema-first is correct, the timeline is wrong."**

The correct framing is: **"schema-first is itself the wrong approach for a 6.5-day sprint."**

D157 recommends either shrinking the Sprint 0 artifact (hardcoded TVA, placeholder mentions légales, no offline) OR extending to 10 days. Both options accept that the current scope belongs in Sprint 0 — it just doesn't fit. But three of the five "shrink" recommendations are not shrink recommendations at all — they are **correct deferrals** that should have been Sprint 1 items all along. The fourth (offline) is a D9 decision that was already made.

---

## Core Arguments

### 1. TVA calculator complexity does not belong on the critical path for Sprint 0.

French TVA has three rate tiers (5.5%, 10%, 20%). The current Sprint 0 plan puts the full TVA calculator on the critical path — meaning Louis must implement multi-tier per-line VAT math before a devis can be considered "complete."

**This is wrong because:**
- A Sprint 0 devis with hardcoded 10% TVA is still a professional, real devis. It is testable.
- The beta user's question is: "Can I create a devis and send it to myself via WhatsApp?" — not "Is the TVA calculation correct per French tax law for rate-tier edge cases?"
- The three TVA tiers are a Sprint 1 refinement. They do not affect the core flow.
- **What is lost with hardcoded 10% TVA in Sprint 0?** Nothing meaningful. The beta user gets a real devis they can use. Louis gets real usage data. The TVA refinement is additive Sprint 1 work.

### 2. Sequential numbering with locking does not belong in Sprint 0.

Sequential numbering with server-side locking (no gaps, no duplicates, annual reset, recovery logic) is a 2-3 day task. It is currently on the Sprint 0 critical path.

**This is wrong because:**
- A simple auto-increment without locking is sufficient for Sprint 0. Two devis sent in the same day can have sequential numbers. The locking concern (concurrent writes causing duplicate numbers) is a multi-user problem — Louis is the only user in Sprint 0.
- Numbering enforcement is a compliance concern for formal facturas. Devis numbering is less regulated.
- **What is lost by dropping locking from Sprint 0?** A cosmetic defect (rare duplicate devis numbers during concurrent writes that won't happen in Sprint 0 anyway). What is gained: 2 days of breathing room in the schedule.

### 3. Mentions légales are boilerplate — not a schema task.

Mentions légales vary by client type (particulier, professionnel, étranger EU, hors EU). The current plan treats this as a schema and rendering complexity problem requiring dynamic logic.

**This is wrong because:**
- Mentions légales are static legal text. Louis has already researched the content (U16). The output is a string — not a dynamic query.
- For Sprint 0: a single hardcoded mentions légales block (suitable for a particulier client) is sufficient. Client-type-specific variants are Sprint 1.
- **What is lost?** Nothing testable. The devis looks professional with a standard mentions légales block. The variation by client type is a Sprint 1 feature enhancement.

### 4. Offline architecture (expo-sqlite + draft-mode) is a D9 item — not Sprint 0.

D9 explicitly deferred offline architecture. D140 (expo-sqlite + draft-mode) resolved offline for Sprint 1, not Sprint 0. The current Sprint 0 plan still lists offline as scope.

**This is wrong because:**
- D9 says: "No offline, no multi-user, no API keys." This was a decision. It stands.
- Sprint 0 is about the happy path. Offline resilience is a reliability concern for Sprint 1, not a Sprint 0 feature.
- **What is lost?** Nothing about the testable artifact. The happy path works fine without offline in Sprint 0. Beta users are on real devices with connectivity.

### 5. The "testable artifact" bar is defined incorrectly.

D157 sets the bar as "Sprint 0 produces a testable artifact by day 6.5." But D157's own "Happy Path First" alternative already implies the correct bar: **"Can I send a devis to myself via WhatsApp and does it look professional?"**

The full-compliance bar ("TVA correct per rate tier, sequential numbering enforced, mentions légales vary by client type") is a Sprint 1 quality bar. Sprint 0's bar is: **does the core flow work?**

---

## Revised Sprint 0 Plan — Happy Path First (4 Days)

The correct Sprint 0 scope is the narrowest possible path from "no app" to "a devis I can send to myself on WhatsApp."

### Day 1: Project Foundation + Minimal Schema
- Expo project setup + Supabase auth (magic link)
- Minimal schema: `clients` (id, name, phone, email) + `devis` (id, client_id, status, created_at)
- `devis_items` table (id, devis_id, description, quantity, unit_price, total) — single TVA field
- No TVA tiers. No sequential numbering enforcement. No mentions légales logic.

### Day 2: Devis Creation Screen
- Add client (name + phone only)
- Add line items (description, qty, price)
- Hardcoded 10% TVA on total only (display line: "TVA 10%: €X")
- Simple auto-increment devis number (DEVIS-001, DEVIS-002...)
- Preview devis screen

### Day 3: WhatsApp Share + PDF Generation
- Generate PDF from devis preview (react-native-html-to-pdf or equivalent)
- Share via WhatsApp (Expo sharing or react-native-share)
- Single static mentions légales block (boilerplate text, hardcoded)
- Client list view

### Day 4: Real Device Smoke Test
- Install on physical device (not simulator)
- Send a real devis to Louis's own WhatsApp
- Verify PDF renders correctly on phone
- Fix any layout/UX issues that appear on real device

### Day 5 (Buffer): Beta Preparation
- Bug fixes from smoke test
- Prepare for beta: install on beta user's device
- Write basic onboarding note for beta user ("here's how you create a devis")

---

**Sprint 0 is now a 4-day sprint with a genuinely testable artifact.**

Days 5+ become Sprint 1 padding: TVA tier refinement, sequential numbering with locking, mentions légales per client type, client-type selector, offline architecture.

---

## What Sprint 1 Adds (From Sprint 0 Deferred Items)

These are not scope additions — they are pre-planned Sprint 1 refinements that belong in the original scope but were incorrectly placed on the Sprint 0 critical path:

1. **TVA multi-taux** — Per-line TVA selector (5.5%, 10%, 20%), TVA breakdown section, rounding accuracy
2. **Sequential numbering enforcement** — Server-side locking, gap detection, annual reset logic
3. **Mentions légales per client type** — Client type field (particulier/professionnel/étranger), dynamic mentions légales renderer
4. **Offline architecture** — expo-sqlite + draft-mode (per D140)
5. **Documents table generalization** — devis and factures on same documents table (schema refinement, not new feature)

---

## Verdict Proposal

**Reject D157's conclusion. Accept D157's diagnosis.**

D157 correctly identified that the Sprint 0 plan cannot produce a testable artifact in 6.5 days. But D157's proposed resolution (shrink OR extend) accepts the wrong framing. The problem is not the 6.5-day timeline. The problem is that the Sprint 0 plan still contains Sprint 1 complexity on its critical path.

**Proposed resolution:**
1. Sprint 0 scope is reduced to Happy Path First — client + devis + WhatsApp share + PDF (4 days)
2. Sprint 0 scope explicitly excludes: TVA multi-taux, sequential numbering locking, mentions légales per client type, offline architecture
3. Sprint 0 timeline: 4 days (target), 5 days (floor with buffer)
4. Sprint 1 begins immediately after with the deferred complexity items above
5. The Sprint 0 artifact is testable: "Can I send a professional devis to myself via WhatsApp?"

**Challenge to Louis:** If the beta user can complete the happy path with hardcoded 10% TVA, auto-increment numbering, and a single mentions légales block — and the real calculator and numbering enforcement are added in Sprint 1 — what is actually lost? The answer is: nothing testable. The beta user's experience of the happy path is fully functional. Sprint 1 makes it legally compliant. Those are different problems.

---

## Status

**D157-REVISITED — Ready for Louis Decision**

The Technical Architect position has evolved: the diagnosis from D157 stands (schema-first Sprint 0 cannot fit in 6.5 days), but the resolution differs. Do not extend Sprint 0. Reduce its scope. The complexity belongs in Sprint 1, not Sprint 0's critical path.

Louis: the decision is not "6.5 days OR 10 days." The decision is "Happy Path First (4 days) OR schema-first (6.5+ days, possibly still not testable)." The former produces a testable artifact. The latter may not.
