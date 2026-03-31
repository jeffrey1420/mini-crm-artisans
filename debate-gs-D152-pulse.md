## Debate GS-D152: Path A Conversion Trigger — "3 Accepted Devis From 3 Distinct Clients" Is the Only Anti-Gaming Option

### Growth Strategist — Defend: 3 Accepted Devis From 3 Distinct Clients

**Assumption challenged:** PS-D146-3P's core assumption that "3 active clients" meaningfully discriminates between casual browser behavior and genuine product commitment — and the secondary assumption that acceptance events are reliably trackable at the Point-of-Sale moment.

---

**Core arguments:**

1. **"3 active clients" is trivially gameable in 10 minutes.**
   Marc opens the app, creates 6 client entries from memory (Jean-Paul, Sophie, Didier, Maria, Ahmed, Laurent), accepts one devis to himself, and the trigger fires. He has zero new clients, zero additional product usage, zero behavioral change. The "3 active clients" signal measures proximity to his existing contact list — not engagement with Louis's product. This is the wrong proxy for conversion intent. Any metric that a non-technical artisan can satisfy in 10 minutes without changing how they work is not a conversion metric. It's a CSV import metric.

2. **"3 accepted devis from 3 distinct clients" requires 3 closed deals across 3 different people.**
   The diversity requirement is load-bearing. One accepted devis to yourself (gaming the trigger) doesn't satisfy "3 distinct clients." Three accepted devis means three separate clients said yes to a price — three real jobs landed through the product. This is the behavioral equivalent of the product earning its keep. The trigger fires when the product has demonstrably moved money into Marc's business, not when Marc has demonstrated he knows how to fill in a form.

3. **The "3" number traces to D96's paid-facture era and was never re-validated for the accepted-devis trigger.**
   D96 originally designed "3+ devis sent" as a soft gate preceding the hard gate of "first paid facture." When the paid-facture hard gate was challenged and replaced with accepted-devis (PS-D146-3P's own innovation), the "3" number was imported without behavioral revalidation. We don't know that 3 accepted devis is the right threshold. We know 3 was the right threshold for 3 devis *sent* under a payment-gated funnel. These are different behaviors with different drop-off rates. The correct validation approach: instrument both triggers (accepted-devis count and accepted-devis + client count) and compare conversion-to-paid rates post-launch.

4. **Accepted devis = client said yes = real business outcome = the correct conversion moment.**
   PS-D146-3P is correct that accepted devis is the right conversion signal (vs paid-facture which introduces external payment dependencies). But PS-D146-3P undermines its own argument by diluting the accepted-devis signal with a "3 active clients" component that has no theoretical grounding in the product's value delivery. If accepted devis is the right moment, then 3 accepted devis (not "1 accepted devis + 3 active clients") is the logically consistent position. PS-D146-3P argues the aha moment is "job won through the app" — but 3 different jobs won is a stronger version of that same signal.

5. **"3 distinct clients" ensures the trigger fires across the actual client portfolio, not a single imported contact.**
   The product's value proposition is "manage your client relationships." A conversion event that requires 3 distinct clients means Marc is using the app as intended — not just keeping one contact's details in the system. This aligns the trigger with the product's core use case. The conversion event and the product's value delivery are the same behavior.

6. **PS-D146-3P's "3 active clients" introduces a tracking dependency that doesn't exist in the product.**
   "Active client" requires a definition: Is it a client with any interaction in 30 days? 90 days? A client who has received a devis? A client who has accepted a devis? PS-D146-3P never specifies. Every definition introduces edge cases: What if Marc sends a devis to a one-time client, gets no response, and the client goes inactive — does that still count? "3 accepted devis from 3 distinct clients" is definitionally precise: accepted devis events are timestamped, client-attributed, and unambiguous. No ambiguity about what "active" means.

7. **The trigger should gate premium access with real behavioral skin in the game.**
   Premium access (the conversion event) should require the user to have demonstrated genuine product value. Three accepted devis across three clients means three separate instances of the product delivering value (client trust, professional document, pricing clarity). This is the right moment to ask for payment. "3 active clients" means Louis is asking for payment before the product has done anything a phone contacts app couldn't do equally well.

**The anti-gaming test:**

| Scenario | PS-D146-3P trigger fires? | GS-D152 trigger fires? |
|----------|--------------------------|------------------------|
| Marc imports 6 old clients, accepts 1 devis to himself | YES | NO |
| Marc creates 3 clients, accepts 3 devis to 3 real clients | YES | YES |
| Marc creates 1 client, accepts 3 devis to same client | YES (3 active clients?) | NO (not 3 distinct) |
| Marc does nothing, 3 old clients already in system | YES (if "active" = any contact) | NO (no accepted devis) |

GS-D152 fires only in the genuine adoption scenario. PS-D146-3P fires in three of four gaming scenarios.

**Challenge to PS-D146-3P's assumption about acceptance event trackability:**

PS-D146-3P assumes acceptance events are reliably trackable ("client says yes to a price = real business outcome"). This is actually harder to track than it sounds. In French B2C/BTP contexts, devis acceptance happens over WhatsApp, phone call, or in-person — not through a product UI action. Marc may never mark a devis as accepted in the app. If Louis is relying on Marc to manually mark "accepted," the acceptance rate will be near zero for Path A users. GS-D152's "3 accepted devis" trigger is equally vulnerable to this tracking gap — but this vulnerability is an argument for better onboarding around marking acceptance (a value-delivery moment worth prompting), not an argument for replacing the trigger with a softer signal.

**The honest fix for acceptance event tracking:**
If accepted devis is the right signal but artisans won't mark it, the solution is: when Marc sends a devis and the client responds (any channel), prompt Marc: "Client accepted? Tap yes to mark as accepted — this counts toward your free trial completion." This is a 1-day addition to onboarding. The alternative (lowering the bar to "3 active clients") doesn't fix the tracking gap — it just hides it behind a signal that's even harder to interpret.

**Verdict:** D96 Path A trigger should be **"3 accepted devis from 3 distinct clients"** — not "first accepted devis + 3 active clients." The latter is gameable, measures wrong behavior, and introduces definitional ambiguity around "active." Louis should confirm GS-D152 position as the resolved Path A trigger.

**Open question for Louis:** Confirm that acceptance event tracking via in-app prompt (when client responds after devis sent) is acceptable as the instrumentation approach. If not, the trigger must be revisited — but "3 active clients" is not the alternative.
