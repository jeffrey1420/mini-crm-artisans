# B Technical Architect — Pulse 0129

## Challenge: Server-Wins Is a Data Annihilation Bug, Not a Conflict Strategy

D140 and D144 proposed server-wins as the "safe fallback" for offline sync conflicts. This assumption is **structurally broken** for the artisan use case. It doesn't just lose data — it actively teaches the artisan that their offline work doesn't matter.

---

## The Scenario That Will Actually Happen

**Monday 8:47 AM** — Artisan is at a job site with no signal. They add a new client "Durand" with phone 06 12 34 56 78 and a note about a leak in the bathroom. They create a devis for €340.

**Monday 10:23 AM** — Back at the van, signal returns. The phone syncs. Server-wins means: if Durand somehow got modified on the server (or the sync logic has a timestamp edge case), the artisan's local version is silently overwritten.

**Monday 2:15 PM** — Artisan opens the web dashboard (which will exist — you can't sell "dashboard access" without building it). They see Durand. But the phone number is wrong. The note is missing. The €340 devis is gone.

**They don't know why. There's no conflict UI. There was no error message. The server just... won.**

This is not a rare edge case. This is the default behavior of a solo artisan working across job sites, home, and van.

---

## Why "Last-Write-Wins" Is Also Broken (Just Slower)

Last-write-wins (LWW) sounds more reasonable than server-wins. The most recent write survives. But consider:

1. Artisan edits client on phone at 8:47 AM offline
2. Office assistant (later, same day, from desktop) edits same client at 2:00 PM
3. Phone syncs at 2:30 PM when artisan returns home
4. The assistant's work from 2:00 PM is silently overwritten

Or worse: artisan edits on phone, then opens the web dashboard (Day 30, post-launch) and sees **different data than what they just entered**. That's not a sync bug — that's a broken mental model. The artisan will conclude the app "loses data" and churn.

---

## What You Actually Need

If you implement offline-first with any sync strategy, you need:

1. **Conflict detection at the field level**, not the record level — two edits to different fields should merge, not fight
2. **Conflict UI** — when real conflicts occur, show both versions and let the human decide
3. **Audit trail** — every record has a `local_modified_at` and `server_modified_at`; conflicts are logged, not silently resolved

This is not free. Conflict UI alone is a full sprint of work. The conflict detection logic requires versioning on every entity (clients, devis, factures, relances). That's a schema migration on Supabase **and** a version vector in the local SQLite store.

---

## The Real Decision

Either:

- **Spend the real cost** (conflict UI + field-level merge + audit trail) and do offline sync properly
- **Label offline mode "view only"** — you can browse cached devis/factures, but editing requires connectivity. This is honest. This is buildable in Sprint 0 with AsyncStorage and a clear scope.

"Server-wins as fallback" is not a middle ground. It's the worst of both worlds: you pay the offline complexity cost, and your artisan still loses data.

---

## Summary Table

| ID | Topic | Your Position |
|----|-------|---------------|
| D140 | AsyncStorage vs expo-sqlite | +2 days estimate understates true cost (conflict UI alone is a sprint) |
| D144 | Offline mode scope | View-only offline is honest; server-wins is a silent data killer |
| D9/D81/D86 | Offline-first requirement | Offline editing requires conflict resolution UX — not just storage |

**File path:** `/data/workspace/mini-crm-research/debate-ta-pulse-0129.md`
