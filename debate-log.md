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
