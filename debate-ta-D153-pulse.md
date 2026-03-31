# TA Position Paper: Draft-Mode Semantics for Sprint 0 — D153 Pulse Defense

## Core Position

Draft-mode with expo-sqlite is not the expensive option on the table — it is the only option that does not actively endanger legally-standing data and user trust, and the "2.5-day cost" estimate is inflated by a comparison point that itself carries hidden, uncosted failure modes.

---

## Key Arguments

1. **AsyncStorage + retry queues is not "simpler" — it defers complexity into failure modes that are harder to debug and harder to test.**  
   A retry queue assumes the write entered the queue before the phone died. In practice, the death happens mid-write, before the queue enqueue. The data is gone. This failure mode is not hypothetical — it is the common case for mobile crash scenarios. Debugging "why did this devis disappear" in production, with no local trace and a server that never saw the record, is a nightmare that costs more than the 2.5 days we are arguing about. expo-sqlite with atomic transactions eliminates this entire class of failure.

2. **The 2.5-day estimate is conservative because expo-sqlite + draft_status enum is a well-understood, low-risk implementation path.**  
   expo-sqlite has been battle-tested across hundreds of production React Native apps. The draft_status enum (pending / synced / conflict) is a straightforward schema addition. There is no novel research here. The "2.5 days" includes time for the Pending Drafts UI, which PS-D147's AsyncStorage approach also requires (you still need UI to show queued items). The net delta for draft-mode is the SQLite setup and schema migration — perhaps 1 day of actual new work, with 1.5 days for the UI that both approaches require anyway.

3. **"Sprint 0 is maxed out" is a resource argument, not a quality argument — and it proves too much.**  
   If Sprint 0 is truly at capacity, the thing to cut is NOT draft-mode; it is the view-only offline feature itself. View-only offline without draft-mode gives users the illusion of offline capability while creating a silent data-loss surface. A user who goes offline, makes changes, and sees those changes vanish when they return online has been actively harmed by the offline feature. Cutting draft-mode to "fit" Sprint 0 means shipping an offline mode that damages trust. If capacity is the constraint, the correct answer is to reduce scope to a narrower offline story — not to ship a dangerous one.

4. **View-only offline is not "good enough" — it is a different product, not a subset of the planned one.**  
   The Mini-CRM use case centers on devis creation and modification. A field agent who visits a client, captures requirements offline, and returns to connectivity expecting their devis to be there is not doing "view-only" work. They are doing data entry. View-only offline serves the use case of "I need to reference existing devis while on the metro." It does not serve the use case of "I need to create a new devis from a client site with no connectivity." Draft-mode serves both. Building view-only and planning to "add writes later" means building the easy half first and front-loading the hard half into Sprint 1 under pressure — which is exactly the path to technical debt.

5. **Server-wins conflict resolution is not a safety compromise — it is silent document annihilation.**  
   Under Code civil Art. 1127-1, a devis is a legally-binding commercial document the moment it is presented to a client. If the server silently overwrites a local draft on conflict (server-wins), the agent's work is gone without warning, without recovery path, and potentially without the agent ever knowing. This is not a UX inconvenience — it is a data-integrity failure with legal exposure. Draft-mode makes conflicts visible and recoverable. That is not optional for a product where the primary artifact is a legally-standing devis.

---

## Challenged Assumptions (Explicit)

- **Assumption A:** AsyncStorage + retry queues is a simpler or cheaper implementation than expo-sqlite + draft-mode.  
  **Challenge:** It shifts complexity into failure modes that are harder to detect, harder to reproduce, and harder to fix in production.

- **Assumption B:** The 2.5-day cost for draft-mode is a net addition to Sprint 0 timeline.  
  **Challenge:** The Pending Drafts UI is required by BOTH approaches. The net new cost of draft-mode is the SQLite layer, which is ~1 day. The remaining 1.5 days is shared UI work.

- **Assumption C:** If Sprint 0 is at capacity, view-only offline is an acceptable fallback scope.  
  **Challenge:** View-only offline does not serve the primary use case (devis creation in the field). It is a different, narrower product. Cutting draft-mode to preserve view-only is shipping half a feature that actively misleads users about what they can do offline.

- **Assumption D:** Server-wins conflict resolution is a reasonable safety trade-off for Sprint 0.  
  **Challenge:** For a legally-standing document type, silent overwrite is not a trade-off — it is an unacceptable data-loss vector with potential legal consequences.

- **Assumption E:** "Sufficient for Sprint 0" as defined by PS-D147 is the right success criterion.  
  **Challenge:** "Sufficient" that destroys data is not sufficient. The criterion must be "safe for the data model," not "fits in the sprint."

---

## Verdict Recommendation

**D140 (expo-sqlite + draft_status enum + Pending Drafts UI) should be adopted as-is for Sprint 0.**

The 2.5-day estimate is conservative and likely 1.5 days of net new work when UI costs are properly attributed to both options. The risk of AsyncStorage + retry queues is not a timeline risk — it is a data-loss risk that surfaces in production after the sprint is closed, making it harder and more expensive to fix than building it correctly the first time.

If Sprint 0 capacity is genuinely the constraint, the correct scope reduction is to **delay offline entirely** rather than ship view-only offline with a hidden write failure mode. Draft-mode is not the luxury add-on — it is the foundation that makes offline safe to ship.
