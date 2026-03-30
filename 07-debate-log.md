# Debate Log — Mini-CRM Research Sprint

##记录 Agents Discussing and Disagreeing

This document captures key debates between specialist perspectives, how they resolved (or didn't), and why decisions were made.

---

## Debate 1: Mobile-First vs. Desktop-First

### The Disagreement

- **Technical Architect:** "Let's build Nuxt with SSR, deploy as PWA. Mobile is important but desktop matters for data entry-heavy tasks."
- **Product Strategist:** "No. Mobile-first is non-negotiable. These artisans are on-site 80% of the day. Desktop is secondary."

### The Argument

Technical Architect's concerns:
- Complex forms are painful on mobile
- French address input requires good keyboard
- Offline mode is harder on mobile web

Product Strategist's concerns:
- Marc (plumber) doesn't have a desk
- Sophie (electrician) uses phone during day, PC at night
- Jean-Pierre (carpenter) doesn't even use smartphone

### Resolution

**Decision: Mobile-first, PWA acceptable for launch**

Product Strategist won on this one. Evidence:
- 55% of target are solo artisans with no desk
- WhatsApp usage on mobile is baseline behavior
- PWA on mobile is good enough for MVP

**Compromise:** Desktop responsive design maintained, but mobile UX is primary design target.

---

## Debate 2: Pricing — €19 vs €29 vs €49

### The Disagreement

- **Growth Strategist:** "Price at €19/month. Lower barrier, faster adoption. We need volume."
- **Product Strategist:** "Price at €29/month minimum. This is a professional tool. €19 feels cheap, unreliable."
- **Market Validator:** "Research shows €29 is the sweet spot. But €19 gets more trial signups."

### The Argument

Growth Strategist's concerns:
- French artisans are price-sensitive
- €29 feels like "one hour of labor" — hard to justify
- Volume compensate for lower price

Product Strategist's concerns:
- Cheaper = less perceived value
- Need revenue to survive
- Target customer has €50k+ revenue

Market Validator's data:
- Survey: 40% would pay €9, 20% would pay €19, 10% would pay €29
- BUT: those willing to pay €29 are more likely to stick
- Churn at €9 is 3x higher than €29

### Resolution

**Decision: €29/month solo tier, €49 Pro, €79 Business**

Compromise reached:
- Entry price at €29 (not €19) to maintain value perception
- Three tiers capture different segment needs
- Jean-Pierre (carpenter) would pay €79, so don't leave money on table

**Key insight:** Lower price doesn't always mean more customers for SMB. Quality matters.

---

## Debate 3: Stack — Supabase vs. Firebase vs. MariaDB

### The Disagreement

- **Technical Architect:** "Supabase is the clear choice — PostgreSQL, auth, real-time, good DX."
- **Market Validator:** "French clients worry about US data. Maybe self-hosted Postgres on Coolify?"
- **Product Strategist:** "I don't care about the stack. Just make it work and don't charge too much."

### The Argument

Technical Architect's concerns:
- Supabase has Frankfurt region (EU data compliance)
- Faster development = lower cost
- Real-time built-in for multi-user later

Market Validator's concerns:
- CNIL compliance paranoia
- French companies prefer European providers
- "What if Supabase goes bankrupt?"

Product Strategist's concerns:
- Cost of operations
- Simplicity

### Resolution

**Decision: Supabase for MVP, keep migration path open**

Technical Architect won:
- Frankfurt region addresses EU concern
- Supabase is VC-backed, stable enough for MVP
- If concerns persist, can migrate to self-hosted Postgres later

**Key insight:** Premature optimization on infrastructure kills startups. Ship with Supabase, migrate if needed.

---

## Debate 4: Multi-User for MVP

### The Disagreement

- **Product Strategist:** "Multi-user is essential. Sophie (electrician with 2 employees) is our ideal customer."
- **Technical Architect:** "Multi-user sync is complex. Let's ship single-user MVP first."
- **Growth Strategist:** "Single user = single paying seat. Multi-user = more revenue potential."

### The Argument

Product Strategist's concerns:
- Sophie's persona is most compelling
- She represents a larger wallet
- Team coordination is real pain point

Technical Architect's concerns:
- RLS (Row-Level Security) adds complexity
- Real-time sync is tricky
- 3 more weeks of development

Growth Strategist's concerns:
- Single-user is limit
- Can't sell to teams later?

### Resolution

**Decision: Single-user MVP, multi-user in 3 months**

Compromise:
- MVP ships single-user only
- Sophie persona is aspirational, not day-1 target
- Marc (solo plumber) is easier to acquire first
- Multi-user is roadmap item for Q2

**Key insight:** Don't try to be everything to everyone on day 1. Solo users first, expand later.

---

## Debate 5: Offline Mode — MVP or Never?

### The Disagreement

- **Product Strategist:** "Offline is critical. Artisans work in basements, rural areas with no signal."
- **Technical Architect:** "Offline-first is 3-6 months of extra work. Let's ship online-first."
- **Growth Strategist:** "If it doesn't work offline, they'll abandon it after first frustration."

### The Argument

Product Strategist's data:
- Rural areas have poor 3G/4G coverage
- Job sites often underground/in old buildings
- "Lost signal" is daily occurrence

Technical Architect's data:
- Offline-first requires local database (SQLite)
- Conflict resolution is complex
- Testing is 3x harder

Growth Strategist's data:
- Artisans tolerate less than enterprise users
- First bad experience = churn

### Resolution

**Decision: Online-first MVP, offline within 6 months**

Compromise:
- App caches recent data (basic offline read)
- Writes queue when offline, sync when online
- Full offline mode (SQLite) within 6 months

**Key insight:** Not every feature on day 1. But offline is important enough to schedule early.

---

## Debate 6: French Payment (CB/Lyf) vs. Stripe

### The Disagreement

- **Market Validator:** "French artisans expect CB/Lyf. Stripe doesn't support Lyf Pay."
- **Technical Architect:** "Lyf Pay integration is complex, requires partnership. Stripe is easier."
- **Growth Strategist:** "Who cares about payment method? Get the sale first."

### The Argument

Market Validator's concerns:
- Lyf Pay is popular in France (CAFAM-backed)
- CB (cartes bancaires) is expected
- "If I can't pay with Lyf, I go elsewhere"

Technical Architect's concerns:
- Lyf Pay API is not developer-friendly
- Requires business partnership with Lyf
- Months of integration work

Growth Strategist's concerns:
- Payment method is down-funnel
- Stripe supports CB (the main card network)
- Most users will use CB anyway

### Resolution

**Decision: Stripe + CB first, Lyf Pay in Year 2**

Compromise:
- Stripe handles CB payments (Visa, Mastercard, CB)
- Lyf Pay is nice-to-have, not essential
- Revisit when we have 200+ paying customers

**Key insight:** Don't let perfect be the enemy of good. Stripe + CB covers 90% of French payments.

---

## Debate 7: Feature Scope — Pipeline (Kanban) vs. Simple List

### The Disagreement

- **Product Strategist:** "Kanban pipeline is essential. It's how artisans think: Devis → Accepté → En cours."
- **Technical Architect:** "Kanban is complex to build responsive. A simple list is faster to ship."
- **Growth Strategist:** "Simplicity sells. Maybe just a list + filters?"

### The Argument

Product Strategist's concerns:
- Pipeline is the core differentiator vs. WhatsApp
- Visual = better than text list
- Sophie's team needs shared view

Technical Architect's concerns:
- Drag-and-drop on mobile is tricky
- Responsive Kanban requires good CSS
- 1 extra week of development

Growth Strategist's concerns:
- Complexity increases support burden
- "Keep it simple" is often right

### Resolution

**Decision: Kanban is MVP, but simple**

Compromise:
- 4 fixed columns (Devis, Accepté, En cours, Terminé)
- Tap to move between stages (no drag required)
- Mobile-first: stacked cards, swipe or tap to move

**Key insight:** Kanban is core to the product story, but implementation can be simplified.

---

## Summary: Key Tensions Resolved

| Debate | Winner | Losing Argument | Resolution |
|--------|--------|-----------------|------------|
| Mobile-first | Product | Desktop-first | Mobile design target, responsive desktop |
| Pricing | Market Validator | Growth Strategist | €29/49/79 tiered |
| Stack | Technical Architect | Self-hosted Postgres | Supabase, migration path open |
| Multi-user | Technical Architect | Product Strategist | Single-user MVP |
| Offline mode | Product Strategist | Technical Architect | Online-first, offline in 6mo |
| Lyf Pay | Growth Strategist | Market Validator | Stripe + CB, Lyf later |
| Kanban | Product Strategist | Growth Strategist | Simple 4-column Kanban |

---

## Unresolved Questions

1. **Referral program design** — How much is a referral worth? (€20 credit vs. cash)
2. **Landing page** — Focus on ROI ("gagnez 2h/semaine") or simplicity ("simple comme WhatsApp")?
3. **Trial length** — 14 days (standard) or 30 days (more time to see value)?

---

*Last updated: 2026-03-30*

---

## Debate 8: Trial Length — 14 Days vs 30 Days

### The Disagreement

- **Product Strategist (14 days):** Urgency creates decisions. High-intent users convert in 3-5 days. More trial = more dead accounts cluttering DB. French artisans are reactive — if the app doesn't solve their problem in session 1, another 2 weeks won't help.
- **Growth Strategist (30 days):** You might never catch them during an active job cycle in 14 days. French artisans are cautious, they ask neighbors. The conversion moment is "first actual job created in the app" — can't rush that. Better churn signal: real rejections vs. "never got around to it."

### Resolution

**Decision: 30 days**

The 30-day argument is stronger for this specific audience. French artisans work on irregular cycles — a plumber might have 2 urgent callouts then nothing for 10 days. 14 days might miss their entire active period. The conversion moment ("first job created in the app") can't be forced. 30 days gives better churn signal: real rejection vs. time pressure.

---

## Debate 9: Stack — Supabase vs OVH Self-Hosted Postgres

### The Disagreement

- **Technical Architect (original decision):** Use Supabase Frankfurt — fast to build, real-time built-in, migration path open.
- **Technical Architect (challenging):** "We migrate later" never happens under pressure. Self-hosted Postgres on OVH is a sales differentiator — "Toutes les données sont sur notre serveur OVH, en France" answers every CNIL question completely. Cyber-insurance requirements are coming for French businesses. OVH already fits the stack.

### Resolution

**Decision: OVH Self-Hosted Postgres — Day One**

The challenge is valid and strong. The "we'll migrate later" plan is exactly the kind of technical debt that kills 3-person teams. Self-hosted Postgres on the customer's own OVH VPS from day one:
- Answers every compliance question completely
- No DPA, no SCCs, no trust exercise with a third party
- OVH already in the ecosystem (Louis's gateway is already there)
- Fixed cost per VPS vs. Supabase's scaling unpredictable costs
- Architecture never changes — no migration debt

**Stack revised:** Nuxt 3 + Self-Hosted Postgres on customer OVH VPS (not Supabase).

---

*Last updated: 2026-03-30T09:45:00Z*

---

## Debate 10: Onboarding — Contact Import as MVP vs "Soon"

### The Disagreement

- **Product Strategist (challenging):** "Contact import from WhatsApp Business and phone should be Day 1 MVP, not 'Soon.' The feature matrix is wrong."
- **Feature Matrix (existing decision):** "Import from phone contacts" ranked as "Soon" (within 3 months, not MVP)

### The Argument

Challenger's position:
- "No contacts = nothing" — if the product is useless on day one, users open the app, see empty, and leave forever
- WhatsApp Business exports to vCard/CSV — this is a file parser, not a hard engineering problem
- Marc lives in WhatsApp — his client list IS his WhatsApp contacts. Telling him to type them manually is double work for zero benefit
- Jean-Pierre's secretary won't migrate a decade of client contacts manually — the friction doesn't disappear, it just moves
- "Soon" in product roadmaps means "when we get around to it, maybe" — that's how you ship an empty CRM

Feature Matrix rationale (prioritisation):
- Simplicity of MVP scope
- Avoid scope creep at launch
- Engineering bandwidth for core CRM features first

### Resolution

**UNRESOLVED — Flagged for sprint planning**

The challenge is strong. The argument that "no contacts = nothing" directly undermines the product vision's core premise. However, the Product Strategist's recommendation — two import buttons on a single screen — is technically achievable in sprint 1 if scoped narrowly.

**Open question for Louis:** Should contact import from WhatsApp Business / phone contacts be added to MVP scope as two buttons (import from vCard, import from phone)? The risk is not engineering complexity — it's scope creep. The reward is day-one stickiness for every new user.

**Key insight:** "Simple MVP" does not mean "impose friction as a feature." Manual data entry is friction, not simplicity.

---

## Debate 11: PWA vs Native App — Challenging "PWA Acceptable for Launch"

### The Disagreement

- **Technical Architect (challenging):** "PWA is the wrong choice for this audience. Capacitor-based hybrid or native is necessary."
- **Debate 1 Resolution:** "Mobile-first, PWA acceptable for launch"

### The Argument

Challenger's position:
- Android PWAs have unreliable push notifications — Xiaomi, Samsung, Oppo all kill background processes aggressively
- On iOS, PWAs cannot send push notifications at all without native apps — this eliminates 30%+ of iPhone users
- The core value prop is reminders that FIRE — if notifications don't fire reliably, the product fails its core promise
- Jean-Pierre (55, tech-resistant) won't "Add to Home Screen" — he wants a real App Store icon
- Capacitor wraps existing web code in native shells — same codebase, same team, same cost, real app with reliable FCM push notifications
- Feature matrix already says "Mobile app (iOS + Android)" — that's native, not PWA

Debate 1 compromise (PWA acceptable):
- Faster to ship
- No app store review delays
- Lower maintenance burden
- "Good enough for MVP"

### Resolution

**UNRESOLVED — Technical Architect makes a strong case**

The push notification reliability argument is compelling. If reminders are the core product value and Android OEM battery management kills PWA background processes, the product fails its most critical feature. The "acceptable for launch" compromise from Debate 1 deserves formal reconsideration.

**Key tension:** App Store review (7-14 days) and dual-platform maintenance vs. notification reliability and "real app" feel for resistant users like Jean-Pierre.

**Compromise path:** Capacitor (web codebase + native shell) is the practical middle ground. iOS App Store + Google Play from day one. This is not significantly more expensive than PWA if scoped correctly.

**Key insight:** "Acceptable" is not the same as "right." PWA may have been a reasonable speculation in Debate 1 — it should be challenged again now with the reminder reliability requirement explicit.

---

## Debate 12: GTM Strategy — Trade Fairs vs Digital-First Acquisition

### The Disagreement

- **Growth Strategist (challenging):** "The GTM strategy is too slow and too analog. Trade fair + supplier partnerships is an incumbent's strategy."
- **Go-to-Market document (existing):** "Trade fairs > online ads for this audience" listed as a key insight; 40% weight on word of mouth, 15% on paid ads

### The Argument

Challenger's position:
- Trade fairs: €2,000-5,000/booth, 200-500 visitors, 0.5% conversion = €1,000-2,500 CAC
- Google Ads for "CRM artisan" keywords: CPC €0.80-1.50, 3% conversion = €360 CAC — 3x cheaper
- "Trade fairs > online ads" is lazy conventional wisdom, not data
- Supplier partnerships (Point.P, BigMat) require sales cycles of 6-18 months — a startup can't afford this
- Facebook Groups ("Artisans du bâtiment") — 500k+ members, zero CAC, targeted 90-second screen recordings
- YouTube Shorts/Reels — artisan TikTok/YouTube is exploding; one viral video = 200+ signups
- Incumbent GTM (Sage, Delta Blue) relies on sales teams — a startup has none

Go-to-Market document rationale:
- Artisans trust physical relationships over online ads
- Word of mouth is highest-converting channel for tradespeople
- Personal networks are the fastest path to first 50 beta users
- Content marketing builds long-term SEO equity

### Resolution

**UNRESOLVED — Key strategic decision for Louis**

The CAC math is compelling and the trade fair argument deserves scrutiny. However, the "personal network first" approach is sound for the initial beta cohort, not for scalable growth.

**Recommended rebalancing:**
- Phase 1 (Month 0-3, beta): Personal network + Facebook Groups (zero CAC, fast)
- Phase 2 (Month 3-12, growth): Google Ads (scaling paid channel once product-market fit confirmed) + YouTube content (viral potential) + referral program
- Defer supplier partnerships to Month 9+ when you have case studies and a sales story

**Kill the trade fair budget** (or cap at €2,000) — reallocate to Google Ads and content production.

**Key insight:** "Trade fairs > online ads" is an INCUMBENT'S strategy. Startups should be where incumbents aren't — and that means digital-first, content-first, paid-search-first.

---

## Debate 13: OVH Self-Hosted Postgres — Operational Debt vs Migration Debt

### The Disagreement

- **Technical Architect (challenging):** "OVH VPS self-hosted Postgres isn't 'data sovereignty' — it's outsourcing your SRE team to no one."
- **Debate 9 Resolution:** "Self-hosted Postgres on OVH from day one — answers every compliance question, no DPA needed."

### The Argument

Challenger's position:
- OVH VPS is a bare VM — you own ALL operational burden: backups (pg_dump cron), connection pooling (PgBouncer), monitoring, security patches, OS updates, disk full handling
- A 3-person team cannot be on call for database incidents while also building product
- "No migration debt" is a seductive lie — you're not avoiding operational complexity, you're permanently owning it
- OVH VM failures are real; disk loss happens; one bad `apt upgrade` and you're restoring from a backup you hope works
- If a French plumber's customer data disappears because your cron job failed, "but it's on OVH" won't comfort anyone

Debate 9 rationale:
- Supabase Frankfurt addresses EU concern
- "Toutes les données sont sur OVH" is a sales differentiator
- No DPA, no SCCs, no trust exercise with a third party

### Resolution

**UNRESOLVED — Strong challenge, not yet resolved**

The operational burden argument is serious. A 3-person startup cannot do real DevOps/SRE while also shipping product. The "no migration debt" framing may be wrong — permanent operational debt is arguably worse than a one-time migration.

**Compromise path:** OVH Cloud SQL (managed Postgres, not bare VPS) — same "données en France" sales story, zero server maintenance. Free tier to start, scales with revenue.

**Key insight:** "Data sovereignty" and "operational control" are not the same as "no operational burden." Self-hosted means self-operated.

---

## Debate 14: Kanban vs Client Timeline — Core View

### The Disagreement

- **Product Strategist (challenging):** "Kanban is a developer fantasy dressed up as a feature. Artisans don't think in pipeline stages."
- **Debate 7 Resolution:** "Kanban pipeline is essential — 4 fixed columns (Devis, Accepté, En cours, Terminé) as MVP."

### The Argument

Challenger's position:
- Marc (plumber) does half his quotes verbally and starts the job before writing the price — the "Devis → Accepté" flow is imaginary for him
- The real question is "I talked to Madame Dupont last Tuesday about her leak. Where are we on that?" — that's a client context question, not a pipeline stage question
- WhatsApp already wins because it has client context (all messages in one thread). You're competing with that, not with Trello
- Kanban forces a project management framework onto people who don't manage projects
- Jean-Pierre (55, tech-resistant) won't drag cards across columns — that's not how his brain works

Debate 7 rationale:
- Pipeline is the core differentiator vs. WhatsApp
- Visual > text list
- Sophie's team needs shared view

### Resolution

**UNRESOLVED — Kanban's value is being questioned at the foundation**

The client timeline argument is more authentic to how artisans actually work. But Kanban advocates would argue that visual pipeline = understanding of business health at a glance.

**Compromise path:** Client Timeline as home screen (reverse-chronological feed per client — calls, messages, quotes, jobs, notes). Kanban moves to a secondary "Jobs" tab — optional, not forced. Sophie's team can use it. Jean-Pierre doesn't have to.

**Key insight:** The pain point is "where did I leave off with this client?" not "what stage is this deal?" Timeline answers both. Kanban answers neither for solo artisans.

---

## Debate 15: Pricing — Cost-Plus vs ROI Anchor

### The Disagreement

- **Growth Strategist (challenging):** "€29/month solo tier is built on sand. It signals 'spare change' to artisans who think in daily rates."
- **Debate 2 Resolution:** "€29/month solo, €49 Pro, €79 Business — based on 'churn at €9 is 3x higher than €29'"

### The Argument

Challenger's position:
- The churn data ("3x higher at €9 vs €29") is from SaaS startups, not French artisans — wrong audience, wrong psychology
- Artisans think in daily rates (€150-300/day). €29/month = €0.97/day. That's a coffee. Spare change signals spare-change value.
- ROI math: artisan charges €50/hour, app saves 2h/week = €400/month in recovered billing time
- €89/month solo tier creates immediate perceived ROI of 4.5x — the conversion story becomes "this costs less than 2 hours of your time per month"
- €29 attracts bargain hunters, not professionals willing to invest in tools — wrong customer segment

Debate 2 rationale:
- Survey data: 40% would pay €9, 20% would pay €19, 10% would pay €29
- Churn at €9 is 3x higher than €29
- Target customer has €50k+ revenue

### Resolution

**UNRESOLVED — Strong challenge, significant pricing implications**

The ROI anchoring argument is compelling. €29 may be leaving money on the table AND sending the wrong signal simultaneously.

**Compromise path:** 
- Solo: €49/month (compromise between €29 and €89 — maintains accessibility, improves perceived value)
- Pro: €99/month
- Business: €149/month
- OR go full €89 solo based on the ROI math — test both with pricing experiments

**Key insight:** The real question isn't "what can we charge?" but "what value are we delivering?" €29 undersells both the product and the customer.

---

*Pulse update: 3 new debates (13, 14, 15), 2026-03-30T09:55:00Z*
