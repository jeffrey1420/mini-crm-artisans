# D93 Product Strategist — Pulse 2347

**Debate:** Guided Creation Flow (D93) — REOPENED at 23:21, partially resolved
**Challenge issued:** 2026-03-30T23:48

---

## The Unchallenged Assumption

The debate log shows D93 moving from "mandatory Guided Creation Flow" → "90-second wizard + opt-in office hours link." The replacement is better. But the debate stopped one step too early.

**The assumption that was never challenged:**

> "Office hours (opt-in) is the right way to deliver human touch in onboarding."

This sounds obvious. Human touch = optional call link = non-prescriptive = good. But this framing misunderstands what "opt-in office hours" communicates to a 50-year-old French artisan who's been avoiding admin his whole career.

---

## Challenge: "Opt-In Office Hours" Is a Conversion Anxiety Signal

**The settled assumption:** Office hours as a link = low-pressure, non-prescriptive, artisan chooses.

**The challenge:** When "book a call" appears anywhere in the onboarding flow — even opt-in, even de-emphasized — it implicitly answers a question the artisan hasn't asked yet: *"Do I need help to use this?"*

The answer is yes. Because why else would you offer a call?

This is the exact inverse of the product's core promise. "Sans vous prendre la tête" means "you don't need help." "Book a call with us" means "you probably do." Every artisan who hesitates before clicking "office hours" has now doubt-tested the product's ease. Some will convert anyway. Many won't.

The second problem is the "5 discovery calls before Sprint 2" validation mechanism. Five calls with warm contacts (network, referrals) tells you whether people who already trust you would take a call. It does not tell you whether cold-signup artisans — the ones who found the app, downloaded it, and opened it at 6pm on a Tuesday — need or want human onboarding. That's a different question, a different population, and a different answer window.

Guerrilla testing at Point P (job site, hardware store, artisan supply shop) with a 90-second wizard prototype would tell you far more. It captures the actual stress environment. It answers: "Can a real artisan on a real job site create a devis in 90 seconds?" Discovery calls answer: "Would my LinkedIn network take a 30-minute call about this?"

---

## Verdict: Free Tier Onboarding at Launch

**The 90-second wizard ships. The office hours link does not — not in the onboarding flow.**

### Onboarding Strategy: Free Tier at Launch

1. **90-second wizard with sensible defaults.** Business name, métier, currency (EUR), payment terms (30 days). Pre-filled from the get-go. No phone contacts import (D93b already established this fails). Skip any field that requires explanation — defaults handle it.

2. **Day 1 experience is frictionless self-serve.** First screen after signup: "Créer un devis" is immediately available. The primary path is: open app → add client (name + phone, no import) → add line items → send. No slot booking. No call offered. No "are you ready?" modal.

3. **Office hours link lives in Settings, not onboarding.** If a user hits a wall — and only then — Settings → Help → "Parler à Louis (30 min)" is there. It's a last resort, not a suggested path. This preserves the "you don't need help" signal throughout the critical first-session flow.

4. **Drop the 5 discovery calls.** Replace with: guerrilla test at Point P in Week 1 of Sprint 1. Five artisans at a job site with a wizard prototype answers the real question faster and cheaper. The network call invites go to people who already like Louis — that's confirmation bias dressed as validation.

5. **The office hours offer (if validated):** If Sprint 1 guerrilla testing shows real friction points that human touch solves, office hours become a growth lever — positioned as "Louis is a real artisan tech guy, he gets it" not "our product requires a call to use." Different positioning. Different conversion signal.

### What D93 Resolution Stays Settled
- Mandatory Guided Creation Flow: **killed**
- 5-minute / evening slot booking: **killed**
- Contact import as primary path: **killed**

### What D93 Resolution Changes
- Office hours link: **moved from onboarding to Settings/help as last resort**
- Discovery calls: **replaced with guerrilla testing at Point P**

---

**Verdict:** Free tier onboarding at launch = 90-second wizard (sensible defaults, no contact import, immediate access to "Créer un devis") + office hours link buried in Settings. No call offered during onboarding. Validate human-touch demand via guerrilla test, not warm-network discovery calls.
