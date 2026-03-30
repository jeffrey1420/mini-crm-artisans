# Mini-CRM → Devis & Factures — Resolved Decisions & TODO

> **Pivot applied 2026-03-30** — Based on external review. Full pivot from "CRM for artisans" to "devis/factures/relances tool."

## ✅ Resolved Decisions

| ID | Topic | Decision | Source | Date |
|----|-------|----------|--------|------|
| D1 | Positioning | Kill "CRM" — sell "devis, factures, relances" | External review | 2026-03-30 |
| D2 | MVP scope | 4 features only: client file, quote, invoice, reminder | External review | 2026-03-30 |
| D3 | Primary persona | Marc — solo smartphone-native artisan | External review | 2026-03-30 |
| D4 | Stack | Single managed Postgres, NOT per-customer VPS | External review | 2026-03-30 |
| D5 | Pricing | €29/€49/€79 tiered (kept from previous) | Previous debate | 2026-03-30 |
| D6 | Trial | 30 days (kept from previous) | Previous debate | 2026-03-30 |
| D7 | Architecture | Nuxt 3 + OVH managed Postgres | Updated | 2026-03-30 |
| D8 | E-invoicing | v2 feature (Chorus Pro compatible) | External review | 2026-03-30 |
| D9 | Not MVP | No Kanban, no multi-user, no offline, no API keys | External review | 2026-03-30 |
| D10 | Buyer trigger | "Admin pain" not "CRM need" | External review | 2026-03-30 |
| D11 | PWA vs Native | PWA first (launch), native within 6 months | Debate 11 revision | 2026-03-30 |
| D12 | Landing page | Simplicity-first — "Vos devis et factures, sans vous prendre la tête" | Debate 19 (Product Strategist) | 2026-03-30 |
| D13 | Home view | Job-first — Active Job Card as home anchor, not Dashboard or Timeline | Debate 20 (Technical Architect) | 2026-03-30 |
| D14 | E-invoicing timing | v2 — NOT Day 1 (Debate 21 Growth Strategist) | Debate 21 |
| D15 | Relances differentiator | Secondary feature only — below fold, "Fonctionnalités" section. Frame as "Suivi de paiement" not "Relances automatiques." Not in hero. | Debate 25 (Product Strategist) |
| D16 | Trial length | 14 days (updated from 30). No credit card at signup. Email drip: day 7, 3, 1. | Debate 26 (Growth Strategist) |
| D17 | Mobile strategy | React Native from Day 1 via Expo (updated from PWA-first). Single codebase, APNS/FCM push, App Store from launch. | Debate 27 (Technical Architect) | 2026-03-30 |

## 🔄 Reopened This Pulse (Need Resolution)

| ID | Topic | Issue | Source |
|----|-------|-------|--------|
| D15 | Relances differentiator | DE-EMPHASIZED — secondary feature below fold | RESOLVED — Debate 25 |
| D16 | Trial length | 14 days, no credit card at signup | RESOLVED — Debate 26 |
| D17 | Mobile strategy | React Native from Day 1 via Expo | RESOLVED — Debate 27 |
| U1 | Real discovery | REOPENED — replace 10-person discovery with 3-day guerrilla usability test + explicit readiness criteria (Debate 28) |
| D2 | MVP scope | REOPENED — Phase 0.5 (devis-only) proposed to validate core flow before full 4-feature build (Debate 29) |
| D5 | Pricing | REOPENED — €29/€49/€79 conflicts with simplicity positioning; €19/€29 two-tier proposed (Debate 30) |

## 🔄 Still Unresolved

| ID | Topic | blockers |
|----|-------|----------|
| U1 | Real discovery | Need to watch 10 artisans do admin tasks before building |
| U7 | Domain | Buy domain — not alize, something memorable for devis/factures tool |

## 📋 Current TODO

### Before Building (Do First)
- [ ] Replace "watch 10 artisans" with 3-day guerrilla usability test (5 artisans at wholesaler, one task: create a devis on prototype) — U1 reopened (Debate 28)
- [ ] Define explicit "ready to build" criteria to replace U1 as gating condition
- [ ] Pick one: Tolteck competitor or Tolteck complement?
- [ ] Buy domain (U7) — something memorable for devis/factures tool
- [ ] Build the Active Job Card data model (`jobs.status`, `jobs.scheduled_date`, `jobs.updated_at`)
- [x] RESOLVE D15: Relances = secondary feature below fold. "Fonctionnalités" section only. NOT in hero.
- [x] RESOLVE D16: Trial = 14 days. No credit card at signup. Email drip day 7, 3, 1.
- [x] RESOLVE D17: React Native from Day 1 via Expo. PWA-first retired.
- [ ] DECIDE D2: 4-feature MVP vs Phase 0.5 (devis-only MVP) — Technical Architect argues Phase 0.5 is faster to validate (Debate 29)
- [ ] DECIDE D5: €29/€49/€79 tiered vs €19/€29 two-tier — Product Strategist argues current structure conflicts with simplicity positioning (Debate 30)

### MVP Build (After Discovery)
- [ ] Client file feature
- [ ] Quote/devis feature (create, send via WhatsApp)
- [ ] Invoice/facture feature (French-legal, sequential numbering)
- [ ] Reminder/relance feature

### Home View Build (D13 — Job-first)
- [ ] Active Job Card as home screen anchor (most recent in_progress job)
- [ ] Upcoming Jobs Strip (next 3 jobs by scheduled date)
- [ ] Quick stats bar (de-emphasized counts for relances/factures impayées — tap to see full list, not alarm on home)
- [ ] "Relances dues" and "Devis en attente" move to secondary "À suivre" tab (not home screen)
- [ ] Client Timeline remains accessible from client profile (not home)

### Landing Page Build (D12 + D15 — Simplicity-first, Relances de-emphasized)
- [ ] Headline: "Vos devis et factures, sans vous prendre la tête."
- [ ] Subheadline: "Pas de formation. Pas de tableau comparatif. Vous envoyez votre premier devis en 5 minutes, depuis votre téléphone."
- [ ] Remove "Vos clients vous payent en 48h" from primary headline (keep as social proof below fold)
- [ ] Keep WhatsApp mention in subhead or features section (not as primary hook)
- [ ] Add peer social proof (French tradespeople testimonials) — secondary, not primary
- [ ] NO ROI claims on landing page — simplicity + outcome framing only
- [ ] Relances = Feature #4 or #5 in "Fonctionnalités" section. NOT in hero. Frame as "Suivi de paiement" or "Rappels" (soft language). Artisan controls it — not "we text your client."

### E-Invoicing v2 (D14 — Not Day 1)
- [ ] Remove "Day 1 e-invoicing" from any planning assumptions
- [ ] When v2 time: evaluate Factea first (API quality + Peppol + solo artisan pricing)
- [ ] E-invoicing inbox + "E-invoice ready" badge = v2 feature, not launch feature

### Mobile Build (D17 — React Native from Day 1)
- [ ] Use Expo for React Native setup (`npx create-expo-app`)
- [ ] Push notifications via Expo Notifications (APNS on iOS, FCM on Android) — not web push
- [ ] App Store + Play Store presence from Day 1 launch
- [ ] Target both iOS and Android simultaneously from start — do not "do one platform then the other"
- [ ] Keep MVP scope tight: client list, job/reminder management, basic invoicing — no feature creep
- [ ] PWA is NOT the mobile strategy — web-only is retired for this product

### Trial Flow (D16 — 14 days, no credit card)
- [ ] Trial length = 14 days (not 30)
- [ ] No credit card at signup — friction kills conversion at awareness stage
- [ ] Email drip sequence: Day 7 ("How's it going?"), Day 3 ("Last 3 days left"), Day 1 ("Trial ends tomorrow — ready to start?")
- [ ] Credit card capture introduced at Day 7-10 for engaged users (in-app prompt, not email block)
- [ ] Aha moments by day: Day 1 (clients organized), Day 5 (quote sent from phone), Day 10 (follow-up reminder received)

## 🚫 What We Deleted

The following were overengineered or wrong:
- Per-customer VPS architecture (too expensive, too complex)
- Kanban as primary view (imposes PM thinking on people who don't manage projects)
- Full multi-tenant architecture (not needed at launch)
- OAuth/MFA for launch
- Inventory management
- Fancy analytics
- Dashboard-first home view (wrong mental model for artisan)
- Timeline-first home view (passive archive, not a launch point)
- Day 1 e-invoicing (provider lock-in before product-market fit)
- ROI-first landing page (invites comparison shopping)

---

## New from Pulse 2026-03-30T10:58

### Resolved (D12, D13, D14):
- **D12 (Landing):** Product Strategist won — simplicity-first beats ROI-first for acquisition. Headline: "Vos devis et factures, sans vous prendre la tête." U3 + U6 resolved.
- **D13 (Home view):** Technical Architect won — neither Dashboard nor Timeline serves Marc's actual mental model. Home = Active Job Card. U4 resolved.
- **D14 (E-invoicing):** Growth Strategist won — regulatory deadline is for senders, not buyers. Provider lock-in before PMF is wrong. U5 resolved. U2 (provider choice) deferred to v2.

### Challenged assumptions this pulse:
1. Landing page ROI framing (Position A) — challenged by Product Strategist
2. Dashboard-first home view — challenged by Technical Architect (both sides wrong)
3. Day 1 e-invoicing urgency — challenged by Growth Strategist (regulatory ≠ buy-side urgency)

---

## New from Pulse 2026-03-30T11:11

### Reopened (D15, D16, D17):
- **D15 (Relances):** Product Strategist won the argument — relances-as-differentiator is fragile. French artisan culture prefers direct calls over automated WhatsApp. Attracts wrong users (cash-flow problems, poor client relationships). Reopen: de-emphasize relances on landing, frame as "schedule reminder for yourself" not "we text your client."
- **D16 (Trial length):** Growth Strategist won — 30 days creates procrastination, not urgency. Shorter trials convert better (self-select for acute-need buyers). Reopen: 14 days, no credit card at signup, aggressive email drip in final week.
- **D17 (Mobile strategy):** Technical Architect won — PWA-first fails on iOS (no web push, storage caps, install friction). React Native from Day 1 = single codebase, reliable notifications, App Store credibility.

### Challenged assumptions this pulse:
1. Relances as primary differentiator (Product Strategist challenged D1/D12 framing)
2. 30-day trial (Growth Strategist challenged D6)
3. PWA-first mobile strategy (Technical Architect challenged D11)

---

*Last updated: 2026-03-30T11:11*

---

## New from Pulse 2026-03-30T11:38

### Reopened (U1, D2, D5):
- **U1 (Discovery):** Growth Strategist challenged — "watch 10 artisans" is a stalling tactic. Personas are sufficient. Competitive analysis already validated pain. Proposes 3-day guerrilla usability test (5 artisans at wholesaler, single devis task) + explicit "ready to build" criteria instead.
- **D2 (MVP scope):** Technical Architect challenged — 4-feature MVP underestimates French invoice complexity (sequential numbering, multi-taux TVA 5.5/10/20%, mentions légales per client type). Proposes Phase 0.5: devis-only MVP (1 week build, 1 week test) to validate core flow before full 4-feature build.
- **D5 (Pricing):** Product Strategist challenged — €29/€49/€79 conflicts with "simple as WhatsApp" positioning. €29 floor is 50%+ above Tolteck (€19) and Obat (€17). Proposes €19/€29 two-tier structure with explicit value anchor: "2h/week saved × €50-80/h = €100-160/week value. Monthly cost: €29."

### Challenged assumptions this pulse:
1. U1 discovery as prerequisite before building (Growth Strategist — personas sufficient, discovery = indefinite deferral)
2. 4-feature MVP achievable in short sprint (Technical Architect — French legal invoicing adds hidden complexity)
3. €29 floor as defensible for simplicity positioning (Product Strategist — above market, conflicts with positioning)

---

*Last updated: 2026-03-30T11:38*
