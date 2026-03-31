# Debate Pulse 0449 — Architect Position

## Sprint 1 Conversion Flow — What Happens After the Trigger Fires?

**D96 resolved:** Path A trigger = first `facture.created` (document event, not payment)
**D110 resolved:** Path B trigger = 5 jobs logged (no client contact gate) + contextual in-app banner, 60-day cooldown

**The question:** What is the in-app experience when either trigger fires? Hard paywall? Soft banner? Conversion modal? What copy/UX creates the upgrade moment without creating resentment?

---

## POSITION: The Celebratory Value-Forward Modal

### Core Argument

**1. The trigger fires at a high-intent moment — exploit it, don't neutralize it.**

Both D96 and D110 triggers fire at moments of genuine product engagement: the artisan just created their first professional invoice (Path A), or has habitually logged 5 jobs across multiple sessions (Path B). These are not moments of frustration or blockage — they are moments of accomplishment. The artisan has demonstrated that the product works for them. This is the highest-intent moment in the entire Free tier lifecycle. The upgrade prompt should land here like a natural conclusion to a story, not an interruption of one.

A hard paywall at this moment punishes the behavior we want to encourage. It says "you've succeeded — now pay." A soft banner at this moment wastes the highest-intent moment we'll ever have with this user. The modal exists because the moment deserves framing, not just notification.

**2. The modal must feel like a celebration before it feels like an ask.**

The emotional sequence matters: first, acknowledge what they've accomplished ("Votre première facture a été créée"). Second, reframe their situation through a value lens they haven't yet seen ("Vous avez un vrai business — il mérite un vrai outil"). Third, make the upgrade feel like the obvious next step, not a demand.

The copy must never use the word "limite" (limit), "bloqué" (blocked), or any countdown language. The Free tier is not presented as a truncated version — it's presented as the beginning of a story. The upgrade is the natural next chapter. This is not sleight of hand; it's accurate. The artisan genuinely has more business needs than the Free tier addresses. We're not manufacturing urgency; we're naming an existing reality.

**3. The Path A and Path B experiences are structurally identical, differently timed.**

Path A (first facture created): The modal fires immediately on `facture.created`, after the PDF is generated and the "sent" confirmation is shown. Natural pause point: the artisan has finished creating and sending a professional document. The modal appears as the logical coda.

Path B (5 jobs logged): The modal fires as an in-app banner — not a full-screen modal — because the trigger is quieter. The Path B artisan hasn't created a document yet; they're using the product as a job tracker. The banner is: *"Vous utilisez [App] depuis 3 semaines pour suivre vos interventions. Pour €29/mois, vos devis et factures sont générés automatiquement."* This matches the D110 resolution language exactly. One banner, 60-day cooldown, informational framing.

**4. Anti-gaming via workflow enforcement, not modal design.**

The D96 resolution correctly noted anti-gaming via workflow enforcement (accepted devis + client required before `facture.created` fires). The modal is not where anti-gaming lives — it's in the trigger conditions. The modal simply reflects what the system already knows: this artisan has crossed a threshold that demonstrates real business usage. A user who creates a fake facture to unlock the modal will find themselves on the €29 plan with no clients, no real business, and no reason to stay. The conversion will not stick. Anti-gaming is self-enforcing through the workflow itself.

---

## Assumption Challenged

**The assumption being challenged:** That the upgrade prompt should feel like a boundary ("you've hit your limit") rather than a milestone ("you've outgrown the free version").

Every prior debate on Free tier design (D43, D46, D63, D70, D96) has treated the conversion moment as a friction event — a wall, a ceiling, a blocked workflow. This framing is inherited from SaaS playbook tradition where trial expirations create urgency through loss. But for French artisans aged 45-55 who are skeptical of software subscriptions and have never been charged via credit card upfront, loss-framing at the moment of first real accomplishment is the wrong psychological move.

The alternative: the upgrade prompt celebrates outgrowing the Free tier, not being punished by it. "Vous avez un vrai business" reframes the €29 as a signal of success, not a cost. This is more aligned with the simplicity-first positioning (D12) and the no-countdown-anxiety Free tier design (D6 refined).

---

## VERDICT

**Path A (first `facture.created`):** Full-screen celebratory modal, fires on `facture.created` after send confirmation, once per user lifetime.

**Path B (5 jobs logged):** Contextual in-app banner (not modal), matches D110 resolution language, 60-day cooldown, shown once.

**Modal structure:**
1. Headline: "Votre première facture a été créée" (celebration, not announcement)
2. Subhead: "Vous avez un vrai business — il mérite un vrai outil."
3. Body: "Pour €29/mois, vous débloquez: devis illimités, factures avec mentions légales, relances automatiques, et export PDF professionnel."
4. CTA: "Continuer avec €29/mois" (primary, monthly framing)
5. Secondary: "Peut-être plus tard" (dismiss, no guilt, no countdown)

**Copy constraints:**
- Never "limite," "bloqué," "vous avez atteint," "il ne vous reste que"
- Always "vous avez," "vous voilà," "votre business"
- Value-forward, not scarcity-forward

**Timing:** Never interrupt active document creation. Fire only after completion confirmation (PDF generated or send confirmed). The modal appears in a paused state, not mid-flow.

**No countdown, no urgency timer, no "offre limitée."** The urgency is real: the artisan has real business needs the Free tier doesn't address. We name that reality without manufacturing artificial scarcity.

---

## Action Items

1. **Modal copy is written above** — product team adopts this framing verbatim or equivalent. Do not revert to loss/limit language.
2. **Path B banner uses D110 resolution language** — "Vous utilisez [App] depuis 3 semaines pour suivre vos interventions. Pour €29/mois, vos devis et factures sont générés automatiquement." Do not add urgency or countdown to the Path B banner.
3. **Implement once-per-lifetime modal firing for Path A** — store `conversionModalShown: true` on the user record, fire only on first `facture.created` where this flag is false. No re-fires.
4. **60-day cooldown on Path B banner** — matches D110 resolution, implement with `bannerShownAt` timestamp check.
5. **Path A anti-gaming is workflow-enforced, not modal-enforced** — accepted devis + client record required before `facture.created` fires the trigger. The modal does not need its own anti-gaming logic.
6. **Test the modal with Guerrilla usability protocol** — validate that "Votre première facture a été créée" + value framing produces positive emotional response before Sprint 1 implementation is finalized.

---

## Why Not the Alternatives

| Approach | Why Rejected |
|----------|-------------|
| Hard paywall (block feature use) | Punishes the exact behavior D96/D110 are designed to reward. Creates resentment before loyalty is built. French artisan trust problem (D46) makes hard walls backfire. |
| Soft banner only (no modal) | Wastes the highest-intent moment in the Free tier lifecycle. Both triggers fire at moments of genuine accomplishment — a banner is insufficient framing for that. |
| Countdown urgency ("offre limitée") | Manufactures scarcity that doesn't exist. Artisans will wait out the countdown. Destroys trust. |
| Email follow-up instead of in-app | Wrong channel (D40). WhatsApp-native artisans don't check email with urgency. The moment passes before the email lands. |
| Day-30 upsell (D138 model) | Correct for annual billing upsell. Wrong for in-product conversion trigger. The trigger fires on specific behavior, not calendar date. |
