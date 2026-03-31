# D141 Resolution Pulse — Growth Strategist Position Paper

**Date:** 2026-03-31T04:17
**Author:** Growth Strategist (GS-D154)
**Status:** OPEN — requires Louis or pulse resolution

---

## Executive Summary

D141 ("stay-in-touch digest for dormant Path B users") has appeared as a "RESTATED" or "REFINED" item at four consecutive pulses (00:58, 01:15, 01:29, 02:59) but has never received a formal verdict. The 02:59 pulse explicitly deferred WhatsApp to v1.1 and confirmed Expo Push as the Sprint 0 notification architecture. This creates a logical gap: D141's digest was never formally re-scoped as Expo Push, nor was it formally killed. The item persists in ambiguity. This paper argues D141 must be formally resolved — either as KILLED (WhatsApp digest deferred to v1.1) or as an Expo Push digest with a fully specified minimum viable implementation.

---

## D141 History — Four Pulses, Zero Verdicts

| Pulse | Action | What Changed |
|-------|--------|--------------|
| 00:58 | ORIGIN | "bi-weekly WhatsApp digest, 14+ days dormant + ≥1 job logged + Path B" |
| 01:15 | RESTATED | Added: "Plain text, user metrics, single CTA, no sales language." Specification expanded but no verdict issued. |
| 01:29 | RESTATED | D146 proposes treating as in-app digest only (no WhatsApp in Sprint 0). WhatsApp explicitly challenged. No verdict — "restated" again. |
| 02:59 | REFINED | "WhatsApp is a retention layer, not acquisition. Path B activation at v1 = Expo Push. **WhatsApp in v1.1 when premium content exists.**" |

At 02:59, WhatsApp was deferred to v1.1 — meaning the digest's delivery channel (WhatsApp) was explicitly removed from Sprint 0 scope. Yet D141 itself was never given a verdict. "Refined" is not a verdict.

---

## The Logical Gap: What Is D141 Now?

**The 02:59 refinement states:**
1. "WhatsApp is a retention layer, not acquisition" — framing clarification
2. "Path B activation at v1 = Expo Push" — notification architecture confirmed as Expo Push only
3. "WhatsApp in v1.1 when premium content exists" — WhatsApp explicitly deferred

**The problem:** D141's digest specification was built on WhatsApp as the delivery channel. When 02:59 killed WhatsApp for Sprint 0, D141's digest lost its channel — but was never re-scoped or killed. This creates a zombie item:

- **If D141's digest is a WhatsApp digest:** It was implicitly killed at 02:59 (WhatsApp deferred to v1.1) and should be marked KILLED, not "restated"
- **If D141's digest can be delivered via Expo Push:** Then it needs to be formally re-scoped as an Expo Push digest and fully specified
- **If D141 is about Path B retention in general:** It should not be conflated with the digest specification, which had a specific channel

The 02:59 pulse resolved the Sprint 0 notification architecture as **Expo Push only**. There is no room in that architecture for a WhatsApp digest. Therefore, D141's digest was implicitly killed — but never formally recorded as such.

---

## Argument 1: D141's Digest Was Implicitly Killed at 02:59

The 02:59 pulse made two decisions directly relevant to D141:

1. **"Path B activation at v1 = Expo Push"** — The Sprint 0 notification channel for Path B activation is Expo Push. There is no mention of a digest in this decision.
2. **"WhatsApp in v1.1 when premium content exists"** — WhatsApp is explicitly not in Sprint 0.

D141's digest specification (bi-weekly, 14+ days dormant, Path B, plain text, user metrics, single CTA) was designed as a **WhatsApp message**. With WhatsApp deferred to v1.1, the digest has no channel. The 02:59 pulse did not say "we'll deliver the digest via Expo Push instead." It said WhatsApp is deferred.

**Therefore:** D141's digest was functionally killed at 02:59. The failure to mark it as KILLED is a documentation gap, not an active decision.

---

## Argument 2: D141 Cannot Be "Restated" Four Times Without a Verdict

Each pulse added specification without resolving scope:

- 00:58 → defined digest format
- 01:15 → added "plain text, user metrics, single CTA, no sales language"
- 01:29 → raised in-app alternative (D146)
- 02:59 → deferred WhatsApp entirely

"Restated" is a holding pattern. It defers resolution while accumulating specification. This is not a decision — it is indecision documented as progress. D141 now carries four pulses of accumulated specification with zero verdicts. This is not a living document; it is unresolved scope debt.

---

## Argument 3: A Digest Is Not a Notification — Expo Push Digest Requires Separate Evaluation

The 02:59 resolution states "Path B activation at v1 = Expo Push." This resolves **notifications** (one-time, event-driven alerts). It does not resolve **digests** (periodic summaries, batched by time/dormancy).

A digest has different semantics than a notification:
- **Notification:** "Your client paid €450" — immediate, event-driven, action-oriented
- **Digest:** "You have 3 pending devis and 2 unpaid factures from the past 14 days" — periodic, dormant-user reactivation, summary-oriented

These require different infrastructure:
- Notification delivery: event-driven push (already resolved at 02:59 as Expo Push)
- Digest delivery: scheduled/batched push (NOT resolved at 02:59 — Expo Push is the vehicle, but the batch/schedule logic is unbuilt)

Therefore: even if D141's digest is re-scoped as Expo Push, it is not covered by the 02:59 notification architecture resolution. It requires a separate, explicit resolution.

---

## Proposed Resolutions (Choose One)

### Option A: KILL D141 (WhatsApp Digest — Deferred to v1.1)

**Rationale:** The 02:59 pulse effectively killed D141's digest by deferring WhatsApp to v1.1. Formalizing this as KILLED removes ambiguity and keeps the v1.1 backlog clean.

**What gets recorded:**
- D141 (WhatsApp digest) = KILLED
- Re-opened as: D141-v1.1 (WhatsApp digest, Sprint 0 scope excluded)
- Sprint 0 re-activation for dormant Path B users = Path A conversion mechanics only (D96 resolved as first facture created)

**What gets lost:**
- The digest specification (14+ days dormant, Path B, plain text, single CTA) is not implemented in Sprint 0

---

### Option B: RE-SCOPE D141 as Expo Push Digest (Sprint 0)

**Rationale:** Path B users who dorm after initial app usage (but before converting via Path A) need a re-activation mechanism. A minimal Expo Push digest is achievable in Sprint 0 and does not require WhatsApp infrastructure.

**Minimum viable digest specification (re-scoped as Expo Push):**

| Parameter | Value |
|-----------|-------|
| **Trigger** | 14+ days since last app session + ≥1 job logged + Path B user (logged, not converted) |
| **Frequency** | Bi-weekly (14 days) maximum — once fired, cooldown resets |
| **Delivery channel** | Expo Push notification (not WhatsApp) |
| **Content** | Plain text only, no sales language |
| **Body format** | "Vous avez [X] devis en attente et [Y] factures non payées depuis votre dernière visite." |
| **Single CTA** | Deep link to home view (Active Job Card if exists, else job list) |
| **Anti-spam** | Fires maximum once per 14-day window; cooldown resets on any app open |
| **No metrics** | User-specific stats removed (simplicity, no "you have 3 pending" personalization in v1) |
| **No acquisition framing** | No "invite a friend," no upgrade prompts, no premium upsell |

**What this achieves:**
- Re-activation loop for dormant Path B users without WhatsApp infrastructure
- Fits within 02:59 Expo Push architecture
- Minimal scope — single scheduled push job, no new infrastructure
- Retains D141's core intent (stay-in-touch for dormant Path B users) without WhatsApp

**What this sacrifices:**
- WhatsApp's superior open rates and conversational format
- Personalization (metrics, user-specific stats)
- These are v1.1 enhancements, not Sprint 0 blockers

---

## Decision Required

| Option | What Happens | Sprint 0 Impact |
|--------|-------------|-----------------|
| **A (Kill)** | D141 WhatsApp digest = KILLED, re-opened as v1.1 item | No digest in Sprint 0 |
| **B (Re-scope)** | D141 = Expo Push digest, fully specified above | Minimal — one scheduled push job |

**The item cannot remain in "restated" limbo. Four pulses of restatement without a verdict is scope debt, not progress.**

---

## Recommendation

**Growth Strategist recommends Option B (re-scope as Expo Push digest).**

Rationale: Path B users who log jobs but don't convert represent a distinct failure mode — the app failed to demonstrate enough value to convert them before they stopped opening the app. A single, minimal digest (14+ days dormant, single re-entry CTA, no sales language) is the lowest-friction way to attempt re-activation without building WhatsApp infrastructure. It fits within the 02:59 Expo Push architecture and adds no new Sprint 0 blockers.

However, this is a Louis decision — not a Growth Strategist unilateral call. The choice between Option A and Option B has implications for Sprint 0 scope and v1.1 planning.

**Status: OPEN — requires Louis or pulse resolution.**
