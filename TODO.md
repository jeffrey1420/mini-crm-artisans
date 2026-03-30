# Mini-CRM → Devis & Factures — Resolved Decisions & TODO

> **Pivot applied 2026-03-30** — Based on external review. Full pivot from "CRM for artisans" to "devis/factures/relances tool."

## ✅ Resolved Decisions

| ID | Topic | Decision | Source | Date |
|----|-------|----------|--------|------|
| D1 | Positioning | Kill "CRM" — sell "devis, factures, relances" | External review | 2026-03-30 |
| D2 | MVP scope | 4 features only: client file, quote, invoice, reminder | External review | 2026-03-30 |
| D3 | Primary persona | Marc — solo smartphone-native artisan | External review | 2026-03-30 |
| D4 | Stack | Single managed Postgres, NOT per-customer VPS | External review | 2026-03-30 |
| D5 | Pricing | Free + €29 two-tier. No €19 SKU. Drop €49/€79. Value anchor: "2h/week = 1h labor = €29/month." | Debate 33 (Product Strategist) | 2026-03-30 |
| D6 | Trial | No time-limited trial. Free tier IS the trial (10 clients, 5 active devis). Conversion happens at Free limit. Engagement: restated by D43 — channel secondary, Free tier design determines activation. 80% limit heads-up notification. No countdown emails. | Debates 38/43 (Product Strategist) | 2026-03-30 |
| D7 | Architecture | Nuxt 3 + OVH managed Postgres — REFINED: API-first preferred but deferred to post-MVP unless blocking Sprint 0 | Growth+Architect | 2026-03-30 |
| D8 | E-invoicing | v2 feature (Chorus Pro compatible) | External review | 2026-03-30 |
| D9 | Not MVP | No Kanban, no multi-user, no offline, no API keys | External review | 2026-03-30 |
| D10 | Buyer trigger | "Admin pain" not "CRM need" | External review | 2026-03-30 |
| D11 | Mobile | React Native from Day 1 via Expo. Push notifications: Expo Push at launch (budget 1-2 weeks). | Debates 27/44/47 (Technical Architect) | 2026-03-30 |
| D12 | Landing page | Simplicity-first — H1: "Vos devis et factures, sans vous prendre la tête." H2: "Créez et envoyez votre premier devis en 5 minutes. Depuis votre téléphone." Proof lives in Free tier. | Debates 19/53 (Product Strategist) | 2026-03-30 |
| D13 | Home view | Job-first — Active Job Card as home anchor, not Dashboard or Timeline | Debate 20 (Technical Architect) | 2026-03-30 |
| D14 | E-invoicing timing | v2 — NOT Day 1 (Debate 21 Growth Strategist) | Debate 21 |
| D15 | Relances differentiator | Secondary feature only — below fold, "Fonctionnalités" section. Frame as "Suivi de paiement" not "Relances automatiques." Not in hero. | Debate 25 (Product Strategist) |
| D16 | Trial length | 14 days (updated from 30). No credit card at signup. Email drip: day 7, 3, 1. | Debate 26 (Growth Strategist) |
| D17 | Mobile strategy | React Native from Day 1 via Expo. Push notifications: preferred Expo Push at launch (if EAS Build exists), alternative cut relances from v1. Never email-only. | Debates 27/44 (Technical Architect) | 2026-03-30 |
| D40 | Engagement channel | RESTATED — channel secondary to Free tier design. Three paths: (A) lower limits, (B) Day 1 redesign, (C) accept long-tail activation. | Debate 43 (Product Strategist) | 2026-03-30 |
| D41 | Notification infra | REVERSED — email-only relances wrong. Obat markets push. Preferred: Expo Push at launch. Alternative: cut relances from v1. | Debate 44 (Technical Architect) | 2026-03-30 |
| D42 | WhatsApp referral | CLOSED — kill CTA in devis, kill in-product peer referral as primary acquisition. Redirect to wholesaler presence + prescriber networks + SEO. | Debate 45 (Growth Strategist) | 2026-03-30 |
| D46 | Free tier limits | Do NOT lower limits from 10/5. Keep generous limits. Trust-building before limit enforcement. Limit should hit AFTER aha moment, not before. | Debate 46 (Product Strategist) | 2026-03-30 |
| D47 | Expo Push estimate | 1-2 weeks, not "few hours." Budget properly or defer to v1.1. | Debate 47 (Technical Architect) | 2026-03-30 |
| D48 | Wholesaler GTM | Not primary GTM. Digital + specialist retailers first. Wholesaler secondary brand-awareness play only. Audit solo artisan purchasing channels first. | Debate 48 (Growth Strategist) | 2026-03-30 |
| D53 | Landing page framing | Simplicity-first RETAINED. H1: "Sans vous prendre la tête." H2: 5-minute specific/demonstrable claim. Proof lives in Free tier. No "professional-grade" in hero. | Debate 53 (Product Strategist) | 2026-03-30 |
| D54 | Sprint 0 approach | Compressed compliance sprint (3-4d): TVA per-line schema, gapless sequential numbering engine, mentions légales renderer, client-type schema. Sprint 1 = client+devis flow. | Debate 54 (Technical Architect) | 2026-03-30 |
| D55 | Buyer-user split | Dual-persona GTM. Marc = economic buyer (primary). Admin handler = operational user (secondary). Expert-comptable = Phase 2. | Debate 55 (Growth Strategist) | 2026-03-30 |
| D56 | WoM attribution | WoM = Month 3+ lagging indicator. Digital acquisition PRIMARY at launch. "Comment connaissez-vous?" at signup. Referral codes in v1. Month 3 target: 20% peer referral. | Pulse 14:57 (Product+Growth) | 2026-03-30 |
| D57 | Architecture | API-first preferred (Fastify + static) but deferred to post-MVP unless Nuxt 3 actively blocks Sprint 0. | Pulse 14:57 (Architect+Growth) | 2026-03-30 |
| D59 | Pricing credibility | Kill €19 founding member offer. Replace with early access €29 locked for life. Guerrilla price validation with micro-artisan rate anchors. | Debate 62 (Technical Architect) | 2026-03-30 |

## 🔄 Reopened This Pulse (Resolved in 15:17 Pulse)

All items below were resolved in the 15:17 pulse — see D60, D61, D62 above.

## New from Pulse 2026-03-30T15:17 — Three Resolved

### Resolved (D60, D61, D62):
- **D60 (WoM attribution):** Product Strategist won — 40% figure RETIRED (unvalidated). WoM as lagging indicator: confirmed. D33/D52/D55 updated to "WoM hypothesized significant based on artisan network density, validated post-launch." Measurement protocol: "Comment connaissez-vous?" at signup + referral codes. Month 3 target: 20% peer referral.
- **D61 (Architecture):** Technical Architect won — API-first (Node/Fastify + static landing page + JWT auth) is cleaner for mobile-first product. OVH managed Postgres retained. Nuxt 3 deferred to post-MVP unless actively blocking Sprint 0.
- **D62 (Pricing):** Technical Architect won — kill €19 founding member offer (permanently anchors product at discount). Replace with "early access, first 50 users lock €29/month for life." Guerrilla price validation: use micro-artisan rates (€25-40/h), not consultant rates (€50-80/h). Show demo, let artisans anchor their own price.

### Challenged assumptions this pulse:
1. "Sans vous prendre la tête" talks down to 45-55yo professionals (Product Strategist challenged: it signals product empathy, not condescension — "we know your time is valuable")
2. Compliance-first requires 5-7 days of pure schema (Technical Architect challenged: 3-4 days — TVA is formulaic, numbering is a counter, mentions légales is a template)
3. Admin handler doesn't feel real pain (Growth Strategist challenged: she feels her own operational pain — forgotten follow-ups, 3h/week tracking — not Marc's pain by proxy)

### New action items from this pulse:
- [ ] **D53 UPDATED:** Landing page H2 updated — "Créez et envoyez votre premier devis en 5 minutes. Depuis votre téléphone." (5-minute specific claim replaces "Pas de formation. Pas de tableau comparatif.")
- [ ] **D53 NEW:** Document quality showcase on landing page — actual devis document screenshots (not stock photos) as proof of professional-grade quality. Below fold only.
- [ ] **D54 NEW:** Sprint 0 deliverables — TVA per-line schema (Day 1), sequential numbering engine (Day 2), mentions légales renderer (Day 3), client-type schema (Day 3)
- [ ] **D54 UPDATED:** Sprint 0 timeline = 3-4 days (not 5-7). Mentions légales = template file (not a schema table). TVA = formula (not a lookup table). Compliance work is more bounded than previously estimated.
- [ ] **D55 NEW:** Dual-persona messaging tracks — Marc: emotional/forgetfulness pain ("Sans vous prendre la tête"); Admin handler: operational efficiency ("Gagnez 2h/semaine sur l'administration")
- [ ] **D55 NEW:** GetApp/Capterra profiles claimed and optimized before launch — admin handlers search here first
- [ ] **D55 UPDATED:** Expert-comptable referrals moved to Phase 2 — relationship-dependent, 6-18 month build time. Not early-stage priority.
- [ ] **D55 NEW:** U12 (Expert-comptable GTM playbook) — document what to say, what materials to leave, how to position for admin handler audience. Ready to execute in Phase 2.


## New from Pulse 2026-03-30T13:28

### Resolved (D49, D50, D51):
- **D49 (GTM Priority):** Growth Strategist won — D48 priority order stands. Digital channels (WhatsApp/Facebook/SEO) → Specialist retailers → Prescriber networks → Wholesaler. Prescribers cannot lead GTM because they recommend artisans to clients, not tools to artisans. U11 audit still worth doing.
- **D50 (Push at Launch):** Technical Architect won — email-only relances at v1 launch is acceptable. Expo Push in v1.1. Engineering bandwidth goes to devis flow, not relances. GetApp/Capterra fear overstates comparison-site impact for artisan discovery.
- **D51 (Free tier conversion):** Product Strategist won — habit formation is seductive but unmeasurable as primary conversion mechanism. Habits form around pain, not convenience. Design for forcing functions + limit-hit as primary. Habit tracking becomes secondary retention KPI (daily engagement rate).

### Challenged assumptions this pulse:
1. Prescriber networks create software adoption pull-through for artisans (Growth Strategist challenged: wrong direction of influence)
2. GetApp/Capterra disqualification is meaningful launch risk (Technical Architect challenged: artisan discovery = peer referral, not comparison browsing)
3. Habit formation → dependency → subscription is the correct conversion model (Product Strategist challenged: habits form around pain, not convenience; external forcing functions are the real trigger)

### New action items from this pulse:
- [ ] **D50 NEW:** Public roadmap statement: "Push notifications in Q3" — neutralizes GetApp/Capterra concern without shipping before ready
- [ ] **D50 NEW:** Engineering priority for v1 = devis flow. Relances = v1.1 feature. Do not deprioritize devis for notifications.
- [ ] **D51 NEW:** Track daily evening open rate as secondary retention KPI (not primary conversion metric)
- [ ] **D51 NEW:** Design upgrade prompts for forcing function moments: competitor outage, client demands professional invoice, peer referral in WhatsApp group
- [ ] **D51 NEW:** Keep Free tier generous (10/5) — do not reduce to create artificial pressure
- [ ] **U11 UPDATED:** Execute prescriber audit (architects, property managers) — if >30% of new jobs come via prescriber, revisit GTM priority order

---

*Last updated: 2026-03-30T14:57*

## New from Pulse 2026-03-30T14:57

### Resolved (D56, D57, D59):
- **D56 (WoM attribution):** REFINED — 40% WoM attribution retired as GTM input. WoM = Month 3+ lagging indicator, not launch channel. Digital acquisition PRIMARY at launch. "Comment avez-vous connu?" at signup (required, predefined options). Referral codes in v1. Month 3 target: 20% peer referral.
- **D57 (Architecture):** REFINED — API-first (Fastify + static landing) is architecturally cleaner for mobile-first + static product. But: shipping velocity matters more than purity for first 10 users. Defer migration unless Nuxt 3 actively blocks Sprint 0. Post-MVP migration if ROI positive.
- **D59 (Pricing credibility):** NEW — €29 price point is unvalidated with real artisans. "One hour of labor" anchor is founder math. Guerrilla price validation (5 artisans) + founding member €19/mo offer + 3% Day-30 conversion target + SEPA direct debit proposed.

### New Action Items from this pulse:
- [x] **D56 RESOLVED:** WoM = Month 3+ lagging indicator. Digital acquisition PRIMARY at launch. "Comment connaissez-vous?" at signup. Referral codes in v1.
- [ ] **D57 UPDATED:** API-first preferred but deferred — don't let architecture debate delay Sprint 0. Migrate post-MVP if Nuxt 3 not blocking.
- [x] **D59 RESOLVED:** Kill €19 founding member offer. Replace with "early access, first 50 users lock €29/month for life."
- [ ] **D59 UPDATED:** Guerrilla price validation — show demo, ask artisans their time spent on devis/week, let THEM anchor the price. Use micro-artisan rates (€25-40/h) not consultant rates (€50-80/h).
- [x] **D59 RESOLVED:** 3% Day-30 conversion target stands as KPI. If Month 2 with <1% conversion, price is likely the barrier.
- [ ] **D59 UPDATED:** SEPA direct debit still worth adding — French artisans skeptical of credit card subscriptions. Evaluate Stripe SEPA integration.
## New from Pulse 2026-03-30T14:41

### Resolved (D58):
- **D58 (Relances in MVP):** Growth Strategist won — email relances = v1 (1-2 days of work, Sprint 2). Expo Push relances = v1.1 (1-2 weeks per D47). The confusion was treating "Expo Push cost" as "relances cost" — they're two different delivery channels with different timelines. D2 sprint order unchanged: Sprint 0 → Sprint 1 → Sprint 2 (factures + email relances) → v1.1 (Expo Push).

### Challenged Assumptions (D56, D57 — Still Open):
- **D56 (WoM %):** 40% word-of-mouth attribution has been treated as settled since D33 without empirical validation. No measurement mechanism exists. WoM is a lagging indicator of product-market fit, not a leading acquisition channel. Anchors D33/D52/D55 decisions without evidence.
- **D57 (Nuxt 3 Architecture):** D7 (Nuxt 3) was decided before React Native was chosen. The product is now mobile-first with a static landing page. Nuxt 3's SSR capabilities are architecturally mismatched. API-first (Node/Express) + static site proposed as alternative.

### New Action Items:
- [x] **D58 RESOLVED:** Email relances in v1 (Sprint 2, 1-2 days). Expo Push relances in v1.1. D2 sprint order stands.
- [ ] **D56 NEW:** Define WoM measurement mechanism before launch — UTM-tagged referral tracking, "comment avez-vous connu l'app?" onboarding question, or explicit referral invite codes. Without measurement, 40% target is unverifiable.
- [ ] **D57 NEW:** Resolve D7 — evaluate Node/Express or Fastify vs Nuxt 3 as backend framework. If Nuxt 3: document why SSR/API routes are needed given React Native is the primary product.

### Challenged This Pulse:
1. "Relances = Expo Push complexity" (Product Strategist D58 challenge) — challenged by Growth Strategist: conflates two separate features. Email relances (1-2 days) ≠ Expo Push (1-2 weeks). Split the feature.
2. "Nuxt 3 is the right backend" (D7) — challenged by Technical Architect: SSR capabilities unused for mobile-first + static landing page product. API-first fits the actual architecture better.


## 📋 Current TODO

### Before Building (Do First)
- [ ] U1 readiness check: (1) Figma/clickable devis-creation prototype, (2) guerrilla test scheduled (5 artisans at Point P/Gedimat), (3) pain confirmed by competitive analysis, (4) feature set frozen
- [ ] **D64 RESOLVED:** Sprint 0 starts with Fastify + Postgres API (NOT Nuxt 3). Day 1 = Postgres schema (TVA per-line, sequential numbering, mentions légales, client-type) + Fastify scaffold. Day 2 = TVA service + sequential numbering engine + mentions légales renderer. Day 3 = full CRUD REST API ready for React Native integration. Nuxt 3 retired from backend — static landing page only. (Debate 64)
- [ ] **D65 RESOLVED:** U15 three-phase guerrilla protocol — (1) 20-min observation of actual admin workflow, no demo, no pitch; (2) pain quantification (time spent/week, emotional weight 1-10, lost revenue from forgotten devis); (3) payment conversation ONLY if pain is confirmed. Remove "show demo, ask price" from U15. (Debate 65)
- [ ] **D63 RESOLVED:** Design the "situation financière" snapshot for Free tier home — automatically-produced weekly output showing: outstanding devis (with days-open), pending factures (aging buckets: 15/30/45/60+ days), revenue this month vs last month, dormant clients (30+ days inactive). This is the Free tier's primary value output. Push-ready content. Notification channel debates are secondary until this exists. (Debate 63)
- [ ] If prototype not ready in 1 week: proceed to build anyway, validate post-launch (Debate 31)
- [ ] Sprint 0: Fastify + Postgres only (NOT Nuxt 3). Compliance foundations first (3-4 days): TVA per-line schema, sequential numbering engine, mentions légales renderer, client-type schema. Sprint 1 = client+devis flow. Sprint 2 = facture+email relances. (Debates 54/64)
- [x] **D57 RESOLVED:** API-first (Node/Fastify + static landing + JWT) preferred. Nuxt 3 deferred unless blocking Sprint 0. OVH managed Postgres retained. (Debate 61)
- [x] **D58 RESOLVED:** Email relances in v1 (Sprint 2, 1-2 days). Expo Push relances in v1.1. (Debate 58)
- [x] **D56 RESOLVED:** 40% WoM figure RETIRED. Measurement protocol: "Comment connaissez-vous?" at signup + referral codes. Month 3 target: 20% peer referral. (Debate 60)
- [ ] Pick one: Tolteck competitor or Tolteck complement?
- [ ] Buy domain (U7) — DEFERRED. Use `devis.lschvn.foo` subdomain or Carrd landing page until MVP validated post-guerrilla test. Domain purchase happens after product direction confirmed. (Debate 34)
- [ ] Build the Active Job Card data model (`jobs.status`, `jobs.scheduled_date`, `jobs.updated_at`)
- [x] RESOLVE D15: Relances = secondary feature below fold. "Fonctionnalités" section only. NOT in hero.
- [x] RESOLVE D16: SUPERSEDED — 14-day trial concept retired. Free tier IS the trial (Debate 38/40).
- [x] RESOLVE D17: React Native from Day 1 via Expo. Email-only at launch. Push deferred to v2 unless 50+ paying users complain (Debate 41).
- [x] RESOLVE D2: Sequenced sprint structure (Sprint 0 = schema, Sprint 1 = client+devis, Sprint 2 = facture+relances). Phase 0.5 retired.
- [x] RESOLVE D5: Free + €29 two-tier. Drop €49/€79. Value anchor: "2h/week = 1h labor = €29/month." No €19 SKU at launch.
- [ ] A/B test pricing page value anchor: "€1/jour" vs "une heure de main d'oeuvre" framing with beta users before launch (Debate 33)
- [ ] Engagement channel for Free tier onboarding: push notifications + optional WhatsApp opt-in (NOT email). Replace Growth Strategist's 3-email Days 1-7 sequence. (Debates 38/40)
- [ ] Optional WhatsApp opt-in during Free tier onboarding — artisans who prefer it over push. This is their native channel. (Debate 40)
- [ ] 80% limit heads-up notification when Free tier user approaches client or devis limit (not countdown, just awareness). (Debate 40)

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
- [ ] **D47 UPDATED:** Push notifications via Expo Notifications — budget 1-2 weeks (not "few hours"). If deadline can't accommodate: defer relances to v1.1, email-only as temporary bridge.
- [ ] App Store + Play Store presence from Day 1 launch
- [ ] Target both iOS and Android simultaneously from start — do not "do one platform then the other"
- [ ] Keep MVP scope tight: client list, job/reminder management, basic invoicing — no feature creep
- [ ] PWA is NOT the mobile strategy — web-only is retired for this product

### Trial Flow (D6 — No Time-Limited Trial. Free Tier IS the Trial.)
- [ ] No time-limited trial — Free tier (10 clients, 5 active devis) IS the trial
- [ ] No credit card at signup — friction kills conversion at awareness stage
- [ ] No countdown emails — remove Day 3 and Day 1 urgency emails entirely
- [ ] Day-7 human check-in only: "How's it going? Need anything?" (human touch, not countdown)
- [ ] Conversion trigger: artisan hits Free limit (10 clients or 5 active devis) — upgrade prompt at that moment, not before
- [ ] Aha moments by usage milestone: first client added, first devis sent, first follow-up reminder received
- [ ] **D46 NEW:** Measure the aha moment — at what usage milestone does a Free user become likely to consider upgrading? Set the limit trigger just BEYOND that moment (not arbitrary 10/5 — those are starting points, not targets)
- [ ] **D46 NEW:** Day 1 onboarding redesign — deliver first value in <5 minutes. First devis created in app, sent to WhatsApp. The limit should hit AFTER this moment, not before.
- [ ] **D46 NEW:** Soft limits before hard blocks — "vous êtes presque à limite" warning before the wall. Let artisan exceed once as a trust-building gesture.
- [ ] **D46 NEW:** Emotionally salient upgrade triggers — upgrade prompt at contextually meaningful moments (e.g., "un gros client? Créez un 6e devis") not cold "limit reached" banners.

### GTM Strategy (D48 — Wholesaler NOT Primary)
- [ ] **D48 NEW:** Audit solo artisan (45-55, French market) purchasing channels — identify top 5 digital touchpoints and top 3 specialist retailer types BEFORE committing to wholesaler investment
- [ ] **D48 NEW:** Primary GTM = digital channels: WhatsApp artisan groups, Facebook artisan communities, SEO for "devis/facture artisan" terms
- [ ] **D48 NEW:** Secondary GTM = specialist retailers who serve solo artisans (not generalist wholesaler chains)
- [ ] **D48 NEW:** Tertiary GTM = prescriber networks (architects, property managers) — pull-through demand at job site level
- [ ] Wholesaler presence (Gedimat/Point P counter displays) = secondary brand-awareness only, not primary acquisition

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

*Last updated: 2026-03-30T12:16*

---

## New from Pulse 2026-03-30T12:16

### Reopened (D6, D17, U8):
- **D6 (Trial):** REOPENED — Growth Strategist argues Free tier creates activation paralysis without time urgency. The "conversion at limit" thesis requires users to reach the limit, and most won't. Proposes 3-email Days 1-7 engagement sequence instead of countdown emails. Best resolution: Keep Free tier, add value-email sequence: "Day 1: Add your first client", "Day 3: Send your first devis", "Day 7: See how it works." Not countdown, not anxiety — value-first engagement.
- **D17 (Mobile strategy):** REOPENED — Technical Architect argues Expo's 2024 notification outages + ExpoKit deprecation history = unacceptable vendor lock-in at v1. Proposes Capacitor-Nuxt as alternative. Best resolution: Stick with Expo-RN BUT add direct FCM/APNS notification pipeline as circuit breaker if Expo fails. Add "no ExpoKit" policy. Monitor Expo notification uptime in first 3 months; if >1 outage, migrate to bare RN.
- **U8 (WhatsApp acquisition):** REOPENED — Product Strategist proposes WhatsApp-as-acquisition-channel. Every devis sent = brand impression + potential referral. Fatal flaw: most WhatsApp recipients are homeowners, not artisans. Test as secondary acquisition mechanism for B2B clients (property managers, business owners) with UTM-tracked CTA in WhatsApp message. Not a standalone GTM — secondary test alongside existing channels.

### New action items from this pulse:
- [ ] Add 3-email Days 1-7 engagement sequence to Free tier onboarding: "Day 1: Add your first client", "Day 3: Send your first devis", "Day 7: See how it works" — value-first, not countdown urgency
- [ ] Implement direct FCM/APNS notification pipeline as backup to Expo Notifications — circuit breaker pattern (Debate 39)
- [ ] Add "no ExpoKit" policy to development standards to prevent managed workflow drift
- [ ] Monitor Expo Notification service uptime for first 3 months — if >1 outage, trigger bare RN migration
- [ ] WhatsApp CTA in devis messages: KILLED. Explicit CTA in WhatsApp devis messages removed (attribution theater, wrong audience). Replace with in-product "Share with fellow artisan" referral mechanism for WhatsApp groups. B2B-only whisper-quiet test (no explicit sales copy) if any. (Debate 42)

### Challenged assumptions this pulse:
1. Free tier removes time pressure → better activation (Growth Strategist challenged: removes urgency that forces the aha moment)
2. Expo managed workflow = correct RN implementation for v1 (Technical Architect challenged: vendor lock-in + 2024 reliability issues)
3. WhatsApp is a delivery feature, not an acquisition channel (Product Strategist challenged: every sent devis = brand impression + referral opportunity)

---

## New from Pulse 2026-03-30T11:50

### Resolved (U1, D2, D5):
- **U1 (Discovery):** Growth Strategist won — U1 retired. Replaced by readiness protocol: (1) Figma prototype exists, (2) guerrilla usability test scheduled (5 artisans at wholesaler, single devis task), (3) pain confirmed via competitive analysis, (4) feature set frozen. If prototype not ready in 1 week: ship anyway and validate post-launch.
- **D2 (MVP scope):** Technical Architect refined — 4-feature MVP stands but with sequenced sprints: Sprint 0 = shared schema (TVA, sequential numbering, mentions légales), Sprint 1 = client file + devis, Sprint 2 = factures + relances. Phase 0.5 retired (teaches wrong lessons, risks schema drift).
- **D5 (Pricing):** Product Strategist won — Free + €29 two-tier. No €19 SKU at launch. Drop €49/€79 entirely. Value anchor: "2 heures par semaine sur vos devis et factures. C'est une heure de main d'œuvre. Votre abonnement? €29/mois."

### Challenged assumptions this pulse:
1. U1 discovery as prerequisite before building — challenged by Growth Strategist (guerrilla test + readiness criteria replace 10-artisan watch)
2. 4-feature MVP as parallel sprint — challenged by Technical Architect (it's a schema sequencing problem, not a parallel work problem)
3. €19/€29 two-tier as optimal — challenged by Product Strategist (Free + €29 two-tier beats €19/€29 on acquisition funnel; trust/usability > price as conversion barrier)

### New action items from this pulse:
- Get clickable devis-creation prototype in front of 5 real artisans within 10 days — or explicitly decide to skip and validate post-launch
- Sprint 0 = schema design (all 4 types + TVA + sequential numbering + mentions légales logic) — this is the critical path before feature development
- A/B test pricing page: "€1/jour" vs "une heure de main d'œuvre" framing with beta users before public launch

---

## New from Pulse 2026-03-30T12:28

### Resolved (D40, D41, D42):
- **D40 (Engagement channel):** Product Strategist won — email is the wrong channel for French artisan activation. Marc lives on WhatsApp, not email. A 9am email lands in an inbox he won't see until 9pm when he's exhausted. Push notifications + optional WhatsApp opt-in replace the 3-email Days 1-7 sequence. D6 updated: push + WhatsApp opt-in for engagement, not email.
- **D41 (Notification infra):** Technical Architect won — push notifications are NOT the product. The product is document management (devis, factures, relances). Email-based relances worked for decades; they're fine for v1. Do NOT build FCM/APNS circuit breaker at launch. Add push only if 50+ paying users complain. D17 updated: email-only at launch, push deferred to v2.
- **D42 (WhatsApp CTA):** Growth Strategist won — explicit CTA in WhatsApp devis messages is attribution theater. Homeowners receiving WhatsApp devis have zero purchase intent for B2B SaaS. Kill the explicit CTA. Replace with in-product "Share with fellow artisan" referral mechanism for WhatsApp group contexts. B2B-only whisper-quiet test (no explicit sales copy) if any. U8 updated.

### Challenged assumptions this pulse:
1. Email as the right engagement channel for Days 1-7 activation (Product Strategist challenged: WhatsApp-native artisans don't check email until 9pm)
2. Push notifications as core feature warranting complex infrastructure (Technical Architect challenged: document management is the product, not notifications)
3. WhatsApp devis CTA as measurable acquisition channel (Growth Strategist challenged: attribution theater, wrong audience)

### New action items from this pulse:
- [ ] Replace 3-email Days 1-7 sequence with push notifications + optional WhatsApp opt-in for Free tier engagement
- [ ] Optional WhatsApp opt-in during onboarding for artisans who prefer it
- [ ] 80% limit heads-up notification (not countdown) when Free tier approaches limits
- [ ] **D43 RESTATED:** Engagement channel is SECONDARY to Free tier design. Resolve first: what changes in Free tier design so artisans feel value BEFORE prompting? Three paths: (A) Lower limits (5 clients/3 devis), (B) Redesign Day 1 experience for immediate value, (C) Accept long-tail activation (month 2-3)
- [ ] **D44 REVERSED:** Do NOT ship email-only relances at launch. Obat markets real-time push notifications — email relances signal product inferiority. Choose: (A) Expo Push Notifications at launch (few hours if EAS Build exists), or (B) Cut relances from v1 entirely. Never email-only.
- [ ] Kill the "50+ users complain" push threshold — by the time 50 users have paid AND complained, reputation for inferior UX is already established
- [ ] 80% limit heads-up notification when Free tier approaches limits (not countdown, just awareness)
- [ ] **D42 CLOSED:** Kill explicit WhatsApp devis CTA — attribution theater, wrong audience
- [ ] **D45 CLOSED:** Kill in-product peer referral ("Share with fellow artisan") as primary acquisition — no incentive structure, wrong social dynamic, <2% expected activation
- [ ] WhatsApp sharing: keep as document sharing only (send devis PDF via WhatsApp — no CTA)
- [ ] **U10 NEW:** Pursue wholesaler/merchant GTM — Gedimat, Point P (1,900+ branches), Samse. Co-brand flyers, counter displays. Artisans visit weekly.
- [ ] **U10 NEW:** Pursue prescriber network outreach — architectes and property managers who recommend artisans. One prescriber → 50+ artisans.
- [ ] **U10 NEW:** SEO for "devis facture artisan" terms — compound growth, not one-shot referral

---

---

## New from Pulse 2026-03-30T12:58

### Resolved (D46, D47, D48):
- **D46 (Free tier limits):** Product Strategist won — do NOT lower limits from 10/5. Trust-building before limit enforcement. Lower limits create frustration ("c'est fait pour me piéger") before the aha moment is established. Keep generous limits, redesign Day 1 onboarding, use soft limits, make upgrade triggers emotionally salient.
- **D47 (Expo Push estimate):** Technical Architect won — "few hours" estimate is wrong. Reality: 1-2 weeks for production-ready Expo Push (token management backend, APNS certificate setup, testing). Budget properly or defer to v1.1.
- **D48 (Wholesaler GTM):** Growth Strategist won — Gedimat/Point P reach account-holder contractors, not solo Marc artisans. Solo artisans are mobile-first orderers, not branch visitors. Digital + specialist retailers first. Wholesaler secondary.

### Challenged assumptions this pulse:
1. Lower limits (5/3) create sooner conversion (Product Strategist challenged: creates frustration before aha moment, not urgency)
2. Expo Push = "few hours" work (Technical Architect challenged: 1-2 weeks reality for production-ready implementation)
3. 1,900+ wholesaler branches reach Marc (Growth Strategist challenged: wrong customer profile at generalist merchants)

### New action items from this pulse:
- [ ] **D46 NEW:** Define and measure the "aha moment" — at what usage milestone does a Free user become likely to upgrade? Set limit trigger just beyond that moment
- [ ] **D46 NEW:** Day 1 onboarding redesign — deliver first value in <5 minutes (first devis created and sent to WhatsApp)
- [ ] **D46 NEW:** Soft limits before hard blocks — "vous êtes presque à limite" warning, let artisan exceed once
- [ ] **D46 NEW:** Emotionally salient upgrade triggers — prompt at contextually meaningful moments, not cold "limit reached" banners
- [ ] **D47 UPDATED:** Expo Push = 1-2 weeks, not "few hours." If deadline can't accommodate: defer relances to v1.1 with email-only bridge
- [ ] **D48 NEW:** Audit solo artisan (45-55, French market) purchasing channels — top 5 digital touchpoints + top 3 specialist retailer types — before wholesaler investment
- [ ] **D48 UPDATED:** Primary GTM = digital channels (WhatsApp groups, Facebook communities, SEO). Secondary = specialist retailers. Tertiary = prescriber networks. Wholesaler = secondary brand-awareness only.

---

*Last updated: 2026-03-30T12:58*

---

## New from Pulse 2026-03-30T13:15

### Reopened (D48, D41/D47, D43/D46/D6):
- **D48 (GTM priority):** REOPENED — Product Strategist argues "digital first" conclusion confuses communication habitat (where Marc chats) with tool discovery pathway (how Marc adopts new tools). Recommends reversing GTM priority: prescriber networks FIRST (architects, property managers, building managers), specialist retailers SECOND, digital channels THIRD. Prescriber creates pull-through demand at moment of new project — highest intent in artisan sales cycle.
- **D41/D47 (Notification infra):** REOPENED — Technical Architect argues email-only relances at launch is a competitive liability, not an acceptable bridge. Obat markets "notifications et rappels en temps réel" as core feature. Feature comparison sites (GetApp, Capterra) will flag "no push notifications" as a red X before trial users ever try the product. 50-user complaint threshold is reactive damage control — by then the review narrative is already set. Expo Push (1-2 weeks budgeted) must ship at launch.
- **D43/D46/D6 (Free tier conversion):** REOPENED — Growth Strategist argues both limit-hit and contextual prompt models assume capacity anxiety/growth motivation that solo artisans don't have. Marc is in equilibrium — 6-7 steady clients, not building an empire. Neither limit proximity nor "meaningful moment" prompts will trigger upgrade desire. The correct model: Free tier → Habit → Dependency → Subscription. Conversion happens when daily use creates switching costs, not when a limit is hit.

### New action items from this pulse:
- [ ] **U11 NEW:** Audit prescriber networks as primary GTM channel — architects, property managers, building managers. What % of Marc's new jobs come via prescriber recommendation? If >30%, move prescriber networks to GTM priority #1.
- [ ] **D48 UPDATED:** Revised GTM priority order: (1) Prescriber networks (architects, property managers, building managers), (2) Specialist retailers serving solo artisans, (3) Digital channels (WhatsApp groups, Facebook, SEO), (4) Wholesaler presence (brand awareness only). Pending validation via U11 audit.
- [ ] **D41/D47 UPDATED:** Expo Push at launch is NOT optional. 1-2 weeks of engineering is already budgeted. Email-only relances as bridge creates feature-comparison disqualification on GetApp/Capterra before trial users ever try the product. Budget the 1-2 weeks; ship push relances at launch.
- [ ] **D43/D46/D6 UPDATED:** Free tier design should optimize for habit formation, not limit management. Primary KPI: daily evening open rate (2-min devis ritual). Secondary KPI: 30-day retention. Limit proximity is a tertiary metric, not primary.
- [ ] **D43/D46/D6 NEW:** Design the "soir" ritual — evening reminder nudge ("C'est l'heure de votre devis du soir") optimized for 8-9pm Paris time. This is the habit anchor, not the upgrade prompt.
- [ ] **D43/D46/D6 NEW:** Raise Free tier limits further if needed to remove friction from habit formation — goal is daily ritual, not proximity to limit.

### Challenged assumptions this pulse:
1. Digital channels = where Marc discovers tools (Product Strategist challenged: confuses communication habitat with discovery pathway; prescriber endorsement at moment of new project is 10x higher intent)
2. Email-only relances = acceptable bridge at launch (Technical Architect challenged: feature comparison disqualification happens before signup, not after; 50-user complaint threshold is reactive)
3. Conversion = limit-hit or contextual prompt (Growth Strategist challenged: solo artisans in equilibrium don't feel capacity anxiety; habit → dependency → subscription is the correct model)

---

*Last updated: 2026-03-30T15:46*

## New from Pulse 2026-03-30T15:46

### Resolved (D63, D64, D65):
- **D63 (Free tier pull):** RESOLVED — "situation financière" snapshot (outstanding devis, pending factures, revenue vs last month, dormant clients) is the Free tier's primary value output. Notification channel debates are secondary until this exists.
- **D64 (Sprint 0 stack):** RESOLVED — Fastify + Postgres must START Sprint 0. Nuxt 3 retired from backend. Day 1 = Postgres schema + Fastify scaffold. Day 2 = TVA service + sequential numbering + mentions légales. Day 3 = REST API ready for React Native integration.
- **D65 (U15 discovery):** RESOLVED — three-phase guerrilla session: observe first (20 min, no demo), quantify pain (time/emotional weight), payment conversation only if pain confirmed. "Show demo, ask price" removed from U15.

### Challenged assumptions this pulse:
1. Engagement channel is the lever for Free tier activation — challenged: channel is secondary to whether Free tier delivers compelling output worth returning to see
2. "Defer API-first to post-MVP" is safe — challenged: Sprint 0 work IS the business logic foundation; migration cost scales with integration depth; deferral becomes permanent
3. "Show demo, ask price" as first validation step — challenged: demo-first puts artisan in audience mode; pain must be observed before payment questions

### New action items from this pulse:
- [ ] **D63 NEW:** Design the "situation financière" snapshot — weekly auto-produced output: outstanding devis (days-open), pending factures (aging buckets: 15/30/45/60+ days), revenue this month vs last month, dormant clients (30+ days inactive). Push-ready content. Primary Free tier value output.
- [ ] **D64 NEW:** Sprint 0 Day 1 — Fastify + Postgres schema (TVA per-line, sequential numbering, mentions légales renderer, client-type). NOT Nuxt 3. Mobile team integrates against REST from Day 3.
- [ ] **D65 UPDATED:** U15 three-phase protocol — observe first (no demo), quantify pain, payment only if confirmed. Remove "show demo, ask price" entirely.

---

*Last updated: 2026-03-30T15:33*

## New from Pulse 2026-03-30T15:33

### Reopened (D63, D64, D65):
- **D63 (Free tier activation):** Product Strategist won — channel (email/push/WhatsApp) is the wrong variable. Free tier needs self-generating pull: a dashboard/report that makes artisans *want* to return, not notifications dragging them back. D40 RESTATED.
- **D64 (Sprint 0 architecture):** Technical Architect won — "defer to post-MVP" is a sunk cost trap. Fastify + Postgres must START Sprint 0. Sprint 0 with Nuxt 3 means business logic inside Nuxt server routes; post-MVP migration never happens. D57 REOPENED.
- **D65 (U15 validation):** Growth Strategist won — customer discovery (observe pain, quantify time/emotional weight) must precede price questions. "Show demo, ask WTP" puts you in persuasion mode. Three-phase guerrilla session: observe → quantify → payment. U15 UPDATED.

### Challenged assumptions this pulse:
1. Engagement channel (email vs push vs WhatsApp) is the activation lever (Product Strategist challenged: channel is secondary to whether Free tier creates pull — a report/dashboard that generates desire to return)
2. "Defer API-first to post-MVP" is safe (Technical Architect challenged: deferral becomes permanent; Fastify+Postgres is faster for Sprint 0 anyway)
3. Price validation with a demo is the right first guerrilla step (Growth Strategist challenged: observe pain first, ask about payment only if pain confirmed)

### New action items from this pulse:
- [ ] **D63 NEW:** Free tier self-generating pull — design a dashboard/report (e.g., "situation financière" snapshot: outstanding devis, pending factures, aging report) that creates desire to return. Notification channel debates premature until this exists.
- [ ] **D64 UPDATED:** Sprint 0 starts with Fastify + Postgres API (NOT Nuxt 3). Day 1: Postgres schema + TVA service + sequential numbering service + mentions légales renderer. Day 3: REST API consumed by React Native. Nuxt 3 never touches the backend.
- [ ] **D65 UPDATED:** U15 three-phase guerrilla session — (1) 20-min observation of actual admin workflow, no demo; (2) pain quantification (time spent/week, emotional weight 1-10, lost revenue from forgotten devis); (3) payment conversation only if pain confirmed. Remove "show demo, ask price" from U15.

