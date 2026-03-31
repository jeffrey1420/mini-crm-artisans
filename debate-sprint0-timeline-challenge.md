# POSITION PAPER — Sprint 0 Timeline Challenge

**Author:** Technical Architect  
**Date:** 2026-03-31T04:17  
**Status:** OPEN — Requires Louis Decision  
**Challenge:** The 5-day Sprint 0 timeline confirmed at 04:05 may be underestimating the documents table + draft-mode implementation. Gate status is also unconfirmed.

---

## 1. The Core Challenge

At 04:05, the pulse resolved:
- "Sprint 0 timeline confirmed at 5 days"
- "Days 1-2: offline architecture + devis flow"
- "expo-sqlite + documents table (UUID, type, status, JSON blob, timestamps)"
- "Draft semantics: saves → pending_draft, explicit confirm → confirmed"
- Claimed implementation time: "half-day to 1-day"

**The problem:** The documents table schema is a new schema entity added to Sprint 0 scope at the 04:05 pulse. It was discussed across multiple prior debates (D140, TA-D153) but was never formally committed as a Sprint 0 deliverable before this pulse. The "half-day to 1-day" estimate for this new entity requires scrutiny.

---

## 2. Breaking Down the Actual Offline Tasks

The "offline architecture + devis flow" for Days 1-2 is not one task — it is a stack of interdependent tasks. Here's the honest breakdown:

### Task 2.1: expo-sqlite Integration + Database Initialization
- Install and configure expo-sqlite (or expo-sqlite/expo-file-system based on Expo SDK version)
- Initialize database with schema version table
- Write migration runner (even minimal ones need a run-once pattern)
- **Estimated: 0.5 days**

### Task 2.2: Documents Table Schema Definition + Creation
- Define TypeScript types: DocumentType, DocumentStatus ('pending_draft' | 'confirmed')
- Create SQLite table: `documents (id TEXT PK, type TEXT, status TEXT, content TEXT, created_at INTEGER, updated_at INTEGER, synced_at INTEGER)`
- Write table creation SQL as part of migration
- **Estimated: 0.25 days**

### Task 2.3: CRUD Helper Functions
- `createDocument(type, content)` → inserts pending_draft
- `updateDocument(id, content)` → updates pending_draft (NOT confirmed)
- `promoteToConfirmed(id)` → status change pending_draft → confirmed, sets synced_at
- `listPendingDrafts()` → queries status = 'pending_draft'
- `getDocument(id)` → single document fetch
- **Estimated: 0.5 days** (including tests)

### Task 2.4: Draft Semantics Logic
- Draft saves (auto-save on field blur, periodic save) → always writes to pending_draft
- Only explicit "Confirm" action promotes to confirmed
- "Discard" action deletes pending_draft
- Sync trigger: confirmed documents are pushed to Supabase on next connectivity
- Conflict logic: confirmed wins (server-wins is safe for confirmed-only sync)
- **Estimated: 0.5 days**

### Task 2.5: Pending Drafts UI Screen
- List view: all documents with status = 'pending_draft'
- Show: type, truncated content, created_at, updated_at
- Actions per draft: Resume (edit), Confirm, Discard
- Empty state: "Aucun brouillon en attente"
- **Estimated: 0.5 days**

### Task 2.6: Confirm/Discard Action Flows
- Confirm: calls promoteToConfirmed() + triggers Supabase sync
- Discard: confirmation dialog ("Supprimer ce brouillon ?") + calls delete
- Optimistic UI update (update local state before async operation completes)
- Error handling: sync failure toast, retry option
- **Estimated: 0.25 days**

### Task 2.7: Devis Flow Integration (The Full Picture)
- The devis form must save to SQLite as pending_draft on every meaningful edit
- The "Envoyer" action in devis flow must promote draft to confirmed + trigger sync
- Draft indicator in devis form (shows "Brouillon" badge for pending_draft items)
- **Estimated: 0.5 days** (this is integration work, not isolated)

---

## 3. Total Estimate

| Task | Estimate |
|------|----------|
| expo-sqlite setup + migration | 0.5 days |
| Documents table schema | 0.25 days |
| CRUD helpers | 0.5 days |
| Draft semantics logic | 0.5 days |
| Pending Drafts UI | 0.5 days |
| Confirm/Discard flows | 0.25 days |
| Devis integration | 0.5 days |
| **Subtotal** | **3.0 days** |

**Parallel work assumption:** If Louis works on mentions légales and Supabase setup simultaneously (Days 4-5), that is legitimate parallelization. But the offline work (Days 1-2) has no parallel track — it is the sequential critical path.

**The gap:** 3.0 days vs. "half-day to 1-day" = **2.0 to 2.5 days of underestimation**.

The original +2.5 days estimate from TA-D153 was not for the full offline architecture — it was for a more complete database schema (multi-table, proper migrations, conflict resolution). The documents table is a simplification. But the simplification reduces complexity from a multi-table schema to a single-table schema, not from 2.5 days to 0.5 days.

**Conservative bottom line:** At minimum, 1.5 to 2.0 days for offline alone. Not 0.5 to 1.0 days.

---

## 4. The Gate Status Problem

The 04:05 pulse lists Sprint 0 blockers:

| Gate Item | Status |
|-----------|--------|
| Mentions légales (D142) — Louis commits real strings to git | **OPEN — Louis has not done this** |
| Supabase EU project — confirm project created | **OPEN — Louis has not done this** |

**The problem:** If Sprint 0 starts without these gates committed:
1. The developer cannot write legal-safe templates until mentions légales content exists
2. The developer cannot configure Supabase sync until the project exists
3. If these gates take 0.5 to 1.0 days each to complete (realistic for first-time setup), they add directly to Sprint 0 duration

**The 04:05 pulse states:** "Days 4-5: mentions légales + Supabase project setup (parallel, independent)"

This implies these are parallel tasks to the main development work. But if Louis hasn't done them before Sprint 0 starts, they become sequential — or worse, blockers that pause development while waiting for his input.

**If both gates take 0.5 days each = +1 day to Sprint 0.**

---

## 5. Revised Sprint 0 Timeline

| Days | Original 04:05 | Revised (This Challenge) |
|------|----------------|---------------------------|
| 1-2 | Offline + devis flow | Offline + devis flow (realistic: 1.5-2 days) |
| 3 | Supabase sync | Supabase sync + remaining offline integration |
| 4-5 | Mentions légales + Supabase setup (parallel) | Mentions légales + Supabase setup (if gates done before start) OR Gates blocking + development stalled |
| **Total** | **5 days** | **5.5 to 6.5 days** |

**If gate items are not pre-committed before Sprint 0 begins:** Sprint 0 is effectively 6.5 to 7.0 days.

---

## 6. What This Paper Is NOT Arguing

This is not an argument against draft-mode semantics. TA-D153 established that draft-mode is the correct architecture. The documents table is the right schema. The offline story is correct.

This is a challenge to the **timeline estimate**, specifically:
1. "Half-day to 1-day" for the documents table + draft semantics is too aggressive
2. The gate items (mentions légales, Supabase project) remain uncommitted and will extend Sprint 0 if not pre-completed
3. The 5-day estimate treats parallel tracks as if they are free — but Louis's gate items are not parallel-ready until he completes them

---

## 7. Proposed Resolution

**Request Louis confirm or provide:**
1. **Mentions légales:** Can Louis commit real business data to `legal/mentions-legales.ts` before Sprint 0 begins? If yes, timeline stands. If no, Sprint 0 is 6 days.
2. **Supabase project:** Has Louis created the Supabase project in EU (Frankfurt)? If yes, offline sync work can proceed. If no, Days 3-5 sync track is blocked.
3. **Buffer acknowledgment:** If offline implementation is 1.5 to 2.0 days (not 0.5 to 1.0), add 0.5 to 1.0 day buffer to Sprint 0, making it 5.5 to 6.0 days total.

**Status:** OPEN — Louis decision required. This is a sanity check, not a scope cut request. The scope is correct. The timeline estimate may not be.

---

*Technical Architect — mini-crm-research pulse*  
*2026-03-31T04:17*
