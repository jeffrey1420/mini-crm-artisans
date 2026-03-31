# Position Paper: Debate Pulse 0228 — Technical Architect

## Challenge Statement

Debate 81/86 concluded that **AsyncStorage + retry queues** provide sufficient offline capability for Sprint 0, deferring expo-sqlite to v1.2. This assumption is **unsafe and must be revisited**. AsyncStorage + retry queues solves a different problem than the one French artisans actually face on job sites.

---

## Core Arguments

- **The retry queue has a fatal blind spot.** It only retries operations that successfully reached the queue. If a phone loses power, is force-closed by the OS, or crashes mid-write during a `setItem()` call, that operation never enters the queue. It is gone. The artisan loses the devis or facture data they just entered — with zero recovery path. This isn't a theoretical edge case; it is the most common phone failure mode for a device used outdoors, in vans, on job sites with dusty environments and variable battery conditions.

- **AsyncStorage is not a database — it's a key-value store with no atomicity guarantees.** Creating a reliable write-ahead log on top of AsyncStorage requires building transaction-like semantics from scratch: explicit fsync patterns, checksummed operation logs, crash-recovery replay logic. This is essentially building a worse version of SQLite. The "deferred complexity" argument collapses when you realize the complexity has to be built anyway, just with more bugs and worse performance.

- **The audience profile amplifies the risk.** French artisans (plumbers, electricians, roofers) using this app on job sites are not tech-savvy users who will notice a sync conflict and manually resolve it. They will assume the devis was saved, leave the job site, and discover data loss days later when the client calls asking about the quote. The trust damage is asymmetric: one data loss event can destroy the business relationship.

- **View-only offline is not a compromise — it's honest Scope 0.** Accepting that offline editing is v1.1+ and Sprint 0 is view-only is transparent, shippable, and still valuable: artisans can show clients their existing devis/factures even without connectivity. This is a genuine offline use case that doesn't require trusting AsyncStorage with critical write paths.

- **Deferring expo-sqlite to v1.2 means building the offline write path twice.** Every day spent building AsyncStorage-based retry queue infrastructure in Sprint 0 is wasted when expo-sqlite lands. The engineering team will either abandon that code (sunk cost) or patch it poorly into the SQLite layer (technical debt). The "+2 days" cost estimate for expo-sqlite in Sprint 0 is almost certainly less than the combined cost of building throwaway retry infrastructure plus the v1.2 migration.

---

## Implication for Sprint 0 Scope and Timeline

- **Remove offline editing from Sprint 0 scope.** Replace with: "View cached devis/factures when offline (read-only)."
- **Add expo-sqlite to Sprint 0 dependencies.** Budget the +2 days now rather than paying the larger cost later.
- **Accept a modest Sprint 0 timeline extension** (2 days) as the honest cost of shipping a system that won't lose data when a phone dies.

---

## Verdict

The decision log for Debate 81/86 should be **overturned**. The assumption that AsyncStorage + retry queues is "sufficient" for the primary offline use case is wrong because it doesn't account for the most common failure mode: mid-write power loss. The correct Sprint 0 decision is:

> **Sprint 0 ships view-only offline. Offline editing requires expo-sqlite and moves to v1.1.**

This is not scope creep — it's scope honesty.
