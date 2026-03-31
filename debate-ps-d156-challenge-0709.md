# POSITION PAPER: Product Strategist
**Challenge to D156 — Sprint 0 Does Not Require Prior WTP Validation**
**Date:** 2026-03-31 | **Author:** Product Strategist (subagent) | **Session:** ps-d156-challenge-0709

---

## Challenge Headline

**D156 is Wrong: Sprint 0 and WTP Validation Are Parallel Tracks, Not a Sequential Gating Mechanism**

D156 argued that WTP must be validated before Sprint 0 begins. This creates a false dependency that delays shipping a testable product by 1-2 weeks for gain of zero additional confidence. Louis does not lack price certainty — he lacks a product to show anyone.

---

## Assumption Challenged

**Assumption (D156):** "Sprint 0 cannot start until WTP is validated. Without confirmed willingness-to-pay at €29, we risk building features for a product nobody will buy."

**Why This Assumption Is Wrong:** WTP validation is a *product question*. Sprint 0 is a *technical foundation*. These are independent workstreams. Blocking engineering on market research produces the worst outcome: delayed shipping + unvalidated assumptions anyway.

---

## Core Arguments

### 1. Sprint 0's Deliverables Are Tech-Stack Decisions — Price-Independent

Sprint 0 builds:
- React Native mobile app shell
- Supabase backend (auth, database schema, RLS policies)
- Free-tier usage limits (e.g., 3 devis, 3 factures)
- Upgrade flow UI stub (free → paid)

None of these depend on whether the paid tier costs €19, €29, or €49. The *conversion mechanism* is identical regardless of price point. The UI copy, the Stripe price ID, the webhook handler — these are Sprint 1+ work. Sprint 0 establishes the *structure* into which any price can be plugged.

### 2. Stripe Integration Is Not a Sprint 0 Deliverable

The billing integration — Stripe checkout, subscription management, invoice generation — is explicitly out of Sprint 0 scope. Louis himself identified this. You cannot validate WTP *for Stripe* in Sprint 0 anyway because Stripe isn't being built yet. This alone dismantles the sequential dependency: Sprint 0 has nothing to do with billing.

### 3. WTP Validation with 5 Beta Users Is Statistical Noise

A sample of 5 artisans cannot tell you whether €29 is the right price. It can only tell you whether 5 specific artisans at 5 specific moments in their business day said something about €29 in a hypothetical conversation. This is not market research. This is noise.

- Small-N qualitative WTP interviews have ±40% error bars minimum
- Hypothetical price questions ("would you pay €29?") systematically overstate actual conversion by 2-4x
- What you actually need: a working product, a real Stripe checkout, and real conversion data from real users with real money at stake

### 4. Price Sensitivity Research Without a Prototype Produces Hypothetical Answers

When you ask an artisan "would you pay €29/month for a devis/factures app?" without a prototype, they are answering a question about their imagination of the product — not the product itself. The delta between imagined value and actual value is enormous, especially for tools artisans interact with daily.

WTP validated *after* Sprint 0 means: "Here is the app. Here is what it does. Here is the upgrade screen. What do you actually pay?" That is a real signal. Sprint 0 *produces the artifact that makes WTP validation meaningful.*

### 5. Sprint 0 Produces the Testable Artifact — THEN WTP Validation Becomes Real

After Sprint 0, Louis has:
- A working mobile app running on his own device
- A real Supabase backend he can demonstrate
- A free-tier flow he can show to 5 beta artisans in person

Now WTP validation means: "Show them the app. Watch them use it. Ask them to pay." Watching a user attempt to hand over money is the only WTP signal that matters. Pre-Sprint 0 "validation" is theater.

### 6. The Real Blocker Is Not WTP — It's Louis's Fear That No Artisan Will Pay Anything

Louis set €29 without WTP data. He knows this. D156 tries to paper over this by demanding more research before building. But the underlying question is not "is €29 the right price?" The underlying question is **"will any French artisan pay for this at all?"**

That question is *only answered by shipping.* No survey, no interview, no focus group answers it. Sprint 0 is the fastest path to an answer. Every day spent on pre-Sprint 0 WTP research is a day not spent learning whether the product has legs.

---

## Verdict Proposal

**REVERSE D156.** Sprint 0 and WTP validation should run in parallel, not sequentially.

### Recommended Execution:

| Track | Sprint 0 (6.5 days) | WTP Validation (concurrent) |
|---|---|---|
| **Owner** | Louis (engineering) | Louis (user interviews) |
| **Deliverable** | Working mobile app on TestFlight | 5 in-person demos → real payment attempts |
| **Exit criterion** | App installs, auth works, free tier flows | "Will they hand over a credit card?" |

### What Sprint 0 Must NOT Do:
- Do not build Stripe integration
- Do not finalize price in UI copy (use a placeholder like "from €XX/mo")
- Do not wait for WTP results before starting

### What WTP Validation Must Produce to Block Sprint 0:
- Evidence that the product concept itself is dead (not just that the price is wrong)
- A direct contradiction from >50% of beta users that they would never pay for *any* version of this workflow

Anything less than "this entire category is DOA" is not a Sprint 0 blocker.

---

## Status

**DRAFT — Pending Louis Decision**

D156 must be formally contested. Louis must choose:
1. **Parallel track (recommended):** Start Sprint 0 now. Run WTP interviews concurrently. Let each inform the other.
2. **Sequential (D156 position):** Delay Sprint 0 by 1-2 weeks for WTP validation. Risk: no product to show at end of validation anyway.

The question is not "do we know the right price?" The question is "do we have a product worth pricing?" Sprint 0 answers that. WTP validation refines the price. These are not the same question.

---

**Filed by:** Product Strategist (subagent)
**Next action:** Awaiting Louis's ruling on parallel vs. sequential execution
