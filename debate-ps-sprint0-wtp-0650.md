# POSITION PAPER

## Topic: Sprint 0 Cannot Proceed Independently of WTP Validation — The Parallel Assumption Is False
**Author:** Product Strategist
**Date:** 2026-03-31
**Session:** ps-sprint0-wtp-0650

---

## Executive Summary

The debate log treats Sprint 0 and WTP validation as independent workstreams running in parallel. This assumption is wrong. Sprint 0 builds features whose conversion logic, billing triggers, and success metrics are all anchored to a €29/month price point that has never been validated. If WTP validation reveals €29 is too high, Sprint 0's output must be rebuilt — and Louis cannot meaningfully run both tracks simultaneously. The "parallel" framing conceals a hidden dependency that creates rework risk, decision debt, and capacity collapse. Sprint 0 must either be delayed until WTP data arrives, or radically scoped to exclude every feature whose behavior depends on validated pricing.

---

## Section 1: The Parallel Assumption Creates a Hidden Rebuild Risk

The assumption under scrutiny: *"Sprint 0 should proceed while WTP validation happens in parallel."*

This framing implies two independent tracks that do not affect each other. They are not independent. Here is the dependency chain:

**Sprint 0 scope → anchored to €29/month:**

- D138 billing structure decision (monthly €29 as primary CTA, annual €240 available) → requires €29 to be the right price
- Conversion triggers at Day 30 → require a price to evaluate conversion success against; if €29 is wrong, the 3% Day-30 conversion target is meaningless
- Sprint 0 exit criteria → "5 beta users complete the happy path and pay €29" → if €29 is wrong, this gate validates nothing
- Path A vs Path B routing → the trigger logic depends on user behavior that is shaped by whether the price feels legitimate

**If WTP reveals €29 is too high** (say, artisans would only pay €15):
- The billing structure decision was premature. Sprint 0 built a checkout flow for a price that fails.
- The Day-30 conversion target of 3% was calibrated to the wrong price. Artisans who would pay €20 churn; the 3% metric masks this with a false ceiling.
- The Sprint 0 exit gate ("5 beta users paid €29") was satisfied under social pressure from known contacts — not under genuine market validation.

**If WTP reveals €29 is too low** (say, artisans would pay €40):
- Sprint 0 locked in a suboptimal price. Annual €240 undervalues annual contracts by ~50% versus WTP.
- Every Sprint 1 pricing decision is anchored to a low price that will be hard to escalate.

In neither case does Sprint 0's 6.5 days survive intact. **The work is not independent of the WTP outcome.** Running them in parallel means running Sprint 0 as a bet that €29 is correct — and committing 6.5 days to that bet before the data exists to evaluate it.

---

## Section 2: Louis Does Not Have Capacity to Run Both Tracks Simultaneously

The "parallel" framing also assumes Louis can execute WTP conversations (5 × 20 minutes = ~2 hours of conversations, plus prep and synthesis) while simultaneously building Sprint 0 features. This is not a time allocation problem. It is a cognitive context-switching problem.

**What WTP validation actually requires:**

- Identifying and recruiting 5 real beta users (not the same 5 people in the current beta pool, because they were pre-primed by Louis and each other)
- Scheduling and conducting 5 semi-structured conversations in French, in the next 2-3 days
- Synthesizing results and deriving a directional WTP range
- Making a go/no-go decision on €29 before Sprint 0 scope is finalized

This is not 2 hours of calendar time. It is a focused research sprint that requires Louis to hold the user's perspective in mind — *"what would a 50-year-old electrician in Brittany actually pay for this?"* — while resisting the pull to confirm what he already believes.

**What Sprint 0 building requires:**

- Deep technical focus over 6.5 consecutive days
- Decision-making on schema, API design, UI component architecture
- Coordination with potentially one additional developer
- Avoiding interruptions that break the build flow

Running both simultaneously means Louis is either:
(a) Switching contexts every 2-3 hours between user research and building — degrading both quality
(b) Running WTP validation in the margins (evenings, between build sessions) — producing shallow, rushed data that doesn't actually inform Sprint 0 scope
(c) Delegating Sprint 0 build to someone else — but the debate log contains no indication of a second developer

The "parallel" framing is only affordable if WTP validation is treated as a checkbox — 5 quick conversations that produce no actionable synthesis. If WTP validation is done properly, it consumes Louis's cognitive bandwidth for 2-3 days at a critical moment in Sprint 0. The parallel assumption only works if the validation is performative rather than real.

---

## Core Position

**Sprint 0 and WTP validation are not independent. They are sequential. Sprint 0 should not begin until the WTP directional range is established.**

The parallel framing is a comfortable fiction that:
1. Commits 6.5 days of build effort to a price that has not been validated
2. Risks rebuilding Sprint 0 features if WTP reveals €29 is wrong
3. Overloads Louis's capacity by running two cognitively demanding tracks simultaneously
4. Produces a Sprint 0 exit gate ("5 beta users paid €29") that is meaningless if the price was wrong

The WTP experiment is not a Phase 2 research project. It is a Sprint 0 prerequisite. The debate log has been treating it as optional — "we'll do it in parallel, it only takes a few conversations." This framing must stop. **WTP is a scope-defining input, not a parallel workstream.**

---

## Resolution Proposal

### Phase 0: WTP Validation (2 days, starting today)

**Objective:** Establish directional WTP range before any Sprint 0 build decisions are made.

**Format:** 5 semi-structured conversations with real French artisans (not current beta pool), 20 minutes each.

**Participants:** 5 artisans aged 45-55, solo operation, smartphone-native, active client base. Recruitment via personal network with strict screening: exclude anyone who has already heard about the product or met Louis in a product context.

**Decision rules:**
- Median WTP ≤ €15 → €29 is too high. Sprint 0 pricing must be reconsidered before billing structure is set. Sprint 0 proceeds with revised pricing or scope adjustment.
- Median WTP = €20-35 → €29 is in range. Sprint 0 proceeds with D138 billing structure (hidden-link monthly-primary).
- Median WTP ≥ €40 → €29 is underpriced. Sprint 0 pricing conversation must happen before committing to €240 annual.

**Output:** A directional range, not a precise number. A clustered answer across 5 users is sufficient to make a go/no-go on €29.

### After WTP: Sprint 0 Scope Decision (Day 3)

**If €29 is validated:** Sprint 0 proceeds as planned. 6.5 days. D138 billing structure: monthly €29 primary, annual €240 hidden-link.

**If €29 is rejected:** Sprint 0 scope must be redefined. Options:
- Pivot pricing to €15-20 and revise billing structure accordingly (changes D138, D99)
- Reduce Sprint 0 scope to pure technical foundation (no billing UI, no conversion triggers) and treat Sprint 1 as the WTP-validated pricing launch
- Delay Sprint 0 by 1-2 weeks pending pricing restructure

**If €29 is underpriced:** Sprint 0 pricing assumptions are conservative. Annual €240 may be reconsidered. This is a growth opportunity, not a blocker — but it must be resolved before Sprint 0 commits to a checkout flow.

### What Cannot Happen

- **Sprint 0 beginning before WTP is complete.** The 6.5 days are not independent of the outcome. Running them in parallel is not parallel — it is gambling 6.5 days on an unvalidated price.
- **Treating WTP as a checkbox.** Five shallow conversations that produce no synthesis are not WTP validation. Louis must do the synthesis before Sprint 0 scope is finalized.
- **Running Sprint 0 as "validation theater" while WTP happens in the background.** The Sprint 0 exit gate ("5 beta users paid €29") should not be treated as a meaningful signal if the price was never validated externally.

---

## What This Changes in the Debate Log

| Entry | Impact |
|---|---|
| GS-WTP-priority-0630 | **Confirmed and strengthened** — WTP is not optional, it is a Sprint 0 prerequisite |
| TA-pathB-trigger-0630 | **Independent concern** — Path B trigger uses Sprint 0 primitives only if pricing is resolved; if pricing changes, trigger thresholds must be re-evaluated |
| GS-Sprint0Timing-0610 | **Partially compatible** — GS argues Sprint 0 exit should be technical, not behavioral; this paper argues Sprint 0 *entry* should require WTP validation before behavioral targets are set |
| PS-D138-0610 (hidden-link) | **Conditionally confirmed** — Hidden-link monthly-primary holds if €29 is validated; otherwise D138 must be reopened |

---

## Summary

The parallel Sprint 0 + WTP framing is seductive but false. Sprint 0 commits to pricing assumptions that WTP is supposed to validate. Louis cannot run deep user research and a 6.5-day build sprint simultaneously without degrading both. The WTP experiment must complete first — not in parallel, not as a checkbox, but as the actual input to Sprint 0 scope definition.

**Sprint 0 begins when €29 is validated. Not before.**

---

*End of Position Paper — ps-sprint0-wtp-0650*
