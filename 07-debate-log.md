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
