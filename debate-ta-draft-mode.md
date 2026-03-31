# Position Paper: Draft-Mode Semantics for Sprint 0 Offline Architecture

**Author:** Technical Architect (TA-Pulse-DraftMode)  
**Date:** 2026-03-31  
**Target:** D140 Offline Scope Decision — Draft-Mode Semantics  

---

## Position Title

**DRAFT-MODE OFFLINE: The Only Architecturally Honest Sprint 0 Choice**

---

## Assumption Challenged

**Challenged assumption from D86/D140:** "Offline-capable" means the artisan's edits are eventually applied to the live document, with server-wins as the fallback conflict resolution.

This assumption treats offline editing as equivalent to online editing, just delayed. It is not. Offline editing on an unstable connectivity device is a fundamentally different operation — and treating it as "same thing, just async" is how you build a system that silently destroys legally-standing documents.

**Also challenged from TA-Pulse-0129:** The framing of "view-only offline" vs "full offline with conflict UI" as the only options. This false dichotomy ignores a third path: draft-mode semantics, which is achievable in Sprint 0 and eliminates silent data destruction without requiring conflict UI.

---

## Core Argument

### 1. A devis is a legally-standing document. It is not a CRM field.

French devis have legal weight. They establish a commercial relationship, a pricing commitment, and a right-to-work basis. When an artisan creates or edits a devis offline — on a job site, in a basement, in a dead zone — that document is being drafted under conditions where connectivity failure is the *expected state*, not an exception.

Server-wins as conflict resolution means: if the artisan's phone dies mid-edit, their legally-standing document is silently overwritten by whatever the server had. This is not a sync bug. This is document annihilation.

### 2. Draft-mode semantics eliminate the conflict problem by removing the conflict.

The draft model:
- **Offline edits are drafts.** They are stored locally, visible to the artisan, marked clearly as "pending sync."
- **Drafts do NOT overwrite the live document.** The live document (on server) is untouched until the artisan explicitly confirms the draft.
- **When connectivity returns,** the artisan reviews pending drafts and confirms. At that moment, the draft becomes the live document.
- **If the phone dies mid-draft:** The draft is persisted locally (SQLite). The artisan loses nothing. When they reopen the app, the draft is there.

Under draft-mode, there is no server-wins vs client-wins conflict because the draft has not yet been promoted to the live layer. The artisan always reviews before publishing.

### 3. Draft-mode matches how artisans actually work.

The mental model of an artisan working across job sites is: "I'm drafting this devis. When I'm done and back in signal, I'll send it." This is *already* a draft workflow. Draft-mode semantics just make the app match the mental model instead of fighting it.

Under server-wins: the artisan assumes their devis is saved locally, but the app silently overwrites the server copy. On reconnect, the artisan's "final" devis is gone.

Under draft-mode: the artisan sees "Draft — pending review" until they explicitly confirm. The flow matches their intent.

### 4. Draft-mode requires no conflict UI in Sprint 0.

Conflict UI (showing two versions, letting the human pick) is +3-5 days of work. It requires field-level versioning, a comparison UI, and decision logic.

Draft-mode requires: a `draft_status` enum on the local record, a "pending drafts" view, and a "confirm draft" action that pushes to the server. This is a straightforward CRUD extension to the existing sync layer.

Sprint 0 cost: +0.5 days. Not +3-5.

### 5. Draft-mode is the correct layer for future conflict resolution.

If v1.2 implements field-level conflict detection, it does so on the *confirmed draft* vs *server document* — not on ephemeral in-memory edits. The draft becomes the unit of conflict resolution. This is architecturally cleaner: conflicts surface at the "publish" step, not at the "sync" step.

---

## Why Server-Wins Fails for a Legally-Standing Devis

A devis is not a "client note" or a "phone number." It is a binding commercial offer. Under French law (Code civil Art. 1127-1 et seq.), a devis constitutes an offer that, once accepted, creates contractual obligations.

When server-wins silently overwrites an artisan's offline devis edit:

1. **The artisan has no record of what was lost.** The server-wins event is silent — no notification, no conflict UI, no audit trail.
2. **The client may have already received the devis.** If the artisan sent the devis (offline, cached as sent), and the server-wins event reverted the server copy, the artisan and client now have different documents.
3. **The legal standing is compromised.** If a dispute arises about what was included in the devis — pricing, scope, materials — the server record (silently-won) is the only record. The artisan's version (silently-lost) had no backup.
4. **No remediation path exists.** The artisan cannot "undo" a server-wins event because they never knew it happened. The server document was overwritten without their knowledge or consent.

Server-wins is an acceptable conflict resolution for low-stakes data (preferences, display settings, non-committed drafts). It is catastrophic for legally-standing documents.

---

## Proposed Resolution: Draft-Mode Semantics for Sprint 0

**Architecture:**
- Local SQLite (expo-sqlite, as refined by D144) stores all records with a `draft_status` field: `confirmed` | `pending_draft`
- When online: edits write directly to `confirmed` state and sync immediately
- When offline: edits write to `pending_draft` state — NOT to `confirmed`
- When connectivity returns: artisan opens "Pending Drafts" view, reviews each draft, taps "Confirm & Send" to promote to `confirmed` and trigger sync
- Drafts that are never confirmed remain local-only until explicitly deleted by the artisan

**Sync behavior:**
- Confirmed records sync to server as they are (no conflict, as no divergence occurred)
- Pending drafts are never pushed to server automatically — only on explicit artisan confirmation
- Server never sends a pending_draft back to the client

**UI additions for Sprint 0 (+0.5 days):**
- Draft indicator badge on records with `pending_draft` status
- "Pending Drafts" list view (separate from confirmed records)
- "Confirm Draft" action button per draft
- "Discard Draft" action (with confirmation dialog)
- Offline indicator in header (cosmetic — no functional change to draft semantics)

**What is NOT in Sprint 0:**
- Server-side draft storage (drafts live only on device until confirmed)
- Cross-device draft sync (a limitation: drafts are device-local — acceptable for Sprint 0 solo use)
- Field-level conflict detection (deferred to v1.2, operates on confirmed documents not drafts)

---

## Sprint 0 Timeline Impact

| Item | Original Estimate | Draft-Mode Addition |
|------|------------------|---------------------|
| expo-sqlite integration | +2 days (D144 refined) | Included |
| Draft status enum + CRUD | — | +0.25 days |
| Pending Drafts UI view | — | +0.15 days |
| Confirm/Discard actions | — | +0.1 days |
| **Total Sprint 0 delta** | **+2 days** | **+2.5 days** |

**Specific implementation notes:**
- `draft_status` column: `TEXT DEFAULT 'confirmed'` — existing records auto-migrate to `confirmed`
- Pending drafts never leave the device — no server API changes required for draft storage
- The "pending drafts" sync behavior is: confirmed records go to server, drafts do not
- On app reinstall: drafts are lost (server has no copy) — this is a known limitation documented in the user-facing FAQ

---

## Summary

Server-wins is not a safe fallback for legally-standing devis documents. It is silent document annihilation. View-only offline eliminates the problem by removing offline editing — but it also removes the primary value proposition for a field artisan.

Draft-mode semantics are the architecturally correct solution for Sprint 0:
- No silent data destruction (drafts never overwrite live documents without artisan confirmation)
- No conflict UI required (the publish step is the confirmation step)
- Matches artisan mental model (draft → review → send)
- Achievable in +0.5 days above the already-necessary expo-sqlite integration

**Recommendation:** Accept draft-mode semantics as the Sprint 0 offline architecture. This resolves D140 decisively: not (A) view-only, not (C) defer to v1.2, but the middle path that is both honest and buildable.
