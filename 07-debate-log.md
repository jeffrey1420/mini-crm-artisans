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

## Debate 11 (REVISED): PWA First, Native Within 6 Months — Challenging Capacitor's Hidden Costs

### The Disagreement

- **Technical Architect (Capacitor from day one):** "Android push is unreliable, iOS push is impossible with PWA. Capacitor wraps web code in native shells — same codebase, same team, real FCM notifications."
- **Revised position:** "Capacitor's hidden costs outweigh its benefits at launch. PWA first, native within 6 months post-launch."

### The Argument

**1. Two app stores = two full-time support burdens from day one.**

Capacitor doesn't eliminate complexity — it adds a wrapper layer. You now have: web app bugs + iOS App Store review cycles + Google Play policy changes + native crash reporting + app store listing management. For a 3-person team shipping an MVP in 3 months, App Store review rejections (7-14 days) can kill your launch timing entirely. PWA deploys when you deploy.

**2. "Same codebase, same cost" is technically true and strategically false.**

Capacitor's hidden costs aren't engineering — they're operational: App Store screenshots (3 sizes × 2 platforms = 6 assets), update review cycles for every sprint, 1-star reviews from users who can't install on iOS 15, support emails about "is this app safe?" from Android users who found it on Google Play instead of your website. These are real hours that don't show up in the "same codebase" calculation.

**3. Push notifications as #1 retention driver is unproven for this audience.**

The assumption: "reminders that FIRE = product delivers value." But Jean-Pierre (55, tech-resistant) doesn't rely on push notifications — he relies on habit, phone calls, and WhatsApp. Push notifications are a SaaS retention mechanism borrowed from consumer apps. For artisans, the retention driver is likely "I got paid because the app reminded me to send the reminder" — which is a value/delivery story, not a notification reliability story. If the invoice gets sent because of in-app logic, not because of push, the notification is a nice-to-have, not the core promise.

**4. PWA push is improving — by 6 months post-launch, it may be sufficient.**

Web Push on Android Chrome has improved significantly. Safari now supports web push on iOS (16.4+). The gap is closing. PWA at launch with web push as a fallback is acceptable for an MVP. Native push via FCM/APNS can be the upgrade sold at 6 months when the team has bandwidth and real user feedback about notification reliability.

**5. The real retention lever is value delivery, not notification format.**

If a user receives a push notification but the invoice was already sent manually via WhatsApp, the notification didn't retain them — the value did. The product needs to be so embedded in the workflow that missing a push is painful, not just annoying. That workflow integration (client history, quote generation, invoice math) is what creates switching costs. A push notification on a low-engagement app is just noise.

### Revised Position

**PWA first (launch), native within 6 months (post-launch when revenue funds it).**

Rationale:
- Launch in 3 months without App Store dependency
- Web push notifications as bridge (improving, not perfect, but functional)
- Native push as paid upgrade story at 6 months — "get reliable push with our native app"
- 6 months of user data tells you WHICH notification failures actually caused churn
- Revenue from first 50 paying users funds the native development sprint

**Key insight:** "Capacitor is easy" underestimates the non-engineering costs. The question isn't "can we build it?" — it's "can we operate it at launch with 3 people and an MVP timeline?" The answer is no.

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

## Debate 13 (REVISED): OVH Self-Hosted Postgres — Operational Debt vs Migration Debt

### The Disagreement

- **Technical Architect (challenging):** "OVH VPS self-hosted Postgres isn't 'data sovereignty' — it's outsourcing your SRE team to no one."
- **Debate 9 Resolution:** "Self-hosted Postgres on OVH from day one — answers every compliance question, no DPA needed."

### Argument: Technical Architect Responds

The challenger raises a legitimate concern, but commits a critical error: **conflating "self-hosted" with "self-operated."** These are not the same thing. OVH Cloud SQL is a managed Postgres service — automated backups, monitored replication, security-patched OS layers, point-in-time recovery — operated by OVH's infrastructure team under a 99.99% SLA. That's not "no SRE team." That's hiring OVH's SRE team as your infrastructure operator, which is precisely what you're paying for with the managed tier. The challenger's framing assumes bare VPS is the only interpretation of "OVH self-hosted." It isn't.

The challenger's second assumption is that a 3-person team cannot absorb operational overhead. This underestimates what a well-scoped managed service actually covers. OVH Cloud SQL handles: automated pg_dump + point-in-time recovery (tested, documented, not a cron job you wrote at 2am), OS security patching without downtime, database parameter optimization and version upgrades, and storage scaling without manual LVM manipulation. The team still writes application code. They do not become DBAs. The operational burden comparison to bare VPS is not "slightly less" — it's categorically different. Bare VPS is DIY DevOps. OVH Cloud SQL is the managed service equivalent of Supabase, but on French infrastructure, under French jurisdiction, with the same "données en France" sales story.

There is a deeper flaw in the challenger's logic: **Supabase was the original recommendation for exactly the operational simplicity being demanded now.** The reason Technical Architect originally chose Supabase (Debate 3) was: faster development, no server maintenance, real-time built-in, managed SLA. The only reason to walk that back was data sovereignty — "toutes les données sur OVH, en France" — which Supabase Frankfurt did not fully satisfy. OVH Cloud SQL satisfies the same sovereignty requirement without the operational debt. The compromise is not a retreat. It completes the original reasoning: keep the sovereignty win, eliminate the operational burden the challenger correctly identifies as unsustainable for a 3-person team.

**The compromise: OVH Cloud SQL (managed Postgres), not bare OVH VPS.** Same OVH France infrastructure. Same CNIL compliance story. Same "données hébergées en France, chez OVH." Zero server maintenance. The Debate 9 decision was directionally right (OVH over Supabase) but implementation was underspecified. Bare VPS was the wrong form factor for the operational reality. OVH Cloud SQL is the right one.

### Resolution

**RESOLVED — OVH Cloud SQL managed Postgres (not bare VPS)**

**Final decision:** Replace bare OVH VPS Postgres with OVH Cloud SQL managed Postgres. This resolves the challenger's operational burden argument while preserving the data sovereignty and CNIL compliance case that motivated Debate 9. The "self-hosted" language survives — data is still on OVH infrastructure in France. The "self-operated" burden does not.

**Key insight:** "Self-hosted" and "self-operated" are different choices. OVH Cloud SQL is self-hosted (data on your infrastructure provider) without being self-operated (OVH handles the SRE). This is the correct model for a 3-person team.

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

**RESOLVED — Client Timeline as Home, Kanban as Secondary**

The challenger's argument is the strongest voice in this debate, and it wins for the MVP. The core assumption to challenge: **the Kanban advocates are designing for the user they wish they had (Sophie) rather than the users they actually have (Marc and Jean-Pierre).**

Here's the critical flaw in defending Kanban as home: **Kanban answers "what stage is this deal?" but the actual pain point artisans describe is "where did I leave off with this client?"** These sound similar but aren't. A plumber doesn't think "I have 3 quotes in Devis stage." He thinks "I talked to Madame Dupont Tuesday, she's deciding, I need to follow up." That's a client memory question, not a pipeline question. Client Timeline answers both — it shows the full history in reverse chronological order, so you see exactly where you left off. Kanban only answers the pipeline question.

The second assumption to challenge: **treating all artisans as a homogeneous group.** Marc (solo plumber, verbal quotes, starts jobs before pricing) and Sophie (electrician with 2 employees, needs team coordination) are not the same customer. Kanban serves Sophie's team coordination needs excellently — it's the right tool for a growing business with employees. But the MVP's first 50 users are almost certainly Marc-like solo artisans. Designing the home view for Sophie while Marc is the beachhead customer is a product-market fit error. The fix isn't to abandon Kanban — it's to make it secondary and optional.

**Final decision:** Client Timeline is home (reverse-chronological feed per client: calls, messages, quotes, jobs, notes). Kanban lives in a secondary "Jobs" tab, visible but not forced. Solo artisans (Marc, Jean-Pierre) never see it if they don't want to. Growing teams (Sophie) can enable it for team coordination. Tap-to-move still works in the Jobs tab for those who want pipeline visibility.

**Why this resolves Debate 14:** The challenger's core insight — "the pain point is 'where did I leave off with this client?'" — is the right north star for the home view. Kanban is preserved as a feature for the right audience (teams), just not the default experience. This honors Debate 7's intent (keep Kanban in the product) while correcting its error (making it the home view for an audience that doesn't think in pipeline stages).

**Key insight:** Kanban is a team feature masquerading as a solo feature. It's essential for Sophie's business. It's friction for Marc's business. The MVP should optimize for Marc first, with a clear upgrade path for Sophie.

---

## Debate 15: Pricing — Cost-Plus vs ROI Anchor (RESOLVED)

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

### The Growth Strategist's Counter-Argument

I challenge the challenger's core assumption: **that artisans make purchasing decisions using explicit ROI calculations.** They don't. Tradespeople buy tools the same way they buy gas — when they need it, when it solves an immediate problem, when the friction of NOT having it outweighs the friction of trying something new. The "€50/hour × 2 hours saved = €400/month recovered" math is a Silicon Valley SaaS fantasy projected onto people who haven't run a spreadsheet since high school. Marc the plumber doesn't track his hours. He knows he's busy. He knows he's losing quotes because he can't follow up. That's the pain, not an abstract ROI model.

The challenger's second flaw is **ignoring competitive anchoring at higher price points.** At €89/month, Mini-CRM enters direct competition with Factomos (€49/month), Teamleader (€59/month starter), and dozens of established French SaaS tools with brand recognition, case studies, and sales teams. For an unknown product with zero social proof, €89 is a positioning disaster. You're not just charging more — you're positioning against established players without their credibility. €29, by contrast, is below the competitive threshold where price comparison even kicks in. It's a "let's see what this is" decision, not a "I'm investing in this tool" decision. That distinction is everything for initial adoption.

Third, and most critically: **the "ROI anchor" pricing strategy requires the ROI claim to be believable at signup.** The challenger's math assumes the app consistently saves 2 hours per week from day one. But this is an unproven, brand-new product with no case studies, no testimonials, and no track record. If you price at €89/month and tell prospects "this will save you 2 hours a week," you're making a promise you can't yet keep. When month one delivers only 45 minutes of value (because onboarding is still rough, because the artisan hasn't changed their workflow yet, because habits die hard), that €89/month subscription gets cancelled immediately — with resentment. €29/month gets more grace. More forgiveness. More "let me give it another month." For a new product finding its feet, that grace period is worth more than the perceived prestige of a higher price.

Finally, the challenger's own data is self-defeating. They cite the survey showing "10% would pay €29" — meaning 90% of prospects in that survey wouldn't pay €29. If only 10% say €29 is acceptable, what does that say about €89? The 90% who won't pay €29 won't suddenly reverse their psychology because you added a zero. The "daily rate thinking" cuts both ways: €89/month = €3/day = roughly 1/50th of a daily rate. That's still not "expensive." But it's also not "I'll take a chance on an unknown app."

### Resolution

**Decision: Keep €29/month solo tier, with ROI framing as an onboarding/nurture message, not a pricing anchor**

The €29 price stands for acquisition. The ROI story ("this pays for itself in under 2 hours of recovered time per month") should live in:
1. The onboarding email sequence (after signup, when commitment is formed)
2. The landing page's secondary proof section (below the fold, for skeptics)
3. Monthly usage reports ("You created 12 quotes this month — that's roughly 3 hours of admin time saved")

This approach:
- Keeps entry friction low for first-time triers
- Builds perceived value through demonstrated usage, not price tags
- Avoids competitive anchoring against established tools
- Gives the product room to deliver on its promise before demanding premium positioning

**Revised pricing tiers:**
- Solo: €29/month *(unchanged)*
- Pro: €49/month *(unchanged — the sweet spot between accessibility and value)*
- Business: €89/month *(up from €79 — this is the tier that benefits from ROI framing, because teams with 2-3 artisans ARE calculating team productivity)*

**Key insight:** You don't need to price at €89 to tell the €89 story. The ROI narrative is a conversion and retention tool — use it after signup, not before. Price low to win the trial. Prove value to earn the upgrade.

---

*Resolution: 2026-03-30T10:15:00Z | Resolved by: Growth Strategist specialist*

---

## Debate 16: Landing Page Angle — ROI ("Gagnez 2h/semaine") vs. Simplicity ("Simple comme WhatsApp")

### The Disagreement

- **Position A (ROI-first):** "The landing page should open with the value proposition: 'Gagnez 2 heures par semaine.' Artisans are busy — lead with what they get, not what it is. The ROI frame makes the price feel trivial."
- **Position B (Simplicity-first):** "Artisans are skeptical of SaaS promises. 'Gagnez 2h/semaine' sounds like every other tech product that overpromises. Lead with simplicity: 'Simple comme WhatsApp, conçu pour les artisans.' Trust is built through familiarity, not math."

### The Argument

Position A (ROI-first) concerns:
- The product solves a time scarcity problem — lead with the solution
- €49/month is easier to justify when framed as "less than 2 hours of labor per month"
- Competitors use ROI framing (Sage, Teamleader's French ads) — it's proven in this market
- The 30-day trial means users need a reason to commit — ROI is that reason

Position B (Simplicity-first) concerns:
- French artisans are notoriously resistant to new tech tools — overpromising triggers skepticism
- WhatsApp is the baseline UX expectation — comparing favorably to it is concrete, not vague
- "2h/semaine" sounds like a sales pitch; "simple comme WhatsApp" sounds like a product that respects their intelligence
- The product's real differentiator vs. WhatsApp is organization, not productivity metrics — that's a harder story to tell in a headline

---

*Pulse update: Debate 15 resolved, Debate 16 opened 2026-03-30T10:15:00Z*

---

## Debate 16 — Landing Page Angle: Product Strategist's Challenge to Position B

### Position: Against Simplicity-First ("Simple comme WhatsApp")

**1. You're competing with free, and you just told them about it.**
"Simple comme WhatsApp" is a comparison to a *free* app. You've just told a craftsman your €49/month tool is "like WhatsApp." That's not a value prop — that's surrender. The simplicity claim had better mean something more than "feels familiar." If the headline implies the product's only advantage is being WhatsApp-adjacent, you've invalidated the price before you've made the sale.

**2. Simplicity is table stakes, not a benefit.**
Nobody buys a tool because it's "simple." They buy because something painful stops happening. The buying trigger is emotional: "I just lost Madame Martin's phone number AGAIN." That pain is not complexity — it's consequence. "Simple comme WhatsApp" describes the interface. "Gagnez 2h/semaine" describes the relief. One answers a feature question nobody asked. The other answers the pain that opened the browser tab.

**3. "Simple" attracts the wrong customer.**
Position B says artisans are skeptical of SaaS promises. True. But "simple comme WhatsApp" doesn't filter for skeptical artisans — it filters for low-commitment users who want the cheapest-looking option. ROI framing attracts professionals who have budget authority and intent. At €29-89/month, you want the artisan who sees a tool, not the artisan who's comparing free apps.

**4. The new angle for Position A: Specificity + Control.**
"Gagnez 2h/semaine" is directionally right but too vague. Here's the upgrade: *specificity signals credibility*. "Gagnez 1h48 par semaine" (€49 ÷ €25/hr) sounds measured, not marketing. It sounds like someone actually did the math. And the deeper emotional frame is **control**, not efficiency: "Reprenez le contrôle de vos devis et factures" speaks to the feeling artisans describe — they're not "inefficient," they're *overwhelmed*. Control is aspirational. Efficiency is a spreadsheet.

### Proposed Landing Page Bridge

> **Headline:** "Gagnez 2 heures par semaine sur vos devis et factures"
> **Subhead:** "L'outil de gestion conçu pour les artisans qui en ont ras-le-bol de courir après leurs clients — sans复杂多余的功能"

**Why this works:** "2 heures par semaine" is the ROI hook. "Ras-le-bol de courir" hits the emotional trigger ("lost Madame Martin's number again"). Simplicity is implicit in the product story — you don't need to announce it in the headline. Let users discover "c'est simple comme WhatsApp" in the onboarding, not in the headline.

---

*Debate 16 contribution: Product Strategist — 2026-03-30T10:19:00Z*

---

## Debate 16: Home View — Client Timeline vs. Dashboard (Stats-First)

### The Disagreement

- **Client Timeline (following Debate 14 resolution):** Home = reverse-chronological feed per client (calls, messages, quotes, jobs, notes). The question answered: "Where did I leave off with this client?"
- **Dashboard (challenger position):** Home = stats dashboard showing business health at a glance (quotes sent this month, acceptance rate, revenue pipeline, jobs completed).

### The Argument

Client Timeline position (following Debate 14):
- Home should answer the artisan's primary question: "What happened last with client X?"
- Timeline is familiar — it works like WhatsApp, email, SMS — all already in their workflow
- Stats dashboards are a manager's tool, not an artisan's tool
- The product's primary value is "never lose track of a client" — Timeline delivers that directly

Dashboard position (challenger):
- Once you have 10+ active clients, you need to know "which clients need attention?" not just "what happened last?"
- Stats give the business a pulse — quotes sent vs. accepted, revenue this month vs. last month
- A dashboard creates a "command center" feeling — the product becomes indispensable rather than just organized
- Sophie's team (2+ employees) needs to see aggregate business health, not just individual client histories
- A stats-first home could show: pending quotes aging >7 days, jobs scheduled this week, clients not contacted in 30+ days

### Key Tension

**The "organizer" vs. "optimizer" product identity.** Mini-CRM can either be:
- **Organizer:** "Never lose track of a client" — Timeline home, simple, WhatsApp-like
- **Optimizer:** "Understand and grow your business" — Dashboard home, stats-forward, business-intelligence-lite

These aren't mutually exclusive forever, but the home view choice shapes the product's first impression and its core value proposition in the user's mind.

### Two Positions

**Position A — Client Timeline home:** Simple, familiar, answers the immediate "where did I leave off?" question. Lower cognitive load. Better for solo artisans (Marc, Jean-Pierre). Organizer identity.

**Position B — Dashboard home:** Business health at a glance. Identifies clients needing attention. Better for growing businesses (Sophie) and users who want to optimize. Stats create stickiness through "I need to check this" daily habit. Optimizer identity.

---

## Debate 16 (ADDENDUM): Dashboard Challenger — Growth Strategist Position

### The Challenge

I'm challenging the Client Timeline home decision from Debate 14. Here's why the Dashboard wins on retention math alone.

**1. WhatsApp familiarity is a ceiling, not a selling point.**

Yes, artisans know WhatsApp. That's also the problem — if your product feels like WhatsApp, why pay €29/month? You're not competing with "nothing." You're competing with "the thing they're already using for free." Familiarity doesn't create desire. It creates a low-expectation commodity trap.

**2. Client Timeline is a passive tool. Dashboard creates a daily habit.**

Timeline answers "what happened with client X?" — you open it when you remember. Dashboard answers "what needs my attention TODAY?" — you open it every morning because it's useful. A plumber checks his phone before leaving for jobs. If Dashboard shows "3 quotes awaiting response >7 days," that's the trigger. Timeline shows you an archive. Dashboard shows you work. The retention math flips entirely when the app becomes a daily command center instead of an historical log.

**3. Proposed minimal solo artisan Dashboard (not a BI tool — 4 things only):**
- **"À suivre"** — clients with open quotes >5 days, no response
- **"Relances dues"** — overdue invoice reminders (the core paid feature)
- **"Devis en attente"** — quotes sent, awaiting accept/refuse
- **"Ce mois-ci"** — revenue this month vs. last month (1 number)

That's it. Not a analytics dashboard. Just "here's what needs attention right now."

**4. The retention math changes completely.**

With Timeline home: artisan opens app when they remember → sees client history → closes app. No urgency, no habit, no "I need this tomorrow." With Dashboard home: artisan opens app every morning → sees 2 things need attention → acts → product proves its value daily → churn drops. Habit formation is the only durable moat for a solo artisan SaaS at €29/month. Dashboard builds habit. Timeline doesn't.

**5. "Never lose track" is solved by BOTH — but Dashboard also solves "never miss an opportunity."**

Client Timeline delivers on "never lose track." Dashboard delivers on that AND "never miss a follow-up." A €29/month tool that only organizes is a digital filing cabinet. A €29/month tool that shows you what needs action TODAY is indispensable. That's the difference between an app they keep and an app they open.

---

*Growth Strategist challenger position added: 2026-03-30T10:19:00Z*

---

## Debate 16: External Review — Full Pivot Required (RESOLVED)

### The Challenge

External reviewer (Louis shared the repo for review) gave a brutal but accurate assessment:

**Problems identified:**
- "Planning archive" with no shipped product — personas and pricing from assumptions, not observation
- Architecture internally contradictory (Supabase vs OVH per-customer vs managed Postgres)
- Wrong trigger: artisans buy admin relief, not a CRM identity
- Target too broad: can't serve Marc solo AND Jean-Pierre with secretary AND Sophie's team in one MVP
- Some artifacts synthetic ("客户", "记录") — lowers confidence in research rigor
- Sector under pressure (3.8% decline) = brutal price sensitivity
- Per-customer VPS at €29/month is gross overengineering

**Key quote:** "The opportunity is real. The current plan is mostly elaborate procrastination."

### The Response

All agents reviewed and accepted the critique. The core mistakes:

1. **Wrong positioning:** "CRM for artisans" sounds like enterprise software they don't want
2. **Wrong scope:** Tried to be everything to everyone
3. **Wrong architecture:** Per-customer VPS is insane at €29/mo price point
4. **Wrong evidence:** Personas written from assumptions, not field observation

### Resolution

**Full pivot executed:**

1. **Positioning:** "Devis, factures, relances" — not CRM
2. **MVP:** 4 things only — client file, quote, invoice, reminder
3. **Persona:** Marc only (solo smartphone-native artisan) — Jean-Pierre and Sophie are post-launch
4. **Stack:** Single managed Postgres (OVH) — not per-customer VPS
5. **Trigger:** Sell admin pain relief — not pipeline management
6. **E-invoicing:** Make it a v2 feature with Chorus Pro compatibility
7. **Real discovery:** Go watch 10 artisans before building more docs

### Key Insight

The market is viable (Tolteck: 33k users at €25/mo, Obat: 31k users). The product plan was not.

**The agents that wrote 1,700 tasks were solving the wrong problem. Field research > document planning.**

---

*Last updated: 2026-03-30T10:17:00Z — External review applied, full pivot*
