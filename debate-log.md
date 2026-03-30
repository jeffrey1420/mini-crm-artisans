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

*Last updated: 2026-03-30T12:01*
