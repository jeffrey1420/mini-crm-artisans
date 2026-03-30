# D92 Android-First — Reconsidered in Light of U15 Elimination

**Analyst:** Growth Strategist
**Date:** 2026-03-30T20:41
**Context:** U15 (founding member offer) eliminated in Pulse 2026-03-30T20:24. "Support Prioritaire" launch framing confirmed. D92 (Android-first) was resolved in the same pulse session — but before U15 elimination was finalized.

---

## Executive Summary

**D92 should be REFLECTED, not confirmed.**

The elimination of U15 changes the GTM mechanics in ways that invalidate one key assumption underlying the Android-first validation strategy: that the Week 1 poll would be conducted among early-access users who had a reason to install. Without that cohort, "Week 1 poll validates" loses its operational meaning. The Android-first default remains directionally correct for the French artisan demographic, but the framing of what "validation" means and how it translates to Sprint 0 priorities needs sharpening.

---

## What D92 Said

D92 resolved at 20:24 (same pulse session) to **Android-first as the default**, with a Week 1 geo-targeted poll as the validation mechanism.

The debate log shows D92 went through three iterations:
1. **Initial:** iOS-first, Android Month 2
2. **Debate 98 (Growth Strategist challenge):** REOPENED — argued Android-first is correct for French artisan persona (BTP demographic is Android-heavy)
3. **Final resolution:** Android-first, Week 1 poll validates

The core argument for Android-first was demographic: French artisans aged 45-55 are Android-majority in BTP trades. The "iOS = serious business user" heuristic is a Silicon Valley assumption that doesn't survive contact with French rural demographics.

---

## How U15 Elimination Changes the Platform Calculus

### What U15 Provided (And What Replaces It)

U15 was the founding member offer: €90 lifetime deal, "Membre Fondateur" label, early-access cohort. This was the GTM mechanism that would create an initial user cohort with genuine investment in the product.

**What U15 provided for platform validation:**
- Early cohort of users with lifetime stakes who had strong incentive to install and engage
- Organic feedback loop from invested early users
- "Week 1 poll" conducted among users who had already committed (even at a discount)
- Natural install urgency: users who paid (even a small lifetime fee) are more likely to complete onboarding

**What "Support Prioritaire" provides:**
- Direct WhatsApp to Louis
- Roadmap vote
- Named credits
- Relationship benefits, not product benefits

**The gap:** "Support Prioritaire" is a retention and loyalty mechanism. It doesn't solve the acquisition problem — getting Marc to install a new app in the first place. For a free-tier user with no financial commitment, the install-to-active-use gap is larger, not smaller.

### The Validation Mechanism Is Broken

D92's resolution included: *"Week 1 geo-targeted poll confirms or denies."* But:

1. **The poll was supposed to run among early-access cohort users.** With no founding member offer, there is no natural early-access cohort at launch. The "Week 1 poll" now means: poll existing network (team + friends), not actual early users. This is sampling bias, not validation.

2. **"Validates" was always ambiguous.** Does it mean:
   - If Android ≥65% in poll → ship Android first?
   - If Android <65% → reconsider?
   
   The problem: the demographic data already says Android ≥70% in French BTP trades. The poll was never meant to discover Android vs iOS preference — it was meant to validate platform priority among engaged early users. Without an engaged early cohort, the poll can't serve its intended purpose.

3. **The "Support Prioritaire" framing adds no platform-specific signal.** Direct WhatsApp to Louis works on both platforms. Named credits work on both. These benefits don't create platform-specific install behavior that would validate Android-first.

### The Acquisition Funnel Shift

**Before U15 elimination:**
```
Founding member offer → Early cohort (lifetime stake) → Active install → Week 1 poll validates
```

**After U15 elimination:**
```
Pure free tier → Anyone can sign up → No financial commitment → Lower install completion rate → Week 1 poll has no natural sample
```

The free tier removes price friction from sign-up but adds friction to install completion. A free, no-commitment product with no urgency trigger means Marc signs up, sees the app, and... doesn't install because "I can do it later." The founding member offer (even as a lifetime deal at €90) created psychological commitment that improved install completion.

**This doesn't mean go back to U15** — the reasoning against founding member framing was sound. But it means the platform validation strategy needs to account for a longer, less committed acquisition funnel.

---

## Challenging a Prior Assumption: "The Poll Validates"

### The assumption: Week 1 poll provides a meaningful validation checkpoint

**Challenge:** This assumption conflates two different things:
1. **Platform preference** (which device Marc uses) — already known from demographic data
2. **Platform priority** (which platform to build for first) — the actual strategic question

The Week 1 poll was designed to measure platform preference among early adopters. But the strategic question — "which platform should we build first" — is not answered by a poll of early adopters who signed up for a free product. It's answered by:
- Demographic data (which device does Marc actually use in the field?) — already available, Android ≥70% in French BTP
- Competitive analysis (where are the competitors? Play Store vs App Store market saturation) — D92 mentioned this but it was never resolved
- Go-to-market channel analysis (where are the referrers? expert-comptables, groupements d'artisans — what devices do they use?)

**The real validation question is not "which platform do our users prefer" — it's "which platform gives us the best distribution leverage at launch."**

For a French artisan CRM:
- Expert-comptables (accountants who refer clients) are predominantly Windows-desktop users — they don't directly determine mobile platform
- Groupements d'artisans (trade associations) are mixed, Android-heavy based on demographic
- Word-of-mouth between artisans happens via WhatsApp, on both platforms equally

The poll was the wrong validation mechanism even when U15 existed. Without U15, it's completely disconnected from the actual strategic question.

---

## What "Android-First" Means Precisely for Sprint 0 Dev Prioritization

"Android-first" is ambiguous and has been used to mean at least three different things:

| Meaning | Description | Implication for Sprint 0 |
|---------|-------------|--------------------------|
| **A. Distribution priority** | Launch on Play Store first, App Store Month 2 | App Store listing is Phase 2 work |
| **B. UI/design priority** | Design for Material Design 3 first, adapt to iOS later | iOS UI is secondary sprint work |
| **C. Development priority** | Build and test on Android devices/emulators first | iOS build tested less frequently |
| **D. (with React Native)** | Single codebase, launch APK on Play Store first | Platform-neutral from code perspective |

**The critical dependency: D24 (PWA vs React Native) is REOPENED.**

If React Native wins (D24), meaning A/B/C are largely irrelevant — "Android-first" becomes purely a **distribution sequencing** question (Play Store launch, then App Store). If PWA wins (D11, which was the original D11, also REOPENED), then "Android-first" means the PWA is optimized for Android browsers first.

**For Sprint 0, "Android-first" must be translated into concrete actions:**

1. **If React Native:** Android APK build is the primary delivery artifact for Week 1. iOS build is secondary. Test devices: Android physical device + Android emulator. Play Store listing copy and assets prepared in Sprint 0 (not built, but planned).

2. **If PWA:** Android Chrome / Samsung Browser is the primary test target. Install prompt (A2HS — Add to Home Screen) is optimized for Android. iOS Safari is a secondary concern until Month 2.

3. **Week 1 poll is replaced by:** Install completion rate tracking (not platform preference — that's known). Day 3 and Day 7 touchpoints for users who signed up but didn't complete install. If Android install completion is <40% by Day 3, investigate and fix before iOS work begins.

---

## Recommendations

### 1. D92: Keep Android-first, but redefine "validation"

**REFLECT, not confirm.** The direction is correct. The validation mechanism is broken. Replace Week 1 poll with:

- **Install completion rate** as the primary Sprint 0 metric (target: ≥50% of signups complete install within 48 hours)
- **Day-7 active usage** as the secondary metric (target: ≥30% of installed users create first devis within 7 days)
- Platform preference is confirmed by demographic data, not by poll. The poll was always the wrong instrument.

### 2. Support Prioritaire framing needs platform dimension

Currently "Support Prioritaire" is all relationship, no product. Consider:

- Add platform-specific onboarding: "On Android, here's how to install properly" guide sent via WhatsApp after signup
- This uses the "direct WhatsApp to Louis" benefit to solve the install friction problem — a genuine value-add for the free tier
- On iOS, the same benefit exists but the install friction is different (App Store review, background refresh settings)

### 3. Remove "Week 1 poll validates" language from D92

Replace with: **"Android-first by demographic default. Install completion rate is the Sprint 0 validation metric. iOS launch follows Play Store distribution data."**

---

## Action Items for TODO.md

```
## D92 — Platform Strategy (REFLECTED)

- [ ] **Replace Week 1 poll with install completion metric** — track % of signups completing install within 48h. Target: ≥50%. D92 "poll validates" language removed from decision record.
- [ ] **Clarify D24 → D92 dependency** — React Native wins means "Android-first" is distribution sequencing only (Play Store → App Store). PWA wins means "Android-first" is both design priority and distribution. D24 resolution gates D92 Sprint 0 specificity.
- [ ] **Add Android install friction to Sprint 0 experiments** — test two onboarding flows: (A) "Install APK directly" vs (B) "Guide to Play Store install." Measure completion rate for each.
- [ ] **Expert-comptable channel device audit** — if referral channel (expert-comptables, groupements) skews iOS, Android-first may underweight the referral lever. Quick WhatsApp poll to 5-10 contacts in Week 1.
- [ ] **"Support Prioritaire" WhatsApp onboarding sequence** — day 0: "Here's how to install on Android." day 1: "Here's how to create your first devis." day 3: "Any issues?" This uses the relationship benefit to solve install friction, not just post-install loyalty.
- [ ] **Play Store review timeline** — Android B2B finance apps face Play Store moderation. Factor 3-5 day review into iOS parity timeline. Do NOT assume Play Store is faster than App Store for B2B apps.
```

---

## Conclusion

D92's Android-first direction is correct. The French artisan demographic is Android-majority. The iOS-first default was a Silicon Valley bias that didn't survive contact with reality.

But the U15 elimination exposed a weakness in how D92 was validated: the "Week 1 poll" was always a weak instrument, and without the founding member cohort, it's now completely disconnected from the actual acquisition funnel. The replacement metric should be **install completion rate**, not platform preference polling.

The bigger insight: **the platform question is downstream from the go-to-market channel question.** If the primary acquisition channel is expert-comptable referrals or groupements d'artisans, the platform priority should follow where those referrers are — not the end-user device split. That analysis was never done. It should be done in Week 1, not assumed.

D92 stands — but with a different validation framework and clearer Sprint 0 specificity tied to D24's resolution.

---

*File: debate-android-first-revisit.md — Growth Strategist, 2026-03-30T20:41*
