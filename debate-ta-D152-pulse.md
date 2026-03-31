## Debate TA-D152: Path B Trigger Belongs in v1.2, Not Sprint 0

### Technical Architect — Sprint 0 Is Maxed Out. Path B Instrumentation Is v1.2 Work.

**Assumption challenged:** GS-D146-3G's assertion that "we won't see Path B signals without an in-app trigger" — and the corollary that Path B (~40-50% of target market) requires immediate trigger infrastructure in Sprint 0.

---

**Core arguments:**

1. **Sprint 0 has exactly 3 deliverables, already at capacity.** PS-D147 established the hard ceiling: Core Devis Flow (3 days), Auth/Offline-Capable (1.5 days), Expo Push Skeleton (0.5 days). Total = 5.0 days. This is not negotiable — it IS the sprint. GS-D146-3G's proposal adds a fourth deliverable: Path B trigger infrastructure. That is scope creep, full stop. The sprint does not have capacity for it.

2. **"Path B trigger" is not one thing — it is five things, none of which are free.** GS-D146-3G says "Sprint 0 needs only a threshold flag (30-day + 3 jobs) and a simple in-app banner." This undercounts the actual work. To ship Path B trigger in Sprint 0, you need: (a) event instrumentation to track "job logged" events server-side, (b) threshold computation logic (30-day clock + 3-job counter), (c) upgrade prompt UI component, (d) the prompt trigger condition wiring, and (e) test scenarios for BOTH Path A and Path B simultaneously. Minimum: 1 full day not currently budgeted. Maximum: 2 days if anything goes wrong. That blows the 5-day sprint before day 1 ends.

3. **The assumption "we won't see Path B signals" is wrong. We will see them via analytics without any in-app trigger.** This is the central flaw in GS-D146-3G's argument. Path B artisans who never reach Path A's 3-accepted-devis threshold will still USE the Free tier. They will log jobs, create clients, send devis. All of this generates server-side events in Supabase — `devis.created`, `client.created`, `job.logged`. We can query this data directly in the Supabase dashboard or via a simple analytics pipeline. We do NOT need an in-app upgrade prompt to observe Path B behavior. The trigger IS NOT the observation mechanism. Analytics are the observation mechanism. The trigger is a conversion mechanism. These are different things.

4. **"Path B is 40-50% of target market" is an unvalidated estimate, not a finding.** Where does this number come from? It appears in the debate log as a given, but it has not been derived from user research, market sizing, or any empirical data. Louis has not interviewed 40 Path B artisans. The number is plausible — verbal workflows are common among French artisans — but "plausible" is not "validated." Building Sprint 0 infrastructure for an unvalidated segment is spending real development days on a hypothesis. If the number is wrong and Path B is actually 15% of users, we have wasted 2 days of Sprint 0 on infrastructure for a minority use case.

5. **"Rough thresholds are valid for learning" — true, but you don't need to BUILD the trigger to START learning.** GS-D146-3G says "30-day + 3 jobs is directionally sound. Perfect numbers aren't needed to start measuring." I agree — but the "start measuring" part does not require building an in-app trigger. You start measuring by instrumenting the analytics pipeline (which is free with Supabase), observing behavior for 30-60 days post-launch, and then building the trigger in v1.2 with real cohort data. The correct sequence is: (1) launch with Path A only + analytics, (2) observe Path B behavior in production for 4-6 weeks, (3) design Path B trigger with real thresholds in v1.2. GS-D146-3G has the right goal (learn fast) but the wrong implementation (build trigger before you have data to calibrate it).

6. **Building the trigger before having data to calibrate it is backwards.** The trigger design (30-day + 3 jobs vs. 45-day + 5 jobs vs. something else) is a calibration question. Calibration questions are answered with data, not intuition. If you build the trigger in Sprint 0 with a guess at thresholds, you will either (a) fire the prompt too early (annoying users who haven't experienced value) or (b) fire it too late (missing the conversion window). Neither is acceptable. Better to wait 4 weeks, observe the actual distribution of job-logging frequency among Free-tier users, and build a trigger calibrated to real behavior. This is basic cohort analysis — it costs nothing extra and produces better results.

7. **GS-D146-3G's "competitive risk" argument applies equally to every feature.** "A competitor designing for verbal workflows from the start will own that segment." True — and a competitor with a rock-solid Path A devis flow will win every formal-devis artisan first. Path A is NOT a minority segment that can be ignored. It is the primary segment for v1. Dominating the formal-devis segment at launch is worth more than spreading thin across both segments with mediocre execution on either.

---

**Verdict:**

Sprint 0 must NOT include Path B trigger infrastructure. The unresolved debate at D146-3G should be closed with:

- **Path B trigger deferred to v1.2.** Sprint 0 ships Path A conversion flow only.
- **Path B observation begins at launch via Supabase analytics.** No in-app trigger required. Server-side event tracking for `devis.created`, `client.created`, `job.logged` is free and immediate.
- **Path B threshold calibration:** After 4-6 weeks of production data, Louis designs Path B trigger in v1.2 sprint planning with real cohort numbers.
- **Path B upgrade prompt:** Built alongside the calibrated trigger in v1.2, not Sprint 0.

**What this resolves:**
- Sprint 0 stays at 5.0 days with 3 confirmed deliverables.
- Path B is not ignored — it is observed.
- Trigger is not built on guesses — it is built on data.
- Louis makes one decision instead of three: confirm Path B deferral to v1.2.

**The single most important Louis decision this debate is blocking:** Sprint 0 scope. Until GS-D146-3G's Path B proposal is resolved, Sprint 0 scope is technically unconfirmed. Close this debate to unblock the sprint.
