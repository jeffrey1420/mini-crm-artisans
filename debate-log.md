# Mini-CRM Debate Log

## Pulse 2026-03-30T10:58 — Three New Debates

---

## Debate 19: Landing Page — Simplicity-First vs ROI-First

**Challenge:** Previous Position A (ROI/emotional hook) swung toward "Vos clients vous payent en 48h" and emotional pain framing. Product Strategist challenges this assumption.

### Product Strategist — Simplicity-First Case

**Core argument:** ROI framing invites skepticism and comparison shopping. "Gagnez 2h/semaine" triggers mental calculation: *"Est-ce que je perds vraiment 2h par semaine?"* — you've started a sales conversation you can't win on a landing page. You're attracting analytical buyers who will comparison-shop, not sign up today.

**Why simplicity-first wins the acquisition funnel:**
1. "Simple comme WhatsApp" kills the real objection (fear of learning new software) before it forms
2. It selects for early adopters without asking them to admit they're early adopters
3. Simplicity creates conditions for the ROI story to write itself — inside the product, not on the landing page
4. The best SaaS onboarding is one where the user discovers value themselves. Over-promise ROI on landing page + 15-minute setup = broken contract

**Proposed headline + subheadline:**
> **Headline:** Vos devis et factures, sans vous prendre la tête.
>
> **Subheadline:** Pas de formation. Pas de tableau comparatif. Vous envoyez votre premier devis en 5 minutes, depuis votre téléphone.

**Rationale:** "Sans vous prendre la tête" = WhatsApp signal in plain French. Addresses cognitive ease, not feature power. "Pas de formation. Pas de tableau comparatif." attacks competitor comparison fear. "Depuis votre téléphone" = mobile-first reassurance. Zero ROI promises — the value prop is friction removal.

**Verdict on U3/U6:** RESOLVED — Simplicity-first wins. U3 = Simplicity framing. U6 = headline above.

---

## Debate 20: Home View — A Third Option

**Challenge:** Both Dashboard-first and Timeline-first are solving the wrong problem. Technical Architect challenges both premises.

### Technical Architect — Job-First Home View

**Core argument:** Both sides assume the home view is about organizing administrative work. Dashboard-first = "what admin tasks are overdue?" (project manager thinking). Timeline-first = "what happened with this client?" (CRM thinking). Neither addresses the actual cognitive state of an artisan at 7:30 AM before heading to a job site.

**The third option — Active Job Card as Home Anchor:**

The home view should answer one question: *"What am I working on right now?"*

The UI renders a single **Active Job Card** containing:
- Job title and address (the physical location he's going to)
- Client name and phone (one-tap call)
- Job type and description (quick context refresh)
- Today's plan/notes
- Status indicator (en cours, en pause, pending materials)
- Quick actions: Mark complete, Add note, View quote, View invoice

Below: **Upcoming Jobs Strip** (next 3 jobs by scheduled date) + **Quick stats bar** (de-emphasized counts for devis en attente / factures impayées that he can tap but aren't surfaced as alarms)

**Why "what job am I working on right now" beats "what admin tasks are overdue":**
1. Dashboard-first surfaces administrative anxiety during work time — when Marc needs to stay focused on the physical task
2. The mental model mismatch: Dashboard assumes Marc's primary job is managing his business. It isn't. His primary job is doing the physical work at hand.
3. Debate 16 Addendum B correctly identified guilt-driven urgency creates avoidance. But the solution isn't Timeline (passive archive). The solution is removing guilt triggers from the home view entirely. Show the job, not the admin backlog.
4. Real-world analogue: When an artisan arrives at a job site, they don't check voicemail and see outstanding invoices. They look at their work order and notes. The app should replicate this.

**Data model implications:**
- `jobs` table needs `status` (pending / in_progress / completed), `scheduled_date`, `updated_at`
- Home query: most recently updated `in_progress` job, or most recent `pending` with today's scheduled date
- Single-tenant: no multi-user complications at launch

**Verdict on U4:** RESOLVED — Job-first home view. Dashboard cards move to secondary "À suivre" tab.

---

## Debate 21: E-Invoicing — Regulatory Pressure ≠ Launch Urgency

**Challenge:** Previous debate treated U5 as a technical question (2-3 sprints vs 6-8 sprints). Growth Strategist reframes it as a go-to-market question.

### Growth Strategist — v2 E-Invoicing Case

**Core argument:** Regulatory pressure ≠ buy-side urgency at launch. The 2026 mandate requires artisans to RECEIVE e-invoices (the sender bears the obligation). The artisan can receive via: Chorus Pro portal (free), a free tier of any PEPPOL-accessible tool, or their accounting software. The outbound e-invoicing obligation (sending) comes later and phases in by company size.

**Why Day 1 e-invoicing is a positioning trap:**
1. Clean MVP pitch: "Create professional devis and invoices in minutes. Get paid faster." E-invoicing at launch adds compliance narrative that: confuses core value prop, makes us look like we're building for B2B SaaS accountants, introduces fear/urgency framing that creates friction in trial sign-up
2. We want desire, not fear, at top of funnel
3. Provider lock-in before product-market fit: committing to Factea or Tebilis before we understand our own users means we can't evaluate which provider truly serves our users' needs

**Why v2 is better growth:**
1. Learn user behavior first: in 30-day trial window, what matters for conversion is devis creation speed, whether artisans understand customization, whether facture → relance flow reduces pain, whether they trust us. E-invoicing onboarding adds complexity without visible value until they're already habituated
2. Clean acquisition funnel: "Gagnez 2h/semaine" attracts the wrong buyer. Positioning around compliance attracts the wrong buyer too — someone who sees this as a compliance tool, not a daily workflow tool
3. The regulatory deadline is real but the urgency is for large companies sending to artisans — not for the artisan evaluating a devis/facture tool for their own workflow

**U2 framework (for when we do e-invoicing in v2):**
- API quality: REST preferred, clear docs, sandbox environment
- Compliance scope: Must support Peppol/PEPPOL access for French e-invoicing mandate
- Pricing: Per-invoice or flat monthly, artisan-friendly (< €15/month for solo)
- Integration complexity: Must be embeddable in Nuxt flow without redirecting to external portal
- Candidates: Factea (has API + Peppol, good dev docs), Tebilis (similar, slightly cheaper), Archipelia (more accounting-focused, less artisan-native)
- Recommendation: Evaluate Factea first — best API docs, already Peppol-connected, solo artisan pricing

**Verdict on U5:** RESOLVED — v2 e-invoicing. Decision D8 stands.

---

## Previous Debates (Summary)

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D1 | Positioning | Kill "CRM" — devis, factures, relances | 2026-03-30 |
| D2 | MVP scope | 4 features only | 2026-03-30 |
| D3 | Primary persona | Marc — solo smartphone-native | 2026-03-30 |
| D4 | Stack | Single managed Postgres | 2026-03-30 |
| D5 | Pricing | €29/€49/€79 tiered | prior |
| D6 | Trial | 30 days | prior |
| D7 | Architecture | Nuxt 3 + OVH managed Postgres | 2026-03-30 |
| D8 | E-invoicing | v2 feature (D8 stands after Debate 21) | 2026-03-30 |
| D9 | Not MVP | No Kanban, no multi-user, no offline, no API keys | 2026-03-30 |
| D10 | Buyer trigger | "Admin pain" not "CRM need" | 2026-03-30 |
| D11 | PWA vs Native | PWA first, native within 6 months | 2026-03-30 |
| D12 | Landing page | Simplicity-first (Debate 19) | 2026-03-30 |
| D13 | Home view | Job-first, not Dashboard or Timeline (Debate 20) | 2026-03-30 |
| D14 | E-invoicing timing | v2 (Debate 21) | 2026-03-30 |
| U1 | Real discovery | Still open — watch 10 artisans |  |
| U2 | E-invoicing platform | Resolved: Factea first when v2 (Debate 21) | 2026-03-30 |

---

*Last updated: 2026-03-30T10:58*
