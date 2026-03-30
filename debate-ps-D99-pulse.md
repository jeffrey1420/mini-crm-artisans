# Product Strategist — Debate D99 Pulse

**Role:** Product Strategist, Mini-CRM (devis/factures for French artisans)
**Debate:** D99 — Per-devis pricing (€1.50/devis, capped €29/month) vs flat €29/month
**Pulse:** 2026-03-30T22:30
**Assumption Being Challenged:** That per-devis pricing is compatible with D96's "first paid facture" conversion trigger architecture — and that flat €29 is merely a simpler alternative, not a structurally superior choice at the conversion moment.

---

## The Assumption

Both sides of the D99 debate accept D96's conversion trigger architecture as given. The pro-per-devis side (D118) argues it removes "will I use this enough?" anxiety. The counter (D99 last position) argued flat €29 is simpler. Neither examined whether per-devis fundamentally conflicts with how D96 converts users.

The shared assumption: "first paid facture" = conversion moment, and per-devis pricing (€1.50/devis) simply determines how much they pay after converting. This assumption is wrong. Per-devis doesn't just determine the bill — it introduces a billing decision AT the conversion moment, which structurally undermines the conversion trigger itself.

---

## Argument

### Problem 1: Per-devis introduces metering friction at the peak conversion moment.

D96's conversion trigger is "first paid facture" — an emotionally charged event. The artisan has just been paid by a client. He used the product, sent a professional devis, the client accepted, the work was done, and money changed hands. This is the moment of maximum trust and investment in the product.

Per-devis pricing injects a billing micro-decision into exactly this moment: "Your first paid facture is in. That's €1.50 for this devis. Continue?"

This is not a feature — it is a churn trigger disguised as flexibility. The artisan is at peak emotional investment AND being asked to make a financial decision tied to a specific transaction. He's now calculating: "Do I want to pay €1.50 for THIS facture?" The answer may be no if the margin on that job was thin, or if the client only paid a partial amount.

Flat €29 converts the entire billing question into a single binary: "Do I want to continue using this product, yes or no?" One decision. Clean. The €29 is not tied to any specific transaction — it's tied to the product relationship as a whole.

Per-devis converts one decision into a metering exercise. For an audience that values simplicity above all ("Sans vous prendre la tête"), this is tonal whiplash at the worst possible moment.

### Problem 2: Per-devis creates a retroactive billing shock for Path B artisans.

D110 established a dual-path conversion model. Path B (verbal-agreement artisan) converts after 45 consecutive days of active product usage OR 7+ jobs logged — not at first paid facture. Under per-devis pricing, this artisan has been using the Free tier for 45 days, accumulating per-devis charges with no conversion event yet.

Here's the billing shock: At the 45-day trigger, he's suddenly presented with: (a) all past per-devis charges he thought were free under the Free tier, AND (b) the transition to either €1.50/devis going forward or €29/month flat. He's paying for usage he believed was free.

Under flat €29, the transition is clean: "You've been using the Free tier for 45 days. For €29/month, you get everything unlimited." No retroactive charges. No per-transaction accounting. No "you owe us €X for those 12 devis you sent."

Per-devis doesn't just create billing complexity — it creates a retroactive billing surprise that violates the trust built during the Free tier period. This is worse than flat €29 because it retroactively punishes usage the artisan thought was permitted.

### Problem 3: The D96/D99 reconciliation in D104 creates a billing-first product experience.

D104 attempted to resolve the D96/D99 conflict by aligning the billing trigger to the conversion moment: convert at limit-hit (5 active devis or 10 clients), activate per-devis billing immediately. The logic: "billing trigger and conversion trigger now aligned."

This creates a product where the first thing a new paying customer experiences is a billing event tied to their specific usage. The product becomes a meter rather than a service. The emotional arc of conversion — "this product helped me get paid, I'm going to keep using it" — is interrupted by a transactional moment: "that will be €1.50."

Flat €29 preserves the emotional arc intact. The first paying experience is: "I'm continuing to use a product I trust, for €29/month." No per-transaction friction. No metering.

---

## Proposed Resolution

Per-devis pricing's structural advantage (seasonality, pay-for-what-you-use) is real but timing is everything. The billing decision cannot coincide with the conversion moment — it must follow it.

**Flat €29 wins for v1.** Here's why the per-devis advantage is actually achievable through annual billing, not usage-based pricing:

1. **Seasonality is solved by annual billing.** French artisans on flat-rate annual plans pay €260 once, not €29 × 12. Low-season months are prepaid. This is the same cash-flow benefit as per-devis without the conversion-moment friction.

2. **The per-devis seasonality argument assumes artisans are making a fresh decision each month.** They are not. Annual billing converts the seasonality question to a single annual decision, which artisans in BTP already make for equipment leases, insurance, and subscriptions. One annual decision is not a burden — it's normal.

3. **Per-devis adds conversion complexity to solve a billing complexity problem.** The real issue (artisanal cash flow seasonality) is solved more elegantly by annual billing with a free tier that enables word-of-mouth before the annual commitment.

**Recommended pricing for v1:**
- Free tier (10 clients, 5 active devis) — no billing
- €29/month flat — simple, clean conversion
- €260/year annual — addresses seasonality, better unit economics, same cap as per-devis maximum

The per-devis model should be revisited in v1.2 — after we have paying users, after we've validated the seasonality concern is real, and after the conversion architecture is no longer sensitive to billing friction at the conversion moment.

---

## New Action Items for TODO.md

- [ ] **D99 UPDATED:** Flat €29/month + annual billing (€260/year) at launch. Per-devis (€1.50/devis, cap €29) deferred to v1.2. Rationale: per-devis conflicts with D96's conversion trigger architecture by introducing metering friction at the peak conversion moment.
- [ ] **D99 NEW:** Add annual billing (€260/year) as the seasonality solution — same maximum cost as per-devis cap, but clean conversion moment. Market this as "pay for the year, use it all year" not "per-devis with a cap."
- [ ] **D99 NEW:** Revisit per-devis in v1.2 after: (1) real user data on seasonality patterns, (2) conversion architecture validated with flat €29, (3) billing integration mature enough to handle per-transaction charging without friction at conversion.
- [ ] **D110 Path B billing clarification:** Path B artisans (verbal-agreement) who convert after 45 days must NEVER receive retroactive charges for Free tier usage. Any billing model must be prospective-only from the conversion date.

---

*Argument written: 2026-03-30T22:30*
