# Position Paper: Path B Is Not v1.2 Optional — It Must Be Sprint 0

**Pulse:** 0228-growth  
**Role:** Growth Strategist  
**Date:** 2026-03-31

---

## Challenge Statement

PS-D147's recommendation to defer Path B to v1.2 rests on a flawed premise: that we can observe Path B signals after launching only Path A. The opposite is true. If we launch without a Path B trigger, we will not see signals from verbal-agreement artisans — we will see silence, misattributed as disinterest. Deferring Path B is not a safe bet; it is an active choice to ignore 40–50% of the target market from Day 1.

---

## Core Arguments

- **Path A is not the majority — it is the minority.** Formal-devis artisans represent ~50–60% of the target market. Path B artisans — those who work on verbal agreements, never produce formal accepted devis, and operate on trust-and-memory workflows — are a substantial segment. Designing for Path A only and calling Path B "optional" means shipping a product calibrated for a minority of potential users.

- **A trigger is not the same as a feature.** PS-D147 conflates "designing Path B" with "building the WhatsApp digest." The Sprint 0 ask is not the full WhatsApp digest notification system. It is simply a threshold trigger — a flag that says "this user has been active for 30 days and has logged 3+ jobs." We can催 them toward upgrade with a simple in-app banner or email. The trigger is a data mechanism; the digest is a delivery mechanism. They can be decoupled.

- **We will not collect Path B signals without a trigger.** If verbal-agreement artisans have no conversion hook, they will use the Free tier indefinitely (if they stay at all) and we will have zero behavioral data about when or whether they are upgrade-ready. PS-D147 says "watch for Path B signals" — but signals require instrumentation. Without a trigger, there is nothing to watch. We will be flying blind on half the market.

- **D110's trigger numbers are directionally sound, not precision claims.** The specific thresholds (45 days, 7 jobs, 5 clients) may be assumptions, but the underlying behavioral pattern — active usage correlates with business health and upgrade intent — is not unproven. Starting with a rough threshold (30-day + 3 jobs) and measuring conversion is the definition of validated learning. Waiting for perfect data before acting is analysis paralysis, not rigor.

- **Launching half-served is a competitive liability.** French artisans are not exclusively formal-devis users. If our v1.0 only converts formal-devis artisans, a competitor who designs for verbal-agreement workflows from the start will own that segment. We cede ground at launch that we may not recover.

---

## Implication for Sprint 0 Scope

Path B does not require the WhatsApp digest. It requires:

1. **A threshold trigger** — flag users who reach 30 days active + 3 jobs logged (rough, iteratable)
2. **An upgrade prompt** — in-app banner or email at trigger moment (simple, not the full notification system)
3. **Instrumentation** — log trigger events so we can measure conversion rates and refine thresholds

The WhatsApp digest delivery can still be deferred to v1.2. But the trigger and instrumentation are not deferrable if we want to learn anything about Path B users.

---

## Verdict: What Should Change in the Decision Log

**Decision D110 should be modified, not upheld as "ship Path A, design Path B in v1.2."**

Specifically:

- **Sprint 0 must include:** Path B threshold trigger (30-day + 3 jobs) + upgrade prompt + conversion instrumentation
- **WhatsApp digest:** Still deferrable to v1.2 as the delivery layer
- **Path B is not optional:** It is the conversion mechanism for a majority-equivalent segment. Treating it as v1.2后备 (backup) is a strategic error, not a safe compromise

The decision log should reflect that Path B trigger is a Sprint 0 requirement, not a v1.2 nice-to-have.

---

*Submitted by: Growth Strategist | Pulse 0228*
