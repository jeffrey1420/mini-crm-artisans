# Position Paper: Defer WhatsApp Business API to v1.1

**Author:** Product Strategist Agent  
**Pulse:** Mini-CRM Research, PS-WhatsApp-Sprint0  
**Date:** 2026-03-31

---

## Position Title

**WhatsApp Business API Does Not Belong in Sprint 0 — Sprint 0 Notification = Expo Push Only**

---

## Assumption Challenged

**D141** stated: *"WhatsApp Business API is the PRIMARY activation channel for Path B (verbal-agreement artisans who never generate formal accepted devis — ~40-50% of target market)."*

This conflates two distinct problems: **acquisition** and **re-activation**. D141 treats WhatsApp as the activation trigger for dormant Path B users. It is not. Activation already happened — they downloaded the app, set up clients, and sent quotes. What Path B users have is a **retention problem**, not an acquisition problem. WhatsApp cannot re-activate a user who stopped opening the app because the app wasn't delivering recurring value. Adding a notification layer on top of a broken value loop does not fix the loop.

---

## Core Argument

**1. Meta Business Verification Alone Breaks the Sprint 0 Timeline**

Meta Business Verification takes 2–14 business days. That's the sprint floor (5 days) exceeded before a single line of code is written. WhatsApp Business Account setup, phone number compliance review, and message template approval add another 3–5 days minimum. This is not a feature — it's a compliance gate on someone else's platform. Sprint 0 cannot be both self-contained and dependent on Meta's approval queue.

**2. At v1, There Is No Premium Content to Push via WhatsApp**

The Free tier *is* the product at launch. There is no premium content, no exclusive digest, no upgrade nudge worth sending through WhatsApp. D141's proposed use case — a bi-weekly WhatsApp digest to dormant Path B users — requires content that doesn't exist yet. Building the pipeline before the product means Sprint 0 effort delivers zero user-facing value.

**3. WhatsApp Nudges Don't Fix a Broken Value Loop**

Path B users stopped opening the app for 14+ days. They didn't ignore a notification — they stopped seeing value in the app itself. A WhatsApp message from "DevisPro" saying "Vous avez des devis en attente" doesn't recreate value. It reminds them of admin anxiety they already decided to ignore. If the app isn't compelling enough to open voluntarily, no external channel will restore habit formation.

**4. Path B Users Are Reachable via Expo Push — We Don't Need WhatsApp to Reach Them**

Push notifications via Expo are faster to implement (days, not weeks), don't require Meta verification, and reach the same dormant users directly on their device. The assumption that WhatsApp is the *only* way to reach Path B users ignores that push notifications reach them on their phone without any third-party gatekeeper.

**5. WhatsApp Belongs in v1.1, Where It Can Deliver Real Value**

WhatsApp Business API is genuinely powerful — but for a product that has premium content to deliver (upgrade prompts, payment reminders, a/b tested offers). At v1, we should ship the core value loop first (devis → facture → relance), validate that Path B users form habits around it, and *then* add WhatsApp as a secondary re-activation channel for users who have lapsed. Building WhatsApp on top of a validated product is sprint planning. Building it on top of a hypothesis is speculation.

---

## Why the Alternative Fails

**"Include WhatsApp in Sprint 0 — accept the timeline risk"** fails because:

- The risk is not manageable within the sprint. Meta's verification timeline is outside our control.
- The deliverable (WhatsApp integration) provides zero user value at v1 — it's infrastructure for a product that doesn't exist yet.
- It delays the validation of the core product loop (devis → facture → relance) by a sprint, pushing real user learning into v1.1.
- Expo Push achieves the same re-activation goal for Path B users at a fraction of the implementation cost.

**"Include WhatsApp in Sprint 0 and accept 6.5–7 days"** fails because that timeline assumes all pre-conditions are met. Adding WhatsApp adds Meta verification (2–14 days, out of sprint), making the 7-day floor effectively 9–21 days — not a sprint.

---

## Proposed Resolution

- **Sprint 0 notification stack:** Expo Push Notifications only (implemented in Sprint 0 as part of the React Native/Expo setup).
- **WhatsApp Business API:** Added in v1.1 sprint planning, after the core value loop is validated.
- **Path B re-activation at v1 launch:** Achieved via push notifications + in-app prompts tied to the devis/facture/relance flow.
- **v1.1 WhatsApp scope:** Include Meta Business Verification timeline in sprint planning (2 weeks parallel track), message template setup, and WhatsApp as a secondary channel for users who have lapsed from push notifications.

---

## Sprint 0 Implications

| Item | With WhatsApp in Sprint 0 | Without (Expo Push Only) |
|------|--------------------------|--------------------------|
| Sprint 0 timeline | 9–21 days (Meta queue) | 5 days (achievable) |
| Notification coverage | Same users, slower | Same users, faster |
| User-facing value at v1 | Zero (empty pipe) | Full (devis flow + push) |
| Meta dependency | Full (external gate) | None |
| Core loop validation | Delayed to v1.1 | Sprint 0 |

**Decision:** Defer WhatsApp Business API to v1.1. Sprint 0 ships Expo Push only. Path B activation at v1 = push notifications + validated core product. WhatsApp becomes the re-activation layer once there is premium content to push through it.

---

*Product Strategist — Mini-CRM Research Pulse*  
*2026-03-31T03:03 UTC*
