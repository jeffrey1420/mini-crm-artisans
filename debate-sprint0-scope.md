## Debate: Sprint 0 Scope — Offline-Capable Beats Offline-First

**Challenger:** Technical Architect (subagent)
**Target:** D81 — "Offline-first required at launch"
**Position:** Sprint 0 should be "offline-capable" not "offline-first" — optimistic UI + retry queues, no local DB until v1.2

---

### Core Argument

D81 resolved that offline-first (WatermelonDB/expo-sqlite + background sync) is required at launch. D84 confirmed Sprint 0 as 8-10 days. Both were decided in the same pulse. The combination is a 3-5 day overage on an already-tight sprint, driven by a stack assumption that was made AFTER the React Native pivot.

Here's the problem: D81's "offline-first = ~2 days mobile work" estimate was challenged but never stress-tested against what "offline-first" actually means in production. It means:
- **Conflict resolution UI** (~1 day): When Marc creates a devis offline, then his wife creates a different devis on the same client from her phone, who wins? Last-write-wins sounds simple until you have to show Marc what was overwritten and let him pick.
- **Sync testing** (~1 day): Offline sync bugs are the hardest class of mobile bug to reproduce and the easiest to ship. Solo developer + tight sprint + untested sync layer = production incidents.
- **Offline edge case handling** (~1 day): What happens when sync partially fails? When a devis is created offline, then the client is deleted online? These aren't theoretical — they're the 20% of cases that consume 80% of the debugging time.

That's 3-5 extra days on top of an already tight 8-10 day sprint. The "2 day" estimate for offline-first was optimistic. The real cost is 5-7 days.

---

### Technical Challenges to D81

**Challenge 1: D81 was decided post-stack-switch without reconsidering the complexity assumption.**

D9 ("no offline") was made for a web stack where offline required IndexedDB, service workers, and sync infrastructure. D81 flipped to "offline-first required" after switching to React Native via Expo — as if the stack change eliminated the complexity. It didn't. WatermelonDB + expo-sqlite + background sync is non-trivial even with the managed workflow. The "stack changed, so the complexity assumption changes" argument was asserted, not demonstrated.

**Challenge 2: The "2 days mobile work" estimate for offline-first is wrong by 2-3x.**

WatermelonDB integration alone — schema definition, sync adapter, and conflict resolution strategy — is 1-2 days for a solo developer who hasn't used it before. That's before writing a single line of the actual devis flow. The D81/D84 estimates never broke down the offline component into real work units.

**Challenge 3: True offline-first creates a conflict resolution problem that solo Marc will never encounter.**

Marc is solo. He has one phone. His "offline conflicts" are: creating a devis without signal, regaining signal, syncing. There is no multi-device conflict because there is no second device in the data model. The conflict resolution UI built for future multi-user scenarios is solving a problem Marc doesn't have in v1. Build it in v1.2 when the feature actually matters.

**Challenge 4: The "job site with no signal" failure mode is edge case, not default.**

Mobile data coverage in France is 98%+ population. Job sites have signal via mobile data. Basements and rural areas are edge cases — and building offline-first architecture to handle edge cases that affect <5% of usage sessions, at the cost of 3-5 extra sprint days, is exactly the over-engineering this product has been fighting against.

---

### Proposed Resolution

**Sprint 0 = Offline-Capable, not Offline-First:**

- **Optimistic UI:** All actions (create devis, add client) reflect immediately in the UI. The server request fires in background. No loading spinners blocking Marc's workflow.
- **Retry queues:** Failed requests (network loss, server error) queue locally and retry with exponential backoff. Marc's devis doesn't disappear when the elevator loses signal.
- **Cached data:** Last-known-good state of clients and recent devis stored in AsyncStorage. Marc can view his last 10 clients even without signal.
- **No local DB:** WatermelonDB/expo-sqlite deferred to v1.2. No sync layer in Sprint 0. No conflict resolution UI. No background sync service.
- **Net Sprint 0 savings:** 3-5 days. Those days go to the devis flow, not the sync infrastructure.

**Backend changes for offline-capable:** Add `updated_at` to all entities. Accept client-generated UUIDs. That's it. ~2 hours.

**v1.2 scope:** WatermelonDB/expo-sqlite, background sync, conflict resolution UI. After the product has real users, real usage patterns, and real conflict scenarios to design against.

---

### Verdict on D81

**D81 should be REVERSED.** The offline-first requirement was added to Sprint 0 scope without a realistic cost breakdown, after a stack switch that changed the implementation path but not the fundamental complexity of offline sync. For a solo artisan using a mobile app with 98%+ network coverage, "offline-capable" (optimistic UI + retry queues + cached data) covers 95% of the real failure modes at 20% of the engineering cost.

The devis flow ships in Sprint 0. Offline sync ships in v1.2 when there's actual data to sync and actual users generating actual conflict scenarios to design for.

---

*Technical Architect (subagent) — pulse-1827-architect*
*2026-03-30*
