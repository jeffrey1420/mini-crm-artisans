# Position Paper: Product Strategist
**Pulse:** 0228-product  
**Author:** Product Strategist Specialist  
**Date:** 2026-03-31

---

## Challenge Statement

D96 established "first paid facture" as the hard conversion gate for Path A. I challenge this assumption as prematurely constraining for v1. Requiring a *paid* invoice as the conversion trigger stacks at least three independent behavioral changes — changes that may never happen for a meaningful segment of French artisans who operate on cash, check, and bank transfer cycles entirely outside the app's payment infrastructure.

---

## Core Arguments

- **The payment layer is a future feature, not a v1 assumption.** If digital payment processing (Stripe, Lydia, Pix) isn't in the MVP scope, then gating conversion on "paid" means Path A never triggers for cash-and-check artisans. That's a significant portion of the target market locked out of conversion forever, not temporarily.

- **"Accepted devis" is the moment of committed intent.** When a client says yes to a quote, the artisan has won the job. They've made a business decision backed by a client's verbal or written agreement. This is qualitatively different from any earlier onboarding action — it's the first proof that the tool is producing real business outcomes, not just busywork.

- **Emotional investment peaks at quote acceptance, not payment.** The artisan's "aha moment" comes when they land a job through the app. Payment is an administrative follow-through, not the value moment. Converting on accepted devis aligns the trigger with genuine product value delivery.

- **Three active clients managed filters for real usage, not vanity metrics.** Requiring 3 active clients alongside accepted devis ensures the artisan isn't just entering one-off data but actively managing a portfolio. This dual condition (accepted devis + 3 clients) is a more robust signal of habit formation than a single payment event that could be anomalous.

- **Path A and Path B should measure the same underlying behavior from different angles.** Path B uses behavioral proxies (days, jobs logged, clients managed). Path A should be no different in principle — "paid facture" just happens to be a *payment* proxy, which introduces external dependencies the product team cannot control or assume.

---

## Implication for Sprint 0 and Conversion Design

**Sprint 0 should ship with the conversion trigger as "first accepted devis + 3 active clients managed" for Path A.** This keeps the conversion signal entirely within the product's control and doesn't assume a payment infrastructure that may not exist in v1.

Conversion design should surface the accepted devis moment prominently — perhaps a congratulations screen, a "your first job won" celebration micro-interaction, and a clear prompt to add two more clients to unlock the full product. This creates a natural progression ladder: 1 accepted devis → 3 clients → (future) first payment → fully converted power user.

The Path B fallback (45 days / 7 jobs / 5 clients) remains unchanged and serves as the behavioral long-tail conversion path for users who engage without formal devis acceptance.

---

## Verdict

**D96 should be revised:** Replace "first paid facture (hard gate) for Path A" with **"first accepted devis + 3 active clients managed" as the Path A conversion trigger.**

The payment requirement should be moved to a post-v1 enhancement — either as a premium tier signal or as a Path A refinement once payment processing is natively integrated. Gating conversion on an external financial event that a significant portion of French artisans will never perform through the app is a conversion-killing assumption for v1.
