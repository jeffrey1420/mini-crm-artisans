# Debate: Document Archive — Retention Asset or Conversion Liability?

**Strategist:** Growth Strategist
**Date:** 2026-03-30
**Status:** RESOLVED

---

## The Core Tension

D70 resolved: document archive = PRIMARY Free tier value. Every devis/facture sent, organized by client, searchable, beautiful PDF renderer. This is the main acquisition hook.

D96 resolved: limit-hit (5 active devis OR 10 clients) = hard conversion gate. First paid facture = soft milestone prompt.

D99 resolved: usage-based billing (€1.50/devis, capped at €29) at launch.

**The unresolved tension:**
The document archive is a retention asset — it gets more valuable over time as the artisan's professional history accumulates. A Free tier user with 3 months of sent devis has a document archive worth keeping. Why would they ever leave the Free tier? The archive is complete, satisfying, and growing. The €29 upgrade offers... what exactly?

The resolution chain created a Free tier that's too satisfying to leave, without a specific reason to upgrade.

---

## Arguments For: Document Archive as Acquisition Hook (Current Resolution)

**D70's decision is correct for acquisition:**

1. **Differentiated from Pennylane/Indy.** They do financial dashboards. The document archive is ours. It solves the "where did I put that devis I sent to Dupont in March?" problem that no competitor solves well for artisans.

2. **Compounding value.** Every sent devis adds to the archive. The longer Marc uses the product, the more valuable the archive becomes. This is the right retention mechanic for a document-focused product.

3. **The archive is what Marc actually wants.** He's not thinking "I need CRM software." He's thinking "I need to find that devis I sent last month." The archive solves his actual daily problem.

4. **Switching cost builds naturally.** After 6 months of devis history in the archive, leaving means losing that history. The archive creates switching cost organically, without artificial lock-in.

**These arguments are correct for retention. They do not address conversion.**

---

## Arguments Against: Document Archive Creates "Good Enough" Lock-in

**The conversion problem:**

The document archive satisfying Marc on Free tier is a retention feature. But retention and conversion are different problems:

- **Retention:** Keep Marc using the product, delay churn
- **Conversion:** Make Marc willing to pay €29/month

A satisfying Free tier creates retention without creating urgency. The archive grows every month. Marc never hits a wall. He never NEEDS to upgrade — the Free tier keeps delivering more value. The limit-hit at 5 devis/10 clients is a nuisance he works around (delete old clients? just don't add new ones?) rather than a genuine upgrade trigger.

**The D96 limit-hit is not the answer:**

D96's limit-hit is a hard gate: 5 active devis OR 10 clients. When Marc hits 5/5, he sees an upgrade prompt. But:

- The document archive is his entire history — deleting clients to make room feels like losing his archive
- The upgrade pitch is "unlimited devis" — but if he's sending 5/month and the archive is satisfying, why does he need unlimited?
- The financial snapshot (€29 feature per D70) is supposed to be the upgrade pull — but if Marc is a repeat-client artisan who rarely sends new formal devis, the financial snapshot is empty anyway

**The repeat-client failure mode (from D76/D96):**

Marc has 6 steady clients. He sends them devis occasionally. His archive grows. He hits 5/5 when he adds a 6th client. The upgrade prompt fires. The pitch: "unlimited clients + financial snapshot."

But his 6 steady clients don't generate new formal devis regularly. His financial snapshot shows: 1 pending devis from March. The €29 upgrade for "financial intelligence" doesn't make sense when his pipeline is 2 steady clients and verbal agreements.

The archive keeps him satisfied. The €29 tier offers things he doesn't need.

---

## The Specific Failure Mode

Walk through what happens when Marc hits 5/5 active devis on the Free tier:

**Day 1:** Marc tries to add a 7th client. App says: "Vous avez atteint la limite de 5 devis." Two options: "Passer à €29" or "Supprimer un ancien devis."

**What Marc thinks:**
- "I can't delete my archived devis — that's my history."
- "Do I really need to track 6 clients right now? I can just remember the 7th one."
- "€29/month for what? I only send 3 devis a month anyway."

**What happens:** He either suppresses the new client (mental workaround) or ignores the prompt. He doesn't upgrade.

**The resentment builds:** The product is now a minor friction in his workflow. Not enough to make him leave (the archive is still valuable). Not enough to make him pay. He's stuck in the middle — a "free forever" user who would have converted if the upgrade had made sense.

**This is the "free forever" trap.** Not dramatic churn — just quiet, permanent non-conversion.

---

## Resolution: How the Document Archive Should Work With Conversion

**The archive was resolved as the PRIMARY Free tier value. This is correct. But it needs a conversion partner — something the archive alone cannot provide.**

**The conversion design must answer:** "Why do I need €29 when my archive is working fine?"

**Three specific recommendations:**

**Recommendation 1: The archive must have a visible ceiling that makes €29 feel necessary.**

The Free tier archive should show Marc his archive, but with a visible "this archive is incomplete without the financial intelligence layer." For example:

- Free tier: full archive of sent devis, organized by client
- €29 tier: same archive + " Vue d'ensemble" — every client has a financial status (pending/payed/expired), every devis has a timeline

The archive alone is a filing cabinet. The archive + financial status is a business management tool. The differentiation is visible and understandable.

**Recommendation 2: The limit-hit notification must give agency, not just a wall.**

"You've reached your limit" is a dead end. The D96 hard gate at 5/5 creates a wall with two bad options.

Replace with: "Votre activité grandit. Avec le plan Pro, chaque client a son tableau de bord complet — devis en attente, paiements reçus, relances automatiques."

This frames the upgrade as solving a problem he recognizes (his business is growing, he needs better tracking) rather than escaping a quota he's managed around.

**Recommendation 3: The financial snapshot must be visible in the Free tier — but incomplete.**

D70 moved the financial snapshot to €29 tier. This was correct to avoid the Pennylane/Indy positioning problem. But an invisible financial snapshot creates no conversion pressure.

The right design: Marc can see the financial snapshot exists (€29 tier gets the full version), but the Free tier shows a teaser:

- Free tier: "Vous avez 3 devis en attente de réponse" — visible but no amounts, no aging, no pipeline value
- €29 tier: "Vous avez €4,200 en devis acceptés en attente de paiement" — full pipeline intelligence

The teaser creates curiosity without giving away the feature. "What would I see if I had the full view?" is a more effective conversion trigger than "your limit is 5."

---

## What €29 Must Exclude From Free

**The €29 tier must provide something the document archive alone cannot:**

| Feature | Free | €29 |
|---------|------|-----|
| Document archive | ✓ | ✓ |
| Search/filter | ✓ | ✓ |
| Financial snapshot teaser (count only) | ✓ | ✗ |
| Financial snapshot full (amounts + aging) | ✗ | ✓ |
| Relances automatiques | ✗ | ✓ |
| Unlimited clients | ✗ | ✓ |
| Priority support (WhatsApp to Louis) | ✗ | ✓ |

**The key insight:** The archive + financial teaser creates curiosity. The full financial snapshot + relances + unlimited + support = the complete package. The conversion trigger is not "you hit a limit" — it's "you can see what you're missing."

---

## Resolution

**RESOLVED — Document archive is PRIMARY Free tier value (D70 confirmed). But three changes required:**

1. **Financial snapshot teaser in Free tier** — show count of pending/payed devis, not amounts. The teaser creates curiosity without full feature exposure.

2. **Upgrade prompt reframed as growth acknowledgment** — not "you hit a wall" but "your business is growing, here's what you need." Agency given: the upgrade solves a problem he recognizes.

3. **€29 tier must be visible as the complete package** — the archive alone is a filing cabinet. Archive + financial snapshot + relances + unlimited + support = a real business tool. Show Marc what he's missing, don't just block him.

**The "free forever" trap is prevented** not by making the Free tier worse, but by making the €29 tier clearly and visibly better in a way that matters for his business growth.

**Action item for TODO.md:** Update Free tier spec to include financial snapshot teaser (count only). Update upgrade prompt copy to frame as growth, not wall. Add "complete package" visibility to €29 tier so the conversion trigger is curiosity, not desperation.