# POSITION PAPER: GS-Sprint0Timing-0610
**Author:** Growth Strategist
**Date:** 2026-03-31
**Topic:** Sprint 0 beta validation is validation theater
**Status:** FINAL — for debate record

---

## Assumption Being Challenged

> *"5 beta users complete the happy path without assistance"*

This criterion is treated as a meaningful Sprint 0 exit gate — proof that the product is validated and ready to proceed. **It is not.** This criterion produces the *feeling* of validation without the *substance* of it. It is theater, not evidence.

---

## Core Arguments

### 1. n=5 is statistically and commercially meaningless

Five users cannot tell you whether your product works for your market. This is not a controversial claim — it is basic sampling logic.

- **Sample size problem:** n=5 tells you nothing about variance, dropout rates, or edge-case failure modes. If 2 out of 5 users hit a bug, your crash rate is 40%. If 0 out of 5 hit it, you have a false sense of security. Either way, you know nothing.
- **Self-selection bias:** Who are these 5 beta users? They are almost certainly people Louis knows personally, who have been primed to expect a rough early build, and who have social incentive to be encouraging. They are not a random sample of 45-55 year old French artisans who found the product through a real discovery channel and chose to install it voluntarily.
- **Guided conditions ≠ real-world usage:** "Completing the happy path without assistance" means someone walked these specific users through the flow, or sat next to them, or at minimum made them aware the build existed. Real users find your app on a landing page, read a App Store description, install it in a different context, and begin with zero guidance. These are categorically different conditions.

### 2. Real validation requires real distribution infrastructure — which doesn't exist until Sprint 1

The Sprint 0 criterion was designed as if the product could be validated in a vacuum. It cannot. Here is what genuine validation actually requires:

- **A landing page that communicates value** — what does the artisan think when they first hear about the product? This is the first commercial signal.
- **An install funnel with real dropout data** — where do people abandon? At the login screen? After the first form? Real users reveal this; guided beta users never do.
- **WhatsApp sharing behavior** — when an artisan uses this with a client, does it get shared? Does it generate organic virality signals? You cannot observe this with 5 hand-picked users in a guided setting.
- **Conversion behavior** — will anyone ever pay for this? At what price point? Guided happy-path completion tells you absolutely nothing about willingness to pay.

None of this infrastructure exists at Sprint 0. Running the "5 beta users" gate before this infrastructure is built is measuring the wrong thing. You are validating that the code runs, not that the market wants it.

### 3. The Sprint 0 beta criterion is founder ego disguised as process

This is the hardest argument to make but the most important one.

- **Emotional relief, not data:** The moment Louis reports "5 beta users completed the happy path," the team feels validated. This is a psychological reward — not a commercial signal. The criterion exists because it feels good to declare victory, not because it produces durable learning.
- **Commitment bias:** Once Sprint 0 "validation" is declared, every subsequent decision is colored by it. The team has emotionally invested in the product being validated. This makes it harder to kill features that aren't working, harder to change direction, and harder to accept negative signals from real users in Sprint 1. The Sprint 0 gate doesn't protect against failure — it amplifies it by delaying the moment of reckoning.
- **No durable data asset:** The output of the Sprint 0 gate is a feeling ("it works") and a Slack message ("beta users confirmed"). There is no dataset, no funnel analysis, no cohort comparison. If the product fails in Sprint 1, you have no Sprint 0 baseline to diagnose why. You have a story about how good it felt.

### 4. The real Sprint 0 exit criterion should be technical, not behavioral

The question Sprint 0 should answer is: *can we build a mobile app that runs on real hardware without crashing?* Not: *do 5 hand-selected humans like it?*

Proposed Sprint 0 exit criteria:
- APK builds successfully from CI
- APK installs on a real Android device (not emulator) without Play Protect blocking it
- Core navigation flow does not crash (can be verified by the team on 3 physical devices)
- No obvious ANRs or memory leaks during a 10-minute smoke test on low-end hardware

This is a real, binary, reproducible gate. It tells you whether your build pipeline works and whether the product can physically reach a real user. **That is what Sprint 0 is for.** User validation belongs in Sprint 1, after you have built the infrastructure to observe real user behavior.

---

## What This Challenges in the Existing Decision Log

This position directly challenges:

| Decision | Entry | What I Dispute |
|---|---|---|
| Sprint 0 exit criteria | "5 beta users complete the happy path without assistance" | Commercial validation requires distribution infrastructure that doesn't exist until Sprint 1; n=5 is below statistical meaningfulness |

**Secondary challenges:**
- Any prior decision that treats Sprint 0 as a "validation" phase rather than a "build infrastructure" phase
- Any planning assumption that Sprint 1 starts with validated product-market fit — it starts with the *ability* to validate, not validation itself

---

## Proposed Resolution

1. **Remove** "5 beta users complete the happy path" as a Sprint 0 exit criterion.
2. **Replace with** a technical gate: build succeeds, installs on 3 real Android devices, no crashes during 10-minute smoke test.
3. **Rename** Sprint 0 from "validation" to "build foundation" in all planning documents.
4. **Move the behavioral validation to Sprint 1**, after the landing page is live and real distribution is possible. At that point, the first 20-50 real installs become a genuine validation signal — not because the number is large, but because they arrived through a real discovery channel with no guided assistance.
5. **Acknowledge explicitly** that Sprint 0 beta testing produces qualitative color but no commercial signal, and should not be used to justify continued investment in the current feature set.

---

## What Remains OPEN After This Position

1. **Who are the real beta users, and how do we find them?** This position doesn't solve the distribution problem — it only says the current gate doesn't solve it.
2. **What is the actual target install count for Sprint 1 validation?** n=20? n=50? This needs a specific, reasoned number.
3. **What behavioral signals, specifically, constitute validation in Sprint 1?** Dropout rate? Time-to-first-devis? WhatsApp share rate? These need to be defined before Sprint 1 begins.
4. **Louis's personal network as a bridge strategy** — whether a small, trusted network of real artisans can serve as a controlled real-world test before broad distribution. This is not the same as the current Sprint 0 gate but may be a legitimate intermediate step.
5. **What happens if the Sprint 1 validation signals are also unclear?** The decision framework for what constitutes "enough signal to proceed" to Sprint 2 is not yet defined.

---

*This paper represents the Growth Strategist position in the Mini-CRM research debate. It is intended to be challenged, refined, and resolved — not to stand as final truth.*
