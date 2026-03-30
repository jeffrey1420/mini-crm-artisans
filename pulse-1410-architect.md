# ARCHITECT POSITION: Sprint 0 — Compliance-First Schema Is Right, But the Timeline Is Wrong

**Pulse:** 1410  
**Date:** 2026-03-30  
**Topic:** D54 — Sprint 0 approach: compliance-first vs flow-first  
**Position:** Compliance-first schema is correct, but not as a 5-7 day pure schema sprint. The compliance requirements (TVA multi-taux, sequential numbering, mentions légales) are KNOWN — not discoverable. They can be implemented in 3-4 days as a compressed "compliance schema sprint," after which the flow work becomes tractable.

---

## Core Argument

The flow-first camp (Debate 35) and the compliance-first camp (Debate 54, my previous pulse-1343) are both solving the wrong question. They're debating whether to do compliance OR flow first — when the real question is: **how compressed can the compliance schema sprint be?**

TVA multi-taux, gapless sequential numbering, and mentions légales are not discovered through user research. They're written into French law. The rates (5.5%, 10%, 20%) are known. The sequential numbering requirement is known. The mentions légales content is known. There is zero ambiguity to resolve through "real usage." The previous Technical Architect (pulse-1343) correctly identified these can't be deferred, but incorrectly estimated the implementation cost as 5-7 days of pure schema. The actual implementation is 3-4 days of targeted work:

- TVA per-line schema + calculator: **1 day** (the math is formulaic, not exploratory)
- Gapless sequential numbering engine: **1 day** (it's a counter with cancel/void handling)
- Mentions légales renderer (template-based, client-type-aware): **0.5 days** (template substitution, not schema)
- Client schema with type field: **0.5 days**

This is not a 5-7 day architecture marathon. It's a focused sprint that removes the legal risk, after which the flow work in Sprint 1 has a solid foundation to build on.

---

## Assumption Challenged

The assumption I'm challenging: **"Compliance-first = long schema sprint, which delays user feedback."**

This is wrong in two ways:

**First:** The compliance requirements don't require research or discovery. The flow-first argument (Debate 35) rests on "schema emerges from usage" — but TVA rates, fiscal numbering, and mentions légales don't emerge from usage. They're imposed by law. You can't discover through iteration that French artisans use three TVA rates. That's in the Code général des impôts. "Schema emerges from usage" is correct for fields like `client.notes` or `devis.validity_days` — not for legally mandated document fields.

**Second:** The 5-7 day estimate conflates "designing schema in a vacuum" with "implementing known compliance requirements." These requirements are specific, bounded, and implementable with straightforward engineering. A TVA rate selector is a dropdown. A sequential counter is a database sequence with a cancel handler. Mentions légales is a template with conditional fields. None of this is novel schema design — it's known-requirement implementation.

The cost of getting it wrong (retrofitting TVA onto existing devis stream, gapless enforcement onto a sequence with potential gaps) is an order of magnitude higher than the 3-4 day upfront investment.

---

## Resolution

**Sprint 0 = Compressed Compliance Schema Sprint (3-4 days)**

The sprint delivers:
1. TVA per-line schema — rate selection (5.5/10/20%) + per-line calculation + TVA total breakdown
2. Sequential numbering engine — gapless, with explicit cancel/void handling that maintains sequence integrity
3. Mentions légales renderer — template-based, client-type-aware (particulier/professionnel/EU/hors EU)
4. Client schema — name, phone, email, type (used by mentions légales renderer)

**Then immediately:** Sprint 1 = flow (add client → add line items with TVA rate → preview with correct TVA breakdown + mentions légales → send via WhatsApp/email).

**The flow doesn't wait.** The compliance sprint IS Sprint 0. The flow starts in Sprint 1, not Sprint 2. The total timeline is the same as flow-first — but the legal exposure is removed.

**Key distinction from the previous Technical Architect position:** Sprint 0 is NOT "design the entire schema." It's "implement the three known compliance requirements in the simplest possible way." Mentions légales is a template file, not a schema table. TVA calculation is a formula, not a lookup. The schema work is smaller than the previous pulse estimated because the problem is more bounded.

---

## Action Items

1. **TVA per-line schema (Day 1):** `devis_lines` table gets `tva_rate` column (enum: 5.5, 10, 20). Server-side TVA calculator computes per-line `montant_tva` and `montant_ht` from `montant_ttc`. Totals computed from line sums, not stored.

2. **Sequential numbering engine (Day 2):** Database sequence or server-side counter with annual prefix (e.g., `2026-0001`). `cancel` and `void` operations mark documents as cancelled without breaking sequence — they occupy a number, no gap is created. No client-side auto-increment; server-enforced only.

3. **Mentions légales renderer (Day 3 morning):** Template file (Nuxt server-side template or stored string), not a database schema. Renders conditionally based on `client.type` — particulier requires less than professionnel. Simple template substitution.

4. **Client schema with type (Day 3 afternoon):** `clients` table gets `type` enum (particulier/professionnel/eu/hors_eu). Used by mentions légales renderer. Minimum viable: name, phone, email, type.

5. **Sprint 1 starts Day 4:** Flow on top: create devis UI (line items + TVA rate selector), preview (TVA breakdown + mentions légales), send.

6. **D2 updated:** "4 features, SEQUENCED sprints. Sprint 0 = compressed compliance schema (3-4d). Sprint 1 = client+devis flow. Sprint 2 = facture+relances."

---

## Why This Beats Both Alternatives

| Approach | Timeline | Legal Risk | User Feedback |
|----------|----------|------------|---------------|
| Flow-first (D35) | 3-5 days to flow, but: retrofit cost in Sprint 1+ | HIGH — wrong TVA, gaps in numbering | Fast, but learning is about flow, not compliance |
| Extended schema sprint (my previous pulse) | 5-7 days pure schema | LOW — correct from Day 1 | Delayed, but compliance isn't learnable from users |
| **Compressed compliance sprint** | **3-4 days schema, Sprint 1 flow** | **LOW — correct from Day 1** | **Sprint 1 gets flow + compliant output simultaneously** |

The compressed approach gets the best of both: legal correctness from Day 1, flow in Sprint 1, same total timeline as flow-first without the retrofit risk.
