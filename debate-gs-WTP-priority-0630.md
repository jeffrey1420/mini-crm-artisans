# POSITION PAPER

## Topic: D138 Cannot Be Resolved Before WTP Validation
**Author:** Growth Strategist
**Date:** 2026-03-31

---

## Executive Summary

Both sides of the D138 debate — the Product Strategist's "hidden-link" position (PS-D138-0610) and the Growth Strategist's "default-annual" position (GS-D153) — share a fatal assumption: that **€29 is the correct price**. This assumption was never validated with a real French artisan. Until it is, neither billing structure decision can be resolved responsibly. The debate is not "annual or monthly first" — it is "do we know if anyone will pay €29 at all?" D138 should be **CONTESTED** pending a WTP (willingness-to-pay) experiment with real beta users.

---

## 1. The D138 Debate Is Premature: Foundation Questions Must Come First

The annual-vs-monthly debate is a **distribution question**: given a price, how do we present it to maximize conversion? The WTP question is a **foundation question**: is this price acceptable to real users at all?

These are not the same question, and they cannot be resolved in the wrong order.

PS-D138-0610 argues that monthly €29 should be the primary CTA because surfacing annual at checkout suppresses monthly conversion. GS-D153 argues annual €240 should be the default because it captures higher LTV and seasonal demand. Both arguments are sophisticated. Both arguments are irrelevant if €29 is the wrong price.

Consider: if artisans would actually pay €40/month for this product, then:
- €29/month is underpriced by 28%
- Defaulting to annual at €240 locks in that underpriced position
- The "hidden-link" approach compounds the error by burying the underpriced option

Conversely: if artisans would only pay €15/month, then:
- €29 is rejected regardless of billing structure
- Either billing presentation fails — monthly gets refused, annual gets refused
- No amount of checkout optimization solves a price rejection problem

**Foundation questions come first.** We have not answered "is €29 acceptable?" Therefore we cannot answer "should annual or monthly be primary?"

---

## 2. U15 Elimination Removed the One Mechanism That Could Have Validated Price at Launch

The founding member offer (U15) was eliminated in Debate 101. This decision was made for sound reasons (discount framing, scarcity signals, price escalation complexity). But it eliminated the one launch mechanism that could have simultaneously tested price sensitivity and acquired early users.

A properly designed founding member offer — "first 20 users lock €29/month permanently" — was not just a pricing tactic. It was a **revealed-preference WTP experiment**. Early adopters who committed signaled: "I value this enough to lock in a price before the product is fully built." That signal is more valuable than any survey response.

With U15 eliminated, there is now **no mechanism** to test whether €29 is too high, too low, or appropriately priced:

- No founding tier to capture high-WTP early adopters
- No trial (D6: Free tier IS the trial) — meaning no conversion funnel with price at the moment of commitment
- No pricing experiment built into Sprint 0

The only remaining path to WTP validation is an explicit experiment. It was TODO from the 05:46 pulse. It has not been executed.

---

## 3. The 3% Day-30 Conversion Target Is Undiagnosable Without a WTP Baseline

The debate log cites **3% Day-30 conversion** as the target KPI. If Louis ships with the current pricing and sees 0.5% Day-30 conversion at Month 2, what does that tell him?

- Is the price too high? (Maybe — but we never validated what "too high" means)
- Is the product not valuable enough? (Maybe — but €29 is below the pain threshold for most artisans with real admin burden)
- Is the distribution broken? (Maybe — wrong channel, wrong message, wrong moment)
- Is the onboarding failing? (Maybe — Free tier users never reach the payment moment)

**Without a WTP baseline, conversion failure is uninterpretable.** The 3% target is a measurement with no diagnostic framework. Low conversion could be any of four problems: price, product, distribution, or activation. You cannot triage a patient you haven't baseline-tested.

PS-D138-0610 argues that "revealed preference is the experiment — watch if they pay €29." This is partially correct but backwards for decision-making purposes: by the time you observe the payment behavior, you've already shipped a price that may be wrong. The WTP experiment before shipping is diagnostic. The payment behavior after shipping is retrospective. You need both.

---

## 4. The Hidden-Link vs Default-Annual Debate Is Unresolvable Without WTP Data

PS-D138-0610's hidden-link argument depends on a specific assumption: that €29 is the correct price and annual is a secondary consideration. If €29 is correct, then surfacing annual prominently introduces anchoring friction that suppresses monthly conversion. Fine.

But if artisans would pay €40, then:
- Default annual at €240 is **underpriced** by 50% relative to WTP
- The hidden-link approach means users never see the annual option they'd happily pay for
- Louis leaves €160/year per user on the table

If artisans would pay €15, then:
- Either billing option fails — €29/month is rejected, €240/year is rejected
- The debate between hidden-link and default-annual is a distinction without a difference
- Both options fail for the same reason: price rejection

The PS-D138 argument also claims that "cohort analysis with n=5 is statistically meaningless." This is true for cohort analysis — but it applies equally to the hidden-link experiment. If zero of five beta users navigate to the hidden annual option, is that evidence of no demand, or evidence that the product isn't valuable enough to justify any payment? You cannot distinguish signal from noise at n=5 regardless of which mechanism you use.

**You cannot choose between hidden-link and default-annual without knowing the price range.** The billing structure debate is not resolved — it is unresolvable — until WTP is established.

---

## 5. PS-D138-0610's Counterarguments Are Correct But Incomplete

PS-D138-0610 raises three arguments against the WTP experiment:

1. **"You need beta users to validate price; beta acquisition is unsolved"** — Correct. Beta acquisition is unsolved. But this is an argument for solving beta acquisition, not for skipping WTP validation. The WTP experiment and beta acquisition are sequential dependencies, not parallel tracks. You cannot skip the second step because the first step isn't done.

2. **"A WTP experiment with 5 users is statistically meaningless"** — Correct for quantitative inference. But the purpose of the WTP experiment at this stage is not to set a price with statistical confidence. It is to establish a **directional baseline**: are we in the €15-20 range, the €25-35 range, or the €40-60 range? Five answers that cluster in one range tells Louis whether he's in the right ballpark. That's not statistics — that's directional sanity-checking.

3. **"Revealed preference is better than stated preference"** — Correct in principle. But revealed preference requires a price to test. You cannot observe payment behavior without a price. The "behavior is the experiment" argument only works if you've first set a price — which is precisely what we're questioning.

The PS-D138 position is internally consistent but assumes the conclusion: it argues against validating €29 because validation is hard, therefore ship €29. This is the confirmation bias version of "move fast."

---

## Core Position

**D138 is CONTESTED — not resolved, not deferred, but CONTESTED.**

The D138 decision cannot be finalized until:
1. A WTP experiment establishes whether €29 is in the right range for French artisans
2. The result of that experiment informs whether annual billing at €240 is appropriately priced, underpriced, or overpriced relative to revealed WTP
3. Only then can the billing structure (hidden-link vs default-annual vs monthly-primary) be determined

The current D138 resolutions from GS-D153 and PS-D138-0610 are **both potentially wrong** — and more importantly, they cannot be compared without the WTP foundation. Default-annual is wrong if €29 is too expensive. Hidden-link is wrong if €40 would have converted. Both positions are speculation dressed as strategy.

---

## Resolution Proposal

### D138 Status: CONTESTED — Pending WTP Experiment

D138 is not resolved. It is contested. The billing structure decision waits for the WTP experiment.

### Sprint 0 Blocker: WTP Experiment

The WTP experiment must be completed before D138 is finalized. It is a Sprint 0 blocker — not a Phase 2 research project.

### WTP Experiment Design

**Objective:** Establish directional WTP range for Mini-CRM among French artisans (45-55, solo, smartphone-native, acute admin pain).

**Participants:** 5 real beta users — currently practicing artisans with ≥1 active client (D138-beta definition applies).

**Format:** 20-minute semi-structured conversation, in person or via phone/WhatsApp.

**Script:**

> *"Je travaille sur un outil pour vous aider à gérer vos devis et factures depuis votre téléphone — moins de temps sur l'administration, plus de temps sur vos chantiers. Quand vous recevez un nouveau client ou un paiement en retard, qu'est-ce que ça vous coûte en temps et en stress ? Combien d'heures par semaine vous prenez sur l'administration ?"*
>
> [Listen. Quantify. Then:]
>
> *"Si cet outil vous faisait gagner 2-3 heures par semaine sur l'administratif — enough to send your quotes faster, track what clients owe you, and follow up without forgetting — what's the most you'd pay per month for that? Don't think about what's cheap. Think about value: if it actually worked and saved you that time every week, what's the most you'd pay?"*
>
> [Document the answer. Document the emotional reaction. Probe if answer is vague: "Give me a number. €10? €20? €50?"]

**Output:**
- Raw WTP number per participant
- Emotional reaction (hesitation, immediate confidence, negotiation)
- Context: time currently spent on admin, current workaround, biggest pain point

**Decision rule:**
- If median WTP ≤ €15: €29 is too high. Pricing must be reconsidered before billing structure is set.
- If median WTP = €20-35: €29 is in range. Proceed with D138 billing structure decision.
- If median WTP ≥ €40: €29 is underpriced. Annual at €240 is also underpriced. Reconsider pricing before billing structure.

**Why 5 users is sufficient for this decision:**
This is not a quantitative study. It is a sanity check. Five consistent answers in one direction (all five say €15-20, or all five say €35-50) is sufficient to establish directional direction. Five scattered answers (€10, €15, €30, €50, €60) indicate the sample is too heterogenous — repeat with 5 more. The goal is not precision; it is avoiding a €29 price that is obviously wrong for the entire segment.

---

## What This Means for the Debate Log

| Entry | Impact |
|-------|--------|
| GS-D153 (default-annual) | CONTESTED — holds only if WTP validates €29 is in range |
| PS-D138-0610 (hidden-link monthly-primary) | CONTESTED — holds only if WTP validates €29 is in range |
| D138 resolution in debate log (04:05, 05:46) | CONTESTED — must be re-examined after WTP experiment |
| D99 (pricing: €29 + €260 annual) | CONTESTED — annual price €260 cannot be validated without WTP |
| 3% Day-30 conversion target | CONTESTED — uninterpretable without WTP baseline for diagnosis |

---

## Call to Action

Louis must run the WTP experiment this week — before Sprint 0 begins, or in parallel with its first days. The experiment is 5 conversations of 20 minutes each. It is not a research sprint. It is a sanity check that prevents shipping a billing structure built on unvalidated assumptions.

**D138: CONTESTED. WTP first. Then decide.**

---

*End of Position Paper — GS-D138-WTP-0630*
