# DEBATE: D140 — Offline Scope: Draft-Mode Is the Only Honest Sprint 0 Answer
**Position: TA — expo-sqlite + draft-mode semantics is already resolved**
**Author: Technical Architect (Pulse)**
**Date: 2026-03-31**

---

## The Ask

Draft-mode semantics for Sprint 0 offline editing is not a new proposal — it was resolved at D150/D151 in the 02:59 pulse. The debate-log shows:
- D140 (01:15): server-wins rejected as "silent document annihilation"
- D150 (02:15): draft-mode explicitly adopted as Sprint 0 offline architecture
- D151 (02:59): expo-sqlite + draft_status + Pending Drafts UI confirmed

PS-D147 (03:20) reopened the AsyncStorage vs expo-sqlite question, arguing AsyncStorage + retry queues is "sufficient for Sprint 0" and expo-sqlite adds "2 days." This is wrong — and the "2 days" framing hides the real cost.

---

## The Core Technical Argument

### 1. AsyncStorage Is Not a Database

AsyncStorage is key-value storage. It:
- Corrupts on unexpected process termination (phone battery dies mid-write)
- Has no query capabilities — cannot do `SELECT * FROM jobs WHERE client_id = X`
- Cannot model a job with line items, photos, and relationships
- Has a 6MB default limit on React Native

For an app where a job entry with photos and line items is the primary data capture mechanism — this is building on sand.

### 2. Retry Queues Only Retry What Entered the Queue

Phone battery dies mid-write → operation never entered the retry queue → data gone. This is not an edge case. For an artisan working on a job site, battery death is a Tuesday occurrence.

The retry queue is built on top of AsyncStorage. If AsyncStorage loses data on phone death, the retry queue loses the data too. This is not resilient architecture with extra steps — it is fragile architecture with extra complexity.

### 3. A Devis Is a Legally-Standing Document

Under Code civil Article 1127-1, a devis establishes contractual obligations. It has:
- A séquentiel number (D32: sequential numbering enforcement)
- TVA per line item (5.5%/10%/20%)
- Legal standing once sent to a client

When Marc's phone comes online 3 days after editing a devis offline, and the server-wins strategy silently overwrites his changes with his wife's web dashboard edits — that is not a sync conflict. That is document destruction. The artisan has no record of what was lost. The client may have already received a different version. The legal coherence of the document is compromised.

Server-wins on a business document is not a fallback strategy. It is arbitrary data destruction.

### 4. Draft-Mode: The Architecturally Honest Answer

When the app goes offline, record a frozen timestamp. While offline, edits are saved as **draft edits** — not overwrites to the live document. When connectivity returns, the artisan manually reviews and confirms. This:

- Eliminates silent data destruction
- Preserves document coherence
- Respects the legal standing of business documents
- Matches the artisan mental model: "I'm drafting this. When I'm done and back in signal, I'll send it."

Implementation:
- `draft_status` enum: `pending_draft | confirmed | rejected`
- Pending drafts list view in the app
- "Confirm draft" action that replaces the live document
- Phone death = draft persisted in SQLite, recoverable on reopen

### 5. The "2 Days" Framing Hides the Real Cost

PS-D147 argues expo-sqlite adds "2 days" to Sprint 0. But the retry queue on AsyncStorage also has a hidden cost — one that surfaces in production, not during Sprint 0:

- Retry queue error handling (partial sync failures, dead queue detection)
- Manual override UI when queue fails
- Debugging silent data loss at 2am when an artisan calls about lost data
- Rebuilding trust after a data loss incident

The 2-day estimate for expo-sqlite is a one-time cost. The retry queue's hidden cost is a recurring production maintenance burden that compounds.

---

## The Anti-Argument: "View-Only Is Good Enough"

Some proposals suggest: ship view-only offline, remove offline editing from Sprint 0 entirely.

This fails the primary value proposition. The product is for artisans on job sites. The value is: capture job data in real-time, offline. View-only means: "you can see old data, but you can't enter new data offline." That is not the product being described. It is a step backwards from WhatsApp + notebook.

---

## Sprint 0 Offline Scope (Final)

**Adopted:**
- expo-sqlite as local persistence (not AsyncStorage)
- `draft_status` enum on all mutable entities
- Pending Drafts list view
- Confirm/Discard draft actions
- Server-wins for confirmed drafts (no multi-device conflict in v1 — Marc is solo)
- Background sync worker triggers on connectivity restore

**What is NOT in Sprint 0 offline:**
- Field-level conflict detection UI
- Bidirectional sync with CRDT/OT
- Multi-device merge logic

These are v1.2.

---

## Summary

| | AsyncStorage + Retry Queue | expo-sqlite + Draft-Mode |
|---|---|---|
| Phone death mid-write | Data lost, queue empty | Draft persisted in SQLite |
| Server-wins on conflict | Silent document destruction | Draft reviewed before overwrite |
| Data model | Key-value, no queries | Relational, proper schema |
| Production debugging | Hidden failures, silent loss | Visible draft status |
| Sprint 0 cost | "Fast" now, painful later | +2 days now, clean later |

Draft-mode is the only architecturally honest answer for a product where business documents have legal standing. This was already resolved at D150/D151. PS-D147's reopening does not introduce new evidence — it reintroduces the AsyncStorage argument that was already rejected.

---

**Recommendation: D140 is RESOLVED. Sprint 0 offline = expo-sqlite + draft-mode. No further debate needed.**
