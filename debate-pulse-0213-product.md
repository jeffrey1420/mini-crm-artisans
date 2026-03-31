# Product Strategist Position Paper — PS-D147
**Pulse:** 01:59 | **Date:** 2026-03-31

---

## Position: Sprint 0 Scope — Cut the Architecture, Ship the Document

### The Challenge to the Prior Debate

The prior debate treated "simplicity-first" (D12 landing page) and "competence-first" (everything-validated-before-launch) as competing Sprint 0 philosophies. This is a false dichotomy. The real choice is not "simple product vs. complex product." It is: **are you building a document tool or an activation machine?**

Sprint 0 should be the former. Path B mechanics, dual-path conversion architecture, WhatsApp Business API — these are all features of an activation machine. Sprint 0 is not ready to be that machine. It has zero users. You cannot validate a 45-day usage trigger without users. Building the activation infrastructure before you have anyone to activate is cargo-cult product management.

The assumption I challenge: **that Sprint 0 must establish the conversion architecture for both Path A and Path B simultaneously.** It should not. Ship Path A cleanly. Let real usage tell you whether Path B is a real segment.

---

## The 3 Maximum Deliverables for Sprint 0 (5 Days, Solo Dev)

**1. Core Devis Flow (3 days)**
Supabase schema (client, devis, TVA per-line with arrondi commercial, sequential numbering), React Native client creation + devis creation screens, expo-print PDF output, native share sheet (WhatsApp/email), plain text mentions légales embedded directly in PDF string — no template engine. This is the entire product on Day 1.

**2. Auth + Offline-Capable (1.5 days)**
Supabase Auth (email/password), AsyncStorage caching of last-fetched client/devis list, retry queue for failed creations. View-only offline — artisan can browse cached documents without signal. No offline editing in Sprint 0.

**3. Expo Push Skeleton (0.5 days)**
Notification permission prompt on first devis send, server-side notification trigger (first accepted devis → push to artisan), notification infrastructure in place but empty. No WhatsApp in Sprint 0.

**Buffer: 0 days built in. This is the honest floor.**

---

## What Gets Cut

| Cut | Reason |
|-----|--------|
| **WhatsApp Business API** | Meta Business Verification alone takes 2-14 days. Louis has no verified Meta Business Manager. Sprint 0 ends before approval. Premium content to send doesn't exist yet. Expo Push only. |
| **Path B mechanics** | D110's 45-day/7-job/5-client trigger cannot be validated without users. This is a v1.2 decision. Path A only in Sprint 0. |
| **Dual-path architecture** | D96 designed two conversion flows before any user exists. Ship Path A (limit-hit on formal devis) as single flow. Real usage reveals whether Path B is real. |
| **Mentions légales template engine** | Handlebars/Nunjucks is over-engineering for Sprint 0. Static strings in the PDF generation function handle all 4 client types at this stage. 8 combinations (devis + facture) = Sprint 2. |
| **expo-sqlite** | D86 reversed D81's offline-first. AsyncStorage + retry queues are sufficient for Sprint 0. expo-sqlite deferred to v1.2. |
| **Full push implementation** | Expo Push skeleton only — trigger, permission, infrastructure. Actual push content in v1.1. |
| **Expert-comptable prep** | D139 correctly moved this to Week 3. Sprint 0 = build only. |

---

## Sprint 0 Timeline Recommendation

**Day 1:** Supabase project setup (EU Frankfurt), schema commit (clients, devis, line_items, TVA calculator), auth setup
**Day 2:** React Native client list + devis list screens, Supabase integration
**Day 3:** Devis creation flow, TVA per-line calculator, expo-print PDF generation, native share sheet
**Day 4:** Mentions légales as static strings (not template engine), sequential numbering, offline-capable caching, retry queues
**Day 5:** Auth flow completion, Expo Push skeleton, notification permission, real device testing (Android)

**Floor: 5.5 days.** If mentions légales gate (D142 — Louis's real legal text committed to git) is not met before Sprint 0 starts, add 0.5 days and use plain text placeholder.

**Pre-sprint gates required:**
1. Louis commits `legal/mentions-legales.ts` with real business data (not TODO comments)
2. Louis confirms Supabase EU project is live and accessible

---

## The Assumptions I'm Challenging

1. **"Simplicity-first and competence-first are mutually exclusive in Sprint 0 planning."** They are not. A simplicity-first Sprint 0 is also a competence-first Sprint 0 — if you cut the right things. The product that emerges from this Sprint 0 is simple because it does one thing: lets Marc create and send a professional devis from his phone. That is both simple AND competent.

2. **"Path B must be designed in Sprint 0."** D110 and D141 are designing conversion mechanics for users who don't exist. You cannot know the soft limit threshold for Path B artisans without observing Path B artisans. The 45-day trigger is an assumption, not a finding. Ship Path A. Watch for Path B signals. Design Path B in v1.2 with real data.

3. **"WhatsApp Business API belongs in Sprint 0 because Path B needs it."** WhatsApp Business API cannot ship in Sprint 0 — verification alone blows the timeline. And Path B's retention mechanism (D141) should be a "stay in touch" digest, not WhatsApp, because WhatsApp is too invasive for dormant users receiving product marketing. Path B digest → in-app or email. WhatsApp → v1.1 at earliest.

---

*Product Strategist — Pulse 0213*
