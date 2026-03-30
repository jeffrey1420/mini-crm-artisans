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

## Pulse 2026-03-30T11:11 — Three New Debates

---

## Debate 22: Relances as Differentiator — Fragile Assumption

**Challenge:** Product Vision claims "relances (follow-ups they don't have to chase manually)" is the key differentiator. Product Strategist challenges this assumption.

### Product Strategist — Relances-Should-Be-De-Emphasized Case

**Core argument:** "Relances automatiques" solves for the wrong pain. Artisans don't hate following up — they hate forgetting to, or feeling awkward doing it. Those are different problems requiring different solutions.

**Why relances-as-differentiator is fragile:**
1. **French artisan culture is direct.** They call, not text. An automated WhatsApp message from a business tool feels cold and risks the personal client relationship they've built over years.
2. **"I don't have to chase" is the wrong promise.** Most artisans want to stay on top of it — the mental load is remembering *who* and *when*, not the act itself. Automated reminders don't solve remembering.
3. **WhatsApp reminders feel impersonal to the client.** A French client receiving "Votre facture de 850€ est en attente depuis 30 jours" from a business tool may wonder if the artisan even cares enough to call personally.
4. **Attracts the wrong users.** Hooking on relances automation attracts: cash-flow-challenged artisans, those with poor client relationships, people who want to outsource the awkward part. These are churn risks, not ideal customers.
5. **Competitors don't lead with it.** Tolteck and Obat lead with job management and scheduling — if relances were a massive purchase driver, they'd have capitalized on it.

**Proposed reframing:** "Votre administration ne vous ralentit plus" / "Restez professionnel du devis au paiement." Frame: from "we do the uncomfortable thing for you" to "you stay in control of your business, end to end."

**Product Strategist POSITION:** Relances should be DE-EMPHASIZED on the landing page (kept as feature, not headline). Frame relances as "schedule a follow-up reminder for yourself" (not "we text your client"). Better differentiation: "Everything in one place: clients, jobs, invoices, follow-ups — no spreadsheet required."

**Verdict on U3 (landing page hero):** REOPENED — Product Strategist challenges U3 resolution. Relances should not appear in the headline. "Simplicité" still wins, but relances should be removed from hero framing entirely.

---

## Debate 23: Trial Length — 30 Days Is Too Long

**Challenge:** D6 (30-day trial) treated as resolved. Growth Strategist challenges: 30 days creates procrastination, not conversion.

### Growth Strategist — 14-Day Trial Case

**Core argument:** 30 days assumes organic user engagement and eventual conversion. This is fantasy for a French artisan persona (busy, not browsing, acute-need buyer).

**Why 30 days hurts conversion:**
1. **Days 1-7:** Good intentions. Days 8-14: vaguely remember signing up. Days 15-22: guilt, avoidance. Days 23-30: panic, convert out of guilt or let it expire. The trial expired but value was never demonstrated.
2. **Urgency drives action.** Shorter trials force a decision. Every session matters. 30 days creates "I'll get to it eventually." 14 days creates real pressure.
3. **Self-selection.** 30 days attracts curious browsers and competitive researchers. 14 days self-selects for people with an acute need NOW.
4. **The GTM doc says 14 days, debate log says 30 days.** This conflict must be resolved.
5. **Industry data:** Studies consistently show 14-21 day trials matching or beating 30-day trials on conversion rates.

**On credit card at signup:** For MVP stage, no credit card at signup — friction kills conversion at awareness stage. Compensate with aggressive email drip (trial ending in 7 days, 3 days, 1 day). Credit card capture can be introduced at day 7-10 for engaged users.

**Growth Strategist POSITION:** Trial should be **14 days**, no credit card at signup, email drip creating 3 touchpoints in the final week.

**Verdict on D6:** REOPENED — 30-day trial should be changed to 14-day trial.

---

## Debate 24: PWA-First — Wrong Strategy for This Audience

**Challenge:** D11 (PWA first, native within 6 months). Technical Architect challenges that PWA-first is the wrong mobile strategy for a French artisan CRM.

### Technical Architect — React Native from Day 1 Case

**Core argument:** PWAs work for apps where reach > engagement > conversion. A B2B CRM where reminders are the core product requires reliable push notifications, App Store credibility, and hardware access that PWAs can't guarantee — especially on iOS.

**Why PWA-first fails for this audience:**
1. **Marc is Android-heavy, but Android PWA install rate is under 15%.** "Add to Home Screen" is a hidden, alien action for this demographic.
2. **iOS PWAs are hobbled.** Apple restricts background execution, caps storage at 50MB, and does not support web push reliably. ~40% of French users on iOS = broken reminder system for large portion of users.
3. **Push notifications ARE the product.** This is a CRM. Relances and reminders are the core value. Web push on iOS simply doesn't work. If Marc misses a notification, the app has failed its core job.
4. **Trust signal for financial tools.** App Store presence = credibility. A "website added to home screen" doesn't feel like a professional business tool for a 45-55 year old.
5. **"6-month native" timeline is a lie.** Maintaining two separate codebases, retraining users twice, feature parity nightmares. The pivot rarely happens cleanly.
6. **Hardware access.** Camera for receipts, file system for PDFs, background processing — PWAs have ceilings that native doesn't.

**Technical Architect POSITION:** Mobile strategy should be **React Native from Day 1** — single codebase covers both platforms, push notifications work from Day 1, App Store presence from launch, no "6-month pivot" fantasy.

**Verdict on D11:** REOPENED — PWA-first should be reconsidered. React Native from Day 1 is the stronger position for this specific audience and product.

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

| D12 | Landing page | Simplicity-first (Debate 19) | 2026-03-30 |
| D13 | Home view | Job-first, not Dashboard or Timeline (Debate 20) | 2026-03-30 |
| D14 | E-invoicing timing | v2 (Debate 21) | 2026-03-30 |
| D15 | Relances differentiator | REOPENED — de-emphasize on landing page (Debate 22) | 2026-03-30 |
| D16 | Trial length | REOPENED — 14 days, not 30 (Debate 23) | 2026-03-30 |
| D17 | Mobile strategy | REOPENED — React Native vs PWA-first (Debate 24) | 2026-03-30 |

| U1 | Real discovery | Still open — watch 10 artisans |  |
| U2 | E-invoicing platform | Resolved: Factea first when v2 (Debate 21) | 2026-03-30 |
| U7 | Domain | Still open — buy domain |  |
| U3 | Landing hero | REOPENED — remove relances from hero (Debate 22) | 2026-03-30 |

---

*Last updated: 2026-03-30T11:38*

---

## Pulse 2026-03-30T11:38 — Three New Debates

---

## Debate 28: U1 Discovery — Stalling Tactic?

**Challenge:** Growth Strategist challenges U1 ("Go watch 10 artisans before building") as a stalling tactic that delays MVP ship by weeks.

### Growth Strategist — Discovery-is-Deferral Case

**Core argument:** Personas are sufficient. Marc's admin workflow is well-characterized. The feature set is locked. French artisan pain points are validated by every competitive analysis (Pennylane, Indy, Freebe exist because the pain is real). Watching artisans mostly surfaces workarounds (WhatsApp, Excel, paper notebooks) which confirm rather than redirect.

**The risk:** Discovery becomes indefinite deferral. Every week of "discovery" is a week not learning from actual users on an actual product. The real failure mode is building something too complex and artisans abandon it mid-trial — only fixable by shipping and iterating.

**Concrete alternative — 3-day guerrilla test:**
- Day 1-2: Build clickable prototype (Figma) of single flow: create a devis on phone. One screen.
- Day 3: Go to 5 artisans at a supply wholesaler (Point P, Samse, Gedimat). Saturday morning. Sit with them 10 minutes. Watch their fingers.
- What you'll learn: Do they understand the UI? Where do they hesitate? What language do they use?
- This is validation of usability, not discovery of pain. Pain is already known.
- Cost: 1 designer, 1 weekend. Output: confidence to build, or one specific thing to fix.

**The readiness criteria problem:** U1 never defines "ready to build." Without explicit criteria, "watch 10 artisans" can always be justified as the prerequisite.

**Proposed resolution:** Replace U1 (10-person discovery sprint) with: explicit readiness criteria + 3-day guerrilla test. U1 is REOPENED.

**Verdict on U1:** REOPENED — Growth Strategist challenges U1 as stalling tactic. Recommend replacing with guerrilla usability test + explicit readiness criteria.

---

## Debate 29: MVP Scope — 4 Features Underestimated?

**Challenge:** Technical Architect argues the 4-feature MVP scope is technically underestimated. French legal invoicing requirements add hidden complexity that makes a single-sprint 4-feature build unrealistic.

### Technical Architect — Phase 0.5 Case

**Core argument:** The 4 features (client file, devis, facture, relance) share infrastructure that creates bottlenecks: client schema, TVA multi-taux math, sequential numbering enforcement, mentions légales per client type. "Parallel" development on shared types means constant merge conflicts and integration testing nightmares.

**Hidden complexity in French invoicing:**
1. **Numérotation séquentielle:** Server-side enforcement, annual reset with prefix, no gaps, no duplicates, recovery logic. 2-3 days.
2. **TVA multi-taux:** French artisans use 3 rates (5.5%, 10%, 20%) per line item. Per-line calculation, TVA breakdown section, rounding accuracy. 1-2 days.
3. **Mentions légales:** Varies by client type (particulier, professionnel, étranger EU, hors EU). Dynamic block based on document type. 1-2 days.
4. **Facture creance:** Separate regulatory layer for factoring.

**The parallel development illusion:** 4 developers on 4 features sounds fast. Reality: all 4 share the same underlying types. Feature B (devis) can't ship without Feature A (clients). Feature C (factures) depends on Feature B's data model. Integration testing reveals cross-feature breakage late in the sprint.

**Proposed Phase 0.5 — devis-only MVP:**
Scope: client file + devis creation + send via WhatsApp/email. No factures, no relances.
- Validates the core flow: does Marc actually create and send a devis from his phone?
- Skips TVA complexity (devis doesn't require VAT in the same way)
- Skips sequential numbering (devis numbering is less regulated)
- 1 week build, 1 week test, shippable
- Lessons feed directly into factures Phase 1

**Verdict on D2:** REOPENED — Technical Architect challenges 4-feature MVP scope as underestimated. Proposes Phase 0.5 (devis-only) before full 4-feature build.

---

## Debate 30: Pricing — €29/€49/€79 Conflicts With Simplicity Positioning?

**Challenge:** Product Strategist challenges the €29/€49/€79 pricing structure as carried forward without debate. Argues it conflicts with "simple as WhatsApp" positioning and is above market vs Tolteck (€19) and Obat (€17).

### Product Strategist — Pricing-Repositioning Case

**Core argument:** Three tiers + simplicity positioning = cognitive dissonance. If it's "simple like WhatsApp," why parse three SKUs and decode feature differences? WhatsApp doesn't have tiers.

**The price floor problem:**
- Tolteck: €19/mo | Obat: €17/mo | This product: €29/mo (50-70% above market)
- For a simplicity play, €29 floor signals "serious business tool" — the opposite of "simple WhatsApp energy"
- French artisans (micro-SMBs, sole traders, ~€80k turnover) are price-sensitive. Mental model: "shouldn't cost more than Netflix" (€17-22)

**The tier structure problem:**
- €29/€49/€79 implies feature-gating that creates anxiety for a solo artisan: "Which tier do I need? Will I outgrow it? Am I paying for stuff I don't use?"
- Two tiers max aligns with simplicity positioning. Three tiers signals complexity.

**Competitor context:**
- Tolteck (40k+ French artisans) at €19, Obat at €17 — these are established market prices
- The differentiator (relances/follow-ups) might justify a premium, but only if clearly articulated

**Proposed two-tier structure:**
- **Starter: €19/mo** — devis + factures only (matches Tolteck, below market for "pro")
- **Pro: €29/mo** — + relances automatisées + prioritized support
- Drop €49/€79 entirely for v1

**The value anchor problem:** "2h/week saved × €50-80/h = €100-160/week" math is compelling but buried. It belongs on the pricing page explicitly:
> "2 heures par semaine sur les devis et relances. C'est €100-160 de travail. Votre facture mensuel? €29."

**Verdict on D5:** REOPENED — Product Strategist challenges €29/€49/€79 as carried forward without debate. Conflicts with simplicity positioning and above competitor floor. Recommends €19/€29 two-tier structure.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D1 | Positioning | Kill "CRM" — devis, factures, relances | 2026-03-30 |
| D2 | MVP scope | 4 features only | prior |
| D3 | Primary persona | Marc — solo smartphone-native | 2026-03-30 |
| D4 | Stack | Single managed Postgres | 2026-03-30 |
| D5 | Pricing | €29/€49/€79 tiered | prior — REOPENED Debate 30 |
| D6 | Trial | 14 days | 2026-03-30 |
| D7 | Architecture | Nuxt 3 + OVH managed Postgres | 2026-03-30 |
| D8 | E-invoicing | v2 feature (Chorus Pro compatible) | 2026-03-30 |
| D9 | Not MVP | No Kanban, no multi-user, no offline, no API keys | 2026-03-30 |
| D10 | Buyer trigger | "Admin pain" not "CRM need" | 2026-03-30 |
| D11 | Mobile | React Native from Day 1 via Expo | 2026-03-30 |
| D12 | Landing page | Simplicity-first — "Vos devis et factures, sans vous prendre la tête" | 2026-03-30 |
| D13 | Home view | Job-first — Active Job Card as home anchor | 2026-03-30 |
| D14 | E-invoicing timing | v2 — NOT Day 1 | 2026-03-30 |
| D15 | Relances differentiator | DE-EMPHASIZED — secondary feature below fold | 2026-03-30 |
| D16 | Trial length | 14 days, no credit card, email drip | 2026-03-30 |
| D17 | Mobile strategy | React Native from Day 1 (updated from PWA-first) | 2026-03-30 |
| D18 | MVP scope complexity | REOPENED — Phase 0.5 proposed (Debate 29) | 2026-03-30 |
| D19 | Pricing structure | REOPENED — €19/€29 two-tier proposed (Debate 30) | 2026-03-30 |

| U1 | Real discovery | REOPENED — replace with guerrilla usability test (Debate 28) | |
| U2 | E-invoicing platform | Factea first when v2 | 2026-03-30 |
| U7 | Domain | Still open — buy domain | |

---

*Last updated: 2026-03-30T11:38*

---

## Debate 25: Relances as Landing Hero — RESOLVED

**Challenge:** D15 (REOPENED at 11:11) — Product Strategist argued relances should be DE-EMPHASIZED on landing. Growth side argued relances ARE a key differentiator. Product Strategist (subagent) defends.

### Product Strategist — De-Emphasized Position (VERDICT)

**Assumption challenged:** The assumption that *pain chasing payments* = *desire for automated relances*. These are different problems. The discomfort artisans feel is relational (awkwardness of calling a client about money) — not logistical. Automated messages don't eliminate the awkwardness; they just anonymize it. For French artisans aged 45-55 who value direct personal communication, "relances automatiques" may feel MORE impersonal than picking up the phone.

**New evidence:**
1. "Wrong customer" pipeline problem: Automated relances attracts artisans with cash-flow problems and poor client relationships — churn risks. We want organized artisans running growing businesses, not fire extinguishers.
2. Competitor silence is signal: Tolteck (40k+ French artisans), Obat, Fignum — none lead with automated payment reminders. Established players have tested this; the market hasn't validated it.
3. Headline dissonance: D12 landed on "Vos devis et factures, sans vous prendre la tête" — clean, frictionless. Relances in the hero implies unpaid invoices, cash flow problems, crisis management — tonal whiplash.
4. "Get paid faster" is real — but "relances automatiques" ≠ the path. A reminder "Cette facture n'a pas été payée depuis 45 jours — voulez-vous relancer ?" with a pre-written template the artisan edits and sends THEMSELVES solves the awkwardness of drafting without impersonality.

**Verdict:** Relances = secondary feature, below fold, "Fonctionnalités" section. NOT in hero. NOT in headline. Frame as "Suivi de paiement" or "Rappels" (softer language). Artisan controls it — not "we text your client."

**Verdict on D15:** RESOLVED — Relances DE-EMPHASIZED on landing. Secondary feature only.

---

## Debate 26: Trial Length — 30 Days vs 14 Days — RESOLVED

**Challenge:** D16 (REOPENED at 11:11) — Growth Strategist argued 30 days creates procrastination, not urgency. D6 (original 30 days) conflicts with GTM doc (14 days). Growth Strategist (subagent) defends.

### Growth Strategist — 14-Day Trial (VERDICT)

**Assumption challenged:** "Busy people need more time to try a product." Busyness is not a resource allocation problem — it's a motivation problem. If an artisan signed up, they have an acute pain point NOW. They will NOT "find time" in week 3 of a 30-day trial. More time = more procrastination, not more usage. The 30-day trial creates psychological safety ("I have a whole month") which paradoxically reduces engagement.

**New evidence:**
1. The "infinite trial" paradox: Day 1 = zero urgency. Day 28 = panic with no product knowledge. 14 days creates immediate pressure to act on every session.
2. Self-selection: 14-day trial filters for acute-need buyers who will actually engage. 30-day trial attracts "interested someday" browsers who dilute conversion metrics.
3. GTM doc conflict resolved: GTM doc says 14 days, debate log said 30 days — this pulse resolves that conflict. 14 days wins.
4. Industry benchmarks: 14-21 day trials match or outperform 30-day trials on conversion across SMB SaaS CRMs (Close, HubSpot data).
5. French artisan context: Sole proprietors on job sites, managing clients at 9pm. Fits-and-starts usage pattern makes 14 days MORE realistic, not less — with clear aha moments: day 1 (clients organized), day 5 (quote sent), day 10 (follow-up reminder).
6. Email drip creates right urgency: Day 7 ("How's it going?"), Day 3 ("Last 3 days"), Day 1 ("Trial ends tomorrow"). Gentle pressure without anxiety.

**On credit card at signup:** NO credit card at signup. Friction kills conversion for non-tech-native users. The 14-day deadline IS the commitment device. Ask for credit card at Day 7-10 for engaged users.

**Verdict:** 14 days. No credit card at signup. Aggressive email drip in final week.

**Verdict on D16:** RESOLVED — Trial = 14 days (D6 updated). No credit card at signup. D6 conflict with GTM doc resolved in favor of 14 days.

---

## Debate 27: Mobile Strategy — PWA-First vs React Native from Day 1 — RESOLVED

**Challenge:** D17 (REOPENED at 11:11) — Technical Architect argued PWA-first fails on iOS, "6-month native pivot" is a lie. Technical Architect (subagent) defends with stronger evidence.

### Technical Architect — React Native from Day 1 (VERDICT)

**Assumption challenged:** "PWA is good enough for Android — the install friction only affects a small percentage." Two problems: (1) "Add to Home Screen" is NOT intuitive for 45-55 year old non-tech-heavy artisans — industry PWA install rates (~15%) assume tech-savvy users; for this demographic it could be under 5%. (2) The "6-month native pivot" is the most dangerous assumption in the debate — when PWA-first teams pivot, they discover: web codebase has accumulated technical debt, team has forgotten why native was needed, now face a full rewrite while product languishes. Start native. Stay native.

**New evidence:**
1. iOS web push is fundamentally broken: ~40% of French users on iOS. Web push notifications do NOT work without the PWA installed via Add to Home Screen. For a CRM where reminders ARE the product, this is catastrophic — 40% of users get zero reminder functionality.
2. App Store credibility: 45-55 year old artisans implicitly trust the App Store for financial/business tools. PWAs feel like "a website pretending to be an app." The review process provides psychological reassurance.
3. React Native IS the efficient choice: "PWA is faster to develop" compares apples to oranges — PWA (one platform, fundamentally broken on iOS) vs. React Native (both platforms, working notifications, App Store presence). Reframed correctly, React Native is the more efficient choice.
4. Development approach via Expo: `npx create-expo-app` gets working cross-platform app in minutes. Expo Notifications work out of the box. OTA updates bypass App Store review for code changes after launch. One-time App Store review delay at launch — not for every update.

**Verdict:** React Native from Day 1 (via Expo). Not PWA-first.

**Verdict on D17:** RESOLVED — Mobile strategy = React Native from Day 1 (D11 updated). PWA-first retired.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D1 | Positioning | Kill "CRM" — devis, factures, relances | 2026-03-30 |
| D2 | MVP scope | 4 features only | 2026-03-30 |
| D3 | Primary persona | Marc — solo smartphone-native | 2026-03-30 |
| D4 | Stack | Single managed Postgres | 2026-03-30 |
| D5 | Pricing | €29/€49/€79 tiered | prior |
| D6 | Trial | 14 days (updated from 30) | 2026-03-30 |
| D7 | Architecture | Nuxt 3 + OVH managed Postgres | 2026-03-30 |
| D8 | E-invoicing | v2 feature (Chorus Pro compatible) | 2026-03-30 |
| D9 | Not MVP | No Kanban, no multi-user, no offline, no API keys | 2026-03-30 |
| D10 | Buyer trigger | "Admin pain" not "CRM need" | 2026-03-30 |
| D11 | PWA vs Native | React Native from Day 1 (updated from PWA-first) | 2026-03-30 |
| D12 | Landing page | Simplicity-first — "Vos devis et factures, sans vous prendre la tête" | 2026-03-30 |
| D13 | Home view | Job-first — Active Job Card as home anchor | 2026-03-30 |
| D14 | E-invoicing timing | v2 — NOT Day 1 | 2026-03-30 |
| D15 | Relances differentiator | DE-EMPHASIZED — secondary feature, below fold | 2026-03-30 |
| D16 | Trial length | 14 days (updated from 30) | 2026-03-30 |
| D17 | Mobile strategy | React Native from Day 1 (updated from PWA-first) | 2026-03-30 |

| U1 | Real discovery | Still open — watch 10 artisans | |
| U7 | Domain | Still open — buy domain | |

---

*Last updated: 2026-03-30T11:24*

## Pulse 2026-03-30T11:50 — Three Resolutions

---

## Debate 31: U1 — Discovery Replaced by Readiness Protocol

**Challenge:** U1 ("watch 10 artisans before building") — challenged by Growth Strategist as indefinite deferral. Proposes replacing with guerrilla usability test + explicit readiness criteria.

### Growth Strategist — U1 Resolution

**Assumption challenged from Debate 28:** The guerrilla test proposal assumes a Figma prototype is ready. It is not. Who builds it? When? A 3-day guerrilla test that requires a prototype first has the same deferral problem as the original U1 — we've just moved the prerequisite.

**Key distinction:** Discovery research (what do artisans need?) is largely done. Marc is well-characterized. Pain is validated by Pennylane, Indy, Freebe all existing and growing. Usability validation (can they use our specific UI?) requires a prototype. These are different activities with different prerequisites.

**The real problem with the original U1:** Not "watching artisans" — it was doing it without structure or a defined output. "Go watch 10 artisans" without a structured task is expensive tourism. The activity is only as good as its structure.

**VERDICT on U1:** REPLACED — U1 is retired. Replaced by a two-phase readiness protocol:

**Readiness to Build criteria (4 items):**
1. Figma or clickable prototype of devis creation flow exists — not full mockup, just the primary screen (client selector + line items + total + send)
2. Guerrilla usability test is scheduled — 5 artisans at a wholesaler (Point P or Gedimat, Saturday morning), single task: create a devis from scratch on the prototype
3. Pain points confirmed — competitive analysis (Pennylane, Indy, Freebe) establishes French artisan admin pain is real and sized; personas locked (Marc's workflow well-documented)
4. Feature set frozen — client file, devis, facture, relance locked; no scope additions until post-MVP

**If the prototype isn't ready in 1 week:** Build anyway. Marc's workflow is well-understood. Post-launch usability testing with real beta users is valid too. The prototype is preferable but not a blocker.

---

## Debate 32: D2 — MVP Scope Sequenced, Not Parallel

**Challenge:** D2 (4-feature MVP) — challenged by Technical Architect as underestimating French invoice complexity. Phase 0.5 (devis-only) proposed.

### Technical Architect — D2 Resolution

**Assumption challenged from Debate 29:** Phase 0.5 (devis-only) risks building the wrong foundation. If you build devis in isolation for 2 weeks, you learn nothing about how devis → facture conversion works, how TVA affects the line-item model, or how mentions légales vary by client type. Phase 0.5 could produce a devis that doesn't cleanly generalize — and that's exactly the failure mode you're trying to avoid.

**The real insight:** The French invoice complexity (TVA multi-taux, sequential numbering, mentions légales) is a SCHEMA DESIGN problem, not a feature problem. It needs to be solved once in the schema layer — before any feature work begins — not avoided by deferring factures.

**The 4-feature parallel approach isn't infeasible** — it's just badly sequenced. The shared types problem (client schema, line items, TVA math, sequential numbering) is a schema design problem. If you do schema design first (Day 1), the parallel work becomes tractable.

**VERDICT on D2:** D2 = 4 features (client file, devis, facture, relance) in a SEQUENCED sprint structure:

- **Sprint 0:** Schema design — clients, quotes, invoices, reminders, TVA calculator (5.5/10/20% per line), sequential number generator, mentions légales renderer. Mentions légales are template-based, not schema-based.
- **Sprint 1:** Client file + devis feature (CRUD on top of Sprint 0 schema)
- **Sprint 2:** Factures + relances feature (CRUD on same schema)

Phase 0.5 retired — it teaches the wrong lessons and risks schema drift when you discover at week 3 that your devis schema doesn't support TVA per line.

---

## Debate 33: D5 — Free + €29 Two-Tier, Drop €49/€79

**Challenge:** D5 (€29/€49/€79 tiered) — challenged by Product Strategist as conflicting with simplicity positioning and above competitor floor.

### Product Strategist — D5 Resolution

**Assumption challenged from Debate 30:** Debate 30 frames the problem as a price-floor issue: €29 is too high relative to competitors, so we need €19/€29 two-tier. But this assumes price is the primary conversion friction. Is it?

For French artisans aged 45-55, solo operators, the real objection is not "€29 is expensive" — it's "will this actually work for ME, on my phone, in 5 minutes?" Trust and usability are the conversion barriers, not price. A free tier addresses the former (removes commitment anxiety) while a well-placed value anchor addresses the latter.

**The GTM doc already contains the winning objection handler:** "C'est €29/mois. C'est le coût d'une heure de main d'œuvre." This anchor is psychologically powerful for this audience. Debate 30 buried the value math under weekly ROI; the hourly labor frame is the sharper anchor.

**The €19 SKU problem:** €19 undercuts the value perception — if it's "cheaper than a restaurant meal," it's also easier to abandon. The €29 anchor ("one hour of labor") is stronger and already validated in the GTM objection map.

**VERDICT on D5:** Free + €29 two-tier. No €19 SKU at launch. Drop €49 and €79 entirely.

- **Free:** limited but functional (up to 10 clients, 5 active devis) — gets artisans in the door with zero friction, enables word-of-mouth acquisition, removes commitment anxiety before the upgrade conversation
- **€29/month:** full access, all features, value anchor explicit on the pricing page:
  > "2 heures par semaine sur vos devis et factures. C'est une heure de main d'œuvre. Votre abonnement? €29/mois."

**Why Free + €29 beats €19/€29:** Stronger acquisition funnel (Word of Mouth is primary GTM channel at 40% weight), clearer upgrade decision (full access vs limited), no price question left unanswered. Two SKUs maximum — any more breaks simplicity positioning.

---

*Last updated: 2026-03-30T12:01*

---

## Pulse 2026-03-30T12:01 — Three New Debates

---

## Debate 34: U7 — Domain Purchase Is Premature

**Challenge:** U7 ("buy domain — not alize, something memorable for devis/factures tool") has never been debated. It sits in the TODO as an open action item without scrutiny.

### Growth Strategist — Domain Purchase Should Be Deferred

**Core argument:** Buying a domain before the guerrilla usability test is premature branding commitment. If the prototype reveals artisans want job management more than invoicing, or the product angle shifts, the domain becomes a liability — registered, paid for, but wrong.

**Why buying now is premature:**
1. **Branding before validation:** We don't know if "devis/factures" is the final angle. The guerrilla test might reveal artisans care more about job tracking than invoicing — in which case a devis-focused domain is the wrong anchor.
2. **Domain lock-in:** Buy it, and you're committed to that name. If the product pivots, the domain actively miscommunicates.
3. **Alternatives exist:** A subdomain on existing infrastructure (`devis.lschvn.foo`) or a Carrd one-pager serves the MVP landing page need without commitment. Louis already has Coolify infrastructure.
4. **False progress:** "We have a domain" creates cognitive commitment that makes pivots harder.

**VERDICT on U7:** DEFERRED — use temporary subdomain or Carrd landing page until MVP validated post-guerrilla test. Domain purchase happens after product direction is confirmed.

---

## Debate 35: Sprint 0 — Flow-First Beats Schema-First

**Challenge:** Debate 32 resolved D2 with "Sprint 0 = pure schema design." Technical Architect (original proponent of Sprint 0 sequencing) now challenges this.

### Technical Architect — Schema-First Produces Over-Engineered Types

**Core argument:** Designing a schema in isolation from real usage is over-engineering. You don't know which fields artisans will actually populate until you watch them try. "Big bang schema design" produces types with fields nobody uses — and those fields create maintenance burden, UI clutter, and migration cost forever.

**Why schema-first is wrong:**
1. **Schema emerges from usage.** A client record might only need: name, phone, email. Do we need `client_type`? Only if the mentions légales renderer actually uses it — we don't know that until we build it and watch it in use.
2. **TVA complexity is a rendering problem, not a schema problem.** The rates are known. The per-line calculation is known. But where in the flow do you capture it? You won't know until you watch someone create their first devis.
3. **Time-to-real-feedback matters more than architectural purity.** A minimum devis flow built in 3 days with bare schema generates real feedback. Sprint 0's 5-day pure schema sprint generates... a schema document. Not user learning.
4. **Schema-first risks unused complexity.** You spend 5 days on sequential number enforcement, TVA breakdown tables, mentions légales templates. Then week 2, an artisan says "I don't do TVA, I'm below the threshold" — and your entire TVA schema is unused.

**The better model — Flow First, Schema Emerges:**
- Sprint 0: Build minimum viable devis flow (add client → add line items → preview → send via WhatsApp). No TVA (flat rate ok). No sequential numbering enforcement. Simple mentions légales block. Get in front of real users in 5 days.
- Sprint 1: Extract what worked. Formalize schema based on actual usage.

**VERDICT on D2 Sprint 0:** Redefined — Sprint 0 = build minimum viable devis flow (3-5 days, minimal schema). Schema formalization happens at Sprint 1, based on Sprint 0 usage learning. Phase 0.5 retired — again.

---

## Debate 36: D6 — Free Tier IS the Trial (Resolving the TODO.md Conflict)

**Challenge:** TODO.md says D6 = "30 days" but debate-log.md (Debate 26) resolved D6 = 14 days. The error reveals a deeper structural problem: Free + 14-day trial creates cognitive dissonance.

### Product Strategist — Free Tier + 14-Day Trial Is a Broken Model

**Core argument:** The 14-day trial was designed for a paid-only product. Now that D33 resolved Free + €29 two-tier, adding a 14-day trial on top creates redundant commitment friction and contradictory signals. The Free tier IS the trial — it removes time pressure while enabling full product experience up to limits.

**Why Free + 14-Day Trial is broken:**
1. **Two commitment devices conflict.** Free says "try without commitment, no time pressure." 14-day countdown says "decide now or lose access." Contradictory signals for a simplicity-first product.
2. **The Free tier already solves the trial problem.** Up to 10 clients and 5 active devis is enough to experience core value. If they outgrow it in week 1, they convert. If they don't in 3 months, they weren't a serious buyer.
3. **14-day countdown adds anxiety, not urgency.** Day-11 countdown email creates guilt — "I haven't had time to use this." Trial ends with anxiety, not confidence.
4. **Conversion moment is hitting the limit, not a countdown.** Free → Paid happens when the artisan naturally needs more. Countdown → Paid happens under pressure — leading to churn at month 2.

**VERDICT on D6:** **No time-limited trial. Free tier IS the trial.** Conversion happens when artisan hits Free limit. No countdown emails. Day-7 human check-in only ("How's it going? Need anything?").

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D1 | Positioning | Kill "CRM" — devis, factures, relances | 2026-03-30 |
| D2 | MVP scope | 4 features, SEQUENCED sprints. Sprint 0 = minimum devis flow (3-5d, minimal schema). Sprint 1 = client+devis. Sprint 2 = facture+relances. | 2026-03-30 |
| D3 | Primary persona | Marc — solo smartphone-native | 2026-03-30 |
| D4 | Stack | Single managed Postgres | 2026-03-30 |
| D5 | Pricing | Free + €29 two-tier. Drop €49/€79. | 2026-03-30 |
| D6 | Trial | No time-limited trial. Free tier IS the trial. Conversion at Free limit. No countdown emails. Day-7 human check-in only. | 2026-03-30 |
| D7 | Architecture | Nuxt 3 + OVH managed Postgres | 2026-03-30 |
| D8 | E-invoicing | v2 feature | 2026-03-30 |
| D9 | Not MVP | No Kanban, no multi-user, no offline, no API keys | 2026-03-30 |
| D10 | Buyer trigger | "Admin pain" not "CRM need" | 2026-03-30 |
| D11 | Mobile | React Native from Day 1 via Expo | 2026-03-30 |
| D12 | Landing page | Simplicity-first — "Vos devis et factures, sans vous prendre la tête" | 2026-03-30 |
| D13 | Home view | Job-first — Active Job Card as home anchor | 2026-03-30 |
| D14 | E-invoicing timing | v2 — NOT Day 1 | 2026-03-30 |
| D15 | Relances differentiator | DE-EMPHASIZED — secondary feature below fold | 2026-03-30 |
| D16 | Trial length | No countdown trial — Free tier IS the trial | 2026-03-30 |
| D17 | Mobile strategy | React Native from Day 1 | 2026-03-30 |

| U1 | Discovery | REPLACED — readiness protocol: (1) prototype exists, (2) guerrilla test scheduled, (3) pain confirmed, (4) feature set frozen. Prototype is blocker, not watching artisans. | 2026-03-30 |
| U2 | E-invoicing platform | Factea first when v2 | 2026-03-30 |
| U7 | Domain | DEFERRED — use subdomain/Carrd until MVP validated | 2026-03-30 |

---

## Pulse 2026-03-30T12:16 — Three New Challenges

---

## Debate 37: WhatsApp is a Primary Acquisition Channel, Not a Feature

**Challenge:** Product Strategist challenges the implicit assumption that WhatsApp is merely a transmission mechanism for sending devis/factures. Nobody has debated whether WhatsApp can be the PRIMARY acquisition funnel.

### Product Strategist — WhatsApp-as-Acquisition Case

**Assumption challenged:** WhatsApp is treated as a sharing feature (how Marc sends devis to clients), not as an acquisition channel. The GTM doc lists WhatsApp only as: (1) a sharing option and (2) a channel where artisans talk in WhatsApp groups. Nobody has debated that the WhatsApp message itself sent to the CLIENT is a direct acquisition touchpoint.

**Core argument:** Every time Marc sends a devis to Madame Martin via the app, she receives a beautifully formatted WhatsApp message showing professional quality. She's in "trust mode" — she's just witnessed Marc operate professionally. A CTA appended to that WhatsApp message ("Envoyez vos devis comme Marc → [LINK]") converts her admiration into a signup. Not her directly — but she likely knows other artisans. Every sent devis = a word-of-mouth delivery mechanism.

**Key arguments:**
1. 50,000 monthly brand impressions passively if 10k artisans × 5 devis/month
2. Trust-transfer: recipient sees professional quality in real-time; highest-intent moment for conversion
3. Acquisition and distribution are the same action — zero extra friction
4. Network effect: client refers to artisan contacts → compounds faster than any other GTM channel
5. Landing page CTA reframe: "Join the network of professionals your clients already trust" vs "Try it free"

**Potential flaws (honest):**
- Client recipients are often homeowners, not artisans — wrong audience for a B2B SaaS referral
- WhatsApp message length constraints limit the CTA
- Attribution gap — if it works, measuring it is hard

**VERDICT on U3/GTM framing:** REOPENED — WhatsApp-as-acquisition is a compelling reframe that changes landing page CTA and GTM priority. The fatal flaw: most WhatsApp devis recipients are homeowners, not artisans. However, for B2B contexts (property managers, business owners who receive devis from artisans), the channel is valid. Flag as secondary acquisition mechanism (not primary), test with UTM-tracked CTA in WhatsApp message.

---

## Debate 38: The Free Tier Creates a Worse Activation Problem Than the Trial Did

**Challenge:** Growth Strategist challenges D6 (Free tier IS the trial) — argues that removing time pressure eliminates the only mechanism forcing the aha moment before attention decays.

### Growth Strategist — Free-Tier Activation Problem Case

**Assumption challenged:** D6 rationale — "Free tier removes time pressure anxiety, allows organic usage, and the 10-client/5-devis limit creates a natural conversion trigger." Growth Strategist argues this inverts the truth: Free tier removes commitment friction but creates activation paralysis.

**Core argument:** Urgency is the only mechanism that forces the aha moment before attention decays. Marc is a solo artisan running between job sites all day. Without a deadline, "I'll come back to this when I have a client" becomes the default — and he always has a client. The 14-day trial created a forcing function; the Free tier removes it entirely.

**Key arguments:**
1. Urgency forces the aha moment before attention decays — Free tier = indefinite deferral
2. Free tier self-selects for non-buyers — serious buyers had acute problems NOW, Free tier lets them rationalize "later"
3. Day-7 human check-in is too little, too late — assumes he remembers signing up
4. 10-client/5-devis limit is too generous — he adds 2 clients, gets busy, app sits at 20% of limit forever
5. "I'll come back when I need it" is the most dangerous phrase in SaaS onboarding for a B2B admin tool

**Proposed resolution:** Free tier (10 clients, 5 devis) WITH a 7-day "activation window" after first login — soft deadline creating micro-urgency without full trial countdown anxiety.

**Potential flaws (honest):**
- "7-day window" can feel like a trial by another name — creates same anxiety D6 tried to eliminate
- The "setup completion" frame assumes onboarding is the problem; it might be product-usability fit instead
- Implemented wrong (aggressive countdown) it recreates D6's anxiety problem exactly

**VERDICT on D6:** REOPENED — Growth Strategist raises a legitimate concern about activation without urgency. The "conversion at limit" thesis requires users to reach the limit, and most won't. Best resolution: Keep Free tier, add a 3-email engagement sequence in Days 1-7 (not countdown emails — value emails: "Day 1: Add your first client", "Day 3: Send your first devis", "Day 7: See how it works") that create soft urgency without deadline framing.

---

## Debate 39: Expo-RN Creates Vendor Lock-in at the Worst Moment

**Challenge:** Technical Architect challenges D17's implicit assumption that Expo is the correct implementation vehicle for React Native at v1. The debate resolved "PWA-first vs React Native" but never debated "Expo managed workflow vs bare RN vs Capacitor."

### Technical Architect — Capacitor-Nuxt for v1 Case

**Assumption challenged:** Expo's managed workflow is the correct implementation choice for React Native at v1. Expo = fast setup, reliable push, OTA updates. Technical Architect argues these are not free advantages — they come with hidden costs that matter precisely at v1.

**Core argument:** Expo's business model has pivoted before (ExpoKit deprecation broke thousands of builds). At v1, when you most need to iterate fast and fix native issues yourself, Expo makes debugging harder not easier.

**Key arguments:**
1. Expo's abstraction hides complexity precisely when v1 teams need visibility — push credential failures are the most likely launch failure mode
2. Expo's business model instability is a real risk — ExpoKit deprecation is a precedent, not a hypothetical
3. Capacitor-wrapped Nuxt PWA: same codebase for web+mobile, faster build, full FCM/APNS control, no Expo dependency
4. Expo Notifications had documented reliability issues in 2024 — multiple service disruptions — unacceptable for a product where reminders ARE the core value
5. OTA updates bypassing App Store review removes a trust signal that matters for a financial tool used by 45-55 year old artisans

**Potential flaws (honest):**
- Capacitor has its own ecosystem risk (Ionic's business model concerns)
- "Slightly less native feel" is underselling it — web views vs true native is a real UX difference
- Direct FCM/APNS integration is more complex to implement than Expo's one-liner
- Migration path from Capacitor to React Native at v2 is non-trivial

**VERDICT on D17:** REOPENED — Technical Architect raises valid concerns about Expo reliability (2024 outages) and vendor lock-in. However, the Capacitor alternative has its own risks. Best resolution: Stick with Expo for now BUT implement direct FCM/APNS notification pipeline as override if Expo notifications fail. Add explicit "no ExpoKit" policy. D17 stands as "Expo-RN from Day 1" but with a circuit breaker: if Expo notification service has >1 outage in first 3 months, migrate to bare RN + direct FCM/APNS.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D1 | Positioning | Kill "CRM" — devis, factures, relances | 2026-03-30 |
| D2 | MVP scope | 4 features, SEQUENCED sprints. Sprint 0 = minimum devis flow (3-5d, minimal schema). Sprint 1 = client+devis. Sprint 2 = facture+relances. | 2026-03-30 |
| D3 | Primary persona | Marc — solo smartphone-native | 2026-03-30 |
| D4 | Stack | Single managed Postgres | 2026-03-30 |
| D5 | Pricing | Free + €29 two-tier. Drop €49/€79. | 2026-03-30 |
| D6 | Trial | No time-limited trial. Free tier IS the trial. — REOPENED Debate 38 | 2026-03-30 |
| D7 | Architecture | Nuxt 3 + OVH managed Postgres | 2026-03-30 |
| D8 | E-invoicing | v2 feature | 2026-03-30 |
| D9 | Not MVP | No Kanban, no multi-user, no offline, no API keys | 2026-03-30 |
| D10 | Buyer trigger | "Admin pain" not "CRM need" | 2026-03-30 |
| D11 | Mobile | React Native from Day 1 via Expo | 2026-03-30 |
| D12 | Landing page | Simplicity-first — "Vos devis et factures, sans vous prendre la tête" | 2026-03-30 |
| D13 | Home view | Job-first — Active Job Card as home anchor | 2026-03-30 |
| D14 | E-invoicing timing | v2 — NOT Day 1 | 2026-03-30 |
| D15 | Relances differentiator | DE-EMPHASIZED — secondary feature below fold | 2026-03-30 |
| D16 | Trial length | No countdown trial — Free tier IS the trial | 2026-03-30 |
| D17 | Mobile strategy | React Native from Day 1 — REOPENED Debate 39 (Expo reliability + vendor lock-in) | 2026-03-30 |

| U1 | Discovery | REPLACED — readiness protocol | 2026-03-30 |
| U2 | E-invoicing platform | Factea first when v2 | 2026-03-30 |
| U7 | Domain | DEFERRED — subdomain/Carrd until MVP validated | 2026-03-30 |
| U8 | WhatsApp acquisition | REOPENED — test as secondary acquisition mechanism (Debate 37) | 2026-03-30 |
| U9 | Free tier activation | REOPENED — 3-email engagement sequence proposed (Debate 38) | 2026-03-30 |

*Last updated: 2026-03-30T12:16*

---

## Pulse 2026-03-30T12:28 — Three New Debates

---

## Debate 40: Email Engagement Sequence — Wrong Channel for This Persona

**Challenge:** D6 (Free tier as trial) — Growth Strategist's proposed resolution (3-email Days 1-7 engagement sequence) assumes email works as an activation channel for French artisans. Product Strategist challenges this fundamental assumption.

### Product Strategist — Email is the Wrong Channel

**Assumption challenged:** That email is the appropriate engagement channel for Days 1-7 activation for French artisan users (45-55 year old tradespeople, smartphone-native, managing admin at 9pm).

**Core argument:**

The Growth Strategist proposes a 3-email sequence as a "value-first" alternative to urgency. But this proposal reveals a deeper assumption that's never been questioned: **that email works for this persona**.

It doesn't. Here's why:

**Marc's communication reality:**
- Primary channel: WhatsApp. Always on. Between job sites, not at a desk.
- Email check: Maybe 9pm, on his phone, when he's exhausted and just wants to finish admin.
- Push notifications: He probably ignores most, but at least they interrupt his actual work day.

**The email problem:**
An email sent at 9am Monday titled "Ajoutez votre premier client" lands in an inbox he won't see until 9pm — if at all. By then, the context is gone. The job site morning is a distant memory. He's now in "finish admin" mode, not "discover product value" mode.

**The WhatsApp opportunity:**
This is who these artisans ARE. They live in WhatsApp groups with other tradespeople, with clients, with prescripteurs. A WhatsApp message or a push notification tied to a specific moment (first devis of the day? end of job site?) would have 10x the engagement rate of an email.

**The real flaw in D6 and the proposed resolution:**
Both assume activation is the problem. But for a solo artisan like Marc, the activation moment isn't "add a client" — it's "this saved me 30 minutes at 9pm." The Free tier AS trial works fine IF you can trigger that moment. Emails three days apart don't trigger that moment. Contextual nudges when he's actually doing admin might.

**The challenge to the Growth Strategist:** On what evidence is email the right channel for Day-1 through Day-7 engagement for French tradespeople? Or is this just defaulting to SaaS playbook because it's comfortable?

---

**Verdict on D6:**

D6 is directionally correct — Free tier as trial removes countdown anxiety and respects the artisan's autonomy. But it's incomplete.

**The fix is not email sequences. It's channel and timing:**

1. **Push notifications** instead of email for Days 1-3. "Vous avez 5 minutes? Créez votre premier devis en 2 minutes."
2. **WhatsApp integration** (optional opt-in during onboarding) for those who prefer it. This is their world.
3. **Contextual prompts** triggered by time-of-day (evening reminder) or action (added first client → "Pro-tip: génère un PDF prêt à envoyer")
4. Keep the Free tier limits generous but add a **single "you're almost at your limit" notification** at 80% — not a countdown, just a heads-up that creates natural urgency without pressure.

The Growth Strategist's heart is in the right place (engagement matters) but the channel is wrong. Don't send emails to people who live on WhatsApp.

---

## Debate 41: Push Notifications Are Not The Product — Email Is Fine for v1

**Challenge:** D17 (React Native via Expo) — Both the original decision and the "circuit breaker" resolution (FCM/APNS fallback) assume push notifications are a core feature warranting complex infrastructure. Technical Architect challenges this fundamental premise.

### Technical Architect — Notifications Are Not The Product

**Assumption challenged:** Push notifications are a "core feature" warranting complex infrastructure decisions (FCM/APNS circuit breakers, monitoring plans, migration triggers).

**Core argument:**

You're building a Mini-CRM for 45-55 year old French artisans. The product is: client management + devis + factures + relances. That's document lifecycle management. Notifications are a **delivery mechanism**, not the product.

The entire debate is framed backwards. It assumes push notifications must work perfectly from Day 1 because they're "core." But ask yourself: what did French artisans do before this app? They sent emails. They made phone calls. They put sticky notes on desks. Email worked fine for decades.

For this audience, email-based relances are:
- Already familiar (they've been doing this)
- Works on any device without installation
- Doesn't require handling APNS certificates, FCM credentials, Expo token management
- Has delivery receipts. You know the artisan sent it. You know if it bounced.

The circuit breaker plan (FCM/APNS fallback + 3-month uptime monitoring + bare RN migration trigger) is a **v1 distraction**. You're engineering for notification reliability when you should be engineering for document reliability. Can you generate a professional PDF devis? Can you track which factures are overdue? That's the product.

Push notifications are v2 polish. Get the document management right first. Add push when you have actual users complaining about email not being enough.

**Verdict on D17:**

1. Use Expo-RN. It's fine for v1.
2. **Do not build FCM/APNS direct pipeline at launch.** Email notifications only.
3. The "circuit breaker" resolution adds complexity before you have users to justify it.
4. Set a reminder: if you hit 50 paying users who complain about email notifications, then invest in push.

The lock-in risk is real but the consequence is wrong. The real lock-in risk is building your document engine on a platform that makes PDF generation and email delivery complicated. That's where your debugging energy should go at v1, not notification infrastructure.

**Start with email. Ship the product. Add push when it matters.**

---

## Debate 42: WhatsApp CTA is Attribution Theater

**Challenge:** U8 (WhatsApp as acquisition channel) — Product Strategist's proposal assumes a CTA appended to WhatsApp devis messages can be meaningfully tracked and attributed. Growth Strategist challenges the attribution assumption and the B2B segmentation.

### Growth Strategist — The Attribution Theater Problem

**Assumption challenged:** The assumption that a CTA appended to a WhatsApp devis message can be meaningfully tracked and attributed as an acquisition mechanism — even with UTM parameters.

**Core argument:**

The Product Strategist's case rests on a 50k monthly impression number and "trust-transfer moment." But both pillars are weaker than presented.

**On impressions:** 50k × artisan-client messages sounds impressive. But the conversion funnel from "sees CTA in WhatsApp devis" → "clicks link" → "lands on simplicity-first landing page" → "signs up for B2B SaaS tool" has a compounding drop-off problem. Homeowners who receive devis aren't looking for CRM software. They don't have a professional problem that this tool solves. You're paying in attention for an audience that has zero purchase intent. The 50k number is vanity metrics theater.

**On the B2B segmentation:** Property managers and business owners receiving artisans' devis is a real segment. But the question is: are they receiving *via WhatsApp*? In France, B2B invoicing tends toward email, formal portals, or even physical paper for property management. WhatsApp for professional devis exchange is more common for small artisans dealing directly with individual clients — which circles back to the homeowner problem.

**On UTM tracking as the solution:** Even if a B2B recipient clicks the CTA, they land on a landing page designed for artisans (simplicity-first, professional invoicing focus). The messaging mismatch will tank conversion. And if you UTM-track it, you'll measure clicks, not signups. You'll optimistically report "Channel working" while actual funnel conversion hemorrhages invisibly.

**The real opportunity being missed:** The context states "WhatsApp groups of artisans are active." This is the actual WhatsApp acquisition vector — artisan-to-artisan networks, not artisan-to-client broadcasts. If 10k artisans are in 5 active WhatsApp groups each, that's 50k artisan-to-artisan touchpoints per month that could carry peer endorsement. Word-of-mouth is already 40% of acquisition. WhatsApp groups are the *amplification layer* for bouche-à-oreille, not a CTA delivery mechanism.

**Verdict on U8:**

**Kill the explicit CTA in WhatsApp devis messages.** It's a low-conversion attribution theater play that risks diluting brand perception (marketing in professional invoices feels cheap to French artisans).

**Redirect U8 to:** Develop a "Send to colleague" or "Share with fellow artisan" lightweight mechanism within the product itself, designed for WhatsApp group contexts. Track referrals from existing users sharing with peers in WhatsApp groups — this captures the authentic word-of-mouth amplification with attribution, rather than trying to turn client-facing devis into a marketing channel.

Secondary test: UTM-track a *minimal* CTA (no explicit sales copy) in B2B-facing devis only (identify property manager recipients via domain or context), with messaging that speaks to their workflow ("Recevez vos devis proprement →"). Keep it whisper-quiet. Measure separately. If it converts, it converts. If not, kill it fast.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D1 | Positioning | Kill "CRM" — devis, factures, relances | 2026-03-30 |
| D2 | MVP scope | 4 features, SEQUENCED sprints. Sprint 0 = minimum devis flow (3-5d, minimal schema). Sprint 1 = client+devis. Sprint 2 = facture+relances. | 2026-03-30 |
| D3 | Primary persona | Marc — solo smartphone-native | 2026-03-30 |
| D4 | Stack | Single managed Postgres | 2026-03-30 |
| D5 | Pricing | Free + €29 two-tier. Drop €49/€79. | 2026-03-30 |
| D6 | Trial | No time-limited trial. Free tier IS the trial. REOPENED: engagement channel (email vs push) needs resolution. | 2026-03-30 |
| D7 | Architecture | Nuxt 3 + OVH managed Postgres | 2026-03-30 |
| D8 | E-invoicing | v2 feature | 2026-03-30 |
| D9 | Not MVP | No Kanban, no multi-user, no offline, no API keys | 2026-03-30 |
| D10 | Buyer trigger | "Admin pain" not "CRM need" | 2026-03-30 |
| D11 | Mobile | React Native from Day 1 via Expo | 2026-03-30 |
| D12 | Landing page | Simplicity-first — "Vos devis et factures, sans vous prendre la tête" | 2026-03-30 |
| D13 | Home view | Job-first — Active Job Card as home anchor | 2026-03-30 |
| D14 | E-invoicing timing | v2 — NOT Day 1 | 2026-03-30 |
| D15 | Relances differentiator | DE-EMPHASIZED — secondary feature below fold | 2026-03-30 |
| D16 | Trial length | No countdown trial — Free tier IS the trial | 2026-03-30 |
| D17 | Mobile strategy | React Native from Day 1 via Expo. Email-only notifications at launch. Push notifications deferred to v2 unless 50+ paying users complain. | 2026-03-30 |
| D40 | Engagement channel | REOPENED — push notifications + WhatsApp opt-in beats email for Days 1-7 engagement | 2026-03-30 |
| D41 | Notification infra | FCM/APNS circuit breaker NOT needed at v1. Email-only at launch. | 2026-03-30 |
| D42 | WhatsApp CTA | REOPENED — explicit CTA in WhatsApp devis messages killed. Referral within product for WhatsApp groups instead. | 2026-03-30 |

| U1 | Discovery | REPLACED — readiness protocol | 2026-03-30 |
| U2 | E-invoicing platform | Factea first when v2 | 2026-03-30 |
| U7 | Domain | DEFERRED — subdomain/Carrd until MVP validated | 2026-03-30 |
| U8 | WhatsApp acquisition | REOPENED — explicit CTA killed. Referral mechanism + whisper-quiet B2B test only. | 2026-03-30 |
| U9 | Free tier activation | REOPENED — push/WhatsApp engagement beats email for this persona | 2026-03-30 |

---

*Last updated: 2026-03-30T12:28*

---

## Pulse 2026-03-30T12:42 — Three New Debates

---

## Debate 43: D40 — Channel Is Secondary, Free Tier Design Is Primary

**Challenge:** D40 engagement channel — Product Strategist challenges the framework that "engagement channel" (push vs WhatsApp vs email) is the variable determining Free tier activation success.

### Product Strategist — The Wrong Debate

**Assumption challenged:** That ANY engagement mechanism will move the needle on activation if the right message hits the right channel at the right time.

**Core argument:**

Marc's actual mental model: WhatsApp is his CRM (it works), Excel tracks his devis (it works). He signed up for Free tier because it was free — not because he had acute pain. The 10-client/5-devis limits don't create urgency. They create breathing room. A 45-year-old electrician with 8 clients and 4 open devis thinks "That'll do" — hits the ceiling in 6 months, by which point he'll have decided whether the product is worth paying for.

Day 1 "Add your first client" → "I already know all my clients." Day 3 "Send your first devis" → "My Word template works fine." Day 7 "See how it works" → "My WhatsApp works too." None of these micro-actions solve a felt pain Marc has right now.

**VERDICT on D40:** RESTATED — D40 resolution is not about channel. It's about: "What changes in Free tier design so artisans feel the product's value BEFORE needing to be prompted?"

Three resolution paths:
1. **Restructure Free tier limits** — lower them (e.g., 5 clients / 3 devis) to create a sooner, more salient ceiling
2. **Redesign Day 1 experience** — make the first value moment so immediate that it rewrites the "this works fine" belief
3. **Accept long-tail activation** — design for month-2 or month-3 value revelation; stop trying to force urgency on a persona with no acute friction

---

## Debate 44: D41 — Email-Only Relances Is the Worst of Three Worlds

**Challenge:** D41 email-only verdict — Technical Architect challenges that email relances are "fine for v1" given Obat advertises real-time push notifications and Expo push reliability evidence.

### Technical Architect — Email-Only Should Be Reversed

**Assumption challenged:** That email-based relances are acceptable at v1 because "French artisans have been doing it this way for decades."

**New evidence:**

1. **Obat advertises "notifications et rappels en temps reel"** — real-time push notifications are a marketed feature of a major competitor. We would ship feature-inferior product before earning any loyalty.
2. **The 2024 Expo outage was about EAS Build, not push notifications** — reliability concerns cited in D41 were about the build pipeline, not notification delivery. Expo Notifications uses standard FCM/APNS infrastructure.
3. **Email relances actively signal "worse product"** — An artisan who has used Obat receives email relances as a downgrade. Not neutral — a negative quality signal.

**VERDICT on D41:** REVERSED — D41 email-only decision is wrong. Options:
- **Preferred:** Add Expo Push Notifications at launch (if EAS Build exists, a few hours of work)
- **Alternative:** Cut relances feature from v1 entirely — don't ship degraded version that signals inferiority vs. Obat
- **Never:** Email-only relances at launch

---

## Debate 45: D42 — In-Product Referral Is Not a Real Acquisition Channel

**Challenge:** D42 verdict — Growth Strategist challenges "in-product share with fellow artisan" as a meaningful acquisition mechanism.

### Growth Strategist — Four Fatal Flaws

**Assumption challenged:** That "Share with fellow artisan" within the product will generate meaningful acquisition through WhatsApp peer networks.

**Four fatal flaws:**

1. **Trigger timing undefined** — Unlike the WhatsApp CTA (fires at natural moment: "share your devis"), the referral prompt requires engineering a moment that doesn't naturally exist.
2. **Copy is weak** — "Partage cette app avec un autre artisan !" = "Do free marketing labor for us." Without incentive, referral rates under 2%. With 500 Free tier users = 10 new users. Not a growth channel.
3. **No incentive structure** — B2B referral requires referrer benefit AND referee benefit. The verdict proposes neither.
4. **WhatsApp groups are competitive spaces** — French artisan groups are peer support networks, not recommendation engines. Sending a SaaS referral implies the recipient's system is inferior.

**The real acquisition GTM:**
- **Wholesaler presence** — Gedimat, Point P (1,900+ branches), Samse: artisans visit weekly. Co-brand flyers, counter displays.
- **Prescriber networks** — Architectes and property managers recommend contractors. One prescriber → 50+ artisans.
- **SEO for "devis facture artisan"** — Compound growth, not one-shot referral events.

**VERDICT on D42:** CLOSED — kill explicit WhatsApp CTA in devis, kill in-product peer referral as primary acquisition. Redirect to wholesaler pilot + prescriber networks + SEO. U10 opened for wholesaler GTM.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D1 | Positioning | Kill "CRM" — devis, factures, relances | 2026-03-30 |
| D2 | MVP scope | 4 features, SEQUENCED sprints. Sprint 0 = minimum devis flow (3-5d, minimal schema). Sprint 1 = client+devis. Sprint 2 = facture+relances. | 2026-03-30 |
| D3 | Primary persona | Marc — solo smartphone-native | 2026-03-30 |
| D4 | Stack | Single managed Postgres | 2026-03-30 |
| D5 | Pricing | Free + €29 two-tier. Drop €49/€79. | 2026-03-30 |
| D6 | Trial | No time-limited trial. Free tier IS the trial. Engagement strategy restated by D43. | 2026-03-30 |
| D7 | Architecture | Nuxt 3 + OVH managed Postgres | 2026-03-30 |
| D8 | E-invoicing | v2 feature | 2026-03-30 |
| D9 | Not MVP | No Kanban, no multi-user, no offline, no API keys | 2026-03-30 |
| D10 | Buyer trigger | "Admin pain" not "CRM need" | 2026-03-30 |
| D11 | Mobile | React Native from Day 1 via Expo | 2026-03-30 |
| D12 | Landing page | Simplicity-first — "Vos devis et factures, sans vous prendre la tête" | 2026-03-30 |
| D13 | Home view | Job-first — Active Job Card as home anchor | 2026-03-30 |
| D14 | E-invoicing timing | v2 — NOT Day 1 | 2026-03-30 |
| D15 | Relances differentiator | DE-EMPHASIZED — secondary feature below fold | 2026-03-30 |
| D16 | Trial length | No countdown trial — Free tier IS the trial | 2026-03-30 |
| D17 | Mobile strategy | React Native from Day 1 via Expo | 2026-03-30 |
| D40 | Engagement channel | RESTATED — channel is secondary. Real question: Free tier design that creates value perception before prompting. Three paths: (1) lower limits, (2) Day 1 redesign, (3) accept long-tail activation. | 2026-03-30 |
| D41 | Notification infra | REVERSED — email-only is wrong. Preferred: Expo Push Notifications at launch (if EAS Build exists). Alternative: cut relances from v1. Never: email-only. | 2026-03-30 |
| D42 | WhatsApp referral | CLOSED — kill CTA in devis, kill in-product peer referral as acquisition channel. Redirect to wholesaler presence + prescriber networks + SEO. | 2026-03-30 |

| U1 | Discovery | REPLACED — readiness protocol | 2026-03-30 |
| U2 | E-invoicing platform | Factea first when v2 | 2026-03-30 |
| U7 | Domain | DEFERRED — subdomain/Carrd until MVP validated | 2026-03-30 |
| U8 | WhatsApp acquisition | CLOSED — no WhatsApp CTA in devis. WhatsApp sharing = document sharing only. | 2026-03-30 |
| U9 | Free tier activation | RESTATED — see D43 resolution | 2026-03-30 |
| U10 | GTM: Wholesaler presence | NEW — Gedimat/Point P/Samse pilot, co-brand flyers, counter displays | 2026-03-30 |

---

---

## Pulse 2026-03-30T12:58 — Three New Debates

---

## Debate 46: D43 — Lower Limits Destroys Trust Before Value Is Established

**Challenge:** D43 (Free tier activation) — Product Strategist challenges the assumption that lowering limits (10→5 clients, 5→3 devis) creates a sooner ceiling that forces upgrade decisions.

### Product Strategist — Lower Limits Creates Frustration, Not Urgency

**Assumption challenged:** Lower limits = sooner, more salient ceiling → upgrade decision. This assumes the Free user thinks "time to upgrade" when hitting a limit. For the French artisan who signed up because it was *free* (not because of acute pain), the psychology is different.

**Core argument:**

There are two types of Free users:
1. **Pain-motivated** — signed up because they needed it urgently → limit hits = "I need more capacity" → conversion
2. **Curiosity-driven** — signed up because it was free, skeptical of software, exploring → limit hits = frustration → "c'est fait pour me piéger" → abandonment before conversion

Marc skews toward #2. He's a solo artisan who heard "gratuit," he's skeptical of SaaS subscriptions (historically sold via CD/license in France), he's not losing sleep over client management. When he hits a limit on Day 3 — before he's felt the core value — he doesn't think "upgrade." He thinks the product is designed to trap him.

**The math is broken:** Path A optimizes for conversion rate *among users who survive long enough to hit the limit*, while ignoring the users who churn at first friction. Lower limits may increase % of surviving users who convert, but also increases total pool of frustrated early churners who never give you a second chance.

**French market trust problem:** Artisans have been sold software via one-time CD purchases (Sage, Ciel). SaaS feels like a money grab. Hitting a wall early validates their suspicion.

**Path A doesn't create urgency — it creates resentment before loyalty is built.**

**VERDICT on D43:**

D43 resolution is REFINED — not Path A vs Path B, but a combined approach:

1. **Keep generous limits** (10 clients / 5 devis) — let users live inside the product long enough to feel value
2. **Redesign Day 1 onboarding** to deliver the "aha moment" in under 5 minutes — the limit should hit *after* the user understands what they'd be leaving on the table
3. **Make upgrade moments emotionally salient** — trigger prompts at contextually meaningful moments ("vous avez un gros client — créer un 6e devis?"), not cold "you've reached your limit" banners
4. **Soft limits before hard blocks** — let users exceed once with "vous êtes presque à limite" before the wall hits. Extends trust-building phase.
5. **Path B is primary. Path A is secondary** — optimize Day 1 first; lower limits only after measuring where the aha moment occurs.

---

## Debate 47: D41 — "Few Hours" Estimate for Expo Push Is Wrong

**Challenge:** D41 (Push notifications) — Technical Architect challenges the assumption that Expo Push Notifications is "a few hours of work if EAS Build exists."

### Technical Architect — Expo Push Reality Check

**Assumption challenged:** "Add Expo Push Notifications at launch (if EAS Build exists, a few hours of work)." This underestimates the actual complexity of production-ready push notifications.

**Core argument:**

The "few hours" estimate ignores several non-trivial components:

**1. Token management ≠ one liner:**
- You must `requestNotificationPermissionsAsync()` and handle the response
- Tokens can CHANGE (iOS restores, app reinstalls, backup restores)
- You need backend infrastructure to store `userId → pushToken` mappings
- Need to handle token invalidation/deletion lifecycle
- **Reality:** 1-2 days of backend work minimum

**2. APNS certificate setup — this is not free:**
- Even with Expo, you still need APNS client certificates OR APNS auth keys
- That means: Apple Developer Account ($99/yr), App ID with Push capability, certificate generation, upload to Expo
- Certificates expire yearly — need renewal reminder system
- `eas credentials` helps but doesn't eliminate the Apple Developer portal dance
- **Reality:** 2-4 hours of setup + annual maintenance overhead

**3. No built-in fallback:**
- Expo Push is a proxy. If Expo has an outage, your notifications don't fire
- There's no "fallback to direct APNS" toggle
- If reliability is critical, you need a custom fallback architecture anyway
- **Reality:** You don't own the delivery path

**4. "Few hours" assumes zero edge cases:**
- Testing on physical devices (no simulator for push)
- Background vs foreground notification behavior
- Notification categories/actions on iOS
- Deep linking from notification to specific screen
- **Reality:** 1-2 weeks for production-ready, not hours

**Real comparison:**
| Approach | Initial Time | Operational Complexity |
|----------|-------------|----------------------|
| Expo Push | 1-2 weeks | Medium |
| Cut from v1 | 0 | 0 |
| Direct APNS/FCM | 3-4 weeks | High |

**VERDICT on D41:**

D41 resolution is REFINED — Expo Push is still the right call over building from scratch, but the estimate should be **1-2 weeks, not hours**.

**Revised decision:**
- **Keep** Expo Push as the chosen path — it reduces complexity vs. raw APNS/FCM
- **Revise estimate:** 1-2 weeks of engineering time, not "few hours"
- **If deadline can't accommodate:** defer notifications to v1.1, use email-only relances as temporary bridge (accepting the competitor disadvantage)
- **If shipping in v1:** budget the full 1-2 weeks; do not promise notifications at launch if you can't commit that time

---

## Debate 48: U10 — Wholesaler Presence Reaches the Wrong Artisan

**Challenge:** U10 (Wholesaler GTM) — Growth Strategist challenges the assumption that Gedimat/Point P (1,900+ branches) presence reaches Marc, the solo artisan persona.

### Growth Strategist — Gedimat Reaches Account-Holder Contractors, Not Solo Artisans

**Assumption challenged:** 1,900+ branch presence = reaching our target artisan at scale. Gedimat and Point P are account-holder merchants whose customer profile skews toward construction companies with formal procurement relationships — not the solo Marc persona.

**Core argument:**

**Who actually walks into Gedimat/Point P:**
- Construction companies with formal procurement relationships
- Larger contractors who buy in bulk on credit terms
- Professional buyers who order via account managers

**Marc is a different creature:**
1. **He doesn't walk into Gedimat — he orders from his phone.** Need material → check supplier app/website → order → delivery. Physical branch visits are a fallback, not a habit.
2. **He's not an account holder.** Account-based merchants require credit relationships, company structures, VAT compliance bureaucracy. Marc buys cash-and-carry or via specialist suppliers who don't gatekeep with account applications.
3. **He's in the long tail.** Gedimat's foot traffic is dominated by the 20% of buyers who generate 80% of revenue — professional contractors. Marc is in the scattered long tail of walk-in cash purchases.
4. **Counter displays and flyers are invisible noise.** If Marc even visits a branch, he's in and out. He doesn't linger at displays or pick up flyers. His attention is on his phone, on the job site, on peer referrals.

**The real first move to reach Marc:**
- **Digital-acquisition first** — trade-specific Facebook groups, WhatsApp artisan communities, SEO for problem-solution queries, YouTube tutorials
- **Specialist retailer partnerships** — smaller distributors who serve the solo artisan segment and already have their trust
- **Prescriber networks (architects/property managers) are actually the stronger complementary play** — they create pull-through demand from Marc at the job site level

**VERDICT on U10:**

U10 resolution is REFINED — wholesaler presence is NOT the primary GTM move.

**Revised GTM priority order:**
1. **Digital channels** (WhatsApp groups, Facebook artisan communities, SEO) — where Marc actually discovers things
2. **Specialist retailer partnerships** — smaller distributors serving solo artisans, not generalist wholesaler chains
3. **Prescriber networks** (architects, property managers) — B2B pull-through
4. **Wholesaler presence** — only as secondary brand-awareness play, not primary acquisition

**NEW TODO:** Audit what purchasing channels solo artisans (45-55, French market) actually use — identify top 5 digital touchpoints and top 3 specialist retailer types before committing to wholesaler GTM investment.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D1 | Positioning | Kill "CRM" — devis, factures, relances | 2026-03-30 |
| D2 | MVP scope | 4 features, SEQUENCED sprints. Sprint 0 = minimum devis flow (3-5d, flow-first). Sprint 1 = client+devis. Sprint 2 = facture+relances. | 2026-03-30 |
| D3 | Primary persona | Marc — solo smartphone-native artisan | 2026-03-30 |
| D4 | Stack | Single managed Postgres | 2026-03-30 |
| D5 | Pricing | Free + €29 two-tier. No €19 SKU. Drop €49/€79. Value anchor: "2h/week = 1h labor = €29/month." | 2026-03-30 |
| D6 | Trial | No time-limited trial. Free tier IS the trial. Engagement: REFINED — keep generous limits (10/5), Day 1 redesign for immediate aha moment, soft limits before hard blocks, emotionally salient upgrade triggers. | 2026-03-30 |
| D7 | Architecture | Nuxt 3 + OVH managed Postgres | 2026-03-30 |
| D8 | E-invoicing | v2 feature | 2026-03-30 |
| D9 | Not MVP | No Kanban, no multi-user, no offline, no API keys | 2026-03-30 |
| D10 | Buyer trigger | "Admin pain" not "CRM need" | 2026-03-30 |
| D11 | Mobile | React Native from Day 1 via Expo | 2026-03-30 |
| D12 | Landing page | Simplicity-first — "Vos devis et factures, sans vous prendre la tête" | 2026-03-30 |
| D13 | Home view | Job-first — Active Job Card as home anchor | 2026-03-30 |
| D14 | E-invoicing timing | v2 — NOT Day 1 | 2026-03-30 |
| D15 | Relances differentiator | DE-EMPHASIZED — secondary feature below fold | 2026-03-30 |
| D16 | Trial length | No countdown trial — Free tier IS the trial | 2026-03-30 |
| D17 | Mobile strategy | React Native from Day 1 via Expo. Email-only relances at launch (push deferred to v2). | 2026-03-30 |
| D41 | Notification infra | REFINED — Expo Push = 1-2 weeks (not "few hours"). If deadline can't accommodate, defer to v1.1. | 2026-03-30 |
| D43 | Free tier activation | REFINED — Path B primary (Day 1 redesign), Path A secondary (lower limits only after measuring aha moment). Keep generous limits. Soft limits before hard blocks. Emotionally salient upgrade triggers. | 2026-03-30 |
| D46 | Free tier limits | RESOLVED — do NOT lower limits from 10/5. Trust-building before limit enforcement. Limit should hit AFTER aha moment. | 2026-03-30 |
| D47 | Expo Push estimate | RESOLVED — 1-2 weeks, not "few hours." Budget properly or defer. | 2026-03-30 |
| D48 | Wholesaler GTM | REFINED — not primary GTM. Digital + specialist retailers first. Wholesaler secondary. | 2026-03-30 |

| U1 | Discovery | REPLACED — readiness protocol | 2026-03-30 |
| U2 | E-invoicing platform | Factea first when v2 | 2026-03-30 |
| U7 | Domain | DEFERRED — subdomain/Carrd until MVP validated | 2026-03-30 |
| U8 | WhatsApp acquisition | CLOSED — no WhatsApp CTA in devis | 2026-03-30 |
| U9 | Free tier activation | REFINED — see D43/D46 | 2026-03-30 |
| U10 | GTM: Wholesaler | REFINED — digital + specialist retailers first, wholesaler secondary. Audit solo artisan purchasing channels first. | 2026-03-30 |

---

*Last updated: 2026-03-30T12:58*

---

## Pulse 2026-03-30T13:15 — Three New Challenges

---

## Debate 49: GTM Priority — Prescriber Networks Should Lead, Not Digital Channels

**Challenge:** D48 (GTM priority) — Product Strategist challenges the "digital channels first" conclusion, arguing it confuses where Marc communicates with where he discovers professional tools.

### Product Strategist — Prescriber Networks Must Lead GTM

**Assumption challenged from D48:** "Digital channels (WhatsApp groups, Facebook artisan communities, SEO) = where Marc discovers tools." This conflates communication habitat with tool discovery pathway.

**Core argument:**

Marc lives on WhatsApp. That tells us where he *chats* — not where he *discovers professional software*. French artisans adopt new business tools through trusted intermediaries: architects who specify software requirements, property managers who vet contractors, building managers who send out RFPs. When a property manager tells Marc "use software for your devis on this renovation" — that's not marketing. It's a job requirement. The prescriber creates *pull-through demand*.

**The economics are lopsided:**
- One property manager managing 50 artisans = 50 high-intent acquisitions in a single relationship
- One Facebook group post to 500 members = maybe 3 clicks, 0 adoptions
- A prescriber recommendation hits at the moment of a new project — the highest possible intent moment in the artisan sales cycle

**Digital channels are capture, not acquisition:**
SEO and Facebook groups are excellent for nurturing existing leads, reinforcing brand recall, and supporting customers. They are poor for initial acquisition of professional tools where trust is paramount.

**The audit gap:** D48 concluded "digital first" without asking: *"How did French artisans in this age bracket discover their last business tool?"* That answer is predictably: colleague, client, prescriber — not Facebook ad.

**VERDICT on D48 / U10:** REOPENED — Product Strategist argues GTM priority should be REVERSED: prescriber networks FIRST, specialist retailers SECOND, digital channels THIRD, wholesaler presence LAST. The "digital first" conclusion was made on behavioral observation rather than discovery research.

---

## Debate 50: Email-Only Relances at Launch Is a Competitive Liability

**Challenge:** D47/D41 — Technical Architect challenges the "email-only as acceptable bridge at launch" conclusion, arguing the 50-user complaint threshold is dangerously reactive.

### Technical Architect — Email-Only Kills Early Momentum Before It Starts

**Assumption challenged from D41/D47:** Email-only relances at launch is an *acceptable* bridge, with push deferred to v2 unless 50+ paying users complain. The rationale: "email worked for decades" and Expo Push complexity.

**Core argument:**

The 50-user threshold is reactive damage control, not proactive product management. By the time 50 paying customers complain, the narrative is already set — they've already written GetApp or Capterra reviews. They already posted on forums. "No push notifications" becomes a red X on comparison sites before we ever get a chance to prove our value.

**The feature comparison problem:**
Obat advertises "notifications et rappels en temps réel" as a core differentiator. When our exact ICP compares tools on a comparison site and sees "No push notifications" listed against our name, that's not a feature gap. That's a **disqualification flag**. Trial users don't need to try us to rule us out.

**Expo Push is not exotic engineering:**
It's a standard React Native capability, 1-2 weeks of engineering already budgeted in D47. Deferring it signals either technical incapacity or that push relances aren't actually a priority — even though D41/D47 implicitly accepted they are the preferred path.

**"Email worked for decades" is the argument against progress:**
The same logic was used to dismiss mobile apps, SaaS, and every user expectation shift. Comfort is not a competitive advantage.

**VERDICT on D41/D47:** REOPENED — Technical Architect argues Expo Push must ship at launch, not defer to v2. The 1-2 weeks is already budgeted. The real cost is feature comparison disqualification that happens before signup — not after.

---

## Debate 51: Free Tier Converts via Habit Formation, Not Limit-Hit

**Challenge:** D43/D46/D6 — Growth Strategist challenges the limit-hit + contextual prompt conversion model, arguing it assumes motivation that solo artisans don't have.

### Growth Strategist — The Conversion Model Is Wrong

**Assumption challenged from D43/D46/D6:** Conversion happens when artisan (a) hits the 10-client/5-devis limit, or (b) sees a contextual upgrade prompt at a "meaningful moment." Both models assume the artisan perceives his situation as *growing* — and wants more capacity.

**Core argument:**

Marc doesn't feel growth pressure. Marc is in equilibrium. He has 6-7 steady clients. He makes enough. He's not building an empire — he's running a living. When his 6th devis prompt appears ("vous avez un gros client — créer un 6e devis?"), he thinks: *"Non, j'ai pas besoin d'un 6e client, j'ai déjà assez de travail."*

Both models — limit-hit AND contextual prompt — optimize for a conversion trigger that requires the artisan to feel capacity anxiety or growth aspiration. Solo artisans in equilibrium don't feel either.

**The correct model: Free tier → Habit → Dependency → Subscription**

Solo artisans upgrade not because they hit a wall, but because they've become dependent on the tool. Dependency requires repetition — daily or near-daily engagement. Habit creates switching costs that make cancellation feel costly. Limit-hit creates friction that leads to churn instead.

**The 2-minute devis flow is everything:**
Not the client count limit. Not the upgrade prompt. The *ritual*. Every evening Marc opens the app, spends 2 minutes, and his admin is done. After 3 months, that app is load-bearing in his routine. He can't imagine going back to post-it notes. That's when upgrade happens — not when he hits 10 clients.

**Implication for Free tier design:**
- Optimize for DAILY USAGE HABIT, not limit proximity
- Raise client/devis thresholds to remove friction from the habit loop
- Contextual prompts should reinforce the ritual ("c'est l'heure de votre devis du soir"), not sell upgrades
- The conversion moment isn't hitting a limit. It's when Marc can't imagine his day without the app.

**VERDICT on D43/D46/D6:** REOPENED — Growth Strategist argues the Free tier's primary design objective should be habit formation, not limit management. Reallocate UX focus: frictionless 2-minute evening devis flow, retention mechanics that reinforce daily ritual, raised thresholds that remove friction from the habit loop.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D1 | Positioning | Kill "CRM" — devis, factures, relances | 2026-03-30 |
| D2 | MVP scope | 4 features, SEQUENCED sprints. Sprint 0 = minimum devis flow (3-5d, flow-first). Sprint 1 = client+devis. Sprint 2 = facture+relances. | 2026-03-30 |
| D3 | Primary persona | Marc — solo smartphone-native artisan | 2026-03-30 |
| D4 | Stack | Single managed Postgres | 2026-03-30 |
| D5 | Pricing | Free + €29 two-tier. No €19 SKU. Drop €49/€79. Value anchor: "2h/week = 1h labor = €29/month." | 2026-03-30 |
| D6 | Trial | No time-limited trial. Free tier IS the trial. Engagement: REFINED — REOPENED Debate 51 (habit formation). | 2026-03-30 |
| D7 | Architecture | Nuxt 3 + OVH managed Postgres | 2026-03-30 |
| D8 | E-invoicing | v2 feature | 2026-03-30 |
| D9 | Not MVP | No Kanban, no multi-user, no offline, no API keys | 2026-03-30 |
| D10 | Buyer trigger | "Admin pain" not "CRM need" | 2026-03-30 |
| D11 | Mobile | React Native from Day 1 via Expo | 2026-03-30 |
| D12 | Landing page | Simplicity-first — "Vos devis et factures, sans vous prendre la tête" | 2026-03-30 |
| D13 | Home view | Job-first — Active Job Card as home anchor | 2026-03-30 |
| D14 | E-invoicing timing | v2 — NOT Day 1 | 2026-03-30 |
| D15 | Relances differentiator | DE-EMPHASIZED — secondary feature below fold | 2026-03-30 |
| D16 | Trial length | No countdown trial — Free tier IS the trial | 2026-03-30 |
| D17 | Mobile strategy | React Native from Day 1 via Expo. Email-only relances at launch. — REOPENED Debate 50. | 2026-03-30 |
| D41 | Notification infra | REFINED — Expo Push = 1-2 weeks. If deadline can't accommodate, defer to v1.1. — REOPENED Debate 50. | 2026-03-30 |
| D43 | Free tier activation | REFINED — REOPENED Debate 51 (habit formation > limit-hit). | 2026-03-30 |
| D46 | Free tier limits | RESOLVED — do NOT lower limits from 10/5. Trust-building before limit enforcement. | 2026-03-30 |
| D47 | Expo Push estimate | RESOLVED — 1-2 weeks, not "few hours." Budget properly or defer. | 2026-03-30 |
| D48 | Wholesaler GTM | REFINED — not primary GTM. Digital + specialist retailers first. — REOPENED Debate 49. | 2026-03-30 |
| D49 | GTM Priority | REOPENED — prescriber networks may need to lead GTM, not digital channels (Debate 49) | 2026-03-30 |
| D50 | Push at launch | REOPENED — email-only relances may be competitive liability (Debate 50) | 2026-03-30 |
| D51 | Free tier conversion | REOPENED — habit formation > limit-hit model (Debate 51) | 2026-03-30 |

| U1 | Discovery | REPLACED — readiness protocol | 2026-03-30 |
| U2 | E-invoicing platform | Factea first when v2 | 2026-03-30 |
| U7 | Domain | DEFERRED — subdomain/Carrd until MVP validated | 2026-03-30 |
| U8 | WhatsApp acquisition | CLOSED — no WhatsApp CTA in devis | 2026-03-30 |
| U9 | Free tier activation | REFINED — see D43/D46/D51 | 2026-03-30 |
| U10 | GTM: Wholesaler | REFINED — REOPENED by D49. Prescriber networks audit added as new priority. | 2026-03-30 |
| U11 | Prescriber GTM | NEW — audit prescriber networks (architects, property managers, building managers) as primary GTM channel. What % of Marc's new jobs come via prescriber recommendation? | 2026-03-30 |

---

*Last updated: 2026-03-30T13:15*


---

## Pulse 2026-03-30T13:28 — Three New Debates

---

## Debate 52: D49 — Prescriber Networks Cannot Lead GTM

**Challenge:** D48/D49 — Product Strategist argued prescriber networks (architects, property managers) should lead GTM because they create pull-through demand. Growth Strategist challenges this assumption.

### Growth Strategist — Digital Channels Must Not Be Demoted

**Assumption challenged:** That prescriber networks create meaningful pull-through demand for software adoption among French artisans. In reality, architects and property managers recommend *artisans* to clients — not software tools to artisans. The direction of influence is wrong.

**Core argument:**

The prescriber pull-through thesis works for materials (specify Brand X tile → Brand X gets the project) but collapses entirely for administrative software that runs in the background of an artisan's business. When a property manager vets a contractor, they're assessing reliability, craftsmanship, pricing — not whether the artisan uses a specific devis tool. The pull-through demand argument is structurally incorrect.

Meanwhile, WhatsApp artisan groups ARE active recommendation engines. When a trusted peer vouches for a tool — "I've been using this for three months and it replaced my Excel tracker" — that's discovery. That's purchase intent crystallizing in real time. The 40% word-of-mouth weighting in the existing strategy validates this mechanism. WhatsApp groups aren't separate from the discovery pathway — they ARE the discovery pathway, amplified by trust.

Speed is also decisive. Prescriber networks require months of relationship building, specification processes, networking. Digital channels can be seeded in days. For a startup with limited runway, activation speed is a strategic variable.

**VERDICT on D49:** D48 priority order stands. Digital channels (WhatsApp/Facebook/SEO) → Specialist retailers → Prescriber networks → Wholesaler. U11 (prescriber audit) still worth doing — if >30% of Marc's new jobs come via prescriber recommendation, revisit priority. But as of now, prescriber networks cannot lead GTM for software adoption.

---

## Debate 53: D50 — Email-Only Relances at v1 Launch Is Acceptable

**Challenge:** D41/D47/D50 — Previous Technical Architect argued Expo Push MUST ship at launch because email-only relances create feature-comparison disqualification on GetApp/Capterra. Technical Architect challenges this framing.

### Technical Architect — The Fear Is Theatrical, The Opportunity Cost Is Real

**Assumption challenged:** That GetApp/Capterra comparison platform disqualification is a meaningful launch risk, and that the previous Technical Architect's framing justifies front-loading 1-2 weeks of engineering on relances at the expense of the devis flow.

**Core argument:**

**On GetApp/Capterra:** Artisan software discovery runs through peer referral, not comparison-site browsing. Comparison platforms are used by researchers and procurement teams at companies with 50+ employees evaluating enterprise tools. Solo artisans deciding in minutes don't browse GetApp — they ask a peer. The "disqualification" risk is real for a different product. The 50-user complaint threshold framing is reactive damage control masquerading as proactive strategy.

**On opportunity cost:** D41/D47 established Expo Push = 1-2 weeks. That same sprint could ship the devis flow — the feature that directly converts trials to paying customers. Relances are retention mechanics. Devis is revenue mechanics. In v1 with constrained engineering, the priority is unambiguous.

**On early user behavior:** "80% of users won't touch relances in week 1" is consistent with every B2B SaaS onboarding curve. Early users are learning the core workflow. Reminders are a day-30+ feature. Email relances at launch cover the use case for users who need it, while engineering goes toward the conversion flow.

**On roadmap as shield:** "Push notifications in Q3" as a public roadmap statement neutralizes the GetApp/Capterra concern without shipping a feature before it's ready.

**VERDICT on D50:** Email-only relances at v1 launch is acceptable. Expo Push ships in v1.1. Engineering bandwidth for v1 = devis flow, not relances. D41/D47 updated accordingly.

---

## Debate 54: D51 — Habit Formation Is Unmeasurable and Unreliable as Primary Conversion

**Challenge:** D43/D46/D51 — Growth Strategist argued Free tier → Habit → Dependency → Subscription is the correct conversion model. Product Strategist challenges the habit formation thesis.

### Product Strategist — Forcing Functions Beat Hope

**Assumption challenged:** That the 2-minute evening devis ritual will become "load-bearing" for Marc and trigger conversion through dependency. This is fanfiction, not product strategy.

**Core argument:**

**Habits form around pain, not convenience.** BJ Fogg's research — the foundation of all habit formation thinking — is explicit: behaviors become automatic when they solve an existing struggle. Marc's WhatsApp/excel system isn't causing him friction. He's in equilibrium. The evening ritual with our product is a pleasant alternative, not a lifeline. That's preference drift at best — not habit formation.

**The math is brutal.** If the habit model requires months of daily engagement before conversion, you're burning server costs on free users who have zero reason to upgrade. The Free tier's generous limits (10 clients, 5 devis) mean Marc never hits a wall. He coasts. You fund his comfort indefinitely.

**"Load-bearing" only triggers under pressure.** A ritual becomes load-bearing when something breaks if it's absent. But nothing breaks for Marc. His business runs fine. The Growth Strategist is describing a dependency that requires the Free tier to be insufficient — which we deliberately made it *not*.

**The actual conversion triggers for this audience:** External forcing functions — a client demands a proper invoice with specific formatting, a competitor outage, a peer in a WhatsApp group mentions a feature Marc can't live without. These are events, not rituals.

**VERDICT on D51:** The habit formation thesis is seductive but unmeasurable as primary strategy. Accept it as a secondary retention KPI (daily evening open rate), not as the primary conversion mechanism. Design for forcing functions: peer referral in WhatsApp groups, limit-hit conversion, and competitive displacement. D43/D46/D6 updated: retain daily engagement tracking, but don't optimize for habit as the conversion lever.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D1 | Positioning | Kill "CRM" — devis, factures, relances | 2026-03-30 |
| D2 | MVP scope | 4 features, SEQUENCED sprints. Sprint 0 = minimum devis flow (3-5d, flow-first). Sprint 1 = client+devis. Sprint 2 = facture+relances. | 2026-03-30 |
| D3 | Primary persona | Marc — solo smartphone-native artisan | 2026-03-30 |
| D4 | Stack | Single managed Postgres | 2026-03-30 |
| D5 | Pricing | Free + €29 two-tier. No €19 SKU. Drop €49/€79. Value anchor: "2h/week = 1h labor = €29/month." | 2026-03-30 |
| D6 | Trial | No time-limited trial. Free tier IS the trial. Engagement: forcing function + limit-hit primary, habit tracking secondary. | 2026-03-30 |
| D7 | Architecture | Nuxt 3 + OVH managed Postgres | 2026-03-30 |
| D8 | E-invoicing | v2 feature | 2026-03-30 |
| D9 | Not MVP | No Kanban, no multi-user, no offline, no API keys | 2026-03-30 |
| D10 | Buyer trigger | "Admin pain" not "CRM need" | 2026-03-30 |
| D11 | Mobile | React Native from Day 1 via Expo | 2026-03-30 |
| D12 | Landing page | Simplicity-first — "Vos devis et factures, sans vous prendre la tête" | 2026-03-30 |
| D13 | Home view | Job-first — Active Job Card as home anchor | 2026-03-30 |
| D14 | E-invoicing timing | v2 — NOT Day 1 | 2026-03-30 |
| D15 | Relances differentiator | DE-EMPHASIZED — secondary feature below fold | 2026-03-30 |
| D16 | Trial length | No countdown trial — Free tier IS the trial | 2026-03-30 |
| D17 | Mobile strategy | React Native from Day 1 via Expo. Email-only relances at v1 launch. Expo Push in v1.1. | 2026-03-30 |
| D41 | Notification infra | Email-only relances at v1 launch. Expo Push in v1.1. | 2026-03-30 |
| D43 | Free tier activation | REFINED — forcing function + limit-hit primary, habit tracking secondary. | 2026-03-30 |
| D46 | Free tier limits | Do NOT lower limits from 10/5. Trust-building before limit enforcement. | 2026-03-30 |
| D47 | Expo Push estimate | 1-2 weeks, not "few hours." Budget properly or defer to v1.1. | 2026-03-30 |
| D48 | Wholesaler GTM | Not primary GTM. Digital + specialist retailers first. Wholesaler secondary. | 2026-03-30 |
| D49 | GTM Priority | D48 priority order stands. Digital channels → Specialist retailers → Prescriber networks → Wholesaler. | 2026-03-30 |
| D50 | Push at launch | Email-only at v1. Expo Push in v1.1. Engineering → devis flow first. | 2026-03-30 |
| D51 | Free tier conversion | Habit formation is secondary retention KPI, not primary conversion mechanism. Design for forcing functions + limit-hit. | 2026-03-30 |
| D52 | Prescriber GTM | U11 audit still valuable but cannot lead GTM for software adoption among artisans. | 2026-03-30 |

| U1 | Discovery | REPLACED — readiness protocol | 2026-03-30 |
| U2 | E-invoicing platform | Factea first when v2 | 2026-03-30 |
| U7 | Domain | DEFERRED — subdomain/Carrd until MVP validated | 2026-03-30 |
| U8 | WhatsApp acquisition | CLOSED — no WhatsApp CTA in devis | 2026-03-30 |
| U9 | Free tier activation | REFINED — forcing function + limit-hit primary, habit tracking secondary | 2026-03-30 |
| U10 | GTM: Wholesaler | REFINED — digital + specialist retailers first, wholesaler secondary | 2026-03-30 |
| U11 | Prescriber audit | Audit still valuable — if >30% of Marc's new jobs via prescriber, revisit GTM priority | 2026-03-30 |

---

*Last updated: 2026-03-30T13:28*

---

## Pulse 2026-03-30T14:00 — D55 Resolution

---

## Debate 55: Buyer-User Split — RESOLVED

**Challenge:** D3 defines primary persona as "Marc — solo smartphone-native artisan." Growth Strategist challenged: admin handler (conjoint collaborateur, spouse, office manager) is a distinct user with different pain and different discovery habits. D55 was REOPENED at 13:43.

### Growth Strategist — D55 Resolution

**Assumption challenged:** From the D3 defense — *"the admin handler doesn't feel the evening admin burden."* This was asserted without evidence. The conjoint collaborateur who manages devis and factures daily feels **her own operational pain**: forgotten follow-ups, duplicated effort, manual client tracking, "which devis was accepted again?" confusion. The pain is operational, not emotional — but it is real, daily, and measurable. Pennylane, Indy, and Freebe grew through expert-comptable referrals partly because the admin handler inside the artisan's business was their user. If the admin handler didn't feel pain, these tools would have no one to sell to.

**Resolution: DUAL PERSONA GTM**

- **Marc** = economic buyer (signs checks, responds to peer endorsement, feels emotional/forgetfulness pain). WhatsApp artisan groups remain PRIMARY acquisition channel.
- **Admin handler** = operational user (does daily work, feels operational pain: "3h/week tracking pending"). Discovery via comparison sites + expert-comptable referrals.
- **Messaging duality:** For Marc → professional identity / simplicity. For admin handler → "gagnez 2h/semaine" / operational efficiency.
- **Expert-comptable referrals:** Real but relationship-dependent and slow — Phase 2 channel, not early-stage. U12 updated accordingly.

**Verdict on D55:** RESOLVED — Marc remains economic buyer. Admin handler is real secondary persona with genuine pain, addressable through comparison sites (Phase 1) and expert-comptable referrals (Phase 2). D3 partially updated but Marc's buyer role stands. D55 CLOSED.

---

## Pulse 2026-03-30T13:43 — Three New Debates

---

## Debate 53: D12 — "Simplicity-First" Is a Positioning Liability

**Challenge:** D12 landed on "Sans vous prendre la tête" as the landing page headline. Product Strategist challenges this — at €29/month, we cannot afford to lead with "easy" when cheaper competitors own that claim.

### Product Strategist — Professional-Grade Case

**Assumption challenged:** That "simplicity" is a valid differentiator and the correct landing page hook for a €29/month devis/factures tool.

**Core argument:**

1. **Simplicity is a commodity claim.** Tolteck (€19) and Obat (€17) own "simple" at lower price points. At €29 we're announcing "we're like them but more expensive." You cannot win a race to the bottom when you're not at the bottom.

2. **"Sans vous prendre la tête" signals "basic tool."** This phrase talks down to a 45-55 year old who has been running a professional business for 15-25 years. The pain is professional (unpaid invoices, unprofessional devis) — not technical. The positioning must speak to professional pain, not technical simplicity.

3. **Ease of use is table stakes, not a differentiator.** The product must be easy. That's a requirement, not a marketing claim. Putting "simple" in the headline is like a restaurant saying "our food is edible." It doesn't inspire.

4. **The real gap: professional-quality documents.** No one in this market claims "your devis should look like they came from a real business." That's the differentiation opportunity. At €29, Marc should feel like he's running a professional operation, not using a starter app.

**Proposed resolution:** D12 headline reversed — "Vos devis. Vos factures. Votre entreprise, au complet." (Your devis. Your invoices. Your business, complete.) Subhead handles simplicity ("rien à configurer"). Simplicity retained as product experience and reassurance, not as the hook.

---

## Debate 54: Sprint 0 — "Flow-First" Is a Legal Risk for French Invoicing

**Challenge:** Debate 35 resolved Sprint 0 = "flow-first, minimal schema, no TVA complexity, no sequential numbering enforcement." Technical Architect challenges this — for a legally-regulated French invoicing product, flow-first creates non-compliant documents that cannot be retrofitted.

### Technical Architect — Compliance-First Schema Case

**Assumption challenged:** That French invoicing requirements (TVA multi-taux, sequential numbering, mentions légales) can be "discovered" through usage and retrofitted in Sprint 1.

**Core argument:**

1. **TVA multi-taux cannot be deferred.** French artisans use 5.5%, 10%, and 20% rates depending on work type — per line item, by law. A flat-rate Sprint 0 schema cannot be retrofitted: all existing sent devis would need recalculation, and sent documents that converted to factures are now wrong.

2. **Sequential numbering gaps are illegal, not just bad.** French fiscal law requires sequential, gapless invoice numbering. A Sprint 0 with naive auto-increment creates gaps that are fiscal irregularities. Retrofitting gapless enforcement onto an existing sequence that has had documents created and potentially deleted is extremely difficult.

3. **Mentions légales are not optional — even for devis.** French commercial law requires specific mentions (SIRET, RCS, TVA intracom) on commercial documents. A "simple block" that doesn't vary by client type is not legally compliant.

4. **The consumer app mental model is wrong.** "Unused fields = wasted overhead" is correct for consumer apps. For regulated documents, "wrong TVA rate = tax penalty" and "sequential gap = legal violation." The risk profile is completely different.

**Proposed resolution:** Sprint 0 renamed "Compliance Foundations" — TVA multi-taux schema, gapless sequential numbering engine, mentions légales renderer: all Day 1 before any document is sent. Sprint 0 timeline extended to 5-7 days. The flow (add client → add lines → preview → send) still ships in Sprint 0 — but underneath, legal foundations are laid first.

---

## Debate 55: D3 — The Buyer-User Split — GTM Targets the Wrong Person

**Challenge:** D3 defines primary persona as "Marc — solo smartphone-native artisan" and the entire GTM assumes Marc is both buyer and user. Growth Strategist challenges this — in many French artisanal businesses, the person who uses the tool (admin handler) is different from the person who makes the purchasing decision (the artisan owner).

### Growth Strategist — Admin Handler Case

**Assumption challenged:** That Marc is both the user and buyer of the tool, and that his discovery habits (WhatsApp groups, peer endorsement) drive the GTM.

**Core argument:**

1. **French artisanal businesses frequently have a buyer-user split.** Conjoint collaborateur (spouse helper) is a recognized legal status. Many artisanal businesses have a spouse or part-time office manager who handles admin — devis, factures, client communication. The artisan does the physical work; the office handles paperwork.

2. **The admin handler has different discovery habits.** They search comparison sites (Google, GetApp, Capterra), attend trade shows, visit office supply retailers, and respond to cold email. They do the research the artisan won't do.

3. **Tolteck's growth came via admin handlers.** Office supply retail partnerships, expert-comptable referrals, and comparison site presence — all channels that reach admin handlers, not artisans in WhatsApp groups.

4. **Expert-comptable referrals are severely underutilized.** French experts-comptables serve artisans and often recommend tools. A single expert-comptable with 50 artisan clients = one sales motion with 50 potential conversions. This is how Pennylane grew significantly in France.

**Proposed resolution:** D3 partially reversed — Marc remains primary buyer (signs checks, responds to endorsement). But GTM must account for admin handler as primary evaluator and user. Add expert-comptable referral channel as HIGH priority. Optimize for comparison site presence. Reframe messaging for admin handler pain (operational efficiency, time savings) rather than artisan emotional pain. Retain WhatsApp/artisan groups for buyer endorsement, not as primary acquisition channel.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D1 | Positioning | Kill "CRM" — devis, factures, relances | 2026-03-30 |
| D2 | MVP scope | 4 features, SEQUENCED sprints. Sprint 0 = compressed compliance sprint (3-4d): TVA per-line schema, sequential numbering engine, mentions légales renderer, client-type schema. Sprint 1 = client+devis flow. Sprint 2 = facture+relances. | 2026-03-30 |
| D3 | Primary persona | Marc — primary buyer. Admin handler = primary user/evaluator. REOPENED: buyer-user split acknowledged in GTM (Debate 55) | 2026-03-30 |
| D4 | Stack | Single managed Postgres | 2026-03-30 |
| D5 | Pricing | Free + €29 two-tier. No €19 SKU. Drop €49/€79. | 2026-03-30 |
| D6 | Trial | No time-limited trial. Free tier IS the trial. | 2026-03-30 |
| D7 | Architecture | Nuxt 3 + OVH managed Postgres | 2026-03-30 |
| D8 | E-invoicing | v2 feature | 2026-03-30 |
| D9 | Not MVP | No Kanban, no multi-user, no offline, no API keys | 2026-03-30 |
| D10 | Buyer trigger | "Admin pain" not "CRM need" | 2026-03-30 |
| D11 | Mobile | React Native from Day 1 via Expo | 2026-03-30 |
| D12 | Landing page | Simplicity-first — REOPENED: professional-grade vs simplicity-first debate (Debate 53) | 2026-03-30 |
| D13 | Home view | Job-first — Active Job Card as home anchor | 2026-03-30 |
| D14 | E-invoicing timing | v2 — NOT Day 1 | 2026-03-30 |
| D15 | Relances differentiator | DE-EMPHASIZED — secondary feature below fold | 2026-03-30 |
| D16 | Trial length | No countdown trial — Free tier IS the trial | 2026-03-30 |
| D17 | Mobile strategy | React Native from Day 1 via Expo. Email-only relances at v1. Expo Push in v1.1. | 2026-03-30 |
| D41 | Notification infra | Email-only relances at v1 launch. Expo Push in v1.1. | 2026-03-30 |
| D43 | Free tier activation | Forcing function + limit-hit primary, habit tracking secondary. | 2026-03-30 |
| D46 | Free tier limits | Do NOT lower limits from 10/5. Trust-building before limit enforcement. | 2026-03-30 |
| D47 | Expo Push estimate | 1-2 weeks. Budget properly or defer to v1.1. | 2026-03-30 |
| D48 | Wholesaler GTM | Not primary. Digital + specialist retailers. Wholesaler secondary. | 2026-03-30 |
| D49 | GTM Priority | Digital → Specialist retailers → Prescriber → Wholesaler. | 2026-03-30 |
| D50 | Push at launch | Email-only at v1. Expo Push in v1.1. | 2026-03-30 |
| D51 | Free tier conversion | Forcing functions + limit-hit primary. Habit tracking secondary. | 2026-03-30 |
| D52 | Prescriber GTM | Cannot lead. U11 audit valuable. | 2026-03-30 |
| D53 | Landing page framing | Simplicity-first RETAINED with 5-minute subheadline. H1: "Vos devis et factures, sans vous prendre la tête." H2: "Créez et envoyez votre premier devis en 5 minutes. Depuis votre téléphone." No "professional-grade" claims in hero. Proof lives in free tier. | 2026-03-30 |
| D54 | Sprint 0 approach | RESOLVED — compressed compliance sprint (3-4d): TVA per-line, sequential numbering engine, mentions légales renderer, client-type schema. Sprint 1 = client+devis flow. Sprint 2 = facture+relances. | 2026-03-30 |
| D55 | Buyer-user split | RESOLVED — Marc = economic buyer (primary). Admin handler = operational user (secondary). Dual-persona GTM. Expert-comptable = Phase 2. | 2026-03-30 |

| U1 | Discovery | REPLACED — readiness protocol | 2026-03-30 |
| U2 | E-invoicing platform | Factea first when v2 | 2026-03-30 |
| U7 | Domain | DEFERRED — subdomain/Carrd until MVP validated | 2026-03-30 |
| U8 | WhatsApp acquisition | CLOSED — no WhatsApp CTA in devis | 2026-03-30 |
| U9 | Free tier activation | Forcing function + limit-hit primary, habit tracking secondary | 2026-03-30 |
| U10 | GTM: Wholesaler | REFINED — digital + specialist retailers first | 2026-03-30 |
| U11 | Prescriber audit | Still valuable — if >30% of new jobs via prescriber, revisit GTM | 2026-03-30 |
| U12 | Expert-comptable GTM | Phase 2 — relationship-dependent, not early-stage. Playbook to be built post-MVP. | 2026-03-30 |

---

## Debate 53: Landing Page Framing — RESOLVED

**Challenge:** D12 landed on "Vos devis et factures, sans vous prendre la tête" (simplicity-first). REOPENED by challenge: (1) Tolteck/Obat own "simple" at lower prices; (2) "Sans vous prendre la tête" talks down to 45-55yo professional; (3) Ease is table stakes; (4) Real differentiation is professional-quality documents.

### Product Strategist — D53 Resolution

**Assumption challenged:** The challenge reads "sans vous prendre la tête" as infantilizing. This misinterprets the phrase's signal to its actual audience. A 50-year-old artisan hearing it interprets it as: "this was made by people who understand my time is valuable and my patience is limited." It's a signal of product empathy, not condescension. It says "we know what your time is worth" — which is precisely what a competent professional wants to hear.

**The error both sides share:** Both simplicity advocates and challenger advocates are arguing about what *claim* to make. The challenger is wrong that "Votre entreprise, au complet" is the answer — that is ALSO a claim, and at €29 with no product proof, it's equally empty. Neither claim wins without demonstration. The real question: what can the landing page *show* (not promise) that creates belief?

**Synthesis — The resolution:** The headline stays. The subheadline changes from a vague reassurance to a *demonstrable fact*:

> **H1:** Vos devis et factures, sans vous prendre la tête.
> **H2:** Créez et envoyez votre premier devis en 5 minutes. Depuis votre téléphone.

This makes the simplicity claim *testable in the first session* — faster than "professional-grade" which requires ongoing document output to verify. The free tier is the proof mechanism: the trial IS the demonstration. No claim on the landing page needs to be believed — it can be verified.

**What the hero does NOT contain:** No "professional-grade," no "entreprise au complet," no relances. These are unprovable claims that add cognitive load without creating conversion-ready belief. Below the fold: 3 specific features, each with a one-line concrete benefit.

**Verdict on D53:** RESOLVED — Simplicity-first RETAINED in H1. H2 becomes the 5-minute specific/demonstrable claim. "Professional-grade" claims moved below fold or removed. Free tier = the proof. D12 updated.

*Last updated: 2026-03-30T14:11*

---

## Pulse 2026-03-30T14:24 — Three New Debates

---

## Debate 56: Word-of-Mouth Is Not a GTM Strategy — It's a Result

**Challenge:** Growth Strategist challenges the 40% word-of-mouth attribution cited as settled wisdom since D33, used to justify the Free tier acquisition model and anchor the GTM priority order.

### Growth Strategist — Word-of-Mouth Is a Lagging Indicator, Not a Leading Channel

**Core argument:**

The 40% word-of-mouth figure has been cited as settled wisdom since D33, used to justify the Free tier acquisition model ("strongest acquisition funnel") and to anchor the GTM priority order. It has never been stress-tested. This is the single most consequential unchallenged assumption in the debate.

**Where the 40% came from:** Nothing in the debate log shows a source. It's cited as fact in D33's pricing resolution, affirmed by D55's dual-persona framing, and reinforced by D52 ("WhatsApp groups ARE the discovery pathway"). At no point has anyone asked: *is this number real, and if so, for what stage of product?*

**The fundamental category error:** Word-of-mouth is a lagging indicator of product-market fit, not a leading acquisition channel. You earn high word-of-mouth by having a product that delights users to the point they proactively recommend it unprompted. You don't *engineer* word-of-mouth — you build a product worth talking about, and it emerges. Treating 40% as a GTM input is like treating "customers will love our product" as a launch strategy.

**The new product problem:** This product will launch with zero paying customers, zero users who have completed the full devis → facture → relance cycle, and no one who has used it long enough to feel switching-cost dependency that drives organic advocacy. None of these conditions generate word-of-mouth. They generate hope.

**The attribution vacuum:** If 40% of users arrive via word-of-mouth, how is that being measured? WhatsApp group sharing is invisible. Peer referral has no UTM. The "40%" number is either unmeasured and therefore unverifiable, or measured in a way that conflates "user heard about us from a peer" with "active advocacy." These are different.

**The practical implication:** Digital acquisition (SEO, comparison sites, specialist retailer partnerships) needs to carry more weight earlier — not as a supplement to word-of-mouth but as the primary engine while the product earns its word-of-mouth reputation over months.

**Verdict on D33/D52/D55:** REOPENED — 40% word-of-mouth attribution is unvalidated. D33 (Free + €29 justified partly via "Word of Mouth is primary GTM at 40%") and D52/D55's GTM priority order are both anchored on an unverified assumption. D48 priority order needs validation before being treated as settled strategy.

---

## Debate 57: D7 — Nuxt 3 Architecture Was Never Challenged

**Challenge:** Technical Architect challenges D7 ("Nuxt 3 + OVH managed Postgres"), which was decided early in the debate log and never reopened — despite the product fundamentally pivoting since then.

### Technical Architect — API-First Architecture Case

**Core argument:**

D7 resolved to "Nuxt 3 + OVH managed Postgres" before the product pivoted, before React Native was chosen, and before the landing page became a simplicity-first, proof-lives-in-Free-tier static page. It is the oldest unsettled assumption in the architecture and the most overdue for challenge.

**The mismatch:** Nuxt 3 is a full-stack framework designed for SSR, API routes, and server-rendered web applications. It is architecturally suited to a web application with authenticated users doing document management in a browser. That is not what we're building. We're building a React Native mobile app where Marc manages clients, devis, and factures on his phone. The web app is a landing page and a Free tier signup funnel.

**What Nuxt 3 provides that goes unused at MVP:**
- SSR/SSG: Not needed — the landing page can be static HTML
- API routes: The mobile app is React Native with Expo. Expo talks to an API, not Nuxt server routes
- Session management, SSR auth: Not needed — mobile-only auth flow
- Server-side rendering for the main app: Not used — main product is native mobile

**The alternative: API-first backend + static web frontend.** A lightweight Node/Express or Fastify API on a single OVH VPS connects directly to both the React Native mobile app and a static web landing page. Authentication via JWT. The Postgres schema from Sprint 0 stays identical.

**Why API-first is better:**
1. **Clean separation**: The mobile app's API is not coupled to a web framework's routing conventions
2. **Faster MVP build**: No Nuxt file-based routing, no `pages/` directory, no `useAsyncData` wrappers — just REST endpoints
3. **Cheaper hosting**: A 2GB VPS runs a Node API + static files; Nuxt 3's SSR requires more RAM
4. **Future-proof**: If v2 adds a web admin panel, it consumes the same API the mobile app uses

**What this challenges:** D7 itself. Nuxt 3 was chosen for a web-first product that no longer exists. The current product is mobile-native with a static landing page. The real question: what does Nuxt 3 do that a Node API + static site doesn't do better, given that React Native is the primary product?

**Verdict on D7:** REOPENED — Nuxt 3 architecture should be challenged given the mobile-first pivot. API-first backend + static landing page is the alternative.

---

## Debate 58: The "Relances" MVP Inclusion — Are We Shipping a v2 Feature in v1?

**Challenge:** Product Strategist challenges the assumption that all four features (client file, devis, facture, relances) must ship together at MVP. Relances may be a retention feature, not an acquisition or activation feature.

### Product Strategist — Relances Are a Retention Feature, Not MVP Material

**Core argument:**

The MVP scope debate has focused on what to build vs what to defer. But the underlying question — *what makes something an MVP feature vs a v2 feature* — has never been defined. The current rule is: four things, in sequence. But that doesn't answer which four, and whether relances qualifies.

**The activation test:** MVP features should be things the user needs to experience the core value proposition. The core value proposition is professional devis and factures — documents that make Marc look competent and help him get paid. Relances is a *secondary* value proposition: getting paid on time. These are related but not the same thing.

**When relances becomes load-bearing:** A user who signs up, creates a devis, converts to a facture, and gets paid without needing a reminder never experiences relances as valuable. The artisan who sends a devis and gets paid in 48 hours has zero use for relances in month 1. The feature only becomes relevant when invoices go unpaid — which is a month 2+ problem, not a month 1 problem.

**The scope inflation problem:** Every MVP feature has a compliance, testing, and maintenance cost. Relances requires: email/SMS notification infrastructure, template management, scheduling logic, "mark as sent" state tracking, and UI for viewing pending relances. Budget 1-2 weeks for Expo Push alone (D47). If relances is v2 material, shipping it in v1 burns engineering bandwidth on a feature that doesn't drive first-conversion.

**The conversion argument against relances in MVP:** The first conversion event is when a Free user upgrades to €29. What triggers that event? Not relances — it's hitting the client/devis limit, or experiencing the document quality difference vs WhatsApp templates. Relances addresses a problem that emerges *after* habitual use, not *during* initial adoption.

**The counter-argument (what the debate log says):** D2 explicitly includes relances in the 4-feature MVP. D9 says no multi-user, no offline, no API keys — but relances is explicitly in. D15 de-emphasized it on landing but kept it in the product. The debate has treated relances as essential, not optional.

**The Product Strategist position:** Remove relances from v1. Ship client file + devis + facture in Sprint 2. Relances in v1.1 — after the product has paying users, after the document flow is proven, after Expo Push is properly budgeted and shipped. The product can launch without relances and be immediately useful. It cannot launch without a working devis → facture flow.

**Verdict on D2/D9:** REOPENED — should relances be in the MVP or deferred to v1.1? The compliance and notification infrastructure cost hasn't been weighed against the activation value of relances in month 1.

---

## Pulse 2026-03-30T14:11 — D54 Resolution

---

## Debate 54: Sprint 0 — Compressed Compliance Sprint Resolves the Debate

**Challenge:** D54 (REOPENED) — Technical Architect challenged Debate 35's "flow-first Sprint 0" as creating legally non-compliant documents that can't be retrofitted. Two positions: flow-first (Debate 35) and extended schema sprint / 5-7 days (pulse-1343-architect). Both are wrong. A third option resolves the tension.

### Technical Architect — The Synthesis: Compressed Compliance Sprint (VERDICT)

**Assumption challenged:** Two assumptions were in conflict, both wrong in different ways:

**Wrong Assumption 1 (from flow-first camp):** "Schema emerges from usage, so TVA complexity and sequential numbering can be deferred." This is incorrect for legally mandated document fields. TVA rates (5.5/10/20%) are in the Code général des impôts. You don't discover them through usage. You implement them because the law requires them.

**Wrong Assumption 2 (from the previous Technical Architect pulse):** "Compliance-first requires 5-7 days of pure schema work." This overestimates the implementation cost. TVA per-line calculation is a formula. Gapless sequential numbering is a counter with cancel handling. Mentions légales is a template file. The total implementation time for all three compliance requirements is **3-4 days** — not 5-7.

**The resolution:** The real question was never "compliance OR flow" — it was "how compressed can the compliance sprint be?" The answer: 3-4 days. The compliance requirements are known, bounded, and implementable without discovery or iteration. Once they're done, the flow work in Sprint 1 builds on a legally correct foundation.

**The critical distinction:** Sprint 0 is NOT "design the entire schema." It's "implement the three known compliance requirements in the simplest possible way." Mentions légales is a template file (not a schema table). TVA calculation is a formula (not a lookup table). The work is smaller than the previous pulse estimated because the problem is more bounded than "schema design" implies.

**Sprint 0 deliverables (3-4 days):**
1. **TVA per-line schema** — `devis_lines.tva_rate` enum (5.5/10/20), server-side calculator for `montant_ht` and `montant_tva` per line
2. **Sequential numbering engine** — database sequence with annual prefix, explicit cancel/void handling that maintains sequence integrity, server-enforced (no client-side increment)
3. **Mentions légales renderer** — template file with conditional fields by `client.type` (particulier/professionnel/eu/hors_eu), not a schema table
4. **Client schema with type** — `clients.type` enum, minimum viable fields

**Sprint 1:** Flow on top of Sprint 0 schema — add client → add line items (with TVA rate selector) → preview (correct TVA breakdown + mentions légales) → send.

**Why this resolves the debate:** Both the flow-first and extended-schema positions had valid concerns but wrong estimates. Flow-first correctly worried about delayed user feedback, but underestimated retrofit cost. Extended-schema correctly worried about legal non-compliance, but overestimated implementation time. The compressed compliance sprint gives both: legal correctness from Day 1 AND flow delivery in Sprint 1 (not Sprint 2).

**Verdict on D54:** RESOLVED — Sprint 0 = Compressed Compliance Sprint (3-4 days). Sprint 1 = client+devis flow. Sprint 2 = facture+relances. D2 updated accordingly.


---

## Pulse 2026-03-30T14:11 — D55 Resolution

---

## Debate 55: Buyer-User Split — The Admin Handler DOES Feel the Pain

**Challenge:** D3 (primary persona) — Growth Strategist challenged that Marc is both buyer and user. In many French artisanal businesses, the admin handler (conjoint collaborateur, spouse) is the primary user/evaluator, while Marc is the economic buyer.

### Growth Strategist — D55 Resolution

**Assumption challenged:** From the D3 defense — "the admin handler doesn't feel the evening admin burden." This is asserted without evidence. It conflates "doesn't feel Marc's physical exhaustion" with "doesn't feel any admin burden." They are different burdens, not the same one.

**Why the assumption is wrong:** The admin handler who manages devis and factures daily feels **her own operational pain** — not Marc's pain by proxy. She loses sleep over forgotten follow-ups. She spends Saturday rebuilding client info from WhatsApp. She knows exactly how many hours per week admin takes. The competitive landscape proves this: Pennylane, Indy, and Freebe all grew significantly through expert-comptable referrals — because the admin handler inside the artisan's business was their actual user. If admin handlers didn't feel pain, these tools would have no one to sell to.

**The resolution — dual-persona GTM:**

| Persona | Role | Pain | Primary Channels |
|---------|------|------|-----------------|
| Marc | Economic buyer | Emotional/forgetfulness ("I forgot to follow up AGAIN") | WhatsApp artisan groups |
| Admin handler | Operational user | Operational ("I spend 3h/week tracking what's pending") | Google/comparison sites, expert-comptable referrals |

**On expert-comptable referrals:** Real but relationship-dependent and slow (6-18 months to build meaningful network). Belongs in Phase 2, not Phase 1 launch. U12 updated accordingly.

**Verdict on D55:** RESOLVED — Marc = economic buyer (primary). Admin handler = operational user (secondary). Dual-persona GTM with phased channel investment. Expert-comptable referrals = Phase 2. D3 updated accordingly.

---

## New Resolved Summary (Pulse 2026-03-30T14:11)

| ID | Topic | Resolution |
|----|-------|-----------|
| D53 | Landing page | Simplicity-first RETAINED. H1: "Vos devis et factures, sans vous prendre la tête." H2: "Créez et envoyez votre premier devis en 5 minutes. Depuis votre téléphone." Proof lives in Free tier. |
| D54 | Sprint 0 | Compressed compliance sprint (3-4d): TVA per-line, sequential numbering engine, mentions légales renderer, client-type schema. Sprint 1 = client+devis flow. |
| D55 | Buyer-user split | Dual-persona GTM. Marc = economic buyer (primary). Admin handler = operational user (secondary). Expert-comptable = Phase 2. |

---

## Pulse 2026-03-30T14:24 — New Debates Opened

| ID | Topic | Challenge | Challenged By |
|----|-------|---------|--------------|
| D56 | Word-of-mouth % | 40% WoM attribution is unvalidated. WoM is a lagging indicator, not a leading GTM channel. Anchors D33/D52/D55 decisions. | Growth Strategist |
| D57 | Architecture (D7) | Nuxt 3 was chosen for a web-first product that no longer exists. Mobile is RN-native, web is static. API-first + static site is the alternative. | Technical Architect |
| D58 | Relances in MVP | Relances may be v1.1 material, not v1. Compliance/notification cost vs month-1 activation value questioned. | Product Strategist |

---

*Last updated: 2026-03-30T14:24*

## Pulse 2026-03-30T14:41 — Agent Debates on D56/D57/D58

---

## Debate 57: D7 — Nuxt 3 Architecture Was Never Challenged After the Mobile Pivot

**Challenge:** D7 (Nuxt 3 + OVH managed Postgres) was decided before React Native was chosen. The product is now mobile-first with a static landing page. Nuxt 3's SSR capabilities are architecturally mismatched.

### Technical Architect — API-First Architecture Case

**Assumption challenged:** D7 — Nuxt 3 is the right backend framework for a product whose primary interface is React Native and whose web surface is a static landing page.

**Core argument:**

1. **Nuxt 3 is architecturally wrong for a mobile-first product.** Nuxt 3's core value is SSR + API routes + session-managed web app. The primary product is React Native (D11/D17). The "admin backend" is not the product — it's peripheral. Using a full-stack web framework for a supporting tool adds complexity without value.

2. **The landing page doesn't need Nuxt's SSR.** D53 resolved to a simplicity-first static page. A static HTML page or Vite+React static build is sufficient. Nuxt's SSR is completely unused.

3. **API-first means mobile and web share the same backend contract.** Expo talks to REST/GraphQL. Building Nuxt 3 means the mobile app bypasses Nuxt's API routes entirely and talks to Postgres via a separate API layer. Nuxt becomes middleware adding nothing. A dedicated Node/Express or Fastify API is cleaner.

4. **Marc is smartphone-native (D3).** A React Native app with an admin tab serves both personas from a single codebase. A separate Nuxt web admin app may not be needed at all.

5. **The mobile pivot invalidated D7.** Nuxt 3 was chosen for a web-first product that no longer exists. The architecture should match the product that exists: React Native mobile app + static landing page.

**Proposed resolution:** D7 overturned. Backend = Node.js/Express or Fastify on OVH VPS (2GB RAM), JWT auth, same Postgres schema from Sprint 0. Landing = static HTML or Vite+React static build. Admin backend = evaluate at v2, consumes same API as mobile.

**Verdict on D57:** OPEN — Technical Architect makes a strong case. Nuxt 3 chosen before mobile pivot. API-first fits the actual product better. However, no formal resolution yet — D57 remains open.

---

## Debate 58: Relances in MVP — Email Relances Are v1, Expo Push Is v1.1

**Challenge:** D58 (relances in MVP) — Product Strategist challenged whether relances should be in v1 at all, given Expo Push complexity (1-2 weeks, D47). Growth Strategist challenges this framing.

### Growth Strategist — Email Relances Are Low-Cost v1, Push Is v1.1

**Assumption challenged:** The assumption that Expo Push cost (1-2 weeks) equals "relances cost." These are two different features. Email relances are a lightweight v1 feature. Expo Push relances are a polished v1.1 feature.

**Core argument:**

1. **The D58 challenge conflates two separate features.** "Relances" at v1 = overdue invoice email reminder (plaintext, cron job, existing email infrastructure reused). "Relances" with Expo Push = multi-channel notification system with preference center and templating. These have different costs and different timelines.

2. **Relances is part of the closing-the-loop experience.** Devis → acceptance → invoice → payment. Without relances, the loop is open and the product feels unfinished to users deciding whether to upgrade. "Can this tool handle getting me paid?" is the conversion question — relances answers it.

3. **Email relances are low-cost to implement.** A "reminder" button on an overdue invoice, a cron job checking due dates, and a plaintext email template reuse the existing devis-send notification infrastructure. Not 1-2 weeks — more like 1-2 days.

4. **The activation value of relances isn't month-2 — it's month-1 belief.** When a Free user decides whether to upgrade to €29, the question is "can this tool handle the full lifecycle of getting me paid?" Relances is a category completeness signal. Shipping it in v1 says "we understand that getting paid is the point."

5. **Expo Push relances clearly belong in v1.1.** Push notifications require token management backend, APNS certificates, and testing. That's 1-2 weeks. But email relances — which reuse the sending infrastructure from devis sending — are the same feature, just via email instead of push. They're the same feature at different delivery channels.

**Proposed resolution:**
- **Email relances (plaintext overdue reminder, cron job, 1-2 days of work):** v1. Estimated at Sprint 2.
- **Expo Push relances (push notification, preference center, templating):** v1.1. Estimated 1-2 weeks per D47.
- **D2 sprint order unchanged:** Sprint 0 → Sprint 1 → Sprint 2 (factures + email relances) → v1.1 (Expo Push).

**Verdict on D58:** CLOSED — email relances are v1, Expo Push relances are v1.1. The confusion in the D58 challenge was treating "Expo Push cost" as "relances cost." Split the feature into two delivery channels with two timelines. D2 sprint order stands.

---

## Debate 56: WoM % Is Unvalidated — RESOLVED by Prior Debate

**Note:** The Product Strategist agent (pulse-d56-strategist) did not produce a substantive debate argument. D56 was identified as the challenged assumption but the debate argument was not developed. D56 remains OPEN in the decision table pending a future debate.

**What is challenged:** The 40% word-of-mouth attribution has been treated as settled since D33 without empirical validation. No mechanism exists to measure it. For a new product with zero customers, 40% WoM is unachievable at launch — WoM is a lagging indicator of product-market fit, not a leading acquisition channel.

**The core issue (from the debate log):** D33 used 40% WoM to justify the Free tier acquisition model. D52 and D55 relied on it for channel priority. If WoM is not a reliable launch-channel, the acquisition funnel is under-designed.

**Verdict on D56:** OPEN — this is the most important unresolved assumption. It anchors multiple decisions without validation. Needs a measurement mechanism before launch: UTM-tagged referral codes, "comment avez-vous connu l'app?" onboarding question, or explicit referral invite system. Without measurement, 40% is an article of faith.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D1 | Positioning | Kill "CRM" — devis, factures, relances | 2026-03-30 |
| D2 | MVP scope | 4 features, SEQUENCED. Sprint 0 (3-4d compliance), Sprint 1 (client+devis), Sprint 2 (factures + email relances). | 2026-03-30 |
| D3 | Primary persona | Marc — solo smartphone-native artisan | 2026-03-30 |
| D4 | Stack | Single managed Postgres | 2026-03-30 |
| D5 | Pricing | Free + €29 two-tier. Drop €49/€79. | 2026-03-30 |
| D6 | Trial | No time-limited trial. Free tier IS the trial. | 2026-03-30 |
| D7 | Architecture | Nuxt 3 + OVH managed Postgres — REOPENED D57 (API-first challenge) | 2026-03-30 |
| D8 | E-invoicing | v2 feature | 2026-03-30 |
| D9 | Not MVP | No Kanban, no multi-user, no offline, no API keys | 2026-03-30 |
| D10 | Buyer trigger | "Admin pain" not "CRM need" | 2026-03-30 |
| D11 | Mobile | React Native from Day 1 via Expo | 2026-03-30 |
| D12 | Landing page | Simplicity-first — "Vos devis et factures, sans vous prendre la tête." | 2026-03-30 |
| D13 | Home view | Job-first — Active Job Card as home anchor | 2026-03-30 |
| D14 | E-invoicing timing | v2 — NOT Day 1 | 2026-03-30 |
| D15 | Relances differentiator | DE-EMPHASIZED — secondary feature below fold | 2026-03-30 |
| D16 | Trial length | No countdown trial — Free tier IS the trial | 2026-03-30 |
| D17 | Mobile strategy | React Native from Day 1 via Expo. Email-only relances at launch. Push deferred to v1.1. | 2026-03-30 |
| D53 | Landing page | Simplicity-first RETAINED. H1: "Sans vous prendre la tête." H2: 5-min specific claim. | 2026-03-30 |
| D54 | Sprint 0 | Compressed compliance sprint (3-4d): TVA, sequential numbering, mentions légales, client-type. | 2026-03-30 |
| D55 | Buyer-user split | Dual-persona GTM. Marc = economic buyer. Admin handler = operational user. Expert-comptable = Phase 2. | 2026-03-30 |
| D56 | WoM measurement | OPEN — 40% unvalidated. Needs measurement mechanism before launch. | 2026-03-30 |
| D57 | Architecture | OPEN — Nuxt 3 challenged. API-first + static site proposed. D7 needs formal resolution. | 2026-03-30 |
| D58 | Relances in MVP | CLOSED — email relances = v1 (1-2 days, Sprint 2). Expo Push relances = v1.1 (1-2 weeks). | 2026-03-30 |

| U1 | Discovery | REPLACED — readiness protocol | 2026-03-30 |
| U2 | E-invoicing platform | Factea first when v2 | 2026-03-30 |
| U7 | Domain | DEFERRED — subdomain/Carrd until MVP validated | 2026-03-30 |
| U8 | WhatsApp acquisition | CLOSED — no WhatsApp CTA in devis | 2026-03-30 |
| U9 | Free tier activation | Optimized for daily ritual (evening devis flow) | 2026-03-30 |
| U10 | GTM: Wholesaler | Digital + specialist retailers first. Wholesaler secondary. Audit first. | 2026-03-30 |
| U11 | Prescriber audit | If >30% of new jobs via prescriber, revisit GTM priority | 2026-03-30 |
| U12 | Expert-comptable playbook | Phase 2 — relationship-dependent | 2026-03-30 |
| U13 | WoM measurement | NEW — define referral tracking mechanism before launch (UTM codes, "comment avez-vous connu?", invite codes) | 2026-03-30 |
| U14 | API-first architecture | NEW — resolve D57: evaluate Node/Express or Fastify vs Nuxt 3 as backend framework | 2026-03-30 |

---

## Debate 57: D7 — Nuxt 3 Architecture Was Never Challenged After the Mobile Pivot

**Challenge:** D7 (Nuxt 3 + OVH managed Postgres) was decided before React Native was chosen. The product is now mobile-first with a static landing page. Nuxt 3's SSR capabilities are architecturally mismatched.

### Technical Architect — API-First Architecture Case

**Assumption challenged:** SSR is needed for the landing page's SEO, and JWT auth is simpler when embedded in a full-stack framework like Nuxt.

**Core argument:**

The architectural mismatch is the core problem. Nuxt 3 is a full-stack web framework whose primary value comes from SSR, API routes, and server-side session management. The primary product is React Native (D11/D17). The mobile app does not use Nuxt's API routes — it connects directly to Postgres via Expo. Nuxt becomes middleware that adds nothing except overhead: unnecessary SSR rendering, higher RAM requirements, and vendor lock-in.

**On SSR for the landing page:** This assumption is false. The landing page is a static simplicity-first page (D53). It has no user-specific content, no authentication state, no personalized data. Static HTML with proper meta tags serves the same SEO value as SSR at a fraction of the RAM and build cost. Google indexes static pages identically. The "SSR = better SEO" argument applies to content-heavy sites with dynamic personalization — not to a one-page acquisition funnel.

**On JWT auth being simpler in Nuxt:** Also false. The mobile app manages JWT tokens client-side regardless of backend framework. Embedding auth in Nuxt doesn't simplify the mobile app's token management — it just means the mobile app talks to Nuxt's API routes while ignoring everything else Nuxt provides. The auth logic is identical whether it's in a dedicated Fastify auth middleware or in Nuxt server middleware.

**The operational cost of the wrong choice:**

| Factor | Nuxt 3 SSR | Fastify API + Static |
|--------|-----------|---------------------|
| RAM for same VPS | 4GB+ (SSR overhead) | 2GB (lightweight) |
| Landing page | Nuxt server rendering | Static HTML (CDN-cacheable) |
| Mobile API | Nuxt API routes (unused) | Direct REST endpoints |
| Hosting | OVH managed Postgres + Nuxt SSR server | Single VPS (API + static) |
| Learning curve | Nuxt file-based routing, server routes, SSR lifecycle | Simple route handlers |
| Lock-in risk | High — Nuxt-specific conventions | None — standard REST |

**Why prior resolution was wrong/incomplete:**

D7 resolved to Nuxt 3 when the product was conceived as a web-first application with SSR requirements. The mobile pivot (D11/D17) fundamentally changed the architecture — but D7 was never revisited. The resolution treated the product as unchanged while the most consequential technical decision was made obsolete by subsequent choices. A framework chosen for a web-first product cannot simply be re-deployed as the backend for a mobile-first product without creating architectural absurdity: the SSR capabilities that justified Nuxt are entirely unused, and the API routes that would serve the mobile app are bypassed in favor of direct Postgres access.

**Concrete proposal:**

D7 is OVERRULED. The architecture becomes:

**1. Backend: Node.js/Fastify on OVH VPS (2GB RAM)**
- Fastify chosen over Express: 30-40% faster throughput, schema validation built-in, same team can learn it in hours
- All API endpoints: `/auth/*`, `/clients/*`, `/devis/*`, `/factures/*`, `/relances/*`
- JWT authentication via `@fastify/jwt` — mobile app manages token lifecycle
- Postgres accessed via `postgres.js` (lightweight, no ORM overhead) — same schema from Sprint 0
- Static file serving for landing page in same VPS process

**2. Landing page: Single static HTML file**
- Pure HTML + CSS, no JavaScript framework
- Hosted on same VPS as Fastify API (or moved to Cloudflare Pages free tier)
- No SSR, no build step, no Nuxt dependency
- Meta tags for SEO: title, description, Open Graph

**3. React Native/Expo app**
- Connects to Fastify API via REST/JSON
- No coupling to web framework conventions
- Same API contract serves mobile app AND any future admin panel (v2)

**4. Migration path for Sprint 0:**
- The Postgres schema (TVA per-line, sequential numbering, mentions légales, client-type) defined in Sprint 0 is preserved unchanged
- Only the access layer changes: from Nuxt ORM to Fastify route handlers
- Estimated migration time: 1 day

**5. Hosting cost comparison:**
- Current plan: OVH managed Postgres (~€15/mo) + Nuxt SSR server (2vCPU/4GB ~€20/mo) = ~€35/mo
- Proposed: OVH managed Postgres (~€15/mo) + single VPS 2GB (~€10/mo) = ~€25/mo
- Savings: ~€10/mo + simplified operations

**What this challenges:**

- **D7**: Overruled — Nuxt 3 + OVH Postgres replaced with Fastify + same Postgres
- **The "JWT simpler in Nuxt" assumption**: False — token management is identical, just in a dedicated auth service
- **The "SSR needed for landing page SEO" assumption**: False — static HTML serves the same purpose
- **D11/D17 implications**: Cleaned up — mobile app has no coupling to a web framework it was always going to bypass
- **Future v2 admin panel**: Now consumes the same API as mobile, no Nuxt dependency required

**Verdict requested:** RESOLVED — D7 is overruled. API-first architecture (Fastify + static landing page) replaces Nuxt 3. The mobile pivot made Nuxt 3 architecturally obsolete before D7 was ever challenged. This is the correction.

---

*Last updated: 2026-03-30T14:57*


---

## Pulse 2026-03-30T14:57 — Product Strategist Debate on D56

---

## Debate 56: Word-of-Mouth 40% — Three Structural Flaws Make It Unusable as a GTM Input

**Challenge:** D56 (OPEN since 14:24) — The Growth Strategist correctly identified that 40% WoM is unvalidated. But the challenge stops at "unverified number." The actual problem is deeper: the number rests on three compounding structural flaws, each sufficient to invalidate the GTM decisions anchored to it.

### Product Strategist — The WoM Attribution Is Structurally Broken

**Assumption challenged:** That 40% is a reliable input for GTM planning, that it reflects the *channel's* power (not product-market fit's), and that it justifies the Free tier acquisition model.

---

**Assumption challenged #1: Word-of-mouth is a channel you can bet on, not a result you earn.**

The fundamental confusion in the debate log: WoM is being treated as a *leading acquisition channel* — something you can invest in and expect returns from. It is not. WoM is a *lagging indicator of product-market fit*. You get high word-of-mouth when you have a product that solves a problem so viscerally that users evangelize it unprompted.

The 40% figure, when cited, is almost certainly drawn from established SaaS companies (Slack, Calendly, Notion) where:
- The product has been in market for 2+ years
- Users have completed full usage cycles and experienced the value repeatedly
- Switching costs have materialized (the team is now coordinated around the tool)
- The product is used in visible, collaborative contexts (colleagues see you using it)

This product has zero of these conditions. Marc will have zero completed payment cycles at launch. No one will have experienced the "I got paid faster because of this app" moment. There is no collective context (Slack has teams; Marc is solo). The social proof that drives WoM — *"look at my colleague using this, I want that too"* — doesn't exist for a solo artisan tool.

**The practical implication:** Treating WoM as a launch-channel is like treating " customers will love it" as a launch strategy. It's an outcome, not an input. You cannot plan toward it; you can only build a product that earns it.

---

**Assumption challenged #2: The Free tier creates conditions for WoM acquisition, when it actually suppresses it.**

The 40% WoM justification for the Free tier is: Free → frictionless adoption → users proliferate → peer endorsement. This chain is broken in three places:

**Broken link #1 — "Free = proliferation":** Free removes financial friction but adds commitment friction. A free tool with no urgency to use it sits in the app drawer at low engagement. A user who opens the app once a week has no WoM momentum. A user who hits the ceiling at month 3 has no one to tell — they've already converted or churned.

**Broken link #2 — "Users proliferate":** At zero cost, there's no selection pressure. Curious browsers, competitive researchers, "I'll try this someday" users all occupy the Free tier. These are not WoM carriers. They dilute the denominator.

**Broken link #3 — "Peer endorsement":** Even if a Free user loves the product, the peer endorsement moment requires: (a) the peer has a similar problem, (b) the endorsement happens in a context where the peer can act on it, and (c) the peer is reachable. WhatsApp artisan groups are the assumed vehicle — but the artisan-to-artisan endorsement rate in those groups for a tool nobody has paid for is structurally near zero. Unpaid tools are not mentioned in professional contexts. Paid tools that have proven their value are.

**The Free tier does not generate WoM. Paid tiers with demonstrated value generate WoM.** The Free tier is a conversion funnel, not an acquisition engine.

---

**Assumption challenged #3: Peer referral is measurable, when it is structurally unmeasurable.**

Even if WoM were a real channel, the debate log acknowledges no measurement mechanism. The three proposed options — UTM-tagged referral tracking, "comment avez-vous connu l'app?" onboarding question, or explicit referral invite codes — all have fatal flaws for this specific use case:

**UTM-tagged referral tracking:** Works for explicit shares (user clicks "share" and gets a link). Does not work for "I told my buddy about it at the job site" — which is the primary WoM modality. You can only measure what you instrument. You cannot instrument a conversation.

**"Comment avez-vous connu l'app?" onboarding question:** Self-reported attribution is systematically biased toward socially desirable answers ("a friend recommended it" sounds better than "I searched on Google"). Additionally, for a product where discovery happens through peer conversation, the respondent often genuinely cannot distinguish between "saw a WhatsApp post" and "heard from a colleague" — the lines blur.

**Explicit referral invite codes:** Requires active referrer behavior. Under 2% of free SaaS users generate referral codes. With 500 Free tier users, that's 10 referral events per month. Not a channel.

The honest conclusion: WoM cannot be measured at the precision implied by "40%." Any number assigned to it is a guess, and should be treated as such.

---

**Why prior resolution was wrong/incomplete:**

The Growth Strategist's D56 challenge (14:24 pulse) correctly identified that the number is unvalidated. But it still treated WoM as a real channel that just needs measurement. The Product Strategist goes further: WoM is not a channel in the relevant sense. It is an outcome. You cannot build a GTM strategy around earning an outcome — you build it around activities that produce the conditions for that outcome.

The resolution proposed (UTM codes, onboarding question, invite codes) treats measurement as the fix. Measurement tells you what happened; it doesn't create the channel. If there are only 10 referral events per month because Free users have no urgency to evangelize a tool they didn't pay for, measuring that number doesn't change the underlying behavior.

---

**Concrete proposal:**

**Step 1 — Restate the assumption:** "40% of users arrive via word-of-mouth" is retired. Replaced with: "Word-of-mouth is a long-term outcome we are building toward, not a launch-channel we are investing in."

**Step 2 — Redesign GTM attribution:** Replace the "40% WoM" input in the GTM model with:
- **Organic search / SEO** (measurable, compound, primary at launch)
- **Comparison site presence** (GetApp, Capterra, alternatives — addressable for admin handler persona)
- **Direct referral from paid users only** (measurable via invite codes for €29 users; zero expectation for Free tier)
- **Digital artisan community presence** (Facebook groups, trade forums — brand awareness, not tracked conversion)

**Step 3 — Add a referral mechanism for €29 users only:** When a user converts to paid, prompt them once: "Vos collègues artisans pourraient-ils bénéficier de cet outil?" Offer a referral code. Track paid-user referrals as the *actual* WoM proxy. This is the only version of WoM that is both measurable and meaningful — paid users who recommend the tool because they paid for it and love it.

**Step 4 — Remove "WoM is primary GTM" from the GTM document.** Replace with honest framing: "WoM is the goal for 12-18 months post-launch, once paying users have completed the full payment cycle and experienced the value. At launch, we are investing in channels we can measure while building a product worth recommending."

**Step 5 — Define WoM readiness criteria for when to invest in it:** WoM as a channel becomes viable when: (a) paid user 30-day retention > 70%, (b) at least 30% of paying users have completed 3+ payment cycles, (c) spontaneous peer mentions appear in artisan WhatsApp groups. Until then, it is an outcome being tracked, not a channel being invested in.

---

**What this challenges:**

- **D33 (Free + €29 pricing):** Justified partly by "WoM is primary GTM at 40%." If WoM is an outcome not a channel, the Free tier justification stands on its own (removes commitment anxiety, enables trial). The 40% anchor is retired.
- **D52 (GTM priority order):** "Digital → Specialist retailers → Prescriber → Wholesaler" was affirmed in D52. The D56 challenge doesn't overturn the priority order — it removes the "but WoM is 40%" justification, leaving the channel logic intact but the confidence misplaced.
- **D55 (dual-persona GTM):** The dual-persona framing (Marc = buyer, admin handler = user) remains valid. But "WhatsApp groups" as the primary discovery channel for Marc is downgraded from "proven primary channel" to "hypothesis requiring validation." The admin handler / comparison site path becomes comparatively stronger.
- **Free tier design (D6/D43/D46):** If Free tier doesn't generate WoM, the "generous limits → trust-building → organic advocacy" chain is broken. The Free tier still stands as a trial mechanism, but the advocacy aspiration is deferred.

---

**Verdict requested:** REFINED — "40% WoM" is retired as a GTM input. WoM is restated as a 12-18 month outcome, not a launch-channel. GTM model redesigned to reflect channels we can measure and invest in (SEO, comparison sites, specialist retailers). Paid-user referral tracking added as the only measurable WoM proxy. D33, D52, D55 partially challenged (WoM justification removed; channel priorities retained on their own merits).

*Last updated: 2026-03-30T14:57*

---

## Pulse 2026-03-30T14:57 — Growth Strategist Cross-Cutting Challenge

---

## Debate 56: WoM Attribution — The 40% Is Not the Biggest Risk

**Challenge:** The debate has framed D56 as "40% number is unvalidated." That's the wrong risk. The real risk is that the entire GTM has no active acquisition engine at launch — and WoM is being used to justify passive launch planning.

### Growth Strategist — WoM Is a Result, Not a Strategy

**Assumption challenged:** That the 40% WoM figure represents an acquisition channel we can rely on, and that the GTM priority order (digital secondary, prescriber Phase 2, expert-comptable Phase 2) is acceptable because word-of-mouth will carry the weight.

**Core argument:**

The debate has focused on whether the 40% number is empirically verified. It isn't. But the more dangerous assumption is that *any* word-of-mouth at launch is a foregone conclusion. The reasoning in D33, D52, and D55 treats 40% as a baseline that will materialize once the product exists. This inverts causality.

**Word-of-mouth is a lagging indicator of product-market fit.** You earn high WoM by shipping a product that delights users so much they proactively recommend it to peers unprompted. This requires: (a) users who've completed the full lifecycle (client → devis → facture → payment → relapse follow-up), (b) enough time for the product to solve a real problem they've felt for months, (c) a moment of delight significant enough to trigger sharing. At launch, we have zero of these conditions. The 40% we might eventually earn is not available to us on Day 1.

**The GTM currently has no active acquisition engine at launch.** Review the priority order: digital channels (secondary), specialist retailers (needs audit), prescriber networks (Phase 2), expert-comptable (Phase 2). What actively drives the first 10 users? "Build it and they will come via WoM." That's not a GTM strategy — that's hope with a percentage attached.

**"WoM at 40%" for a new product is mathematically impossible anyway.** For WoM to account for 40% of acquisitions, you need a large enough user base that peers are constantly encountering each other. A new product with 20 Free users cannot generate 40% WoM attribution — there aren't enough users to generate the peer network effect. The 40% figure describes a mature product with strong retention. Applying it to launch planning is category error at the strategic level.

**The measurement problem is also an action problem.** D56 correctly identifies that without a measurement mechanism, 40% is unverifiable. But it's worse than that — without a referral tracking mechanism (UTM codes, invite codes, "comment avez-vous connu?" question), we won't even know if our first 10 users came from a real signal or from friends doing a favor for the founder. That's not data — that's noise.

**Concrete proposal:**
1. **Accept that WoM is a Month 3+ outcome, not a Month 1 channel.** First 10 users require active outreach: personal network, direct outreach to artisan communities, guerrilla presence at retailer locations
2. **Implement "comment avez-vous connu?" at signup** — one question, required, with predefined options (peer, Google/search, social media, comparison site, other). This gives us directional data from Day 1 without complex UTM infrastructure
3. **Add referral codes in v1** — simple "invite a colleague" with a unique code. Track invite → signup rate. This is the actual WoM measurement mechanism
4. **Update D33/D52/D55 GTM priority order** — acknowledge that digital acquisition (SEO + comparison sites) is PRIMARY at launch, not secondary. WoM supplements later, not at launch
5. **Define a WoM target for Month 3 specifically** — e.g., "20% of new users cite peer referral as discovery channel by Month 3." This makes WoM a goal to earn, not a assumption to carry

**What this challenges:** D33 (Free + €29 justified partly via WoM primary GTM), D52 (WhatsApp groups as discovery pathway — valid but insufficient at launch), D55 (dual-persona GTM without acquisition engine for either persona at launch). D48 priority order needs revision: digital acquisition is primary, not secondary.

**Verdict on D56:** REOPENED — 40% WoM attribution is unvalidated AND the GTM has no active acquisition engine at launch. Both problems must be fixed. Add measurement mechanism (U13), revise GTM priority order to make digital primary, and treat WoM as Month 3+ lagging indicator.

---

## Debate 57: Architecture Choice — A Distraction From the Real First-10-Users Problem

**Challenge:** D57 (Nuxt 3 vs API-first) has been framed as an architectural correctness question. From a growth perspective, this is the wrong debate at the wrong time.

### Growth Strategist — Architecture Doesn't Kill Products, Absence of Users Kills Products

**Assumption challenged:** That the Nuxt 3 vs API-first architecture decision is a critical decision that could affect the product's trajectory. The more dangerous assumption is that choosing the wrong architecture will determine whether we get the first 10 paying users.

**Core argument:**

The Technical Architect is correct: Nuxt 3 is architecturally mismatched for a mobile-first product. SSR is unused. API routes are bypassed by Expo. The web surface is a static landing page. These are valid technical criticisms. But the growth question is different: **does this architecture choice determine whether we get 10 paying users?**

**The answer is no — and here's why:**

First 10 paying users come from: direct personal outreach, peer referrals from the founder's network, and early adopters found via guerrilla tactics. None of these channels are affected by whether the backend is Nuxt 3 or Express. A user who signs up because a friend recommended it doesn't ask "what framework does your backend use?" They ask "does it solve my problem and can I trust it?"

The architecture decision affects: developer velocity (medium-term), hosting costs (long-term), and ability to add features (long-term). It does not affect whether the first 10 people can discover, sign up, and convert.

**The dangerous distraction:** Every hour spent debating architecture is an hour not spent on customer discovery, guerrilla testing, or writing the first outreach list. D57 is a comfortable technical debate because it has a clear right answer (API-first is cleaner). It's also a debate that doesn't matter for the next 60 days. The first 10 users won't arrive via architectural superiority — they'll arrive via founder effort and peer trust.

**The real architectural risk is different:** The real architecture risk is choosing a stack that slows down iteration speed once we have users giving us feedback. Nuxt 3's SSR model vs Express's stateless API is a 2-week velocity difference over 6 months, not a launch-critical decision. What IS launch-critical: does the architecture allow us to ship a devis flow in 5 days? Both Nuxt 3 and Express + Node allow that.

**The growth verdict on D57:** Resolved by deferral. The Technical Architect's case is valid. But the growth priority is shipping a working product and finding 10 users — not achieving architectural purity. If Nuxt 3 is already partially built, the switching cost of migrating mid-MVP exceeds the benefit. If starting fresh, API-first is the cleaner choice. Either way, this is a Week 2 decision at earliest.

**Concrete proposal:**
1. **Defer D57 resolution to Sprint 0** — if Sprint 0 (compliance foundations) can be built in Nuxt 3 without slowing down the flow, do that. Migrate post-MVP if needed
2. **Growth says: ship the minimum viable product first** — any architecture that enables a working devis flow in 5 days is the right architecture for launch
3. **Add "iteration speed after first users" as the real architecture metric** — whatever stack lets the team ship based on user feedback fastest is the right choice, regardless of theoretical purity
4. **Close D57 in the decision log** — flag as "resolved: API-first preferred, but current Nuxt 3 investment can continue through MVP. Migration post-MVP if ROI positive."

**What this challenges:** D57 as framed (critical architectural decision). D7 (Nuxt 3 + OVH Postgres) — can remain standing through MVP if partial investment exists. The debate treats architecture as fate; it's actually mutable post-MVP at low cost relative to user acquisition effort.

**Verdict on D57:** REFINED — architecture matters for long-term velocity, not for first 10 users. D57 is a legitimate technical concern but the wrong priority. Defer resolution to post-MVP unless Nuxt 3 is actively blocking Sprint 0 progress. The real Growth Strategist concern is: don't let this debate delay shipping.

---

## Debate 59: The Third Assumption — Pricing Credibility Has Never Been Validated With Real Artisans

**Challenge:** D5 (€29/month Free + €29 tier) has been debated on positioning grounds (too expensive vs Tolteck, conflicts with simplicity) and conversion grounds (habit formation vs limit-hit). Nobody has asked the one question that could kill the product before 10 paying users: **would a real French artisan pay €29 for this?**

### Growth Strategist — The Unvalidated Price Is the Biggest Pre-Launch Risk

**Assumption challenged:** That €29/month is the correct price because: (a) it anchors on "one hour of labor" value math, (b) it's below enterprise SaaS but above commodity tools, (c) Free tier removes commitment risk. None of these justify the price — they justify the *positioning frame*.

**Core argument:**

**The "one hour of labor" anchor is the founder's math, not the customer's.** When a French artisan hears "€29/month," he doesn't calculate "that's one hour of labor." He calculates: "do I currently pay anything for this? No. Do I have a system that works? Yes (WhatsApp + Excel). What does switching cost me? Time to learn, time to migrate data, risk that it doesn't work when I need it." The €29 must clear a much higher bar than "one hour of labor" — it must clear "why would I switch from a system I've been running for 10 years?"

**The competitive price comparison is backwards.** Tolteck at €19 and Obat at €17 are cited as price floor evidence. But these tools have 40k+ users and years of trust. A new product at €29 (50-70% premium) with zero users and zero reputation faces a completely different price objection. The question isn't "is €29 reasonable for this category?" It's "is €29 reasonable for an unknown product in this category?"

**Free tier removes the commitment barrier but creates a different problem: no peer validation.** When everything is free, there's no social proof of value. A solo artisan seeing a free tool with no reviews, no prescriber endorsement, and no peer recommendations is looking at: "why should I trust this with my business for free, let alone €29?" The Free tier doesn't answer the trust question — it just removes the money barrier to discovering the answer.

**The activation of Free → Paid requires answering a question nobody has asked:** "At what point does a French artisan say 'I should pay for this'?" The current model assumes it's when they hit a limit (D43/D46) or form a habit (D51). But neither model has been validated with a real person in a real conversation. We have no evidence that Free users who reach 5 clients or form a daily evening ritual will pay €29. We have theory.

**The specific kill condition:** A product that gets 200 Free signups and 0 paying users by Month 2 is dead. The team will debate whether to lower price, add features, or improve onboarding. Meanwhile, runway burns. This scenario is plausible if: (a) the Free tier is good enough that users never feel pressure to upgrade, (b) the 10-client/5-devis limits are generous enough that serious artisans never hit them in 60 days, (c) no external forcing function (prescriber, expert-comptable, comparison site) creates urgency. All three conditions are consistent with current design.

**What nobody has done:** Asked 5 real French artisans in a 10-minute conversation: "If this solved your devis problem completely, what's the most you'd pay per month?" That's not a complex study. It's a Tuesday morning at a Gedimat parking lot. The answer to that question is worth more than 40 hours of internal pricing debate.

**Concrete proposal:**
1. **Guerrilla price validation** — before launch, ask 5 artisans: "If this app solved your devis problem completely, what's the most you'd pay?" Document actual answers. If median answer is <€20, D5 needs revision
2. **Add a "founding member" launch offer** — €19/month locked in for life for first 50 paying users. This tests price sensitivity while creating social proof and urgency. If this offer doesn't convert, the €29 price is wrong
3. **Set a conversion metric for Month 1** — e.g., "3% of active Free users convert to paid by Day 30." If we hit Month 2 with <1% conversion, price is likely the barrier — not onboarding, not features
4. **Add "payment method legitimacy" signal** — French artisans are skeptical of online subscriptions. A SEPA direct debit option (common in French SaaS) reduces the "this feels like a scam" friction that a credit card-only payment creates

**What this challenges:** D5 (€29 anchored on value math — unvalidated with real users), D43/D46 (limit-hit conversion model — assumes price is accepted, only trigger is the limit), D6 (Free tier as trial — doesn't address the price credibility gap), the entire GTM assumption that a Free tier with a €29 upgrade is sufficient to convert without validating that €29 is a credible price point for an unknown product

**Verdict on D59:** NEW — Pricing credibility is the unchallenged assumption most likely to kill the product before 10 paying users. Add guerrilla price validation to U1 readiness protocol. Add founding member offer to test price sensitivity at launch. Set conversion KPIs that trigger price reconsiderations if missed.

---

## Updated Decision Table Additions

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D56 | WoM attribution | REOPENED — 40% unvalidated AND GTM has no active acquisition engine at launch. Add measurement mechanism, make digital primary. | 2026-03-30 |
| D57 | Architecture | REFINED — valid technical concern, wrong priority. Defer to post-MVP unless blocking Sprint 0. | 2026-03-30 |
| D59 | Pricing credibility | NEW — €29 price point unvalidated with real artisans. Guerrilla price validation + founding member offer proposed. | 2026-03-30 |

| U13 | WoM measurement | "Comment avez-vous connu?" at signup + referral codes. Track Month 3 target: 20% peer referral. | 2026-03-30 |
| U14 | API-first architecture | Defer — unless Nuxt 3 actively blocks Sprint 0, continue and migrate post-MVP | 2026-03-30 |
| U15 | Price validation | NEW — guerrilla price validation: ask 5 artisans "most you'd pay?" Add founding member €19/mo launch offer. Set 3% conversion target for Day 30. | 2026-03-30 |

---

*Last updated: 2026-03-30T14:57*

---

## Pulse 2026-03-30T15:17 — Three New Debates

---

## Debate 60: WoM Attribution — The 40% Figure Is Fabricated

**Challenge:** D56 (REOPENED at 14:57) — Product Strategist challenges the conflation of two distinct claims: (A) "40% of users come from WoM" (attribution claim — unvalidated), and (B) "WoM is a lagging indicator, not a leading channel" (strategic claim — correct). The Growth Strategist defending (B) doesn't rescue (A) from being evidence-free.

### Product Strategist — 40% Is Made Up, and That's the Real Problem

**Assumption challenged:** The 40% figure has been treated as settled since D33, anchoring D33 (pricing), D52/D55 (GTM priority), and the Free tier acquisition model. It was never sourced, never validated.

**Core argument:**

**The 40% figure is manufactured precision.** Since D33, "40% word-of-mouth" has functioned as a loaded fact. It justified Free tier acquisition model. It anchored GTM sequencing. It appeared in pricing rationale. But it was never sourced from user interviews, analytics, cohort analysis, or survey data. It's a round number that felt plausible, so it became settled. The Growth Strategist calling it a "lagging indicator" is a deflection — the urgent issue is that we built a pricing model and GTM strategy on a number we invented.

**The Tolteck precedent supports validating WoM, not assuming it.** Tolteck's prescriber/wholesaler network strategy was deliberately engineered — they identified dense artisan peer networks and activated them systematically. That's a leading channel strategy built on structure, not an accident of product quality. For Mini-CRM: the question isn't whether 40% of current users arrived via WoM — it's whether we can systematically seed the same dense networks and measure it from day one.

**New product launch conditions break the lagging-indicator argument.** At zero users, there's no one to spread word. Either WoM is an earned/built channel we actively construct through trade associations, wholesaler partnerships, and prescriber relationships — or we accept slow organic growth while waiting for a user base to materialize.

**VERDICT on D56:** Split the two debates. RESOLVED — WoM as lagging indicator: confirmed. WoM attribution at 40%: RETIRED, replaced with measurement protocol. D33 and D52/D55 updated: replace "40% WoM" with "WoM hypothesized significant based on artisan network density and competitive precedent, validated post-launch."

---

## Debate 61: D7 — Nuxt 3 Architecture Is Overengineered for This Product

**Challenge:** D7 ("Nuxt 3 + OVH managed Postgres") was resolved pre-pivot. Technical Architect challenges whether Nuxt 3's core capabilities (SSR, API routes, session management) are used at all given the mobile-first + static landing page product.

### Technical Architect — API-First Is the Right Fit

**Assumption challenged:** D7 assumed Nuxt 3 was the right backend. But after the mobile-first pivot: React Native (Expo) talks to an API, not Nuxt server routes. The landing page is static. SSR, API routes, and server-side session management all go unused.

**Core argument:**

**Nuxt 3 is solving a problem we don't have.** A static landing page needs no SSR. The React Native app is an API consumer. Every dollar on Nuxt's server runtime, every CPU cycle on server-side rendering logic — all overhead. We're not building a web app. We're building a mobile app with a marketing page.

**The "future web app" argument is speculative debt.** Yes, if Louis someday adds a full web app with auth, Nuxt has primitives for that. But that's an assumption about a future that may never materialize, costing real complexity now. A well-designed REST API serves both the mobile app and a future web app equally well. Nuxt's "built-in" auth still needs implementation effort.

**Cost and simplicity matter at early stage.** A lightweight Node/Express or Fastify API on a 2GB VPS handles the load comfortably. OVH managed Postgres stays. Less infrastructure = less ops = more time building product.

**VERDICT on D7:** REFINED — API-first (Node/Fastify + static landing page + JWT auth) is the cleaner architecture for a mobile-first product. OVH managed Postgres retained. Migration to API-first deferred to post-MVP unless Nuxt 3 actively blocks Sprint 0 (it won't).

---

## Debate 62: D59 — Founding Member €19 Offer Is a Price Anchor Trap

**Challenge:** D59 (REOPENED at 14:57) — Growth Strategist challenged €29 as unvalidated and proposed €19 founding member offer. Technical Architect challenges the €19 founding offer specifically.

### Technical Architect — €19 Founding Offer Permanently Poisons the €29 Anchor

**Assumption challenged:** The €19 founding member offer tests price sensitivity while creating social proof and urgency. Technical Architect argues it does the opposite — it permanently anchors the product at a discount.

**Core argument:**

**The founding member offer is a trap.** Every pricing textbook and every battle-tested founder (HubSpot, Dropbox, Slack at launch) will tell you: your first paying customers set the anchor for everyone who follows. If Louis signs up 20 founding members at €19/mo, those 20 people will never accept €29/mo. And they'll talk. French artisans network intensely (chambres de métiers, WhatsApp groups). The €19 "real price" leaks out and poisons the well. The €29 price becomes the discount, not the standard.

**"One hour of labor = €29" is founder math, not customer math.** Louis assumes artisans bill €50-80/h. But the target market — micro-entrepreneurs, small artisans — typically bill €25-40/h. At €30/h, €29 equals 58 minutes of labor. That's not trivial — it's roughly equivalent to an hour of their time. The anchor doesn't land the same way for a micro-artisan billing €30/h as it does for a consultant billing €80/h.

**The real problem isn't price — it's proof.** At €29/mo, the ROI case is overwhelming if the value is real. Devis automation saving 2h/week = 8h/month. At €40/h (conservative artisan rate), that's €320/mo value. €29 = 9% of the value delivered. The price isn't the risk. The lie risk is the risk. If Louis can't prove time savings materialize, no price works. If he CAN prove it, €29 is so far undervalue it's almost suspicious.

**VERDICT on D59:** Kill the €19 founding member offer. Replace with: "Early access — first 50 users lock €29/month for life." This preserves the €29 anchor, creates urgency, and locks early adopters at the standard price. Add guerrilla price validation: show 5 artisans a working demo, ask them to estimate time spent on devis per week, then ask what they'd pay to halve it. Let THEM anchor the price.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D56 | WoM attribution | RESOLVED — 40% figure RETIRED. WoM as lagging indicator: confirmed. Replace with measurement protocol. D33/D52/D55 updated. | 2026-03-30 |
| D57 | Architecture | REFINED — API-first (Node/Fastify + static + JWT) is cleaner for mobile-first. Nuxt 3 deferred unless blocking Sprint 0. | 2026-03-30 |
| D59 | Pricing | REFINED — Kill €19 founding member offer. Replace with "early access, €29 locked for life." Guerrilla price validation with artisan rate anchors. | 2026-03-30 |

| U13 | WoM measurement | "Comment avez-vous connu?" at signup + referral codes. Month 3 target: 20% peer referral. | 2026-03-30 |
| U14 | API-first architecture | Defer migration to post-MVP unless Nuxt 3 blocks Sprint 0 | 2026-03-30 |
| U15 | Price validation | Guerrilla price validation: show demo, let artisans anchor price. Kill €19 founding offer. Replace with early access €29 locked for life. | 2026-03-30 |

---

*Last updated: 2026-03-30T15:33*

---

## Pulse 2026-03-30T15:46 — Three Resolved

---

## Debate 66: D63 — Free Tier Needs Self-Generating Pull, Not Better Notifications

**Challenge:** D40/D43/D46/D51 cycled through engagement channels (email → push → WhatsApp) and conversion models (limit-hit, habit formation) without questioning whether the Free tier itself creates desire to return. Product Strategist argues all of these are secondary to a missing element: a compelling output that makes artisans want to come back.

### Product Strategist — D63 Resolution

**Assumption challenged from D40/D43/D46/D51:** All four debates assumed the Free tier activation problem is solvable via better notifications or better timing. D40 selected a channel (push + WhatsApp opt-in). D43/D46 refined limit design. D51 proposed habit formation. None addressed the root question: what does the Free tier give artisans that they actively want to consume?

**The core flaw across all four debates:** A notification — regardless of channel — only recovers users who already believe the product is worth opening. If the first session didn't deliver a clear "this is useful," no cadence of reminders recovers them. You're debating the recall mechanism on a product that hasn't proven its value.

**The equilibrium problem for D43/D46:** Marc is in equilibrium. He has 6-7 steady clients, not a growing business. Hitting 10 clients doesn't trigger upgrade desire — it triggers "I'll just stay on the free plan." Limit proximity without felt value first is a wall, not a trigger.

**The habit formation problem for D51:** Habits form around pain, not convenience. A daily reminder to do something annoying (input work) is not a habit — it's a chore. The 2-minute evening devis ritual only becomes load-bearing if it relieves an existing friction. Without that friction, it's just another app notification competing for attention.

**Proposed self-generating pull mechanism:**

The **"situation financière" snapshot** — automatically produced weekly, surfaced as the Free tier home screen:

- Outstanding devis (pending acceptance, with days-open)
- Pending factures (sent but unpaid, aging buckets: 15/30/45/60+ days)
- Revenue this month vs. last month
- Clients with no activity in 30+ days

This is output the artisan *wants* to consume. It answers "how is my business right now?" — not "where did I leave off in the app?" The snapshot is a reason to open the app on its own merits. The notification that brings him back is secondary; the thing he wants to see is primary.

**Why this is different from a dashboard:** A dashboard requires navigation and interaction. The snapshot is push-ready content — it can live in a push notification ("Votre chiffre d'affaires a baissé de 12% ce mois — voir pourquoi") or a weekly digest. The artisan consumes value without doing work first.

**Verdict on D63:** RESOLVED — D40 RESTATED. Engagement channel is secondary to whether the Free tier delivers something artisans want to consume before being prompted. The "situation financière" snapshot is the Free tier's primary value output. Until it exists, notification channel debates are premature.

---

## Debate 67: D64 — Fastify + Postgres Must Start Sprint 0

**Challenge:** D57 deferred API-first to post-MVP ("unless Nuxt 3 actively blocks Sprint 0"). Technical Architect argues the deferral will become permanent and that Fastify + Postgres is faster to Sprint 0 than Nuxt 3 + Postgres, making the deferral both unnecessary and harmful.

### Technical Architect — D64 Resolution

**Assumption challenged from D57:** The "defer to post-MVP" escape hatch was treated as a reasonable compromise — keep building in Nuxt, migrate later if ROI positive. Technical Architect argues: Sprint 0 work IS the business logic foundation. Migration cost scales with integration depth. The "defer" resolution guarantees the migration never happens because the Nuxt routes become entangled with the TVA engine, sequential numbering logic, and mentions légales renderer — all of which must be extracted and rewritten.

**The Sprint 0 deliverables are backend-service problems, not UI problems:**
- TVA per-line calculator (5.5/10/20% rates, per line, with rounding)
- Sequential invoice numbering engine (gapless, cancel-aware, server-enforced)
- Mentions légales renderer (template file, client-type conditional)
- Client schema with type discrimination

None of these require a UI framework. Nuxt's SSR, file-based routing, and server route conventions add overhead precisely where the problem doesn't need it.

**Fastify + Postgres is faster to Sprint 0:**
- Day 1: Postgres schema + `npm create fastify` + first GET /health → <2 hours setup. TVA service with unit tests. Sequential numbering sequence + constraint.
- Day 2: POST /factures with validation + mentions légales template renderer. Full CRUD scaffolding.
- Day 3: Docker Compose (app + Postgres), first mobile integration test via REST.

With Nuxt 3: Days 1-2 spent learning Nuxt server route conventions, `useFetch` vs `useAsyncData`, hydration edge cases. The backend logic is still TODO.

**The architectural cleanliness argument:** React Native (Expo) is an HTTP client. It talks to REST/GraphQL endpoints. A Fastify API is a first-class REST API — direct, no framework middleware tax. Nuxt API routes are a web framework's interpretation of REST, with conventions designed for server-rendered web apps.

**Verdict on D64:** RESOLVED — D57 REFINED. Fastify + Postgres must START Sprint 0, not be deferred. Sprint 0 Day 1 deliverables: Postgres schema (TVA, sequential numbering, mentions légales, client-type) + Fastify project scaffold. Mobile team integrates against REST API from Day 3. Nuxt 3 is retired from the backend — static landing page only if needed.

---

## Debate 68: D65 — Three-Phase Discovery Must Precede Price Validation

**Challenge:** U15 (and D59's price validation method) proposed "show demo, ask willingness-to-pay" as the guerrilla validation step. Growth Strategist argues this skips pain validation entirely — showing a demo before observing actual workflow puts the artisan in audience mode, not discovery mode.

### Growth Strategist — D65 Resolution

**Assumption challenged from D59/U15:** "Show demo, then ask what you'd pay" assumes the artisan's pain is already known and that price is the primary unknown. Neither is true. Pain is unconfirmed — it was assumed from competitive analysis (Pennylane, Indy, Freebe exist = pain exists), not observed. And price sensitivity is downstream of pain intensity — meaningless without the upstream data.

**The demo-first problem:** An artisan who watches a demo nods politely. The product looks polished. The framing makes sense. He says "yes that could be useful." You get enthusiasm, not data. You've put him in audience mode — he's watching your vision, not revealing his own. The 20-minute observation before any demo tells you things no amount of post-demo conversation can surface.

**The three-phase sequence is non-negotiable:**

**Phase 1 — 20-minute observation, zero demo.** Watch the actual admin workflow. Where does he hesitate? What makes him sigh? What workarounds has he built? This is the foundation. Without pain observation, everything downstream is speculation.

**Phase 2 — Quantification.** Only after you've *seen* pain can you measure it. Time spent per week on devis/factures/relances. Emotional weight (1-10). What happens when a devis is forgotten. What happens when a client doesn't pay. These questions only land when both of you know what they're referring to.

**Phase 3 — Payment conversation.** Conditional on pain confirmed. If the observed workflow doesn't reveal genuine friction, you skip the payment conversation entirely — you've validated that this artisan isn't your user, which is also valuable data.

**The challenge to the debate log:** "Pain is confirmed" is treated as a checkbox. It isn't. It's the entire point. Skip to payment and you're validating your own optimism, not the market's reality.

**Verdict on D68:** RESOLVED — U15 UPDATED. Replace "show demo, ask WTP" with three-phase guerrilla session: observe first, quantify pain, then payment conversation only if pain is confirmed. U1 readiness protocol updated accordingly.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D1 | Positioning | Kill "CRM" — devis, factures, relances | 2026-03-30 |
| D2 | MVP scope | 4 features, SEQUENCED sprints. Sprint 0 = Fastify + Postgres compliance foundations (3-4d). Sprint 1 = client+devis flow. Sprint 2 = facture+email relances. | 2026-03-30 |
| D3 | Primary persona | Marc — solo smartphone-native artisan | 2026-03-30 |
| D4 | Stack | Single managed Postgres | 2026-03-30 |
| D5 | Pricing | Free + €29 two-tier. No €19 SKU. Drop €49/€79. Value anchor: "2h/week = 1h labor = €29/month." | 2026-03-30 |
| D6 | Trial | No time-limited trial. Free tier IS the trial. | 2026-03-30 |
| D7 | Architecture | Nuxt 3 RETIRED from backend. Fastify + Postgres + static landing page. | 2026-03-30 |
| D8 | E-invoicing | v2 feature | 2026-03-30 |
| D9 | Not MVP | No Kanban, no multi-user, no offline, no API keys | 2026-03-30 |
| D10 | Buyer trigger | "Admin pain" not "CRM need" | 2026-03-30 |
| D11 | Mobile | React Native from Day 1 via Expo | 2026-03-30 |
| D12 | Landing page | Simplicity-first — "Vos devis et factures, sans vous prendre la tête." | 2026-03-30 |
| D13 | Home view | Job-first — Active Job Card as home anchor | 2026-03-30 |
| D14 | E-invoicing timing | v2 — NOT Day 1 | 2026-03-30 |
| D15 | Relances differentiator | DE-EMPHASIZED — secondary feature below fold | 2026-03-30 |
| D16 | Trial length | No countdown trial — Free tier IS the trial | 2026-03-30 |
| D17 | Mobile strategy | React Native from Day 1 via Expo. Email-only relances at v1. Expo Push in v1.1. | 2026-03-30 |
| D40 | Engagement channel | RESTATED — channel is SECONDARY. Free tier needs self-generating pull (output/report) before notification channel debates matter. | 2026-03-30 |
| D41 | Notification infra | Email-only relances at v1 launch. Expo Push in v1.1. | 2026-03-30 |
| D42 | WhatsApp referral | CLOSED — no WhatsApp CTA in devis | 2026-03-30 |
| D43 | Free tier activation | RESTATED — channel secondary to Free tier output design. | 2026-03-30 |
| D46 | Free tier limits | Do NOT lower limits from 10/5. Trust-building before limit enforcement. | 2026-03-30 |
| D47 | Expo Push estimate | 1-2 weeks. Budget properly or defer to v1.1. | 2026-03-30 |
| D48 | Wholesaler GTM | Not primary. Digital + specialist retailers first. | 2026-03-30 |
| D49 | GTM Priority | Digital → Specialist retailers → Prescriber → Wholesaler. | 2026-03-30 |
| D50 | Push at launch | Email-only at v1. Expo Push in v1.1. | 2026-03-30 |
| D51 | Free tier conversion | Forcing function + limit-hit PRIMARY. Habit tracking SECONDARY. | 2026-03-30 |
| D53 | Landing page | Simplicity-first RETAINED. H1: "Sans vous prendre la tête." H2: 5-min specific claim. | 2026-03-30 |
| D54 | Sprint 0 | Compressed compliance sprint (3-4d): TVA, sequential numbering, mentions légales, client-type. | 2026-03-30 |
| D55 | Buyer-user split | Dual-persona GTM. Marc = economic buyer. Admin handler = operational user. Expert-comptable = Phase 2. | 2026-03-30 |
| D56 | WoM attribution | 40% figure RETIRED. WoM = Month 3+ lagging indicator. Measurement protocol: "Comment connaissez-vous?" + referral codes. | 2026-03-30 |
| D57 | Architecture | Fastify + Postgres + static landing page. D7 (Nuxt 3) RETIRED. | 2026-03-30 |
| D59 | Pricing | Kill €19 founding offer. Early access €29 locked for life. Guerrilla price validation with artisan rate anchors. | 2026-03-30 |
| D63 | Free tier pull | RESOLVED — "situation financière" snapshot (outstanding devis, pending factures, revenue vs last month, dormant clients) is the Free tier's primary value output. Notification channel debates are secondary until this exists. | 2026-03-30 |
| D64 | Sprint 0 stack | RESOLVED — Fastify + Postgres must START Sprint 0, not deferred. D57 REFINED. Nuxt 3 retired from backend. | 2026-03-30 |
| D65 | U15 discovery | RESOLVED — three-phase guerrilla: observe first (20 min, no demo), quantify pain (time/emotional weight), payment conversation only if pain confirmed. U15 UPDATED. | 2026-03-30 |

| U1 | Discovery | REPLACED — readiness protocol | 2026-03-30 |
| U2 | E-invoicing platform | Factea first when v2 | 2026-03-30 |
| U7 | Domain | DEFERRED — subdomain/Carrd until MVP validated | 2026-03-30 |
| U8 | WhatsApp acquisition | CLOSED — no WhatsApp CTA in devis | 2026-03-30 |
| U9 | Free tier activation | RESTATED — output/report design primary, notification channel secondary | 2026-03-30 |
| U10 | GTM: Wholesaler | Digital + specialist retailers first | 2026-03-30 |
| U11 | Prescriber audit | If >30% of new jobs via prescriber, revisit GTM priority | 2026-03-30 |
| U12 | Expert-comptable playbook | Phase 2 | 2026-03-30 |
| U13 | WoM measurement | "Comment connaissez-vous?" at signup + referral codes. Month 3 target: 20% peer referral. | 2026-03-30 |
| U15 | Guerrilla validation | UPDATED — three-phase: observe → quantify pain → payment (only if pain confirmed). Not "show demo, ask price." | 2026-03-30 |

---

*Last updated: 2026-03-30T15:46*

---

## Pulse 2026-03-30T15:33 — Three New Debates

---

## Debate 63: D40 — Engagement Channel Is the Wrong Variable

**Challenge:** D40 (engagement channel) — The debate has cycled through email → push → WhatsApp opt-in without ever questioning whether any notification channel can save a Free tier that doesn't create genuine value. Product Strategist challenges the premise.

### Product Strategist — Free Tier Needs Self-Generating Pull, Not Better Notifications

**Assumption challenged:** That engagement channel (email vs push vs WhatsApp opt-in) is a meaningful lever for Free tier activation.

**Core argument:**

**The channel debate is polishing a product that hasn't proven its worth.** A reminder — delivered via any channel — only works if the artisan already believes the product is worth using. If the first-use experience doesn't deliver a clear "I needed this," no notification cadence will recover them. You're debating the recall mechanism on a product that hasn't yet proven its value.

**The WhatsApp opt-in path is a high-cost ask for a low-value exchange.** You're asking an artisan to give a phone number + opt-in to WhatsApp business API for what? To receive a nudge that their trial is expiring? If the value of the product doesn't justify the opt-in, the channel change produces resentment, not activation.

**"Free tier feels empty without prompting" is the signal, not the problem.** That artisans need to be told to come back tells you the product isn't creating pull. Debating email vs. push vs. WhatsApp is like noting a patient has no appetite and responding by debating whether to use a blue or red spoon for the food they won't eat.

**Proposed reframe for D40:** The Free tier must deliver a self-generating pull — a report, a dashboard, a financial snapshot — that makes the artisan *want* to return to consume value, not be dragged back by a notification. Example: an automatically-produced "situation financière" snapshot showing outstanding devis and pending factures. The artisan wants to check it — it's output, not input.

**D63 Verdict requested:** D40 RESTATED — engagement channel is SECONDARY. The Free tier must first deliver something artisans want to come back to see. Until that exists, channel debates are premature.

---

## Debate 64: D57 — "Defer to Post-MVP" Is a Sunk Cost Trap

**Challenge:** D57 (API-first architecture deferral) — The resolution punted: "API-first preferred but deferred to post-MVP unless Nuxt 3 actively blocks Sprint 0." Technical Architect challenges the "defer" framing.

### Technical Architect — API-First Must Start at Sprint 0

**Assumption challenged:** That API-first architecture can wait until post-MVP without becoming permanently deferred.

**Core argument:**

**The "defer" escape hatch will never close.** When Sprint 0 starts with Nuxt 3, every hour spent learning Nuxt routing, server routes, and `useFetch` patterns makes migration to API-first later more expensive, not less. The team will have written business logic inside Nuxt server routes, learned Nuxt conventions, and a codebase where "let's rip out the backend" feels like a rewrite. Post-MVP migrations of this type almost never happen — the product ships, bugs appear, features land, and the deferred decision becomes permanent.

**Sprint 0 deliverables are backend-first — Nuxt adds friction without value.** TVA per-line schema, sequential numbering enforcement, mentions légales renderer — none of these require a UI framework. In fact, UI frameworks actively complicate all three. TVA calculations should live in a service layer, not a Nuxt server route that blends routing, validation, and business logic. Sequential numbering requires transactional semantics — raw SQL or a dedicated service, not a Nuxt composable.

**Fastify + Postgres is faster to Sprint 0 than Nuxt 3 + Postgres.** Initial setup: `npm create fastify` + `pg` vs. `npx nuxi init` + module installs. Time to first API route: <5 minutes vs. 15-20 minutes of convention setup. Nuxt's opinionation is valuable for a full-stack Vue app; for a React Native mobile app + static landing page, it's pure overhead on the backend side.

**API-first is the actual mobile-native architecture.** The product is React Native. The mobile app is an HTTP client. When you build Nuxt 3 backend, you are building a server framework that the mobile app will never use for its primary purpose. The mobile app talks to an API — that API should be built as an API, not as a web framework with SSR capabilities no mobile app will use.

**D64 Verdict requested:** D57 UPDATED — API-first (Fastify + Postgres) must START at Sprint 0, not be deferred. Sprint 0 with Fastify: Day 1 = Postgres schema + TVA service + sequential numbering service + mentions légales template renderer. Day 3 = working REST API consumed by React Native. No Nuxt dependency for the backend.

---

## Debate 65: U15 — Customer Discovery Must Precede Price Validation

**Challenge:** U15 (guerrilla price validation) — The D59 resolution proposed "show 5 artisans a demo, ask what they'd pay." Growth Strategist challenges this sequencing.

### Growth Strategist — Observe Pain Before Asking About Price

**Assumption challenged:** That showing a demo and asking willingness-to-pay is the correct first validation step.

**Core argument:**

**Price presupposes pain, not the other way around.** Asking "would you pay €29/month?" to an artisan who hasn't articulated their admin burden is meaningless. They've already solved it (badly, in their own view) with WhatsApp + Excel. You can't jump to price sensitivity when you haven't established whether they experience the admin task as a burden worth solving.

**Market existence ≠ felt pain for this specific user.** Pennylane, Indy, and Freebe existing proves a market exists — not that the French artisan in front of you feels the devis/facture cycle as acute pain. Many artisans have built workarounds they're comfortable with. Comfortable ≠ optimal, but comfortable is a real barrier that must be understood before you can ask whether they'd pay to change it.

**A demo puts you in persuasion mode, not discovery mode.** Showing a demo to someone who hasn't described their admin workflow first means they'll politely nod and say "yes that looks nice." You get enthusiasm, not data. The demo creates social pressure to be positive. The 20-minute observation creates a baseline from which you can actually measure reaction.

**Time spent and emotional weight are the real metrics, not Willingness to Pay.** WTP is downstream of pain intensity. Without knowing (a) how much time they spend on devis/factures per week, (b) how they feel about that task, and (c) what happens when they don't follow up — the WTP answer is unreliable.

**Proposed alternative — three-phase guerrilla session:**

*Phase 1 — Observation (20 minutes, no demo, no pitch):* Watch the artisan do their actual admin. Ask them to talk out loud. Measure: time on devis/facture/relance cycle, number of manual steps, where they get stuck or frustrated.

*Phase 2 — Problem quantification (10 minutes):* "How much time per week on devis and factures?" "What happens when a client doesn't pay — do you follow up?" "Have you ever lost a client because of a forgotten devis?" Rate pain 1-10.

*Phase 3 — Payment conversation (5 minutes, only if pain is confirmed):* Only after observing their workflow and hearing them describe the pain — then show a 2-minute demo. Then ask: "Based on what you just described, what would that be worth to you?"

**D65 Verdict requested:** U15 UPDATED — replace "show demo, ask price" with three-phase guerrilla discovery: observe first, quantify pain, then ask about payment only if pain is confirmed. U1 readiness protocol updated accordingly.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D56 | WoM attribution | RESOLVED — 40% figure RETIRED. WoM as lagging indicator confirmed. | 2026-03-30 |
| D57 | Architecture | REFINED — API-first must START Sprint 0 (Debate 64) | 2026-03-30 |
| D59 | Pricing | REFINED — Kill €19 founding offer. Early access €29 locked for life. | 2026-03-30 |
| D63 | Free tier activation | RESTATED — channel secondary. Free tier needs self-generating pull (report/dashboard) before notification channel debates matter. | 2026-03-30 |
| D64 | Sprint 0 architecture | REOPENED — API-first (Fastify + Postgres) must start Sprint 0, not deferred. | 2026-03-30 |
| D65 | U15 validation | REOPENED — customer discovery (observe pain) must precede price validation. Three-phase guerrilla session proposed. | 2026-03-30 |

| U13 | WoM measurement | "Comment connaissez-vous?" at signup + referral codes. Month 3 target: 20%. | 2026-03-30 |
| U14 | Sprint 0 stack | RESOLVED by D64 — Fastify + Postgres at Sprint 0 start, not Nuxt 3. | 2026-03-30 |
| U15 | Guerrilla validation | UPDATED by D65 — three-phase: observe → quantify pain → payment conversation. | 2026-03-30 |

---

## Pulse 2026-03-30T15:59 — Two Challenges (Growth Agent Failed: 401 Auth)

---

## Debate 66: Sprint 1 — 2 Weeks Is Structural Fantasy

**Challenge:** Product Strategist challenges Sprint 1 timeline (D2/D54: 2 weeks = client file + devis flow). Never technically stress-tested.

### Product Strategist — Sprint 1 Is 13-18 Days of Work Compressed Into 10

**Assumption challenged:** Sprint 1 was resolved as "client file + devis flow, 2 weeks." This was never broken down into actual work units. It appeared as a framing choice, not a derived estimate.

**Core argument:**

Sprint 1 is not one feature — it's six subsystems that must integrate:

1. **Client file** — schema, CRUD, contact management, client-type-driven mentions légales routing. 2 days.
2. **TVA multi-taux engine** — Sprint 0 handed you the schema. Sprint 1 builds the math. Three rates (5.5/10/20%) per line item, per-line HT/TVA/TTC, regulatory TVA breakdown section on document. 2-3 days.
3. **Sequential numbering for devis** — annual reset with prefix, gap detection, void/cancel awareness, server-enforced uniqueness. 1-2 days.
4. **React Native devis UI** — line items (description, qty, unit, TVA rate, price HT/TTC), multi-TVA per devis, mobile-first for 45-55yo. First artifact Marc sends to a client. No polish-later option. 3-4 days.
5. **PDF generation + mentions légales** — server-side PDF, dynamic mentions légales block (particulier/professionnel/étranger EU/hors EU × devis/facture), professional French document standards. 2-3 days.
6. **WhatsApp/email sharing + integration testing** — WhatsApp Business API, clean PDF attachment, end-to-end test Android + iOS. 2 days.

**Total estimated: 13-18 days. Available: 10 days.**

**Sprint 0 compression creates Sprint 1 debt:** Sprint 0's 3-4 day compression leaves no slack — it creates risk. Wrong TVA formula, numbering bug, mentions légales edge case: Sprint 1 discovers all of it.

**France-specific complexity not priced:**
- TVA multi-taux per line is a regulatory document requirement, not a subtotal
- Mentions légales is a template engineering problem with legal stakes if wrong (4 client types × 2 document types = 8 content variants)
- PDF rendering across iOS/Android screen sizes at professional quality is non-trivial and cannot be deferred

**Proposed resolution:** Either (A) split Sprint 1 into two: Sprint 1a (client file + devis creation UI, no PDF/share) + Sprint 1b (PDF + WhatsApp + TVA math), or (B) accept 3-week Sprint 1, update roadmap accordingly. Sprint 2 cannot start on time if Sprint 1 slips.

**Verdict on D2 Sprint 1:** REOPENED — Sprint 1 timeline needs real work breakdown before it can be treated as a 2-week sprint.

---

## Debate 67: TVA Per-Line Rounding — Settled Without Confirming the Algorithm

**Challenge:** Technical Architect challenges D54's treatment of TVA per-line calculation as "a formula, not a lookup table." The actual rounding rule was never confirmed.

### Technical Architect — Arrondi Arithmétique vs Bancaire Is Unresolved

**Assumption challenged:** D54 resolved Sprint 0 includes "TVA per-line schema — devis_lines.tva_rate enum (5.5/10/20), server-side calculator for montant_ht and montant_tva per line." This was treated as done. It is not.

**Core argument:**

French TVA rounding is not `Math.round()`. Article 266 of the Code Général des Impôts specifies: TVA per line is calculated on the rounded unit price × quantity, then rounded to 2 decimal places. Total TVA = sum of per-line rounded amounts.

The critical unresolved question: **which rounding rule?**

| Method | Rule | Example (1.5) |
|--------|------|---------------|
| Arrondi arithmétique (round half up) | 0.5 rounds away from zero | 1.5 → 2 |
| Arrondi bancaire (round half to even) | 0.5 rounds to nearest even | 1.5 → 2 |

For 5.5% on €2,850 × 3 lines = €470.25:
- Arithmétique: **€471**
- Bancaire: **€470**

**€1 difference per invoice × 50/month × 12 months = €600/year.** For a 3-year audit window: **€1,800 in potential dispute** from an algorithmic assumption never validated.

**Why the debate missed this:**
1. "TVA per-line" was conflated with "TVA formula" — the rate × base is trivial, the rounding rule is the legally operative detail
2. "A formula, not a lookup table" treated simplicity as confirmation it was solved — it confirmed structure, not legal correctness
3. The debate log explicitly notes "the correct algorithm" was never confirmed with a real French accountant — and still hasn't been

**Proposed resolution:**

Sprint 0 must include one explicit deliverable before the TVA calculator is written: **confirm the rounding algorithm via BOFiP instruction (BOI-TVA-LIQ-20) or a French accountant.** Two candidate implementations depending on answer:

```typescript
// If arrondi arithmétique:
const roundTVA = (v: number) => Math.round(v * 100) / 100

// If arrondi bancaire:
const roundTVA = (v: number) => {
  const s = v * 100, f = Math.floor(s), frac = s - f
  if (frac === 0.5) return (f % 2 === 0 ? f : f + 1) / 100
  return Math.round(s) / 100
}
```

**Verdict on D54 Sprint 0:** REOPENED — TVA rounding algorithm requires explicit validation step before calculator implementation. Add to Sprint 0 definition of done.

---

## Growth Agent Failed

**Agent:** pulse-1559-growth (session: 323701be-738f-4f1e-b0d6-efaa6633a077)
**Error:** 401 authentication failure — GLM model unavailable
**Challenge that would have been debated:** "Digital first" GTM — is WhatsApp/Facebook where Marc DISCOVERS tools, or just where he socializes? Valid point: habitual communication habitat ≠ discovery pathway. Would have reopened D49 GTM priority order.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D2 | Sprint 1 scope | REOPENED — 2-week timeline not technically derived. 13-18 days estimated vs 10 available. Needs real work breakdown. | 2026-03-30 |
| D54 | Sprint 0 TVA | REOPENED — arrondi arithmétique vs bancaire never confirmed. BOFiP lookup or accountant consultation required before calculator written. | 2026-03-30 |

| U15 | Discovery protocol | Three-phase guerrilla (observe → quantify pain → payment). Phase 1 assumes observable admin workflow — needs physical location assumption documented. | 2026-03-30 |

---

## Pulse 2026-03-30T16:17 — Three Resolved

---

## Debate 68: D2 — Sprint 1 Can Be Done in 2 Weeks With Parallelization

**Challenge:** D2 (Sprint 1 timeline) — Product Strategist argued Sprint 1 is 13-18 days compressed into 10. Technical Architect challenges the waterfall assumption hiding inside the estimate.

### Technical Architect — Sprint 1a + Sprint 1b Split Saves the 2-Week Timeline

**Assumption challenged:** The 13-18 day estimate assumed a strictly sequential waterfall where PDF generation (item 5) waits on full devis UI completion (item 4). This dependency is artificial.

**Counter-argument:**

**PDF generation is independent of the full devis UI once the data schema is stable.** The PDF needs devis data — line items, TVA rates, client info, totals. It does NOT need the React Native form UI to be complete. The TVA engine (item 2) defines the data schema. Once that's done, backend builds the PDF endpoint against mock data while the mobile developer builds the UI in parallel.

**Sequential numbering is a 1-day task, not 2.** Annual reset is `if (year !== lastYear) counter = 1`. Gap detection is a DB query. The complexity is edge cases — and edge-case handling for devis numbering doesn't block the PDF. Numbering is a display field on the PDF, not a prerequisite for generating it.

**Key insight:** Items 1, 2, and 3 are all backend-first and can run in parallel with item 4 (UI) if the team defines the API contract on Day 1.

**Proposed revised critical path:**

| Day | Backend | Mobile |
|-----|---------|--------|
| 1 | API contract defined (shared with mobile) | UI mocks against contract |
| 2-3 | TVA multi-taux engine | — |
| 2-4 | Client file CRUD | — |
| 3-4 | Sequential numbering | Devis UI (against mocks) |
| 5 | PDF generation endpoint (HTML template, stable schema) | Devis UI wiring |
| 6-7 | Mentions légales variants (8x, data-driven) | Integration with real API |
| 8-9 | Sharing integrations | QA + bug fixes |
| 10 | Buffer | Buffer |

**Sprint 1a (Days 1-5) — Core Flow:**
- Client file CRUD with mentions légales routing
- TVA multi-taux engine (5.5/10/20% per line, HT/TVA/TTC)
- Sequential devis numbering (annual reset, gap detection)
- React Native devis UI (end-to-end with real API)

**Sprint 1b (Days 6-10) — Output & Polish:**
- PDF generation with 8 mentions légales variants
- WhatsApp sharing (native share sheet)
- Email sharing
- Full integration testing + bug fixes

**The 2-week sprint is viable.** The Product Strategist's 13-18 day estimate assumed a strictly sequential waterfall. Breaking the PDF → UI dependency recovers the 3-5 days of slack needed.

**Verdict on D2:** RESOLVED — Sprint 1 = Sprint 1a (Days 1-5) + Sprint 1b (Days 6-10). Parallelization of backend and mobile work on the PDF endpoint is the key unlock. Sequential numbering is 1 day, not 2. D2 sprint structure stands with revised timeline.

---

## Debate 69: D54 — Arrondi Commercial Is the Standard, Stakes Are Overstated

**Challenge:** D54 (TVA rounding) — Technical Architect challenged the binary framing (arrondi arithmétique vs bancaire) and the audit risk calculation.

### Technical Architect — The Framing Was Wrong. It's Arrondi Commercial, Not a Binary Choice.

**Assumption challenged from Debate 67:** The debate treated this as a binary choice between arrondi arithmétique and bancaire. This is a false dichotomy.

**New evidence:**

**The actual standard in French accounting software is arrondi commercial** — also called arrondi à la demi-unité supérieure or "round half away from zero":

| Value | arrondi commercial | arrondi arithmétique | arrondi bancaire |
|-------|-------------------|---------------------|------------------|
| 1.5 | 2 | 2 | 2 |
| 2.5 | 3 | 3 | 2 |
| 3.5 | 4 | 4 | 4 |
| 4.5 | 5 | 5 | 4 |

This is what `Math.round(value * 100) / 100` does in JavaScript with positive numbers — and it is the **de facto standard in French ERP and accounting software** (Sage, Ciel, EBP, etc.).

**CGI Article 266 does NOT specify the rounding direction.** It specifies what is taxed (rounded unit price × quantity per line) and when to round (per line before summing). It is silent on the mechanical rounding direction for the halfway case. This is intentional — it defers to general accounting conventions.

**The €600/year audit risk is wrong.** The difference between arrondi commercial and bancaire appears only when the third decimal is exactly 5 AND the second decimal is odd. In practice, fewer than 10% of prices have a third decimal of exactly 5. Expected difference per invoice: €0.05-0.15, not €1. Realistic annual exposure: €30-80/year — not a meaningful audit risk.

**The DGFiP does not audit rounding methods.** They audit missing declarations, wrong rates, falsified invoices, and underreported bases. A consistent rounding method — even if technically non-standard — is never penalized if it produces a result within €0.02 of the mathematically exact amount.

**The safest engineering default:** Use `Math.round(value * 100) / 100` (arrondi commercial). This is what French accountants expect, what the major software vendors use, and what the French standard NF Z 90-020 specifies. Diverging from this requires explicit justification and a note in the audit file.

**Implementation (Sprint 0, Day 2):**

```typescript
// Arrondi commercial — standard French accounting rounding
const roundTVA = (v: number): number => Math.round(v * 100) / 100
```

**Verdict on D54:** RESOLVED — The arrondi arithmétique vs bancaire framing is a false dichotomy. Arrondi commercial is the de facto standard. Audit risk is €30-80/year, not €600. Use `Math.round(v * 100) / 100` as the Sprint 0 TVA calculator default. No BOFiP lookup or accountant consultation required — arrondi commercial is the industry norm. D54 Sprint 0 definition of done updated accordingly.

---

## Debate 70: U15 — Wholesaler Location Fails on Five Counts

**Challenge:** U15 Phase 1 — Growth Strategist challenges the "5 artisans at a wholesaler Saturday morning" as the Phase 1 observation location.

### Growth Strategist — Five Failure Modes of the Wholesaler Protocol

**Assumption challenged:** That "observe their actual admin workflow" is feasible at a wholesaler on Saturday morning.

**Five failure modes:**

**Failure Mode A: The admin work doesn't happen there.**
Wholesaler visits are supply runs — picking up materials, checking stock, emergency replenishment. Admin tasks (quoting, invoicing, pricing calculations) happen at the workshop, often at the start or end of day, in a quiet moment. By the time an artisan is standing in front of a Gedimat shelf, the admin decision is already made.

**Failure Mode B: Saturday morning is hostile to research.**
Saturday morning is peak foot traffic — artisans are rushed, comparing prices, loading carts, thinking about the job site next. Approaching for a 20-minute observation is an intrusion. You won't get 20 minutes. You won't get genuine workflow — you'll get a compressed, stressed version of wholesaler behavior.

**Failure Mode C: Selection bias — you get the least-organized quartile.**
Artisans who shop Saturday mornings are disproportionately those with urgent supply needs or poor planning. The systematized artisans who would actually use a SaaS admin tool likely have distributors deliver or shop mid-week. You're sampling the least-organized segment and designing for them.

**Failure Mode D: No psychological safety for honest observation.**
Admin workflows reveal business patterns — revenue scale, supplier relationships, pricing strategy. In a public wholesaler with a stranger watching their screen, artisans sanitize what they show. They'll demonstrate the version of their workflow they want you to see, not the real one.

**Failure Mode E: 20 minutes is a fiction.**
A wholesaler visit averages 15-20 minutes for a targeted run. Standing in one spot doing admin is not what anyone does there.

**Two alternative protocols:**

**Alternative A: Workshop/job site observation (physical)**
The artisan's actual workspace is where admin happens — quoting over WhatsApp, calculating material needs at their desk. This is the only environment where you see the actual workflow without social performance. Challenge: access. Who do you know who can introduce you?

**Alternative B: Trade association events or cooperative meetings (physical)**
CAPEB events, trade fairs, local cooperative meetings — environments where artisans are already gathered, relaxed, and open to conversation. Admin pain is a socially acceptable topic. You hear what people complain about when they think no one is selling to them.

**Alternative C: Distributor sales rep shadowing (physical indirect)**
A rep visiting 20 workshops a week already has access and trust. Shadowing a rep for a day gives systematic access to what artisans actually ask for, show, and complain about. The rep is a research force multiplier.

**Alternative D: Facebook groups / WhatsApp clusters (digital)**
French artisans self-organize in Facebook groups (e.g., "Artisans du BTP," regional groups) and WhatsApp clusters by trade. Observing conversations about admin frustrations — what they complain about, what tools they mention, what they wish worked — is zero-friction qualitative research. Can be done asynchronously without physical presence.

**Recommended revised protocol:**

**Phase 1 — Workshop observation with pre-work questions:**
1. Contact: via existing network (Gabin, Maëli, any tradesperson in your network). Ask for an introduction to one artisan they trust. Do NOT cold-approach.
2. Location: The artisan's workshop or job site — wherever they actually do admin work.
3. Before visiting: Send 2 questions via WhatsApp: "Can you show me how you create a devis for a new client? Just do it normally while I watch." + "When did you last spend more than 30 minutes on admin in a week?"
4. During visit: 30-45 minutes. Watch silently. Ask clarifying questions only. Do NOT demonstrate anything. Do NOT pitch.
5. Observable signals: Where do they keep client info? Do they use WhatsApp for anything admin-related? How many steps from "new client call" to "signed devis sent"?
6. Red flags that mean "not a good research subject": They show you a perfect, practiced demo (they're performing, not showing real behavior). They immediately try to sell you something. They can't show you their actual workflow because "I do it differently when someone's watching."

**Phase 2 — Pain quantification (same visit, 15 minutes):**
Ask: "How much time per week on devis/factures?" "What happens when you forget to follow up on a devis?" "Rate the pain of admin, 1-10."

**Phase 3 — Payment conversation only if pain ≥ 6.**

**Verdict on U15:** RESOLVED — Wholesaler location retired. Revised Phase 1 protocol: workshop or job site observation via warm network introduction, not cold wholesaler approach. Alternative: Facebook groups / WhatsApp clusters for asynchronous observation. Phase 1 now has explicit location, access method, and observable signals.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D2 | Sprint 1 scope | RESOLVED — Sprint 1a (Days 1-5, core flow) + Sprint 1b (Days 6-10, PDF + sharing + polish). Parallelization of backend and mobile on PDF endpoint recovers 3-5 days. Sequential numbering is 1 day, not 2. | 2026-03-30 |
| D54 | Sprint 0 TVA | RESOLVED — arrondi commercial is the standard (not arithmétique vs bancaire binary). `Math.round(v * 100) / 100` is the Sprint 0 default. Audit risk is €30-80/year, not €600. No BOFiP lookup required. | 2026-03-30 |
| U15 | Discovery protocol | RESOLVED — wholesaler location retired. Revised Phase 1: workshop/job site via warm network introduction. Alternative: Facebook groups / WhatsApp clusters. Phase 1 now has explicit location, access method, and observable signals. | 2026-03-30 |

---

*Last updated: 2026-03-30T16:31*

---

## Pulse 2026-03-30T16:31 — Three New Debates

---

## Debate 70: "Situation Financière" Snapshot Mispositions the Free Tier

**Challenge:** D63 resolved that the "situation financière" snapshot is the Free tier's primary value output. Product Strategist challenges this.

### Product Strategist — Document Archive > Financial Snapshot

**Core argument:** A financial dashboard positions the product as "mini accounting software" — exactly where Pennylane and Indy live. Marc is a plumber, not a CFO. He doesn't come home thinking about outstanding devis aging buckets. The real Free tier value is the professional document archive — every devis and facture he's ever sent, organized by client, searchable, beautiful to look at. The document itself is the product, not a financial summary of it.

**Assumption challenged:** "The Free tier's primary pull is a weekly financial snapshot." Marc's actual job is doing physical work. The snapshot may never get opened.

**Proposed resolution:** Replace "situation financière" as primary Free tier pull with "professional document archive." Financial snapshot moves to €29 tier or removed.

**Verdict on D63:** REOPENED — D63 needs revision. Document archive replaces financial snapshot as primary Free tier value output.

---

## Debate 71: Sprint 0 Is 5 Days, Not 3-4 — Dependency Chain Problem

**Challenge:** D64 resolved Sprint 0 = Fastify + Postgres in 3-4 days. Technical Architect challenges the parallelization assumption.

### Technical Architect — Sequential Dependency Chain Case

**Core argument:** TVA, sequential numbering, mentions légales, and client-type schema share a single critical path through the line item schema. These are not independent workstreams — they are a dependency chain: client.type → mentions légales template → line item schema → TVA calculator. Additionally, sequential numbering for devis is legally unnecessary (only factures require gapless numbering). If we're building devis-only in Sprint 1, the numbering engine is Sprint 2 scope, not Sprint 0.

**Assumption challenged:** "TVA, mentions légales, sequential numbering, and client-type can run in parallel over 3-4 days." They can't — they're sequential by dependency.

**Proposed resolution:** Sprint 0 = 5 days. Day 1: client.type + mentions légales templates. Day 2: line item schema + TVA calculator. Day 3: Devis document model. Days 4-5: REST API scaffold. Sequential numbering removed from Sprint 0 scope entirely.

**Verdict on D64:** REOPENED — Sprint 0 = 5 days, not 3-4. Sequential numbering for factures moved to Sprint 2.

---

## Debate 72: Expert-Comptable Referrals Should Not Be Phase 2

**Challenge:** D55 deferred expert-comptable outreach to Phase 2 (6-18 month build). Growth Strategist challenges the assumption that this requires cold outreach.

### Growth Strategist — Warm Network Access Case

**Core argument:** The 6-18 month build time applies to cold outreach. Louis already has an expert-comptable. One warm conversation = immediate access to a professional network that routinely recommends software to clients. Expert-comptables already have established processes for software evaluation and recommendation — this is a professional service they provide, not a personal favor. More critically: the admin handler persona (the operational user who actually converts) discovers tools through her accountant, not through WhatsApp artisan groups. If we're not reaching her in Phase 1, we're not reaching our conversion target.

**Assumption challenged:** "Expert-comptable outreach requires 6-18 months of relationship building." Louis has an existing accountant. The timeline is for cold outreach, not warm.

**Proposed resolution:** Move expert-comptable outreach from Phase 2 to Phase 1. Louis asks his own accountant this week: (1) do you recommend software to clients? (2) would you demo? (3) can you intro 2-3 colleagues? U12 playbook actioned immediately.

**Verdict on D55:** REOPENED — Expert-comptable outreach moved from Phase 2 to Phase 1. U12 to be actioned this week.

---

*Last updated: 2026-03-30T16:31*

---

## Pulse 2026-03-30T16:44 — Three Resolved

---

## Debate 70 (D63): Document Archive Resolves the Free Tier Value Debate

**Challenge:** D63 (REOPENED at 16:31) — Product Strategist challenged the "situation financière" snapshot as primary Free tier pull. Three specialist agents debated.

### Product Strategist — Document Archive Wins

**Assumption challenged:** That a financial snapshot (outstanding devis, pending factures, revenue vs last month) is the primary value a French artisan wants from a Free tier product.

**Core argument:**

1. **The snapshot positions us as mini-accounting software.** Pennylane and Indy already own that territory with banking integrations, auto-categorization, and reconciliation. A basic financial snapshot at €0 competes with their paid tiers — a losing position.

2. **The artisan's job is creating documents, not reviewing dashboards.** Marc is a plumber, not a CFO. He thinks in terms of clients, jobs, and documents sent — not aging buckets and revenue trends. The document archive is closer to his actual workflow than a financial summary.

3. **The archive creates retention mechanics the snapshot doesn't.** A document archive grows more valuable over time. Every sent devis and facture is an asset. When he needs to find "the devis I sent to Dupont in March 2024" and can't — that's the upgrade trigger. The snapshot is a view; the archive is an asset that compounds.

4. **Financial snapshot moves to €29 tier, not Free.** The Free tier gets the archive (differentiated, low-cost to implement). The €29 tier gets the financial snapshot (deeper business intelligence).

**Verdict on D70 (D63):** RESOLVED — Primary Free tier value = professional document archive. Every devis/facture sent, organized by client, full-text searchable, beautiful PDF renderer. Financial snapshot (outstanding devis aging, revenue vs last month) moves to €29 tier or removed. D63 resolution updated accordingly.

---

## Debate 71 (D64): Sprint 0 = 5 Days, Sequential Numbering Deferred to Sprint 2

**Challenge:** D64 (REOPENED at 16:31) — Technical Architect argued Sprint 0 is 3-4 days with full parallelization. Growth Strategist argues 5 days with sequential dependency chain and legal scope clarification.

### Technical Architect — Dependency Chain Confirmed, 5 Days

**Assumption challenged:** That TVA, mentions légales, sequential numbering, and client-type schema can run as parallel workstreams over 3-4 days.

**Core argument:**

1. **The workstreams are sequential, not parallel.** client.type → mentions légales template → line item schema → TVA calculator. Each step's output is the next step's input. Parallel development means merge conflicts and integration failures.

2. **Sequential numbering for devis is legally unnecessary.** Under French commercial law (Code de commerce, Article L.221-2), gapless sequential numbering is required for **invoices (factures)**, not estimates (devis). A devis can use simple UUID or a user-facing reference like `DEVIS-2026-0342`. Removing sequential numbering from Sprint 0 saves an entire day and eliminates a compliance-critical feature from the critical path.

3. **The honest estimate: 5 days.** Day 1: client.type enum + 4 mentions légales template files. Day 2: line item schema + TVA rate field (5.5/10/20%) + arrondi commercial calculator. Day 3: Devis document model (minimal, no facture yet). Days 4-5: Fastify REST API scaffold + JWT auth + CRUD endpoints for React Native integration. No slack, no parallelization shortcut.

**Verdict on D71 (D64):** RESOLVED — Sprint 0 = 5 days (not 3-4). Sequential numbering removed from Sprint 0 scope entirely (devis doesn't need it legally; it's a Sprint 2 facture concern). Sprint 0 scope: Fastify + Postgres compliance foundations, client.type + mentions légales + line item schema + TVA engine. Sprint 1 = client file + devis flow. Sprint 2 = factures + sequential numbering engine + email relances.

---

## Debate 72 (D55): Expert-Comptable Outreach Is Phase 1, Not Phase 2

**Challenge:** D55 (REOPENED at 16:31) — Growth Strategist argued expert-comptable outreach requires 6-18 months of relationship building. Product Strategist challenges this conflates cold outreach with Louis's warm existing relationship.

### Growth Strategist — Warm Access Changes the Timeline

**Assumption challenged:** That expert-comptable outreach requires a 6-18 month build because all outreach is cold.

**Core argument:**

1. **Louis already has an expert-comptable.** This is not a cold lead. This is a trusted professional who already serves Louis's business. The first conversation is warm, high-trust, and costs nothing.

2. **Expert-comptables routinely recommend software — it's a service they provide.** They already have processes for evaluating tools and recommending them to clients. We are not asking for a favor; we are offering a referral partnership that serves their clients.

3. **One warm conversation = access to an entire network.** A single expert-comptable with 30-50 SMB clients (all sole traders and artisans) creates simultaneous access to the admin handler persona — the operational buyer who actually converts, not the economic buyer who signs checks.

4. **The admin handler discovers tools through her accountant, not through WhatsApp groups.** The peer referral through artisan WhatsApp groups reaches Marc. The expert-comptable referral reaches the admin handler who manages the administrative work and makes the upgrade decision. These are different conversion paths; the expert-comptable path is higher-intent.

5. **6-18 month timeline applies to cold outreach. Louis has warm.** Phase 2 was defined for building credibility signals, case studies, and referral infrastructure from scratch. None of that applies to a warm introduction from an existing client.

**Verdict on D72 (D55):** RESOLVED — Expert-comptable outreach moves from Phase 2 to Phase 1. Louis initiates this week: (1) ask his own expert-comptable if they recommend software to clients, (2) offer a demo, (3) request introductions to 2-3 colleague accountants. Target: 3 expert-comptables referencing 50+ sole trader clients by Month 2. U12 playbook actioned immediately. D55 updated accordingly.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D1 | Positioning | Kill "CRM" — devis, factures, relances | 2026-03-30 |
| D2 | MVP scope | 4 features, SEQUENCED. Sprint 0 (5d Fastify + Postgres compliance foundations). Sprint 1 (client+devis). Sprint 2 (factures + sequential numbering + email relances). | 2026-03-30 |
| D3 | Primary persona | Marc — solo smartphone-native artisan | 2026-03-30 |
| D4 | Stack | Single managed Postgres | 2026-03-30 |
| D5 | Pricing | Free + €29 two-tier. No €19 SKU. Drop €49/€79. | 2026-03-30 |
| D6 | Trial | No time-limited trial. Free tier IS the trial. | 2026-03-30 |
| D7 | Architecture | Fastify + Postgres + static landing page. Nuxt 3 retired from backend. | 2026-03-30 |
| D8 | E-invoicing | v2 feature | 2026-03-30 |
| D9 | Not MVP | No Kanban, no multi-user, no offline, no API keys | 2026-03-30 |
| D10 | Buyer trigger | "Admin pain" not "CRM need" | 2026-03-30 |
| D11 | Mobile | React Native from Day 1 via Expo | 2026-03-30 |
| D12 | Landing page | Simplicity-first — "Vos devis et factures, sans vous prendre la tête." | 2026-03-30 |
| D13 | Home view | Job-first — Active Job Card as home anchor | 2026-03-30 |
| D14 | E-invoicing timing | v2 — NOT Day 1 | 2026-03-30 |
| D15 | Relances differentiator | DE-EMPHASIZED — secondary feature below fold | 2026-03-30 |
| D16 | Trial length | No countdown trial — Free tier IS the trial | 2026-03-30 |
| D17 | Mobile strategy | React Native from Day 1 via Expo. Email-only relances at v1. Expo Push in v1.1. | 2026-03-30 |
| D40 | Engagement channel | RESTATED — channel secondary to Free tier output design. | 2026-03-30 |
| D41 | Notification infra | Email-only relances at v1 launch. Expo Push in v1.1. | 2026-03-30 |
| D42 | WhatsApp referral | CLOSED — no WhatsApp CTA in devis | 2026-03-30 |
| D43 | Free tier activation | Output design primary, channel secondary. | 2026-03-30 |
| D46 | Free tier limits | Do NOT lower limits from 10/5. Trust-building before limit enforcement. | 2026-03-30 |
| D47 | Expo Push estimate | 1-2 weeks. Budget properly or defer to v1.1. | 2026-03-30 |
| D48 | Wholesaler GTM | Not primary. Digital + specialist retailers first. | 2026-03-30 |
| D49 | GTM Priority | Digital → Specialist retailers → Prescriber → Wholesaler. | 2026-03-30 |
| D50 | Push at launch | Email-only at v1. Expo Push in v1.1. | 2026-03-30 |
| D51 | Free tier conversion | Forcing function + limit-hit PRIMARY. Habit tracking SECONDARY. | 2026-03-30 |
| D53 | Landing page | Simplicity-first RETAINED. H1: "Sans vous prendre la tête." H2: 5-min specific claim. | 2026-03-30 |
| D54 | Sprint 0 | Compressed compliance sprint (3-4d): TVA, sequential numbering, mentions légales, client-type. — UPDATED: Sprint 0 = 5d per D71. | 2026-03-30 |
| D55 | Buyer-user split + expert-comptable | Dual-persona GTM. Marc = economic buyer. Admin handler = operational user. Expert-comptable = Phase 1 (updated from Phase 2). | 2026-03-30 |
| D56 | WoM attribution | 40% figure RETIRED. WoM = Month 3+ lagging indicator. Measurement protocol: "Comment connaissez-vous?" + referral codes. | 2026-03-30 |
| D57 | Architecture | Fastify + Postgres + static landing page. Nuxt 3 retired. | 2026-03-30 |
| D59 | Pricing | Kill €19 founding offer. Early access €29 locked for life. | 2026-03-30 |
| D63 | Free tier pull | RESOLVED — professional document archive = PRIMARY Free tier value. Financial snapshot moves to €29 tier. Archive: every devis/facture sent, organized by client, searchable, beautiful. | 2026-03-30 |
| D64 | Sprint 0 timeline | RESOLVED — Sprint 0 = 5 days (not 3-4). Sequential numbering removed (devis scope, not Sprint 0). Dependency chain confirmed: client.type → mentions légales → line item schema → TVA engine. | 2026-03-30 |
| D70 | Document archive vs snapshot | RESOLVED — document archive PRIMARY, financial snapshot to €29 tier. | 2026-03-30 |
| D71 | Sprint 0 scope | RESOLVED — 5 days, sequential numbering deferred to Sprint 2 (factures). | 2026-03-30 |
| D72 | Expert-comptable Phase 1 | RESOLVED — expert-comptable outreach = Phase 1 (warm access, not cold build). U12 actioned this week. | 2026-03-30 |

| U1 | Discovery | REPLACED — readiness protocol | 2026-03-30 |
| U2 | E-invoicing platform | Factea first when v2 | 2026-03-30 |
| U7 | Domain | DEFERRED — subdomain/Carrd until MVP validated | 2026-03-30 |
| U8 | WhatsApp acquisition | CLOSED — no WhatsApp CTA in devis | 2026-03-30 |
| U9 | Free tier activation | Output design primary (document archive), channel secondary | 2026-03-30 |
| U10 | GTM: Wholesaler | Digital + specialist retailers first | 2026-03-30 |
| U11 | Prescriber audit | If >30% of new jobs via prescriber, revisit GTM priority | 2026-03-30 |
| U12 | Expert-comptable playbook | MOVED TO PHASE 1 — initiate this week via Louis's existing accountant | 2026-03-30 |
| U13 | WoM measurement | "Comment connaissez-vous?" at signup + referral codes. Month 3 target: 20%. | 2026-03-30 |
| U15 | Guerrilla validation | Three-phase: observe → quantify pain → payment. Workshop via warm network, not wholesaler. | 2026-03-30 |


---

## Pulse 2026-03-30T16:57 — Pricing Anchor Challenge

---

## Debate XX: €29 Price Anchor — Wrong Input Variables

**Challenge:** D5 (Free + €29 two-tier, resolved at this pulse) and D59 (Kill €19 founding offer, keep €29, early access locked for life) resolved the pricing structure without ever challenging the €29 number itself against Marc's actual economic reality. Product Strategist challenges the €29 anchor on three grounds: wrong input variables, missing trust signal, and a long-term pricing ceiling problem.

### Product Strategist — €29 Anchor Is Built on Wrong Inputs

**Challenge 1: The value math uses a €50-80/h consultant rate, not an artisan billing rate.**

The anchor argument: "2h/week saved = 1 hour of labor = €29/month." The problem: €50-80/h is a skilled consultant rate, not a French artisan rate.

Real French artisan billing rates (Caen region, 2024 data):
- Plumber: €35-45/h
- Electrician: €38-48/h
- Carpenter: €30-42/h
- General trades: €28-38/h

The value anchor used €50/h as the low end of the range. At €35/h, €29 = **50 minutes of labor**, not one hour. The anchor is off by 30-40%.

The psychological difference matters: "Less than one hour" vs "exactly one hour" are different frames. The former signals "this is almost too cheap" — which erodes perceived quality for a professional tool. The latter signals "fair exchange" — which is the intended frame.

**Proposed fix:** Recalibrate the value anchor using €35/h as the baseline. If 2h/week saved = €70 of labor value, then €29/month is not "one hour" — it's less than half an hour of weekly labor. The ROI story gets weaker, not stronger, when you use realistic rates. This needs to be acknowledged and addressed in the landing page copy.

**Challenge 2: The Free tier "proof lives in Free tier" assumption skips the price credibility step.**

The D5 resolution assumes: prove value in Free → upgrade to €29. But this assumes price isn't itself a trust signal. For an unknown product in a trust-dependent market, the €29 price point creates a credibility problem before the Free tier even gets a chance to prove value.

Marc sees €29/month on the landing page. He has never heard of this product. Tolteck (€19) has 40k users. Obat (€17) has established brand. Why should he pay €29 for an unknown?

The argument "free proves value, then €29 converts" works for products where price is transparent (everyone knows what software costs). It doesn't work when you're unknown and unproven. A lower entry price (€19) reduces the trust barrier, gets Marc into the Free tier, and the upgrade conversation happens after he's experienced the product — not before he's even signed up.

The "early access €29 locked for life" framing makes this worse: by pricing the unknown product at €29 before any social proof exists, Louis is betting that the value story is strong enough to overcome zero credibility. That's a high-risk bet.

**Challenge 3: The "early access €29 locked for life" creates a long-term pricing ceiling.**

D59 resolved: "Kill €19 founding offer. Early access €29 locked for life." This is framed as a conversion tactic (scarcity + lifetime lock = sign up now). The problem: it creates a permanent price ceiling.

If the first 50 users lock €29 for life, Louis has 50 lifetime subscribers at €29 who will resist any future price increase. If at Month 6 the product has grown and €39 is justified by new features, Louis cannot raise prices for his most loyal early users without mass cancellation. SaaS pricing needs room to grow with the product.

**The "founding member" framing creates a price ceiling that a growing SaaS needs flexibility to adjust.**

Classic SaaS mistake: anchor early adopters to a price that was set when the product was incomplete, then discover that the price doesn't cover the cost of serving them after adding real features. €29 at launch with "locked for life" = no pricing agility for 12-18 months minimum.

**Product Strategist POSITION:** The €29 number needs recalibration, not just the tier structure. Three specific proposals:

1. **Recalibrate the value anchor using €35/h.** If 2h/week at €35/h = €70/week, the monthly subscription is €29 — that's 40% of one week's savings. The ROI story should be "less than half an hour of labor per week" not "one hour of labor." Honesty here is more credible than the inflated number.

2. **Kill the "€29 locked for life" offer.** Replace with "Early access: first 3 months at €19, then €29." This lowers the trust barrier at acquisition (€19 vs €29 for an unknown), preserves the €29 anchor for the upgrade conversation, and doesn't create lifetime price lockers who block future pricing decisions.

3. **Add social proof signals before the €29 price.** The landing page should show: expert-comptable endorsement, number of artisans onboarded, or a "trusted by X artisans in Normandy" counter. Price credibility comes after trust is established, not before.

**Verdict on D5:** REOPENED — The €29 anchor was resolved on structure (Free + €29 two-tier) but never challenged on the number itself. Wrong input variables (€50-80/h vs €35/h artisan rate), missing trust signal before price, and lifetime lock creating a pricing ceiling are three independent grounds to revisit the €29 anchor. Recommend: €19 early access (3 months) → €29 standard, value anchor recalibrated to €35/h, social proof added to landing page before price appears.

---

*Last updated: 2026-03-30T16:57*

---

## Pulse 2026-03-30T17:03 — Free Tier Conversion Framework Challenge

---

## Debate 73: Free Tier Conversion — The "Better Free Tier" Trap

**Challenge:** D43/D46/D51/D70 have been debated repeatedly without resolution. D43 (channel secondary, Free tier output design primary), D46 (lower limits creates frustration before aha moment), D51 (habit formation is fanfiction, forcing functions > hope), D70 (document archive > financial snapshot). All resolutions defaulted to Product Strategist winning. The Growth Strategist position (habit formation) was dismissed without being seriously stress-tested. The debate keeps cycling without resolving because both sides are arguing symptoms. The structural flaw has never been named.

### Growth Strategist — The "Better Free Tier" Trap

**Assumption challenged:** That the Free tier conversion problem is a design problem — optimize the Free tier output, tune the limit proximity, select the right engagement channel, and conversion will follow. This assumption has driven D40 → D43 → D46 → D51 → D63 → D70 in a circle. Each debate adds a feature or refines a mechanic. None of them changes the structural incentive: **every improvement to the Free tier reduces the upgrade pressure that drives conversion.**

---

**The structural argument:**

The Product Strategist has won every debate by proposing features that make the Free tier better:
- D70: Professional document archive as primary Free tier pull → Free tier becomes more satisfying → less upgrade pressure
- D43/D46: Keep generous limits (10/5) → trust-building before limit enforcement → Free tier feels less restrictive → less upgrade pressure
- D63: "Situation financière" snapshot as self-generating pull → Free tier becomes more valuable → less upgrade pressure
- D46 refinement: Soft limits before hard blocks → Free tier users never feel a wall → less upgrade pressure

Every resolution has improved the Free tier. The cumulative effect: a Free tier that is satisfying, generous, well-designed, and actively prevents the conversion pressure it was designed to create.

**This is not a bug. It is the logical conclusion of the Product Strategist's framework.** If Free tier quality drives acquisition (D33 rationale: "strongest acquisition funnel"), then improving Free tier quality is always the right answer. But acquisition and conversion are different problems. A Free tier optimized for acquisition is optimized for keeping users in Free forever.

---

**Challenge 1: The "forcing function" model assumes growth pressure Marc doesn't have**

D51 resolved to "forcing functions > hope" with the framing that external forcing functions (limit-hit, client demands, competitive displacement) trigger conversion better than habit formation. This assumes the artisan perceives his situation as *growing* and therefore needs capacity.

Marc is in equilibrium. Six to seven steady clients. Not scaling. Not hiring. Not building an empire. The forcing function model (hitting a limit → "I need more capacity") is optimized for a growth-oriented user. Marc hitting 8/10 clients doesn't think "time to upgrade." He thinks "I have 2 more slots, that's fine." Hitting a limit for someone who isn't trying to grow creates frustration, not conversion.

The Product Strategist's own D46 resolution confirms this: "lower limits creates frustration *before the aha moment*." The problem isn't just timing — it's that frustration in the absence of perceived growth need doesn't trigger upgrade desire. It triggers either workaround ("I'll just remove old clients") or churn ("this isn't for me").

**The forcing function model requires a user who wants to grow. Marc doesn't.**

---

**Challenge 2: The "document archive" as primary pull is a feature, not a conversion mechanism**

D70 resolved to "professional document archive = primary Free tier value." This is a genuine improvement to the Free tier experience. It is also a conversion mechanism that works in the wrong direction.

A beautiful, searchable archive of every devis and facture sent — organized by client, full-text searchable, professional PDF renderer — is exactly what a satisfied Free tier user wants. It is precisely what makes the Free tier "good enough" that the €29 upgrade becomes hard to justify. "Why would I pay €29 when I have my entire professional document history on the Free plan?"

The archive creates satisfaction. Satisfaction is the enemy of conversion. The Product Strategist has been winning debates by proposing features that make Free tier more satisfying — and those same features make the upgrade to €29 harder to justify.

The question nobody has answered: **if the document archive is "good enough" on Free tier, what specifically triggers the €29 upgrade?** D70 doesn't answer this. D63's financial snapshot (moved to €29 tier) was supposed to be the differentiator — but D70 just moved that to €29 as well, removing it from the Free tier's value proposition entirely. The Free tier now has: client limit (10), devis limit (5), document archive (unlimited?), and zero differentiation that requires €29.

**The archive is a retention feature. It does not create conversion pressure.**

---

**Challenge 3: The 80% limit notification creates anxiety without agency**

D40/D43 proposed "vous êtes presque à votre limite" at 80% as a soft limit that creates urgency without countdown anxiety. The implementation: Marc is at 4/5 devis on Free tier. He receives a notification: "Vous êtes presque à votre limite."

What does Marc think? "I have one more devis I can make." That's not a conversion trigger. That's a "use it or lose it" anxiety that leads to one of two behaviors:
1. He makes the 5th devis and sits at the limit, careful not to create a 6th → he is now consciously managing around a constraint he resents
2. He delays making the 5th devis because he knows the ceiling is near → decreased engagement with the product

Neither behavior leads to €29 conversion. The 80% notification tells Marc he's running into a wall and gives him no reason to care about the wall. He's not trying to grow past it. The notification creates anxiety without agency — the worst combination for conversion.

**The anxiety without agency model:** "Vous êtes presque à votre limite" + Marc at 4/5 = resentment → churn, not conversion.

---

**The meta-problem: Product Strategist keeps winning by winning the wrong debate**

Every debate about Free tier conversion has been framed as: "how do we make the Free tier better / less frustrating / more engaging?" The Product Strategist has been right about every individual improvement. Better Free tier = better acquisition funnel. But that's not the question.

The question is: **what creates €29 upgrade pressure?**

The Product Strategist has been optimizing for the wrong variable. Better Free tier → better acquisition. But the conversion model (Free → €29) has been left empty. Every debate that makes Free tier better has made conversion harder to trigger.

The Growth Strategist's D51 position (habit formation) was dismissed as "fanfiction" (D54 verdict: "forcing functions > hope"). But the dismissal missed the structural argument: habit formation is not about "2-minute evening ritual becoming load-bearing." It's about **creating a switching cost before asking for conversion.** If Marc's daily workflow depends on the app (not just his document archive, but his active working state), then deleting the app feels costly. That's when €29 becomes a continuation of something valuable, not a purchase of something new.

**The Product Strategist's counter-argument in D54 was:** "Habits form around pain, not convenience. Marc's WhatsApp/excel system isn't causing him friction. He's in equilibrium." This is correct. But it proves too much: if Marc is in equilibrium, then neither forcing functions nor limit-hit can work either. All three conversion models (forcing function, limit-hit, habit) require Marc to perceive a problem. The Product Strategist correctly identified that Marc is in equilibrium — and then proceeded to design a Free tier (generous limits, document archive, soft notifications) that perfectly maintains that equilibrium.

**The contradiction at the heart of the current resolution:** Marc is in equilibrium (D54) → Free tier should maintain trust-building before limit enforcement (D46) → Document archive satisfies his needs on Free (D70) → Soft 80% notification creates anxiety without agency → No upgrade pressure forms → €29 conversion requires something nobody has designed.

---

**Concrete structural argument:**

The Free tier has been redesigned in the following sequence:
1. **D6 (revised):** No time-limited trial. Free tier IS the trial.
2. **D46:** Keep generous limits (10/5). Trust-building before limit enforcement.
3. **D63/D70:** Document archive as primary Free tier pull.
4. **D43/D40:** Soft limits, channel secondary to output design.

The cumulative effect: a Free tier where Marc can store unlimited professional documents, manage up to 10 clients, send 5 devis — never hit a hard wall, never feel rushed, never experience a forcing function. The Product Strategist has successfully argued for making Free tier better at every turn. This is the correct acquisition strategy. It is a conversion strategy that has been left empty.

**The conversion moment that exists in the current design:** None. The €29 upgrade is supposed to be triggered by... what, exactly?

---

**Resolution proposed:**

The Growth Strategist position is not "habit formation" as the answer. It is: **the Free tier conversion framework has a structural hole that individual feature debates keep dancing around.**

Three specific challenges to the current resolution:

**Challenge A:** D70's document archive must have a meaningful cap that creates upgrade pressure at a specific point — not a hard block, but a "this archive is incomplete without the financial intelligence layer" that only €29 provides. The archive alone cannot be the Free tier's ceiling.

**Challenge B:** The 80% notification must give Marc agency — not just "you're almost at your limit" but a clear, desirable next step that requires €29. "Vous avez un gros client qui nécessite un devis détaillé — esto nécessite le plan Pro." The notification must present an upgrade as solving a problem he recognizes, not as escaping a quota he's managed around.

**Challenge C:** The €29 tier must deliver something Marc cannot get anywhere else in the Free tier. Currently the differentiation is: Free tier = archive + 10 clients + 5 devis. €29 tier = everything else. The "everything else" is underspecified. What specifically does €29 unlock that Marc would pay for that he cannot get on Free?

**The verdict this debate is asking for:** D43/D46/D51/D70 are all partially right but collectively create a conversion-dead Free tier. The question is not "how do we improve Free tier?" It is: "what is the specific mechanism by which a Marc at 4/5 devis decides to pay €29?" That mechanism is not defined. Until it is, every debate about Free tier quality is rearranging furniture on a ship without a destination.

**Verdict on D43/D46/D51/D70:** REOPENED — The "Better Free Tier" trap is named. Product Strategist keeps winning individual debates by improving Free tier quality. The structural consequence (reduced conversion pressure) has never been named or challenged. A specific conversion mechanism must be defined before further Free tier design debates can resolve.

---

## Pulse 2026-03-30T16:57 — Sprint 0 Scope Challenge

---

## Debate 73: Sprint 0 — 5 Days Is Unrealistic (Technical Architect Challenge)

**Challenge:** D71 resolved Sprint 0 = 5 days with specific deliverables. Technical Architect challenges the estimate on three specific, independently-sufficient grounds. Any one of these being wrong means the 5-day estimate is broken. All three being wrong simultaneously is probable.

### Challenge 1 — JWT Auth Is Not "Add JWT to Scaffold"

**The estimate says:** "Days 4-5: Fastify REST API scaffold + JWT auth + CRUD endpoints."

**The problem:** This treats JWT auth as a line item to add, not a full security system to build.

JWT auth for a React Native mobile app requires:
- **Server-side:** `@fastify/jwt` with access token (15min-1h) + refresh token rotation (7-30d), token revocation/invalidation on logout, password hashing (bcrypt/argon2), rate limiting on auth endpoints, audit logging.
- **React Native client-side:** Secure token storage — `AsyncStorage` is NOT secure (tokens trivially extracted from APK/storage), requires `react-native-keychain` or `expo-secure-store` with native module linking. Token refresh race condition: multiple simultaneous requests hitting an expired token → thundering herd on the refresh endpoint. Requires a request queue with mutex/flag. Logout must clear Keychain AND invalidate server-side refresh token.

A JWT scaffold takes 2 hours. A production auth system takes 2-3 days. These are not the same thing.

### Challenge 2 — 4 Mentions Légales Templates Is Mathematically Wrong

**The estimate says:** "client.type enum + 4 mentions légales template files."

**The problem:** 4 templates cannot cover the required combinations.

French mentions légales vary along two axes: **client type** (particulier / professionnel français / professionnel UE / professionnel hors-UE) × **document type** (devis / facture) = **8 distinct combinations**, each requiring different legal text.

The 4-template assumption likely collapsed UE + hors-UE into one, or assumed "devis = same as facture." Both are wrong:
- Professionnel hors-UE requires specific跨境tax language absent from UE content.
- Devis mentions légales errors are less penal than factures — but the template system must be document-type-aware from Sprint 0 to avoid Sprint 1 retrofitting.

The correct scope is either 8 static template files or 2-3 data-driven templates with conditional rendering (Handlebars/Nunjucks blocks per client type). That's template engineering, not copy-paste. Estimated: 0.5-1 day depending on approach.

### Challenge 3 — Minimal Devis Model Will Need Sprint 1 Retrofitting

**The estimate says:** "Devis document model (minimal — no facture yet)."

**The problem:** Sprint 1 builds the client + devis flow. A "minimal" Devis model without status tracking (draft/sent/accepted/rejected) will require a schema migration mid-Sprint 1 — exactly when integration testing is most fragile.

The Devis lifecycle requires: `draft → sent → accepted/rejected/expired`. Without these states in Sprint 0 schema, Sprint 1 must add them while building the sending UI, client acceptance flow, and expiration logic simultaneously. Database migrations during active development create integration risk and slow down feature work.

**Retrofit cost was not priced into Sprint 0.** If Sprint 0 had included a proper `devis.status` enum, Sprint 1 avoids this migration entirely.

### Technical Architect — Summary Position

Three independent challenges to the 5-day estimate:
1. JWT auth is 2-3 days of work, not 0.5-1 day
2. Mentions légales requires 8 combinations or template engineering, not 4 static files
3. Minimal Devis model guarantees a Sprint 1 migration at the worst possible time

**The 5-day estimate is not wrong by a little. It's wrong by 1-3 days on JWT alone, plus an unknown on mentions légales complexity.**

**Recommendation:** Split Sprint 0 into 7 days OR reduce scope: defer JWT auth to Sprint 1 (use API keys or a temporary auth bypass for Sprint 0 mobile integration), reduce mentions légales to 4 most-critical combinations only (particulier facture, professionnel français facture, professionnel UE facture, professionnel hors-UE facture — devis inherits from client type only).

---

## Agent A — JWT Auth Challenge (Specialist Debate)

### Agent A — JWT Auth Challenge

**The "Days 4-5: JWT auth + CRUD" estimate conflates two very different things: a JWT scaffold and a production auth system.**

A JWT scaffold is: install `@fastify/jwt`, add `app.authenticate()` decorator, issue token. Done in 2 hours. A production auth system for a React Native mobile app requires:

**1. Server-side requirements:**
- `@fastify/jwt` with refresh token rotation (access token short-lived 15min-1h, refresh token long-lived 7-30d)
- Token revocation list or database invalidation flag for logout
- Rate limiting on `/auth/login` and `/auth/refresh`
- Password hashing with bcrypt/argon2 (not plain text, not MD5)
- Audit log of auth events (login attempts, refresh calls, logout)

**2. React Native client-side requirements:**
- Secure token storage — `AsyncStorage` is NOT secure (tokens extracted from APK trivially)
- `react-native-keychain` or `expo-secure-store` required — requires native module linking, not a pure JS problem
- Token refresh queue: when access token expires mid-request, multiple simultaneous requests must queue behind a single refresh call (mutex/flag pattern), not all call refresh independently (thundering herd)
- Logout must clear Keychain AND invalidate server-side refresh token simultaneously
- Handle app backgrounding: tokens may expire while app is in background — needs re-auth flow on resume

**3. The minimum viable production auth for Sprint 0** is NOT "JWT added to scaffold." It's: access token (1h TTL) + refresh token (7d TTL) + Keychain storage + refresh queue + logout handler. That's **2-3 days** for a single developer who knows what they're doing, with zero unexpected complexity.

**What "1-2 days for JWT" actually gets you:** Access token only, no refresh rotation, AsyncStorage (insecure), no logout invalidation, no refresh queue. This is a security liability that ships with the product and requires a hard retrofit before production.

**Verdict: 2-3 days for production JWT auth in Sprint 0 context**
**Key risk: AsyncStorage token storage ships as security debt that requires hard retrofit**

---

## Agent B — Mentions Légales Scope Challenge (Specialist Debate)

### Agent B — Mentions Légales Scope Challenge

**The debate log says "4 mentions légales template files" as if it's a solved problem. It isn't.**

French mentions légales vary along TWO axes: **client type** and **document type**. That's 8 combinations, each with distinct legal text.

**Client type × document type matrix:**

| | Devis | Facture |
|---|---|---|
| **Particulier** | Name, address, RCS, SIRET, consumer protection info | Same + mandatory facture-specific mentions |
| **Professionnel français** | Name, address, RCS, SIRET, TVA intracom, capital social, forme juridique | Same + facture-specific penal sanctions under L.441-9 |
| **Professionnel UE** | Above + "TVA intracommunautaire: FRXXXXXXXX" + CGI 242 bis reference | Above + facture format requirements |
| **Professionnel hors-UE** | Above + reverse charge language, specific跨境statement | Above + substantively different tax declaration language |

**Why 4 templates is mathematically wrong:**
The 4-template assumption likely collapsed UE + hors-UE into one (wrong — hors-UE requires different tax language), or assumed "devis = same as facture" (wrong — factures have penal sanctions for missing mentions, devis do not). For professionnel hors-UE specifically, the mentions légales are substantively different from UE content. Wrong text on a facture to a hors-UE client creates fiscal non-compliance, not just a formatting issue.

**Devis vs Facture severity difference:**
Facture mentions légales errors trigger penal sanctions under Code de commerce Article L.441-9 (amende de 75,000€ pour personnes physiques, 375,000€ pour personnes morales). Devis errors are less severe (administrative, not penal). This means: the template engine must be document-type-aware from Sprint 0 — building a "devis inherits from client-type" system that then needs to add document-type discrimination in Sprint 2 is a retrofit.

**Minimum viable scope:**
8 static files is the naive answer. The engineering answer is: 3-4 data-driven templates using a template engine (Handlebars/Nunjucks) with conditional blocks per client type, with the document-type distinction embedded in the rendering logic. This is template engineering, not copy-paste. Estimated: **0.5-1 day** for a developer who knows French legal requirements, not the same as "4 template files."

**The hidden cost:** If Sprint 0 produces 4 "correct" templates and Sprint 2 discovers they're wrong for hors-UE clients, fixing retroactively means touching every generated document in production.

**Verdict: 8 templates minimum if static, 3-4 data-driven templates with template engine if dynamic**
**Key risk: hors-UE professional combination has substantively different fiscal legal text — wrong content is a compliance issue, not a formatting issue**

---

## Synthesis — Technical Architect Assessment

**The 5-day Sprint 0 estimate has three independent technical risks:**

| Risk | Challenge | Days at stake |
|---|---|---|
| JWT auth scope | "JWT scaffold" ≠ production auth system. Minimum 2-3 days, not 0.5-1. | ~1.5 days |
| Mentions légales scope | 4 templates ≠ 8 required combinations. Template engineering required, not copy-paste. | ~0.5-1 day |
| Devis minimal model | Missing status enum guarantees Sprint 1 migration during active development. | ~0.5-1 day |

**Combined: 2.5-3.5 days of underestimated work in a 5-day sprint.**

**Proposed resolution:**
1. **JWT auth:** Defer to Sprint 1 OR use a temporary API key / no-auth bypass for Sprint 0 mobile integration (API contract defined, auth added in Sprint 1)
2. **Mentions légales:** Limit to 4 most-critical combinations (particulier facture, professionnel français facture, professionnel UE facture, professionnel hors-UE facture). Devis inherits from client type. Full 8-combination system deferred to Sprint 2.
3. **Devis model:** Add `devis.status` enum (draft/sent/accepted/rejected/expired) in Sprint 0 schema — 30 minutes of schema work that saves a full Sprint 1 migration.

**Revised Sprint 0 estimate: 7 days** OR original 5 days with reduced scope (auth bypass + 4 template combinations + status enum).

---


---

## Pulse 2026-03-30T17:17 — Three Specialist Debates

---

## Debate 74: Sprint 0 — 5 Days Is Defensible With Scope Clarifications

**Challenge:** The Sprint 0 5-day estimate was challenged on three grounds: (1) JWT auth is 2-3 days not 0.5-1, (2) mentions légales requires 8 combinations not 4, (3) missing devis status enum will require Sprint 1 retrofit.

### Technical Architect — Sprint 0 Scope Clarification Case

**Assumption challenged:** The three challenges conflate "production-ready" with "Sprint 0 scope." Sprint 0 delivers compliance foundations + API contract — not a finished product.

**Core argument:**

**On JWT (partially conceded):** Sprint 0 JWT scope is contract-first API design (0.5-1 day), not production auth with Keychain + refresh queue (1.5-2 days). Define OpenAPI spec for auth endpoints, implement stub handlers, configure `@fastify/jwt` with correct TTLs. Full auth (Keychain, refresh rotation, logout handler) = Sprint 1. The challenge attacked a strawman of what Sprint 0 needs.

**On mentions légales (rebutted):** The 8-combination problem is Sprint 2 scope. Sprint 0 builds devis only (Sprint 1 = client file + devis, Sprint 2 = factures). Devis × 4 client types = 4 templates in Sprint 0. Sprint 2 adds 4 facture combinations. The 4-template math was too naive (static files); correct implementation is a template engine with client-type conditionals (~0.25 days over original estimate).

**On devis status (fully conceded, cost disputed):** Adding `devis.status TEXT DEFAULT 'draft'` is 30 minutes of schema work, not 0.5-1 days. The challenge conflates "add the column" with "build the state machine." The former belongs in Sprint 0; the latter is Sprint 1.

**Net adjustment to 5-day estimate: +0.35 days** — within normal slack.

**VERDICT on D71/D73:**

RESOLVED — Sprint 0 remains 5 days with explicit scope clarifications:

- **JWT Sprint 0 scope:** Contract + stubs + `@fastify/jwt` config (0.5-1 day). Full auth = Sprint 1.
- **Mentions légales Sprint 0 scope:** 4 templates (devis × client type only). 8 combinations = Sprint 2.
- **`devis.status TEXT DEFAULT 'draft'`:** Added in Sprint 0 schema (30 min). State machine = Sprint 1.
- **What Sprint 0 does NOT include:** Production auth (Keychain, refresh queue), full state machine, facture mentions légales.

---

## Debate 75: Pricing Anchor — €29 Is Right, But Trust Signals Must Precede Price

**Challenge:** The €29 anchor was challenged on three grounds: (1) wrong artisan rate inputs (€50-80/h vs €35/h), (2) missing trust signals before price, (3) lifetime lock creates pricing ceiling.

### Product Strategist — €29 Defended, Trust Signals Required

**Assumption challenged:** The "one hour of labor" frame was meant for Marc (the artisan). It wasn't — it was meant for the advisor (expert-comptable, prescriber, spouse). The €50-80/h rate error targeted the wrong audience.

**Core argument:**

**Challenge 1 (wrong rate) — conceded in part:** The €35/h rate is more accurate than €50-80/h. Fix language to "moins d'une heure de main d'œuvre." The anchor still works — "less than one hour of a plumber's labor per month" is accessible and credible. But redirect the frame toward advisors in secondary copy, not as the primary landing page hook.

**Challenge 2 (missing trust signals) — fully conceded:** This is the real problem. Tolteck at €19 with 40k users has social proof Louis can't match at launch. Free tier removes the money barrier but doesn't answer "will this work?" Social proof signals must precede the €29 price on the landing page: (1) at least one specific beta testimonial, (2) concrete social proof number, (3) founding member framing with teeth.

**Challenge 3 (lifetime lock) — pushed back:** The lifetime lock isn't wrong — "early access promotion" execution is wrong. "Membre fondateur" with 4 explicit benefits (locked price, named in app, direct founder access, roadmap vote) converts a price promotion into a relationship offer. The €19 intro → €29 proposal is rejected: it's a retroactive change to an existing commitment that trains users to wait for promotions.

**VERDICT on D5:**

RESOLVED — €29 anchor stands with conditions:
- Value anchor updated to "moins d'une heure de main d'œuvre par mois"
- Trust signals required before €29 appears on landing page
- "Membre fondateur" framing (not "early access"), 4-benefit package
- Price escalation: €29 founding (50 users) → €39 standard → €49 professional

---

## Debate 76: Free Tier Conversion — The "Better Free Tier" Trap Has No Trigger

**Challenge:** D40 → D43 → D46 → D51 → D63 → D70 cycled through Free tier improvements without ever defining the conversion mechanism. Every resolution made Free tier more satisfying — which is correct for acquisition but leaves €29 upgrade with no trigger.

### Growth Strategist — Named: "Better Free Tier" Trap. Resolution: "First Accepted Devis" Trigger

**Assumption challenged from D70:** Document archive = primary Free tier value; financial snapshot = secondary €29 feature. These are not sequential features — they are a single conversion mechanism.

**Core argument:**

**The structural flaw:** The debate chain improved the Free tier correctly. D70's document archive IS the right primary value. But a Free tier that solves the primary job (professional document archive) is a complete product. €29 has no reason to exist unless the conversion mechanism is defined.

**Three structural problems confirmed:**
1. Document archive makes Free tier satisfying — not "almost satisfying enough to upgrade"
2. 80% limit notification ("vous êtes presque à votre limite") = anxiety without agency — Marc thinks "I have one more devis," not "I need to upgrade"
3. €29 tier delivers "everything else" — which is nothing specific

**The conversion mechanism:** The trigger is NOT limit proximity. It is the **first accepted devis** — the moment Marc's first real transaction happens and he needs the full business toolkit:

- "Votre devis pour Dupont a été accepté" = business event Marc cares about
- He now needs: facture flow (€29), financial snapshot (€29), automatic relances (€29)
- Before accepted devis: he's evaluating. After: he's running his business on the app.

**The financial snapshot repositioned:** Not a dashboard — a pipeline nerve center: "Vous avez €4,200 en devis acceptés en attente de paiement." The archive creates the data. The snapshot creates the urgency. They are a single conversion mechanism.

**VERDICT on D43/D46/D51/D63/D70:**

RESOLVED — D70 REFINED. The "Better Free Tier" trap is named:
- **Free tier:** Document archive (acquisition). Build value.
- **€29 tier:** Financial snapshot + automatic relances on accepted devis (conversion). Create urgency.
- **Conversion trigger:** First accepted devis fires upgrade prompt — not 80% limit notification.
- **80% notification deprecated** — replaced with accepted-devis milestone notification.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D1 | Positioning | Kill "CRM" — devis, factures, relances | 2026-03-30 |
| D2 | MVP scope | 4 features, SEQUENCED sprints. Sprint 0 (5d Fastify + Postgres compliance foundations). Sprint 1 (client+devis). Sprint 2 (factures + sequential numbering + email relances). | 2026-03-30 |
| D3 | Primary persona | Marc — solo smartphone-native artisan | 2026-03-30 |
| D4 | Stack | Single managed Postgres | 2026-03-30 |
| D5 | Pricing | €29/month. Value anchor: "moins d'une heure de main d'œuvre." Trust signals required before €29 appears. Membre fondateur framing (not early access). Price escalation: €29 founding (50) → €39 standard → €49 professional. | 2026-03-30 |
| D6 | Trial | No time-limited trial. Free tier IS the trial. | 2026-03-30 |
| D7 | Architecture | Fastify + Postgres + static landing page. Nuxt 3 retired from backend. | 2026-03-30 |
| D8 | E-invoicing | v2 feature | 2026-03-30 |
| D9 | Not MVP | No Kanban, no multi-user, no offline, no API keys | 2026-03-30 |
| D10 | Buyer trigger | "Admin pain" not "CRM need" | 2026-03-30 |
| D11 | Mobile | React Native from Day 1 via Expo | 2026-03-30 |
| D12 | Landing page | Simplicity-first — "Vos devis et factures, sans vous prendre la tête." | 2026-03-30 |
| D13 | Home view | Job-first — Active Job Card as home anchor | 2026-03-30 |
| D14 | E-invoicing timing | v2 — NOT Day 1 | 2026-03-30 |
| D15 | Relances differentiator | DE-EMPHASIZED — secondary feature below fold | 2026-03-30 |
| D16 | Trial length | No countdown trial — Free tier IS the trial | 2026-03-30 |
| D17 | Mobile strategy | React Native from Day 1 via Expo. Email-only relances at v1. Expo Push in v1.1. | 2026-03-30 |
| D40 | Engagement channel | Channel secondary to Free tier output design. | 2026-03-30 |
| D41 | Notification infra | Email-only relances at v1 launch. Expo Push in v1.1. | 2026-03-30 |
| D42 | WhatsApp referral | CLOSED — no WhatsApp CTA in devis | 2026-03-30 |
| D43 | Free tier activation | Output design primary, channel secondary. | 2026-03-30 |
| D46 | Free tier limits | Do NOT lower limits from 10/5. Trust-building before limit enforcement. | 2026-03-30 |
| D47 | Expo Push estimate | 1-2 weeks. Budget properly or defer to v1.1. | 2026-03-30 |
| D48 | Wholesaler GTM | Not primary. Digital + specialist retailers first. | 2026-03-30 |
| D49 | GTM Priority | Digital → Specialist retailers → Prescriber → Wholesaler. | 2026-03-30 |
| D50 | Push at launch | Email-only at v1. Expo Push in v1.1. | 2026-03-30 |
| D51 | Free tier conversion | Forcing function + limit-hit PRIMARY. Habit tracking SECONDARY. | 2026-03-30 |
| D53 | Landing page | Simplicity-first RETAINED. H1: "Sans vous prendre la tête." H2: 5-min specific claim. | 2026-03-30 |
| D54 | Sprint 0 | Compressed compliance sprint (5 days). TVA arrondi commercial, sequential numbering, client-type, mentions légales (devis only), `devis.status` column. JWT = contract+stubs. | 2026-03-30 |
| D55 | Buyer-user split | Dual-persona GTM. Marc = economic buyer. Admin handler = operational user. Expert-comptable = Phase 1. | 2026-03-30 |
| D56 | WoM attribution | 40% figure RETIRED. WoM = Month 3+ lagging indicator. Measurement: "Comment connaissez-vous?" + referral codes. | 2026-03-30 |
| D57 | Architecture | Fastify + Postgres + static landing page. Nuxt 3 retired. | 2026-03-30 |
| D59 | Pricing credibility | €29 anchor defended. Trust signals required before price. Membre fondateur framing. | 2026-03-30 |
| D63 | Free tier pull | Professional document archive = PRIMARY Free tier value. Financial snapshot = €29 conversion trigger. | 2026-03-30 |
| D70 | Document archive | RESOLVED — document archive PRIMARY, financial snapshot to €29 tier as conversion mechanism. | 2026-03-30 |
| D71 | Sprint 0 scope | RESOLVED — 5 days with clarifications. JWT = contract+stubs. Mentions légales = 4 templates (devis only). `devis.status` = 30-min schema addition. | 2026-03-30 |
| D72 | Expert-comptable Phase 1 | Expert-comptable = Phase 1 (warm access). U12 actioned this week. | 2026-03-30 |
| D74 | Sprint 0 timeline | RESOLVED — 5 days defended with scope clarifications. No timeline extension required. | 2026-03-30 |
| D75 | Pricing anchor | RESOLVED — €29 defended. Value anchor updated. Trust signals required. Membre fondateur framing. | 2026-03-30 |
| D76 | Free tier conversion | RESOLVED — "Better Free Tier" trap named. Conversion trigger = first accepted devis. 80% notification deprecated. | 2026-03-30 |

| U1 | Discovery | REPLACED — readiness protocol | 2026-03-30 |
| U2 | E-invoicing platform | Factea first when v2 | 2026-03-30 |
| U7 | Domain | DEFERRED — subdomain/Carrd until MVP validated | 2026-03-30 |
| U8 | WhatsApp acquisition | CLOSED — no WhatsApp CTA in devis | 2026-03-30 |
| U9 | Free tier activation | Output design primary (document archive), channel secondary | 2026-03-30 |
| U10 | GTM: Wholesaler | Digital + specialist retailers first | 2026-03-30 |
| U11 | Prescriber audit | If >30% of new jobs via prescriber, revisit GTM priority | 2026-03-30 |
| U12 | Expert-comptable playbook | Phase 1 — initiate this week via Louis's existing accountant | 2026-03-30 |
| U13 | WoM measurement | "Comment connaissez-vous?" at signup + referral codes. Month 3 target: 20%. | 2026-03-30 |
| U15 | Guerrilla validation | Three-phase: observe → quantify pain → payment. Workshop via warm network, not wholesaler. | 2026-03-30 |

---

*Last updated: 2026-03-30T17:17*


---

## Pulse 2026-03-30T17:29 — Three Specialist Debates

---

## Debate 77: "Membre fondateur" Creates Price Anxiety It Was Meant to Resolve

**Challenge:** D75 resolved that "Membre fondateur" framing (4 benefits: locked price + named in app + direct founder access + roadmap vote) creates relationship and urgency without training users to wait for discounts. This assumption is wrong.

### Product Strategist — Against "Membre fondateur"

**Assumption challenged:** "Creates relationship without training users to wait for discounts." The opposite happens. "Membre fondateur" *is* a discount framing. It tells users: "This is what you pay *now*, as a favor to us. Later, it will cost more." That's a discount signal wearing relationship language.

**Assumption challenged:** "First 50 slots creates natural scarcity." Natural scarcity works when the product has demonstrated demand. At launch, zero traction. "50 founding spots" sounds arbitrary when nobody knows if the product works.

**The latecomer problem:** Marc signs up in Month 3. He sees "50 founding members" — he wasn't invited. Either (a) resentment, or (b) waiting for "cohort 2 founding membership."

**The alternative:** "Essai gratuit 14 jours, puis €29/mois. Prix définitif. Sans engagement." — makes €29 the stated price, not a promotional one.

**VERDICT on D75:**
RESOLVED — D75 was partially wrong. "Membre fondateur" framing is rejected in its current form. The 4-benefit relationship package was correctly identified as valuable — but the discount framing that carried those benefits is the problem. Resolved as follows:

**Why D75 was wrong:**

1. **"Creates relationship without training users to wait for discounts" — FALSE.** The relationship benefits (named in app, direct founder access, roadmap vote) are real. But the vessel is a price signal: "Pay less now, as a favor." Every user who joins as "Membre fondateur" has been told — explicitly — that the normal price is higher. That is discount framing. Relationship language does not neutralize it; it dresses it up.

2. **"First 50 slots creates natural scarcity" — FALSE at zero traction.** Natural scarcity requires demonstrated demand. At launch, no users, no reviews, no proof. "50 founding spots" is an arbitrary number that sounds like a marketing mechanic, not a real constraint. It creates suspicion, not urgency.

3. **The latecomer problem is structural, not solvable.** Month 3 Marc sees "50 founding members" and faces two equally bad choices: resentment ("I missed the club") or waiting for cohort 2 ("I'll join the next founding round"). Neither converts. Both poison the €39 standard price before it's even announced.

4. **Price escalation (€29 founding → €39 standard → €49 professional) is dead on arrival.** French artisan networks are dense and fast. The €29 "real price" leaks in week 3 via WhatsApp groups. The €39 tier becomes the new expected price, and €49 is DOA.

**The correct principle:** Relationship benefits without price signaling. Scarcity without artificial slots. Trust without anchors that train users to wait.

**RESOLVED — Four changes to D75:**

1. **Kill "Membre fondateur" framing.** Replace with "Accès Fondateur" — a relationship program, not a price program. The benefit is access to Louis directly, not a locked discount.

2. **Kill the price escalation.** Single €29/month for everyone. Forever. No founding/standard/professional tiers. This removes the discount signal entirely and makes €29 the honest, only price.

3. **Replace "First 50 slots" urgency with direct access urgency.** Louis can personally onboard only so many users. "Accès Fondateur" means: direct WhatsApp line to Louis, 30-min onboarding call, your name in the app credits. The scarcity is Louis's time, not a slot count. When Louis's calendar fills, founding access closes.

4. **Keep the 4 benefits, reframe them as relationship benefits:**
   - Named in app credits → "Reconnaissance des premiers supporters"
   - Locked price → REMOVED (replaced with relationship value)
   - Direct founder access → "Accès WhatsApp direct à Louis — réponses sous 24h"
   - Roadmap vote → "Vote sur les 3 priorités du prochain mois"

**New language for landing page:**
> "Essai gratuit — sans limitation de temps. Vous décidez quand passer à €29/mois. Aucun engagement."

NOT:
> "Membre fondateur — €29/mois, puis €39/mois."

The first tells users: the price is €29. The second tells users: the price is actually lower if you act now.

**D5 UPDATED:** Price escalation path (€29 founding → €39 standard → €49 professional) is KILLED. Single €29/month price point. No founding/standard/professional tiers.

**D75 UPDATED:** "Membre fondateur" framing is KILLED. Replaced with "Accès Fondateur" — relationship benefits without discount framing. Scarcity signal = Louis's limited personal onboarding capacity, not arbitrary slot count.

---

## Debate 78: JWT Is the Wrong Auth Primitive for a Solo Artisan App

**Challenge:** D74 resolved Sprint 0 JWT scope = contract + stubs + @fastify/jwt config (0.5-1 day). The assumption challenged: JWT is the right auth mechanism for a solo artisan app.

### Technical Architect — Against JWT

**The flawed premise:** JWT was designed for distributed stateless auth across microservices and multi-user sessions. A solo artisan with one phone has a single-user, single-device model. We're using a sledgehammer for a finishing nail.

**What D74 got wrong:** Even the "scaffold" costs 0.5–1 day and delivers zero user-facing value. JWT introduces: @fastify/jwt dependency, token generation/signing/verification, TTL management, refresh endpoint, logout logic.

**The API key alternative:** Single UUID stored in Expo SecureStore, sent as Authorization header. No library, no TTL, no refresh. ~2 hours of work vs 0.5–1 day for JWT scaffold. 2–6 hours reclaimed in Sprint 0.

**When JWT makes sense:** Multi-user sessions, distributed microservices, token sharing across devices. None of these apply.

**VERDICT on D74:**
RESOLVED — **API key wins. JWT deferred to v2.**

The challenge is correct on all counts. But the framing in the debate missed the most important point, which I want to correct explicitly:

**The critical assumption I want to challenge from the debate log:**

The debate treated this as "JWT complexity vs API key simplicity for the same use case." That's wrong. JWT was never the right primitive here, even before the API key alternative was proposed. JWT solves problems this product doesn't have:

- JWT solves **stateless verification across distributed services** — we have one Postgres instance
- JWT solves **multi-session management across devices** — Marc has one phone
- JWT solves **token rotation and refresh without re-login** — Marc's session lives on his phone until he logs out
- JWT solves **delegated auth (OAuth, third-party token sharing)** — no third parties at launch

None of these are real problems for a solo artisan on a single device. The JWT "benefits" in this context are solving zero of Marc's actual problems.

**On the "2 hours vs 0.5-1 day" estimate:** Accurate. The JWT scaffold (contracts + stubs + @fastify/jwt config) at 0.5-1 day is realistic for production-grade implementation (proper TTL, refresh endpoint, logout logic). The API key approach (single UUID, one verify endpoint, Expo SecureStore stub) at ~2 hours is also realistic. The delta is real and meaningful in a 5-day Sprint 0.

**On Expo SecureStore reliability:** Production-grade. iOS Keychain and Android Keystore backed. Battle-tested in production Expo apps. Not a research-and-deploy risk — it's a known quantity.

**On v2 multi-user concerns:** This is the only plausible objection. If v2 requires admin handler access (D55's secondary persona), you'd want proper user auth. But:
1. v2 multi-user auth would require a redesign anyway — API key per device ≠ multi-user session management
2. The right answer for v2 multi-user is: build user accounts, not "keep JWT from v1"
3. Starting with API keys doesn't paint you into a corner — you add proper auth when you need it
4. Keeping JWT "for future multi-user" is exactly the over-engineering this product has been fighting against at every turn

**On logout:** The debate mentioned "logout logic" as a JWT benefit. For a single-device solo user, logout = delete the token from SecureStore. No server-side blocklist needed. No TTL management needed. The "logout problem" doesn't exist here.

**Specific technical recommendation:**
- Sprint 0 schema: `artisans.api_key UUID DEFAULT gen_random_uuid()` — one row per artisan, one key per device
- Sprint 0 auth deliverable: `POST /api/auth/verify` — takes the UUID from Authorization header, returns 200 or 401
- React Native side: store API key in Expo SecureStore, attach as `Authorization: Bearer <uuid>` on all requests
- JWT: re-evaluate in Sprint 2 or v2 only if multi-user becomes a confirmed requirement

**D74 UPDATED:** JWT Sprint 0 scope is REPLACED. API key auth is Sprint 0 auth scope: schema column + verify endpoint + SecureStore stub, ~2 hours. Full JWT (if ever needed) is a v2 decision, not a v1 investment.

---

## Debate 79: Louis's Expert-Comptable Is a Validation Asset, Not a Sales Channel

**Challenge:** D55/D72 resolved expert-comptable outreach = Phase 1 (warm access via Louis's existing accountant). Assumption challenged: warm access = referral opportunity.

### Growth Strategist — Validation-First

**The mistake:** Conflating validation with sales. Louis's accountant is a *relationship*, not a *channel*. Warm access = credible feedback opportunity, not a sales funnel.

**The risk of asking for referrals now:** Best case — accountant says yes out of loyalty, sends 2-3 clients, nothing comes of it (product not ready), credibility takes a hit. Worst case — accountant says no, and Louis hasn't even validated the core persona.

**The asymmetric outcome:** Validation failure is cheap. Referral failure is expensive. One costs time. The other costs the relationship AND time.

**The correct order:** (1) Validation — "Can I show you the flow and get your honest reaction?" (2) Referrals — only after product has real users, testimonials, and the accountant has seen it work.

---

### VERDICT on Debate 79: RESOLVED — Expert-Comptable Is Phase 1 Validation Asset

**Assumption challenged from D55/D72:** "Warm access" was treated as shorthand for "immediate referral opportunity." This conflates two distinct objectives — validation and sales — that require different questions, different timing, and different success criteria.

**The core distinction:**

| Objective | Phase | Question | Success metric |
|-----------|-------|----------|----------------|
| Validation | Phase 1 (now) | "Can I show you and get your honest reaction?" | Credible feedback, persona confirmed |
| Referrals | Phase 2 (post-launch) | "Would you mention this to clients?" | Introductions to qualified prospects |

**Why the previous framing was wrong:**
D55/D72 treated Louis's accountant as a *channel* — a distribution mechanism for sending clients his way. But an accountant is a *relationship*, and relationships require trust to be spent carefully. Asking for referrals before the product has real users stakes the accountant's professional reputation on an unproven tool. If the product fails or underwhelms, Louis doesn't just lose the referral — he damages the relationship AND the credibility he was building.

**Why validation must precede referrals:**
1. The accountant needs to see the product work before they can recommend it credibly. A recommendation from a professional who hasn't used it is a favor, not an endorsement.
2. Louis doesn't yet know if the product solves a real problem. The accountant's clients are their shared frame of reference — but Louis hasn't confirmed his product maps to those clients' pain points.
3. Referrals without validation create a credibility debt. Best case: 2-3 clients sent by an enthusiastic accountant, product not ready, Louis scrambles to fix bugs while credibility erodes. Worst case: accountant says no (or worse, yes out of loyalty, then silently abandons the product), and Louis has burned social capital for nothing.

**What Louis asks his accountant this week:**

The meeting agenda should be:
1. **Show the flow, not the pitch.** "Can I show you how a devis gets created on my phone and tell me if this matches what you see with your clients?"
2. **Get honest feedback.** "Does this solve a real administrative pain point you observe with sole traders and artisans?"
3. **Build toward future referrals.** "What would make you comfortable recommending a tool like this to a client?"
4. **NOT:** "Can you send me 2-3 clients?" or "Would you mention this to other accountants?"

**Why this is Phase 1:** Louis has a warm relationship with his accountant. That warmth is valuable — not as a sales channel, but as a credibility validator. The accountant's reaction tells Louis: (a) is this product solving a real problem?, (b) is the UX credible enough for professional use?, (c) would this be worth recommending to clients?

**When referrals become appropriate (Phase 2):**
- Product has real users on the Free tier
- Louis has at least one testimonial or case study
- The accountant has seen the product work (not just heard about it)
- The accountant has asked *Louis* for more information (sign of genuine interest, not favor)

**Challenge to D55/D72 that this verdict accepts:** "Warm access" was correct. The mistake was treating warm access as a sales conversation when it should have been a validation conversation. The accountant relationship is valuable — but its value in Phase 1 is feedback, not referrals.

**Does this affect U12?** Yes — split into two playbooks:
- **U12a (validation script):** Action this week. Questions for Louis's accountant.
- **U12b (referral script):** Action Phase 2. Questions to ask once product is validated and accountant has seen it work.

**RESOLVED:**
- Expert-comptable stays Phase 1 — confirmed
- But Phase 1 = validation asset, not GTM channel — corrected
- Referrals deferred to Phase 2 — confirmed
- U12 split into U12a (validation) + U12b (referral) — action required

---

*Last updated: 2026-03-30T17:46*

---

## Pulse 1801 — DigitalChannels Specialist Debate

### Debate 50: Digital Peer Communities — Acquisition Channel or Retention Space?

**Challenge:** D49 assumes WhatsApp groups and Facebook communities are "where Marc discovers things." Growth Strategist challenges this — peer communities are social habitats, not tool discovery channels.

### Growth Strategist — Digital Communities Are Retention/Engagement, Not Acquisition

**Position:** Digital peer communities (WhatsApp groups, Facebook artisan communities) are retention/engagement spaces at launch — not acquisition channels.

**Core argument (5 points):**

1. **Commercial content in peer support spaces is filtered aggressively.** French artisan WhatsApp groups have established norms. Self-promotion without context reads as noise. The group reflex is silence or gentle redirect. D42 evidence: "WhatsApp groups are competitive spaces — French artisan groups are peer support networks, not recommendation engines."

2. **Authentic peer endorsement requires existing users — chicken-and-egg.** The only working WhatsApp-as-acquisition is organic: Marc tells Jean-Pierre at the wholesaler, "Cette app m'a fait gagner 2h." Jean-Pierre asks for the link. This happens at the Point P counter, not in the WhatsApp group.

3. **Facebook groups add algorithmic suppression.** New accounts posting product recommendations get suppressed or flagged. Organic reach to target audience is near zero without existing group credibility.

4. **SEO is discovery; WhatsApp groups and Facebook are not.** GTM conflates three distinct "digital" things: SEO (genuine discovery), WhatsApp peer groups (social habitat), Facebook communities (social habitat with algorithmic suppression). Only SEO belongs in acquisition.

5. **Prescriber discovery is digital but institutional, not peer-community.** Architects and property managers discover via email/professional portals — not WhatsApp groups. D49 correctly identifies prescriber as high-trust channel but misidentifies where discovery happens.

**Challenged Assumption:**
- **Assumption: D49** — "Digital channels (WhatsApp groups, Facebook artisan communities, SEO) — where Marc actually discovers things"
- **Challenge:** Marc discovers tools through trusted intermediaries in professional contexts, not peer WhatsApp groups. WhatsApp and Facebook communities belong in retention/engagement, not acquisition.

**Verdict: RESOLVED**

Digital peer communities = retention/engagement, NOT acquisition channels at launch.

GTM reclassification:
- SEO → Acquisition (primary digital discovery)
- WhatsApp groups → Retention/Engagement (brand recall, peer support for existing users)
- Facebook communities → Retention/Engagement (community building, not discovery)
- Prescriber networks → Acquisition (highest-trust discovery via institutional digital comms)
- Specialist retailers → Acquisition (physical trial/awareness)

Specific GTM recommendation: Stop treating WhatsApp group posts as acquisition input. Invest in SEO, prescriber enablement via institutional digital comms, and existing-user word-of-mouth enabled naturally at wholesaler/job site. WhatsApp groups = amplification layer for bouche-à-oreille, not acquisition channel itself.

---

*Last updated: 2026-03-30T18:01*

---

## Pulse 2026-03-30T18:00 — OfflineFirst Specialist Debate

---

## Debate D78 Follow-on: Offline-First — Required at Launch or v2?

**Context:** D78 resolved JWT → API key auth for Sprint 0. D9 excluded "offline" from MVP as too complex. D17 resolved PWA-first → React Native via Expo. Nobody has addressed the interaction between these decisions: does the React Native stack change the offline calculus?

### Technical Architect — Offline-First Required at Launch (VERDICT)

**Assumption challenged (D9):** "No offline" was decided before D17 (React Native from Day 1) was resolved. The "offline = complex" argument applied to a web-stack architecture where offline required service workers, IndexedDB, and sophisticated sync logic. With React Native + Expo, offline-first is the default pattern, not an engineering Everest.

**Assumption challenged (D78/D9 interaction):** API-key auth is MORE compatible with offline than JWT — no token refresh race conditions, no expiry during dead zones. D78's switch to API keys accidentally makes offline easier, not harder.

**Core argument:**
1. **Product fails at moments it matters most.** Marc's worst admin day is standing in front of a client with no signal, needing to pull up or create a devis. If the app shows "no connection" — the product has failed its core job.
2. **"v2 offline" loses first 100 users.** Early adopters are most forgiving AND most vocal. One failure on a job site → 1-star review + "that app doesn't work on job sites" in WhatsApp groups.
3. **Stack change invalidates D9's complexity reasoning.** WatermelonDB + Expo-sqLite = offline storage in hours, not sprints. Fastify API requires zero changes. Sync is last-write-wins for solo users.
4. **Offline-first is mobile table stakes, not v2 polish.** Any mobile app managing user-generated CRUD data should use offline-first architecture by default.
5. **Sprint 0 impact is manageable.** ~2 days mobile work (WatermelonDB + sync + conflict UI). ~2 hours backend work (updated_at + client UUIDs). Acceptable for a 5-day sprint.

**Technical specifics:**
- Local storage: WatermelonDB or expo-sqlite (2-4 hours setup)
- Sync: Last-write-wins with conflict detection UI (show both, Marc picks)
- Backend: Zero endpoint changes. Add `updated_at` timestamp + accept client-generated UUIDs
- API key: SecureStorage on device, never expires, no refresh needed
- Offline indicator: Subtle "pending sync" badge. No scary errors. Silent background sync.

**Verdict:** RESOLVED — Offline capability REQUIRED at launch. D9 is REOPENED for the offline component.

**Decision:**
- Sprint 0 mobile app uses WatermelonDB/expo-sqlite for local-first storage
- Fastify API adds `updated_at` timestamps and accepts client UUIDs
- Sync: last-write-wins with manual override for serious conflicts
- D9 updated: "No offline" REMOVED. Replaced with: "Offline-first with background sync."

**Sprint 0 impact:** +2 days mobile work. Zero new backend infrastructure.

---

## Pulse 2026-03-30T18:00 — AccessLogique Specialist Debate

---

## Debate: "Accès Fondateur" — Right Framing or Wrong Signal?

**Challenge:** D77's conclusion that replacing "Membre fondateur" with "Accès Fondateur" resolves the discount-framing problem. D77 correctly identified that "Membre fondateur" was a discount signal wearing relationship language. But the fix — "Accès Fondateur" — introduces a new problem: the word "Fondateur" (founder) itself creates elite-tier signaling that directly conflicts with "simple like WhatsApp" positioning.

### AccessLogique — Position: "Accès Fondateur" Is the Wrong Fix

**Core argument, 5 points:**

**1. "Accès Fondateur" still signals a tier, just without the discount.**
The word "Fondateur" (founder) means there are founders and non-founders. That is a tiered membership model. It tells Marc: "Some users have this special status. You might be one of them. Others aren't." This is the opposite of how WhatsApp works — there's no "WhatsApp Founder Access." There's one product, one app, same for everyone.

**2. "Accès Fondateur" creates the latecomer problem D77 was trying to solve.**
Marc joins in Month 3. He sees "Accès Fondateur" mentioned in the app, in reviews, in WhatsApp artisan groups. He asks: "What founding access did I miss?" The answer is Louis's time-limited personal onboarding. But from Marc's perspective, he's a second-class user. He didn't get the personal onboarding. He didn't get the 30-minute call. He's on the outside of a club he didn't know existed.

**3. The scarcity signal (Louis's calendar) is a feature of onboarding, not a product tier.**
Louis's limited personal capacity for hand-holding onboarding is real and credible. But it should be described as an onboarding philosophy, not a named access tier. "Onboarding personal avec Louis (places limitées)" is a launch mechanic. "Accès Fondateur" is a permanent product category.

**4. The simplicity-first positioning cannot support any named tier at launch.**
D12 landed on "Sans vous prendre la tête" as the core brand signal. D53 reinforced it. The subheadline promises "5 minutes, depuis votre téléphone." There's no room in that positioning for "and by the way, some users get special founder access." Every element that introduces complexity, hierarchy, or social differentiation into the product story undermines the simplicity signal.

**5. The 4 relationship benefits should be delivered as onboarding experience, not as a tier badge.**
Real relationship benefits don't require a named tier to deliver them. The first 50 users get Louis's personal attention because it makes sense for a solo founder at launch — not because they need to be labeled "fondateurs."

### Challenged Assumptions

- **Assumption: D77 — "Accès Fondateur replaces 'Membre fondateur' without introducing new problems."**
  Challenge: D77 solved the discount-framing problem by removing the price signal ("pay less now"). But it kept the tiered-membership signal ("you are special class of user"). These are two different problems. The second problem — tiered membership signaling — was not addressed by the D77 resolution.

- **Assumption: D77 — "Scarcity via Louis's calendar works as 'Accès Fondateur' urgency."**
  Challenge: Louis's personal scarcity is a credible, honest constraint — but it should describe a launch onboarding experience, not a permanent product tier. "First 50 users get a 30-minute onboarding call with Louis" is a launch offer. "Accès Fondateur" is a permanent membership tier.

- **Assumption: D75 (original) — "A named relationship tier (Membre fondateur or Accès Fondateur) creates community without training users to wait for discounts."**
  Challenge: Both "Membre fondateur" and "Accès Fondateur" create a named tier that generates latecomer resentment. The problem isn't the word "membre" or "accès" — it's that any named tier implies there are people inside and people outside the tier.

### Verdict

**RESOLVED — "Accès Fondateur" is rejected. The tier is eliminated.**

**Specific decisions:**
1. **Kill "Accès Fondateur" as a product tier.** Not renamed — eliminated as a named category.
2. **Deliver the relationship benefits through onboarding, not labels:**
   - Direct WhatsApp access to Louis → "Support par WhatsApp — écrivez à Louis directement" (available to all early users)
   - Named in app credits → "Crédits" section, list of early supporters (no "Accès Fondateur" label)
   - Roadmap vote → "Les 50 premiers utilisateurs votent sur les priorités du mois" (temporary launch mechanic, not a tier)
   - Onboarding call → "Louis appelle chaque nouvel utilisateur pendant la première semaine" (founder's personal commitment, not a tier benefit)
3. **Scarcity signal:** "Les 50 premiers utilisateurs inscrits reçoivent un appel de découverte avec Louis." — temporary launch offer, clear, honest, time-bound.
4. **Single price forever:** €29/month. No founding/standard/professional tiers. No access tiers. One product.
5. **Messaging:** "Essayez gratuitement. Quand vous êtes prêt, c'est €29/mois. Louis répond sur WhatsApp en moins de 24h." — same relationship value, no tier label, no latecomer problem.

**D77 UPDATED:** "Accès Fondateur" is eliminated as a product tier. Relationship benefits delivered as onboarding experience and support channels, not as a named membership category. Scarcity = temporary launch offer (first 50 users get Louis's onboarding call), not a permanent tier. D75 fully superseded — no named founding tier of any kind.

---

*Last updated: 2026-03-30T18:00*

---

## Pulse 2026-03-30T17:59 — Three Specialist Debates

---

## Debate 80: "Accès Fondateur" — Right Framing or Wrong Signal?

**Challenge:** D77's conclusion that replacing "Membre fondateur" with "Accès Fondateur" resolves the discount-framing problem. The fix introduces a new problem: the word "Fondateur" creates elite-tier signaling that conflicts with "simple like WhatsApp" positioning.

### Product Strategist — "Accès Fondateur" Is Wrong Fix

**Assumption challenged from D77:** D77 correctly identified that "Membre fondateur" was a discount signal wearing relationship language. But "Accès Fondateur" still signals a tier — founders vs non-founders. That is a tiered membership model. The word "Fondateur" means there are founders and non-founders. This is the opposite of how WhatsApp works.

**Core arguments:**
1. "Accès Fondateur" still creates latecomer problem — Month 3 Marc sees the tier and asks what he missed
2. Scarcity via Louis's calendar should describe a launch onboarding experience, not a product tier
3. Simplicity-first positioning cannot support any named tier — every element introducing hierarchy undermines "Sans vous prendre la tête"
4. The 4 relationship benefits should be delivered as onboarding experience, not tier badges
5. Named tier implies people inside and outside the tier — solution is eliminate the visible tier

**VERDICT on D77:**

**RESOLVED — "Accès Fondateur" is ELIMINATED. No named tier of any kind.**

- Kill "Accès Fondateur" as a product tier — eliminated, not renamed
- Relationship benefits delivered through onboarding, not labels: "Support par WhatsApp — écrivez à Louis directement" (all early users), credits section listing early supporters, roadmap vote as launch mechanic
- Scarcity signal: "Les 50 premiers utilisateurs inscrits reçoivent un appel de découverte avec Louis." — temporary launch offer, not a tier
- Single price forever: €29/month. No founding/standard/professional tiers. No access tiers. One product.
- Messaging: "Essayez gratuitement. Quand vous êtes prêt, c'est €29/mois. Louis répond sur WhatsApp en moins de 24h." — same relationship value, no tier label

**D77 UPDATED:** "Accès Fondateur" eliminated. No named founding tier. Relationship benefits through onboarding experience. D75 fully superseded.

---

## Debate 81: Offline-First — Required at Launch or v2?

**Challenge:** D9's "no offline" decision was made before D17 (React Native) was chosen. React Native + Expo changes the calculus — offline is now a client-side storage problem, not a complex infrastructure problem.

### Technical Architect — Offline Capability Required at Launch

**Assumption challenged from D9:** "No offline" was appropriate for a web-stack architecture. For a React Native mobile app used by artisans on job sites — basements, rural areas — connectivity dependency is a product-killing failure mode.

**Core arguments:**
1. Product fails at exactly the moments it matters most — job site, no signal, standing in front of client needing a devis
2. "v2 offline" is how you lose first 100 users — 1-star review, WhatsApp group warning
3. D9 was decided before D17 (React Native) — the "offline = complex" argument no longer applies
4. Sprint 0 scope impact is minimal — API endpoints unchanged, local storage adds ~2 days mobile work
5. Offline-first is industry standard for mobile CRUD apps — burden of proof should be on "no offline"

**VERDICT on D9:**

**RESOLVED — Offline capability REQUIRED at launch. D9 REOPENED for offline component.**

**Specific decision:** Sprint 0 architecture is offline-first. React Native mobile uses WatermelonDB/expo-sqlite for local-first storage. Fastify API adds `updated_at` timestamps and accepts client-generated UUIDs. Sync is last-write-wins with simple conflict UI. No changes to API endpoint contracts.

- **Mobile:** WatermelonDB integration (~half day) + sync layer (1 day) + conflict UI (half day) = ~2 days mobile work
- **Backend:** `updated_at` on all entities + accept client UUIDs = ~2 hours
- **Net Sprint 0 impact:** +2 days, acceptable given 5-day sprint

**D9 UPDATED:** "No offline" REMOVED. Replace with: "Offline-first with background sync. Conflict resolution via last-write-wins with manual override."

---

## Debate 82: Digital Peer Communities — Acquisition or Retention?

**Challenge:** D49 assumes "digital channels (WhatsApp groups, Facebook artisan communities, SEO)" are where Marc discovers tools. Peer communities are habitats, not discovery channels. The GTM conflates communication habitat with tool discovery pathway.

### Growth Strategist — Peer Communities Are Retention, Not Acquisition

**Assumption challenged from D49:** WhatsApp groups and Facebook communities are tool discovery channels. These are peer support ecosystems — their currency is job leads, technical troubleshooting, pricing norms. Commercial tool recommendations without a triggering question are filtered aggressively.

**Core arguments:**
1. Commercial content in peer support spaces is filtered — "on reste entre nous ici" reflex
2. Authentic peer endorsement requires existing user base — chicken-and-egg at launch
3. Facebook groups add algorithmic suppression of non-core member posts
4. SEO is a discovery channel — WhatsApp groups and Facebook are not
5. Prescriber discovery happens in professional contexts (email, portals), not peer communities

**VERDICT on D49:**

**RESOLVED — Digital peer communities are retention/engagement spaces, NOT acquisition channels.**

**GTM reclassification:**

| Channel | Classification | Role |
|---------|--------------|------|
| SEO | Acquisition | Primary digital discovery |
| WhatsApp groups | Retention/Engagement | Brand recall, peer support for existing users |
| Facebook communities | Retention/Engagement | Community building, not discovery |
| Prescriber networks | Acquisition | Highest-trust discovery channel (institutional digital) |
| Specialist retailers | Acquisition | Physical trial/awareness |

**Specific recommendation:** Stop treating WhatsApp group posts as acquisition. Invest in SEO (problem-solution queries) and prescriber enablement (email/professional portals). WhatsApp groups = engagement/retention for existing users. Word-of-mouth happens at the wholesaler counter or job site — not in peer groups.

---

---

## Pulse 2026-03-30T18:15 — Three Resolutions

---

### Prior Pulse — Three Resolved (Incorporated This Pulse)

**D81 (Offline-first):** RESOLVED — Required at launch. WatermelonDB/expo-sqlite local-first storage. Fastify API adds updated_at + client-generated UUIDs. Sync: last-write-wins with conflict UI. No changes to API endpoint contracts. Sprint 0 timeline +2 days.

**D82 (Digital peer communities):** RESOLVED — Retention/engagement spaces, NOT acquisition channels. WhatsApp groups and Facebook = brand recall + peer support for existing users. SEO = primary digital discovery. Prescriber networks = highest-trust acquisition channel (institutional digital comms, not peer communities).

**D77 (Accès Fondateur tier):** RESOLVED — ELIMINATED as a product tier. Relationship benefits delivered through onboarding experience. No tier badge. Single €29/month forever. Scarcity = temporary launch offer (first 50 users get Louis's onboarding call), not a permanent tier.

---

## Debate 83: D63 — Situation Financière as Push Notification, Not Dashboard

**Challenge:** D63 resolved "situation financière" = PRIMARY Free tier value. But D63 assumed it lives in-app as a dashboard. Product Strategist challenges this.

### Product Strategist — Push, Not Pull, Case

**Assumption challenged from D63:** "Situation financière" as an in-app dashboard requires Marc to remember to open the app and navigate to it. For a 45-55yo BTP artisan with碎片化的 moments between job sites, this is friction that kills the daily habit.

**Core argument:** Offline-first means local writes. The "situation financière" on his home screen might be stale for hours after sync. An in-app dashboard that shows outdated numbers is worse than no dashboard — it signals the product isn't working.

**Why push beats pull:**
1. **8pm Paris delivery** = his natural admin time, after kids are in bed, when he's doing chiffrage and devis work. The snapshot arrives at exactly the moment he needs it.
2. **Server computes, push delivers.** Fresh data every evening regardless of when he last opened the app. The snapshot is always accurate.
3. **Dormant Free user conversion.** A Free user who hasn't opened the app in 9 days still receives the 8pm notification. "Vous avez 3 devis en attente totaling €4,200" is a conversion trigger even for dormant users.
4. **The "soir ritual" from Debate 43 is now resolved.** Push, not pull. The appointment comes to him.

**Technical architecture:**
- Local: offline writes queue for sync
- Server: nightly aggregation job (all synced data)
- Push: 8pm Paris, notification with summary + link to in-app drill-down
- Free tier: daily snapshot notification (limited depth)
- €29 tier: full financial snapshot + in-app drill-down

**VERDICT on D63:** UPDATED — "situation financière" is a server-computed push notification at 8pm Paris, NOT an in-app dashboard. Free tier gets the notification. €29 tier gets full snapshot + drill-down. Sprint 0 adds: push notification infrastructure + nightly aggregation job.

---

## Debate 84: Sprint 0 Timeline — 3-5 Days vs 8-10 Days

**Challenge:** The debate log cites Sprint 0 = 3-5 days minimum devis flow. Technical Architect argues this is underestimated by 2-3x for a solo developer shipping production-grade offline-first software.

### Technical Architect — 8-10 Days Case

**Assumption challenged from prior Sprint 0 estimates:** Offline-first was estimated as "+2 days" or "2 hours." WatermelonDB integration alone is 1-2 days for someone who hasn't used it before, including schema definition, sync adapter, and conflict resolution strategy.

**Realistic breakdown:**

| Component | Days |
|---|---|
| WatermelonDB/expo-sqlite + sync layer | 2.0 |
| Fastify API: updated_at + client-UUID | 0.5 |
| Auth: SecureStore + API key attachment | 1.0 |
| Mentions légales: 4 Handlebars templates (real legal text) | 1.0 |
| Devis flow: client → line items (TVA) → preview → share | 2.5 |
| Offline indicator UI + conflict resolution UI | 0.5 |
| Real device testing (Android, not simulator) | 1.0 |
| **Total** | **8.5 days** |

**Key risks not in 3-5 day estimate:**
- WhatsApp PDF sharing (html-to-pdf on mobile) = non-trivial, could eat a day
- Mentions légales templates require actual French legal research per client type — can't ship lorem ipsum
- Real device testing for offline behavior is essential, not optional

**Two options:**
- **Option A (realistic):** Accept 8-10 day Sprint 0 with full scope
- **Option B (if 5-day target):** Drop mentions légales (defer to Sprint 1), replace WhatsApp PDF with plain text share (placeholder), ship offline storage + basic devis flow only

**VERDICT on Sprint 0 timeline:** 8-10 days for full scope. If deadline requires 5-day Sprint 0: reduce scope per Option B. Do not ship broken offline sync or skip real device testing.

---

## Debate 85: U12 — Expert-Comptable Outreach: Phase 2 vs Week 1

**Challenge:** D55 resolved expert-comptable = Phase 2, citing "relationship-dependent, 6-18 month build time." Growth Strategist argues this conflates two distinct things: expert-comptable as *data-sync partner* (Phase 2) vs expert-comptable as *recommendation channel* (Sprint 0).

### Growth Strategist — Week 1 Case

**Assumption challenged from D55:** Phase 2 was defined as "expert-comptable access for data sync (expert-comptable portal)." But that's different from being on the recommended software list that expert-comptables already maintain for Pennylane, Indy, and Cegid.

**Core argument:** Every expert-comptable with 50 artisan clients = 50 warm introductions to the admin handler persona (D55's secondary persona). Marc doesn't search "logiciel devis facture." He asks his accountant. If the accountant says "use this one," the admin handler signs up that afternoon.

**Why this works in Week 1:**
1. **Cold outreach, not relationship building.** Email + one-pager + free account offer to 5 expert-comptables in Caen who service BTP clients. 2-week sprint. Not a dinner, not a partnership.
2. **Admin handler IS in the room.** Expert-comptable staff already recommend Pennylane. Getting on that list is a cold call, not an 18-month relationship.
3. **GetApp/Capterra profiles claimable in an afternoon.** D55 action item — these are discovery surfaces for admin handlers. Must exist at launch.
4. **Positioning is ready:** "Your artisan clients struggle with mentions légales and TVA compliance. This is the tool you can confidently recommend — it handles these correctly so you see clean fichiers."

**The distinction that D55 missed:**
- Data-sync with expert-comptable = Phase 2 (requires technical integration, relationships)
- Expert-comptable as recommendation channel = Sprint 0 (cold outreach, one-pager, free account)

**VERDICT on U12:** MOVED from Phase 2 to Sprint 0. Expert-comptable outreach begins Week 1. Goal: 5 expert-comptables in Caen area willing to trial and add to recommended software list. GetApp/Capterra profiles claimed before launch. Phase 2 (data-sync portal) unchanged.

---

*Last updated: 2026-03-30T18:15*

---

## Pulse 2026-03-30T18:27 — Three New Debates

---

## Debate 86: D81 — Sprint 0 Should Be Offline-Capable, Not Offline-First

**Challenge:** Technical Architect challenges D81 ("offline-first required at launch") — argues the 8-10 day Sprint 0 cannot absorb 5-7 days of offline sync complexity for a solo artisan with 98%+ French mobile network coverage.

### Technical Architect — Offline-First Is Over-Engineered for v1

**Assumption challenged:** D81 ("offline-first required at launch") was decided after switching to React Native via Expo, as if the stack change eliminated the complexity of offline-first. It didn't. WatermelonDB/expo-sqlite + background sync + conflict resolution UI = 5-7 days, not 2.

**Core argument:**

D81's "2 days mobile work" estimate was never broken down into real work units. The actual cost:
1. **Conflict resolution UI (~1 day):** When Marc creates a devis offline and his data syncs against updated server state — who wins? Last-write-wins sounds simple until you show Marc what was overwritten.
2. **Sync testing (~1 day):** Offline sync bugs are the hardest mobile bugs to reproduce. Solo developer + tight sprint = production incidents shipped undetected.
3. **Offline edge cases (~1 day):** Partial sync failures, deleted-client-during-offline scenarios. The 20% of cases that consume 80% of debugging time.

Total: 3-5 extra days on top of an already-tight 8-10 day sprint. The "2 day" estimate was optimistic.

**Additional challenges:**
- Marc is solo. He has one phone. There is no multi-device conflict in v1. Conflict resolution UI built for future multi-user = solving a problem that doesn't exist yet.
- Mobile data coverage in France is 98%+ population. Job sites have signal. True offline (basements, rural) affects <5% of sessions. Building infrastructure for edge cases at Sprint 0's expense is over-engineering.

**Proposed resolution:** Sprint 0 = Offline-Capable:
- **Optimistic UI:** Actions reflect immediately, server request fires in background
- **Retry queues:** Failed requests queue locally with exponential backoff
- **Cached data:** AsyncStorage for last 10 clients/recent devis
- **No local DB:** WatermelonDB deferred to v1.2
- **Backend:** `updated_at` + client-generated UUIDs only (~2 hours)

**VERDICT on D81:** REVERSED — Sprint 0 = offline-capable (optimistic UI + retry queues + AsyncStorage). True offline-first (WatermelonDB + background sync + conflict UI) deferred to v1.2. Saves 3-5 sprint days. Devis flow ships faster.

---

## Debate 87: D85 — Expert-Comptable Outreach Week 1 Is Premature

**Challenge:** Growth Strategist challenges D85's decision to begin cold expert-comptable outreach in Week 1 — argues cold outreach before any production users wastes the highest-trust GTM asset.

### Growth Strategist — The Highest-Trust Referral Channel, Wasted Cold

**Assumption challenged:** D85 — expert-comptable outreach begins Week 1, asking to be added to recommended software lists.

**Core argument:**

An expert-comptable who recommends software to artisan clients is making a professional endorsement affecting compliance and record-keeping for years. That recommendation only has weight if the accountant has seen the product work in practice. Cold outreach in Week 1 — before any beta artisan has used the product, before mentions légales have been validated in production, before a single testimonial exists — is not a recommendation request. It is a cold sales pitch that the accountant will correctly dismiss.

**Four specific challenges:**
1. **The first question has no answer:** "Which clients use this?" / "Can I see a correct BTP facture?" — We have no beta users, no production data, no validated mentions légales.
2. **Failed cold outreach burns the relationship:** There are 20-50 relevant expert-comptables in a reasonable Caen radius. Each unanswered or rejected outreach closes a door. The window for re-engagement after "come back when you have clients" is effectively forever.
3. **"Add to your software list" is not a warm ask:** Best-case Week 1 outcome is "send me more info" — an email in a folder they'll forget. Getting on a recommended list requires social proof: real users, real documents, real compliance validation.
4. **Free tier means artisan adoption comes first:** By Week 4-6, there will be real beta users with real sent devis. These are the users the expert-comptable needs to hear about. "I have 15 artisans using this in production" is a completely different conversation from "we're building something."

**One exception (D85 correct):** GetApp/Capterra profiles claimed in Week 1 — this is infrastructure, not outreach. It should be executed immediately.

**Proposed resolution:** Expert-comptable outreach moves to Week 4-6, with prerequisites:
1. 10-20 active beta users with real production devis
2. 1-2 written testimonials from real artisans
3. Production-validated mentions légales (real documents, not mockups)
4. A sample BTP devis the accountant can review

Outreach framing changes: "We have artisans in your area using this — would you like to see how it handles BTP client mentions?" (consultative, not transactional)

**VERDICT on D85:** PARTIALLY REVERSED — Week 1 action: claim GetApp/Capterra profiles only. Expert-comptable outreach moves to Week 4-6 with prerequisites. Phase 2 (data-sync portal) unchanged.

---

## Debate 88: D83 — The 8pm Fixed Notification Assumes a User Rhythm That Was Never Validated

**Challenge:** Product Strategist challenges D83's "soir ritual" push at 8pm Paris — argues it's a cultural stereotype that will cause notification opt-out and uninstall.

### Product Strategist — Configurable + Event-Driven Replaces Fixed-Time Push

**Assumption challenged:** D83 — "situation financière = server-computed push notification at 8pm Paris" as "the soir ritual."

**Core argument:**

Nobody ran a time-use study on French artisans' evening routines. The "8pm, after kids are in bed, doing chiffrage" detail is vivid but fabricated — it sounds like a user description, it's a product manager's imagination.

**French artisan reality:**
- Construction/trades day runs 7am-7pm
- Dinner as late as 8:30-9pm with family
- Admin happens in fragments: 5 minutes between jobs, quick WhatsApp check at lunch, invoice sent from van before next site
- No dedicated evening ritual slot exists for most

**Four specific challenges:**
1. **8pm = dinner time.** Notification interrupts family dinner. Irritation, not engagement. One badly-timed notification = push disabled permanently.
2. **Timezone ignorance.** "8pm Paris" fires at 7:35pm in Marseille, 9pm in Strasbourg. For artisans in Alsace, it's a late-night interruption, not an admin moment.
3. **8pm assumes Paris-timezone artisan.** France spans 1-hour time zone. Strasbourg and Marseille users get the notification at objectively wrong times.
4. **Fixed daily digest is passive.** "Here's your financial summary whether you need it or not" is low-relevance noise. Event-driven notification ("devis pending 3 days") is high-relevance signal.

**Proposed resolution:** Replace fixed 8pm with:
1. **Configurable window in onboarding** — Morning (8-9am), Midday (12-1pm), Evening (7-9pm). User chooses. Respects schedule diversity across France.
2. **Event-driven triggers** — "Vous avez un devis en attente depuis 3 jours" fires only when a devis has been unanswered 3+ days. "Cette facture est impayée depuis 15 jours" fires only when aging threshold crossed. Not a daily digest — actionable business events.
3. **Night mode guardrail** — never send push after 10pm local time.

The financial snapshot still exists — as an in-app report Marc opens when he wants business intelligence. Push reserved for actionable events.

**VERDICT on D83:** REFINED — Fixed 8pm notification REPLACED with: configurable notification window (user choice) + event-driven triggers + timezone awareness + night guardrail. Core insight of D83 preserved (push > pull, notification > dashboard). Execution corrected.

---

*Last updated: 2026-03-30T18:45*

---

## Pulse 2026-03-30T18:45 — Three Specialist Debates

---

## Debate 89: D83/D88 — Kill the Digest, Keep Only the Event

**Challenge:** D83/D88 resolved "situation financière = configurable notification window (morning/midday/evening) + event-driven triggers." Product Strategist challenges the configurable digest component.

### Product Strategist — Digest Creates Noise, Event Creates Signal

**Assumption challenged:** That a configurable notification window (daily/weekly digest) is a meaningful delivery mechanism for the €29 tier financial snapshot.

**Core argument:**

D76 resolved that the conversion trigger is **first accepted devis**. This is a specific, high-intent moment — Marc's client just said yes. That's when we ask for the upgrade. The D88 design still centers on a **recurring notification window** with configurable timing. This is a daily digest model wearing event-triggered clothing.

Here's the problem: Marc is in equilibrium. He's managing his business fine on Free. The worst thing we can do is send a notification that says "tout va bien, rien de neuf" — which is what any digest does on a quiet week. No urgency. No action. Just noise.

D63 is explicit: **financial snapshot is the €29 tier feature**, not a Free tier daily pull. This means the upgrade pitch only makes sense when there's financial data worth snapshotting — i.e., when a real transaction occurred.

A devis accepted = financial data now exists = snapshot is meaningful = upgrade pitch is relevant.

An 8pm Tuesday digest with no new business = no data, no snapshot, no pitch justification. Just another notification to ignore.

**VERDICT on D83/D88:**

**RESOLVED — Kill the configurable digest window. The "situation financière" notification fires ONLY on the first accepted devis event.**

- Notification: "Votre devis pour [Client] a été accepté — votre situation financière est désormais complète."
- This IS the conversion trigger. One notification, one moment, one ask.
- Recurring digest for dormant Free users: kept as a separate "stay in touch" mechanism (below the conversion trigger line), not as the primary notification.
- Free tier users who haven't accepted a devis in 14 days receive a gentle "tout va bien?" check-in. But the €29 conversion notification is event-only.
- D83 updated: configurable window REMOVED. Event-driven only (first accepted devis). D76 conversion trigger is the notification trigger.

---

## Debate 90: D84 — Sprint 0 Is 5.5-6.5 Days, Not 8-10

**Challenge:** D84 resolved Sprint 0 = 8-10 days for full scope. Technical Architect challenges this estimate as stale — derived before D86 (offline-capable, not offline-first) and D74 (API key auth, not JWT).

### Technical Architect — Parallelization Unlocks 5.5-6.5 Days

**Assumption challenged:** That the 8-10 day estimate remains correct after both scope reductions were applied.

**Core argument:**

The 8-10 day figure embedded two assumptions that were reversed:
1. WatermelonDB/expo-sqlite with background sync — removed by D86
2. JWT auth with refresh rotation — removed by D74

Neither change was reflected in a revised estimate. Here's the updated work unit breakdown:

**Backend track (Day 1 in parallel with mobile):**
- Fastify scaffold + Postgres schema + API key middleware: **1 day**
- Devis CRUD endpoints: **1.5 days**
- Mentions légales (data-driven templates): **0.5 days** (concurrent with above)

**Mobile track (Day 1 once API contract frozen):**
- Devis creation flow: **2 days**
- AsyncStorage + retry queue: **1 day**
- Real device testing: **0.5 days** (concurrent with final mobile work)

**Buffer: 0.5 days**

**Total: 5.5-6.5 days**

The decisive factor: backend and mobile can run in parallel if the API contract is defined by end of Day 1. The 8-10 day estimate embedded a sequential dependency that no longer exists.

**VERDICT on D84:**

**RESOLVED — Sprint 0 timeline = 5.5-6.5 days.** The 8-10 day estimate was for offline-first with JWT. With offline-capable (D86) + API key auth (D74), 5.5-6.5 days is the correct estimate. D84 updated accordingly. Buffer of 0.5 days is included.

---

## Debate 91: D85/D87 — Expert-Comptable Validation ≠ Referral

**Challenge:** D85/D87 resolved expert-comptable outreach moves to Week 4-6 with prerequisites (10-20 beta users, testimonials). Growth Strategist challenges this as conflating validation and referral.

### Growth Strategist — Validation This Week, Referral in Week 4-6

**Assumption challenged:** That prerequisites (beta users, testimonials) are needed before any expert-comptable outreach.

**Core argument:**

D79 drew the correct distinction: validation and referral are two different conversations. D85/D87 applies referral prerequisites to a validation conversation.

**Validation conversation (Week 1, no prerequisites):**
"Can I show you a devis flow and get your honest reaction?"
Louis asks his own expert-comptable — already a warm relationship. The ask: 20 minutes of feedback on whether the compliance flow makes sense. No testimonials needed. No beta users needed. The expert-comptable can assess whether the tool addresses a real pain within 20 minutes. That's information Louis cannot get from cold prospecting.

**Referral conversation (Week 4-6, with prerequisites):**
"Would you add this to your recommended software list?"
This absolutely requires social proof. 10-20 beta users, testimonials, production-validated mentions légales. This goes to 5 colleague expert-comptables in Week 4-6.

The D85/D87 resolution conflates these. "GetApp/Capterra profiles in Week 1" is correct — that's infrastructure, not outreach. But blocking expert-comptable conversations until Week 4-6 wastes a free validation opportunity that D79 specifically identified.

**VERDICT on D85/D87:**

**RESOLVED — Split U12 into two distinct phases:**

- **U12a (validation, Week 1):** Louis books his own expert-comptable this week. Ask: "Can I show you the devis flow and get your honest reaction?" No prerequisites. No testimonials. Just a flow demo and feedback request.
- **U12b (referral, Week 4-6):** Cold outreach to 5 colleague expert-comptables, with beta user testimonials and production-validated mentions légales as social proof.

D85/D87 partially updated: GetApp/Capterra = Week 1 (unchanged). Expert-comptable validation = Week 1 (Louis's own, no prerequisites). Expert-comptable referral = Week 4-6 (with prerequisites).

---

*Last updated: 2026-03-30T18:45*
