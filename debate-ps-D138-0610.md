# DEBATE POSITION PAPER
## D138 — Annual Billing at Launch: The Hidden-Link Approach Is Correct
**Author:** Product Strategist (PS立场)
**Date:** 2026-03-31
**Pulse:** D138-0610

---

## Assumption Being Challenged

> **"Annual billing should be a prominent opt-in option at checkout alongside monthly €29."**

This assumption — advanced primarily in GS-D153 — asserts that both billing tiers deserve co-equal visibility in the checkout flow. The hidden-link alternative (PS-D138-0529) disagrees: monthly €29 is the primary CTA, annual €240 is available but not surfaced prominently. This paper argues the hidden-link is the correct launch decision.

---

## Core Arguments

### 1. Checkout Context Is the Wrong Moment for Annual Anchor Pricing

At first conversion, Marc (45-55yo French artisan, mobile-first, checking out on phone) is evaluating commitment. The €240 price point triggers "significant purchase" psychology — a mental accounting event that introduces friction and hesitation. €29 triggers "coffee and a croissant" psychology — a low-stakes trial decision. 

Presenting annual alongside monthly at this moment does not "anchor down" the annual price; it anchors the hesitation. The behavioral economics literature on decoy pricing works in contexts where the product is already trusted. At launch, with an unproven product and a skeptical artisan demographic, surfacing the annual option as prominent does not drive annual uptake — it suppresses the monthly conversion that the business needs to survive long enough to test annual demand.

**Conclusion:** Monthly-primary at checkout maximizes first-conversion rate. Annual can be tested without being featured.

---

### 2. Cohort Analysis With n=5 Beta Users Is Statistically Meaningless

The GS-D153 position argues that annual billing enables cohort analysis of annual vs. monthly users over time. This argument requires ignoring reality: the beta currently has 5 (five) users.

With n=5:
- Any annual cohort will have 0, 1, or 2 users. This is not a cohort — it is noise.
- Annual renewal signal arrives 12 months after signup. Monthly churn signal arrives in 30 days.
- With a sample this small, **delayed signal is worse than no signal** — it lulls the team into false confidence in a direction while burning months of runway.

Monthly churn metrics at n=5 are still noisy, but they are *actionable* on a 30-day cycle. The hidden-link approach lets the team observe whether any beta users independently seek out annual pricing (via support inquiry, email, or behavior analytics) without engineering a prominent option that contaminates the primary conversion metric.

**Conclusion:** Cohort analysis requires a meaningful sample size. With n=5, monthly churn metrics dominate. Annual can be monitored via the hidden-link mechanism.

---

### 3. Hidden-Link Tests Demand Without Polluting the Primary Decision

The hidden-link is not a compromise — it is a clean experimental design:

- **If 1 in 5 beta users independently finds and selects annual:** There is genuine demand. The team builds a proper annual upsell flow post-signup (email sequence, account settings page, upgrade prompt) rather than relying on checkout real estate.
- **If 0 in 5 beta users ever select annual:** Monthly-only is confirmed. No anchoring cost was paid, no checkout friction was introduced.

The prominent opt-in (GS-D153) contaminates the experiment: you cannot distinguish between "annual uptake because it was visible" and "annual uptake because there is real demand." The hidden-link approach provides clean signal because it removes the visibility variable.

**Conclusion:** Zero anchoring cost. Clean experiment. Actionable signal from day one.

---

### 4. "Seasonal Preference for Annual" Is Unvalidated Speculation

The argument that peak-season artisans prefer annual billing is plausible but unvalidated. The hidden-link approach tests this hypothesis without making it an architectural commitment:

- If seasonal artisans exist and want annual, they will find the annual option (support inquiry, email, or a discreet settings page link).
- Surfacing annual prominently validates nothing about seasonal preference — it only validates that some users exposed to the annual price convert to it.

The seasonal preference argument is essentially a product intuition. Intuition should be tested, not featured. The hidden-link is how you test it without betting the checkout conversion rate on it.

**Conclusion:** Test the hypothesis. Don't bet the primary CTA on it.

---

## What This Challenges in the Existing Decision Log

This position directly challenges the implicit assumption in **GS-D153** that prominent dual-options at checkout is a neutral or beneficial starting state. Specifically:

| Decision Log Entry | Challenge |
|---|---|
| Annual €240 as "prominent opt-in alongside monthly €29" (GS-D153) | Prominent annual anchor at checkout suppresses monthly conversion. The behavioral assumption (anchor drives annual uptake) does not hold at first-conversion with an unproven product and skeptical audience. |
| Annual cohort analysis as a justification for dual prominence | Cohort analysis requires n >> 5. With current beta size, this is not a valid launch-day justification. |
| Seasonal preference as a reason for annual prominence | Unvalidated intuition. Hidden-link tests it without making it a structural commitment. |

---

## Proposed Resolution

**At launch (D138 resolution):**

1. **Primary CTA:** Monthly €29 — featured, clearly labeled, single action.
2. **Annual €240:** Available in account settings / billing section. Not surfaced at checkout.
3. **Demand signal mechanism:** Track via analytics whether any users navigate to annual option within first 30 days. Track support inquiries mentioning annual billing.
4. **Post-launch (month 3+):** If hidden-link uptake ≥ 1 in 10 users, commission a proper annual upsell flow (post-signup email sequence, upgrade prompt in settings). If uptake is 0 after month 3, deprioritize annual entirely.
5. **No checkout redesign for annual at launch.** Monthly conversion rate is the north-star metric for the first 90 days.

---

## What Remains OPEN After This Position

1. **Annual pricing level** — Is €240/year the right number? Hidden-link demand signal informs this, but does not resolve it. A pricing study with real users is needed.
2. **Post-signup annual upsell flow** — Design, timing, and messaging of an annual upgrade prompt are not specified here. This is a separate workstream.
3. **Seasonal campaign testing** — If/when the product has meaningful user base, a seasonal campaign (Q4 " Jahresabo" equivalent for artisans) can be A/B tested against the baseline.
4. **Annual data retention for annual subscribers** — This was a separate D-series question (D140-adjacent). Not resolved here.
5. **Long-term pricing architecture** — This position assumes monthly €29 is the anchor. Whether a future tiered structure (e.g., Pro annual at €199) should exist is outside D138 scope.

---

*End of Position Paper — PS-D138-0610*
