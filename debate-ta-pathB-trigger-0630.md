# POSITION PAPER

## Topic: Path B Trigger Is Unimplemented in Sprint 0

**Author:** Technical Architect  
**Date:** 2026-03-31  
**Session:** ta-pathB-trigger-0630

---

## Executive Summary

D110's Path B trigger — "5 jobs logged" — is **not implementable in Sprint 0**. The `jobs` concept does not exist in the Sprint 0 data model, schema, or feature scope. Treating this decision as Sprint 0-ready is a latent scope conflict that will surface mid-build and require emergency renegotiation. This paper documents the architectural mismatch, the logical gaps, and proposes two concrete resolution paths.

---

## 1. "Job" Is Not Defined in the Sprint 0 Schema

Sprint 0 scope, as ratified, covers:

- Client management (create/edit/delete clients)
- Devis creation and lifecycle (create/accept/decline/envoyer)
- Facture creation (standalone, not yet tied to devis acceptance)
- TVA calculator
- Sequential numbering (devis + facture)
- Mentions légales

**There is no `jobs` table, no job logging UI, no job events, and no job state machine in Sprint 0.**

The D13 home view — which includes the "Active Job Card" — is explicitly scoped to Sprint 1+. The Active Job Card is a Sprint 1 deliverable. The job entity it displays does not exist in the Sprint 0 database.

Therefore, the conversion trigger **"5 jobs logged"** references a data object that will not exist when the trigger is supposed to fire. This is not a minor gap. It is a structural dependency: you cannot count jobs that are never created.

---

## 2. The Path B Persona Doesn't Match the Sprint 0 Data Model

Path B was designed for artisans who operate on **verbal agreements** — no formal devis, no paper trail, just work performed and invoiced. Their primary interaction with the app is logging work done.

But Sprint 0 does not support job logging. Day 1 features are:

- Add a client
- Create a devis (which may or may not be sent)
- Record a facture
- Calculate TVA

There is no UI for "log a job." There is no event emitted when a job is logged. There is no persistence model for job state.

If Path B artisans cannot log jobs in Sprint 0, they have **no meaningful Day 1 workflow**. They cannot be converted via a trigger that requires an action they cannot perform. The Path B persona is effectively locked out of the beta until Sprint 1.

This is not a user research problem. It is a **build sequencing problem**.

---

## 3. Path B Trigger Creates an Unplanned Feature Dependency

D110 implies the following dependency chain:

```
5 jobs logged → job logging must exist → job logging is Sprint 1+ → Path B trigger cannot fire until Sprint 1
```

Three resolution paths exist, but only one was not taken:

**(a) Scope creep Sprint 0 to include job logging.**  
This undermines the Sprint 0 definition — a stable, constrained MVP — and creates risk of delay. Job logging has its own UX, data model, and state machine. It cannot be bolted on cheaply.

**(b) Defer Path B trigger to Sprint 1 (when job logging ships).**  
This is honest but was never recorded as a decision. The D110 log shows no such caveat. The decision implies Sprint 0 readiness when it does not exist.

**(c) Redefine Path B trigger using Sprint 0 primitives.**  
This is the correct approach and is detailed in Section 5.

The team proceeded as if (c) was the intent without ever doing the work to define what (c) actually means. The decision is underspecified.

---

## 4. The 5-Job Threshold Is Arbitrary

Even if job logging existed, the threshold of **5 jobs** was chosen for plausibility, not derived from user behavior data. There is no cohort analysis, no funnel study, no user interview that establishes that 5 is the correct number versus 3, 7, or 12.

This matters because:

- Too low: artisan converts before establishing habit
- Too high: artisan churns before reaching the trigger
- Arbitrary: no basis to defend in design review or stakeholder meeting

Without data, any threshold is a guess. The 5-job figure should be treated as a **hypothesis**, not a commitment.

---

## 5. Resolution Proposal

### Option A: Redefine Path B Trigger Using Sprint 0 Primitives (Preferred)

Path B artisans who don't send formal devis can still be identified by **engagement signals that exist in the Sprint 0 schema**:

**Proposed Path B trigger (Sprint 0-compatible):**
> *"5 client records created with at least 1 facture issued, and no devis has been sent in the session."*

This captures the Path B behavior (informal workflow, no devis, relying on factures) using only:

- `clients` table
- `factures` table
- `devis` table (as a negative filter: no devis sent)

It does **not** require job logging. It maps to real Sprint 0 data. It fires at a moment the system can actually detect.

**Alternative (simpler):**
> *"3 factures created, 0 accepted devis in the same session."*

This identifies the artisan who works informally and bypasses devis entirely. Threshold of 3 is still a hypothesis but is more conservative (faster conversion signal, lower risk of churn before trigger).

### Option B: Explicitly Defer Path B Trigger to Sprint 1

If the team cannot agree on a Sprint 0-compatible trigger, Path B should be **explicitly marked as Sprint 1**:

> *"Path B conversion trigger is out of scope for Sprint 0. Path B artisans will be eligible for the same onboarding flow as Path A until job logging ships in Sprint 1. D110 is revisited at Sprint 1 planning."*

This is a valid outcome. It is honest. It avoids shipping broken conversion logic. But it requires a recorded decision — not silence.

---

## 6. Recommended Decision

**Adopt Option A with the "3 factures, 0 accepted devis" trigger.**

Rationale:

1. Uses only Sprint 0 schema primitives
2. Fires faster than 5-job (lower churn risk)
3. Captures the Path B behavioral signature (informal, no devis)
4. Is testable and measurable from Day 1 of beta
5. The 3-facture threshold remains a hypothesis but is no worse than 5 and costs less in churn

**Action required before Sprint 0 build begins:**

- [ ] Decision recorded: Path B trigger = "3 factures created, 0 accepted devis"
- [ ] D110 updated to reflect Sprint 0-compatible trigger definition
- [ ] Analytics event defined: `path_b_trigger_fired` with context `{ factures_count, accepted_devis_count, session_id }`
- [ ] Threshold reviewed at first data review (post-beta week 2)

---

## Appendix: Schema Gap Summary

| Concept | Sprint 0 | Sprint 1+ | D110 Trigger? |
|---|---|---|---|
| Client records | ✅ Exists | — | ❌ Not used |
| Devis | ✅ Exists | — | ❌ Not used |
| Facture | ✅ Exists | — | ✅ Proposed |
| Job logging | ❌ No schema | ✅ Full feature | ❌ Required by trigger |
| Active Job Card | ❌ No UI | ✅ D13 | ❌ Required by trigger |

D110's trigger requires Sprint 1 infrastructure to exist in Sprint 0. This is the core problem.

---

*Filed by: Technical Architect | 2026-03-31 | For Mini-CRM debate resolution*
