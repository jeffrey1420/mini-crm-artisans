# Position Paper: Challenge to D110 Deferral — Path B Soft Limit Trigger

**Date:** 2026-03-31T04:17  
**Author:** Product Strategist (PS-D154)  
**Challenge to:** TA-D152 (Path B trigger deferred to v1.2)  
**Status:** OPEN — Louis decision required

---

## 1. The Deferral Was Premature

TA-D152's argument for deferring D110 to v1.2 rests on two pillars:

1. **Sprint 0 is at capacity** — no room for Path B trigger work
2. **"Observe via analytics first"** — gather usage data before designing the trigger

Both arguments collapse under scrutiny.

### Sprint 0 Capacity Is a Scoping Choice, Not a Physical Constraint

Sprint 0 has been cut four times:
- WhatsApp Business API removed (was in scope, now deferred to v1.1)
- Dual-path onboarding deferred (merged into single path)
- Mentions légales simplified (was more comprehensive, cut down)
- E-invoicing removed entirely (v2 feature)

Each cut reduced what Louis ships. The pattern is consistent: when something is hard or uncertain, it gets deferred. Path B trigger is the latest in this pattern. The question is not whether Sprint 0 *can* accommodate it — it's whether Louis *wants* to prioritize it.

### "Observe via Analytics First" Is Backwards Logic

Analytics observe behavior. They do not create conversion. This is the critical distinction TA-D152 missed:

- Analytics can tell you: "Path B users log 3.2 jobs on average before churn"
- Analytics cannot tell you: "Which threshold triggers an upgrade prompt"
- Analytics cannot create: the prompt itself, the re-engagement moment, the upgrade offer

The argument "observe via analytics before designing the trigger" confuses *discovery* with *conversion*. We already know the problem: Path B users (verbal-agreement artisans) churn silently at 45 days with no upgrade prompt. We don't need analytics to tell us this is the problem. We need to design the solution.

Waiting for analytics to tell us "when" to prompt is like waiting for a hungry person to tell you exactly what food they want before cooking. The person is already hungry. The food is already needed.

---

## 2. Path B Is 40-50% of the Target Market

The mini-CRM's target persona is the **solo artisan** who:
- Does physical trade work (plumbing, electrical, construction)
- Operates on verbal agreements and informal deals
- Does not send formal written devis — jobs are agreed by phone or in person
- Tracks work with notebooks, WhatsApp texts, or memory

This is not a niche. This is a substantial segment of French sole traders and micro-enterprises. The GTM document identifies this as a primary segment, not an edge case.

**Launching without a Path B conversion mechanism means:**
- 40-50% of target users arrive at the product
- They log jobs (it's useful even without devis)
- They never hit Path A (no accepted devis = no facture)
- At 45 days, they churn — silently, no upgrade prompt, no re-engagement
- Louis ships an MVP that only converts Path A users

This is not an edge case failure. It is a systemic conversion gap covering nearly half the market.

---

## 3. The Minimum Viable Path B Trigger Is Not 1 Day of Work

TA-D152's unstated assumption is that Path B trigger = complex WhatsApp Business API integration. This conflates the mechanism with the trigger.

**What Path B trigger actually requires:**
1. A threshold flag: "user has logged N jobs with client contact info captured"
2. An in-app banner: "Vous utilisez [App] pour suivre vos interventions. Envie d'organiser tout ça? Découvrez [Plan]."

That's it. No WhatsApp. No Business API. No external integration.

**The threshold flag is a database query:**
```sql
SELECT COUNT(*) FROM jobs
WHERE user_id = :user_id
AND client_id IS NOT NULL
AND client_phone IS NOT NULL OR client_email IS NOT NULL
AND created_at > :thirty_days_ago
```

If count >= threshold → set `user.upgrade_flag = 'path_b_triggered'`

**The in-app banner is a UI component:**
- Shown once, dismissible, not shown again for 60 days
- Links to upgrade/plan comparison page
- No WhatsApp, no push notification, no external API

**Implementation estimate:** 2-4 hours, not 1 day. This is not a Sprint 0 blocker.

---

## 4. What Louis Must Decide

Louis must answer one question:

**What is the threshold?**

Options:
- **Option A:** 3 jobs logged + client contact info (phone or email) captured → trigger fires
- **Option B:** 5 jobs logged + client contact info captured → trigger fires
- **Option C:** 30 days of active usage + at least 1 job logged → trigger fires

The specific number is less important than **committing to a number**. The 3-job threshold is reasonable but unvalidated. A 5-job threshold is more conservative. A time-based threshold (30 days) is the most conservative.

**The decision Louis must make:**
> "Path B trigger fires when: [threshold value] is reached. Threshold value = [3 / 5 / 30 days]."

That's it. That's the decision. No WhatsApp. No complex architecture. One number.

---

## 5. What Is NOT Being Proposed

This position paper does NOT propose:
- WhatsApp Business API integration (deferred to v1.1)
- Push notifications (deferred)
- Automated follow-up messages (deferred)
- Any external integration or API

What IS being proposed: **a threshold flag + in-app banner**, nothing more.

---

## 6. The Risk of Not Shipping a Path B Trigger

If D110 remains deferred to v1.2:

| Month | Path A Users | Path B Users |
|-------|-------------|--------------|
| Month 1 | Sign up, create devis | Sign up, log jobs |
| Month 1.5 | Create accepted devis | — |
| Month 2 | First facture created → trigger | Churn silently |
| Month 2.5 | Conversion prompt shown | Gone. No prompt. No re-engagement |
| Month 3 | Path A conversion happens | — |
| Month 6 | Cohort data shows 45% Path B churn | — |

Louis launches with a product that converts Path A users and loses Path B users invisibly. Analytics will later confirm "40-50% of users churned at 45 days." But by then, v1.2 is already scoped and the fix is still not designed.

The 45-day churn window is the conversion opportunity. Missing it at launch is not recoverable via analytics.

---

## 7. Proposed Resolution

**Add to Sprint 0 (non-critical path):**
- Threshold flag logic: `jobs.count >= 3 AND client_contact_exists = true` → `user.upgrade_flag = 'path_b'`
- In-app banner component: shown once, dismissible, 60-day cooldown

**Louis decision required:**
> Decision D110: Path B trigger threshold = **[3 / 5 / 30 days]**?

**Note:** WhatsApp Business API remains deferred to v1.1. This paper does not revisit that deferral.

---

## Summary

| Argument | TA-D152 Position | Product Strategist Response |
|----------|-----------------|---------------------------|
| Sprint 0 capacity | At capacity | Non-critical-path item, 2-4 hours, not a blocker |
| Observe via analytics first | Defer to v1.2 to gather data | Analytics observe, they don't convert. We know the problem. Design the solution. |
| Path B = WhatsApp | Trigger = WhatsApp API | Trigger = threshold flag + in-app banner. No external API. |
| 3-job threshold unvalidated | Wait for data | Every threshold is unvalidated at launch. Ship a reasonable default. |
| Scope cuts pattern | — | WhatsApp removed, dual-path deferred, mentions légales cut, e-invoicing removed. Each cut reduced what Louis ships. |

**Status: OPEN — Louis decision required on threshold value (D110).**
