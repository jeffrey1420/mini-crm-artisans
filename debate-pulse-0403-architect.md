# DEBATE D140 — Sprint 0 Offline Architecture
## Technical Architect Position (TA-D153)

**Date:** 2026-03-31  
**Status:** CONTESTED — needs resolution before Sprint 0 gates close  
**File:** `mini-crm-research/debate-pulse-0403-architect.md`

---

## 1. Challenging PS-D147: The AsyncStorage Retry-Queue Has a Fundamental Atomicity Gap

PS-D147 argues that AsyncStorage + retry queues are sufficient for Sprint 0. This position contains a critical assumption that does not hold under the primary failure mode of field workers: **phone death mid-write**.

### The Failure Mode PS-D147 Does Not Account For

```
User fills in devis → taps "Enregistrer" → 
Phone dies (battery, drop, crash) BEFORE the write completes →
Operation never entered the retry queue →
Data is GONE.
```

The retry queue is a **recovery mechanism for operations that successfully entered the queue**. It is not a write-ahead log. If the write hasn't hit AsyncStorage yet, the retry queue has nothing to retry. This is not a theoretical edge case — it is the **dominant failure scenario** for artisans in the field:

- Working on-site, battery not fully charged
- Cold weather degrades battery performance
- Phone dropped while rushing between jobs
- App crash under memory pressure (large devis with multiple line items + photos)

### What AsyncStorage Actually Guarantees

AsyncStorage is a simple key-value store. There is no transaction semantics. There is no atomic commit guarantee across multiple keys. Writing a devis with 10 line items = 10+ separate AsyncStorage writes. If the process dies after write 7, you have a partial, inconsistent state — and no way to know which writes completed and which didn't.

### The AsyncStorage Mental Model Is Wrong

PS-D147 appears to be treating AsyncStorage as a "safe enough" local store with a retry layer on top. This conflates two different problems:

| Problem | What PS-D147 Solves | What Remains Unsolved |
|---|---|---|
| Network failure mid-sync | Retry queue handles this | ✅ Covered |
| Phone death mid-write | Retry queue does NOT help | ❌ Data loss |
| Partial write corruption | Not addressed | ❌ Inconsistent state |

**For a devis/factures tool where each document is legally significant and financially binding, partial-write corruption is not acceptable.** A half-written facture is worse than no facture — the artisan may believe it was saved when it wasn't.

---

## 2. Challenging the "+2 Days" Estimate for expo-sqlite

PS-D147 estimates expo-sqlite adds 2+ days to Sprint 0. I contest this estimate on two grounds:

### A. The +2 Days Assumes a Full SQLite Implementation — But We Don't Need That

The TA-D153 proposal is **not** "implement full SQLite with complex migrations." The proposal is:

1. Use expo-sqlite (pre-integrated, well-documented)
2. Store each devis/facture as a single JSON blob in one table with status field
3. Add a `pending_draft` / `confirmed` status column
4. Never update the live document row — INSERT a new confirmed row instead

This is not a database architecture project. It's adding one table, one enum column, and changing the write path. expo-sqlite has clear docs, and the CRUD surface area is small.

### B. The Real Cost Is Debugging AsyncStorage in Production

Here's what the Sprint 0 timeline actually looks like with AsyncStorage:

```
Day 1-2: Implement AsyncStorage retry queue (looks fast, feels done)
Day 3-4: Edge cases emerge — partial writes, queue ordering, concurrent edits
Day 5:   Sprint review with a system that works in the happy path
Post-mortem: Field reports of lost devis → emergency patch sprint
```

vs. expo-sqlite:

```
Day 1:   expo-sqlite setup + write path refactor
Day 2:   Draft semantics wired up (pending_draft → confirmed flow)
Day 3:   Sync layer integration
Day 4:   Edge cases handled (SQLite transactions handle atomicity for free)
Day 5:   Sprint review with a system where phone death = recoverable draft
```

The +2 days estimate treats implementation speed as the only variable. It ignores **debugging time in weeks 2-4 when field workers start reporting data loss**.

### The True Cost Calculation

| Scenario | Day 1-5 Cost | Week 2-4 Cost | Total Sprint 0-1 Cost |
|---|---|---|---|
| AsyncStorage + retry | Low (appears) | High (production bugs) | Higher |
| expo-sqlite | Medium (known) | Low (robust by design) | Lower |

The +2 days for expo-sqlite is front-loaded and visible. The AsyncStorage debugging cost is back-loaded and hidden — which is precisely why it looks cheaper on day 1.

---

## 3. Resolution Proposal

Given the Sprint 0 timeline pressure (5 days, 2/6 gate criteria unmet), I propose a **tiered approach** that does not require choosing between speed and safety:

### Resolution: expo-sqlite with Minimal Schema (Not Full Architecture)

**What we implement in Sprint 0:**

```
Table: documents
- id: TEXT PRIMARY KEY (UUID)
- type: TEXT ('devis' | 'facture')
- status: TEXT ('pending_draft' | 'confirmed')
- content: TEXT (JSON blob — full document snapshot)
- created_at: INTEGER (Unix timestamp)
- updated_at: INTEGER (Unix timestamp)
- synced_at: INTEGER (Unix timestamp, nullable)
```

**The draft semantics rule:**  
A "save" always creates or updates a `pending_draft` record. The artisan explicitly promotes a draft to `confirmed`. The confirmed record is what syncs to Supabase. The draft is never deleted until the artisan explicitly confirms AND sync succeeds.

**What this gives us:**
- Phone dies mid-write → SQLite transaction ensures atomic write → draft is recoverable ✅
- No partial writes (JSON blob = one value) ✅
- Clear semantic distinction between draft and live document ✅
- Minimal schema, no complex migrations ✅
- expo-sqlite has had stable releases and is actively maintained ✅

**What we explicitly defer to Sprint 1:**
- Conflict resolution (two devices editing same document)
- Background sync with service workers
- Multi-table schema normalization

### Timeline-Adjusted Sprint 0 Scope

| Task | Original | Adjusted |
|---|---|---|
| expo-sqlite integration | Day 1 | Day 1 (half-day) |
| `documents` table schema | Day 1 | Day 1 (half-day) |
| Draft save flow (UI → SQLite) | Day 2 | Day 2 |
| Confirm/promote flow | Day 2 | Day 2 |
| Supabase sync for confirmed docs | Day 3 | Day 3 |
| Mentions légales | — | Day 4 (parallel) |
| Supabase project setup | — | Day 4 (parallel) |
| Buffer / edge cases | Day 5 | Day 5 |

**The mentions légales and Supabase gate criteria are independent of the offline architecture decision.** They can proceed in parallel on Day 4. The offline architecture task (expo-sqlite + documents table) is a half-day to one-day task — not two days.

---

## 4. Conclusion

PS-D147's position is based on a false economy: it optimizes for perceived day-1 speed while accepting a data-loss failure mode that is precisely the most common experienced by the target users (field artisans). The retry queue does not solve phone-death mid-write because the operation must first reach the queue to be retried.

The "+2 days" estimate for expo-sqlite conflates a full database architecture with a minimal single-table document store. A minimal expo-sqlite implementation with draft semantics is a 1-day task, not 2 days.

**Recommendation:** Adopt TA-D153 with the tiered scope above. Split the sprint: offline architecture on Days 1-2, Supabase + mentions légales on Days 4-5 (parallel tracks). This meets all six gate criteria within Sprint 0 while ensuring data safety is architected in, not bolted on.

---

**Filed by:** Technical Architect (TA-D153)  
**For:** Sprint 0 decision on D140  
**Urgency:** Blocker — gate criteria cannot be met until this is resolved
