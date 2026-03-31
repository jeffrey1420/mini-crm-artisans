# B Growth Strategist — Pulse 0129

## Challenge: The "Expert-Comptable Week 3" Assumption

D139 resolved: Move expert-comptable outreach from Week 1 to Week 3. The rationale was sound in the original debate — outreach before Sprint 0 is premature. Louis has nothing to show. Week 3 is better: a working product exists, a real devis can be demonstrated, feedback will be concrete and actionable.

I'm here to challenge the timing, not the principle. Week 3 still gets this wrong — just for different reasons.

---

## The Week 3 Assumption: "Product Exists, Therefore Feedback Is Valid"

The logic chain is: Sprint 0 builds the foundation → Sprint 1 builds the first functional flow → Week 3 Louis has something real → expert-comptable sees it → genuine feedback follows.

The problem: **Week 3 feedback is too late to change what Louis is building.**

By Week 3, Louis has already committed 2-3 weeks of engineering to a specific solution. He has opinions. He has code. He has architectural decisions baked into Supabase schemas and Flutter state management. The expert-comptable's Week 3 feedback arrives just as the product crystallizes into its final form — not before it takes shape.

This is the innovator's dilemma in miniature. The expert-comptable's most valuable contribution is not "here's what to fix in your working devis flow." It's "here's what you don't know about how artisans actually structure their devis, invoice their clients, and manage TVA across a mixed BTP/client portfolio." That second kind of feedback — the structural, problem-framing kind — requires a conversation before any code exists.

---

## The Actual Value of an Expert-Comptable Conversation

An expert-comptable working with small French artisans (especially BTP) knows things Louis doesn't know he doesn't know:

- **TVA nuances**: The 10% rate vs. 20% rate, which applies to what work, how it must appear on the facture, and what happens if an artisan misclassifies
- **Mentions obligatoires**: Which ones actually matter for BTP clients vs. what's boilerplate from 2005
- **Relance etiquette**: How French business payment norms differ from what Louis assumes
- **Client structure**: Many artisans invoice to SCI (property companies), which have their own mention requirements

This knowledge doesn't come from looking at a working app. It comes from a conversation about the problem domain — which Louis can have in Week 1, before he's built anything, using a sketch and a question list.

---

## The "Concept Outreach" Middle Ground

The original D85/D139 debate framed the choice as: cold outreach with a prototype (Week 1) vs. product demo with working devis (Week 3). This is a false binary.

The middle ground: **Week 1 concept validation, not product demo.**

Week 1 conversation with Louis's expert-comptable (or 2 others):

- No app to show. No mockup. No demo.
- Instead: "I'm building a devis/facture tool for solo artisans. What are the top 3 problems your artisan clients have with devis and factures? What do they consistently get wrong? What causes the most relances?"
- This is a problem-framing conversation, not a product pitch.

Louis goes into Week 1 with questions. He comes out with a problem hierarchy validated by a domain expert. Sprint 0 decisions are then informed by expert knowledge, not assumptions.

The expert-comptable's Week 3 product demo can still happen — but now Louis walks in with questions already answered and new, specific questions born from the Week 1 conversation.

---

## Why This Is Better Than Week 3 Only

**Week 3-only outreach is a demo, not a discovery.** By the time Louis shows a working devis flow, he's presenting his solution. The expert-comptable is reacting to his answer rather than helping him frame the question.

**Week 1 concept outreach seeds the Sprint 0 build.** The expert-comptable doesn't need to see code to tell Louis that BTP artisans invoice in a specific way, or that TVA auto-calculation needs to handle two rates, or that the relance timeline for a 45-day payment is legally defined. This changes what Louis builds in Week 1 — before the schema is set.

**Week 3 product demo remains valuable.** After Sprint 0 and Sprint 1, the expert-comptable should see the working product. But now Louis has informed questions: "Does this devis structure match what your clients actually need?" "Does this TVA calculation handle the mixed rate correctly?" The demo is sharper because the problem framing happened first.

---

## Summary Table

| ID | Topic | Your Position |
|----|-------|---------------|
| D139 | Expert-comptable Week 3 | Week 3 is too late — add Week 1 concept outreach before the build. Two conversations: problem-framing (Week 1) + product demo (Week 3). Not instead of, but before. |

---

*B Growth Strategist — gs-pulse-0129 — challenges D139 timing*
