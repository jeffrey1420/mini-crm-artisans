# POSITION PAPER: Growth Strategist
**Date:** 2026-03-31 07:09
**Re:** D158 Revisited — Path B Conversion Strategy Is Built on a Contradiction
**Status:** CHALLENGE — Fundamental redesign proposed

---

## Challenge Headline

**Path B Cannot Be Converted Through a Document-Based Trigger — By Definition**

The "3 factures created, 0 accepted devis" trigger is not just wrong — it is logically incoherent. It requires Path B artisans to transform their workflow *before* the trigger fires, making the trigger consequence rather than cause. We are designing a conversion mechanism for a user who, by our own definition of Path B, does not exist in our product.

---

## Assumption Challenged

**Assumption:** Path B artisans (verbal-agreement, cash-payment, ~40-50% of target market) will naturally begin creating formal factures once they have the app, and will accumulate enough to hit the "3 factures created" threshold.

**The contradiction:** Path B is defined precisely as artisans who operate outside formal document workflows. They give handwritten receipts. They take cash at the job site. They don't issue devis because clients don't ask for them. The 06:30 verdict replaced "5 jobs logged" (Sprint 1 infrastructure) with "3 factures created" (Sprint 0-compatible) — but "Sprint 0-compatible" is not the same as "correct." The trigger is Sprint 0-compatible only in the narrow technical sense that factures ship in Sprint 0. It is wrong in every meaningful product and behavioral sense.

---

## Core Arguments

### 1. The Trigger Fires AFTER the Behavior Change — It's Backwards

"3 factures created" means the artisan has already transformed their workflow from verbal/cash to formal invoicing. The trigger that prompts conversion fires *after* they've become the kind of artisan who creates formal factures. But the entire premise of Path B is that this transformation does not happen organically. The trigger presupposes the very behavior it is meant to prompt.

This is not a threshold calibration problem. Adjusting from "3 factures" to "1 facture" does not fix it — it still requires Path B artisans to adopt a document-first workflow as a precondition for conversion. We are asking them to become Path A users before we prompt them to pay.

**Analogy:** Asking a non-swimmer to tread water for 10 minutes before offering them a life vest.

---

### 2. Path B's Actual Trigger Moment Is Identical to Path A's

Both archetypes share the same conversion trigger moment: the first time a client asks for a formal devis and the artisan feels the pain of NOT having the app.

For Path A, this is routine — clients regularly request formal devis, and the artisan feels friction without a tool. For Path B, this is a rupture event — a client who previously accepted verbal agreements suddenly requests a formal document. This is the "why didn't I have this already?" moment.

The conversion trigger should fire at the **first formal-devis attempt** — not at a downstream count of factures. The rupture event IS the conversion moment for both paths. The difference is only frequency, not nature.

---

### 3. The Intent Signal Has Already Fired — We're Not Capturing It

The Path B artisan who downloads this app is already showing intent. He recognized, at least once, that he needed a formalization tool. He found us. He signed up.

We are discarding that signal and waiting for downstream document counts that will never come. The trigger should capture the **moment of recognized intent** — the download, the first client entry, the first session where he explores document creation — not a document count that requires weeks of behavior change.

A Path B user who enters 3 clients and never creates a devis is not disengaged. He is actively using the product for job tracking. He is deriving value. He is exactly the user we want to convert — but the trigger architecture cannot see him.

---

### 4. Designing a Document-Based Conversion for Non-Document Users Is Building for a Phantom

If Path B artisans never create formal factures — by definition — then "3 factures created" is a trigger for a user who doesn't exist in our product. We are engineering a conversion funnel for a segment that, by our own research, operates outside the document lifecycle.

This is not a gap in the trigger. It is a category error. The trigger cannot be calibrated to fix it because the trigger and the user are logically incompatible.

**What we actually have:** A product that requires formal devis/facture workflows to generate conversion signals, being marketed to a market segment that predominantly operates outside those workflows.

---

### 5. The Correct Path B Trigger Fires on the Behavior Gap, Not the Behavior

The correct signal is not "factures created" — it is **"active but not formalizing."** This is a behavior gap, not a behavior count.

Two concrete trigger candidates:

**Candidate A: "3 clients entered + 7 days active + 0 formal documents"**
- Fires on the gap between engagement (active, adding clients) and formalization (no devis/facture sent)
- This captures the artisan who is using the product but hasn't felt the rupture yet
- The prompt: "Vous utilisez [Product] depuis une semaine. Vos clients sont là. Quand un client vous demande un devis officiel, vous serez prêt." — frames the product as preparation, not urgency

**Candidate B: "Second client entry + 0 formal documents ever"**
- The first client entry is exploration. The second client entry is intent.
- At that moment, the artisan is demonstrating they have a recurring workflow — not a one-time admin task
- This fires earlier than any document-count trigger and captures the intent moment before it fades

---

### 6. Proposed Replacement Trigger

**"7 days active + at least 3 client entries + 0 formal documents created"**

- **Active:** App opened at least once in last 7 days
- **3 client entries:** Demonstrates workflow habit, not one-time curiosity
- **0 formal documents:** Fires on the gap, not the behavior
- **Prompt framing:** "Vos clients et vos travaux sont enregistrés. Pour €29/mois, vos devis et factures s'ajoutent sans limite." — upgrade as natural extension of what he's already doing, not a wall he hits

This trigger fires on the behavior gap (active but not formalizing) rather than on formalization behavior itself. It identifies artisans who are finding value in the product's non-document features and prompts conversion by making the upgrade feel like a natural expansion, not a requirement.

---

### 7. The Expert-Comptable Channel Is the Right Path B Acquisition — Not In-App Conversion

There is a deeper challenge worth raising: **is Path B a Sprint 0 conversion target at all?**

Path B artisans (verbal-agreement, cash-payment) are not just a different conversion archetype — they are a different business stage. They are, by definition, less formalized businesses. The expert-comptable (accountant) who serves these artisans is the natural channel for formalization: they are the ones who tell Path B artisans when and how to start issuing formal invoices.

The expert-comptable referral channel (U12, designated Phase 2) is actually the correct path to Path B formalization — not an in-app conversion trigger. We should not be designing in-app prompts to convert users who need an accountant's guidance first.

**Implication:** Path B conversion may belong in a different product lifecycle phase — after expert-comptable partnerships have formalized their businesses. Sprint 0 Path B "conversion" may be better redefined as Path B *retention* (keep them active until the expert-comptable formalizes them) rather than Path B *conversion* (prompt them to pay before their business is ready to pay).

---

## Verdict Proposal

| Decision | Current State | Proposed State |
|----------|-------------|----------------|
| D110 Path B trigger | "3 factures created, 0 accepted devis" | RETIRED — logically incoherent for Path B |
| Path B trigger (new) | Not defined | "7 days active + ≥3 client entries + 0 formal documents" |
| Path B Sprint 0 scope | In-app conversion trigger | RETAINED — but trigger is behavior-gap, not document-count |
| Path B longer-term | In-app conversion | Expert-comptable referral (Phase 2) is the correct formalization channel |
| U16 (Path B discovery) | Sprint 1 task | KEEP — but specifically: validate behavior-gap trigger thresholds, not "do Path B users exist?" |

**What Louis must decide:**
1. Accept that Path B conversion cannot use document-based triggers — confirm or reject
2. If confirmed: implement behavior-gap trigger ("7d active + ≥3 clients + 0 docs") as Path B conversion mechanism
3. If confirmed: acknowledge expert-comptable channel is the structural Path B conversion path, and in-app trigger is a bridge/retention tool for Path B users who will formalize later
4. U16 Path B discovery is still critical — but it should validate trigger thresholds, not question whether Path B exists

---

## Status

**OPEN — Requires Louis Decision**

This is a fundamental challenge to D110 (06:30 verdict). The 06:30 resolution ("3 factures created, 0 accepted devis") was Sprint 0-compatible in implementation terms but wrong in product logic. D158 was raised at 06:50 but was not resolved before this position paper was written.

Louis: the question is not "what threshold?" The question is "can a document count ever be the right trigger for a non-document user?" My position is no. The trigger must fire on the behavior gap, not the behavior itself.

---

*Growth Strategist — Mini-CRM Research*
*Position paper: gs-d158-revisited-0709*
