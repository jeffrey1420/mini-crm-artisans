## Debate TA-D148: Offline Capability Is the Wrong Problem — Multi-Device Conflict Resolution Is

---

### Challenge Statement

The 02:28 pulse debated AsyncStorage vs expo-sqlite and correctly identified that **both are insufficient**. But the follow-up framing — "the real problem is offline capability" — is still the wrong diagnosis. The actual architectural gap is **multi-device conflict resolution**, and no debate-log proposal in this pulse, D140, D144, or D9 addresses it. This paper argues that the Sprint 0 offline scope must be reconceived as "draft-mode only" — offline changes queue as new documents, not direct overwrites — because the alternative (direct overwrites with any conflict resolution strategy) is architecturally v1.2 minimum.

---

### The Real Scenario No Debate Has Addressed

**Marc edits a devis on his phone while offline. Simultaneously — on the same business account — his wife makes a different edit via the web dashboard. The phone comes back online 3 days later. What happens?**

This is not a hypothetical edge case. It is a direct consequence of three resolved decisions:

- **D9 (Not MVP):** "No multi-user" was scoped at a time when the product was single-device solo artisan. D3 (Primary persona: Marc — solo smartphone-native) was resolved with the implicit assumption that Marc is the only human using the account. But the product is a business tool, not a personal app. Spouses, partners, and assistants sharing a craft business account is normal in French micro-SMBs. The "solo" assumption in D3 is a **persona constraint, not an architectural constraint**. The system must not break when a second human uses it.
- **D140 (AsyncStorage offline):** The retry queue fires after 3 days offline. It sends Marc's local edits to the server. The server has his wife's edits already. The retry queue has no concept of "Marc's edits happened before his wife's edits" or vice versa — because Marc was offline when he made them, there is no server timestamp for his local edits.
- **D144 (expo-sqlite migration):** Even with SQLite under the hood, the sync protocol is still a last-write-wins or server-wins strategy. Expo-sqlite is a storage engine. It does not define conflict semantics. It does not know that a devis edit is a versioned business document with TVA implications, not a key-value overwrite.

**The honest answer to "what happens":** Nobody knows. The debate log has no decision for this scenario. That is the architectural gap.

---

### This Is NOT a Sync Problem — It Is a Business Logic Problem

Every debate about offline capability frames it as a **data synchronization problem**: how do we get data from the device to the server reliably? The answers offered — AsyncStorage + retry queues, expo-sqlite + background sync, WatermelonDB — are all synchronization solutions. They answer the question: "how does data move from A to B?"

They do not answer the question: **"when the same business document is edited in two places with conflicting intent, which version is the legal record?"**

A devis is not a text field. It is a **versioned business document** with French legal implications:

- A devis has a **séquentiel number** (D32: sequential numbering enforcement). If Marc's offline edit changes line items and his wife's web edit changes the status, which séquentiel number represents the authoritative record?
- A devis has **TVA calculations** per line item (5.5%, 10%, 20%). If two edits modify different line items, the TVA breakdown in the footer changes. There is no "merge" operation for a TVA-per-line document — only a "which version of the entire document do we treat as real?"
- A sent devis has **legal standing**. If Marc's phone had an older cached version and his wife updated the prices before the client signed, the signed document must match what was actually sent. An offline edit that overwrites the sent version with a stale local copy creates a **document discrepancy** — not a sync conflict, a **legal record inconsistency**.
- French artisans are required to keep **cohérent** (internally consistent) financial records. A devis that shows 3 line items in one version and 5 in another, with no audit trail of which was sent to the client, is a compliance issue — not a UX issue.

**The debate-log has treated devis as structured data. It is actually structured legal documentation.** These are different engineering problems.

D32 (Sprint 0 schema design) correctly identified sequential numbering and TVA multi-taux as schema complexity. It did not identify that **offline editing creates version forks of legally significant documents** — because that was outside the scope of the schema design debate. But that is the correct scope, and it was never debated.

---

### The CRDT/Operational Transform Argument — And Why It Is v1.2, Not Sprint 0

Any competent multi-device conflict resolution strategy requires one of:

- **CRDT (Conflict-free Replicated Data Types):** Elegant mathematical approach. Each operation is commutative — operations can be applied in any order and converge to the same state. Problem: CRDTs require operations to be decomposed into fine-grained, commutative units. A devis line-item edit is not naturally a CRDT operation. You cannot trivially CRDT-merge "Marc changed line 2 price to €85" and "Sophie changed line 2 description to 'fourniture plomberie'" into a single coherent document without semantic understanding of what changed.
- **Operational Transform (OT):** The Google Docs approach. Transforms concurrent operations against each other to produce a consistent result. Problem: OT requires a central server to order and transform operations. For a web + mobile architecture with offline-first clients, you need an OT server that can receive, transform, and redistribute operations. This is a non-trivial server component that does not exist in the current Sprint 0 Fastify architecture.
- **Manual merge UI:** The simplest approach. When a conflict is detected, show both versions to a human and let them choose. Problem: for a French artisan using the app on a job site, a "resolve this conflict" modal at 7:30 AM before heading to a client is not a good UX. And the conflict may not surface immediately — it may be detected only when a TVA-deducted invoice is generated from a devis that has conflicting line items.

**None of these is a Sprint 0 deliverable.** CRDT engineering for a business document model is a research problem before it is an implementation. OT requires a server component and API redesign. Manual merge requires a conflict UI that D140 explicitly deferred to v1.2.

The debate-log has been comparing AsyncStorage vs expo-sqlite as if the choice of local storage engine determines the offline capability. It does not. Neither storage engine provides conflict resolution semantics. Neither was designed to.

---

### Challenging a Prior Assumption: D9's "No Multi-User" Is Inconsistent With the Offline Architecture

**D9 (Not MVP):** "No Kanban, no multi-user, no offline, no API keys."

D9 correctly excluded multi-user from Sprint 0 scope as a product feature — multiple simultaneous editors on the same account is not a Day 1 requirement. But the debate-OfflineFirst.md (Technical Architect position, D146-era) argued that offline capability is required at launch because "the stack change invalidates the original 'no offline' reasoning."

**The conflict these two positions create:** If offline editing is enabled for a single-user on a solo device, D9's exclusion of multi-user is coherent. If offline editing is enabled for a device that shares an account with a web dashboard (Marc + spouse), then D9's exclusion of multi-user has been implicitly violated by the offline architecture itself — regardless of whether "multi-user editing" was intended as a product feature.

The debate-OfflineFirst.md argues (correctly) that offline-first with a solo device is "dramatically simpler than D9's framers assumed." But this simplification only holds when the device is the **sole writer** to the account. The moment you enable offline editing, you have created a second writer — the offline device — that will eventually conflict with the first writer — the server/web dashboard.

D9's exclusion of multi-user as a **product feature** is correct. But the offline-first architecture has implicitly introduced multi-writer semantics without resolving the multi-writer conflict problem. The assumption that "solo device = no conflict risk" is what the 02:28 pulse's conclusion correctly challenged.

---

### Challenging a Prior Assumption: D140's "Server-Wins" Fallback Is Not a Resolution

**D140 (AsyncStorage offline):** "Last-write-wins with conflict detection UI. For a solo artisan, conflicts are rare and trivially resolvable — show both versions, let Marc pick. No distributed consensus needed. Server-wins as fallback."

D144 (Technical Architect, 01:15 pulse) refined D140 by noting that "server-wins works fine for a single user syncing their own data *if* the client IDs match. It fails silently when the client ID universe has diverged."

But the deeper problem with D140's server-wins fallback was never articulated in D144: **server-wins on a devis document is not a sync strategy — it is document destruction**.

Consider: Marc's phone has been offline for 3 days. During those 3 days, his wife (web dashboard) updated the devis to reflect a client-requested price change and sent it to the client. Marc, on his phone, made different edits to the same devis (different line items, different pricing). When Marc's phone comes online:

- **Server-wins:** Marc's edits are discarded. His local changes — which he made believing he was working on the current document — vanish. The devis his wife sent is preserved. Marc sees his edits disappear with no explanation.
- **Client-wins (last-write-wins):** The sent devis is overwritten with Marc's offline version. The client received a different document than what is now stored in the system. The coherence between "what was sent" and "what is stored" is broken.

Neither outcome is acceptable. "Show both versions and let Marc pick" requires a conflict UI — which D140 explicitly deferred to v1.2. Without that UI, the fallback is either data loss (server-wins) or document incoherence (client-wins).

D140's server-wins fallback is not a conflict resolution strategy. It is an **arbitrary choice between two bad outcomes**, pre-made without user input. For a business document with legal standing, this is not a fallback — it is a liability.

---

### The Honest Sprint 0 Answer: Frozen Window or Draft Mode

The correct Sprint 0 architecture for offline editing is one of two options — both honest about what offline editing actually does:

**Option A — Frozen Window (Recommended):**

When the app goes offline, a **frozen timestamp** is recorded. While offline, any edits made to a devis are saved as **draft edits** — not overwrites to the live document. When connectivity returns, the sync protocol does not apply the draft as a conflict against the server version. Instead:

- The draft is flagged for review: "You made changes to this devis while offline. Your spouse made changes on [date]. Review before saving."
- The artisan manually reviews both versions and confirms the final state.
- Only after manual confirmation does the draft become the live document.

This preserves document coherence, respects both editors' work, and makes the conflict visible rather than silent. The cost: a review-and-confirm UI for offline drafts. This is a small feature (half a day) and is honest about what the system is doing.

**Option B — Draft Mode (Simpler):**

Offline edits are always treated as **new drafts** — never as overwrites of existing documents. When connectivity returns, the artisan sees: "You created a draft of [devis name] while offline. Send as new?" This is the "reply as new email" pattern. The original document is never touched.

This is simpler to implement (no conflict UI, no frozen timestamp) but less powerful. It treats every offline edit as a new document creation. For an artisan who makes minor offline corrections to an existing devis, this is cognitively awkward — they wanted to update the existing devis, not create a new one.

**Option A is the correct Sprint 0 answer.** It makes conflicts visible rather than silent, respects the legal standing of business documents, and is implementable within Sprint 0 with a modest scope addition (draft review screen).

---

### This Changes the Sprint 0 Deliverable Scope

The 02:28 pulse concluded that both AsyncStorage and expo-sqlite are insufficient for offline capability. That conclusion is correct — but for the wrong architectural reason. The problem is not which local storage engine. The problem is **what offline edits mean when they rejoin a shared document store**.

The Sprint 0 deliverable must change:

**What was planned (D140/D144):**
> "Offline editing with retry queue. Server-wins fallback. Conflict UI in v1.2."

**What should be planned (this paper):**
> "Offline editing with draft-mode semantics. When offline, changes are saved as drafts pending review. They do not overwrite the live document until the artisan explicitly confirms after reviewing any concurrent changes. This is not sync — it is draft-queue. Real sync with conflict resolution = v1.2 minimum."

This is not scope reduction. It is scope precision. The technical implementation of draft-mode (storing edits as new records with a `parent_document_id` reference) is not significantly more complex than the retry queue approach — but it eliminates the silent data destruction problem that D140's server-wins fallback creates.

The storage engine debate (AsyncStorage vs expo-sqlite) becomes secondary once the semantic model is "drafts, not overwrites." Either engine can store drafts. Expo-sqlite is still preferred for reliability (D144's argument about phone-death data integrity stands on its own), but it is no longer the linchpin of the offline architecture.

---

### Verdict

The 02:28 pulse correctly identified that the AsyncStorage vs expo-sqlite debate was the wrong question. This paper supplies the correct question: **what do offline edits mean in a multi-writer document system, and what is the Sprint 0 answer to that question?**

The verdict on TA-D148:

> **Offline capability is not the core architectural gap. Multi-device conflict resolution on versioned business documents is the gap — and no proposal in the debate log addresses it. Sprint 0 offline editing must be scoped as "draft-mode only": changes made offline queue as drafts pending manual review, never as direct overwrites of the live document. Real bidirectional sync with conflict resolution is a v1.2 deliverable requiring CRDT or OT infrastructure that does not exist in the current architecture. The Sprint 0 deliverable scope changes accordingly: draft review screen replaces retry-queue conflict fallback. Expo-sqlite is preferred for local storage reliability but is not the architecturaldeterminant — the draft semantic model is.**
