# DEBATE D96 — Path A Conversion Trigger
## Product Strategist Position (PS-D153) — Rebuttal & Resolution

**Date:** 2026-03-31
**Status:** RESOLVED — Sprint 0 must decide now
**Author:** Product Strategist (PS-D153)

---

## 1. CHALLENGE TO POSITION A: The Payment Infrastructure Objection Is Based on a Flawed Premise

GS-D152 argues that "first facture created" requires Stripe/Lydia/Pix integration not in MVP scope. **This is wrong.**

A `facture` (invoice) in French business practice is first and foremost a **document** — a formatted PDF with line items, totals, TVA, payment terms. It does not require embedded payment. The payment happens via:
- Virement bancaire (bank transfer — outside system)
- Chèque (outside system)
- Espèces (cash — outside system)
- Eventually: Stripe/Lydia/Pix (optional, later phase)

**The trigger fires on `facture.created`, not `facture.paid`.** These are different state transitions. A user can create a facture today and receive payment in 30 days via virement. The conversion event is document creation, not payment receipt.

This means the payment infrastructure objection dissolves entirely. The trigger is achievable in MVP with zero payment API integration.

---

## 2. CHALLENGE TO POSITION B: "Distinct Client" Has No Technical Enforcement

GS-D152 presents "3 accepted devis from 3 distinct clients" as anti-gaming, but provides no mechanism for enforcing "distinct."

Consider the attack vector GS-D152 dismisses:
- Marc creates client "Entreprise Marc" → devis accepted
- Marc creates client "Marc SARL" → devis accepted  
- Marc creates client "Marc BTP" → devis accepted

Three accepted devis. Three "distinct" clients by name. All fake.

**The "distinct client" requirement is only meaningful if the system enforces client uniqueness through:**
- SIRET/SIREN validation (INSEE database lookup)
- Phone number verification (SMS OTP)
- Email domain verification
- Bank account verification

Without technical enforcement, "distinct clients" is **trust-based**, not **fact-based**. And trust-based anti-gaming on a self-serve SaaS tool is inherently broken.

GS-D152's own position undermines its strength by not addressing the enforcement gap.

---

## 3. REBUTTAL OF THE "Never Invoice" Argument

GS-D152's strongest point: many French artisans work on verbal agreements and never issue invoices.

This is valid for *why Path A is hard to reach*, but it does NOT argue for a weaker trigger. It argues for:

| Scenario | Path A Trigger | Outcome |
|---|---|---|
| Verbal deal, no invoice | First facture | Never converts |
| Written devis, accepted, no invoice | 3 accepted devis | Never converts |
| Both | First facture | Never converts if no invoice issued |

**If an artisan never creates a facture, they are not a converted customer by any reasonable definition.** The purpose of a devis/factures tool is to create those documents. Someone who refuses to document their deals is not a product user — they're a churned prospect.

The trigger should measure **product engagement through the core workflow**, not a proxy for "seriousness."

---

## 4. RESOLUTION: First Facture Created (With Explicit State Definition)

**Proposed Path A Trigger:**
> The user's workspace fires Path A conversion when the **first `facture` record is created** (status: `draft` or `sent` — not `paid`).

**Why this synthesizes both positions:**

| Requirement | PS-D153 original position | Resolution |
|---|---|---|
| Full value chain validated | Client + devis + accepted + facture | ✅ Maintained — cannot create facture without client and accepted devis |
| Unambiguous | No legacy number, clear state | ✅ `facture.created` is a single database event |
| Anti-gaming | (weak) "no dummy client attack" | ✅ Maintained — you still need accepted devis |
| Anti-gaming | (strong) "3 distinct clients" | ⚠️ Partially addressed — see below |
| MVP-compatible | Required Stripe (objection) | ✅ Resolved — payment integration not required |
| French artisan realism | Never invoice (objection) | ⚠️ Partially valid — but non-invoicing users are churn, not converted |

**Why "3 distinct clients" remains partially right but wrong on enforcement:**

GS-D152 is correct that "3 accepted devis from 3 distinct clients" raises the bar vs. a single devis. But without SIREN/SIRET enforcement in MVP, the distinctness is cosmetic. The real anti-gaming comes from:

1. **Accepted devis** — requires explicit client interaction ("yes I accept this quote")
2. **Facture creation** — requires actual line-item document production

The "3 distinct clients" suggestion conflates "more steps = better" with "enforced uniqueness = better." More steps helps. Enforced uniqueness requires infrastructure (INSEE API) not in MVP.

---

## 5. FINAL RECOMMENDATION

**Go with: First `facture` created**

**Implementation notes for Sprint 1:**
- The `facture` record should be create-able in `draft` state (no payment integration required)
- Path A fires on `facture.created` event, regardless of payment status
- Consider adding a soft notification: "You created your first invoice! Path A unlocked." (avoids hard "conversion" framing during onboarding)

**Deferred to post-MVP (Path B or v1.1):**
- SIRET/SIREN validation for client uniqueness enforcement
- Payment integration (Stripe/Lydia/Pix) for `facture.paid` trigger variant

**The debate is resolved. Sprint 1 UX can proceed with a clear trigger definition.**

---

*PS-D153 — Product Strategist position, original Position A confirmed as correct with clarified state definition.*
