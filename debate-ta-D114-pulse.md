# Debate TA-D114-Pulse: Technical Architect — PDF Legal Sufficiency Challenge

**Role:** Technical Architect  
**Debate:** D114 — PDF Generation for Sprint 0  
**Pulse timestamp:** 2026-03-30T22:30  
**Assumption challenged:** "Ephemeral PDF is legally sufficient for Sprint 0"

---

## The Assumption

D119 argues that expo-print's in-memory PDF generation is the correct Sprint 0 approach because: "storage for archival is a v2 concern." The PDF is an ephemeral render artifact — it lives in WhatsApp, gets re-shared by the client, and disappears from the artisan's phone when they delete it. D119 frames this as a feature, not a limitation: no blob storage, no document table, no storage cost.

This assumption is legally untenable under French accounting law.

---

## The Argument

### 1. French Invoice Retention Law Is Not Optional

Article L123-22 of the Code de Commerce requires that commercial invoices (*factures*) be retained in their original form for **10 years**. The original must be stored in a way that guarantees its integrity — not just "accessible via a WhatsApp thread on someone's phone." A PDF that lives in a chat application, deletable by sender or recipient at any moment, is not compliant storage.

The penalty for non-compliance is not theoretical. The *Direction Générale des Finances Publiques* can reject invoice documentation during audit. An artisan whose invoices are stored in WhatsApp has no defense: "my client still has the PDF" is not an accounting archive.

### 2. WhatsApp Is Not an Accounting Archive

WhatsApp does not provide:
- **Integrity guarantees**: PDFs can be re-sent, modified, re-compressed. No hash verification.
- **Audit trail**: No record of when a document was sent, viewed, or altered.
- **Tamper-evident storage**: Deleting a message removes any evidence the invoice existed.
- **Access controls**: Anyone with access to the phone can forward, delete, or modify.
- **10-year retention**: WhatsApp conversations are routinely deleted, phones are replaced, accounts are abandoned.

D119's proposal that "the client has a copy in their WhatsApp thread" is presented as a feature — the client can always re-send it. This is the exact opposite of an accounting archive. The client having the only copy is the compliance failure.

### 3. The Phase 2 Migration Problem Is Already Visible

D72 (expert-comptable data-sync portal) is already in the roadmap. That portal requires stored documents — PDF URLs, document tables, blob references, creation timestamps, integrity hashes. expo-print's ephemeral architecture provides **none of this**. When Phase 2 begins, every line of expo-print integration must be replaced:

- No `documents` table → must be created from scratch
- No blob storage → must be provisioned (Supabase Storage already exists for auth)
- No PDF URL in API response → API contract must change
- No document references on `factures` records → migration required

This is not "deferred complexity." This is **duplicate work**. The Sprint 0 expo-print investment produces a PDF that Phase 2 will discard entirely.

### 4. The Resolution Is Honest Labeling, Not Architectural Denial

The argument is not "abandon expo-print." The argument is: **label the artifact correctly.**

Sprint 0 expo-print PDF = **prototype document**. WhatsApp-share only. No legal value. No archival guarantee. Explicitly communicated to the artisan: "this is a professional-looking draft, not your accounting record."

Sprint 1b = **production document**. Supabase blob storage + `documents` table + PDF URL in API response + integrity hash + `created_at` + `created_by`. Stored for 10 years. Audit-ready.

These two architectures are incompatible. Treating them as the same thing — by saying "storage is a v2 concern" — defers the legal exposure without eliminating it. The artisan using the app believes they have invoices. They don't. They have WhatsApp messages.

---

## Proposed Resolution

**D119 expo-print in-memory APPROVED for Sprint 0** — with the following explicit conditions:

1. **Label it as a prototype PDF**: The app must communicate (internally in code comments, in the TODO, in the Sprint 0 handoff doc) that the Sprint 0 PDF has no legal value and is not an accounting document.
2. **Document the Sprint 1b migration**: The TODO must include a Sprint 1b item: "Replace expo-print ephemeral PDFs with Supabase Storage blob + `documents` table + PDF URL in API response." This is not optional — it is the legal compliance gate.
3. **Add a storage gate to Sprint 0**: Before shipping Sprint 1, the expert-comptable data-sync portal (D72) requires a document table. The blob storage integration is a prerequisite for Phase 2, not a nice-to-have.

**The architectural decision**: Sprint 0 uses expo-print for speed. Sprint 1b adds proper document storage. These are sequential investments, not alternative paths. The cost of Sprint 1b migration must be acknowledged in the Sprint 0 estimate.

---

## Action Items for TODO.md

- [ ] **NEW — Sprint 1b gate:** Replace expo-print ephemeral PDFs with Supabase Storage blob + `documents` table + PDF URL in API response. This is the legal compliance prerequisite for Phase 2 (expert-comptable data-sync, D72). Not optional.
- [ ] **NEW — Legal labeling:** Sprint 0 PDF is a prototype document with no legal value. Add inline code comment and Sprint 0 handoff doc note: "WhatsApp share only — not an accounting record."
- [ ] **NEW — Sprint 1b estimate:** Budget 2-3 days for document storage migration (blob storage setup, `documents` table, PDF URL in API response, document reference on `factures` records). This is the Phase 2 prerequisite.
