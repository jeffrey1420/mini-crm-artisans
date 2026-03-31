# Mini-CRM → Devis & Factures — Resolved Decisions & TODO

> **Pivot applied 2026-03-30** — Based on external review. Full pivot from "CRM for artisans" to "devis/factures/relances tool."

## ✅ Resolved Decisions

| ID | Topic | Decision | Source | Date |
|----|-------|----------|--------|------|
| D1 | Positioning | Kill "CRM" — sell "devis, factures, relances" | External review | 2026-03-30 |
| D2 | Sprint 1 timeline | RESOLVED — Sprint 1a (Days 1-5: client file + devis flow) + Sprint 1b (Days 6-10: PDF + mentions légales + sharing + polish). Parallelization of backend and mobile on PDF endpoint recovers 3-5 days. Sequential numbering is 1 day, not 2. Viable 2-week sprint. | Debate 68 (Technical Architect) | 2026-03-30 |
| D3 | Primary persona | Marc — solo smartphone-native artisan | External review | 2026-03-30 |
| D4 | Stack | **Supabase EU-hosted (Frankfurt)** — self-hosted on OVH NOT recommended for v1. Fastify + Postgres + Coolify retired for v1. EU-hosted = fastest path, zero ops overhead, full GDPR compliance. Prior Postgres schema work transfers directly to Supabase. | Debate 100 (Technical Architect) + pulse-2040-architect | 2026-03-30 |
| D5 | Pricing | Free + €29 two-tier. No €19 SKU. Drop €49/€79. Value anchor: "2h/week = 1h labor = €29/month." | Debate 33 (Product Strategist) | 2026-03-30 |
| D6 | Trial | No time-limited trial. Free tier IS the trial (10 clients, 5 active devis). Conversion happens at Free limit. Engagement: restated by D43 — channel secondary, Free tier design determines activation. 80% limit heads-up notification. No countdown emails. | Debates 38/43 (Product Strategist) | 2026-03-30 |
| D7 | Architecture | Nuxt 3 + OVH managed Postgres — REFINED: API-first preferred but deferred to post-MVP unless blocking Sprint 0 | Growth+Architect | 2026-03-30 |
| D8 | E-invoicing | v2 feature (Chorus Pro compatible) | External review | 2026-03-30 |
| D9 | Not MVP | No Kanban, no multi-user, no API keys. Offline-first with background sync. | External review + D81 | 2026-03-30 |
| D10 | Buyer trigger | "Admin pain" not "CRM need" | External review | 2026-03-30 |
| D11 | Mobile | React Native from Day 1 via Expo. Push notifications: Expo Push at launch (budget 1-2 weeks). | Debates 27/44/47 (Technical Architect) | 2026-03-30 |
| D12 | Landing page | Simplicity-first — H1: "Vos devis et factures, sans vous prendre la tête." H2: "Créez et envoyez votre premier devis en 5 minutes. Depuis votre téléphone." Proof lives in Free tier. | Debates 19/53 (Product Strategist) | 2026-03-30 |
| D13 | Home view | Job-first — Active Job Card as home anchor, not Dashboard or Timeline | Debate 20 (Technical Architect) | 2026-03-30 |
| D14 | E-invoicing timing | v2 — NOT Day 1 (Debate 21 Growth Strategist) | Debate 21 |
| D15 | Relances differentiator | Secondary feature only — below fold, "Fonctionnalités" section. Frame as "Suivi de paiement" not "Relances automatiques." Not in hero. | Debate 25 (Product Strategist) |
| D16 | Trial length | 14 days (updated from 30). No credit card at signup. Email drip: day 7, 3, 1. | Debate 26 (Growth Strategist) |
| D17 | Mobile strategy | React Native from Day 1 via Expo. Push notifications: preferred Expo Push at launch (if EAS Build exists), alternative cut relances from v1. Never email-only. | Debates 27/44 (Technical Architect) | 2026-03-30 |
| D40 | Engagement channel | REFINED — Path A: channel secondary to output design. Path B: channel IS the primary activation lever. WhatsApp non-negotiable for Path B. Sprint 0 must build WhatsApp Business API as first-class notification channel, not optional. | Debate 143 (Product Strategist) | 2026-03-31 |
| D41 | Notification infra | REVERSED — email-only relances wrong. Obat markets push. Preferred: Expo Push at launch. Alternative: cut relances from v1. | Debate 44 (Technical Architect) | 2026-03-30 |
| D42 | WhatsApp referral | CLOSED — kill CTA in devis, kill in-product peer referral as primary acquisition. Redirect to wholesaler presence + prescriber networks + SEO. | Debate 45 (Growth Strategist) | 2026-03-30 |
| D46 | Free tier limits | Do NOT lower limits from 10/5. Keep generous limits. Trust-building before limit enforcement. Limit should hit AFTER aha moment, not before. | Debate 46 (Product Strategist) | 2026-03-30 |
| D47 | Expo Push estimate | 1-2 weeks, not "few hours." Budget properly or defer to v1.1. | Debate 47 (Technical Architect) | 2026-03-30 |
| D48 | Wholesaler GTM | Not primary GTM. Digital + specialist retailers first. Wholesaler secondary brand-awareness play only. Audit solo artisan purchasing channels first. | Debate 48 (Growth Strategist) | 2026-03-30 |
| D53 | Landing page framing | Simplicity-first RETAINED. H1: "Sans vous prendre la tête." H2: 5-minute specific/demonstrable claim. Proof lives in Free tier. No "professional-grade" in hero. | Debate 53 (Product Strategist) | 2026-03-30 |
| D54 | Sprint 0 TVA | RESOLVED — arrondi commercial is the standard (not arithmétique vs bancaire binary). `Math.round(v * 100) / 100` is the Sprint 0 default. Audit risk is €30-80/year, not €600. No BOFiP lookup required. Sprint 0 TVA calculator implement with arrondi commercial. | Debate 69 (Technical Architect) | 2026-03-30 |
| D55 | Buyer-user split | Dual-persona GTM. Marc = economic buyer (primary). Admin handler = operational user (secondary). Expert-comptable = Phase 2. | Debate 55 (Growth Strategist) | 2026-03-30 |
| D56 | WoM attribution | WoM = Month 3+ lagging indicator. Digital acquisition PRIMARY at launch. "Comment connaissez-vous?" at signup. Referral codes in v1. Month 3 target: 20% peer referral. | Pulse 14:57 (Product+Growth) | 2026-03-30 |
| D57 | Architecture | **CLOSED — Nuxt 3 eliminated from v1 architecture.** No role for Nuxt 3 — no web application, landing is static, mobile app bypasses Nuxt entirely. Backend = Supabase EU-hosted (D100). | Pulse 00:58 (Technical Architect) | 2026-03-31 |
| D59 | Pricing credibility | **SUPERSEDED by U15 (Debate 101):** Founding member offer ELIMINATED. No lifetime deal. No founding/access tier. Replace with "Support Prioritaire" (relationship benefits: direct WhatsApp to Louis, roadmap vote, named credits). Single €29/month price, no founding/standard tiers. | Debate 101 (Growth Strategist) | 2026-03-30 |
| D63 | Free tier pull | UPDATED — Situation financière = server-computed push notification at 8pm Paris, NOT in-app dashboard. Free tier gets daily notification. €29 tier gets full snapshot + in-app drill-down. **REFINED: Path A (formal-devis) conversion trigger ONLY. Path B (verbal-agreement) excluded — see D141.** | Debate 83 (Product Strategist) + Pulse 00:58 (Growth Strategist) | 2026-03-30 |
| D64 | Sprint 0 timeline | UPDATED — Sprint 0 = 5-7 days (D86 reversed offline-first, recovering 3-5 days). Full scope: offline-capable + mentions légales + WhatsApp PDF + real device testing. | Debate 84/86 (Technical Architect) | 2026-03-30 |
| D70 | Document archive | RESOLVED — document archive PRIMARY, financial snapshot to €29 tier. | Pulse 16:44 | 2026-03-30 |
| D71 | Sprint 0 scope | RESOLVED — 5 days, sequential numbering deferred to Sprint 2 (factures). | Pulse 16:44 | 2026-03-30 |
| D72 | Expert-comptable Phase 1 | UPDATED — Expert-comptable outreach = Week 1 (recommendation channel, not data-sync). Data-sync portal = Phase 2. GetApp/Capterra profiles claimed before launch. | Debate 85 (Growth Strategist) | 2026-03-30 |
| D81 | Offline-first | REVERSED — Sprint 0 = offline-capable (optimistic UI + retry queues + AsyncStorage). WatermelonDB/expo-sqlite + background sync + conflict UI deferred to v1.2. Sprint 0 recovers 3-5 days. | Debate 86 (Technical Architect) | 2026-03-30 |
| D82 | Digital peer communities | Retention/engagement spaces, NOT acquisition channels. WhatsApp groups + Facebook = brand recall + peer support. SEO = primary digital discovery. Prescriber = highest-trust acquisition. | debate-DigitalChannels.md | 2026-03-30 |
| D83 | Situation financière delivery | REFINED by D89 — configurable notification window KILLED. Event-only notification on first accepted devis. Recurring digest for dormant Free users (14+ days no accepted devis) as "stay in touch" mechanism. **REFINED by D141: applies to Path A only. Path B excluded.** Sprint 0 adds: push infra + accepted-devis trigger. | Debates 83/88/89 (Product Strategist) + Pulse 00:58 (Growth Strategist) | 2026-03-30 |
| D84 | Sprint 0 realistic timeline | REFINED by D90 — 5.5-6.5 days (updated from 8-10). D86 (offline-capable) + D74 (API key auth) eliminate sequential dependency. Parallel backend + mobile tracks from Day 1. | Debates 84/90 (Technical Architect) | 2026-03-30 |
| D85 | GetApp/Capterra | **RESOLVED — REMOVED from TODO.** Channel does not match D55 buyer journey (admin handler validates, does not discover). Week 1 hours reallocated to expert-comptable outreach. Revisit Month 3 only if artisan survey contradicts peer-referral model. | Debate 122 (Growth Strategist) | 2026-03-30T22:30 |
| D89 | Situation financière notification | RESOLVED — event-only notification (first accepted devis). Configurable digest window REMOVED. D76 conversion trigger = notification trigger. | Debate 89 (Product Strategist) | 2026-03-30 |
| D90 | Sprint 0 timeline estimate | RESOLVED — 5.5-6.5 days with parallel backend + mobile tracks. API contract defined Day 1. | Debate 90 (Technical Architect) | 2026-03-30 |
| D91 | Expert-comptable validation vs referral | RESOLVED — U12 split: validation (Week 1, Louis's own, no prerequisites) ≠ referral (Week 4-6, with testimonials). | Debate 91 (Growth Strategist) | 2026-03-30 |
| D95 | Sprint 0 timeline | **RESOLVED (FINAL) — Debate 108:** 5 days (target) if pre-conditions confirmed before sprint. 6.5 days (floor) if pre-conditions not confirmed. Do NOT cut corners on TVA rounding or mentions légales to hit 5 days. Pre-sprint gates: (1) Louis shows written 4 mentions légales templates (file/git commit), (2) Louis shows Supabase project dashboard. Cut order if pressure: mentions légales plain text → AsyncStorage. | Debate 108 (Technical Architect) | 2026-03-30 |
| D96 | Conversion trigger | **SUPERSEDED by Debate 110 — Dual-path conversion:** Path A (Formal-Devis Artisan): Limit-hit (5 active devis OR 10 clients) OR first paid facture = hard gate. Path B (Verbal-Agreement Artisan): 45 consecutive days of active product usage (job created/updated) OR 7+ jobs logged OR 5+ active clients managed = conversion trigger. Day 14 human WhatsApp check-in applies to both archetypes as primary conversion moment. | Debate 110 (Product Strategist) | 2026-03-30 |
| D97 | Sprint 0 prep | Louis writes 4 mentions légales templates this week (2h) — gate for 5-day Sprint 0. **REFINED by D142: gate NOT met as of 2026-03-31. 5-day timeline CONDITIONAL on real committed strings. See D142.** | Debate 97 (Technical Architect) + Pulse 00:58 (Product Strategist) | 2026-03-30 |
| D98 | Platform default | **REFLECTED — Direction confirmed, validation mechanism updated.** Android-first remains correct for French artisan demographic. "Week 1 poll validates" REMOVED (wrong instrument after U15 elimination). Replaced with install completion rate (≥50% in 48h) as Sprint 0 metric. D24 resolution gates Sprint 0 specificity. | Debates 98/103 (Growth Strategist) | 2026-03-30 |
| D99 | Pricing structure | **KILLED — Usage-based billing permanently retired.** Flat €29/month + €260/year annual billing at launch. Usage-based incompatible with dual-path conversion (Path B artisans can't be metered). | Debate 125 (All 3 agents) | 2026-03-30T23:31 |
| D114 | PDF Sprint 0 gate | **RESOLVED — HTML-to-PDF Edge Function (not expo-print).** Same HTML serves WhatsApp OG preview. Mentions légales embedded in HTML string Sprint 0. | Debate 126 (Technical Architect) | 2026-03-30T23:31 |
| U15 | Founding member offer | ELIMINATED — no lifetime deal, no founding/access tier, no "50 places" scarcity. Single €29/month. Replaced by "Support Prioritaire" (direct WhatsApp to Louis, roadmap vote, named credits). | Debate 101 (Growth Strategist) | 2026-03-30 |
| U7 | Domain purchase | RESOLVED — buy domain now (park it), defer brand decision. Domain = infrastructure, not branding. Parking costs ~€10-15/year. Expert-comptable outreach and GetApp/Capterra profiles need a proper domain to establish credibility. Brand name decision stays open. | Debate 109 (Growth Strategist) | 2026-03-30 |
| D138 | Annual billing implementation | REFINED — Annual €240/year = €20/month = DEFAULT at checkout. Monthly €29 = fallback option. Annual-first framing: "La plupart de nos artisans préfèrent l'abonnement annuel." Opt-in annual achieves ~10% uptake; default annual targets 35-45%. "Payez quand vous êtes chargé" seasonal framing KILLED — wrong frame for cash-flow-sensitive artisans. | Debate 145 (Growth Strategist) | 2026-03-31 |
| D139 | Expert-comptable timing | REFINED — Customer development = Week 3 (not Week 1). Sprint 0 = build only. Week 3 = working iOS/Android build + real devis = genuine feedback conversation. Louis's own accountant = Week 3 validation call (not Week 1). Referral program = Month 4+. Week 1 hours reallocated from outreach to Sprint 0 build. | Debate 145 (Growth Strategist) | 2026-03-31 |
| D140 | Offline architecture | REFINED — AsyncStorage + retry queues inadequate for Sprint 0. Phone death mid-write loses in-memory operations (primary use case, not edge case). 50-job sync burst creates client ID divergence risk with server-wins resolution. Expo-sqlite (+2 days to Sprint 0) required for production-grade offline reliability, OR Sprint 0 offline labeled demonstration-only with honest engineering disclosure. | Debate 144 (Technical Architect) | 2026-03-31 |
| D141 | Situation financière notification | REFINED — notification is Path A (formal-devis) conversion trigger ONLY. Path B (verbal-agreement) has no "situation financière" trigger. Path B retention = usage-based (job logging habit) + recurring "stay in touch" digest for dormant Free users (14+ days inactive). | Pulse 00:58 (Growth Strategist) | 2026-03-31 |
| D142 | Sprint 0 gate | REFINED — mentions légales gate requires real committed strings (Louis's own business data in `legal/mentions-legales.ts`). TODO comments eliminated. Gate must be verified before Sprint 0 starts. 5-day timeline is CONDITIONAL on gate being met. | Pulse 00:58 (Product Strategist) | 2026-03-31 |

## New from Pulse 2026-03-31T00:58 — Three Specialist Debates (D57 CLOSED, D141, D142)

### Resolved

- **D57 CLOSED (Architecture):** Technical Architect closed the oldest open architectural question — Nuxt 3 has no role in v1. Backend = Supabase EU-hosted (D100). Landing = static HTML. Mobile = Expo/React Native direct to Supabase. No Nuxt 3 anywhere in the stack. D57 was SUPERSEDED by D100 but never formally CLOSED — now closed.
- **D141 (Situation financière notification):** Growth Strategist revealed "situation financière" notification is Path A (formal-devis) conversion trigger ONLY. Path B (verbal-agreement artisan) has no "situation financière" trigger — they never produce formal accepted devis. Path B retention = usage-based (job logging habit) + recurring "stay in touch" digest for dormant Free users (14+ days inactive). Debate log's framing of "situation financière" as universal PRIMARY Free tier value was incorrect for ~40-50% of target market.
- **D142 (Sprint 0 gate):** Product Strategist confirmed the Sprint 0 gate has NOT been met. Louis has not committed the 4 mentions légales templates to the repo. The 5-day Sprint 0 estimate is CONDITIONAL on this gate being satisfied. Mentions légales as TODO comments eliminated. Gate must be: `legal/mentions-legales.ts` committed to git with Louis's actual business data before Sprint 0 begins.

### Challenged Assumptions This Pulse

1. "Nuxt 3 remains relevant as a web framework given Supabase replaced Fastify" — challenged by Technical Architect: no web application exists to justify Nuxt 3's SSR capabilities; mobile app bypasses Nuxt entirely
2. "Situation financière is the universal Free tier retention mechanism" — challenged by Growth Strategist: Path B artisans never produce an accepted devis event; notification is Path A-only
3. "5-day Sprint 0 is achievable this week" — challenged by Product Strategist: gate not met, mentions légales as TODO comments not acceptable, 7-8 days is the realistic floor

### New Action Items

- [ ] **D57 CLOSED:** Nuxt 3 is eliminated from v1 architecture. No Nuxt dependency in any Sprint 0 planning. Update any existing Nuxt project references in the repo.
- [ ] **D141 NEW — Path B retention mechanism:** Define the recurring "stay in touch" digest for dormant Free users (14+ days inactive) — content, frequency, delivery channel. This is Path B's primary retention touch.
- [ ] **D141 NEW — Path A notification timing:** The "situation financière" first-accepted-devis event trigger should also include: "your pipeline is now worth €X" (server-computed from accepted devis amounts). Conversion ask follows the notification.
- [ ] **D142 — Sprint 0 gate (URGENT):** Louis must commit `legal/mentions-legales.ts` to git with real business data BEFORE Sprint 0 begins. If not committed: Sprint 0 = 7-8 days. If committed: 5-day Sprint 0 stands. This week.
- [ ] **D142 NEW — Sprint 0 handoff doc:** Add explicit note: "Mentions légales gate: Louis's own data committed as real strings, not TODO comments. Gate verified by: git status legal/"
- [ ] **D141 UPDATED — D83/D89 updated:** "Situation financière" notification is Path A conversion trigger ONLY. Path B excluded by workflow design. D83 entry in this doc updated accordingly.

### Challenged This Pulse

1. "Nuxt 3 + Supabase is the architecture" — Technical Architect: Nuxt 3 is irrelevant, mobile bypasses it, landing is static
2. "Situation financière is the universal Free tier retention mechanism" — Growth Strategist: Path B artisans never trigger it
3. "5-day Sprint 0 is achievable" — Product Strategist: gate not met, mentions légales not committed


## 🔄 Reopened This Pulse (Resolved in 15:17 Pulse)

---

## New from Pulse 2026-03-30T22:30 — Three Resolved (D120, D121, D122)

### Resolved

- **D120 (D99 — Pricing):** RESOLVED — Flat €29/month + €260/year annual billing at launch. Per-devis deferred to v1.2. Annual billing solves seasonality without per-devis conversion-moment friction (metering at peak conversion moment = churn trigger). Per-devis revisited in v1.2 after real seasonality data and billing maturity.
- **D121 (D114 — PDF Sprint 0 gate):** RESOLVED — expo-print Sprint 0 prototype APPROVED. Sprint 1b adds proper document storage (Supabase blob + documents table + PDF URL). Legal labeling required in Sprint 0 handoff doc. Phase 2 compliance prerequisite acknowledged.
- **D122 (D85 — GetApp/Capterra):** RESOLVED — REMOVED from TODO. Channel doesn't match D55 buyer journey. Admin handler validates Marc's choice (not independently discovers on comparison sites). Week 1 hours reallocated to expert-comptable cold call script + D91 validation.

### Challenged Assumptions This Pulse

1. "Per-devis pricing is compatible with D96's conversion trigger" — challenged by Product Strategist: metering friction at peak conversion moment + retroactive billing shock for Path B artisans
2. "Storage is a v2 concern" for expo-print PDFs — challenged by Technical Architect: French invoice retention law (L123-22) requires 10-year tamper-evident storage; WhatsApp is not an accounting archive
3. "GetApp/Capterra is relevant to the admin handler's buyer journey" — challenged by Growth Strategist: D55 defines admin handler as operational validator, not prospective discoverer; peer referral closes deal before comparison sites become relevant

### New Action Items

- [x] **D120 RESOLVED:** Flat €29/month + €260/year annual at launch. Per-devis deferred to v1.2.
- [x] **D122 RESOLVED:** GetApp/Capterra removed from TODO. Week 1 hours → expert-comptable outreach script + D91 validation.
- [ ] **D121 NEW:** Sprint 1b document storage migration — Supabase blob + documents table + PDF URL in API response. 2-3 days. Legal compliance gate for Phase 2.
- [ ] **D121 NEW:** Sprint 0 handoff doc note — "WhatsApp share PDF is a prototype, not an accounting record."
- [ ] **D122 NEW:** Validate D55 admin handler buyer journey at Point P this Saturday — "When you needed new software, how did you find out about it?" If >40% say peer referral, peer model stands.
- [ ] **D120 Path B billing:** Any billing model for Path B artisans must be prospective-only from conversion date. No retroactive charges for Free tier usage.


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
- **D49 UPDATED (Debate 82):** Digital peer communities (WhatsApp groups, Facebook) reclassified as RETENTION/ENGAGEMENT, NOT acquisition. SEO = primary digital acquisition. WhatsApp groups + Facebook = brand recall and peer support for existing users, not discovery.
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

*Last updated: 2026-03-30T17:59*

## New from Pulse 2026-03-30T14:57

### Resolved (D56, D57, D59):
- **D56 (WoM attribution):** REFINED — 40% WoM attribution retired as GTM input. WoM = Month 3+ lagging indicator, not launch channel. Digital acquisition PRIMARY at launch. "Comment avez-vous connu?" at signup (required, predefined options). Referral codes in v1. Month 3 target: 20% peer referral.
- **D57 (Architecture):** REFINED — API-first (Fastify + static landing) is architecturally cleaner for mobile-first + static product. But: shipping velocity matters more than purity for first 10 users. Defer migration unless Nuxt 3 actively blocks Sprint 0. Post-MVP migration if ROI positive.
- **D59 (Pricing credibility):** NEW — €29 price point is unvalidated with real artisans. "One hour of labor" anchor is founder math. Guerrilla price validation (5 artisans) + founding member €19/mo offer + 3% Day-30 conversion target + SEPA direct debit proposed.

### New Action Items from this pulse:
- [x] **D56 RESOLVED:** WoM = Month 3+ lagging indicator. Digital acquisition PRIMARY at launch. "Comment connaissez-vous?" at signup. Referral codes in v1.
- [ ] **D57 CLOSED:** Nuxt 3 eliminated from v1 architecture. Backend = Supabase EU-hosted (D100). Sprint 0 uses Supabase directly — no Fastify, no Nuxt 3. Verify no Nuxt references in any Sprint 0 code.
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
- [ ] U1 readiness check: (1) Figma/clickable devis-creation prototype, (2) guerrilla test scheduled (workshop/job site via warm network — NOT wholesaler), (3) pain confirmed by competitive analysis, (4) feature set frozen
- [ ] **D64 RESOLVED:** Sprint 0 starts with Supabase EU-hosted (D100). Day 1 = Supabase schema (TVA per-line, sequential numbering, mentions légales, client-type). Day 2 = TVA calculator + sequential numbering engine + mentions légales renderer. Day 3 = full CRUD REST via Supabase client ready for React Native integration. Fastify retired. Nuxt 3 eliminated. (Debate 64 + D100 + D57 CLOSED)
- [ ] **D65 RESOLVED:** U15 three-phase guerrilla protocol — (1) 20-min observation of actual admin workflow, no demo, no pitch; (2) pain quantification (time spent/week, emotional weight 1-10, lost revenue from forgotten devis); (3) payment conversation ONLY if pain is confirmed. Remove "show demo, ask price" from U15. (Debate 65)
- [ ] **D63 RESOLVED:** Design the "situation financière" snapshot for Free tier home — automatically-produced weekly output showing: outstanding devis (with days-open), pending factures (aging buckets: 15/30/45/60+ days), revenue this month vs last month, dormant clients (30+ days inactive). This is the Free tier's primary value output for Path A. Push-ready content. **For Path B: "stay in touch" digest for dormant users (14+ days inactive) is the retention mechanism.**
- [ ] If prototype not ready in 1 week: proceed to build anyway, validate post-launch (Debate 31)
- [ ] Sprint 0: Supabase EU-hosted only (NOT Fastify, NOT Nuxt 3). Compliance foundations first (3-4 days): TVA per-line schema, sequential numbering engine, mentions légales renderer, client-type schema. Sprint 1 = client+devis flow. Sprint 2 = facture+email relances. (Debates 54/64 + D100 + D57 CLOSED)
- [ ] **D81 NEW (SUPERSEDED by D86):** Sprint 0 is offline-first. WatermelonDB/expo-sqlite for local-first storage (~2 days mobile work). Backend: add `updated_at` timestamps + accept client-generated UUIDs on all entities (~2 hours). Sync: last-write-wins with conflict UI. No changes to API endpoint contracts.
- [ ] **D81 UPDATED (SUPERSEDED by D86):** Sprint 0 timeline updated to 7 days (was 5 days, +2 days for offline-first). Offline-first is required at launch — D9's "no offline" decision was made before React Native stack was chosen and no longer applies.
- [x] **D57 RESOLVED:** API-first (Node/Fastify + static landing + JWT) preferred. Nuxt 3 deferred unless blocking Sprint 0. OVH managed Postgres retained. (Debate 61)
- [x] **D58 RESOLVED:** Email relances in v1 (Sprint 2, 1-2 days). Expo Push relances in v1.1. (Debate 58)
- [x] **D56 RESOLVED:** 40% WoM figure RETIRED. Measurement protocol: "Comment connaissez-vous?" at signup + referral codes. Month 3 target: 20% peer referral. (Debate 60)
- [ ] Pick one: Tolteck competitor or Tolteck complement?
- [x] ~~Buy domain (U7)~~ **RESOLVED — Debate 109:** Buy domain now (park it), defer brand decision. Domain = infrastructure, not branding. A parked domain costs €10-15/year and blocks nothing. Expert-comptable outreach and GetApp/Capterra setup need a proper domain. Brand name decision stays open. (Debate 109)
- [ ] Build the Active Job Card data model (`jobs.status`, `jobs.scheduled_date`, `jobs.updated_at`)
- [x] RESOLVE D15: Relances = secondary feature below fold. "Fonctionnalités" section only. NOT in hero.
- [x] RESOLVE D16: SUPERSEDED — 14-day trial concept retired. Free tier IS the trial (Debate 38/40).
- [x] RESOLVE D17: React Native from Day 1 via Expo. Email-only at launch. Push deferred to v2 unless 50+ paying users complain (Debate 41).
- [x] RESOLVE D2: Sequenced sprint structure (Sprint 0 = schema, Sprint 1 = client+devis, Sprint 2 = facture+relances). Phase 0.5 retired.
- [x] RESOLVE D5: Free + €29 two-tier. Drop €49/€79. Value anchor: "2h/week = 1h labor = €29/month." No €19 SKU at launch.

### New from Pulse 2026-03-31T01:15 (D143, D144, D145)
- [ ] **D40 NEW — WhatsApp Business API Sprint 0:** For Path B, WhatsApp is the primary activation channel, not optional. Sprint 0 notification architecture must include WhatsApp Business API as first-class delivery. This is the activation mechanism for ~40-50% of the target market (verbal-agreement artisans).
- [ ] **D141 NEW — Path B digest spec:** WhatsApp Business API, bi-weekly (Day 14, 28, 42), max 3 digests, 14+ days dormant + ≥1 job logged + Path B. Plain text, user metrics reflected, single re-entry CTA, Louis contact. No upgrade prompts. Conversion by re-establishing habit until limit-hit fires.
- [ ] **D110 REFINED — Path B soft limit:** Define Free tier soft limit for Path B (e.g., 1 client / 3 jobs cap) that creates blocked workflow equivalent to Path A's limit-hit. Usage-based triggers (45d/7jobs/5clients) fire without felt friction — Sprint 0 must specify this.
- [ ] **D138 REFINED — Annual as DEFAULT checkout:** Present annual €240/year = €20/month as DEFAULT. Monthly €29 is fallback. Stripe annual plan with monthly installments. Framing: "La plupart de nos artisans préfèrent l'abonnement annuel." Remove opt-in discount language.
- [ ] **D139 REFINED — Expert-comptable MOVED to Week 3:** Sprint 0 = build only. Expert-comptable Week 3 with working build + real devis. Louis's own accountant = Week 3 validation. Week 1 hours reallocated to Sprint 0.
- [ ] **D140 REFINED — Expo-sqlite required Sprint 0:** Decision: (+2 days) OR (label Sprint 0 offline as demonstration-only). AsyncStorage loses data on phone death (primary use case). Expo-sqlite + background sync is production-grade.

### New from Pulse 2026-03-31T01:29 (D40/D139/D140 challenged — OPEN)

**D40 CHALLENGED (PS-Pulse-0129):** Product Strategist challenges WhatsApp Business API in Sprint 0: Meta Business Verification alone takes 2-14 days (blowing 5-day sprint), delivers zero value at v1 (no premium content to push), and conflates acquisition with retention. Position: defer WhatsApp to v1.1; Sprint 0 notification = Expo Push only.
- [ ] **D40 DECISION NEEDED:** Louis chooses — WhatsApp in Sprint 0 (accept timeline risk) OR defer to v1.1 (Expo Push only in Sprint 0). Gates Sprint 0 notification architecture.

**D139 CHALLENGED (GS-Pulse-0129):** Growth Strategist challenges Week 3 expert-comptable timing: Week 3 produces solution-feedback (reacting to what Louis built), not problem-framing feedback (what he should have built). Position: add Week 1 concept-only outreach before Sprint 0 begins.
- [ ] **D139 DECISION NEEDED:** Louis prepares 5-question problem-framing script for expert-comptable conversations this week. Sprint 0 decisions informed by expert-comptable problem domain knowledge, not just founder assumptions.

**D140 CHALLENGED (TA-Pulse-0129):** Technical Architect challenges server-wins as offline sync fallback: silently annihilates artisan's offline edits (phone dies mid-write, no conflict UI, no error). Position: (A) full offline with field-level conflict detection + conflict UI (+3-5 days), or (B) view-only offline for Sprint 0.
- [ ] **D140 DECISION NEEDED:** Louis chooses offline scope: (A) view-only offline (browse cached, no offline editing, honest engineering), or (B) full offline editing with expo-sqlite + conflict UI (+3-5 days to Sprint 0). Gates Sprint 0 timeline.

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
- [ ] **D98 UPDATED:** Android-first as default (D92 updated). Marc has an Android phone — build for him first. iOS remains secondary polish phase. Week 1 poll validates split. If Android 65%+, iOS stays polish; if iOS majority, reverse priority.
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
- [ ] **D82 UPDATED:** Primary GTM = SEO (problem-solution queries for devis/facture artisan) — THIS is where Marc actively searches for solutions
- [ ] **D82 UPDATED:** WhatsApp groups + Facebook = RETENTION/ENGAGEMENT, not acquisition. Role: brand recall, peer support for existing users, boca-à-oreille amplification layer. Stop treating as acquisition input.
- [ ] **D48 NEW:** Secondary GTM = specialist retailers who serve solo artisans (not generalist wholesaler chains)
- [ ] **D82 UPDATED:** Prescriber networks = highest-trust ACQUISITION channel — but through institutional digital comms (email, professional portals), not peer communities. Architect/property manager → artisan discovery happens in professional contexts, not WhatsApp groups.
- [ ] Wholesaler presence (Gedimat/Point P counter displays) = secondary brand-awareness only, not primary acquisition
- [ ] **D85 NEW:** Expert-comptable outreach = Week 1 (not Phase 2). Cold outreach to 5 expert-comptables in Caen area who service small BTP/construction clients. Ask: add to recommended software list for new artisan clients. Positioning: "Your artisan clients struggle with mentions légales and TVA compliance — this handles it correctly."
- [ ] **D85 UPDATED:** ~~GetApp and Capterra profiles claimed and optimized before launch — admin handlers search here first~~ **REMOVED.** Channel does not match D55 buyer journey. Admin handler validates Marc's choice, does not independently discover on comparison sites. Replaced by expert-comptable outreach (see below). (Debate 122)
- [ ] **D85 NEW:** Expert-comptable data-sync portal = Phase 2 (distinct from recommendation outreach). Phase 2 requires: real users + testimonials + accountant has seen it work.

### Sprint 0 Build (D54 + D71 + D74 + D81 + D84 + D100 — 5 Days, Supabase Backend)

**D100 (Debate 100) RESOLVED:** Sprint 0 backend = Supabase EU-hosted (Frankfurt). Fastify + Postgres + Coolify retired. Prior Postgres schema work transfers directly to Supabase. Eliminates 2-4h of Coolify setup + 15-20h of Fastify scaffold. React Native connects via Supabase JS client. **Self-hosted on OVH NOT recommended for v1** — adds ops complexity without compensating user benefit.

**D84 UPDATED:** Sprint 0 = 5.5-6.5 days (D90, per Technical Architect). D86 reversed D81 offline-first requirement. Offline-capable (optimistic UI + retry queues + AsyncStorage) + mentions légales + WhatsApp PDF + real device testing = 5.5-6.5 days IF pre-conditions met.

**D95 NEW (Challenge from Technical Architect):** D90's parallelization assumption is organizational (two teams) not individual (solo dev). Realistic solo dev estimate: 7-8 days unless specific pre-conditions are confirmed. Three independent risks: (1) parallelization is organizational fiction for solo dev — adds +1 day, (2) mentions légales = legal research not template engineering — adds +0.5-1 day, (3) integration underbudgeted — adds +0.5 day.
- [ ] **D95 CONFIRM before committing to 5.5-6.5 days:** Confirm Louis has pre-researched mentions légales legal text for all 4 client types. If not pre-researched: add 0.5-1 day to Sprint 0 OR defer mentions légales to Sprint 1 with plain text placeholder.
- [ ] **D95 SCOPE CUTS:** Three cuts make 5.5-6.5 days achievable without pre-conditions: (1) defer mentions légales to Sprint 1 (plain text placeholder), (2) defer AsyncStorage to Sprint 1 (online-only), (3) single client type in Sprint 0. Without cuts: accept 7-day timeline.
- [x] **D95 RESOLVED (FINAL — Debate 108):** Sprint 0 = 5 days (target) with pre-conditions confirmed. 6.5 days (floor) without pre-conditions. Non-negotiable: TVA arrondi commercial, sequential numbering. Cut first: mentions légales plain text placeholder, then AsyncStorage (online-only). Pre-sprint gates: (1) Louis shows 4 written mentions légales templates, (2) Louis shows Supabase project dashboard. Do not start sprint without both confirmed.
- [ ] **D96 NEW:** Conversion trigger = first paid facture (hard gate). Secondary soft trigger: 3 sent devis with zero paid factures → gentle upsell prompt. NOT "first sent devis" as primary trigger.
- [ ] **D100 CONFIRMED:** Supabase EU-hosted (Frankfurt) — sign up at supabase.com, select EU region. 10-minute setup. Self-hosted on OVH NOT recommended for v1 (reintroduces infra complexity, marginal cost saving, no user-facing benefit). Revisit at €5k/month revenue.
- [ ] **D100 POST-LAUNCH:** At 50 paying customers: evaluate self-hosted Supabase migration. Track: Supabase bill, OVH VPS load, ops time spent. If Supabase bill >€100/month AND OVH VPS has headroom → migrate.
- [ ] **D100 DATA PORTABILITY:** Ensure PDF export works well before any infrastructure migration conversation. French artisan data trust = "can I get my data out" not "where does it live."
- [ ] **D81 NEW:** Sprint 0 = offline-capable (optimistic UI + retry queues). WatermelonDB/expo-sqlite deferred to v1.2. Supabase handles auth, storage, realtime.
- [ ] **D121 NEW — Sprint 1b gate:** Replace expo-print ephemeral PDFs with Supabase Storage blob + `documents` table + PDF URL in API response. Legal compliance prerequisite for Phase 2 (expert-comptable data-sync, D72). Budget 2-3 days. Not optional.
- [ ] **D121 NEW — Legal labeling:** Sprint 0 PDF is a prototype document with no legal value. Add inline code comment and Sprint 0 handoff doc note: "WhatsApp share only — not an accounting record." Artisans must not believe their invoices are legally stored.
- [ ] **D74 RESOLVED:** Sprint 0 scope: client.type enum (4 values) + mentions légales template engine (Handlebars/Nunjucks, 4 client-type templates, devis-only). Sprint 2 adds 8 combinations.
- [ ] **D74 RESOLVED:** Auth: Supabase auth (email/password). API key replaces JWT per D78.
- [ ] **D74 RESOLVED:** `devis.status TEXT DEFAULT 'draft'` added in Sprint 0 schema (30 min). State machine = Sprint 1.
- [ ] **D54 RESOLVED:** TVA arrondi commercial calculator: `Math.round(v * 100) / 100`. No BOFiP lookup required.
- [ ] **D71 RESOLVED:** Mentions légales = 4 templates (devis × client type). 8 combinations (devis + facture) = Sprint 2 scope.
- [ ] **D83 NEW:** Push notification infra + nightly aggregation job added to Sprint 0 scope. Server computes financial snapshot nightly. Push at 8pm Paris. Free tier gets daily notification (limited depth). €29 tier gets full snapshot + in-app drill-down.
- [ ] **D84 UPDATED:** 5.5-6.5 day Sprint 0 achievable if pre-conditions met (D95) AND Supabase replaces Fastify+Postgres+Coolify (D100). Mentions légales retained. If timeline pressure: drop mentions légales (defer to Sprint 1), use plain text WhatsApp share instead of PDF.

### Pricing (D5 + D59 + D75 + D77 — €29 Single Price Point)
- [x] **D75 UPDATED (Debate 77):** "Membre fondateur" framing KILLED. Discount framing trains users to wait for promotions. Replaced with "Accès Fondateur" — relationship benefits without price anchoring.
- [x] **D75 UPDATED (Debate 77):** Price escalation (€29 founding → €39 standard → €49 professional) KILLED. Single €29/month for everyone, forever. No tiers.
- [x] **D75 UPDATED (Debate 77):** "First 50 slots" urgency KILLED. Scarcity signal = Louis's limited personal onboarding capacity (direct WhatsApp access, 30-min call), not arbitrary slot count.
- [x] **D75 UPDATED (Debate 77):** 4 benefits retained, reframed as relationship benefits (not price benefits): (1) named in app credits, (2) direct WhatsApp to Louis, (3) roadmap vote, (4) monthly priority vote. No locked price benefit.
- [x] **D75 RESOLVED:** Value anchor: "Moins d'une heure de main d'œuvre par mois." Trust signals required BEFORE €29 appears on landing page: (1) at least one specific beta testimonial, (2) concrete social proof number, (3) founding member framing with explicit benefits.
- [x] **D59 RESOLVED:** SEPA direct debit — evaluate Stripe SEPA integration (French artisans skeptical of credit card subscriptions).
- [x] **U15 (Debate 101) RESOLVED:** Founding member offer ELIMINATED. No lifetime deal. No founding/access tier. No "50 places" scarcity. Replace "Accès Fondateur" with "Support Prioritaire" — relationship benefits (direct WhatsApp to Louis, roadmap vote, named credits), not price discount. Single €29/month everywhere.
- [ ] **Landing page pricing copy:** Single €29/month. No founding tier. Language: "Essayez gratuitement. Quand vous êtes prêt, c'est €29/mois. Louis répond sur WhatsApp en moins de 24h."
- [x] **D99 RESOLVED:** Flat €29/month + €260/year annual billing at launch. Per-devis (€1.50/devis, cap €29) deferred to v1.2. Annual billing solves seasonality without per-devis conversion-moment friction. Revisit per-devis in v1.2 after: (1) real user data on seasonality patterns, (2) conversion architecture validated with flat €29, (3) billing integration mature enough for per-transaction charging.

### Free Tier + Conversion (D43 + D46 + D63 + D70 + D76 + D83)
- [ ] **D76 RESOLVED:** "Better Free Tier" trap named — every Free tier improvement without a conversion trigger makes the product harder to monetize. Document this risk.
- [ ] **D96 RESOLVED:** Conversion trigger = first paid facture (hard gate). "Votre facture pour [Client] a été payée — voulez-vous continuer à suivre vos paiements avec nous?" Secondary: 3 sent devis + zero paid factures → gentle upsell prompt.
- [ ] **D76 RESOLVED:** 80% "vous êtes presque à votre limite" notification DEPRECATED. Replace with accepted-devis milestone notification.
- [ ] **D76 RESOLVED:** Free tier = document archive (acquisition). €29 tier = financial snapshot + automatic relances on accepted devis (conversion). These are different jobs, not sequential tiers.
- [ ] **D63 RESOLVED:** Document archive = PRIMARY Free tier value. Financial snapshot (outstanding accepted devis, pipeline value, automatic relances) = €29 tier conversion trigger.
- [ ] **D70 RESOLVED:** Financial snapshot content: "Vous avez €X en devis acceptés en attente de paiement" — not a dashboard, a pipeline nerve center.
- [ ] **D83 UPDATED:** Situation financière = server-computed push notification at 8pm Paris (not in-app dashboard). The "soir ritual" is resolved: push arrives at 8pm, his natural admin time. Server aggregation ensures fresh data even for users offline for days. Free tier gets daily notification; €29 tier gets full snapshot + in-app drill-down.

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

*Last updated: 2026-03-30T15:59*

## New from Pulse 2026-03-30T15:59

### Reopened (D2, D54):
- **D2 (Sprint 1 timeline):** REOPENED — Product Strategist argues 2-week Sprint 1 contains 13-18 days of work (client file, TVA math engine, sequential numbering, RN devis UI, PDF+mentions légales, WhatsApp sharing + integration testing). 10 days available. Sprint 0 compression creates Sprint 1 debt. Needs real work breakdown.
- **D54 (TVA rounding):** REOPENED — Technical Architect argues arrondi arithmétique vs bancaire was never confirmed with BOFiP or French accountant. €1/invoice discrepancy × 50/month × 12 months = €600/year, × 3-year audit window = €1,800 in potential dispute. Sprint 0 must include explicit algorithm validation step before calculator is written.

### Challenged assumptions this pulse:
1. Sprint 1 = 2 weeks (Product Strategist challenged: 13-18 days estimated vs 10 available — structural timeline risk)
2. TVA per-line = "a formula" (Technical Architect challenged: arrondi arithmétique vs bancaire algorithmically distinct with real compliance stakes)

### New action items from this pulse:
- [ ] **D2 NEW:** Break down Sprint 1 into real work units before committing to 2-week timeline. Two options: (A) Split into Sprint 1a (client file + devis creation UI) + Sprint 1b (PDF + WhatsApp + TVA math), or (B) Accept 3-week Sprint 1 and update roadmap. Sprint 2 cannot start on time if Sprint 1 slips.
- [ ] **D54 NEW:** Sprint 0 definition of done must include: confirm TVA rounding algorithm via BOFiP instruction (BOI-TVA-LIQ-20) or consultation with French accountant. Two candidate implementations ready to plug in.
- [ ] **D54 NEW:** Validate sequential numbering requirements for devis specifically — gapless numbering is legally required for factures, but is it required for devis? If not, Sprint 0 numbering engine scope can be reduced.

### Note: Growth agent failed (401 auth — GLM model unavailable). Would have challenged D49 "Digital first" GTM — is WhatsApp/Facebook where Marc discovers tools or just socializes? Habitual communication habitat ≠ discovery pathway.

---

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

---

*Last updated: 2026-03-30T16:31*

## New from Pulse 2026-03-30T16:17 — Three Resolved

### Resolved (D2, D54, U15):
- **D2 (Sprint 1 timeline):** RESOLVED — Sprint 1a (Days 1-5: client file + devis flow) + Sprint 1b (Days 6-10: PDF + mentions légales + sharing + polish). Parallelization of backend and mobile on PDF endpoint recovers 3-5 days. Sequential numbering is 1 day, not 2. Viable 2-week sprint.
- **D54 (TVA rounding):** RESOLVED — arrondi commercial is the standard (not arithmétique vs bancaire binary). `Math.round(v * 100) / 100` is the Sprint 0 default. Audit risk is €30-80/year, not €600. No BOFiP lookup required.
- **U15 (Discovery location):** RESOLVED — wholesaler location retired. Revised Phase 1: workshop/job site via warm network introduction. Alternative: Facebook groups / WhatsApp clusters. Phase 1 now has explicit location, access method, and observable signals.

### Challenged assumptions this pulse:
1. Sprint 1 is 13-18 days — Technical Architect challenged: sequential waterfall assumption hides parallelization. PDF can run parallel to UI if API contract defined Day 1.
2. TVA rounding is a binary choice between arrondi arithmétique and bancaire — Technical Architect challenged: it's arrondi commercial (round half up), the de facto French accounting standard.
3. "5 artisans at a wholesaler Saturday morning" is a viable Phase 1 location — Growth Strategist challenged: five failure modes (admin doesn't happen there, Saturday is hostile to research, selection bias, no psychological safety, 20 minutes is a fiction).

### New action items from this pulse:
- [ ] **D2 NEW:** Sprint 1a Days 1-5: client file + TVA engine + sequential numbering + devis UI (end-to-end). Sprint 1b Days 6-10: PDF generation + mentions légales variants + WhatsApp/email sharing + integration testing. Define API contract on Day 1 to enable parallelization.
- [ ] **D54 NEW:** Sprint 0 TVA calculator — implement with arrondi commercial: `const roundTVA = (v: number): number => Math.round(v * 100) / 100`. No BOFiP lookup required.
- [ ] **D54 UPDATED:** Sprint 0 definition of done — TVA calculator (Day 2), sequential numbering (Day 2), mentions légales renderer (Day 3). Compliance work is bounded and more tractable than previously estimated.
- [ ] **U15 NEW:** Phase 1 revised protocol — workshop/job site observation via warm network introduction (not wholesaler). Pre-work questions via WhatsApp before visiting. 30-45 min silent observation. Red flags: performed demo, can't show real workflow, tries to sell you something.
- [ ] **U15 NEW:** Alternative Phase 1 — Facebook groups / WhatsApp clusters (asynchronous observation of admin pain conversations). Zero-friction qualitative research without physical presence.

## New from Pulse 2026-03-30T16:31 — Three Reopened

### Reopened (D63, D64, D55):
- **D63 (Free tier pull):** REOPENED — Product Strategist argues "situation financière" snapshot positions us as mini accounting software (Pennylane/Indy territory). The real Free tier value is the professional document archive (every devis/facture ever sent, organized by client). Snapshot moves to €29 tier or removed.
- **D64 (Sprint 0 timeline):** REOPENED — Technical Architect argues Sprint 0 = 5 days, not 3-4. The workstreams (TVA, mentions légales, sequential numbering) share a dependency chain through the line item schema and cannot run in parallel. Additionally, sequential numbering for devis is legally unnecessary (only factures require gapless numbering).
- **D55 (Expert-comptable GTM):** REOPENED — Growth Strategist argues expert-comptable outreach should be Phase 1, not Phase 2. Louis has an existing accountant — one warm conversation = immediate network access. The admin handler (the operational buyer) discovers tools through her accountant, not through WhatsApp artisan groups.

### New action items from this pulse:
- [ ] **D63 REVISED:** Primary Free tier pull = professional document archive (all sent devis/factures organized by client, searchable, beautiful), NOT financial snapshot
- [ ] Financial snapshot (outstanding devis aging, revenue vs last month) moved to €29 tier or removed from Free tier entirely
- [ ] **D63 NEW:** Design the "document archive" as the home screen of the Free tier — every devis/facture ever sent, tap to resend, tap to duplicate for new client
- [ ] **D64 REVISED:** Sprint 0 = 5 days (not 3-4). Sequential numbering removed from Sprint 0 scope (devis doesn't need it; it's a Sprint 2 facture concern).
- [ ] **D64 NEW:** Day 1: client.type enum + 4 mentions légales template files (plain text templates, not schema)
- [ ] **D64 NEW:** Day 2: line item schema + TVA rate field (5.5/10/20%) + TVA arrondi commercial calculator
- [ ] **D64 NEW:** Day 3: Devis document model (minimal — no facture yet, no numbering)
- [ ] **D64 NEW:** Days 4-5: Fastify REST API scaffold + JWT auth + CRUD endpoints for React Native integration
- [ ] **D55 REVISED:** Expert-comptable outreach moved from Phase 2 to Phase 1 — parallel track with digital channels
- [ ] **D55 UPDATED:** U12 expert-comptable GTM playbook — document what to say, what materials to leave, how to position for admin handler audience — action this week
- [ ] **D55 NEW:** Louis asks his own expert-comptable this week: (1) do you recommend software to clients? (2) would you demo? (3) can you intro 2-3 colleagues?
- [ ] **D55 NEW:** Target: 3 expert-comptables referencing 50+ sole trader clients by Month 2
- [ ] **D55 NEW:** Remove "6-18 month build" framing — warm outreach via existing accountant is not the same as cold outreach



---

## New from Pulse 2026-03-30T16:44 — Three Resolved

### Resolved (D70, D71, D72):
- **D70/D63 (Free tier pull):** RESOLVED — professional document archive = PRIMARY Free tier value. Every devis/facture sent, organized by client, full-text searchable, beautiful PDF renderer. Financial snapshot (outstanding devis aging, revenue vs last month) moves to €29 tier. Competitive mispositioning avoided: Pennylane/Indy do financial dashboards better.
- **D71/D64 (Sprint 0):** RESOLVED — Sprint 0 = 5 days (not 3-4). Dependency chain confirmed: client.type → mentions légales → line item schema → TVA calculator. Sequential numbering removed from Sprint 0 scope — devis doesn't legally require it; it's a Sprint 2 (factures) concern. Sprint 0 scope: Fastify + Postgres, client.type + mentions légales + TVA engine + Devis document model + REST API scaffold.
- **D72/D55 (Expert-comptable):** RESOLVED — expert-comptable outreach moves from Phase 2 to Phase 1. Louis initiates this week via existing accountant. One warm conversation = access to professional network of 30-50 SMB clients. Admin handler (operational buyer who converts) discovered through accountant referral, not artisan WhatsApp groups. U12 to be actioned immediately.

### Action items from this pulse:
- [ ] **D70 NEW:** Design the professional document archive as the Free tier home — every sent devis/facture, organized by client, searchable. Primary pull mechanism.
- [ ] **D70 NEW:** Financial snapshot (outstanding devis aging, revenue vs last month) moved to €29 tier feature list.
- [ ] **D71 NEW:** Sprint 0 = 5 days. Sequential numbering removed entirely from Sprint 0. Fastify + Postgres only. Days 1-2: client.type + mentions légales + line item schema + TVA arrondi commercial engine. Days 3-4: Devis document model. Days 4-5: REST API scaffold + JWT auth for React Native integration.
- [ ] **D72 NEW:** U12 (expert-comptable playbook) — initiate this week. Louis asks his accountant: (1) do you recommend software to clients? (2) would you demo? (3) can you intro 2-3 colleagues? Target: 3 expert-comptables referencing 50+ sole trader clients by Month 2.
- [ ] **D72 NEW:** Expert-comptable GTM = Phase 1 parallel track alongside digital channels. Warm outreach timeline is days, not months.

---

## New from Pulse 2026-03-30T16:57

### Three New Debates (Technical Architect, Growth Strategist, Product Strategist)

**Debate 73 (Technical Architect):** Sprint 0 5-day estimate challenged on three independent grounds:
1. JWT auth is 2-3 days (not 0.5-1 day) — scaffold ≠ production auth system
2. Mentions légales require 8 combinations (4 templates insufficient) — template engineering required
3. "Minimal" Devis model missing status enum guarantees Sprint 1 retrofitting mid-development

**Revised Sprint 0 estimate: 7 days OR 5 days with reduced scope (auth bypass + 4 template combos + status enum).**

**Debate 74 (Growth Strategist — D43/D46/D51/D70):** Free tier conversion framework challenged — the Product Strategist keeps winning debates by improving Free tier quality, which reduces conversion pressure. No specific conversion mechanism has been defined for "how a Marc at 4/5 devis decides to pay €29." D43/D46/D51/D70 REOPENED.

**Debate 75 (Product Strategist — D5/D59):** €29 price anchor challenged:
1. Wrong input variable: artisan billing rate €30-45/h (not €50-80/h), so €29 = 50min not 1h
2. €29 for unknown product vs established competitors (Tolteck €19, Obat €17) creates trust barrier before Free tier proves value
3. Lifetime €29 lock creates pricing ceiling that prevents future increases

### Action Items from this pulse:
- [ ] **Debate 73 UPDATED:** Sprint 0 revised to 7 days OR 5 days with auth bypass (API key temp) + 4 mentions légales combos (factures only) + devis.status enum in Sprint 0 schema
- [ ] **Debate 73 NEW:** JWT auth deferred to Sprint 1 — use API key bypass or no-auth for Sprint 0 mobile integration. Fastify JWT scaffold can ship in Sprint 0 but production auth (refresh rotation, Keychain storage, refresh queue) ships Sprint 1.
- [ ] **Debate 73 NEW:** Mentions légales scoped to 4 most-critical combinations (particulier facture, professionnel français facture, professionnel UE facture, professionnel hors-UE facture). Devis inherits from client type only. Full 8-combination system deferred to Sprint 2.
- [ ] **Debate 73 NEW:** Devis status enum (draft/sent/accepted/rejected/expired) added to Sprint 0 schema — 30min of schema work that saves Sprint 1 migration.
- [ ] **Debate 74 NEW:** Define specific conversion mechanism — what is the exact moment/condition when Marc decides to pay €29? Not "better Free tier" — a specific trigger. If it can't be defined, the conversion model is broken.
- [ ] **Debate 75 UPDATED:** Recalibrate value anchor to €35/h (realistic artisan rate). Kill lifetime €29 lock. Replace with "€19 early access for first 3 months → €29 standard."
- [ ] **Debate 75 NEW:** Add social proof signals to landing page BEFORE €29 price appears (testimonials, expert-comptable mention, usage numbers) — reduce price credibility gap for unknown product.

---

## New from Pulse 2026-03-30T17:17 — Three Specialist Debates Resolved

### Resolved (D74, D75, D76):
- **D74 (Sprint 0 timeline):** Technical Architect defended 5-day estimate with scope clarifications. JWT Sprint 0 scope = contract + stubs (0.5-1 day). Full auth = Sprint 1. Mentions légales = 4 templates (devis only; 8 = Sprint 2). `devis.status TEXT DEFAULT 'draft'` added in Sprint 0 (30 min). No timeline extension. D71 REFINED.
- **D75 (Pricing anchor):** RESOLVED by Debate 77 — "Membre fondateur" framing KILLED (discount signal wearing relationship language). Price escalation (€29 founding → €39 standard → €49 professional) KILLED. Single €29/month for everyone. "Accès Fondateur" replaces "Membre fondateur" — relationship benefits (direct WhatsApp to Louis, named in app, roadmap vote) without price anchoring. Scarcity = Louis's limited personal onboarding capacity, not "first 50 slots." D5/D59/D75 UPDATED.
- **D76 (Free tier conversion):** Growth Strategist named "Better Free Tier" trap. Conversion trigger = first accepted devis (not 80% limit notification). Free tier = document archive (acquisition). €29 tier = financial snapshot + automatic relances (conversion). 80% notification deprecated. D43/D46/D51/D63/D70 REFINED.

### New Action Items from this pulse:
- [ ] **D74 NEW:** Sprint 0 Day 1 — `client.type` enum (4 values) + mentions légales template engine (Handlebars/Nunjucks, 4 client-type templates). Devis × client type only. Sprint 2 adds 4 more for factures.
- [ ] **D74 NEW:** Sprint 0 JWT = contract + stubs + `@fastify/jwt` config (0.5-1 day). Full auth (Keychain, refresh queue, logout) = Sprint 1 deliverable.
- [ ] **D74 NEW:** Sprint 0 schema: `devis.status TEXT DEFAULT 'draft'` — 30 min. State machine (valid transitions, expiration cron) = Sprint 1.
- [ ] **D75 NEW:** Trust signals required BEFORE €29 appears on landing page: (1) specific beta testimonial, (2) concrete social proof number ("500+ devis envoyés"), (3) "Accès Fondateur" framing with 4 relationship benefits (NOT price benefits).
- [ ] **D75 UPDATED (D77):** Price escalation KILLED. Single €29/month. No founding/standard/professional tiers. "Accès Fondateur" is a relationship program, not a discount program.
- [ ] **D76 NEW:** Accepted-devis conversion notification: "Votre devis pour [Client] a été accepté. Passez à €29 pour suivre ce qui vous est dû." — fires on first `devis.status = accepted`, not on 80% limit proximity.
- [ ] **D76 NEW:** €29 tier delivers: (1) financial snapshot ("vous avez €X en devis acceptés en attente de paiement"), (2) automatic email relances at 14/30/60 days on accepted devis. Not a dashboard — a pipeline nerve center.
- [ ] **D76 NEW:** 80% "vous êtes presque à votre limite" notification DEPRECATED — replace in product spec with accepted-devis milestone trigger.

---

## New from Pulse 2026-03-30T17:29 — Three Open Debates

### Open (D77, D78, D79):
- **D77 (Membre fondateur):** OPEN — Product Strategist argues "Membre fondateur" framing creates price anxiety by signaling €29 is promotional, not the real price. Alternative proposed: "Essai gratuit 14 jours, puis €29/mois. Prix définitif. Sans engagement."
- **D78 (JWT vs API key):** RESOLVED — API key auth wins. See resolved items below.
- **D79 (Expert-comptable reframed):** OPEN — Growth Strategist argues Louis's accountant = validation asset, not sales channel. Phase 1 = validation ("can I show you and get your reaction?"). Phase 2 = referrals (only after product has real users + testimonials).

### New Action Items from this pulse:
- [x] **D77 RESOLVED:** Kill "Membre fondateur" A/B test — framing is rejected. Single €29 price, relationship program only.
- [x] **D77 RESOLVED:** Founding member language REMOVED from onboarding — replaced with "Accès Fondateur" (relationship framing, no price signal).
- [x] **D77 RESOLVED:** Scarcity signal = Louis's limited personal onboarding capacity (direct WhatsApp access), not arbitrary slot count or seats remaining.
- [x] **D78 RESOLVED:** Replace JWT with API key auth in Sprint 0 — `artisan.api_key UUID DEFAULT gen_random_uuid()` in schema. Sprint 0 auth deliverable: `POST /api/auth/verify` + Expo SecureStore stub, ~2 hours. JWT re-evaluate for v2 only if multi-user confirmed. (Debate 78)
- [x] **D79 RESOLVED:** Expert-comptable = Phase 1 validation asset, not GTM channel. U12 split: U12a (validation script — action this week) + U12b (referral script — action Phase 2). Louis's meeting: show flow → get reaction → ask what would make them comfortable recommending. NOT: ask for referrals. Phase 2 triggers: real users + testimonials + accountant has seen it work. (Debate 79)

## New from Pulse 2026-03-30T18:27

### Resolved (D81, D85, D88):
- **D81 (Offline-first):** REVERSED — Sprint 0 = offline-capable (optimistic UI + retry queues + AsyncStorage cache). WatermelonDB/expo-sqlite deferred to v1.2. Saves 3-5 sprint days. (Debate 86)
- **D85 (Expert-comptable outreach):** PARTIALLY REVERSED — Week 1: claim GetApp/Capterra profiles only. Expert-comptable outreach moves to Week 4-6 with prerequisites: 10-20 active beta users, 1-2 testimonials, production-validated mentions légales, sample BTP devis for review. (Debate 87)
- **D88 (8pm notification):** REFINED — Fixed 8pm notification REPLACED with: configurable notification window (morning/midday/evening, user chooses in onboarding) + event-driven triggers (devis pending 3+ days, facture 15+ days unpaid) + timezone awareness + 10pm night guardrail. (Debate 88)

### New Action Items from this pulse:
- [ ] **D81 NEW:** Sprint 0 = offline-capable. Implement optimistic UI (immediate local feedback, background server sync), retry queues with exponential backoff, AsyncStorage cache for last 10 clients/recent devis. No WatermelonDB until v1.2.
- [ ] **D81 UPDATED:** Sprint 0 timeline reverts to 5-7 days (was 8-10 with offline-first). Those recovered 3-5 days go to devis flow and real device testing. NOTE: D90 further updated to 5.5-6.5 days — see D95 challenge re: solo dev parallelization.
- [ ] **D85 UPDATED:** Expert-comptable outreach DEFERRED to Week 4-6. Prerequisites: 10-20 active beta users, 1-2 testimonials, production mentions légales, sample BTP devis. Week 1: claim GetApp/Capterra profiles only.
- [ ] **D88 NEW:** Add notification preference to onboarding flow — "Quand voulez-vous recevoir vos rappels?" Morning / Midday / Evening. Default to user's stated preference.
- [ ] **D88 NEW:** Replace daily 8pm financial digest push with event-driven triggers: (1) devis unanswered 3+ days → "Ce devis attend une réponse depuis 3 jours", (2) facture unpaid 15+ days → "Cette facture est impayée depuis 15 jours"
- [ ] **D88 NEW:** Timezone guardrail — push notification send time adjusts for user's declared timezone (not "Paris time" for all of France)

## New from Pulse 2026-03-30T18:45 — Three Specialist Debates Resolved

### Resolved (D89, D90, D91):
- **D89 (Situation financière notification):** RESOLVED — configurable digest window KILLED. Notification fires ONLY on first accepted devis event. "Votre devis pour [Client] a été accepté — votre situation financière est désormais complète." This IS the D76 conversion trigger. Recurring digest for dormant Free users kept as separate "stay in touch" mechanism, not primary notification. (Debate 89)
- **D90 (Sprint 0 timeline):** RESOLVED — Sprint 0 = 5.5-6.5 days (updated from 8-10). D86 (offline-capable) + D74 (API key auth) eliminate the sequential dependency that drove the 8-10 day estimate. Backend and mobile run in parallel from Day 1 once API contract is defined. (Debate 90)
- **D91 (Expert-comptable validation vs referral):** RESOLVED — U12 split confirmed. U12a (validation, Week 1): Louis books his own expert-comptable this week, shows devis flow, gets feedback. No prerequisites. U12b (referral, Week 4-6): cold outreach to 5 colleague expert-comptables with testimonials and production-validated mentions légales. (Debate 91)

### Challenged assumptions this pulse:
1. D88's configurable notification window is meaningful for €29 tier conversion (Product Strategist challenged: digest creates noise, event creates signal — D76's "first accepted devis" is the only notification that matters)
2. 8-10 day Sprint 0 estimate remains correct after D86/D74 scope reductions (Technical Architect challenged: parallelization unlocks 5.5-6.5 days)
3. D85/D87's "10-20 beta users before expert-comptable outreach" applies to validation conversations (Growth Strategist challenged: validation ≠ referral, prerequisites apply to referral only)

### New Action Items from this pulse:
- [ ] **D89 NEW:** Remove configurable notification window from onboarding. The €29 conversion notification fires ONLY on first accepted devis. Message: "Votre devis pour [Client] a été accepté. Passez à €29 pour suivre ce qui vous est dû." One notification, one moment, one ask.
- [ ] **D89 NEW:** Free tier dormant user "stay in touch" push — if no accepted devis in 14 days, gentle "tout va bien?" check-in. Below the conversion trigger line. No upgrade pitch.
- [ ] **D90 NEW:** Sprint 0 timeline = 5.5-6.5 days. Backend and mobile run in parallel from Day 1. API contract (OpenAPI spec or shared types) must be defined by end of Day 1 to unlock parallelization.
- [ ] **D90 NEW:** Sprint 0 Day 1 morning: define Fastify API contract with mobile team. Then backend builds to contract, mobile builds to contract in parallel.
- [ ] **D91 NEW:** U12a (validation — THIS WEEK): Louis books his own expert-comptable. Ask: "Can I show you the devis flow and get your honest reaction?" No testimonials, no beta users, no prerequisites. Just a flow demo and feedback request.
- [ ] **D91 NEW:** U12b (referral — Week 4-6): cold outreach to 5 colleague expert-comptables. Prerequisites: 10-20 active beta users, 1-2 testimonials, production-validated mentions légales. Frame: "We have artisans in your area using this — would you like to see how it handles BTP client mentions?"
- [ ] **D91 UPDATED:** D85/D87 partially superseded by D91. GetApp/Capterra = Week 1 (unchanged). Expert-comptable validation = Week 1 (Louis's own, no prerequisites). Expert-comptable referral = Week 4-6 (with prerequisites).

## New from Pulse 2026-03-30T19:00 — Three Specialist Debates

### Resolved (D92, D93, D94):
- **D92 (App Store launch):** iOS-first, Android Month 2. Validate platform split in Week 1 via geo-targeted Facebook/Instagram poll in Caen + competitor review count analysis. If Android majority confirmed → launch Android simultaneously or first. Android Play Store moderation risk is real for B2B finance apps.
- **D93 (Day 1 onboarding):** Guided Creation Flow. 5-minute sequence: (1) full-screen "create your first devis in 60 seconds" intro card, (2) create first client via phone contact import or name/phone fallback, (3) create and send first devis via WhatsApp/email native share. Time-to-first-document is the primary retention driver. Position B (Explore First) is higher-risk for this persona.
- **D94 (GetApp/Capterra):** Claim Week 1 (D85 confirmed). Publish Week 3-4 once screenshots, accurate pricing (Free + €29), feature matrix, and 2-3 seed reviews are ready. Empty skeleton profile is worse than no profile. Expert-comptable referral channel (D87) generates organic review accumulation in Week 4-6.

### Challenged assumptions this pulse:
1. Platform split is 50/50 (Mobile Growth challenged: population-level data doesn't apply to this B2B persona; actual split needs validation)
2. "Explore First" is the safer onboarding choice (Product Strategist challenged: empty state leads to abandonment; time-to-first-document is the retention driver)
3. GetApp/Capterra should be live at launch (Growth challenged: empty profile is worse than no profile; D85 conflated claiming with publishing)

### New Action Items from this pulse:
- [ ] **D92 NEW:** Week 1 platform validation — geo-targeted Facebook/Instagram poll in Caen ("What phone do you use for your business?" iOS/Android), €20-50 ad spend targeting 200+ artisans. Also: check 3-5 competitor App Store review counts (iOS vs Android) to infer platform split.
- [ ] **D92 NEW:** If geo-targeted poll shows 55%+ Android → reverse launch order or go simultaneous. Document the decision rule before Sprint 0 starts.
- [ ] **D93 UPDATED:** Guided Creation Flow is evening-only (10-15 min), not 5-min daytime task. Day 1 split: daytime = app install + home view orientation (job card, situation financière notification). Evening = Guided Creation Flow ("Vous avez 10 minutes? Créons votre premier devis ensemble."). The 5-minute daytime flow is unrealistic — artisan day has no focused 5-minute window.
- [ ] **D93 NEW:** Contact import is secondary, not primary. Manual entry (name + phone) is the happy path. Phone contacts rarely contain solo artisan client data (kept in WhatsApp). Import UI must show "Entrez le nom et téléphone" immediately, not after a failed import.
- [ ] **D93 UPDATED:** 5-minute claim on landing page is unverified. Verify in real conditions (mid-range Android, gloves, sunlight, one interruption) before using it. If flow takes 10-15 minutes, update the landing page claim.
- [ ] **D93 NEW:** Flow must be interruption-safe — every step saves progress locally. If Marc gets a client call mid-flow, he returns to exactly where he left off.
- [ ] **D93 NEW:** Resolve D83/D93 internal inconsistency — D83 rejected 8pm notification ("too presumptuous about daily rhythm"). D93 Guided Creation implicitly requires evening. Explicit distinction: evening notification (D83) = too presumptuous. Evening Guided Creation onboarding = appropriate framing for when a focused moment exists. The evening moment is a user choice, not a product assumption.
- [ ] **D94 NEW:** GetApp + Capterra — Week 1: claim and verify ownership, enter basic company data, set to draft/private. Do NOT publish yet.
- [ ] **D94 NEW:** Week 2-3: add 3-5 real product screenshots (devis creation, facture, document archive), accurate pricing ("Free plan. Pro: €29/month"), French-language description written for artisan audience, feature checklist matching MVP.
- [ ] **D94 NEW:** Week 3-4: publish profile once 2-3 seed reviews from beta/early users exist. Ask founding members to leave reviews as part of activation flow.
- [ ] **D94 NEW:** Week 4-6: expert-comptable outreach (D87) generates organic review accumulation — ask satisfied accountants to leave reviews on GetApp/Capterra.


## New from Pulse 2026-03-30T19:15 — D76/D89 Challenge: First Accepted Devis Trigger

### REOPENED (D76/D89):
- **D76/D89 (Conversion trigger):** Growth Strategist challenged "first accepted devis" as the conversion trigger. Three-step chain (create devis → formal acceptance → status update) fails regularly: (1) Marc doesn't send formal devis to repeat clients (60-70% of his work), (2) French BTP verbal agreements mean client "accepts" verbally without a record, (3) Marc may never mark status as accepted. Estimated trigger fires on ~5% of new-client situations, zero for repeat-client situations. Proposed replacement: "first sent devis" as primary conversion trigger. "First accepted devis" becomes a secondary €29 tier notification (financial snapshot trigger), not the primary Free → €29 conversion trigger.

### New Action Items from this pulse:
- [ ] **D76/D89 NEW:** Conversion trigger changed from "first accepted devis" to "first sent devis." Notification fires when Marc sends his first devis ever: "Votre devis a été envoyé. Passez à €29 pour suivre vos clients, vos devis acceptés, et vos factures impayées." No client acceptance required.
- [ ] **D76/D89 NEW:** "First accepted devis" becomes the financial snapshot trigger for €29 tier (D70: "vous avez €X en devis acceptés en attente de paiement"), not the primary Free → €29 conversion trigger.
- [ ] **D76/D89 NEW:** UX forcing function: 24h after sending a devis, prompt "Client accepted? Tap yes → we update the status." This maintains accepted-devis data for the €29 tier financial snapshot without making it the conversion trigger.
- [ ] **D76/D89 NEW:** €29 tier differentiation: client limit (10 on Free vs unlimited on €29), relances, financial snapshot. First sent devis fires the conversion ask; accepted-devis data enriches the €29 tier experience.
- [ ] **D76/D89 NEW:** Landing page + onboarding messaging update: "Créez et envoyez votre premier devis en 5 minutes" — the first sent devis moment is the core value moment, not the accepted-devis moment.

## New from Pulse 2026-03-30T19:43 — Three Specialist Debates

### Reopened (D76/D89, D92, D95):
- **D76/D89 (Conversion trigger):** REOPENED again — Product Strategist argues "first sent devis" fires too early (no value proven yet). Proposes "first paid facture" as the conversion trigger (real value moment) + human WhatsApp check-in by Louis at Day 14 (actual conversion mechanism for French artisans).
- **D92 (Platform default):** REOPENED — Growth Strategist argues iOS-first is wrong default for French artisan persona (Android skews working-class trades). Proposes Android-first with Week 1 validation poll. "Business user = iPhone" is a Silicon Valley stereotype.
- **D95 (Sprint 0 timeline):** REOPENED — Technical Architect argues 7-8 day estimate conflates pre-sprint prep (legal research) with sprint work. If mentions légales templates are pre-researched this week (2h), Sprint 0 becomes 5 days.

### New Action Items from this pulse:
- [ ] **D96 NEW:** Conversion trigger restated — Product Strategist proposes "first paid facture" (not "first sent devis") as conversion trigger, because it fires when value is proven (money received), not when action is taken (devis sent). Push notification conversion model challenged — human WhatsApp check-in by Louis at Day 14 is the correct mechanism.
- [ ] **D96 NEW:** Day 14 human check-in: Louis sends WhatsApp to all active Free users — "Salut Marc, comment ça se passe ?" Not a sales pitch. A conversation. The conversion happens here, not via push notification.
- [ ] **D97 NEW:** Sprint 0 pre-work this week: Louis spends 2 hours researching and writing the 4 mentions légales templates (particulier, pro-français, pro-UE, pro-hors-UE). Sprint 0 then targets 5 days, not 7-8.
- [ ] **D98 NEW:** Week 1 platform validation poll: if Android majority (>55%) in Caen artisan sample → Android-first. If iOS majority → iOS-first. Don't assume iOS is the default for this persona.

## New from Pulse 2026-03-30T19:55 — Three Specialist Resolutions

### Resolved (D92, D95, D96):
- **D92 (Platform default):** RESOLVED — Android-first is the correct default for French artisan persona. Marc has an Android phone; working-class trades skew Android. iOS-first was a Silicon Valley stereotype. Week 1 poll confirms or denies. Expo builds handle both — Android-first is sequencing, not a technical constraint.
- **D95 (Sprint 0 timeline):** RESOLVED — 5 days IF Louis writes mentions légales templates before sprint (2h pre-sprint, pre-sprint dependency). Pre-condition is the gate. Coordination risk (two-person buffer) ≠ throughput risk (solo dev). Sprint 0 tasks are tightly scoped (TVA = formula, mentions légales = template files). If templates not pre-written: accept 6.5 days.
- **D96 (Conversion trigger):** RESOLVED — Conversion trigger = first paid facture (hard gate). Secondary soft trigger: 3+ sent devis with zero paid factures → gentle upsell prompt. "First sent devis" alone is insufficient — it rewards activity, not value. Human WhatsApp check-in by Louis at Day 14 remains the actual conversion mechanism.

### New Action Items from this pulse:
- [x] **D92 RESOLVED:** Android-first as default. Week 1 poll validates. If Android 65%+, iOS stays polish phase. Update mobile build sequencing in Sprint 0 planning.
- [x] **D95 RESOLVED:** Sprint 0 = 5 days (gate: mentions légales templates pre-written). Update sprint planning.
- [x] **D96 RESOLVED:** Conversion trigger = first paid facture. Update conversion design spec.

*Last updated: 2026-03-30T19:55*

## New from Pulse 2026-03-30T20:08 — Three Specialist Debates

### Reopened (D4, D68, U15):
- **D4 (Backend architecture):** RESOLVED — Supabase EU-hosted (Frankfurt) wins. Fastify + Postgres + Coolify retired. Self-hosted on OVH NOT recommended for v1 (adds ops overhead without user benefit). See pulse-2040-architect.
- **D68 (Pricing model):** REOPENED — Product Strategist argues flat €29/month creates seasonal churn friction. Usage-based (€1.50 per devis, capped at €29) aligns payment with artisan cash flow reality and eliminates January payment friction.
- **U15 (Founding member offer):** REOPENED — Growth Strategist argues founding member pricing undermines credibility with risk-averse French artisans. "Membre fondateur" signals beta/unproven. €90 lifetime deal undercuts €29/month. Pure free trial is the correct launch mechanism.

### New Action Items from this pulse:
- [ ] **D99 NEW (D68 reopened):** Pricing model debate — evaluate usage-based model: €1.50 per devis sent, capped at €29/month. Does this better align with French artisan seasonal cash flows than flat €29/month? Does it affect the conversion trigger (first paid facture)?
- [ ] **D100 NEW (D4 reopened):** Architecture debate — evaluate Supabase self-hosted or EU-hosted for v1. Does the 5-day sprint constraint justify BaaS over custom Fastify? What is the real e-invoicing compliance timeline for Mini-CRM's scope?
- [ ] **D101 NEW (U15 reopened):** Founding member offer — kill founding member tier? Evaluate: does "membre fondateur" framing help or hurt credibility with 45-55 year old French artisans? Is pure free trial + €29/month the cleaner launch model?
- [ ] **D99/D100/D101:** Louis reviews these three reopened debates and makes resolution decisions before Sprint 0 begins. These affect core pricing, architecture, and launch strategy — all must be resolved before Sprint 0 spec is finalized.

*Last updated: 2026-03-30T20:08*

---

## New from Pulse 2026-03-30T20:40 — Three Resolutions (D92/D96/D99/D100 Resolved)

### Resolved (D92 REFLECTED, D96 UPDATED, D99 RESOLVED, D100 RESOLVED):
- **D100 (Supabase hosting):** RESOLVED — EU-hosted Supabase (Frankfurt) confirmed for v1 Sprint 0. Self-hosted on OVH NOT recommended (adds ops overhead without compensating benefit). Sign up at supabase.com, EU region, Day 1.
- **D92 (Platform default):** REFLECTED — Android-first direction confirmed. "Week 1 poll validates" REMOVED (wrong instrument, no early cohort without founding member offer). Replaced with install completion rate (≥50% in 48h) as Sprint 0 validation metric. D24 resolution gates Sprint 0 specificity.
- **D96 (Conversion trigger):** UPDATED — Limit-hit (5 active devis OR 10 clients) as hard gate. First paid facture = soft milestone prompt (celebration + upgrade offer), not hard gate. Billing trigger now aligned with conversion trigger.
- **D99 (Usage-based pricing):** RESOLVED (Implementation-Ready) — €1.50/devis, cap €29 at launch. Activates at conversion (limit-hit). Billing trigger and conversion trigger now aligned. Flat-rate alternative (€29 unlimited) offered at conversion moment.
- **D68 (Pricing model):** RESOLVED — Usage-based (€1.50/devis, cap €29) + flat-rate alternative (€29 unlimited). Seasonal cash flow benefit confirmed. Both options presented at conversion.

### New Action Items from this pulse:
- [x] **D100 RESOLVED:** EU-hosted Supabase (Frankfurt) — sign up at supabase.com, EU region. Self-hosted on OVH NOT recommended. Revisit at €5k/month revenue.
- [x] **D92 REFLECTED:** Install completion rate replaces Week 1 poll. Target: ≥50% of signups complete install within 48h.
- [x] **D96 UPDATED:** Limit-hit conversion (5 devis/10 clients). First paid facture = milestone prompt.
- [x] **D99 RESOLVED:** Usage-based billing (€1.50/devis, cap €29) at launch. Billing UI: two options at limit-hit: (A) pay-per-devis or (B) €29 unlimited. Default to A with note "most start with per-deavis, can switch anytime."
- [ ] **D92/D24 dependency:** D24 (PWA vs React Native) resolution gates Sprint 0 specificity on Android-first. If React Native → distribution sequencing (Play Store → App Store). If PWA → design priority + Android browser optimization.
- [ ] **Play Store review timeline:** Android B2B finance apps face Play Store moderation (3-5 days). Do NOT assume faster than App Store. Factor into iOS parity timeline.
- [ ] **Expert-comptable device audit (Week 1):** If primary acquisition channel is expert-comptable referrals, platform priority should follow referrer device split — not just end-user device. Quick WhatsApp poll to 5-10 contacts.

*Last updated: 2026-03-30T20:45*

---

## New from Pulse 2026-03-30T20:53

### Resolved (D83/D93, D106, D107):
- **D83/D93 (Evening onboarding contradiction):** RESOLVED — D83 (event-only notifications, no time-based triggers) and D93 (opt-in onboarding session) operate in different interaction contexts. Not contradictory when properly scoped. Notifications: imposed timing = bad. Onboarding: opt-in commitment = good.
- **D93 (Guided Creation timing):** UPDATED — "Evening-only" reframed as "focused 10-15 minute window" (most artisans find this in evening, not mandated). Bookable slot during Day 1 orientation. Async fallback available.
- **D106 (WhatsApp sharing):** RESOLVED — PDF attachment via native share sheet ships in Sprint 0. Placeholder attachment until Sprint 1b delivers proper PDF. WhatsApp Business API direct sending not viable in Sprint 0 (template approval takes weeks). Deep links = Sprint 1.
- **D107 (Document archive + conversion):** RESOLVED — Archive stays PRIMARY Free tier value (D70 confirmed). Three changes: (1) financial snapshot teaser in Free tier (count only), (2) upgrade prompt reframed as growth acknowledgment ("votre activité grandit"), (3) €29 visible as complete package. "Free forever" trap prevented by curiosity, not desperation.

### Challenged assumptions this pulse:
1. D83's rejection of evening notifications contradicts D93's requirement for evening-focused onboarding (Product Strategist resolved: separate notification context from onboarding context)
2. WhatsApp sharing requires PDF generation to be viable (Technical Architect resolved: native share sheet works with placeholder attachment, PDF = Sprint 1b)
3. Document archive creates retention without creating conversion pressure (Growth Strategist resolved: archive satisfies but doesn't convert without three specific design changes)

### New Action Items from this pulse:
- [ ] **D83/D93 NEW:** Guided Creation Flow — offer as bookable 10-15 minute slot during Day 1 orientation. Options: morning / midday / evening. Artisan chooses. No forced evening. Async fallback if no slot selected.
- [ ] **D83/D93 NEW:** Remove any notification that imposes a time-based schedule on artisans. Event-only triggers only (first accepted devis, limit-hit).
- [ ] **D106 NEW:** Sprint 0 sharing deliverable — React Native `Share` API with WhatsApp pre-selected. Placeholder attachment (text or basic PDF) until Sprint 1b. No WhatsApp Business API in Sprint 0.
- [ ] **D106 NEW:** Sprint 1b additions: server-side PDF generation (html-to-pdf via Edge Function), mentions légales per client type, WhatsApp preview card (OG tags on devis preview page).
- [ ] **D106 NEW:** Sprint 1+: universal deep links for devis (`minicrm://devis/123`), read receipts for €29 tier.
- [ ] **D107 NEW:** Free tier financial snapshot teaser — show count of pending/payed devis (no amounts). "Vous avez 3 devis en attente de réponse." The full amounts + aging = €29 tier only.
- [ ] **D107 NEW:** Upgrade prompt reframe — "Votre activité grandit. Avec le plan Pro, chaque client a son tableau de bord complet — devis en attente, paiements reçus, relances automatiques." Not "vous avez atteint votre limite" — growth acknowledgment with clear value.
- [ ] **D107 NEW:** €29 tier visibility — archive + financial snapshot + relances + unlimited + support = complete business tool. Show Marc what's missing from Free tier, don't just block him.
- [ ] **D107 NEW:** "Free forever" trap prevention — the upgrade prompt fires when Marc can see what he's missing, not when he's desperate. Curiosity > desperation as conversion mechanism.

*Last updated: 2026-03-30T20:53*

---

## New from Pulse 2026-03-30T21:13

### Reopened (D95, U7, D96/D104) — ALL RESOLVED in 21:27 Pulse:
- **D95 (Sprint 0 timeline):** REOPENED — Product Strategist argues 5-day estimate assumes parallelization that doesn't exist for a solo developer. U16 (mentions légales templates) is not started. Supabase signup is unconfirmed. Without both pre-conditions confirmed, realistic estimate is 6.5-7 days.
- **U7 (Domain deferral):** REOPENED — Growth Strategist argues "wait for guerrilla test" is structurally indefinite because test prerequisites (prototype + scheduled session) don't exist yet. Domain absence blocks expert-comptable outreach and GetApp/Capterra credibility. Fix: buy domain now (park it), defer brand decision.
- **D96/D104 (Conversion trigger):** RESOLVED (Debate 110) — Dual-path conversion. Path A (formal-devis): limit-hit OR first paid facture. Path B (verbal-agreement): 45 consecutive days active OR 7+ jobs logged OR 5+ active clients managed. Day 14 WhatsApp check-in applies to both archetypes.

### Challenged assumptions this pulse:
1. Sprint 0 can start today (Product Strategist challenged: U16 not done, Supabase signup unconfirmed — pre-conditions not met)
2. "Wait for guerrilla test" is a safe deferral for domain purchase (Growth Strategist challenged: circular dependency, no timeline because test prerequisites don't exist)
3. Limit-hit OR first paid facture triggers conversion (Technical Architect challenged: both assume formal written devis exist, which verbal-agreement artisans never produce)

### New action items from this pulse:
- [ ] **D95 NEW:** CONFIRM U16 (4 mentions légales templates) is done before Sprint 0 starts. If not done: accept 6.5-7 days, not 5.
- [ ] **D95 NEW:** CONFIRM Supabase signup is complete before Sprint 0 starts. If not done: add 2-4h to Day 1 for account creation + RLS policy design + migration workflow.
- [ ] **D95 NEW:** If either pre-condition is incomplete, update Sprint 0 estimate to 6.5-7 days. Do not try to squeeze a realistic 6.5-7 day sprint into a 5-day window.
- [x] ~~**U7 UPDATED**~~ **U7 RESOLVED (Debate 109):** Buy domain now (park it), defer brand decision. Domain = infrastructure, not branding. A parked domain costs €10-15/year and blocks nothing. Expert-comptable outreach and GetApp/Capterra setup need a proper domain to look credible. Brand name decision stays open.
- [x] **D96/D104 RESOLVED (Debate 110):** Dual-path conversion trigger. Path A (formal-devis): limit-hit OR first paid facture. Path B (verbal-agreement): 45 consecutive days active OR 7+ jobs logged OR 5+ active clients managed. Day 14 WhatsApp check-in applies to both.
- [ ] **D96/D104 NEW:** Sprint 1 must include robust job logging (Active Job Card from D13) — this is the verbal-agreement artisan's primary entry point. Path B conversion requires job tracking to be first-class, not secondary.
- [ ] **D96/D104 NEW:** Add usage analytics to identify "active verbal-agreement users" — those with jobs logged but zero devis sent. Segment for Path B conversion treatment.
- [ ] **D96/D104 NEW:** Guerrilla test validation: what % of Marc's clients require formal written devis vs verbal approval? If >40% verbal, Path B becomes the primary conversion design consideration.

*Last updated: 2026-03-30T21:27*

---

## New from Pulse 2026-03-30T21:38 — Three New Challenges

### Reopened (Debate 111, Debate 112, Debate 113):
- **Debate 111 (Job logging Sprint 1):** Product Strategist argues job logging (Active Job Card, D13) must be a Sprint 1 non-negotiable, not v1.2 deferral. Path B conversion (verbal-agreement artisan) is structurally impossible without job logging at launch. Sprint 1 scope cuts proposed: defer WhatsApp PDF sharing (Sprint 1b), mentions légales template engine (Sprint 2), multi-taux per line (Sprint 2). Sprint 1 keeps: client file + devis CRUD + flat-rate TVA calculator + minimum viable job logging.
- **Debate 112 (Expert-comptable conflict):** Growth Strategist argues Louis's accountant is not an outreach channel — conflict of interest creates passive non-execution. Network effect of 50 artisan clients weaker than assumed. Week 1 validation with accountant is biased feedback. Proposed: validate with non-conflicted artisan instead; use accountant only to learn what accountants need; referral playbook moved to Month 2-3.
- **Debate 113 (Sprint 0 blockers):** Technical Architect identifies six items that must be confirmed (not scheduled) before Sprint 0 can begin: (1) 4 mentions légales templates committed to git, (2) Supabase project dashboard accessible, (3) 1-page Sprint 0 scope document written, (4) API contract defined, (5) navigation library chosen (Expo Router recommended), (6) PDF generation approach chosen (server-side Supabase Edge Function recommended).

### New action items from this pulse:
- [ ] **Debate 111 NEW:** Sprint 1 scope revision — add minimum viable job logging (job create, status update, job notes, Active Job Card home view) as Sprint 1 non-negotiable. Cut from Sprint 1: WhatsApp PDF sharing (Sprint 1b), mentions légales template engine (Sprint 2), multi-taux per line (Sprint 2). Path B conversion requires job logging to exist.
- [ ] **Debate 111 NEW:** Sprint 1 job logging minimum scope: `jobs` table (id, client_id, title, description, status, scheduled_date, created_at, updated_at), home query (most recent in_progress/pending job), create job (title + client + date), update status (single tap), job notes (free text).
- [ ] **Debate 112 NEW:** U12 rethink — validate with one non-conflicted artisan in Week 1, not Louis's accountant. Accountant meeting reframed: learn what accountants need before recommending, not validation of the product.
- [ ] **Debate 112 NEW:** Expert-comptable referral playbook moved to Month 2-3. Prerequisites: 5-10 paying users, testimonials, accountant has seen product work.
- [ ] **Debate 112 NEW:** Acknowledge conflict of interest explicitly if accountant agrees to refer: "I want you to know — I'm your client and I don't want this to look like steering. If you don't think this is right for your clients, I want that feedback more than the referral."
- [ ] **Debate 113 NEW:** Sprint 0 pre-work (must be DONE, not scheduled): (1) 4 mentions légales templates committed to git, (2) Supabase project created (EU region), (3) 1-page Sprint 0 scope doc written, (4) API contract as shared types file, (5) Expo Router chosen for navigation, (6) server-side PDF generation chosen.
- [ ] **Debate 113 NEW:** Total pre-sprint work estimated: ~2.5 hours. This is the actual gate for 5-day Sprint 0.

*Last updated: 2026-03-30T21:38*


---

## New from Pulse 2026-03-30T21:55 — Three Resolutions

### Resolved (D111, D112, D113):
- **D111 (Job logging in Sprint 1):** RESOLVED — Job logging (Active Job Card, D13) is Sprint 1 non-negotiable. Dual-path conversion architecture (D110) requires both Path A (formal-devis artisan) and Path B (verbal-agreement artisan) operational at launch. Path B has no entry point without job logging. Sprint 1 scope updated: client file + devis flow + Active Job Card. PDF, mentions légales full engine, WhatsApp sharing moved to Sprint 1b.
- **D112 (Expert-comptable conflict of interest):** RESOLVED — Louis's existing accountant is a validation asset, not a sales channel. The conflict of interest creates structural incentives for passive non-execution. Expert-comptable GTM = cold outreach to 3-5 conflict-free expert-comptables in Caen area. Louis's existing accountant = validation conversation only.
- **D113 (Sprint 0 blockers):** RESOLVED — Sprint 0 cannot start until all six gate criteria are confirmed. All six must be committed to git and signed off. Sprint 0 = 5 days from gate-open.

### Action Items from this pulse:
- [ ] **D111 NEW:** Sprint 1 scope updated — client file + devis flow + Active Job Card (job logging) are all Sprint 1 non-negotiables. PDF generation, mentions légales full engine, WhatsApp sharing moved to Sprint 1b.
- [ ] **D112 UPDATED:** Expert-comptable GTM = cold outreach to 3-5 conflict-free expert-comptables in Caen area (no relationship to Louis). Louis's existing accountant = validation conversation only ("can I show you and get honest feedback?"). Remove "ask for referrals" from Louis's existing accountant conversation.
- [ ] **D113 NEW:** Sprint 0 gate criteria — all six must be confirmed before sprint starts:
  1. 4 mentions légales templates in git (U16 ✓)
  2. Supabase project dashboard visible (EU region)
  3. 1-page Sprint 0 scope document in git
  4. API contract defined (shared types or OpenAPI)
  5. Navigation library chosen (Expo Router recommended)
  6. PDF generation approach chosen (Supabase Edge Function recommended)

*Last updated: 2026-03-30T21:55*

---

## New from Pulse 2026-03-30T22:07 — Three Reopened

### Reopened (D99, D113 gate, D85):
- **D99 (Usage-based pricing):** REOPENED — Product Strategist argues €1.50/devis, capped at €29 creates value anchoring problem, revenue zero-sum for infrastructure costs, and cognitive overload at conversion moment. Flat €29/month is argued as simpler, better for unit economics, and aligned with single conversion path. Annual billing discount (€260/year) proposed as alternative seasonality fix.
- **D113 gate (PDF generation):** REOPENED — Technical Architect argues PDF generation approach must be the 7th Sprint 0 gate item. Three approaches (server-side, client-side, hybrid) have mutually exclusive constraints on data model, API contract, and mentions légales strategy. D74's Handlebars/Nunjucks template engine assumption may be wrong if PDFs are client-rendered.
- **D85 (GetApp/Capterra):** REOPENED — Growth Strategist argues pre-launch optimization is misallocated effort. French artisans don't browse comparison sites pre-discovery. Admin handlers use GetApp to validate Marc's choice, not to find the product. Blank profile with no reviews signals irrelevance. Defer to Month 3 after real user reviews exist.

### Action Items from this pulse:
- [ ] **D99 NEW:** Louis evaluates implementation complexity of usage-based billing (€1.50/devis, capped €29) vs flat €29/month. If usage-based is technically complex or creates billing uncertainty: kill D99, go flat €29. If seasonality is validated customer pain: address with annual billing discount (€260/year) not metering.
- [ ] **D113 gate UPDATED:** Add PDF generation approach as 7th Sprint 0 gate item. Three options to evaluate before sprint: (A) Supabase Edge Function + headless Chrome/Puppeteer (server-side), (B) react-pdf/expo-print (client-side), (C) server HTML template + expo-print (hybrid). Choice constrains mentions légales engine (D74), API contract (item 4), and blob storage strategy.
- [ ] **D85 UPDATED:** GetApp/Capterra optimization DEFERRED to Month 3. Spend those hours on SEO content, prescriber outreach, and expert-comptable cold calls instead. Reclaim profile setup time for Month 3 after 10+ real French artisan reviews exist.

*Last updated: 2026-03-30T22:07*

## New from Pulse 2026-03-30T22:18 — Three New Debates

### Reopened (D85, D99, D114):
- **D85 (GetApp/Capterra):** REOPENED — Growth Strategist argues Week 1 claim is a competitive ranking land-grab, not SEO investment. GetApp's algorithm weights review count and recency. A competitor listing today with 4-6 reviews structurally outranks our empty profile for 12-18 months. Deferring to Month 3 cedes ranking position permanently. Week 1: claim + populate with screenshots/pricing/features (not reviews). Publish Week 3-4 when beta user reviews are ready.
- **D99 (Pricing structure):** REOPENED — Product Strategist argues per-devis (€1.50/devis, cap €29) eliminates the "will I use this enough?" anxiety that flat €29 creates at conversion moment. Maps to D12 simplicity-first positioning. Seasonality handled in model itself. Annual billing discount (€260/year) becomes retention mechanic for engaged users, not acquisition tool.
- **D114 (PDF Sprint 0 gate):** REOPENED — Technical Architect proposes fourth approach: expo-print in-memory rendering (zero-schema). PDF is ephemeral render of current state, not stored document retrieval. No blob storage, no template file, no Handlebars dependency. Data model dependency: zero. 4-hour implementation estimate.

### New Action Items:
- [ ] **D85 NEW:** Claim GetApp and Capterra profiles Week 1 (not deferred to Month 3). Populate with screenshots, feature list, and pricing immediately. Do NOT publish until 3+ beta reviews exist (Week 3-4). Competitive ranking moat, not SEO play.
- [ ] **D85 NEW:** Seed GetApp/Capterra reviews from beta users in Week 2-3. Ask 5 beta users to leave reviews. First 3 reviews publish Week 3-4. Monitor competitor listing dates and review counts.
- [ ] **D99 NEW:** Louis evaluates per-devis billing complexity: Stripe usage-based billing (€1.50/devis, capped €29) vs flat €29. If usage-based is technically feasible in Supabase billing: replace D5's flat €29 with per-devis model. If complex: flat €29 stands, annual billing (€260/year) as seasonality fix.
- [ ] **D114 NEW:** Evaluate expo-print in-memory PDF approach as Sprint 0 gate item (4th option, zero-schema). Proof-of-concept in 4 hours. If print quality or sharing options inadequate on real devices: fallback to server-side Edge Function approach.
- [ ] **D114 UPDATED:** PDF generation = 7th Sprint 0 gate item. expo-print in-memory preferred. Mentions légales embedded in HTML string (no template file needed in Sprint 0). Handlebars/Nunjucks (D74) deferred to Sprint 1 if needed.

*Last updated: 2026-03-30T22:18*

---

## New from Pulse 2026-03-30T22:43 — Three New Challenges

### Reopened (D12, D72/D91, D100) — RESOLVED in 22:56 pulse below

- **D12 (Landing page):** Product Strategist challenged — "Sans vous prendre la tête" attracts avoidance-motivated buyers, not acute-pain buyers. Proposed alternative: competence frame ("Arrêtez de courir après vos paiements") + trial delivers proof in 5 minutes. → **RESOLVED: Simplicity-first RETAINED**
- **D72/D91 (Expert-comptable timing):** Growth Strategist challenged — French expert-comptables have professional liability exposure. Compliance review cycle = 3-6 months minimum. Expert-comptable = Phase 2 channel, not Month 1-2. → **RESOLVED: Phase 2, prescriber networks primary**
- **D100 (Supabase exit):** Technical Architect challenged — revenue-based triggers are either premature or too late. Proposed: composite usage-based exit trigger. → **RESOLVED: Usage-based composite trigger adopted**

*Last updated: 2026-03-30T23:08*

## New from Pulse 2026-03-30T22:56 — Three Resolved

### Resolved

- **D12 (Landing page):** Simplicity-first RETAINED. H1 stays "Sans vous prendre la tête." H2 delivers competence via 5-minute claim. Free tier is proof mechanism. "Arrêtez de courir" rejected — too negative, selects for crisis buyers.
- **D72/D91 (Expert-comptable timing):** Expert-comptable outreach = Phase 2 (Month 4+). Compliance liability is decisive. Louis's accountant = internal validation artifact only, not a referral mechanism. Prescriber networks primary Month 1-3 GTM.
- **D100 (Supabase exit trigger):** Composite usage-based exit adopted. Trigger: 3 consecutive months (>10k docs + >100 MAU + >€150/mo Supabase bill). Target: OVH/Hetzner VPS + Coolify + managed Postgres (€40-60/mo vs €300-600 Supabase). Migration planned from Day 1 with thin abstraction layer.

### Challenged Assumptions

1. "Acute pain buyers are the majority at awareness stage" — challenged: they already shop, they don't need convincing to look
2. "Simplicity frame selects the wrong buyer" — challenged: it selects the procrastinating artisan, not the drowning one
3. "Expert-comptable outreach is a Month 1-2 channel" — challenged: compliance liability makes it Month 4+ minimum
4. "Revenue-based migration triggers are sufficient" — challenged: they are lagging indicators that trigger too late

### New Action Items

- [ ] **D12 UPDATED:** A/B test landing page — simplicity frame vs competence frame with beta users before launch. Measure: time-on-page, signup rate, Day-7 retention. H1 stays simplicity for now.
- [ ] **D72/D91 UPDATED:** Expert-comptable outreach = Phase 2 (Month 4+). Do not budget Week 1 hours. Prescriber networks primary Month 1-3. Document in GTM strategy.
- [ ] **D100 UPDATED:** Add usage-based exit trigger to architecture notes: 3 months (>10k docs + >100 MAU + >€150/mo Supabase bill). Target stack: OVH/Hetzner + Coolify + managed Postgres. Build thin DB abstraction layer in Sprint 0.
- [ ] **D124 NEW:** Document Supabase exit plan: trigger metrics, target stack specs, migration effort estimate.

*Last updated: 2026-03-30T22:56*

## New from Pulse 2026-03-30T23:08 — Three New Challenges (D93, D81/C, D56)

### Reopened (D93, D81/C, D56)

- **D93 (Guided Creation Flow):** Product Strategist challenged — mandatory/scheduled onboarding call selects FOR hand-holders (high-cost, low-LTV users) and AGAINST autonomous professionals (ideal customers). "15 minute call" signals product assumes you can't figure it out. Sprint 0 building infra for call 70% of best-fit users skip.
- **D81/C (Offline scope):** Technical Architect challenged — "offline-capable" (optimistic UI + retry queue) fails where job logging needed: basements, rural sites, concrete buildings. Phone death, tunnel gaps, client crashes = unrecoverable data loss without local persistence.
- **D56 (SEO as primary digital):** Growth Strategist challenged — French BTP artisans don't Google for software. Hundreds/month nationally, not thousands. SEO attracts comparison-shoppers. Marc discovers via WhatsApp peer networks, not content. SEO = 6-12 month payoff; community seeding = WoM in weeks.

### New Action Items:
- [ ] **D93 NEW:** Replace mandatory Guided Creation Flow with 90-second in-app setup wizard (sensible defaults) + on-demand "comment ça marche" video. Opt-in, not required. Frame "open office hours" as drop-in, not personalized setup.
- [ ] **D93 NEW:** Instrument Guided Creation Flow if kept: track conversion rate of users who complete onboarding call vs those who skip. Use data to kill or keep.
- [ ] **D81 NEW:** Re-evaluate WatermelonDB/expo-sqlite for Sprint 0. If job logging ships Sprint 1 and artisans work in poor-connectivity environments, local SQLite persistence is foundational layer — not retry queue. Add 1-2 days to Sprint 0 estimate if adopted.
- [ ] **D81 NEW:** If offline SQLite adopted: add `sync_status` field (pending/synced/conflict) on all mutable tables as minimum viable conflict-detection for v1.
- [ ] **D56 NEW:** Deprioritize SEO from primary GTM to Month 6+ long-tail. Reallocate Sprint 0/1 digital hours to community seeding: identify 5-10 French BTP Facebook groups and WhatsApp clusters, join genuinely (no spam), instrument referral tracking ("comment connaissez-vous?" at signup + WhatsApp share codes).

### Challenged Assumptions:
1. "Guided Creation Flow increases Day-7 retention" — challenged: selects for hand-holders, repels autonomous pros
2. "Offline-capable sufficient for job-site job logging" — challenged: retry queue fails when phones die, connectivity gaps hours-long
3. "SEO is primary digital discovery channel" — challenged: artisans discover via peer networks, not Google search

*Last updated: 2026-03-30T23:08*

## New from Pulse 2026-03-30T23:21 — Three Debates Resolved

### Resolved

- **D93 (Guided Creation Flow):** RESOLVED — Sprint 0 should NOT include mandatory Guided Creation Flow. Replace with: 90-second in-app wizard (sensible defaults) + opt-in "open office hours" link. Mandatory call is rejected. Validated by: wrong user selection bias, infrastructure for 70% who skip, opportunity cost, and validation-before-build principle.
- **D81/C (Offline architecture):** RESOLVED — AsyncStorage + retry queue is insufficient for job-site environments. Sprint 0 must include local SQLite (expo-sqlite or WatermelonDB) as persistence foundation. Add 1-2 days to Sprint 0 estimate. Add `sync_status` field on mutable tables. Server-wins conflict resolution for v1.
- **D56 (SEO as primary channel):** RESOLVED — SEO is not the primary discovery channel for French BTP artisans. Move to Month 6+ long-tail. Primary Month 1-3 GTM = community seeding (WhatsApp/Facebook BTP groups) + referral tracking + prescriber outreach.

### Challenged Assumptions:
1. "Mandatory onboarding call increases Day-7 retention" — challenged: selects for hand-holders, repels autonomous pros
2. "Retry queue survives phone death and hours-long connectivity gaps" — challenged: AsyncStorage is not a database; job logging is core data, not cache
3. "SEO is the primary digital discovery channel" — challenged: artisans discover via peer networks, not Google search

### New Action Items:
- [x] **D93 RESOLVED:** Remove mandatory Guided Creation Flow from Sprint 0 scope
- [ ] **D93 NEW:** Sprint 0 ships: 90-second in-app wizard (business name, métier, currency, payment terms as defaults) + opt-in "open office hours" Calendly link in settings/help
- [ ] **D93 NEW:** Run 5 discovery calls with real artisans before Sprint 2 to validate call-based onboarding demand. Build only if data supports it
- [x] **D81/C RESOLVED:** Replace AsyncStorage + retry queue with expo-sqlite or WatermelonDB in Sprint 0
- [ ] **D81/C NEW:** Sprint 0 updated: add 1-2 days for local SQLite implementation. Add `sync_status` enum (pending/synced/conflict) on mutable tables. Build background sync worker triggered on connectivity restore
- [ ] **D81/C NEW:** Sprint 0 offline architecture: local SQLite (foundation) + background sync worker + sync_status field. Server-wins conflict resolution in v1
- [x] **D56 RESOLVED:** Move SEO from primary GTM to Month 6+ long-tail
- [ ] **D56 NEW:** Add referral tracking to signup flow this week: "Comment nous avez-vous connu?" at signup + WhatsApp share codes
- [ ] **D56 NEW:** Join 5-10 French BTP Facebook groups genuinely (no spam) this week
- [ ] **D56 NEW:** Build prescriber outreach list (architects, property managers) — Week 2

*Last updated: 2026-03-30T23:21*

## New from Pulse 2026-03-30T23:31 — Three Resolutions (D99, D113, D56)

### Resolved

- **D99 (Usage-based pricing):** KILLED — Flat €29/month + annual billing (€260/year) for seasonality. All three specialist agents independently rejected usage-based billing. Path B artisans (verbal-agreement, no formal devis) cannot be metered. Usage-based creates a two-tier billing architecture that contradicts dual-path conversion. 3-5 days of Stripe metering engineering for uncertain revenue benefit. Flat €29 requires one Stripe subscription. Annual billing solves seasonality without billing complexity.
- **D113 (PDF Sprint 0 gate):** RESOLVED — Reject expo-print in-memory. Adopt HTML-to-PDF via Supabase Edge Function. Same HTML serves WhatsApp OG tag preview page (no separate endpoint). Mentions légales embedded in HTML string Sprint 0. Handlebars/Nunjucks template engine deferred to Sprint 1 if needed.
- **D56 (Community seeding timing):** UPDATED — Community seeding pushed to Month 4+. Louis (solo dev) is the wrong person for community seeding right now — requires 2-4h/week commitment, 3-6 month lag before signal, social capital he doesn't have yet. Month 1-3 GTM = prescriber outreach + personal network introductions + referral tracking + GetApp/Capterra profiles.

### Challenged Assumptions:
1. "Usage-based billing helps seasonal cash flow" — challenged: benefit only applies to Path A (formal-devis artisans); Path B (verbal artisans) pay €0 indefinitely
2. "expo-print in-memory is fast enough for Sprint 0" — challenged: TVA arrondi precision issues, no WhatsApp OG preview, 4-hour POC risk of quality failure
3. "Community seeding is Month 1-3 priority" — challenged: solo dev lacks social capital and time for 2-4h/week community management

### New Action Items:
- [x] **D99 KILLED:** Usage-based billing (€1.50/devis, capped €29) permanently retired. Flat €29/month + €260/year annual billing at launch.
- [x] **D113 RESOLVED:** PDF generation = Supabase Edge Function (HTML-to-PDF). WhatsApp OG preview = same HTML template. Mentions légales embedded in HTML Sprint 0.
- [x] **D56 UPDATED:** Community seeding pushed to Month 4+. Month 1-3 GTM = prescriber outreach + personal network + referral tracking.
- [ ] **D99 NEW:** Update pricing page to show annual billing option (€260/year) alongside flat €29/month. Frame: "2 mois offerts" annual vs monthly.
- [ ] **D113 NEW:** Sprint 0 gate item — confirm PDF generation approach (HTML-to-PDF Edge Function) before sprint starts. POC in 2-4 hours to validate quality.
- [ ] **D56 UPDATED:** Remove "join 5-10 French BTP Facebook groups this week" from Week 1 tasks. Replaced with: (1) referral tracking in signup flow, (2) prescriber list of 10 architects/property managers in Caen area, (3) ask 3 people in personal network for artisan introductions.
- [ ] **D56 NEW:** Month 1-3 GTM execution order: Week 1 (referral tracking + personal network), Week 2 (prescriber list), Week 3-4 (first prescriber outreach calls), Month 2 (GetApp/Capterra profiles published with beta reviews).

*Last updated: 2026-03-30T23:31*

---

## New from Pulse 2026-03-30T23:48 — Three Resolved (D56, D81/C, D93)

### Resolved
- **D56 (SEO as Month 1-3 primary):** Growth Strategist won — SEO is the only channel Louis can execute alone with compounding returns. Community seeding pushed to Month 4+. Prescriber cold outreach Month 4+. Warm personal network introductions Month 1-3.
- **D81/C (Offline architecture):** Technical Architect won — expo-sqlite replaces AsyncStorage + retry queue. Background sync worker. Server-wins. +1 day to Sprint 0.
- **D93 (Onboarding):** Product Strategist won — office hours link moves from onboarding to Settings/Help. No call offered during onboarding. Discovery calls replaced with guerrilla test at Point P.

### New action items from this pulse:
- [ ] **D56 NEW:** Write one SEO-optimized landing page targeting "logiciel devis facture artisan" — no blog, no content engine, just one high-intent conversion page with U3 simplicity frame. Ship with Sprint 0.
- [ ] **D56 NEW:** "Comment avez-vous connu l'app?" tracking live from Day 1 signup.
- [ ] **D56 NEW:** Claim and optimize GetApp/Capterra profiles Week 1, publish Week 3-4 (admin handler audience — secondary discovery path).
- [ ] **D81/C NEW:** Sprint 0 includes expo-sqlite local persistence (not AsyncStorage). Background sync worker with `sync_status` enum (pending/synced/conflict). Server-wins conflict resolution.
- [ ] **D81/C NEW:** Add 1 day to Sprint 0 estimate for expo-sqlite integration.
- [ ] **D81/C NEW:** Sprint 0 cut order if needed: mentions légales plain text placeholder → WhatsApp PDF styling → client type field. Never cut SQLite.
- [ ] **D93 NEW:** Office hours link lives in Settings → Help only. Not in onboarding flow. Last resort.
- [ ] **D93 NEW:** Guerrilla test at Point P in Week 1 of Sprint 1 — 5 artisans with 90-second wizard prototype. Not warm-network discovery calls.
- [ ] **D93 NEW:** If Sprint 1 guerrilla testing shows friction points solvable by human touch, office hours re-emerges with different positioning ("Louis is a real artisan tech guy") not as onboarding infrastructure.

---

## New from Pulse 2026-03-30T23:55 — Three Resolved (D24, Sprint 0 Gate, D56 Prescriber Timing)

### Resolved

- **D24 (PWA vs React Native):** REVISED — PWA-first for Android. React Native deferred. D11/D17 superseded by D92 Android-first context. PWA eliminates Play Store moderation delay, enables APK direct distribution, and matches French artisan BTP download behavior. React Native reconsidered if iOS polish phase requires App Store presence, or if PWA proves insufficient for offline/camera/push requirements.
- **Sprint 0 Gate:** **CLOSED** — 0/6 items committed to git. All six gate items are decisions in debate log, not committed artifacts. Louis needs 3-4 hours gate-opening work before Sprint 0 can begin.
- **D56 (Prescriber outreach timing):** REVISED — Prescriber cold outreach deferred to Sprint 1 Week 1 (requires working demo). Month 1 GTM = warm network (Grinto alumni, MyDigitalSchool) + SEO content + landing page with email capture. Expert-comptable = Month 4+ (unchanged).

### Challenged Assumptions This Pulse

1. "App Store / Play Store distribution is required for mobile credibility" — challenged: French artisan BTP demographic installs via APK/WhatsApp, not App Store browsing
2. "Sprint 0 can start tomorrow" — challenged: zero of six gate items are committed to git; gate is closed
3. "Prescriber list building should happen in parallel with Sprint 0" — challenged: cold outreach without product = relationship damage; warm network is Month 1 channel

### New Action Items from This Pulse

- [ ] **D24 NEW:** Define PWA capabilities boundary for Sprint 0 — what offline sync is possible within 50MB service worker storage
- [ ] **D24 NEW:** Test APK direct download + home screen install flow with 3-5 artisan beta users before committing to PWA-only
- [ ] **D24 NEW:** Document deferred React Native criteria (push notifications, deep iOS integration, performance)
- [ ] **D24 NEW:** Confirm iOS secondary strategy — web-only iOS acceptable as Phase 1, or native App Store required?
- [ ] **Gate NEW — Louis completes gate-opening sequence (3-4 hours total):**
  - [ ] Write 4 mentions légales HTML template strings (one per client type). Commit to `legal/mentions-legales/`
  - [ ] Sign up at supabase.com → create project (EU region, Frankfurt). Share project URL
  - [ ] Write `docs/sprint-0-scope.md` — 1 page step sequence of devis flow. Commit
  - [ ] Create `src/shared-types.ts` — minimum type definitions (devis, client, line item, user). Commit
  - [ ] Formally choose Expo Router — add to scope doc + `package.json`. Commit
  - [ ] Scaffold `supabase/functions/generate-pdf/index.ts` — HTML template stub + Puppeteer. Commit
- [ ] **Gate NEW:** Sprint 0 cannot start until all six gate items are confirmed committed
- [ ] **D56 UPDATED:** Warm network outreach (Grinto alumni, MyDigitalSchool) = Month 1 primary GTM. Not cold prescriber outreach.
- [ ] **D56 UPDATED:** Prescriber cold outreach = Sprint 1 Week 1 (needs working demo URL/screenshots in hand)
- [ ] **D72 UNCHANGED:** Expert-comptable = Month 4+. Compliance liability is decisive. No change.

---

*Last updated: 2026-03-30T23:55*


---

## New from Pulse 2026-03-31T00:12 — Three New Debates (D126, Sprint 0 Gate, D128)

### Reopened (D126, D72/D91, Sprint 0 Gate)

- **D126 (Annual billing default):** REOPENED — Product Strategist argues annual billing (€260/year) creates acquisition friction that exceeds its churn benefit. French artisans have lumpy project-based cash flow — €260 upfront in a slow month is a genuine barrier. Monthly €29 removes this friction. Annual commitment also requires trust the product hasn't earned (no switching costs, no brand recognition, no data lock-in). L221-28 Code de la consommation 14-day cooling-off period creates involuntary churn window. Recommendation: monthly €29 as DEFAULT, annual €240/year as opt-in discount.

- **Sprint 0 Gate:** RESOLVED — Gate simplified to 2 items maximum. Louis is a solo technical founder — gate assumes non-technical founder scenario. Real gate-opening time is 6-8 hours, not 3-4. All other items deferred to Sprint 0 Day 1. Gate now: (1) Supabase project created, (2) mentions légales drafted as inline TODO comments in code.

- **D72/D91 (Expert-comptable timing):** REOPENED — Growth Strategist argues waiting until Month 4+ costs 3-4 months of referral pipeline. Expert-comptables need 2-3 months of relationship building before referring. By Month 4, Louis has no reference clients, no testimonials, no "Marc" success story to tell. Month 1 outreach is NOT a sales motion — it's customer development: problem discovery + relationship seeding. Expert-comptables evaluate "will this create more work or less?" — the answer is "less" regardless of UI polish.

### Challenged Assumptions This Pulse

1. "Annual billing solves seasonality churn" — challenged: forces retention through slow months, building resentment that erupts at renewal; monthly lets artisans self-select
2. "Gate items must be committed before Sprint 0" — challenged: gates are coordination tools for teams; Louis is solo and technical; real gate time is 6-8 hours
3. "Build product first, then do expert-comptable outreach" — challenged: referral pipeline takes 2-3 months to fill; building first means outreach starts when the pipeline should be delivering

### New Action Items from This Pulse

- [ ] **D126 NEW:** Evaluate monthly €29 as the DEFAULT pricing page offer, with annual €240/year (2 months free) as opt-in discount shown below monthly. Does this reduce acquisition friction vs leading with €260/year annual? Get artisan validation before committing.
- [ ] **D126 NEW:** If annual is still preferred: change landing page to show monthly first (€29/month), annual as secondary option. Annual-first positioning was never validated with real artisans.
- [ ] **D126 NEW:** Test cash flow framing: "Payez quand vous êtes chargé" (pay when you're busy) vs standard monthly/annual framing. Seasonal billing alignment may be a stronger conversion argument than annual discount.
- [ ] **Sprint 0 Gate UPDATED:** Simplified to 2 items. Louis creates Supabase project (EU region) + drafts mentions légales as inline TODO comments in code. All other gate items deferred to Sprint 0 Day 1.
- [ ] **Sprint 0 Gate NEW:** Louis completes gate-opening sequence this week (before Sprint 0 begins): Supabase project + 4 inline mentions légales TODO blocks. Estimated 2-3 hours total.
- [ ] **D72/D91 UPDATED:** Expert-comptable outreach = Week 1 Month 1 customer development conversations (NOT sales). Louis talks to 3 expert-comptables: problem discovery + relationship seeding. No product demo, no pitch, no brochures. Frame: "What compliance issues do you see with artisan clients?" and "I'm building something in this space — can I keep you posted?"
- [ ] **D72/D91 NEW:** Expert-comptable referral conversations (NOT validation) remain Month 4+ with prerequisites: real beta users, testimonials, production-validated mentions légales. The distinction is: customer development (Month 1) ≠ sales referral (Month 4+).

*Last updated: 2026-03-31T00:12*

---

## New from Pulse 2026-03-31T00:32 — Three Specialist Debates (D99, D72, D81/C)

### Reopened (D99 Annual Billing, D72 Expert-Comptable, D81/C Offline Architecture)

- **D99 (Annual billing — REOPENED again):** Product Strategist closes the case: monthly €29 is the ONLY defensible default. Annual €260/year creates acquisition friction (40% of potential customers won't pay upfront), creates involuntary churn at renewal via payment failures, and requires trust the product hasn't earned at v1. Monthly handles seasonality naturally through pause/resume cycles. Annual should be opt-in discount (€240/year, save €108) offered at conversion moment (80% Free tier limit hit). NOT YET RESOLVED.
- **D72 (Expert-comptable timing — REOPENED again):** Growth Strategist challenges the compliance liability argument as applied to the wrong action. Compliance liability blocks the REFERRAL ASK (Month 4+), but NOT relationship seeding (Week 1). The expert-comptable's question at Month 4 is "do your clients use it and does it work?" — requires real users, not polish. Week 1 outreach = problem discovery conversations. Referral conversation = Month 4+ after real users exist. NOT YET RESOLVED.
- **D81/C (Offline architecture — REOPENED again, THREE new challenges):**
  - Debate 135: Server-wins conflict resolution is invisible data corruption, not acceptable for job logging where data loss = revenue loss. Add sync_status: conflict detection (+0.5 days). NOT YET RESOLVED.
  - Debate 136: Mentions légales as TODO comments creates compliance discovery risk. Must be committed as real strings (Louis's own business data). Gate = 2.5 items, not 2. NOT YET RESOLVED.
  - Debate 137: "+1 day to Sprint 0" for expo-sqlite was never broken down into tasks. Real estimate: 1.5-2.5 days. Options: +2 days for full offline, or defer to Sprint 1. NOT YET RESOLVED.

### Challenged Assumptions This Pulse

1. "Annual billing solves seasonality churn while being acquisition-neutral" — challenged by Product Strategist: €260 upfront is a barrier for cash-constrained artisans; monthly handles seasonality through natural pause/resume
2. "Compliance liability blocks all expert-comptable conversations" — challenged by Growth Strategist: blocks referral ask only, not relationship seeding
3. "Server-wins conflict resolution is acceptable for v1" — challenged by Technical Architect: invisible corruption, not acceptable for revenue-tracking
4. "Mentions légales as TODO comments is a valid compliance shortcut" — challenged by Technical Architect: real strings with Louis's data required
5. "+1 day to Sprint 0 for expo-sqlite" — challenged by Technical Architect: real estimate is 1.5-2.5 days when broken into actual tasks

### New Action Items from This Pulse

- [ ] **D99 NEW (Product Strategist):** Pricing page architecture: €29/month as PRIMARY and ONLY required option. €240/year as opt-in discount (save €108) shown below monthly at conversion moment only. No annual-first presentation. No "€260 upfront" at signup.
- [ ] **D99 NEW:** Conversion prompt at 80% Free tier limit: "Vous utilisez [AppName] régulièrement — merci. Si vous savez déjà que cet outil vous fait gagner du temps, vous pouvez choisir de payer annually et économiser €108/an." [Payer €29/mois] [Économiser €108 — payer €240/an]
- [ ] **D99 NEW:** Test "Payez quand vous êtes chargé" framing (seasonal alignment) vs standard billing. Could be stronger conversion argument than annual discount.
- [ ] **D72 UPDATED:** Expert-comptable outreach = Week 1 Month 1 customer development conversations (problem discovery, relationship seeding). NOT a sales motion. NOT a product demo. Frame: "Je construis quelque chose dans ce domaine — quelles difficultés voyez-vous avec vos clients artisans?"
- [ ] **D72 NEW:** Louis books his own expert-comptable this week for a 20-minute problem-discovery call. Bring: questions about invoicing compliance pain points, NOT a product pitch. Ask if they'd be open to updates as the product develops.
- [ ] **D72 NEW:** Expert-comptable referral conversations stay Month 4+. Prerequisites: real beta users, testimonials, production-validated mentions légales. These prerequisites cannot be manufactured in Month 1-3 — they take time.
- [ ] **D81/C NEW (Technical Architect):** Sprint 0 offline scope decision required before sprint starts. Options: (A) +2 days budget for full expo-sqlite + background sync + conflict detection, OR (B) defer expo-sqlite to Sprint 1, ship with in-memory state only, label clearly as "demonstration only."
- [ ] **D81/C NEW:** If +2 days adopted: add sync_status: conflict detection in Sprint 0 (not just pending/synced). Half-day cost. Never silently overwrite with server-wins.
- [ ] **D81/C NEW:** Sprint 0 gate updated: mentions légales must be Louis's own business data committed as real strings (not TODO comments). Estimated 1 hour to fill in. Supabase project created remains gate item 1.

## New from Pulse 2026-03-31T00:40 — Three Resolutions (D138, D139, D140)

### Resolved (D138, D139, D140)

- **D138 (Annual billing implementation):** RESOLVED — Monthly €29 as PRIMARY and ONLY required option on pricing page. Annual €240/year as opt-in discount shown BELOW monthly at conversion moment only. Stripe subscription with annual pricing plan (monthly installments), NOT pre-payment. "Payez quand vous êtes chargé" (seasonal alignment) as primary conversion argument. Annual-first presentation KILLED.
- **D139 (Expert-comptable timing):** RESOLVED — Week 1 Month 1 customer development conversations with expert-comptables (Louis's own accountant = first call this week). Problem-discovery only: "What invoicing problems do your artisan clients bring to you?" NOT a product demo or sales pitch. Referral program = Month 4+ with prerequisites (real beta users, testimonials, production-validated mentions légales). Customer development ≠ sales referral.
- **D140 (Offline architecture):** PARTIALLY RESOLVED — Sprint 0 ships with AsyncStorage + retry queues (NOT expo-sqlite). Labeled as "demonstration only" if shipped in Sprint 0. expo-sqlite deferred to Sprint 1 (add 1.5-2.5 days to Sprint 1 estimate). sync_status field added to Sprint 0 schema regardless (30 min). Conflict detection UI deferred to Sprint 1.2 (after multi-user scenarios exist). Sprint 0 gate: mentions légales must be Louis's own business data committed as real strings, not TODO comments.

### Challenged Assumptions This Pulse

1. "+1 day" estimate for expo-sqlite was never task-broken (Technical Architect challenged: real estimate is 1.5-2.5 days when properly scoped)
2. "Annual billing solves seasonality" — challenged by Product Strategist: €260 upfront at conversion moment creates friction, not benefit; monthly handles seasonality through natural pause/resume
3. "Compliance liability blocks all expert-comptable conversations" — challenged by Growth Strategist: 14-day cooling-off applies to service contracts, not software recommendations; customer development ≠ referral sales

### New Action Items from This Pulse

- [x] **D138 RESOLVED:** Pricing page — €29/month PRIMARY, €240/year opt-in discount BELOW monthly. Stripe annual plan (monthly installments), not pre-payment.
- [x] **D138 NEW:** Update pricing page copy: primary CTA = "€29/mois — sans engagement." Secondary = "€240/an — soit 2 mois offerts." Add "Payez quand vous êtes chargé" seasonal framing.
- [ ] **D138 NEW:** Stripe configuration: set up annual pricing plan as subscription with monthly installments (not one-time €260 charge).
- [x] **D139 RESOLVED:** Expert-comptable customer development = Week 1. Louis books his own accountant this week for 20-min problem-discovery call.
- [ ] **D139 UPDATED:** Expert-comptable referral program = Month 4+. Prerequisites unchanged. Do not conflate customer development with sales referral.
- [ ] **D140 NEW:** Sprint 0 offline = AsyncStorage + retry queues. expo-sqlite deferred to Sprint 1. Add to Sprint 1 estimate: +1.5-2.5 days.
- [ ] **D140 NEW:** Sprint 0 adds sync_status field to schema (pending/synced/conflict) — 30 min, does not require expo-sqlite.
- [ ] **D140 NEW:** Sprint 0 gate: Louis commits 4 mentions légales templates as real strings (his own business data) before sprint starts.
- [ ] **D140 UPDATED:** Conflict detection UI deferred to Sprint 1.2. Marc is solo — no multi-user conflicts exist in v1.

*Last updated: 2026-03-31T00:40*

---

## New from Pulse 2026-03-31T01:47 — Three Specialist Debates (D146)

### Resolved
NONE — all three debates remain OPEN, requiring Louis's adjudication.

### Challenged Assumptions This Pulse

1. **"WhatsApp digest and soft limit friction are complementary"** — challenged by Product Strategist: D110 (soft limit) fires on active engagement; D40 (WhatsApp digest) fires on dormancy. Opposite psychological states, opposite goals. Shipping both without priority spec creates a self-undermining conversion funnel.
2. **"'demonstration only' is an acceptable offline scope constraint"** — challenged by Technical Architect: beta habits become production mental models; the label protects the team, not the product; silent data loss in Week 2 becomes broken trust in Month 4.
3. **"D138 (pricing) and D139 (expert-comptable outreach) are independent workstreams"** — challenged by Growth Strategist: €29/month "sans engagement" is consumer-conversion framing; it signals "no skin in the game" to expert-comptables, the most promising B2B referral channel.

### New Action Items from This Pulse

- [ ] **D40/D110 NEW — Sprint 0 conversion funnel design:** Louis decides: is WhatsApp a re-activation channel (dormant users) or a conversion channel (active users hitting limits)? These are different jobs. D40 Sprint 0 commitment blocked until D110 + D40 interaction is spec'd.
- [ ] **D40 NEW — WhatsApp deferral:** If D146 accepted: explicitly defer WhatsApp Business API to v1.1. Sprint 0 = Expo Push only. If rejected: spec D40/D110 priority interaction before committing WhatsApp to Sprint 0.
- [ ] **D140 NEW — Sprint 0 offline scope (updated from D146):** Louis chooses: (A) no offline editing in Sprint 0 — view-only cache + connectivity prompt on edit; honest scope, no silent data loss. OR (B) AsyncStorage offline editing with "demonstration only" label + visible beta onboarding screen disclosure. No silent data loss.
- [ ] **D138/D139 NEW — Dual framing protocol:** Louis prepares two separate pricing narratives: (1) landing page = €29/month, "sans engagement," consumer frame; (2) expert-comptable = daily anchor ("moins d'un euro/jour ouvré") OR competitive anchor ("moins que Sage en licences"). These are different pitches for different audiences.
- [ ] **D138/D139 NEW — Expert-comptable Week 1 talking points:** Louis writes 5-question problem-framing script including the expert-comptable-specific pricing anchor. Landing page copy does NOT go to expert-comptable meetings.
- [ ] **D141 NEW — In-app digest (D146 refinement):** If WhatsApp deferred to v1.1, D141 digest becomes in-app digest (Expo Push) for Sprint 0. Triggers at 14+ days dormant, Path B, ≥1 job logged. Plain text, user metrics reflected back, single re-entry CTA, no sales language.

*Last updated: 2026-03-31T01:47*

---

## New from Pulse 2026-03-31T01:59 — Three Specialist Debates (PS-D147, TA-D147, GS-D147)

### Challenged Assumptions This Pulse

1. "Sprint 0 can deliver the current scope in 5 days" — Product Strategist: 6+ major feature areas absorbed (WhatsApp Business API, Path B mechanics, dual-path architecture, mentions légales template engine, expo-sqlite), solo dev can't ship this in 5 days
2. "D110, D40, D140 are independent Sprint 0 deliverables" — Technical Architect: they form a tightly coupled dependency chain (soft limit threshold → notification channel → offline scope → back to threshold), must be resolved as one architectural unit before Sprint 0
3. "Annual €240 as DEFAULT at checkout maximizes conversion" — Growth Strategist: anchoring at wrong moment (product hasn't delivered value), monthly as "fallback" poisons the monthly tier, 35-45% uptake stat measures pressure not product-market fit

### New Action Items This Pulse

- [ ] **Sprint 0 scope reduction (PS-D147):** Pick 3 maximum deliverables for Sprint 0:
  1. Core devis flow (3 days): schema + client creation + devis creation + TVA calculator + expo-print PDF + WhatsApp share via native sheet + plain text mentions légales
  2. Auth + basic offline (1 day): Supabase auth + AsyncStorage caching + retry queues + view-only offline
  3. Notification foundation (0.5 days): Expo Push skeleton only, no WhatsApp
  Revised timeline: **4.5 days** (buffer for real device testing included)
  **Cut from Sprint 0:** WhatsApp Business API, Path B mechanics, dual-path architecture, mentions légales template engine, expo-sqlite, full push implementation, expert-comptable outreach prep

- [ ] **Path B architectural gate (TA-D147):** Restructure TODO — D140, D40, D110 cannot appear as three independent Sprint 0 workstream items. Single gated decision block:
  - **[BLOCKER] Path B conversion funnel:** D140 (offline scope, resolve first) → D40 (notification channel, conditioned on D140) → D110 (soft limit threshold, conditioned on D40). All three resolved together before Sprint 0 begins. This is one nested decision, not three parallel ones.

- [ ] **D138 revised — Annual billing (GS-D147):**
  - **Remove:** annual as default at checkout from D138 checkout flow spec
  - **Add:** monthly €29 as PRIMARY default at checkout — "Simple, flexible, cancel anytime" (not a fallback framing)
  - **Add:** annual €240 as opt-in upgrade presented AFTER 30+ days of active usage (5+ devis sent OR 3+ relances OR 10+ archived documents) — contextual upgrade prompt with value proof
  - **Add:** 3-month prepaid quarterly option at €79 (€26.33/month equivalent) as mid-tier for price-sensitive artisans
  - **Redesign checkout copy:** monthly €29 as positive confident choice, not the lesser alternative
  - **New KPI:** 40%+ of monthly users upgrade to annual within 60 days of hitting engagement triggers — measures product-market fit, not conversion pressure

- [ ] **Sprint 0 gate verification (D142 — still open):** Louis must commit `legal/mentions-legales.ts` to git with real business data BEFORE Sprint 0 begins. Sprint 0 = 4.5 days if gate met, 6+ days if not. This week.

*Last updated: 2026-03-31T01:59*

## New from Pulse 2026-03-31T02:13 — Three Specialist Debates (PS-D147, TA-D147, GS-D147)

*Note: Technical Architect position paper (TA-D147) was still processing at time of this pulse. Position paper expected at debate-pulse-0213-architect.md.*

### Resolved This Pulse
NONE — all three debates require Louis's input on scope and pricing decisions.

### Challenged Assumptions This Pulse

1. **"Simplicity-first and competence-first are mutually exclusive in Sprint 0."** Challenged by Product Strategist: a simplicity-first Sprint 0 that does one thing well is both. Path B mechanics are not Sprint 0 work.
2. **"35-45% annual uptake validates annual-as-default."** Challenged by Growth Strategist: that figure is coerced uptake in mature products, not applicable to first-conversion v1 SaaS. Monthly €29 PRIMARY confirmed.
3. **"Path B must be designed in Sprint 0."** Challenged by Product Strategist: you cannot validate conversion mechanics for users who don't exist yet.
4. **"WhatsApp Business API belongs in Sprint 0."** Challenged by Product Strategist: Meta verification alone blows the sprint timeline; Path B digest should be in-app/email, not WhatsApp.
5. **"D140, D40, D110 are independent Sprint 0 deliverables."** Challenged by Technical Architect: they form a tightly coupled dependency chain. [TA-D147 verdict pending]

### New Action Items from This Pulse

- [ ] **PS-D147 — Sprint 0 scope cuts:** Louis decides: accept 3-deliverable Sprint 0 (Core Devis Flow 3d + Auth/Offline-Capable 1.5d + Expo Push Skeleton 0.5d = 5 days). Cuts: WhatsApp Business API, Path B mechanics, dual-path architecture, mentions légales template engine (→ static strings), expo-sqlite (→ AsyncStorage), full push, expert-comptable prep. **Blocks Sprint 0.**
- [ ] **PS-D147 — Path B deferral confirmed:** Louis confirms: Path B conversion mechanics deferred to v1.2. Sprint 0 ships Path A only. Confirms D110, D141, D40 deferral.
- [ ] **GS-D147 — Pricing page architecture:** Louis confirms: monthly €29 as PRIMARY, annual €240 as secondary opt-in savings ("épargnez €108/an"), quarterly €79 as mid-tier. Three-zone layout. Annual as contextual upgrade prompt at 30+ active days (5+ devis sent), NOT at first checkout.
- [ ] **GS-D147 — Pricing KPI:** Confirm: 40%+ of monthly users who hit engagement triggers upgrade to annual within 60 days. Replaces conversion rate as pricing health KPI.
- [ ] **GS-D147 — Challenged assumption:** 35-45% annual uptake stat retired. Correct benchmark: 10-15% opt-in annual uptake at month-1 conversion (genuine preference signal). Coerced annual conversions generate involuntary churn at renewal.
- [ ] **TA-D147 — Path B architectural gate:** Louis decides: D140 (offline scope) → D40 (notification channel, conditioned on D140) → D110 (soft limit threshold, conditioned on D40). All three resolved as one unit before Sprint 0. [PENDING Technical Architect position paper]
- [ ] **D142 — Sprint 0 gate (URGENT):** Louis commits `legal/mentions-legales.ts` to git with real business data (his own). NOT TODO comments. Gate must be verified before Sprint 0 begins. 5-day Sprint 0 is CONDITIONAL on this.
- [ ] **D142 — Supabase project:** Louis confirms Supabase EU project (Frankfurt) is live and accessible. Gate item 2.

### Louis's Decisions Required Before Sprint 0 (02:13 Updated)

| Decision | Options | Sprint 0 Status |
|----------|---------|-----------------|
| Sprint 0 scope cuts | Accept 3-deliverable OR negotiate | BLOCKS Sprint 0 |
| Path B deferral | Confirm v1.2 | BLOCKS Sprint 0 |
| Pricing page architecture | Confirm monthly €29 primary | Unblocks planning |
| Path B architectural gate | Resolve D140→D40→D110 | BLOCKS Sprint 0 |
| Mentions légales gate | Commit real strings to git | BLOCKS Sprint 0 |
| Supabase project | Confirm EU project live | BLOCKS Sprint 0 |

### Sprint 0 Scope (PS-D147 Proposal — Requires Louis Confirmation)

**If accepted (5 days):**

| Day | Deliverable |
|-----|-------------|
| 1 | Supabase EU project + schema (clients, devis, line_items, TVA calculator) + auth |
| 2 | RN client list + devis list screens, Supabase integration |
| 3 | Devis creation flow, TVA per-line, expo-print PDF, native share |
| 4 | Mentions légales as static strings, sequential numbering, offline caching, retry queues |
| 5 | Auth completion, Expo Push skeleton, real device testing (Android) |

**Cuts accepted:** WhatsApp Business API, Path B mechanics, dual-path architecture, mentions légales template engine, expo-sqlite, full push implementation, expert-comptable prep.

**Floor: 5.5 days** if mentions légales gate not met.

*Last updated: 2026-03-31T02:13*

## New from Pulse 2026-03-31T02:28 — Three Specialist Debates (D146-3A, D146-3G, D146-3P)

### Resolved This Pulse

NONE — all three debates are CONTESTED. Louis decisions required before Sprint 0 can proceed.

### Challenged Assumptions This Pulse

1. **AsyncStorage + retry queues is sufficient for Sprint 0 offline** (Debate 81/86) — challenged by Technical Architect: power loss mid-write = data lost, retry queues have fatal blind spot, view-only or expo-sqlite required
2. **Path B can wait for v1.2** (PS-D147) — challenged by Growth Strategist: Path A is minority segment (~50-60%), Path B = 40-50% of target market, threshold trigger + upgrade prompt + instrumentation should be Sprint 0
3. **"First paid facture" is the Path A conversion trigger** (D96) — challenged by Product Strategist: requires payment infrastructure outside product control, "first accepted devis + 3 clients" is better conversion moment

### New/Updated Action Items

- [ ] **D81 UPDATED — Offline scope decision (URGENT):** Louis chooses — (A) view-only offline for Sprint 0 (honest engineering disclosure, browse cached only, no offline editing), OR (B) expo-sqlite in Sprint 0 (+2 days, production-grade offline editing). **Blocks Sprint 0.**
- [ ] **D110 UPDATED — Path B in Sprint 0:** Sprint 0 must include Path B threshold trigger (30-day + 3 jobs) + upgrade prompt + conversion instrumentation. WhatsApp digest deferrable to v1.2. **Path B is not v1.2 optional — it covers 40-50% of target market.** **Blocks Sprint 0 scope.**
- [ ] **D96 UPDATED — Path A conversion trigger:** Replace "first paid facture" with **"first accepted devis + 3 active clients managed."** "Paid facture" requires payment infrastructure (Stripe/Lydia/Pix) not in MVP scope. Accepted devis = committed client intent = maximum emotional investment moment. **Low urgency — affects post-Sprint 1 conversion design.**
- [ ] **D81 UPDATED — Sprint 0 timeline revised:** If option (B) accepted (expo-sqlite): Sprint 0 = 7 days (was 5.5-6.5). If option (A) accepted (view-only): Sprint 0 = 5.5 days with honest disclosure note.
- [ ] **D140/D40/D110 dependency chain — REVISED:** D81 (offline scope) → D40 (notification channel) → D110 (Path B threshold). All three must be resolved as one unit before Sprint 0. Louis resolves D81 first.

### Louis's Decisions Required Before Sprint 0 (02:28 Updated)

| Decision | Options | Sprint 0 Status |
|----------|---------|-----------------|
| Offline scope (D81) | (A) View-only OR (B) expo-sqlite (+2d) | **BLOCKS** |
| Path B trigger in Sprint 0 (D110) | (A) Sprint 0 trigger + prompt + instrumentation OR (B) defer to v1.2 | **BLOCKS** |
| Path A trigger (D96) | (A) First accepted devis + 3 clients OR (B) first paid facture | Post-Sprint 1 |
| Mentions légales gate | Commit real strings to git | **BLOCKS** |
| Supabase project | Confirm EU project live | **BLOCKS** |

*Last updated: 2026-03-31T02:28*

## New from Pulse 2026-03-31T02:43 — Two Specialist Debates (TA-D148, GS-D148)

*Note: PS-D148 (Product Strategist — Conversion Moment Design) was still processing at time of this pulse. Position paper expected.*

### Resolved This Pulse

NONE — both debates are CONTESTED. Louis decisions required.

### Challenged Assumptions This Pulse

1. **"Offline capability is the core architectural problem"** — challenged by Technical Architect: multi-device conflict resolution on versioned business documents is the gap, not local storage engine choice (D140, D144)
2. **"D9's 'no multi-user' exclusion covers the spouse/shared-account scenario"** — challenged by Technical Architect: enabling offline editing implicitly creates a second writer, violating D9's intent (D9)
3. **"Server-wins is a valid offline fallback"** — challenged by Technical Architect: it discards the user's offline work silently; not conflict resolution, just arbitrary data destruction (D140)
4. **"3 active clients" meaningfully discriminates conversion intent** — challenged by Growth Strategist: trivially gameable with existing client imports; measures existing relationships, not product adoption (PS-D146-3P)
5. **"3 active clients" as a validated threshold** — challenged by Growth Strategist: number traces to D96's paid-facture era, never re-validated for accepted-devis trigger (D96, D110)

### New/Updated Action Items

- [ ] **D81 REVISED — Offline scope decision (URGENT):** Louis chooses — (A) view-only offline for Sprint 0 (no offline editing), OR (B) draft-mode offline (+0.5 days, changes queue as drafts pending review, not overwrites), OR (C) full offline editing deferred to v1.2. **Blocks Sprint 0.** TA-D148 argues that the choice of local storage engine (AsyncStorage vs expo-sqlite) is secondary to the semantic model (draft vs overwrite).
- [ ] **D140 REVISED — Offline edit semantics:** Sprint 0 offline editing must adopt draft-mode semantics: offline changes saved as drafts pending manual review. They do NOT overwrite the live document until the artisan explicitly confirms after reviewing concurrent changes. This eliminates silent data destruction from server-wins fallback. Real bidirectional sync = v1.2 minimum.
- [ ] **D96 REVISED — Path A conversion trigger:** GS-D148 and PS-D146-3P are in direct conflict. GS-D148 proposes: "3 accepted devis from 3 distinct clients" (harder to game, requires 3 closed deals across different clients). PS-D146-3P proposed: "first accepted devis + 3 active clients" (easier to satisfy with dummy imports). Louis decides. **Post-Sprint 1 — low urgency.**
- [ ] **D110 REVISED — Path B trigger refinement:** GS-D148 proposes: "3 jobs logged with client contact info captured (name + phone or email)" — prevents placeholder job logging. D110 original: "3 jobs logged" (no scope floor). Louis decides. **Post-Sprint 1 — low urgency.**
- [ ] **D9 REVIEWED — Multi-user architecture note:** TA-D148 identified that D9 (no multi-user) is implicitly violated by enabling offline editing on an account that also has web dashboard access (spouse/assistant sharing). Sprint 0 architecture must document this constraint: offline editing is single-device-only (the offline device is the sole writer while offline). Multi-device concurrent editing = v1.2.

### Louis's Decisions Required Before Sprint 0 (02:43 Updated)

| Decision | Options | Sprint 0 Status |
|----------|---------|-----------------|
| Offline scope (D81) | (A) View-only; (B) draft-mode (+0.5d); (C) full offline defer v1.2 | **BLOCKS** |
| Mentions légales gate | Commit real strings to git | **BLOCKS** |
| Supabase project | Confirm EU project live | **BLOCKS** |
| Path A trigger (D96) | (A) 3 accepted devis from 3 distinct clients; (B) first accepted devis + 3 active clients | Post-Sprint 1 |
| Path B trigger (D110) | (A) 3 jobs + client contact info; (B) 3 jobs logged | Post-Sprint 1 |

*Last updated: 2026-03-31T02:43*
