# D81/C — Technical Architect Verdict: Offline Architecture for Sprint 0

**Date:** 2026-03-30T23:48  
**Debate:** D81/C — Offline Architecture (REOPENED at 23:21)  
**Role:** Technical Architect  

---

## Assumption Challenged

**"AsyncStorage + retry queue is sufficient for v1 offline capability."**

This assumption is wrong, and the cost of being wrong is not evenly distributed.

The debate has treated offline-capable (optimistic UI + retry queue) as a pragmatic middle ground — good enough for v1, with full offline-first (SQLite) coming in v1.2. The reasoning: AsyncStorage avoids the 1-2 day cost of WatermelonDB/expo-sqlite integration. This framing is backwards.

**AsyncStorage does not give you offline capability. It gives you offline theatre.**

AsyncStorage is key-value storage. It corrupts on phone death. It has no query capabilities. It cannot model a job with line items, photos, and relations. The retry queue sits on top of AsyncStorage — so when AsyncStorage loses data, the queue loses the data too. This is not a resilient architecture. It is a fragile one with extra steps.

The retry queue is also not a sync strategy. It is a best-effort recovery mechanism that fails on OS process kills, app backgrounding, and phone reboots mid-write. For an artisan logging 4 hours of labour on a rural job site, the scenario is not theoretical: phone dies, retry queue is empty, data is gone. That is a product-killing failure for someone whose livelihood depends on accurate billing records.

**The "1-2 day cost" framing is the most dangerous settled assumption in this debate.** The argument is that SQLite adds 1-2 days, implying the alternative is cheaper. But the alternative ships debugging time instead of building time. The retry queue needs its own error handling, partial-sync recovery, dead-queue detection, and manual override UI. That is not 0 days — it is hidden days spread across every subsequent sprint as edge cases surface in production.

---

## Verdict

**Sprint 0 offline architecture: expo-sqlite as the local persistence foundation.**

- **Storage:** expo-sqlite (preferred over WatermelonDB for Sprint 0 — simpler API, smaller bundle, sufficient for the schema)
- **Sync strategy:** Background sync worker triggers on connectivity restore. Not a retry queue — a sync worker that reads `sync_status` flags from local tables.
- **Conflict resolution:** Server-wins in v1. The `sync_status` field (pending/synced/conflict) is the minimum conflict detection layer. No custom conflict UI in Sprint 0.
- **What this replaces:** AsyncStorage + retry queue entirely. No queue. No optimistic "assume it synced" behaviour. Local writes → sync worker → server.

**Sprint 0 timeline impact:** Add 1 day for expo-sqlite integration (schema setup, sync worker, sync_status fields). This is a known, bounded cost — not the unbounded debugging cost of a fragile retry queue.

**What this does NOT add:** Conflict resolution UI. That is v1.2. Server-wins is acceptable for solo artisans with single-device usage.

---

## What Gets Cut If Sprint 0 Needs Buffer

If timeline requires cutting: cut **features before foundation**. Do not cut SQLite to make room for mentions légales. The persistence layer is load-bearing for every feature that follows — job logging, photos, multi-line items. Cutting it creates a cracked foundation that every Sprint 1 feature will fall through.

Cut order: mentions légales (plain text placeholder) → WhatsApp PDF styling → client type field. Never cut the local database.

---

## D81/C Resolution

| Item | Decision |
|------|----------|
| Local persistence | expo-sqlite in Sprint 0 |
| Sync mechanism | Background sync worker (not retry queue) |
| Conflict detection | `sync_status` enum: pending/synced/conflict |
| Conflict resolution | Server-wins (v1) |
| Conflict UI | Deferred to v1.2 |
| Sprint 0 impact | +1 day |
| AsyncStorage | Removed from offline architecture |

**D81/C: RESOLVED.** Local SQLite replaces AsyncStorage + retry queue in Sprint 0.
