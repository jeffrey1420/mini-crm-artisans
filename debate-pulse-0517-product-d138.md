# PS-0517: Eliminate Annual Billing Entirely at Launch
**Position: D138 ELIMINATED — Monthly €29 ONLY. Annual deferred to v1.2.**
**Author: Product Strategist**
**Date: 2026-03-31T05:17**

---

## The One-Sentence Position

Ship one SKU at launch: €29/month. Annual €240 is a v1.2 retention product, not a v1 launch SKU.

---

## Argument 1: Monthly Only at Launch Is the Correct Decision for a Product Without PMF

We have zero paying users. We have zero retention data. We have a six-day Sprint 0 timeline and a hypothesis that French artisans will pay €29/month for better devis and facture management.

Adding annual billing at launch means building pricing infrastructure, cohort analytics, churn logic, and accounting entries for a product tier we have not validated. Not because the engineering is hard — Stripe makes annual subscriptions trivial — but because every pricing model we build before PMF is a model built on guesswork.

When Louis has 50 paying monthly users in Month 3, he will know something he does not know today: what the actual annual retention curve looks like. That knowledge is what determines whether annual billing is a good product for this user base. Offering annual at launch to users we haven't retention-tested means we're pre-committing to a pricing structure before we understand who we're pricing it for.

The correct sequence is: validate monthly retention first, then add annual as a retention and LTV tool for users who have already proven they stay.

---

## Argument 2: The "Predictability" Assumption Is Unvalidated for This Cohort

The debate log contains an implicit assumption: "Some artisans prefer annual billing because it provides predictability." This assumption has never been validated with actual French artisans.

Let me challenge it directly.

What kind of predictability are we talking about? Budget predictability — knowing the tool costs €240/year rather than facing a monthly line item? Or usage predictability — knowing the tool will remain relevant throughout the year?

For budget predictability: the artisan who wants €240/year predictability is already thinking annually. That artisan will self-select for annual when offered at Day 30. The artisan who thinks in monthly cash flow cycles — which is most sole traders and small artisans — does not want budget predictability. They want low-commitment, low-cash-out options. Offering them annual at checkout introduces friction they didn't ask for.

The assumption that "predictability is broadly desired" is doing a lot of work in the GS position. It maps a SaaS industry convention onto a user base we haven't studied. Every SaaS offers annual because it improves LTV and reduces churn. That doesn't mean users are asking for it. It means providers find it useful to offer it.

If Louis has spoken to five artisans and three of them said "I prefer annual because X," then the predictability assumption is grounded in evidence. If not, it's an assumption dressed as product wisdom.

Monthly-only at launch tests whether artisans will commit to a monthly relationship with this product. That is the fundamental question. Annual billing answers a different question: "Once committed, will they deepen the relationship?" We cannot answer the second question until we've answered the first.

---

## Argument 3: The Competitive Risk From Tolteck/Obat Annual Pricing Is Real But Irrelevant at Launch

GS-D153 raises a legitimate concern: if Tolteck or Obat enters with €20/month annual pricing, Louis appears to charge more in peer conversations and cannot match the referral story ("I pay €20/month, all year").

This is a real competitive dynamic. It is also irrelevant to the launch decision.

Here is why. The competitive framing assumes Louis and his competitor are competing for the same prospect at the same moment. They are not.

At launch, Louis is not competing with Tolteck's pricing page. He is competing with the inertia of "I'll figure out my devis management someday." His conversion challenge is not "am I cheaper than Tolteck?" It is "does this artisan care enough about devis management to pay anything at all?"

Monthly €29 lowers the commitment barrier to the lowest defensible point. It says: "Try this for one month. If it works, stay. If it doesn't, leave." The competitive pricing conversation happens after the artisan has experienced value — which is exactly when Louis should introduce the annual upsell.

If Louis launches with annual billing and a competitor is advertising €20/month, Louis's problem is not the annual pricing. His problem is that he's trying to close a high-commitment sale against a low-commitment prospect. Monthly-first fixes this. Annual-first amplifies it.

The Day 30 annual upsell — offered to users who have already experienced 30 days of value — is categorically stronger than annual-at-checkout against competitive pressure. A user who knows the product and sees €108 savings is a user who converts. A user at checkout comparing €29/month to a competitor's €20/month is a user who hesitates.

---

## Argument 4: Day 30+ Annual Is Not "Annual Billing With a Different Name." It Is a Different Product.

GS-D153 argues: "Day 30 upsell framing is categorically different from annual-as-default. It is annual-as-retention-offer." And then concludes: "Therefore, we should offer annual at checkout as opt-in."

This logic does not follow.

If the Day 30 upsell is the right mechanism — annual offered only to users who have experienced 30 days of value — then the correct product decision is: do not offer annual at checkout. Offer it at Day 30.

GS-D153 is using the quality of the Day 30 upsell to justify the existence of annual billing. That is correct. But they are then using the existence of annual billing to justify offering it at checkout. Those are two different decisions.

The Day 30 upsell argument is actually my argument, not GS's. GS is saying: "Annual should be introduced after value is established." I agree. That is exactly what I am proposing with the v1.2 annual introduction. The disagreement is whether annual should ALSO be available at checkout from Day 1.

My position: no. The checkout page is not the right place for a product we have not validated with our users. The Day 30 upsell screen is the right place — because at Day 30, we know three things we do not know at checkout:

1. The user has opened the app at least once in 30 days
2. The user has created a devis or facture (the product delivered a workflow outcome)
3. The user has not already churned

These three conditions make the Day 30 user the right candidate for annual. The Day 0 visitor is a stranger making a first-time commitment decision with incomplete information. These are fundamentally different decision contexts, and conflating them by offering annual at both is what creates the confusion in the GS position.

---

## Challenging the Prior Assumption: "Both Billing Models Mask Seasonality Equally"

GS-D153 argues: "Annual cohort analysis gives a calendar anchor that makes seasonality correlation visible. Monthly churn lacks this internal reference."

I challenge this directly.

Monthly churn fires when the customer leaves. If a customer cancels in August, Louis sees "cancelled in August." He can immediately investigate: follow up, look at usage data, notice a pattern. The signal is immediate and local.

Annual cohort data does not fire until renewal. A customer who uses the product lightly for 8 months and decides in Month 9 that it's not worth renewing looks identical to a customer who used it heavily for 8 months and left for pricing reasons. Both churn at the annual boundary. The annual cohort data cannot distinguish between "product didn't deliver value" and "product delivered value but I can't afford €240 right now." Monthly churn can distinguish between these — if a customer cancels in their second month, that's a value signal. If they cancel in month 11, that's a different signal.

The "calendar anchor" that GS-D153 praises is also a blind spot. Annual cohort analysis shows you when customers leave at renewal boundaries. It cannot tell you when customers silently disengage during the year. Monthly churn catches silent disengagement. Annual cohort analysis misses it until the annual boundary.

More fundamentally: Louis does not need a sophisticated cohort analytics system to understand his early users. He needs to talk to them. Five artisans who cancelled in their second month is more actionable than a cohort table showing renewal rates. The "annual gives better analytics" argument assumes Louis has enough users to run cohort analysis meaningfully. At launch, he does not.

---

## What I'm NOT Arguing

I am not arguing that annual billing is bad. I am not arguing that annual should not exist in the product. I am not arguing that the Day 30 upsell is wrong.

I am arguing that annual billing at checkout on Day 1 — for a product with zero users, zero retention data, and a six-day Sprint 0 deadline — is a decision made on behalf of users we haven't met. It pre-commits us to a pricing infrastructure before we know if the monthly model works.

The correct time to add annual billing is when Louis has monthly retention data, a cohort of users who have crossed Day 30, and evidence that those users are worth offering an annual upgrade to. That is v1.2. Not Day 1.

---

## Summary

| | Monthly Only at Launch | GS Position (Monthly + Annual at Checkout) |
|---|---|---|
| Launch complexity | Single pricing decision | Dual pricing decision at checkout |
| First conversion ask | Low commitment | Higher commitment |
| PMF validation | Clean signal | Mixed signals from dual SKU |
| Annual introduced | v1.2, post-30-day retention data | Day 1, before any retention validation |
| Day 30 upsell | Available when users are validated | Available but checkout already split attention |
| Cohort analytics | Built from clean monthly churn | Built from mixed monthly + annual |

---

## Recommendation

**D138: Eliminate annual billing at launch. Monthly €29 ONLY. Annual billing enters at v1.2 as a Day 30 upsell offered exclusively to users who have created their first devis or facture. Louis builds one pricing page, acquires one type of customer, and learns whether the monthly relationship holds before adding annual.**

The debate has run long enough. Monthly-only at launch is the correct call.
