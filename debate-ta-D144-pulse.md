# Pulse 2026-03-31T01:15 — Technical Architect (D144)

---

## Debate 143: D110 Path B — The Conversion Trigger Has No Conversion Moment

### Challenge: D110's Path B triggers create a conversion prompt without a conversion context

**Assumption challenged from D110:** That usage-based milestones (45 days active OR 7+ jobs logged OR 5+ clients managed) function as conversion triggers equivalent to Path A's "limit-hit" moment. They do not. Path A converts because the artisan *feels* the limit. Path B converts because an arbitrary counter reaches a number. These are not equivalent UX events.

---

### The Core Problem: Frictionless Accumulation Has No Friction

Path A's conversion moment is architecturally clean:

1. Artisan is creating devis, hitting the Free tier limit (3 clients, 10 documents, etc.)
2. The app shows: "Limite atteinte — upgrade to continue"
3. Artisan feels the pain directly: a blocked workflow
4. Upgrade prompt appears at peak frustration (when they need to send one more devis)
5. The €29/month upgrade removes the specific blocker they just hit

This is a *friction-born conversion*. The limit creates the friction. The upgrade removes it. The timing is self-evident.

Path B's conversion triggers are structurally different:

**45 days active** — The artisan used the app for 45 days. During those 45 days, nothing blocked them. They logged jobs at their own pace. At day 46, a notification fires: "You've been using the app for 45 days — upgrade?" The implicit message is: "Thanks for being a customer. Pay up now." There is no blocked workflow. No friction was felt. The conversion ask arrives uninvited and context-free.

**7+ jobs logged** — Same problem, amplified. The artisan hit "job 7" without incident. Each job was logged successfully. The upgrade prompt fires at job 7 and says: "You've logged 7 jobs — time to pay." Why? What blocked them? What pain does €29/month remove at this exact moment? The answer is: nothing. The Free tier didn't stop them. The conversion prompt arrives with no justification the artisan can feel.

**5+ clients managed** — Same structural failure. The 5th client was added without friction. The upgrade prompt follows.

---

### The Undefined Edge Case: What Does the Path B Upgrade Prompt Actually Say?

D110 resolved the *triggers* but never resolved the *upgrade prompt content* for Path B. This is not a copywriting problem — it is an architectural gap.

Path A upgrade prompt: "Vous avez atteint la limite du plan gratuit. Passez à Essentials (€29/mois) pour continuer à envoyer des devis."

This prompt is:
- **Contextual**: the artisan hit a specific, visible limit
- **Actionable**: the upgrade directly removes the specific blocker
- **Timed**: it fires at the exact moment of frustration

Path B upgrade prompt for 45-day trigger: "...?"

What does this say? "Vous utilisez l'app depuis 45 jours" is a statement of fact, not a pain point. "Passez à Essentials pour..." — for what? The Free tier has no visible limit for Path B artisans. They haven't hit anything. The prompt has no natural completion.

This is the undefined edge case D110 created and never resolved. The conversion trigger exists in the decision log. The conversion *UX* does not.

---

### The Silent Accumulation Problem

Path B's usage-based triggers have a second structural flaw: **the artisan accumulates value without ever needing to pay for it**.

- Day 1-45: artisan logs jobs, manages clients, builds historical record
- Day 46: artisan is told to upgrade
- What does the artisan think? "I've been using this free for 45 days. Why do I need to pay now? Nothing stopped me."

Path A artisan can answer "why pay now?" with "because I hit the limit and can't send my next devis." Path B artisan cannot answer that question. The Free tier worked fine for 45 days.

The conversion rate for Path B will be lower than Path A precisely because the trigger lacks justification. The trigger fires — but the artisan doesn't feel *why* they should convert.

---

### The Path B Upgrade Prompt Problem: Proposed Resolution

**POSITION:** D110's Path B conversion triggers (45 days / 7 jobs / 5 clients) are insufficient as conversion mechanics without a corresponding upgrade prompt that the artisan experiences as justified. The current resolution leaves Path B conversion as "the trigger fires and then... what?"

The fix is not a better notification copy. The fix is that **Path B must have its own friction moment**.

Proposed resolution: Path B Free tier has a *soft limit* that creates the friction Path A has automatically:

- **Path B soft limit**: Free tier allows 1 client and 3 jobs. Above that: upgrade prompt. This creates a visible, blockable friction point for Path B — the artisan tries to add client #2 and is blocked. The upgrade prompt now has context: "Vous avez atteint la limite du plan gratuit pour la gestion de clients. Passez à Essentials pour gérer vos clients sans limite."
- **Path B soft limit alternative** (if client cap feels too restrictive for onboarding): Free tier allows unlimited job logging BUT only 10 jobs stored locally before sync-required. Artisan loses offline access above 10 unsynced jobs. The friction is "I can't log more jobs offline" — not a limit-hit, but a degraded-experience trigger.

Either way: Path B needs a *visible degradation of the Free tier* at a specific threshold — not an arbitrary day/job/client counter that fires without felt friction.

**D110 should be REFINED:** Path B conversion triggers require a corresponding Free tier soft limit that creates the friction moment. Without it, Path B conversion rates will be materially lower than Path A. The decision log currently specifies the trigger but not the friction that makes the trigger meaningful.

---

## Debate 144: D140 — AsyncStorage Cannot Survive 50 Jobs Over 3 Months

### Challenge: D140's AsyncStorage + retry queue assumption creates a silent data integrity failure at the exact moment of first meaningful use

**Assumption challenged from D140:** "AsyncStorage + retry queues" is adequate offline infrastructure for Sprint 0. It is not. The retry queue is not a synchronization mechanism — it is a best-effort heuristic that fails silently under the primary use case: an artisan using the app for weeks without reliable connectivity, then returning to sync.

---

### The Scenario: 50 Jobs Over 3 Months

Consider the Path B artisan who converts (eventually) and uses the app as intended:

- Month 1: Logs 15 jobs across 6 clients. Rural job sites, intermittent 4G, occasional dead zones in basements and rural France.
- Month 2: Logs 20 more jobs. Phone battery dies twice mid-entry. One session killed by OS during a long job entry.
- Month 3: Logs 15 more jobs. Goes on holiday for 2 weeks — phone in airplane mode.
- Day 90: Opens app at home on WiFi. Connection restored. Sync should happen.

**What happens in the AsyncStorage + retry queue architecture:**

1. **AsyncStorage stores the queue.** The queue is a serialized array of pending operations: `{ id, type: 'CREATE_JOB', payload: {...}, retries: 0, createdAt: '...' }`.

2. **When the phone died mid-entry (Month 2):** The in-memory operation was never written to AsyncStorage. The queue does not contain this job. The artisan does not know the job was lost until they check their job list and notice it's missing.

3. **When OS killed the process during a long session (Month 2):** Any jobs in the process of being added to the queue were in memory, not yet persisted. Gone.

4. **The retry queue processes old operations.** On reconnect, the queue sends 50 job records to the server. The server accepts them. The artisan sees "synced" — but the artisan has no idea how many jobs were lost in Months 1-2 when the phone died before the retry queue was updated.

5. **The artisan has no way to audit queue health.** How many operations are in the queue? How many failed? How many were lost to phone death? There is no queue status UI in the current D140 architecture.

**This is not an edge case. This is the primary use case.**

Rural French artisans (the core BTP demographic) face daily connectivity gaps. They work in basements, rural sites, inside buildings with poor reception. Phone death during long job entries is routine. The AsyncStorage + retry queue architecture loses data in exactly the conditions the product is designed for.

---

### The 3-Month Sync Is the Wrong Problem

The more immediate problem D140 doesn't address: **what happens when 50 jobs arrive at the server in a single sync burst after 3 months offline?**

The server receives: 50 job creation requests, 50 client records (some new, some updates to existing), potentially duplicate clients (if the artisan created "Jean-Michel" client on the phone while also having "Jean-Michel" from an earlier session that synced).

The server's current schema (D140: sync_status field added Sprint 0) can mark these as `pending` — but:

- **Duplicate client detection**: If "Jean-Michel" exists with ID `uuid-a` on the server, and the artisan created "Jean-Michel" locally with ID `uuid-b`, the server must either merge or reject. D140 says no conflict UI until Sprint 1.2. Server-wins is the fallback — but server-wins means the artisan's local "Jean-Michel" (with 15 jobs attached) gets orphaned or duplicated.
- **Client ID references**: Each job references a client ID. If the server's client record for "Jean-Michel" wins (server-wins), but the artisan's local job entries reference `uuid-b` (local), the jobs are now orphaned from the client record.
- **Retry queue ordering**: If job A was created before job B locally, but a network timeout caused B to sync before A, the server receives them out of order. The retry queue doesn't track dependency order — only retry count.

The D140 architecture says "server-wins conflict resolution in v1." Server-wins works fine for a single user syncing their own data *if* the client IDs match. It fails silently when the client ID universe has diverged (local created vs server existing).

---

### The Data Integrity Risk Is Not Visible

AsyncStorage corruption and phone-death data loss are **silent failures**. The artisan opens the app, sees their job list, doesn't see the jobs that died mid-write. They assume the app is working. Months later, when they need to produce historical records for their expert-comptable, they discover gaps.

This is the worst kind of data integrity failure: the artisan trusted the system, the system failed silently, and the failure only surfaces when the data is critically needed.

A retry queue that loses jobs when the phone dies is not a "retry" mechanism — it is a **false promise of reliability**.

---

### The Expo-Sqlite Deferral Is Not a Technical Problem — It's a Priority Problem

The debate log frames the AsyncStorage vs expo-sqlite decision as a technical tradeoff: expo-sqlite is better but costs +1-2 days. This framing is wrong. The real question is: **what does Sprint 0 offline actually guarantee?**

Under D140 (AsyncStorage + retry queue):
- Sprint 0 offline guarantees: operations attempted while online will be retried if they fail
- Sprint 0 offline does NOT guarantee: operations survive phone death, OS process kill, or app backgrounding mid-write

Under expo-sqlite (local SQLite + background sync worker):
- Sprint 0 offline guarantees: all operations are persisted locally before the network is attempted
- Operations survive phone death, OS kill, and app backgrounding because they are in a real database, not a queue in key-value storage

The +1-2 day cost is real. But the +0 alternative ships a system that loses data in normal use conditions.

---

### D140 Resolution: REFINED — AsyncStorage Is Not Adequate for Sprint 0 Job Logging

**POSITION:** D140's resolution (AsyncStorage + retry queues Sprint 0) is inadequate for the primary use case. The decision must be revisited.

Two options:

**Option A (preferred):** Accept +2 days to Sprint 0. Use expo-sqlite from Day 1. Local SQLite with background sync worker. Add `sync_status` enum (`pending/synced/conflict`). This is the architecture that matches the reliability requirements for a product whose primary value is historical job and client record-keeping.

**Option B (if 5-day Sprint 0 is non-negotiable):** Keep AsyncStorage for Sprint 0 but label it explicitly: "Sprint 0 offline is demonstration-only. Do not use for primary job logging on a job site. Data may be lost if the app is closed or the phone dies mid-entry." This is honest engineering. A 5-day Sprint 0 with an honest label is better than a 5-day Sprint 0 that silently loses data.

**What D140 must NOT be:** Sprint 0 ships with AsyncStorage + retry queue as if it is production-grade offline infrastructure. It is not. The +1 day framing (D140 says "+1 day" for expo-sqlite — Debate 130 established this estimate is false) was the mechanism by which this inadequate architecture got approved. Close that framing gap: there is no "+1 day" that ships production offline with AsyncStorage. The real cost is +2 days or a degraded, honestly-labeled Sprint 0.

**D140 REFINED:** AsyncStorage + retry queue is inadequate for Sprint 0 job logging reliability. Expo-sqlite (+2 days) or honest labeling of Sprint 0 offline as demonstration-only. The retry queue does not survive phone death — which is the primary use case, not an edge case.

---

## Summary: Two Challenges, Two Positions

| Decision | Assumption Challenged | My Position |
|----------|----------------------|--------------|
| D110 Path B | Usage-based triggers (45 days / 7 jobs / 5 clients) create a conversion prompt without a conversion *context* | D110 REFINED — Path B requires a visible Free tier soft limit (e.g., 1 client / 3 jobs cap) that creates friction equivalent to Path A's limit-hit moment. Without felt friction, Path B conversion rates will be materially lower. |
| D140 AsyncStorage | AsyncStorage + retry queue is adequate offline infrastructure for Sprint 0 | D140 REFINED — AsyncStorage cannot survive phone death mid-write (primary use case). Retry queue loses operations on process kill. 50-job sync burst creates client ID divergence risk with server-wins conflict resolution. Expo-sqlite (+2 days) or honestly-labeled demonstration-only Sprint 0 offline. |
