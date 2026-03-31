# Position Paper: Against "3 Accepted Devis From 3 Distinct Clients"

**Author:** Product Strategist (PS-D153)
**Topic:** D96 — Path A Conversion Trigger
**Date:** 2026-03-31

---

## Core Position (1 sentence)

GS-D152's "3 accepted devis from 3 distinct clients" is more gameable than the anti-gaming table admits, measures deal-closing ability rather than product value, and is the wrong moment entirely — the real conversion trigger should be **first facture created**, not first accepted devis.

---

## What I'm Challenging

**Challenging GS-D152:**
1. "Distinct client" is not a meaningful discriminator — Marc can create 3 dummy clients in 15 minutes and accept 1 devis to each
2. The trigger measures deal-closing ability (independent of the software) not product value
3. "3 accepted devis" is a legacy number from D96's paid-facture era, never re-validated for this context
4. The anti-gaming table's "accepting a devis to yourself" gaming scenario is not clearly illegitimate

**Challenging my own prior position (PS-D146-3P):**
5. "First accepted devis + 3 active clients" was wrong. The "3 active clients" component was arbitrary, gameable, and theoretically ungrounded.
6. I now argue the correct trigger is **first facture created** — not "first accepted devis" — because creating a facture requires the complete workflow, proving end-to-end product usage.

---

## Key Arguments

### 1. "Distinct Client" Is Gameable — The Anti-Gaming Table Has a Blind Spot

GS-D152's anti-gaming table shows four scenarios. In every "gaming" scenario, Marc is gaming with EXISTING or IMPORTED clients. The table never addresses the simplest gaming path:

**The dummy-client attack:**
- Marc creates "Société Martin" (fake company, real phone number he controls)
- Marc creates "SARL Dupont" (fake)
- Marc creates "EI Ahmed" (fake)
- Sends a devis to each, accepts each from his app (or just marks each as "accepted" — acceptance tracking is broken for WhatsApp/phone acceptance anyway, per GS-D152's own argument)
- 3 accepted devis. 3 distinct clients. Trigger fires. Zero real business done.

GS-D152's diversity requirement only prevents gaming via **one** relationship. It does not prevent gaming via **three** fake relationships. The load-bearing assumption is: "creating fake clients is harder than creating fake deals." This is not obviously true. If the trigger is worth €29/month to Marc, he will find 15 minutes to create three fake clients.

**The definability problem compounds this:** What is a "distinct client"? Is it a unique database row? A unique email/phone combination? What prevents Marc from creating "Dupont Père" and "Dupont Fils" as separate clients with the same phone number? The "distinct" requirement is a natural-language constraint, not a technical one. It cannot be enforced in code without a client identity verification layer — which is not in scope for v1.

### 2. The Trigger Measures Deal-Closing Ability, Not Product Value

GS-D152 argues: "3 different jobs won is a stronger version of the same signal [accepted devis]." This is precisely the problem.

**The software does not win jobs. The software creates devis.**

Marc's ability to win 3 jobs depends on:
- His pricing competitiveness
- His reputation in the local market
- The quality of his craft
- His personal relationships with clients
- Luck (timing, competitor availability)

None of these are influenced by the software. The software's contribution is: Marc created professional-looking devis quickly, sent them via WhatsApp, tracked them, and got paid through the product. The trigger fires BEFORE any of that downstream value happens.

If Marc is charming and well-priced, he wins 3 deals using the app OR using WhatsApp directly. If Marc is over-priced or low-reputation, he loses 3 deals using the app OR WhatsApp. The trigger tells us about Marc's business, not about the software's value.

**The correct conversion moment is when the software delivers value — not when Marc's business acumen wins a deal.**

### 3. "3 Accepted Devis" Is a Legacy Number, Never Re-Validated

GS-D152 acknowledged: "The '3' number traces to D96's paid-facture era and was never re-validated for the accepted-devis trigger." This is a concession that demolishes the position.

D96 originally designed "3+ devis sent" as a SOFT gate preceding a hard gate of "first paid facture." The paid-facture gate was supposed to be the real conversion moment. When that was challenged and replaced, the "3" number was ported forward without behavioral revalidation.

We have no evidence that:
- 3 is the right threshold (vs. 1, 2, 4, or 5)
- The drop-off rate between 1 and 3 accepted devis is tolerable
- French artisans regularly produce 3 accepted devis within a trial window

If we're going to use a threshold trigger, we should instrument the funnel first and pick the threshold from data. GS-D152 is defending a number pulled from an obsolete framework.

### 4. "Accepting a Devis to Yourself" May Not Be Gaming

The anti-gaming table treats "Marc imports 6 old clients, accepts 1 devis to himself" as a gaming scenario. But GS-D152 themselves argued: "Acceptance events are hard to track in French BTP (WhatsApp/phone/in-person acceptance)."

If Marc creates a devis and marks it "accepted" — even to himself — he has completed the full acceptance workflow in the product. He has:
- Created a client record
- Created a devis with line items
- Marked it as accepted
- All timestamps and attribution are in the system

This is legitimate product usage. The fact that the client is Marc (or a dummy) is irrelevant to the software's contribution. He used the product correctly. The trigger fired. He experienced the product's value.

**The gaming label assumes bad faith. But a user stress-testing the acceptance workflow is a feature, not a bug.** The correct anti-gaming measure is not "who is the client" — it's "did real work happen through the product."

### 5. The Real Conversion Trigger: "First Facture Created"

**This is my primary counter-proposal. Drop accepted devis as the trigger. Use first facture created.**

Creating a facture requires:
1. A client record (exists)
2. A devis (created and sent)
3. The devis marked as accepted (client said yes)
4. A facture created from that accepted devis

**Every step of the product's value chain is validated before the trigger fires.** The artisan didn't just send devis — a client actually accepted and the artisan billed them. This is the moment the product has demonstrably moved money into the business.

**Why first facture beats first accepted devis:**
- Filters out deals lost after devis acceptance (client accepted, then found another contractor)
- Filters out verbal agreements that never became formal transactions
- Requires the full workflow (devis → acceptance → facture), not just the upstream event
- Is definitionally unambiguous: a facture row exists or it doesn't
- Doesn't require knowing whether acceptance was "real" — the facture is the real business outcome

**Why first facture beats "3 accepted devis from 3 distinct clients":**
- Fires sooner (1 event vs. 3), reducing the free-ride window
- No dummy-client attack possible (facture requires a billable event, not just a marked-accepted devis)
- The number 1 is not a legacy import from an obsolete framework
- Measures product value end-to-end, not deal-closing ability

**The single weakness:** For cash/check artisans who don't use the product for invoicing, the trigger may never fire. Counter: if Marc isn't using the product for invoicing, he isn't in the paid tier's target market. The Free tier holds his client data and devis workflow. That's sufficient.

---

## Challenged Assumptions (Explicitly Listed)

1. **"Distinct client" is a meaningful anti-gaming constraint** — challenged: creating 3 dummy clients is as easy as creating 1, and the system cannot verify client legitimacy
2. **3 accepted devis measures product value** — challenged: it measures deal-closing ability, which is independent of the software
3. **The number "3" is validated for the accepted-devis context** — challenged: it was ported from D96's paid-facture era without revalidation
4. **"Accepting a devis to yourself" is gaming** — challenged: completing the acceptance workflow in-app is legitimate product usage, not gaming
5. **"First accepted devis" is the right conversion moment** — challenged: first facture created is better because it requires the full workflow
6. **My prior position (PS-D146-3P): "3 active clients" meaningfully discriminates** — conceded and retracted: GS-D152 is correct that "3 active clients" is gameable. I was wrong.

---

## Verdict Recommendation

**Replace all Path A trigger candidates with: First Facture Created (hard gate)**

If first facture is too restrictive for cash-only artisans, the fallback is:

**Dual-gate for Path A:**
- Soft gate: First accepted devis (surface upgrade prompt, do not hard-block)
- Hard gate: First facture created (actual conversion moment)

Under this model:
- The artisan gets a first-accepted-devis notification: "Félicitations ! Vous avez gagné un client. Passez à €29 pourfactures illimitées et relances automatiques."
- The hard conversion happens at first facture, when the product has definitively delivered financial value

This resolves:
- GS-D152's valid anti-gaming concern (facture requires real transaction)
- PS-D146-3P's valid point that accepted devis is the right signal neighborhood
- The tracking ambiguity GS-D152 themselves acknowledged (WhatsApp/phone acceptance is hard to capture)
- The legacy "3" number problem (no legacy number, just 1)

**Kill "3 accepted devis from 3 distinct clients." Kill "first accepted devis + 3 active clients." Use first facture created.**

---

*Position paper PS-D153 — Product Strategist*
*Challenge to: GS-D152 (Growth Strategist D96 position)*
*Also challenges: PS-D146-3P (prior Product Strategist position)*
