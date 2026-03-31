POSITION PAPER: D138 — Annual Billing
Product Strategist | Pulse 2026-03-31T05:29

---

1. CHALLENGE TO GS-D153: "Annual Cohort Analysis Gives Better Seasonality Signal"

GS-D153 argues: monthly churn masks seasonality as "customer churned in August" with no internal reference point. Annual cohort data gives a calendar anchor — "8 of 14 prepaid customers churned at their annual renewal in September" — which makes seasonality correlation more actionable.

This is wrong in two specific ways.

First, the "calendar anchor" GS-D153 describes is not a signal — it is a lag. Annual churn data tells Louis that seasonality was a problem 12 months ago, not that it is a problem now. A heating engineer who prepaid in October and cancels in August (peak season end for heating work) shows up as an August churn event under monthly billing AND as a "renewal failure at month 12" under annual billing. The annual data does not reveal the August signal faster. It obscures it by wrapping it in a 12-month commitment window. Monthly churn data tells Louis in real time: "this artisan left in August." Annual data tells Louis 12 months later: "this artisan left near the end of their annual term, which may have been August." That is not a better signal. That is a delayed, confounded version of the same signal.

Second, GS-D153's "actionable" framing assumes Louis can do something with a cohort of 14 annual prepaid customers. At 5 beta users, there is no cohort. There is no statistical validity. "8 of 14 prepaid customers" requires 14 prepaid customers — which requires having launched with annual as an option and having users choose it. If Louis follows PS-D152's monthly-only position, he accumulates monthly churn data from which seasonality can be inferred. If Louis follows GS-D153's position, he splits his 5 beta users between monthly and annual, gets a small annual cohort that tells him almost nothing, and loses the clean monthly signal. GS-D153's seasonality argument is only valid at scale. At 5 users, it is not a signal — it is noise dressed up as a signal.

The correct seasonality signal for a 5-beta-user launch is: monthly churn rate correlated against external seasonal calendars (heating engineers slow down in April, construction in December, etc.). Louis does not need annual cohort data to see this. He needs monthly users and a calendar.

---

2. MY WEAKEST ASSUMPTION: "€240 Upfront IS Expensive for Solo Artisan"

In PS-D152 I argued: "€240 upfront IS expensive for a solo artisan, regardless of the monthly equivalent. For a solo plumber in January — between jobs, heating bills high, income low — €240 is a significant cash outlay."

This is the right intuition but the wrong universal claim.

Here is the counter-case: a heating engineer in September. He just finished a summer of boiler replacements before the winter rush. He received a large payment last week. He is in peak cash-flow mode. At that moment, €240 feels cheap — it is a rounding error on a good month. He would happily prepay €240 to lock in a tool he is already using and valuing. The framing "it's only €20/month!" is not a marketing trick in that moment. It is a genuine reflection of his economic reality.

My argument collapses for seasonal users who have peak cash windows. And these users — heating engineers, HVAC, seasonal construction — are likely a significant portion of the target market. For them, annual billing is not a cash-flow burden. It is a smart deployment of peak-season surplus.

The correct claim is not "€240 is always expensive." The correct claim is "€240 is expensive at the WRONG moment in the seasonal cycle." Which means the question is not "should we have annual billing" — it is "when in the user's seasonal cycle should we surface the annual offer?"

That is exactly what the Day 30 upsell (GS-D153) and the hidden-link middle ground (below) are trying to solve. I was wrong to state my assumption as universal when it is only true for a specific temporal window.

---

3. MIDDLE-GROUND PROPOSAL: Annual Available But Not Displayed

Neither PS-D152 (eliminate) nor GS-D153 (prominent opt-in) is correct for a 5-beta-user launch. Here is the middle ground:

Monthly €29 is the primary and only advertised CTA. Full stop.

Annual €240 is available at checkout but not prominently displayed. Specifically: a small text link below the main CTA that reads, in muted styling, "facturation annuelle disponible — €240/an." No emphasis. No call to action. No upsell copy. Just availability disclosure.

This is different from GS-D153 in one critical way: the annual option does not appear on the pricing page. It does not change the mental framing of the primary CTA. It does not introduce anchoring ("€20/month vs €29/month") at the decision point. A user who wants to find the annual option can find it. A user who sees €29/month and asks "but can I pay annually?" finds it immediately. A user who sees €29/month and is making a snap decision to try the product is not primed to think "I should compare this to the annual equivalent."

Why not the Day 30 upsell? Because the Day 30 upsell requires: (1) tracking 30-day engagement, (2) a separate notification/prompt system, (3) a framed copy flow. That is engineering work. For a 5-beta-user launch with no PMF, we want to test whether annual uptake exists at all — not build a sophisticated retention engine. A small text link at checkout is the minimum viable test of annual demand with zero engineering cost and zero anchoring pollution.

The hidden-link approach tests: do any beta users spontaneously choose annual when offered, without us priming them to consider it? If the answer is yes — even 1 of 5 — there is real annual demand worth building a proper upsell flow around. If the answer is no, monthly-only is confirmed.

---

4. RECOMMENDATION FOR LOUIS: 5 Beta Users, No PMF

Eliminate (PS): Wrong. You are throwing away signal. With 5 users, you need to know if ANY of them prefer annual. Throwing the option away entirely means you cannot learn from the beta.

Prominent opt-in (GS): Wrong. You are poisoning the monthly frame before you have PMF. With 5 users, the anchoring effect is not your biggest risk — churn from insufficient value is your only risk. Make the monthly decision as clean as possible.

Hidden-link (middle ground): Correct. Monthly €29 as primary. Annual €240 available but not prominent. Test uptake. Learn from the beta. Build annual as a proper upsell flow in v1.2 once you know monthly retention is real.

Specific implementation: The checkout page shows one CTA — "Commencer à €29/mois." Below it, in small gray text: "facturation annuelle disponible — €240/an." No bold. No highlight. No separate pricing tier displayed on the main pricing page. Only discoverable at the moment of commitment decision.

This is the right call for 5 beta users because it maximizes learning while minimizing structural commitment. You do not know yet whether your product delivers value. You do not know whether your users are in a cash-poor or cash-rich moment. Do not make the billing decision for them — give them the option to choose without priming them toward either choice.

---

5. D138 STATUS

OPEN — with a clear recommended resolution.

The debate between PS-D152 (eliminate) and GS-D153 (prominent opt-in) is genuinely unresolved. But the middle ground (hidden-link annual availability) is available and superior to both extremes.

Louis should decide: adopt the hidden-link approach and move on. D138 is not a blocker for Sprint 0. It is a one-line copy change at checkout.

---

END OF POSITION PAPER