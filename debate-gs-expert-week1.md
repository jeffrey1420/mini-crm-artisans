# Position: Week 1 Expert-Comptable Outreach — Problem Framing Before Sprint 0

**Author:** Growth Strategist  
**Debate:** D139  
**Date:** 2026-03-31

---

## Assumption Challenged

**D91 / D145** — The assumption that expert-comptable feedback is most useful as *solution validation* (after a working build, Week 3) rather than *problem framing* (before any code exists, Week 1).

D91 resolved that "expert-comptable validation = Week 3 (after working build + real devis)." D145 refined this to "Sprint 0 = build only. Week 3 = working iOS/Android build + real devis = genuine feedback conversation."

Both decisions assume the expert-comptable's primary value is reacting to what Louis built. **They are wrong about what expert-comptable feedback is useful FOR.**

---

## Core Argument

**1. Week 3 feedback arrives after the most expensive decisions are already made.**

By Week 3, Louis has committed 2-3 weeks of Supabase schema design, Flutter state management, and architectural choices. Expert-comptable feedback at that point can only suggest adjustments to a solution already built. It cannot reframe the problem. Problem-framing conversations must happen before the schema is set, the UI is sketched, or the first widget is written.

**2. "Real devis" doesn't make feedback more valid — it makes it less malleable.**

The D91/D145 logic: "Week 3 = real devis = genuine feedback." But a real devis shown to an expert-comptable is a solution artifact. The expert-comptable reacts to Louis's answer, not the problem. The feedback becomes: "move that field higher," "TVA should auto-calculate," "change the invoice number format." These are polish notes, not structural insights. The real insight — *what Louis didn't know to build* — requires a conversation before any answer exists.

**3. Expert-comptables have problem-domain knowledge Louis doesn't know he lacks.**

BTP artisans invoice in specific ways. TVA auto-calculation must handle two simultaneous rates (10% + 20%). SCI clients have distinct mention requirements. Mentions obligatoires for BTP are stricter than standard. Relance timelines are legally defined in French business culture. None of this appears in a working app demo. All of it appears in a 30-minute problem-framing conversation. This knowledge directly shapes Sprint 0 decisions — what entities to model, how TVA fields behave, what validation rules to implement first.

**4. Week 1 concept conversations are zero-prep for the expert-comptable.**

There's no demo to prepare, no production data to anonymize, no mockup to build. The conversation is: "I'm building a devis/facture tool for BTP artisans. What are the top problems your clients have? What do they consistently get wrong? What causes the most relances?" This takes 30 minutes to schedule and 20 minutes to conduct. It is the lowest-friction expert validation available.

**5. Week 1 outreach does not conflict with Week 3 demos.**

This is not either/or. Week 1 = problem-framing conversations. Week 3 = working product demo with informed, specific questions. The two conversations are sequential and complementary. Louis walks into Week 3 with questions already answered and sharper questions born from Week 1. Sprint 0 is better because it was built on expert knowledge, not assumption.

---

## Why Solution-Demo at Week 3 Is the Wrong Kind of Feedback

Week 3 produces **reactive feedback** — the expert-comptable evaluates a specific solution. This is valuable for polish, not for direction. The moment Louis shows a working devis flow, he has implicitly declared his answer to the problem. The expert-comptable can only react to that answer.

The alternative — Week 1 problem framing — produces **generative feedback** before any answer exists. The expert-comptable describes the problem landscape: what artisans get wrong, where TVA errors originate, how relances actually work. Louis enters Sprint 0 with a problem hierarchy, not just a solution hypothesis.

These are fundamentally different conversations. D91/D145 chose the one that produces feedback too late to change the build.

---

## 5-Question Problem-Framing Script

*(For Louis's own expert-comptable first, then 1-2 additional expert-comptables)*

1. **"What are the top 3 problems your artisan clients have with devis and factures — not software problems, but compliance or process problems?"**

2. **"Where do artisans most often make TVA errors? Is it the rate classification, the calculation, or how it appears on the document?"**

3. **"Do any of your BTP clients invoice to SCI or property companies? Are there special mention requirements for those clients?"**

4. **"What does a correct relance process look like for an artisan with a 45-day payment term? What do most get wrong?"**

5. **"If a solo artisan could only fix one thing in their devis/facture workflow, what would make the biggest difference for their compliance?"**

---

## Why This Makes Sprint 0 Better, Not Slower

- **Sprint 0 schema is informed, not assumed.** Louis knows which TVA scenarios matter before he designs the database.
- **Feature prioritization is validated.** The expert-comptable's "biggest fix" question tells Louis what to build first, not just what he假设 matters.
- **Mentions obligatoires are correct from day one.** BTP-specific requirements surface in Week 1, not after a compliance audit at Week 8.
- **The Week 3 demo is sharper.** Louis walks in with domain-informed questions, not just "here's what we built."
- **No delay to Sprint 0.** The outreach takes 2-3 hours total (scheduling + conversation). Sprint 0 still starts on schedule. The only difference is that Louis builds on expert knowledge instead of founder assumption.

---

**Verdict on D139:** OPEN — Add Week 1 concept-only outreach before Sprint 0. Week 3 product demo remains. Sprint 0 informed by expert problem-framing. Not instead of, but before.
