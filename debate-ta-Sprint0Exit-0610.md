# Position Paper: Technical Architect
## Debate: Sprint 0 Exit Criteria for Mini-CRM MVP
**Date:** 2026-03-31
**Topic:** The correct Sprint 0 exit criteria for a solo-developer MVP

---

## Assumption Being Challenged

> "5 beta users complete the happy path without assistance" is the correct Sprint 0 exit criterion.

This is the proposed gate. I challenge it—not because beta testing is worthless, but because it is the wrong instrument at the wrong stage for a solo developer with 6.5 days of Sprint 0 scope and no secured beta pipeline.

---

## Core Arguments

### 1. Beta user dependency introduces a blocker Louis cannot control

Sprint 0 has a fixed time budget. Beta user availability does not.

- **Expert-comptable referrals** are 3–6 weeks away. Louis cannot manufacture these connections in Sprint 0.
- **Gabin's network** and **Maël's contacts** are unverified — no confirmation they are actual French artisans who match the ICP (45–55yo, active devis/factures cycle, WhatsApp-native).
- **Grinto clients** are structurally the wrong ICP — Grinto is a B2B SaaS tool; its clients are offices, not field artisans. Using them as beta users produces feedback from the wrong persona.
- **The risk:** Sprint 0 stalls or extends indefinitely because Louis is waiting on people he cannot compel or schedule.

A Sprint 0 exit criterion must gate on something Louis controls. Beta user availability is not that thing.

---

### 2. Technical exit criteria are measurable, repeatable, and not subject to social bias

"5 beta users complete the happy path" is a social criterion dressed as a product one.

- **Binary tests are enforceable.** "App installs on Android 12+ without crash within 30 seconds of launch" is a measurable, pass/fail statement. No judgment call.
- **Automated criteria scale to any reviewer.** If Louis brings in a helper, a technical gate can be evaluated consistently. A "completed without assistance" gate requires the same 5 humans to return and subjective-assess the same session.
- **Social criteria introduce noise.** A friendly beta user who wants to encourage Louis will interpret ambiguity charitably. A technical criterion does not.

**Proposed alternative technical gates (examples):**
- APK installs and launches successfully on Android 12, 13, 14 (3 devices, no crash)
- Devis creation flow completes end-to-end with test data (title, client, line items, total, PDF export) without ANR
- App passes `adb shell am start -W` launch timing on low-end hardware (≤5 seconds)
- No unhandled exceptions in Firebase Crashlytics (or equivalent) on first launch

These are Louis's to verify. He does not need to wait for anyone.

---

### 3. The happy path requires real clients and real devis — beta users without active client relationships produce theater, not validation

The Mini-CRM product handles **devis** (quotes) and **factures** (invoices) for **real artisan businesses**. The value of the product is entirely bound up in real-world use:

- A real artisan's client list (different from a test client)
- Real line items with real French business terminology
- Real total calculations that an expert-comptable will accept
- Real PDF outputs that match French legal requirements

**Beta users who are friends, family, or Grinto clients doing a "favor" will:**
- Use invented test data
- Not exercise the full edge cases a real artisan encounters (foreign client, multi-line items, currency edge cases, French legal formatting)
- Report success because they want to be helpful, not because the product works in their actual business

Real validation — whether the product solves Louis's ICP's actual problem — cannot happen without real clients. Real clients are a post-Sprint 0 outcome, not a Sprint 0 input.

---

### 4. The real Sprint 0 validation happens after shipping — real field conditions, real French SIM cards, real WhatsApp sharing on real networks

Louis's ICP (French artisans, 45–55yo) has specific characteristics that no beta session can simulate:

- **WhatsApp as the primary business communication channel** — sharing a devis via WhatsApp from an Android device is a different experience from sharing a PDF over email in a test session
- **Mobile-first, low-bandwidth conditions** — artisans work on-site, in areas with 3G or intermittent connectivity
- **Low digital literacy, high touch-dependency** — UI patterns that feel intuitive to a developer or a 28-year-old SaaS user feel completely different to a 52-year-old plumber managing his business from his phone
- **French-specific regulatory context** — devis and factures have legal requirements (mentions obligatoires, numérotation, TVA rules) that only surface in real use

**Sprint 0 cannot validate these conditions. Only production traffic validates them.**

This means Sprint 0's job is not to validate product-market fit. Sprint 0's job is to produce a build that is **technically sound enough to survive first contact with real users**. That is a much lower bar and a much clearer one: build it so it doesn't crash, doesn't lose data, and produces a usable PDF. Ship it. Then listen.

---

## What This Challenges in the Existing Decision Log

The current decision framing treats **beta user validation** as a prerequisite to shipping. This position challenges that framing at the level of Sprint 0 philosophy:

| Existing Assumption | Technical Architect Position |
|---|---|
| "We need 5 beta users to validate before shipping" | Beta validation is a Sprint 1+ activity, not a Sprint 0 gate |
| "Beta users confirm the happy path works" | The happy path requires real business context that beta users cannot provide |
| "Sprint 0 produces a validated MVP" | Sprint 0 produces a **technically deployable** artifact; validation is post-launch |

This does not mean the existing decision is wrong in absolute terms — it is wrong **as a Sprint 0 exit criterion**. For a solo developer with 6.5 days, Sprint 0 exit should produce a build, not a validated product.

---

## Proposed Resolution

**Sprint 0 exit is confirmed when:**

1. **Technical gate (required, verifiable by Louis alone):**
   - App installs on Android 12, 13, 14 without crash
   - Full devis creation flow completes with test data
   - PDF export produces a readable, correctly formatted document
   - No unhandled exceptions on first launch

2. ** Louis ships to a small real user group immediately after Sprint 0** — this is where beta engagement starts, not as a gate but as a parallel post-Sprint 0 activity.

3. **Beta user feedback is captured as a Sprint 1 input**, not as a Sprint 0 exit gate.

The key shift: **Sprint 0 proves the app works. Sprint 1 proves the app solves the right problem.**

---

## What Remains OPEN After This Position

1. **Who are Louis's first real users?** The technical gate does not solve the outreach problem. Expert-comptable intro timeline, Gabin/Maël network verification, and Grinto client ICP mismatch all remain unresolved.
2. **What is the definition of "technically sound enough"?** This position gives examples; Louis needs to codify a specific, agreed checklist.
3. **When does Louis stop adding scope to Sprint 0?** If the technical gate is clear but the scope creep is not, the gate is irrelevant.
4. **How is beta feedback collected and prioritized?** Post-Sprint 0, a framework is needed to turn field feedback into Sprint 2 scope decisions.
5. **What is the rollback plan if the shipped build fails on real hardware?** Louis needs a definition of "acceptable failure" vs. "critical bug requiring hotfix."

These are real questions. This position does not dissolve them — it relocates them to the correct sprint so they stop blocking Sprint 0.

---

*Technical Architect — Mini-CRM Research Debate*
*Sprint 0 Exit Criteria Position | 2026-03-31*
