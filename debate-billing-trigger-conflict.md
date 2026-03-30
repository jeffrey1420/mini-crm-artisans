# Debate-Billing Trigger Conflict — D96/D68/D99 Resolution

**Strategist:** Product Strategist  
**Date:** 2026-03-30  
**Status:** Proposed Resolution

---

## What the Conflict Actually Is (Precisely)

Two decisions are in tension:

- **D96:** Conversion trigger = first paid facture (hard gate). Secondary soft trigger: 3+ sent devis with zero paid factures → gentle upsell prompt.
- **D99/D68:** Usage-based pricing = €1.50/devis sent, capped at €29/month. Declared "directionally superior" but flagged as unresolved pending implementation complexity check.

**The structural problem:** Under usage-based billing, you charge per action (devis sent). The conversion moment should be when the artisan begins generating that metered usage. But D96 says conversion happens at first *paid* facture — a client-dependent event that could occur weeks after the artisan first became a meaningful user.

Concretely, the misalignment:

| Day | Event | Usage-based billing | D96 conversion state |
|-----|-------|---------------------|---------------------|
| 1 | Signs up (Free tier) | €0 | Not converted |
| 8 | Sends 1st devis | €1.50 (if paying) | Not converted |
| 12 | Sends 2nd devis | €1.50 | Not converted |
| 18 | Sends 3rd devis | €1.50 | Soft prompt fires (3+ devis, no paid facture) |
| 25 | Client accepts, facture created | €0 | Still not converted |
| 32 | Client pays facture | €0 | **CONVERSION TRIGGERS HERE** |
| 32 | First bill issued | €1.50 × 4 devis? | First billing event |

Under this model, the artisan has sent 4 devis over 32 days before converting. They've been using the product meaningfully for a month. But their first billing event (€1.50 × 4 = €6) comes *after* a month of free usage. The usage-based model's value proposition — "pay only for what you use" — has been negated by D96's conversion gate, which delays billing until a client-payment event occurs.

**The core tension:** D96's conversion trigger was designed for a flat-rate model (convert → pay €29/month). Under usage-based, the conversion moment is also the first billing moment. These should be the same event. D96 makes them different events separated by weeks.

---

## The Assumption I'm Challenging

**Challenged assumption (from D96):** "The first paid facture is the right conversion moment because it marks genuine business value received."

This assumption is correct for a flat-rate SaaS where the conversion event is arbitrary (30-day trial expiry, hitting a limit). The first paid facture is a strong signal: Marc's client said yes, money is coming, this is real. Converting at that moment makes psychological sense.

**But it is wrong for usage-based pricing because it conflates two distinct events:**

1. **The moment Marc starts generating value for us** (first meaningful action = first devis sent)
2. **The moment Marc's client pays him** (first paid facture)

Under flat-rate pricing, these can both be conversion triggers because both are arbitrary gates — there's no per-use revenue implication. Under usage-based, conflating them creates a month of free usage before billing, which undercuts the model's core promise.

**The corrected principle:** Under usage-based billing, the conversion moment = first metered action (first sent devis beyond the free limit). The "first paid facture" is a milestone worth acknowledging, but it is not the billing trigger.

---

## Resolution Options

### Option A: Decouple Conversion Trigger from Billing Trigger

**Mechanism:**
- **Conversion trigger (upgrade prompt):** First paid facture (D96 hard gate) — unchanged. This is the *experience* moment when we ask for the upgrade.
- **Billing trigger (first charge):** End of the calendar month in which conversion occurs — OR first sent devis in the following month.
- Usage-based billing activates at conversion, but the first month's invoice = €1.50 × (number of devis sent since signup). Not €0 at conversion + retroactive billing.

**Trade-offs:**
- ✅ Preserves D96's conversion moment (first paid facture is still the right human moment to make the ask)
- ✅ Usage-based billing activates at conversion, not weeks later
- ✅ Artisans who send 8 devis before converting pay €12 that month, not €0 — aligns revenue with usage
- ❌ Retroactive proration on month-of-conversion is mechanically awkward
- ❌ First paid facture still gates the conversion event — engagement period before conversion remains free
- ❌ Complexity: tracking devis count from signup → conversion → billing cycle requires clean bookkeeping

**Complexity:** Medium-high. Proration + usage tracking + conversion event matching requires careful implementation.

---

### Option B: Change Conversion Trigger to First Sent Devis (Hard Gate), Keep Usage-Based Billing

**Mechanism:**
- **Conversion trigger:** First sent devis beyond Free tier (5th devis) — hard gate. Artisan hits 5 active devis → upgrade prompt fires.
- **Billing:** €1.50 × every subsequent devis sent. Capped at €29.
- First paid facture becomes a secondary touchpoint (celebration moment, not conversion gate). The 3-devis soft prompt from D96 moves to "3rd devis sent with zero paid factures → gentle nudge toward €29 unlimited."
- Free tier: 5 devis, 10 clients. Paying tier: unlimited devis at €1.50 each, capped at €29.

**Trade-offs:**
- ✅ Conversion trigger and billing trigger are the same event — clean, aligned, no gap
- ✅ Revenue starts immediately when usage crosses the free tier threshold
- ✅ Cap at €29 means power users pay the same as flat-rate — no penalty for high usage
- ✅ Removes dependency on client-payment chain (verbal agreements, repeat clients who never send new devis)
- ❌ "First paid facture" as a high-intent conversion moment is lost — this was D96's strongest insight
- ❌ artisans who never hit the free limit stay free forever — usage-based only generates revenue from power users
- ❌ Low-volume artisans (1-2 devis/month) pay €1.50-3/month — viable but trivial revenue per user

**Complexity:** Low. Per-devis billing on metered action. Standard metered SaaS pattern.

---

### Option C: Hybrid — Two Conversion Paths (Recommended)

**Mechanism:**
- **Primary conversion path (limit-hit):** Free tier limit (5 active devis OR 10 clients) → hard gate → upgrade to €29 unlimited OR €1.50/devis capped at €29. Artisan chooses at moment of upgrade.
- **Secondary conversion path (first paid facture):** When first paid facture event fires (client pays), offer the €29 unlimited plan as the "next step" for €29/month. Not a gate — a value prompt. "Your business is real now. Lock in full access."
- **Billing:** Usage-based from day 1 for paying users. Flat-rate for those who choose €29 unlimited.
- The 3-devis soft prompt (D96) remains for artisans who are engaged but haven't converted — but it now points to usage-based pricing, not flat-rate.

**Trade-offs:**
- ✅ Converts on limit-hit (clear, unambiguous trigger) OR on first paid facture (high-intent moment) — captures both power users and first-time converters
- ✅ Usage-based billing activates immediately when artisan chooses to pay (no gap)
- ✅ artisans who never hit the limit get to experience the product fully — no artificial scarcity
- ✅ The "first paid facture" moment is preserved as a soft conversion opportunity, not a hard gate — leverages D96's insight without blocking billing
- ✅ Simple mental model: "Hit the limit? Pay per use or flat rate. Got your first payment? Time to go pro."
- ❌ Two pricing options at conversion moment adds choice complexity — "per devis or flat?" could cause decision paralysis at the worst moment
- ❌ Requires clear UI explaining the difference at the moment of upgrade

**Complexity:** Medium. Two pricing options require comparison UI at upgrade moment.

---

## Recommended Resolution

**Adopt Option B with a modification — Conversion at free tier limit, usage-based billing from day one of paying status.**

The modification: retain the "first paid facture" as a *celebration moment* (not a gate) with a targeted upgrade prompt:

> "Félicitations — [Client] vous a payé. Votre outil de suivi devrait évoluer avec votre activité. Passez à €29/mois pour un accès illimité."

This captures the psychological power of D96's insight (first paid facture = "this is real") without using it as a billing gate.

**Why Option B over Option C:**
- Option C's "choose your plan at upgrade" moment introduces decision friction precisely when the artisan needs a simple next step.
- Option B's limit-hit conversion is cleaner: no choices, just "you've used 5 devis, here's what unlimited costs." Decision made before they hit the limit.
- The "first paid facture" soft prompt in Option B still captures the high-intent moment without making it a gate.

**The pricing architecture:**
- **Free:** 10 clients, 5 active devis. €0.
- **Pay-per-use:** €1.50/devis sent beyond 5. Capped at €29.
- **Unlimited:** €29/month. Devis unlimited. (First paid facture prompt offers this as the "full access" option.)

Under this model:
- Month 1 (4 devis sent): €0 (Free tier)
- Month 2 (8 devis sent): €1.50 × 3 = €4.50 (pay-per-use on 8th, 9th, 10th devis)
- Month 3 (15 devis sent): €1.50 × 10 = €15 (capped at 10 paid devis = €15, well below €29 cap)
- Month 4 (25 devis sent): €1.50 × 20 = €30, capped at €29

The artisan who sends 25 devis/month pays €29. The artisan who sends 3 devis/month pays €4.50. Cash flow alignment preserved. Revenue ceiling preserved. Conversion trigger aligned with billing trigger.

**Why not Option A:**
Option A's retroactive proration and month-boundary complexity creates billing edge cases that are confusing to explain and hard to debug. For an MVP targeting non-technical artisans, billing clarity > theoretical revenue precision.

---

## Action Items for TODO.md

1. **D96 UPDATED:** Conversion trigger = first free tier limit hit (5 active devis OR 10 clients). "First paid facture" becomes a soft conversion touchpoint (celebration + upgrade prompt), not a hard gate. The 3-devis soft prompt remains for engaged non-converters.

2. **D99 IMPLEMENTATION:** Usage-based billing activates at conversion (limit-hit). €1.50/devis sent beyond free tier. Capped at €29/month. First bill issued immediately upon upgrade.

3. **Billing UI:** At limit-hit upgrade moment, show two options: (A) Pay €1.50/devis (capped at €29) or (B) €29 unlimited/month. Default to (A) with a note "Most artisans start with per-devis — you can switch anytime."

4. **First paid facture moment:** When first paid facture event fires (for Free or paying users), trigger a "milestone" notification: "🎉 [Client] vous a payé! Votre activité est réelle. Débloquez le suivi complet →" linking to upgrade page. Not a hard gate — a value prompt.

5. **D68 RESOLVED:** Usage-based (€1.50/devis, cap €29) at launch. Flat-rate option (€29 unlimited) as alternative at conversion moment. Both capture the seasonal cash flow benefit — low-activity months = low bill, high-activity months capped at €29.

6. **U15 REFINEMENT (Debate 101):** "Support Prioritaire" (direct WhatsApp to Louis) remains the primary retention hook for paying users. Usage-based pricing makes this more valuable: "You're on €4.50/month — if you need anything, I'm here."

---

## Summary Table

| Decision | Current | Proposed |
|----------|---------|----------|
| D96 Conversion trigger | First paid facture (hard gate) | Limit-hit (5 devis OR 10 clients) as hard gate; first paid facture as soft milestone prompt |
| D99 Usage-based billing | €1.50/devis, cap €29 (directionally resolved) | Confirmed — activates at conversion, not at calendar month |
| D68 Pricing model | Usage-based (open) | Usage-based (€1.50/devis, cap €29) + flat-rate alternative (€29 unlimited) at conversion |
| Billing trigger alignment | Misaligned (conversion → billing gap of weeks) | Aligned (conversion = first paying action) |
