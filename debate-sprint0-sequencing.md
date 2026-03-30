# Debate 35: Sprint 0 — Schema-First vs Flow-First

**Challenge:** Debate 32 resolved D2 with "Sprint 0 = pure schema design" — design all types (clients, devis, facture, relance), TVA calculator, sequential numbering, mentions légales before any feature work. Technical Architect (original proponent) now challenges this.

### Technical Architect — Schema-First Produces Over-Engineered Types

**Core argument:** Designing a schema in isolation from real usage is over-engineering. You don't know which fields artisans will actually populate until you watch them try. "Big bang schema design" before any feature work produces types with fields that nobody uses — and those fields create maintenance burden, UI clutter, and migration cost forever.

**Why schema-first is the wrong approach:**
1. **Schema emerges from usage, not the other way around.** The devis creation flow will reveal which fields are actually needed. A client record might only need: name, phone, email. Do we need `client_type` (particulier/professionnel)? Only if the mentions légales renderer actually uses it — and we don't know that until we build the renderer and watch it in use.
2. **TVA multi-taux is known complexity — but it's a rendering problem, not a schema problem.** The TVA rates (5.5%, 10%, 20%) are known. The per-line calculation is known. But where in the flow do you capture it? On the line item, or on the total? You won't know until you watch someone create their first devis and struggle with where to enter "plomberie" and what rate applies.
3. **Time-to-real-feedback matters more than architectural purity.** A "minimum devis flow" (create client, create devis, send via WhatsApp) built in 3 days with a bare schema generates real feedback. Sprint 0's 5-day pure schema sprint generates... a schema document. Not user learning.
4. **The real risk of schema-first:** You spend 5 days designing sequential number enforcement, TVA breakdown tables, mentions légales templates. Then week 2, an artisan says "I don't do TVA, I'm below the threshold" — and your entire TVA schema is unused.

**The better model — Flow First, Schema Emerges:**
- Sprint 0: Build minimum viable devis flow. No TVA (flat rate ok for MVP). No sequential numbering enforcement (just auto-increment). No mentions légales complexity (simple text block, update later). Single-scaffold app: add client → add devis line items → preview → send via WhatsApp.
- Sprint 1: Extract what worked. Formalize schema based on actual usage. Add TVA calculator when you know which clients need it. Add mentions légales when you know which client types require what. Add sequential numbering when you know the legal risk.
- This compresses time-to-real-feedback by 1-2 weeks and produces a schema that matches actual usage.

**VERDICT:** Redefine Sprint 0 from "schema design" to **"build minimum viable devis flow (3-5 days, minimal schema, no TVA complexity, no sequential numbering, no mentions légales complexity)."** Schema formalization happens at Sprint 1, based on what was learned from Sprint 0 usage.

**Proposed Sprint 0 redefinition:**
- OLD: `Sprint 0: Design shared schema — client, devis, facture, relance types + TVA multi-taux calculator + sequential number generator + mentions légales renderer`
- NEW: `Sprint 0: Build minimum devis flow (add client → add line items → preview → send via WhatsApp). Minimal schema. No TVA complexity (flat rate ok). No sequential numbering enforcement. Simple mentions légales block. Goal: get in front of real users in 5 days, not architectural purity.`
