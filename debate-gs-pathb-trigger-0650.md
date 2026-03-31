# POSITION PAPER

## Topic: Path B Sprint 0 Trigger — Challenging the "3 Factures" Assumption

**Author:** Growth Strategist
**Date:** 2026-03-31

---

## Executive Summary

The Technical Architect proposes replacing the Sprint 1 Path B trigger ("5 jobs logged") with a Sprint 0-compatible alternative: "3 factures created, 0 accepted devis." This substitution merely replaces one unvalidated assumption with another. The fundamental problem is not the threshold — it is the premise. Path B artisans, by definition, operate on verbal agreements and informal payment workflows. If their daily practice bypasses formal invoicing, they will never produce the 3 factures required to trigger conversion. The Technical Architect's alternative is not safer; it is a different gamble with the same unknown odds. Path B may be structurally unaddressable in Sprint 0, and we should make that explicit rather than papering over it with arbitrary numbers.

---

## Section 1: Path B Artisans Are Defined by Their Resistance to Formal Documentation

Path B is not merely a user segment — it is a behavioral archetype defined by informality. Artisans who operate on verbal agreements do so for structural reasons: cash transactions, trusted client relationships built over years, tax avoidance motives, administrative aversion, or simple inertia. These are not users who will gradually discover the benefits of formal invoicing. They are users whose workflow actively bypasses the document creation events that Path A triggers rely upon.

The Technical Architect's proposed trigger — "3 factures created, 0 accepted devis" — assumes that Path B artisans will naturally begin creating formal factures once given the tool. This is a critical assumption with no supporting evidence. In fact, the defining characteristic of Path B is the opposite: they have operated without formal factures for years, often by choice or by client expectation. Introducing an app does not automatically change this behavior. It changes the *opportunity* to create a facture, not the *likelihood* that a cash-based artisan will suddenly start documenting every payment formally.

The threshold of "3 factures" is stated without justification. Why 3? Why not 1? Why not 10? The Technical Architect has not validated this number through user research, A/B testing, or any empirical basis. It is a round number that *feels* reasonable — which is not the same as being correct. Any trigger threshold must be grounded in observed behavior, not intuition.

---

## Section 2: The "Receipt-Only" Failure Mode — Path B May Be Invisible in Sprint 0 Data

Consider the realistic usage pattern of a Path B artisan who downloads the app in Sprint 0:

- They log 1–2 jobs manually (perhaps out of curiosity or a client's mild suggestion)
- Their payment is cash, handed over at the job site
- They give the client a handwritten receipt or no document at all
- They never open the "Create Facture" flow, because it does not match how they operate

Under this scenario, the trigger event ("3 factures created") never fires — not because the artisan is disengaged, but because the product is asking them to change a deeply ingrained workflow that their entire business is built around.

This is not a failure of onboarding. This is a fundamental mismatch between the product's conversion trigger and the user's actual behavior. We cannot A/B test our way out of this with a different threshold number. The trigger itself is misaligned with the segment it is meant to address.

If Path B artisans are effectively invisible to the "3 factures" trigger — if they churn silently without ever creating a single formal invoice — then we are not addressing Path B in Sprint 0 at all. We are only capturing Path A users who were always going to convert regardless. This makes Path B a silent casualty of our Sprint 0 design choices.

---

## Core Position

Path B artisans will NOT naturally produce enough factures to trigger conversion in Sprint 0, or likely ever without structural product changes that are out of scope for this sprint. The "3 factures" threshold is arbitrary and unvalidated. More importantly, the premise that Path B users will adopt formal invoicing workflows simply because the app offers the capability is contradicted by everything that defines the Path B segment. The Technical Architect's proposed trigger does not fix the Sprint 0 compatibility problem — it replaces one assumption with another while leaving the core behavioral mismatch unaddressed.

---

## Resolution Proposal

**Phase Path B conversion tracking differently, and stop pretending Sprint 0 can address Path B effectively.**

Concretely:

1. **Acknowledge Path B is out of scope for Sprint 0 conversion triggers.** The `jobs` table and the informal workflow problem are two separate issues. Path B's trigger problem cannot be solved by swapping the trigger metric. Either invest in Sprint 1 research to understand what Path B actually does in the app, or accept that Path B conversion will not be measured in Sprint 0.

2. **Replace the "3 factures" trigger with a leading indicator for Path A only in Sprint 0.** Path A (structured, devis-accepting artisans) will naturally produce devis and factures. Use "1 accepted devis" or "2 jobs logged" — metrics that are behaviorally aligned with Path A, not Path B. This gives Sprint 0 a clean, validated trigger for the segment it can actually address.

3. **For Path B, establish a Sprint 1 discovery task.** Before defining any Path B trigger, conduct 5–10 user interviews with artisans who operate primarily on verbal agreements and cash payments. Ask: *What would make you open this app after a job?* Do not assume. Observe. Then, and only then, design a trigger that matches their actual behavior — which may be "first login after 3 days" or "1 job logged via quick-entry" rather than any document-creation metric.

4. **If forced to keep Path B in Sprint 0 scope**, use a proxy trigger with lower behavioral demands: "3 sessions opened, no devis created." This captures artisans who are engaging with the app but not yet formalizing their workflow — a more honest signal of early Path B adoption than document creation.

The Technical Architect's alternative is not a solution. It is a different guess. We should stop guessing and start researching.

*End of Position Paper*