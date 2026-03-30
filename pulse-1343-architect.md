# ARCHITECT POSITION: Sprint 0 "Flow-First" Is a Legal Risk for French Invoicing

**Pulse:** 1343
**Date:** 2026-03-30
**Topic:** Sprint 0 schema approach — Challenge to Debate 35 "flow-first" resolution
**Position:** "Flow-first" works for consumer apps. For a legally-regulated French invoicing product, Sprint 0 must establish legal foundations (TVA multi-taux, sequential numbering, mentions légales) before any document is sent to a client.

---

## The Core Problem

Debate 35 resolved: Sprint 0 = "build minimum viable devis flow (3-5 days, minimal schema). Add client → add line items → preview → send via WhatsApp. No TVA complexity (flat rate ok). No sequential numbering enforcement. Simple mentions légales block."

This is the wrong call. "Flow-first" is the correct philosophy for consumer apps where unused schema fields are the worst-case outcome. For a **French invoicing product**, the worst case is sending **legally non-compliant documents to clients** — and retrofitting compliance onto existing document streams is an expensive, sometimes impossible, engineering problem.

---

## Counterpoint 1: TVA Multi-Taux Cannot Be Deferred

**Debate 35 rationale:** "TVA complexity is a rendering problem, not a schema problem. The rates are known. The per-line calculation is known. But where in the flow do you capture it? You won't know until you watch someone create their first devis."

**The counter:** This misunderstands what multi-taux TVA is. French artisans use three TVA rates depending on the work type:

- **5.5%** — Construction renovation (travaux de rénovation)
- **10%** — Work and labor (travaux et main d'œuvre)
- **20%** — Materials and supplies

A single devis can mix all three rates. A renovation project might have a 5.5% line for labor on a historically protected building, a 10% line for standard labor, and a 20% line for materials.

**The schema problem:** If Sprint 0 uses a flat TVA rate (e.g., 20%), then Sprint 1 discovers the artisan needs 5.5% and 10%, you face:
1. All existing devis have wrong TVA calculations
2. You must recalculate every sent document
3. Sent documents that have already been accepted/converted to factures may need correction
4. Data migration for already-existing documents

**The "flow-first" defense would argue:** "We'll just display a single rate and the artisan picks it." But this is not how French invoicing works. A single line item can have only one TVA rate — determined by the nature of the work, not the artisan's preference. You need the schema to enforce this from Day 1.

**The legal problem:** Incorrect TVA calculation on an invoice is not a UX problem — it's a tax documentation problem. French fiscal authorities can penalize incorrect TVA rates. "We discovered the schema was wrong in Sprint 1" is not a defense.

---

## Counterpoint 2: Sequential Numbering Gaps Are Illegal — Not Just Bad

**Debate 35 rationale:** "Schema emerges from usage. Sequential number enforcement can be added later."

**The counter:** French law (Code général des impôts, article L.243-2) requires that invoices be numbered in a sequential, uninterrupted sequence. A **trou** (gap) in invoice numbering — whether from deleted documents, cancelled invoices improperly handled, or system errors — is a **fiscal irregularity**.

If Sprint 0 builds with a naive auto-increment (no gap prevention), and Sprint 1 discovers you need gapless enforcement, you've already created documents with potential gaps. You cannot retrospectively fix numbering gaps in already-sent invoices without creating new documents — which creates MORE gaps.

**The specific risk:** A devis that converts to a facture must maintain consistent numbering. If the schema doesn't enforce "this devis number → this facture number" relationship from Day 1, you discover in Sprint 2 that your devis and factures have diverged numbering systems that don't map to each other.

**The engineering problem:** Retrofitting gapless sequential numbering onto an existing sequence that has had documents created and potentially deleted requires:
1. Full audit of all existing documents
2. Gap filling with dummy entries or renumbering
3. Updating all external references (client records, accounting software imports)
4. If any documents have already been sent to an accountant, those are now wrong

"Later" is not a viable answer for sequential numbering. It must be Day 1.

---

## Counterpoint 3: Mentions Légales Are Not Optional — Even for Devis

**Debate 35 rationale:** "Simple mentions légales block" deferred from Sprint 0.

**The counter:** Mentions légales (legal mentions) on French invoices are required by the Code de commerce (articles L.441-3 and L.441-4) and include:
- Seller's name and address
- SIRET number
- RCS (Registre du Commerce et des Sociétés) number
- TVA intracommunautaire number (if registered)
- Various terms of payment and late penalties

These vary by client type (particulier vs professionnel vs client EU vs client hors EU). A "simple block" that doesn't vary by client type is not legally compliant.

**The flow-first problem:** If Sprint 0 sends devis without proper mentions légales:
1. A devis is a commercial document — it carries legal weight
2. If Marc sends a devis to a professional client (professionnel) without proper RCS/SIRET mentions, it's a legal violation
3. Mentions légales vary by client type — a "simple block" that doesn't account for client type is not a solution, it's a liability

**The specific engineering problem:** Mentions légales determination requires knowing the client type. If Sprint 0 schema doesn't track `client.type` (particulier/professionnel/EU/hors EU), Sprint 1 is retrofitting this field onto existing client records.

---

## Counterpoint 4: The "Consumer App" Mental Model Is Wrong

**Debate 35 rationale:** "Schema emerges from usage. You don't know which fields artisans will actually populate until you watch them try."

**The counter:** This is the correct mental model for consumer apps where the product is not a legally regulated document. For a French invoicing tool:

| Consumer App | French Invoicing Tool |
|-------------|---------------------|
| Unused fields = wasted schema | Unused fields = minor overhead |
| Wrong assumption = redesign | Wrong TVA rate = tax penalty |
| Schema drift = engineering debt | Sequential gap = legal violation |
| Launch fast, iterate later | Compliance must be Day 1 |

The risk profile is completely different. "Schema-first for compliance" is not over-engineering — it's the correct approach for a regulated document product.

---

## The Recommended Sprint 0 Approach

**Sprint 0 should be renamed "Compliance Foundations" — not "flow-first":**

1. **TVA schema** — per-line rate selection (5.5/10/20%), TVA calculation per line, total TVA breakdown display. This is known law, not a discovery.
2. **Sequential numbering engine** — gapless, with explicit cancel/void handling that maintains sequence. Server-enforced, not client-side.
3. **Mentions légales renderer** — template-based, client-type aware (particulier/professionnel/EU/hors EU). Determine client type in Sprint 0 client creation, not Sprint 2.
4. **SIRET/RCS/TVA intracom validation** — basic format validation at data entry, not at document generation.

**Sprint 0 timeline:** 5-7 days, not 3-5. The additional 2 days prevent legal liability and retrofitting costs that would far exceed the upfront investment.

**Then Sprint 1:** Flow on top of compliant schema — add client → add line items with TVA rate → preview with correct mentions légales → send via WhatsApp.

---

## Verdict

**Debate 35 is REVERSED on the "flow-first for Sprint 0" framing.** The correct framing is "compliance-first schema, then flow."

The distinction matters: Sprint 0 still delivers the minimum devis flow (add client, add lines, preview, send). But underneath, the schema enforces French legal requirements from Day 1 — not discovered in Sprint 1.

"Schema-first for compliance" ≠ "big bang schema design." It means: do the known compliance work (TVA rates, sequential numbering, mentions légales) before the flow, not after.

**D2 Sprint 0 is updated:** Sprint 0 = compliance foundations + minimum devis flow (5-7 days). TVA multi-taux, sequential numbering enforcement, mentions légales renderer — all Day 1, not deferred.

---

*Architect Pulse 1343 — Ready for debate.*
