# Debate Challenge: SEPA Direct Debit Is a Conversion Killer in Disguise

**Challenging:** The implicit assumption that SEPA direct debit is a French-specific trust mechanism that aids conversion at signup. It has never been debated. It should be.

---

## The Assumption

Unchallenged premise: French artisans trust SEPA direct debit more than card payments because it's embedded in their banking relationship. Therefore, offering SEPA at signup creates trust → conversion.

This assumption appears nowhere in the debate log. It's been carried forward from conventional French SaaS wisdom without examination.

---

## Why SEPA Is Wrong for This Acquisition Context

### 1. The mandate process adds friction at the worst possible moment

The SEPA direct debit mandate process requires:
- Artisan provides IBAN (off the top of their head? On mobile? At 9pm after a long day?)
- Mandate is submitted → bank validates → SEPA mandate activated (1-5 business days typically)
- First charge hits after mandate is validated

For a tool positioning itself as "Sans vous prendre la tête," asking Marc to navigate his bank's SEPA mandate flow during signup is a catastrophic irony. The very first interaction with the product asks him to do administrative work — exactly what he's trying to escape.

Stripe's card flow: enter card number → done. 30 seconds. No IBAN lookup. No mandate waiting period.

### 2. "Trust signal" is conflated with "familiar ritual"

Proponents confuse "SEPA is how French people pay subscriptions" with "SEPA creates trust for a new tool." These are different things.

SEPA is familiar for recurring, predictable payments — gym memberships, phone plans, energy bills. These are established relationships where the merchant has already been trusted. SEPA mandate signing for an unknown SaaS tool from an unknown vendor is not a trust signal — it's a commitment request from someone who has no evidence the product will deliver.

Stripe card payment for a new SaaS tool is also unfamiliar — but it's faster, reversible (chargebacks exist), and doesn't require the artisan to find his IBAN and fill out a mandate form.

### 3. The GTM doc itself says "Stripe" — and then stays silent on SEPA

The Month 0 checklist reads: "Payment via Stripe (Lyf/CB later)." That's it. No SEPA mandate process. No discussion of payment provider strategy. The implementation plan defaults to Stripe without debate — which is exactly right. But the SEPA-as-trust-signal assumption was never challenged to understand why it wasn't included.

### 4. SEPA creates false confidence in churn risk

SEPA direct debit makes cancellation harder — which sounds like a retention feature. In reality, for a tool where Marc hasn't yet felt value, harder cancellation means one thing: resentment. He'll forget to cancel, get charged, call the bank to reverse, and leave a negative review. "C'est fait pour me piéger" is exactly the French artisan suspicion of SaaS that D43/D46 correctly identified.

Stripe's card flow makes cancellation frictionless — which paradoxically makes Marc more willing to try. Low-friction cancellation with a satisfaction guarantee is more trustworthy than a SEPA mandate that locks him in.

### 5. The timing is backwards

SEPA direct debit could be a genuine trust signal at renewal — when Marc has been using the product for 3 months, understands its value, and the SEPA mandate is a signal of long-term commitment. "Je reste car ça marche" expressed via continuing SEPA mandate.

At signup, it's a commitment asked before value is proven. That's the wrong moment for commitment.

---

## Proposed Resolution

**Payment flow at launch: Stripe card only. No SEPA at signup.**

Design decisions:
1. Stripe Checkout (card) as sole payment method at launch — fastest time-to-paid
2. SEPA as optional payment method offered post-signup, after Marc has experienced the product (Month 2+ renewal touchpoint)
3. Lyf/CB (French mobile payments) as a secondary option to investigate — both solve the "no card" problem for unbanked or card-averse users but without mandate friction
4. "Compte bancaire requis" is a localization message that should appear in settings, not in the signup flow

**The simplicity positioning demands payment friction of zero at signup. SEPA mandate process violates this directly.**

---

## What Winning Looks Like

If this challenge is accepted: Payment provider debate is opened. The implementation defaults to Stripe card-only at launch, with SEPA deferred to post-conversion retention. Lyf/CB added as French-market alternative.

If this challenge is rejected: The burden of proof is on proponents to show that the SEPA mandate process (IBAN lookup + mandate signing + validation wait) does NOT add friction at the exact moment we're trying to convert a skeptical artisan who's never heard of us.
