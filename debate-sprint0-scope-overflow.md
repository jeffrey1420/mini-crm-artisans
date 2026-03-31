# Debate: Sprint 0 Scope — The Sprint Has Become a Product Design Sprint in Disguise

**Challenger:** Product Strategist (subagent)
**Target:** The assumption embedded in D95/D84/D90 — that Sprint 0 can deliver a 5-day sprint with the current scope
**Position:** Sprint 0 has absorbed more scope than any single sprint should carry. Louis needs to pick 3 maximum deliverables and defer the rest to v1.x.

---

## Assumption Challenged

**"Sprint 0 can realistically deliver a 5-day sprint with the current scope (offline-capable + mentions légales + PDF generation + WhatsApp Business API + Path B conversion triggers + dual-path conversion architecture)."**

This assumption appears across multiple decisions: D84 (5.5-6.5 days), D95 (5 days target, 6.5 days floor), and the implicit scope assumption in D40/D83/D96/D110/D140/D141/D142 that all of these can be packed into Sprint 0.

The debate log shows Sprint 0 has absorbed scope in six distinct categories:

1. **D40 + D141 + D110:** Path B WhatsApp digest + soft limits + dual-path conversion architecture
2. **D83 + D89:** Situation financière notification infrastructure + nightly aggregation job
3. **D140:** Expo-sqlite offline (view-only OR full offline with conflict UI)
4. **D114 + D121:** PDF via Edge Function + document storage migration spec
5. **D71 + D74 + D142:** Mentions légales template engine (4 client types, Handlebars/Nunjucks)
6. **D96:** Dual-path conversion trigger architecture

That's six major feature areas on top of the core devis flow. No single sprint — let alone a 5-day solo dev sprint — delivers this.

---

## My Argument

### Point 1: Path B conversion mechanics are v1.x scope, not Sprint 0 scope

The debate log has Path B mechanics scattered across D40, D110, D141, and D96. But here's the problem: **you cannot validate a 45-day/7-job/5-client conversion trigger without real users generating real usage patterns.**

D110 defines Path B's soft limit (7 jobs / 5 clients / 45 days) and D141 defines the bi-weekly WhatsApp digest content. But these are guesses. Louis doesn't have 10 Path B artisans using the product. He has zero users. The right time to design Path B conversion mechanics is after he has 5-10 real users — then he can see which triggers actually correlate with willingness to pay.

Sprint 0 Path B mechanics are premature optimization. Cut them. Build Path A (limit-hit on formal devis) only. Let Path B be informed by real usage data in Week 3-4.

### Point 2: WhatsApp Business API in Sprint 0 is a Meta verification problem, not an engineering problem

D40 committed to WhatsApp Business API as "first-class notification channel" in Sprint 0. D40-Pulse-0129 correctly challenged this: **Meta Business Verification alone takes 2-14 days.** Louis doesn't have a Meta Business Manager account verified. He doesn't have a business phone number verified. He doesn't have an app review completed. These are Meta's processes, not Louis's.

Even if Louis starts verification TODAY, Sprint 0 ends before verification completes. The WhatsApp Business API deliverable in Sprint 0 is vapor. It cannot ship.

More critically: **there is nothing to send on WhatsApp in Sprint 0.** The "premium content" (situation financière, accepted devis events) doesn't exist yet. Sprint 0 produces a devis-creation flow. The first notification a user receives is "your devis was accepted" — which requires a user to have created and sent a devis. That's Week 2 minimum.

Defer WhatsApp to v1.1. Sprint 0 notification = Expo Push only. Budget Expo Push at 1-2 days (D47 already established this). WhatsApp is v1.1 after Louis has verified Meta Business and has actual premium content to send.

### Point 3: Dual-path conversion architecture is premature architecture

D96 established the dual-path model. D110 refined Path B triggers. But the debate log hasn't grappled with what "dual-path architecture" actually means for the codebase:

- Two distinct onboarding flows?
- Two different home screen states?
- Two different notification triggers?
- Two different upgrade prompts?
- Two different retention mechanics?

Each of these is a design decision that needs real user input to answer correctly. Sprint 0 should not be building dual-path architecture. It should be building a single-path devis flow that works for one type of user (Path A — formal devis artisan).

The dual-path framing belongs in v1.2, informed by actual user data: do we have Path A users who hit the limit? Do we have Path B users who log jobs but never create formal devis? Let the product answer these questions before engineering two parallel systems.

### Point 4: The mentions légales gate hasn't been met — Sprint 0 isn't even guaranteed 5 days

D142 explicitly states: **"gate NOT met as of 2026-03-31."** Louis has not committed the 4 mentions légales templates to `legal/mentions-legales.ts` with real business data. The TODO.md still shows these as unresolved.

D95's 5-day estimate is explicitly CONDITIONAL on this gate being met. Without the gate: 7-8 days. The debate log is planning a 5-day sprint with pre-conditions that haven't been satisfied.

Even if the gate were met: the mentions légales template engine (D74: Handlebars/Nunjucks, 4 client-type templates) is scope that should be cut. Sprint 0 needs **plain text mentions légales** — static strings, no template engine. The template engine is nice-to-have for Sprint 1 when there are 8 combinations (devis + facture) × 4 client types. Sprint 0 needs 1 static block of legal text that covers the single devis use case.

---

## Proposed Resolution

**Louis must pick exactly 3 deliverables for Sprint 0:**

### Deliverable 1 — Core devis flow (3 days)
- Supabase schema: clients, devis, TVA per-line, sequential numbering
- Client creation + devis creation (Path A only — single flow, no branching)
- TVA arrondi commercial calculator
- expo-print PDF generation (prototype, not legal storage)
- WhatsApp share of PDF via native share sheet (no WhatsApp API)
- Mentions légales as plain text string (no template engine)
- Single client type (particulier) for Sprint 0

### Deliverable 2 — Auth + basic offline (1 day)
- Supabase auth (email/password)
- AsyncStorage caching of last-known clients/devis (read-only offline, no offline editing)
- Retry queues for failed network requests
- NO WatermelonDB, NO expo-sqlite, NO background sync in Sprint 0
- Label this honestly: "offline-capable for viewing, not for editing"

### Deliverable 3 — Notification foundation (0.5 days)
- Expo Push setup (D47: 1-2 weeks is the full budget; Sprint 0 gets 0.5 days for the infra skeleton)
- Nightly aggregation job skeleton (D83) — timing and content defined, not fully implemented
- Push at 8pm Paris — code stub only, activate in v1.1
- NO WhatsApp Business API in Sprint 0

**What gets cut from Sprint 0:**

| Cut Item | Why | Moved To |
|----------|-----|----------|
| WhatsApp Business API | Meta verification takes 2-14 days; no Sprint 0 value possible | v1.1 |
| Path B conversion triggers/mechanics | Cannot validate trigger design without real users | v1.2 |
| Dual-path conversion architecture | Premature complexity; single path ships first | v1.2 |
| Mentions légales template engine | Static strings sufficient for Sprint 0 | Sprint 1 |
| Expo-sqlite + background sync | View-only offline covers 90% of failure modes | v1.2 |
| Path B digest spec (D141) | WhatsApp-dependent; no channel in Sprint 0 | v1.1 |
| Situation financière push content | No accepted devis events exist in Sprint 0 | v1.1 |
| Dual framing protocol for onboarding | Single path first; dual framing informed by real users | v1.2 |

**Revised Sprint 0 timeline: 4.5 days** (not 5.5-6.5, not 5)

This accounts for:
- 3 days: core devis flow
- 1 day: auth + basic offline
- 0.5 days: notification skeleton
- 0.5 days: buffer for real device testing + edge cases

---

## What This Means for the TODO

### Remove from Sprint 0 scope immediately:
- ~~D40 — WhatsApp Business API as first-class notification channel~~
- ~~D141 — Path B digest spec (WhatsApp Business API)~~
- ~~D110 — Path B soft limit definition~~
- ~~D83 — Push notification infra + nightly aggregation job~~ (replace with skeleton only)
- ~~D140 — Expo-sqlite OR view-only offline~~ (view-only confirmed, full offline deferred)
- ~~D74 — Mentions légales template engine (Handlebars/Nunjucks)~~ (replace with plain text)
- ~~D96 — Dual-path conversion trigger architecture~~ (Path A only for Sprint 0)
- ~~D139 — Expert-comptable outreach prep~~ (moved to Week 3 per D139 REFINED)

### Update Sprint 0 scope doc:
- Sprint 0 = 3 deliverables, 4.5 days
- Mentions légales = static string, not template engine
- Offline = view-only with retry queues, not offline editing
- Notifications = Expo Push skeleton only, WhatsApp in v1.1
- Conversion = Path A (limit-hit on formal devis) only, single flow

### Add to v1.x scope (NOT Sprint 0):
- WhatsApp Business API (v1.1) — after Meta verification
- Path B conversion mechanics (v1.2) — informed by real usage data
- Dual-path architecture (v1.2)
- Mentions légales template engine (Sprint 1)
- Expo-sqlite + background sync (v1.2)
- Full push notification implementation (v1.1)

### Sprint 0 gate verification (D142):
Louis must commit to git BEFORE Sprint 0 begins:
1. `legal/mentions-legales.ts` with his actual business data as static strings (NOT TODO comments)
2. Supabase project dashboard visible

If gate not met by Sprint 0 start: add 1 day, making Sprint 0 = 5.5 days.

---

*Product Strategist (subagent) — PS-D147-Sprint0Scope*
*2026-03-31*
