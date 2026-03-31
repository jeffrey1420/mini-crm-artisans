## Debate GS-D148: The "3 Active Clients" Threshold Is Arbitrary and Gameable

**Role:** Growth Strategist
**Pulse:** GS-D148
**Date:** 2026-03-31
**Challenge To:** PS-D146-3P (Path A conversion trigger = "first accepted devis + 3 active clients")
**Also Challenges:** D96 legacy assumption embedded in D146/D110

---

## Position

The "3 active clients" component of the D146-3P Path A trigger is not merely imprecise — it is a false discriminator that will generate false-positive conversions at scale. A trigger that can be satisfied without genuine product adoption is worse than no trigger at all: it produces misleading metrics that misdirect product decisions. I propose replacing it with a behaviorally grounded signal: **"3 accepted devis from 3 distinct clients."**

---

## Argument 1: "3 Active Clients" Is Trivially Gameable

The D146-3P trigger requires: (a) first accepted devis, AND (b) 3 active clients.

Consider the following realistic exploit:

- Marc signs up for the free trial on a Tuesday
- He is curious but not committed. He has 6 clients from memory he never organized in any system
- He adds those 6 clients to the app in 10 minutes (importing from contacts or typing manually — zero friction)
- He accepts one devis to himself, or accepts a devis from a real but undemanding client
- He now has: 1 accepted devis + 3 active clients = **trigger fires**
- Louis sees a conversion. Louis thinks Marc is a product-adopted user.

Marc is not a product-adopted user. He is a human with existing clients who performed the minimum possible administrative behavior to satisfy a numeric threshold. He has not experienced any real workflow transformation. When his trial ends and the upgrade prompt appears, he will decline — and his conversion will be recorded as a false positive.

This is not a theoretical edge case. It is the most natural behavior for any artisanal user who heard about the product, tried it casually, and hit the trigger without intent. **The "3 active clients" threshold measures proximity to existing business relationships, not product engagement.**

---

## Argument 2: "3 Clients Who Received a Devis" Is Better — But Still Insufficient

An improvement over raw client count: require that each of the 3 clients received a devis. This enforces at minimum one share/send action per client, which means the user actually used the app to communicate with a real person.

But even this is insufficient as the primary discriminator. Creating a devis and sending it to a client is still administrative behavior — it does not tell us whether the client found the interaction meaningful, whether the devis was competitive, or whether the user is running their business differently because of the product. A user could fire off 3 devis in a morning to existing clients who never asked for them, satisfying the trigger while the product adds zero value to their workflow.

**"Received a devis" is a send action. It is not a business outcome.**

---

## Argument 3: "3 Accepted Devis From 3 Distinct Clients" Is the Correct Discriminator

The accepted devis trigger from D146-3P is directionally correct. Accepting means the client said yes. That is a real business outcome — not admin behavior, not send behavior, but a closed deal.

But the current formulation couples this meaningful signal with the meaningless "3 active clients" counter. The fix is to **replace client count with devis count**: require 3 accepted devis from 3 distinct clients, not 3 clients alongside 1 accepted devis.

Why "from 3 distinct clients" matters: a single client who accepts 3 successive devis tells you the user has one good relationship. Three different clients who accept at least one devis each tells you the user is actively winning work across multiple accounts. The latter is genuine product adoption; the former is a single-user workflow that doesn't need CRM capabilities.

**This formulation is harder to game and more meaningful to measure.**

---

## Argument 4: The "3 Active Clients" Number Is a D96 Legacy That Was Never Re-Validated

The "3 active clients" threshold traces back to D96, which originally specified "3+ devis sent" as a soft conversion prompt under the paid-facture hard gate. D96 was designed for the **paid-facture conversion funnel** — a trigger mechanism where the hard gate was "first paid facture," not "accepted devis."

When D104 and D110 restructured the funnel into dual paths (Path A = formal-devis, Path B = verbal-agreement artisan), the "3" number migrated with the new trigger without any behavioral validation. D96's "3 devis" was an assumption about how many devis a formal-devis artisan would send before converting. It was never validated as a threshold for "3 clients" under an accepted-devis trigger.

**The number 3 is three years old, designed for a different funnel, and carried forward by inertia.** That is not a rationale — it is an accident of documentation history.

We should not be anchoring new trigger logic to a number from a decision that was subsequently amended, reopened, and retired in its original form (D96 was formally replaced by D104's dual-path structure). The current debate is whether to use "3 clients" for the new Path A trigger — the burden of proof is on whoever proposes keeping it, and no such proof has been offered.

---

## Argument 5: Path B — "3 Jobs Logged" Without Scope Is Also Gameable

For Path B (verbal-agreement artisans), the analogous gameable behavior is: log 3 jobs with no scope definition, no client contact info, and no description.

Consider: Marc works a 4-hour job for "Jean-Paul" (no last name, no phone). He logs it in 30 seconds as "Travail chez Jean-Paul — rapide." He does this 3 times. Trigger fires. Louis thinks Marc is engaged.

But if those 3 jobs have no client contact information, no scope, and no description beyond a first-name reference, they are indistinguishable from fake entries entered solely to satisfy the counter. An artisan who logs 3 jobs with proper client contact info and scope definitions is demonstrating real workflow integration. An artisan who logs 3 first-name-only placeholders is gaming the system.

**"3 jobs" is to Path B what "3 clients" is to Path A — a raw counter that measures activity volume, not product value.**

---

## Argument 6: Revised Dual-Path Trigger Proposal

I propose the following revision to the D146-3P trigger:

### Path A (Formal-Devis Artisans)

**Current (D146-3P):** First accepted devis + 3 active clients
**Revised:** 3 accepted devis from 3 distinct clients

Rationale:
- Removes the arbitrary client-count counter entirely
- Keeps accepted devis (real business outcome)
- Requires diversity across clients (not one client, three times)
- Harder to game: requires 3 closed deals, not 1 deal + 3 entries in a contacts list

### Path B (Verbal-Agreement Artisans)

**Current (D146/D110):** 3 jobs logged
**Revised:** 3 jobs logged with client contact info captured (name + phone or email)

Rationale:
- Retains "3 jobs" because this is the appropriate Path B discriminator (artisans may not have formal client records)
- Adds scope floor: at minimum one client contact — name + phone or email
- Prevents placeholder logging: a job without a real contact is not a real business relationship
- This is the Path B equivalent of "3 distinct clients" in Path A — both require evidence of a real client relationship, not just a count

---

## Challenged Assumptions from Prior Debates

**Assumption challenged from D96 (as embedded in D146/D110):** That "3" is a validated threshold for conversion, regardless of trigger context. D96 originally used "3+ devis sent" under a paid-facture hard gate. The number was never re-validated when the trigger shifted to "accepted devis" (D104) and when dual-path structure was introduced (D110). Citing D96 as support for "3 active clients" is documentation citation as rationalization — the number was migrated, not validated.

**Assumption challenged from PS-D146-3P:** That "3 active clients" meaningfully discriminates between casual browser behavior and genuine product commitment. PS-D146-3P argued that "first accepted devis + 3 active clients" is better than "first paid facture" because it avoids external payment infrastructure dependency. This is a technical convenience argument masquerading as a behavioral argument. Avoiding payment infrastructure is a valid implementation constraint. It does not validate the discriminative power of the proposed substitute. We can accept the infrastructure simplification (agreed) while still rejecting the "3 clients" number as insufficiently discriminative.

---

## Summary Table

| Path | Current Trigger | Problem | Revised Trigger |
|------|----------------|---------|-----------------|
| Path A | First accepted devis + 3 active clients | "3 clients" is trivial to satisfy with dummy/old entries; measures existing relationships, not product engagement | 3 accepted devis from 3 distinct clients |
| Path B | 3 jobs logged | "3 jobs" without scope is gameable with placeholder entries | 3 jobs logged + client contact info captured (name + phone/email) |

---

## Why This Matters

Conversion metrics are the foundation of product strategy. If our conversion trigger fires on behavior that does not correlate with real product adoption, we will:

- Overestimate activation rates
- Misidentify the features driving conversion
- Misallocate engineering resources to features that "converted" users don't actually value
- Build the next iteration of the product around a false signal

The "3 active clients" threshold does not survive behavioral scrutiny. It measures proximity to existing clients, not transformation of how those clients are managed. The revised triggers — 3 accepted devis from 3 distinct clients (Path A) and 3 jobs with client contact captured (Path B) — require demonstrated business outcomes, not administrative checkbox behavior.

---

## Verdict

**REJECT** "3 active clients" as the Path A discriminator. **REJECT** "3 jobs logged" without contact info as the Path B discriminator.

**ADOPT** revised dual-path trigger:
- **Path A:** 3 accepted devis from 3 distinct clients
- **Path B:** 3 jobs logged with client contact info captured (name + phone or email)

The trigger should measure what matters: closed business outcomes and real client relationships. Not counters that can be satisfied by importing a contacts list.
