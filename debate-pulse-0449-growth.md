# Debate Pulse 0449 — Growth Strategist

## Sprint 0 Exit Criteria — How Does Louis Know When to Ship?

---

## The Question

Sprint 0 is 6.5 days. The scope is: client file + devis flow + offline (expo-sqlite draft-mode) + mentions légales + PDF generation + WhatsApp PDF sharing.

**What are the explicit criteria for Sprint 0 to be considered DONE?** Not "we used all the time" — specific, measurable conditions that indicate "this is good enough to ship to a first cohort of beta users." Who validates? What must work? What can be deferred?

---

## Core Argument

**1. The exit criterion is NOT "scope complete" — it's "happy path works without crashing."**

Sprint 0 delivers the first professional document Marc sends to a client. The entire value proposition collapses if that first document fails. But "works" doesn't mean "perfect." It means: a client can be created, a devis can be generated with correct TVA and mentions légales, a PDF can be produced that looks professional, and that PDF can be sent via WhatsApp. Every other path (error states, empty states, edge cases like foreign clients) can be handled post-launch. The beta cohort's job is to validate the happy path, not to find edge cases — that's what QA is for.

**2. "Draft mode" offline is not a blocker — it's an honest label that sets correct expectations.**

D9 explicitly resolved: no offline capability is NOT MVP. The debate-log language is "offline (expo-sqlite draft-mode)" — draft mode means Louis and the team know it's incomplete. Beta users who are told "this is beta, expect rough edges" will tolerate draft-mode offline. Beta users who encounter it unexpectedly will churn. The exit criterion for offline is: (a) it doesn't crash the app when there's no network, and (b) beta users are explicitly told it's draft. That's achievable in Sprint 0 without making offline a launch blocker.

**3. The validation gatekeeper is NOT Louis — it's the first 5 beta users.**

Louis is the founder. He built it. He cannot objectively assess whether it's "good enough." The exit criterion must include: 5 beta users successfully complete the core flow (create client → create devis → send via WhatsApp) without assistance. If 3 of 5 fail, Sprint 0 is not done. If 5 of 5 succeed, it's done. This is measurable, external, and removes the founder-blindness problem.

**4. What can be deferred past Sprint 0 with zero damage:**

- Offline sync conflict resolution (draft-mode is explicitly label-free)
- TVA arrondi edge cases beyond arrondi commercial (D69 confirmed €30-80/year risk, not €600)
- Email relances infrastructure (Sprint 2 scope)
- Sequential numbering for factures (Sprint 2 scope)
- Expo Push notifications (v1.1 scope)
- E-invoicing (v2 scope)

These are all explicitly in later sprints. Shipping them in Sprint 0 would cost 2-3 weeks of engineering and produce zero additional signal about whether the core value proposition works.

---

## What Assumption I'm Challenging

The assumption embedded in the sprint structure is: **Sprint 0 is done when the scope is complete.** This treats the sprint boundary as a completion marker rather than a validation marker. It assumes that shipping is a build decision, not a user decision.

The alternative assumption: **Sprint 0 is done when the first 5 beta users confirm the core flow works.** This is a validation decision. It means Sprint 0 might end early (if 5/5 succeed by day 4) or might need extension (if 3/5 fail and fixes are needed). Treating Sprint 0 as fixed-duration rather than fixed-scope is the right mental model for a 6.5-day sprint with a real product at stake.

The specific assumption I'm challenging: that "draft-mode offline" is a risk that blocks launch. It isn't — it's labeled draft, beta users will be warned, and D9 explicitly excludes offline from MVP. The risk is shipping it without disclosure, not shipping it at all.

---

## Verdict

**Sprint 0 is DONE when:**

1. **The 5-user test passes:** 5 beta users (real artisans, not the team) complete client → devis → WhatsApp PDF send without assistance. Success = 5/5 or 4/5 with documented edge case. Failure = 3/5 or worse means Sprint 0 continues.

2. **PDF output meets professional standard:** At least one beta user opens the PDF on their phone and says "this looks like something I'd send to a client" — not "this is fine" but genuine professional approval. This is a 5-minute conversation, not a formal review.

3. **Mentions légales render without legal disclaimer language:** The PDF contains correct mentions légales for a test "particulier" client and a test "professionnel" client. This is a checklist review by Louis, not a legal opinion — the mentions légales content is a template, not legal advice.

4. **WhatsApp PDF sharing works on both Android and iOS:** One test on each OS. Document opens in WhatsApp conversation. This is a 10-minute test.

5. **No crash on airplane mode (draft offline):** The app doesn't crash when network is unavailable. Data is lost — that's the draft label. Crash is the exit criterion, not data persistence.

**Who validates:** Louis + 5 external beta users (Gabin's network, expert-comptable referral network, or guerrilla approach — workshop observation per U15 protocol). Louis does NOT count as a validator of his own work.

**What must work:** Client creation, devis creation, TVA calculation, mentions légales rendering, PDF generation, WhatsApp sharing. Happy path only. Error states are logged but not fixed pre-launch.

**What can be deferred:**
- Offline data persistence (labeled draft-mode)
- Email relances (Sprint 2)
- Sequential numbering for factures (Sprint 2)
- Expo Push notifications (v1.1)
- E-invoicing (v2)
- Expert-comptable referral network (Phase 1, U12)

**What cannot be deferred:** The happy path must not crash. A beta user who gets a white screen when they tap "envoyer" is not a "draft mode" problem — it's a launch blocker. That's the bar.

---

## Action Items

1. **Define the 5-user test protocol before Sprint 0 starts:** Select 5 artisans in Gabin's/Maël's network. Send them the APK via TestFlight/instalation profile. Give them one task: "Create a client, create a devis, send it to yourself via WhatsApp." 30 minutes of their time. Document what happens.

2. **Add "draft mode" disclosure to the app's first-launch screen:** One sentence: "Le mode hors-ligne est en version draft. Vos données ne seront pas sauvegardées sans connexion." This is the disclosure that makes draft-mode acceptable for beta.

3. **Create a PDF review checklist:** Louis reviews one devis PDF for a "particulier" client and one for a "professionnel" client against the mentions légales checklist (SIRET, RCS, TVA intracom if applicable). Takes 15 minutes. Must pass before launch.

4. **Budget 1 day post-Sprint 0 for bug fixes based on 5-user test:** Sprint 0 ends when the test passes — but if 2 of the first 5 users hit a crash, 1 day of hotfixes before official "ship" is the right call, not "Sprint 0 is done, ship it anyway."

5. **Set the launch bar for Louis:** "Ship" means the APK is distributed to beta users and the landing page has a working signup. It does NOT mean "all scope is complete." The scope is a plan, not a contract.

---

*Debate by Growth Strategist subagent — session gs-D155-pulse-0449*
*Source: /data/workspace/mini-crm-research/debate-log.md (read through 2026-03-30T17:03)*
