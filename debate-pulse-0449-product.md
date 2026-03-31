# Debate Pulse 0449 — Product Strategist

## D72/D139 — Expert-Comptable Outreach Timing: Week 1 vs Week 3

---

## Current State

- **D72** (original): Expert-comptable = Phase 1 warm access
- **D139** (01:15 pulse): Expert-comptable outreach = Week 1 (Louis's own accountant = first call)
- **D139 refined (01:29 pulse)**: Growth Strategist proposed Week 1 concept-only outreach OR Week 3 product demo
- **D139 contested (01:47 pulse)**: Still OPEN — dual framing protocol added as requirement; requires Louis decision

---

## POSITION

**Verdict: Week 1 concept-only outreach is the right move. Week 3 product demo is the wrong goal.**

---

### 1. Core Argument

- **The expert-comptable's most valuable input comes before any product exists.** The expert-comptable's unique knowledge — TVA multi-taux errors they see repeatedly, SCI client handling, common devis mistakes, how BTP artisans structure payments — is *problem knowledge*, not *solution feedback*. Solution feedback (Week 3 demo) tells Louis how to improve what he built. Problem knowledge (Week 1 conversation) tells Louis whether he understood what to build in the first place. These are not the same conversation, and they don't belong in the same meeting.

- **A Week 3 product demo creates anchor bias that corrupts problem feedback.** Once Louis shows a working iOS build with a real devis, the expert-comptable shifts into *reaction mode* — "I'd change this," "the layout is confusing here," "why does it do X instead of Y?" — all solution feedback. The open-ended problem question ("what do your artisan clients consistently get wrong with devis and factures?") gets short-circuited by the artifact on the screen. The demo becomes the conversation, not the starting point for one.

- **Louis's accountant has a conflict of interest that disqualifies them from Week 3 demo validation.** Louis pays them directly. The accountant will be supportive regardless. A supportive validation is not validation — it's reassurance. The accountant conversation is only useful as a *problem-framing* exercise (what pain do you see?), not a *product endorsement* exercise. This is confirmed by D55/D91 — the conflict of interest was named but not acted on.

- **Week 3 is too late for problem knowledge anyway.** Sprint 0 begins in Week 1. By Week 3, Louis has already committed the schema design, the TVA calculator logic, the mentions légales block, and the client data model. Those decisions are made. Showing a working build to the accountant in Week 3 is showing finished work and asking for reactions to it — not using the accountant's knowledge to inform what gets built. Week 1 problem-framing can actually change what Sprint 0 produces. Week 3 feedback cannot.

---

### 2. What Assumption I'm Challenging

**Assumption being challenged:** That "validation" means "show them the product and see if they like it."

This assumption, inherited from D139's evolution, treats the expert-comptable conversation as a *demo checkpoint* — a moment to gauge reception of Louis's work. That's the wrong frame for a Phase 1 expert-comptable interaction.

The correct frame: the expert-comptable is a *context provider*. Their value is domain knowledge Louis cannot acquire elsewhere — specifically:

- Common TVA structuring errors they correct in artisan clients' annual returns
- How SCI-structured clients (rare but real) handle devis vs. standard clients
- What "accepted devis" documentation they need for their records
- Whether artisans actually follow up on relances or let invoices age silently
- Mentions légales gaps they see most often

This knowledge is only accessible before the product exists. Once Louis shows a working devis with working TVA math, the accountant reacts to his solution instead of volunteering their domain expertise. The artifact hijacks the conversation.

---

### 3. Specific Verdict

**D139 is REFINED — not toward Week 3, but toward a split-conversation model:**

| When | Who | Purpose | Deliverable |
|------|-----|---------|-------------|
| **Week 1** | Louis's own expert-comptable | Problem-framing only. No product, no mockup. | 5-question script covering TVA errors, SCI clients, relance norms, mentions légales gaps, common compliance mistakes |
| **Week 3** | 2-3 *other* expert-comptables (not Louis's) | Product demo with real devis. Social proof: "I have 5 beta users sending real devis." | Genuine feedback on solution; referral conversation if reception is strong |

**Louis's own expert-comptable is explicitly NOT a validation asset — they are a problem-knowledge asset only.** The conflict of interest (Louis pays them directly) makes them unsuitable for endorsement or referral. They are useful for one thing: filling gaps in Louis's assumptions about French artisan billing before Sprint 0 begins.

**The Week 1 conversation requires zero product. The Week 3 conversation requires working product + real beta users.**

---

### 4. Action Items

1. **Louis writes a 5-question problem-framing script before Week 1.** Questions: (1) What TVA errors do BTP artisans make most often on devis/factures? (2) How do you handle SCI-structured clients differently? (3) What mentions légales gaps do you see most? (4) Do artisans actually follow up on unpaid invoices, or let them age? (5) What would make you confident recommending a devis tool to a client?

2. **Louis explicitly frames his own expert-comptable conversation as problem research, not product demo.** The opening line: *"Je construis un outil pour les artisans qui gèrent leurs devis et factures depuis leur téléphone. Avant de commencer le développement, je veux comprendre ce que vous observez chez vos clients artisans — les erreurs récurrentes, les points de friction."* No demo. No URL. No pitch.

3. **Week 3 expert-comptable outreach targets 2-3 external accountants only.** These conversations require social proof (real beta users, real devis sent), the working product, and a purpose-built expert-comptable pricing narrative (daily anchor: *"moins d'un euro par jour ouvré"*, NOT the landing page "sans engagement" frame — per D146).

4. **The D146 dual-framing protocol is confirmed.** Expert-comptable pricing narrative = daily expense frame or competitive (Sage) frame. Landing page = consumer sans-engagement frame. These are separate documents, not the same conversation.

5. **D72/D139 status: RESOLVED — Week 1 = problem-framing only (Louis's accountant). Week 3 = product demo (external accountants). Louis's own accountant is excluded from validation/referral role permanently.**
