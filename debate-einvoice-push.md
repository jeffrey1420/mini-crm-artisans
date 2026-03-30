# ARGUMENT: E-Invoicing Must Be Day 1 — Not v2

## Challenging Decision D8

The current decision to defer e-invoicing to v2 is a critical strategic mistake. I'm arguing we flip D8: **e-invoicing (receiving at minimum) must ship at launch**.

---

## The Regulatory Clock Is Ticking — and Loud

The French government's e-invoicing mandate isn't abstract. **September 2026 is ~18 months away.** For Marc the solo plumber, this isn't a nice-to-have upgrade — it's the law. By September 2026, *every* business in France must be capable of receiving e-invoices. By September 2027, they must send via approved platforms.

This is not a future concern. It's a present revenue driver. Artisans are already feeling the pressure. When Mini-CRM launches and says "we handle your devis, factures, and relances," the first question Marc will ask in six months is: *"Can I receive e-invoices?"* If the answer is no, he churns or never converts.

**The window to capture compliant-seeking artisans is NOW — not in Q3 2026.**

---

## Private Providers Remove the "Complexity" Excuse

The main argument for deferring is Chorus Pro's API complexity. That's a false dilemma. Chorus Pro is the public portal — clunky, bureaucratic, designed for enterprises. But private Peppol-accessible providers like **Factea, Archipelia, and Tebilis** exist specifically to serve artisans and SMBs.

These providers offer:
- Simplified REST APIs (no Chorus Pro onboarding nightmare)
- Peppol network access (compliant with the 2026 mandate)
- Pricing tailored to small volumes (€5-15/month, not enterprise-tier)
- Fast onboarding — Marc could be e-invoice ready in 10 minutes

Integrating with one private provider at launch is a **2-3 sprint engineering effort**, not a 6-monthChorus Pro odyssey. This is not a technical blocker. It's a prioritization choice — and we're making the wrong one.

---

## E-Invoicing Is a Conversion Engine, Not a Feature

Consider the positioning. Mini-CRM's MVP targets Marc — smartphone-native, €29/month, overwhelmed by admin. He currently uses a mix of WhatsApp, paper notes, maybe Excel. He doesn't wake up excited about e-invoicing.

But here's what he *does* care about: **not getting left behind**. The French government sent every business owner a letter about this mandate. Marc knows compliance is coming. When he's evaluating Mini-CRM vs. the competition, the tool that says "and you're e-invoice ready on day one" wins the sale.

**Being early to compliance is a sales argument. Being late is an abandonment argument.**

---

## The v2 Trap

If we ship v1 without e-invoicing:
1. We spend 2025 acquiring users who can't comply in 2026
2. We scramble to build e-invoicing under pressure while also building v2 features
3. Our competitors (who ship Day 1) capture the compliance-motivated segment
4. We become known as "the tool that doesn't handle e-invoices properly"

The v2 deferral also signals internal ambivalence. If it's truly important, it ships with the product. If it's not important enough for launch, why is it important enough for v2?

---

## My Recommendation

**YES — e-invoicing should be a Day 1 feature.**

Minimum viable scope for launch:
- **Receive** e-invoices via one private provider (Factea or Tebilis)
- Simple inbox showing received invoices
- Basic parsing and record creation

Sending (required Sept 2027) can be v2 — but the receiving capability that the law demands in September 2026 must be present at launch.

The regulatory timeline is not a suggestion. It's a forcing function. Let's build Mini-CRM into the solution Marc needs *before* he's legally required to have it, not after.

---

## Summary
| Criterion | Day 1 E-Invoicing | Remain v2 |
|-----------|-------------------|-----------|
| Regulatory compliance | ✅ Ready for Sept 2026 | ❌ Gap at mandate |
| Engineering effort | Low (private provider) | N/A |
| Sales positioning | "Compliant from day one" | "Coming eventually" |
| Competitive capture | High — early adopters | Lost to competitors |
| Risk of deferral | Low | High — mandate missed |
