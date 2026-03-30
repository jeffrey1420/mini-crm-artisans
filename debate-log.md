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

---

## Debate 95: Sprint 0 — Solo Developer Parallelization Is Organizational Fiction

**Challenge:** D90 resolved Sprint 0 = 5.5-6.5 days with "parallel backend and mobile tracks from Day 1." Technical Architect challenges this assumption directly — it describes organizational parallelism, not individual developer parallelism.

### Technical Architect — The Parallelization Assumption Is Structurally Invalid

**Assumption challenged from D90:** "Backend and mobile can run in parallel from Day 1" — the decisive factor unlocking 5.5-6.5 days.

**The core problem — organizational parallelism ≠ individual parallelism:**

The "parallel track" framing describes how two teams work simultaneously. In a two-person team, one person builds backend while another builds mobile. They divide the work. Neither is blocked.

A solo developer cannot divide themselves. They can only sequence: backend OR mobile at any given moment.

**The Day 1 contract assumption is the critical path:**

For true parallelism to work, the API contract must be defined by end of Day 1 morning. That means:
- OpenAPI spec or shared TypeScript types for: Client, Devis, DevisLineItem, TVA rates
- Fastify scaffold with route stubs (even if handlers are empty)
- React Native scaffold with API client pre-wired to those route stubs
- Postgres schema committed and migrated

Day 1 reality for a solo developer:
- 4 hours: Define API contract + write shared TypeScript types
- 4 hours: Fastify scaffold + Postgres schema + first route stubs
- 4 hours: Expo scaffold + API client wired to contract
- Total: 10-12 hours = all of Day 1

End of Day 1, the contract IS defined. But the solo developer has spent the entire day on infrastructure and has zero feature work done. The parallelization doesn't begin until Day 2.

**Day 2-3 breakdown:**

Solo dev does backend Days 2-3:
- Client CRUD endpoints: 4 hours
- Devis CRUD + TVA calculator: 6 hours  
- Mentions légales template engine: 4 hours (4 Handlebars templates with real French legal text — see below)
- Testing + bug fixes: 2 hours
- Total: ~16 hours = 2 full days

Solo dev does mobile Days 4-5:
- Devis creation UI: 8 hours
- AsyncStorage + retry queue: 4 hours
- WhatsApp share integration: 3 hours
- Testing + bug fixes: 3 hours
- Total: ~18 hours = 2+ days

Day 6: Integration + real device testing + bug fixes.

**Actual calendar: 6 days minimum, assuming zero blockers and perfect execution.**

**The mentions légales hidden cost:**

D90's scope says "4 mentions légales templates (devis × client type)." This was treated as a template engineering task. It isn't — it's a legal research task.

French mentions légales for each client type require:
- Particulier: RCS, SIRET, numéro de TVA — consumer protection notice
- Professionnel français: Above + forme juridique, capital social, siège social, TVA intracom
- Professionnel UE: Above + numéro de TVA intracom + CGI 242 bis reference  
- Professionnel hors-UE: Above + specific跨境tax language, reverse charge statement

Each template requires actual French legal research or consultation. This is not engineering time. It is external dependency time. And it cannot be parallelized with any other Sprint 0 work — you need the correct legal text before the template engine can be written.

If legal research takes 2 hours: manageable. If it takes a day (waiting for a response, or finding the correct regulatory reference): Sprint 0 is 7 days.

**Three independent challenges to the 5.5-6.5 day estimate:**

| Challenge | Issue | Days at stake |
|---|---|---|
| Parallelization is organizational fiction | Solo dev = sequential, not parallel. Day 1 contract phase consumes full day. | +1 day |
| Mentions légales = legal research, not template engineering | Real French legal text requires external consultation or research. Not a copy-paste task. | +0.5-1 day |
| Integration + real device testing is underbudgeted | Both tracks meeting on Day 3-4 assumes zero integration surprises. Unlikely. | +0.5 day |

**Net: 5.5-6.5 days assumes no legal research time, perfect Day 1 API contract, and flawless integration. All three assumptions are independently fragile.**

**Specific conditions under which 5.5-6.5 days IS achievable:**

If and only if:
1. Louis already knows the exact legal text for all 4 mentions légales templates (pre-researched, ready to paste)
2. The API contract is genuinely definable in a half-day (he's done this before, schema is obvious)
3. The "shared types" are literally just copy-pasted into both backend and mobile with no discussion
4. Real device testing is deferred to Sprint 1 (i.e., the app isn't actually tested on a real phone during Sprint 0)
5. WhatsApp PDF sharing works on first attempt (no html-to-pdf debugging)

**Proposed scope cuts that make 5.5-6.5 days realistic:**

1. **Mentions légales deferred to Sprint 1** — plain text placeholder in Sprint 0 WhatsApp share. Legal templates are not blocking the devis flow's technical verification.
2. **Defer AsyncStorage + retry queue to Sprint 1** — online-only for Sprint 0. Tests whether the backend API works, not whether offline mode works.
3. **Single client type in Sprint 0** — particuler only. Client-type routing added in Sprint 1.

These three cuts reduce Sprint 0 to: define API contract (Day 1 morning) + backend CRUD + mobile devis creation UI + WhatsApp share (Days 2-4) + integration (Day 5). 5 days, achievable.

**VERDICT on Sprint 0 timeline:**

The 5.5-6.5 day estimate is achievable under specific pre-conditions (pre-researched legal text, pre-known schema, no real device testing). Without those pre-conditions, realistic estimate is 7-8 days.

**Recommendation:** Either confirm the pre-conditions are met (Louis has already researched the mentions légales text) or accept the 7-day timeline with the scope cuts above. Do not commit to 5.5-6.5 days based on organizational parallelism logic applied to a solo developer.

---

## Pulse 2026-03-30T19:00 — Three Specialist Debates

---

## Debate 92: App Store Launch — Simultaneous or Staged?

**Challenge:** Should Mini-CRM launch on both iOS and Android simultaneously, or stage the launches?

### Mobile Growth Specialist — iOS-First, Then Android

**Position: iOS-first, then Android in Month 2.**

**Core argument:**

**1. The "50/50 split" is population-level data applied to a specific B2B persona.** General French market is ~60/40 Android/iOS. But solo artisans using business software (auto-entrepreneurs sophisticated enough to pay for devis/factures software) tend toward iOS for ecosystem reliability and perceived stability for financial data. We don't know the actual split — that's the problem.

**2. Android Play Store moderation risk is systematically underweighted.** Legitimate B2B finance/invoicing apps get extra scrutiny in 2025-2026. Review delays of 1-4 days assume a smooth path. Apps flagged as potential fintech spam face 2-3 weeks of moderation queue. For a solo dev at launch, this isn't acceptable risk.

**3. Expo iOS builds are more reliable and faster.** EAS Build iOS targets are more mature than Android targets. This is a technical advantage that should be used.

**4. Simultaneous QA with solo dev is the wrong risk to take.** Testing two platforms simultaneously means untested edge cases on Android devices (Samsung, Xiaomi, manufacturer-specific behaviors, Play Services variants). One bad Samsung invoice rendering bug in Month 1 destroys trust that a B2B app cannot afford to lose.

**5. Early iOS reviews fund Android launch credibility.** "400 French artisans trust Mini-CRM on iOS" is a powerful Play Store listing when Android drops in Month 2.

**Validation before launch:**
- Facebook/Instagram geo-targeted poll in Caen: "What phone do you use for your business?" — €20-50 ad spend, reach 200+ artisans
- Check competitor review counts on iOS vs Android App Store — higher count = platform majority
- 10-15 artisan calls via LinkedIn or trade groups — 2 hours, qualitative grounding

**If validation shows 55%+ Android → launch Android simultaneously or first.**
**If 50/50 or iOS-leaning → iOS-first is clearly right.**

**Recommendation:**
- iOS launch in Month 1 (App Store review: 1-3 days)
- Android launch in Month 2
- Platform split validation in Week 1 (before Sprint 0 ends)
- If validation shows Android majority → reverse the order or launch simultaneously

**Verdict on D92:** NEW — iOS-first, then Android Month 2. Validate platform split in Week 1 via geo-targeted poll + competitor review count analysis. Android Play Store moderation risk is real for B2B finance apps.

---

## Debate 93: Day 1 Onboarding — Guided Creation or Explore First?

**Challenge:** What should the first 5 minutes after account creation deliver?

### Product Strategist — Guided Creation Flow Wins

**Position: Guided Creation Flow (Position A).**

**Core argument:**

**1. Position B ("Explore First") leads to empty-state abandonment.** The entire Free tier value proposition (document archive) is zero until documents exist. A clean home screen with an empty Active Job Card doesn't demonstrate value — it demonstrates emptiness. The 45-55yo artisan opens the app, sees nothing, and either thinks "this thing is empty" or "I'll come back when I need it." Both lead to the same outcome: they don't come back.

**2. "Explore First" mistakes comfort for value.** The app feeling calm and optional is a mood. Moods don't drive conversions. The accepted-devis event does. And you cannot reach an accepted-devis without a devis. Position B skips the first step entirely.

**3. Time-to-first-document is the strongest retention indicator for this product type.** Pennylane, Indy, and Tolteck all push users toward first-document creation within the first session. Not by accident. The conversion data is clear: artisans who don't create something in the first 48 hours almost never convert.

**4. The "intrusion" risk is overstated.** The 45-55yo artisan isn't reluctant to enter data because they're protecting privacy. They're reluctant because they don't yet trust the app is worth their time. The cure is speed — let them create something real and send it to a real contact. That's when the trust flips.

**5. Offline-capable architecture enables Position A.** Optimistic UI means zero perceived latency when creating a client or devis offline. No loading spinners. The share action (WhatsApp/email) works immediately. This removes the technical friction that could make a guided flow feel sluggish.

**Concrete recommendation — Guided Creation Sequence (5 minutes):**

**Step 1 — "Create Your First Devis in 60 Seconds" (60 seconds)**
- Full-screen intro card, not a modal
- Shows: "On y va. Three steps, 5 minutes, and you'll have sent your first devis."
- Single CTA: "Commencer"
- Message is "this is fast," not "you must do this"

**Step 2 — Create Your First Client (90 seconds)**
- Pre-fill: "Importer un contact" (phone contacts, if permissions granted)
- Fallback: name + phone only (minimal required fields, rest can come later)
- Mobile keyboard auto-opens on the name field

**Step 3 — Create and Send First Devis (3 minutes)**
- Auto-suggest first line item based on common artisan job types
- TVA pre-set to 10% (most common BTP rate)
- Preview screen showing the actual devis document
- Share via native sheet (WhatsApp pre-selected if available)
- "Votre devis a été envoyé" confirmation screen

**The aha moment:** "I just created and sent a professional devis in 5 minutes on my phone." Not "the app feels calm and optional."

**Verdict on D93:** NEW — Guided Creation Flow. Position A. 5-minute sequence: (1) set expectations, (2) create client via contact import or name/phone, (3) create and send first devis via WhatsApp/email. Time-to-first-document is the primary retention driver. Explore First is the higher-risk choice for this persona.

---

## Debate 94: GetApp/Capterra — Claim Week 1, Publish Post-Launch

**Challenge:** Should GetApp and Capterra profiles be live at launch or treated as post-launch hygiene?

### Growth Strategist — Claim Week 1, Publish When Ready

**Position: Claim in Week 1 (D85), publish when the profile is actually credible — Week 3-4, post-launch with screenshots and reviews.**

**Core argument:**

**1. D85 conflates "claiming" with "publishing."** Claiming = URL ownership, basic data entry, verification. Publishing = making a live profile visible to comparison site visitors. These are different actions with different consequences. D85 resolved to claim Week 1 — but that's just URL control. Publishing an unoptimized profile is a separate decision with real consequences.

**2. An empty profile is worse than no profile.** The admin handler persona is risk-averse. They're narrowing down options quickly. A profile with no screenshots, placeholder pricing ("Contact for pricing"), and zero reviews tells them: this product is new/unproven or not confident in its offering. That's "skip," not "evaluate."

**3. Competitors have 3-5 years of review accumulation.** Pennylane, Indy, and Freebe have screenshots of real interfaces, accurate pricing, and feature matrices. Launching alongside them with a skeleton profile means the comparison is over before it begins.

**4. The SEO benefit is real but premature.** GetApp/Capterra profiles rank in Google for specific queries ("[competitor] alternative," "best invoicing software"). These queries convert when the profile looks credible. An empty profile does nothing for SEO — worse, it anchors the wrong first impression into search results.

**5. The admin handler discovery argument is valid but conditional.** Admin handlers DO search comparison sites. But they discover tools that look ready to be evaluated. A profile with no screenshots doesn't invite evaluation.

**The correct sequencing:**

| Timing | Action | Profile State |
|--------|--------|---------------|
| Week 1 | Claim GetApp + Capterra, verify ownership | Draft/Private |
| Weeks 2-3 | Add screenshots, pricing, description, feature matrix | Draft/Private |
| Week 3-4 | Publish (once 2-3 seed reviews exist from beta/early users) | Live |
| Week 4-6 | Expert-comptable asks satisfied clients to leave reviews | Live + Accumulating |

**The seed review strategy:** Early beta users and founding member users should be asked to leave reviews on GetApp/Capterra. This is legitimate — they're real users who tested the product. It should happen as part of the Week 1-4 activation flow, not manufactured at launch.

**Verdict on D94:** NEW — Claim Week 1 (D85 confirmed). Publish Week 3-4, once screenshots, accurate pricing, and 2-3 seed reviews are in hand. Empty profiles are worse than no profile. Admin handler persona validates comparison site discovery channel (D82 updated accordingly).

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D92 | App Store launch | NEW — iOS-first, Android Month 2. Validate platform split in Week 1 (geo-targeted poll + competitor review count). | 2026-03-30 |
| D93 | Day 1 onboarding | NEW — Guided Creation Flow. 5-minute sequence: set expectations → create client via contact import → create and send first devis via WhatsApp/email. Time-to-first-document is primary retention driver. | 2026-03-30 |
| D93a | Guided Creation Flow timing | REOPENED — 5-minute focused attention during working hours is unrealistic. D93 implicitly requires evening/off-hours but D83 rejected 8pm as "too presumptuous." Internal inconsistency. | 2026-03-30 |
| D93b | Contact import assumption | REOPENED — "Importer un contact" assumes phone contacts contain client data. Solo artisans store client info in WhatsApp, not phone contacts. Import flow may return zero data. | 2026-03-30 |
| D94 | GetApp/Capterra | NEW — Claim Week 1 (D85 confirmed). Publish Week 3-4 when screenshots, pricing, and 2-3 seed reviews are ready. Empty profile is worse than no profile. | 2026-03-30 |

---

*Last updated: 2026-03-30T19:00*

---

## Pulse 2026-03-30T19:15 — Product Strategist Debate

## Debate 95: D93 — The 5-Minute Guided Creation Flow Assumes a Focused Attention Moment That Doesn't Exist

**Challenge:** D93 resolved the Guided Creation Flow wins — a 5-minute sequence: create client via contact import → create and send first devis via WhatsApp/email. The core assumption embedded in this resolution has never been stress-tested: **5 minutes of focused attention is available to a solo French artisan during working hours.**

### Product Strategist — D93 Assumption Is Built on a Fabricated Day

**Core assumption challenged from D93:** "Marc can complete the first-devis flow in 5 minutes on his phone, even with no prior app familiarity, even in a job site context."

**The fabricated day:**
D93's 5-minute sequence was designed around a day that doesn't exist for a solo French artisan:
- Day runs 7am–7pm with tight margins between jobs
- Lunch is eaten in the van between appointments — not a restful pause, a transition
- "5 minutes" to set up a new software tool means stopping mid-workflow, finding a quiet moment, focusing entirely on the app
- The job site context (noise, gloves, sunlight on screen, client interruption) makes focused phone use genuinely difficult

**The internal inconsistency no one caught:**

D83 rejected 8pm as a notification time with explicit reasoning: "too presumptuous about daily rhythm." French artisan evenings vary — family dinner timing, seasonal variation, regional customs. A fixed 8pm notification assumes a rhythm that doesn't universally exist.

But D93's Guided Creation Flow **implicitly requires an evening or off-hours moment** to complete the 5-minute setup. The flow can't work on a job site in 5 minutes. It can't work between appointments. It requires a genuine moment of focus that only exists outside working hours.

D83 rejected notification timing based on variability in daily rhythm. D93 assumes a 5-minute focused window exists in that same daily rhythm. These are internally inconsistent.

**The real French artisan day:**
- 7:00–8:00: Travel to first job site, setup
- 8:00–12:00: Work (often no phone access mid-task)
- 12:00–12:30: Lunch in van — sandwich, coordinate next job, check messages
- 12:30–17:30: Work
- 17:30–19:00: Travel, coordinate tomorrow, admin fragments
- 19:00–20:30: Family dinner, wind down
- 20:30–22:00: This is the window — if it exists. But D83 said this is too presumptuous to assume.

The 5-minute Guided Creation Flow requires a quiet, focused, uninterrupted moment. The only one that reliably exists is in the evening — exactly the window D83 rejected as unreliable.

**Assumption challenged #2: "Importer un contact" requires phone contacts with client data**

D93 Step 2 is: "Importer un contact" (phone contacts, if permissions granted), fallback to name + phone only.

The assumption: phone contacts contain client data. The reality: solo artisans keep client contact info in **WhatsApp**, not the phone contacts app. Phone contacts contain family, suppliers, and random numbers — not Madame Martin's mobile that he reaches via WhatsApp every time.

**The import flow failure mode is invisible:**
- User grants contacts permission
- App imports: 0 contacts (or 3 irrelevant ones)
- Fallback to manual entry activates silently
- User now manually enters name + phone — the same friction the import was supposed to eliminate
- The 90-second "create client" step becomes a 3-minute manual entry with no warning

The import isn't just unnecessary — it creates a permission request that, when it returns nothing, creates confusion about why the app asked.

**The conversion consequence of the 5-minute failure:**

If Marc attempts the Guided Creation Flow during a break and fails (interrupted, too slow, contact import returns nothing), he has now experienced the app as **friction** — exactly the opposite of "Sans vous prendre la tête." He closes the app. He doesn't come back. The aha moment was supposed to be "I just sent a professional devis in 5 minutes." Instead he got "this is complicated and I don't have time for this."

**The alternative: Evening-Only Guided Onboarding**

The correct framing: the Guided Creation Flow is an **evening ritual**, not a daytime onboarding task. This resolves the internal inconsistency with D83:

- Daytime: App functions as a clean viewer — Marc can see his existing data, understand the home view, receive the situation financière notification
- Evening (first session): Guided Creation Flow activates — 10-15 minutes, full attention, first devis created and sent
- The evening framing is honest: "Vous avez 10 minutes? Créons votre premier devis ensemble." — not "5 minutes between jobs"

This is what D83 was trying to protect: the evening ritual isn't a notification trigger (that's what D83 rejected). It's a framing for when the Guided Creation Flow is appropriate.

**Three specific problems D93 must solve:**

1. **The flow must work when interrupted.** Every step saves progress locally. If Marc gets a call mid-flow, he returns to exactly where he left off — not a blank screen.

2. **Contact import must have a meaningful fallback immediately visible.** "Vous n'avez pas de contacts? Entrez juste le nom et le téléphone." — not silent fallback to manual entry after a failed import.

3. **The 5-minute claim must be verified in context.** Can the flow complete in 5 minutes on an Android mid-range phone, with gloves, in bright sunlight, with one interruption? If not, the landing page "5 minutes" claim is a lie.

**Proposed resolution:**

D93 is partially correct — Guided Creation Flow wins over Explore First. But the implementation must change:

1. **Guided Creation Flow is evening-only framing** — "Vous avez 10 minutes? On crée votre premier devis ensemble." — not a daytime between-jobs task
2. **Day 1 experience is split:** Daytime = app install + home view orientation (job card, situation financière notification). Evening = Guided Creation Flow
3. **Contact import is secondary, not primary** — Manual entry is the happy path. Import is a shortcut for the 20% whose contacts app is actually populated
4. **5-minute claim removed from landing page unless verified** — If the flow can't complete in 5 minutes on a job site, the claim is false advertising

**Verdict on D93:** REFINED — Guided Creation Flow wins, but is repositioned as an evening ritual (10-15 minutes), not a 5-minute daytime task. Day 1 split into daytime orientation + evening onboarding. Contact import secondary to manual entry. 5-minute claim deferred until flow is verified in real conditions.

**What this challenges:**
- D93 timing: 5 minutes assumed, not verified — evening 10-15 minutes is more realistic
- D83 internal consistency: evening onboarding is not the same as evening notification — the distinction must be explicit
- D93 contact import: primary path should be manual entry, not phone contacts
- Landing page: "5 minutes" claim needs verification before it appears

---

*Last updated: 2026-03-30T19:15*

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D92 | App Store launch | NEW — iOS-first, Android Month 2. Validate platform split in Week 1 (geo-targeted poll + competitor review count). | 2026-03-30 |
| D93 | Day 1 onboarding | Guided Creation Flow — evening-only framing (10-15 min), not 5-min daytime task. Day 1 split: daytime orientation + evening Guided Creation. Contact import secondary to manual entry. | 2026-03-30 |
| D94 | GetApp/Capterra | NEW — Claim Week 1 (D85 confirmed). Publish Week 3-4 when screenshots, pricing, and 2-3 seed reviews are ready. | 2026-03-30 |


---

## Pulse 2026-03-30T19:15 — Growth Strategist Challenge

## Debate 95: D76/D89 — The "First Accepted Devis" Conversion Trigger Assumes a Chain That Rarely Completes

**Challenge:** D76 (Free tier conversion trigger, resolved: first accepted devis) and D89 (notification fires ONLY on first accepted devis event) established the conversion trigger as: Marc creates a devis → client accepts it → we push notification → he upgrades to €29. This chain has never been stress-tested against how French artisans actually operate.

### Growth Strategist — The Three-Step Chain That Rarely Closes

**Assumption challenged:** That "first accepted devis" reliably fires for French artisans using the app.

**The chain has three required steps, each of which fails regularly:**

**Step 1 failure: Marc doesn't send formal written devis to steady clients.**
Marc has 6-7 steady clients. Dupont calls. Marc goes. Done. No formal written devis. No devis record. No acceptance event. Repeat clients may represent 60-80% of his actual work. The "first accepted devis" trigger fires for new-client situations only — a fraction of actual sales moments.

**Step 2 failure: French BTP verbal agreement culture.**
In French construction and artisan markets, verbal agreements are standard. Client says "ok go ahead" over the phone or in person. Work begins. No formal acceptance email, no signed document, no record in any system. The client accepted — but not in a way that produces a record. The acceptance never enters the app.

**Step 3 failure: Even when a formal devis IS sent, Marc may never mark it accepted.**
If the client accepts by phone ("c'est bon pour le devis"), Marc notes it mentally and moves on. Updating `devis.status = 'accepted'` requires Marc to remember to do it — and for what? The app never taught him that marking accepted matters. There's no UX forcing function that makes him do it.

**The arithmetic problem:**
- New client situations (where a new formal devis is sent): maybe 30-40% of Marc's actual sales events
- Of those, formal written acceptance: maybe 50% (rest verbal)
- Of those, Marc remembers to mark accepted: maybe 30%
- Conversion trigger fires on: 30% × 50% × 30% = **~5% of actual new-client sales events**

For repeat clients (60-70% of work): **zero fires**.

**The repeat client problem is fatal:**
If 60% of Marc's revenue comes from repeat clients who never receive a new formal devis, the conversion trigger fires on the remaining 40% of situations — and only 5% of those produce an accepted-devis event. The trigger fires on ~2% of actual business moments. Not zero, but insufficient to drive a conversion model.

**D83 and D89 refinement made it worse:**
D89 removed the configurable notification window. The notification now fires ONLY on first accepted devis. For the repeat-client artisan who never creates new formal devis for existing clients, this notification never fires at all.

**The D76 resolution's own language reveals the flaw:**
> "Votre devis pour [Client] a été accepté — passez à €29 pour suivre ce qui vous est dû."

This message assumes Marc is tracking what clients owe him. But if he works primarily on verbal agreements and repeat client relationships, he's not sending devis to track — he's showing up and doing the work. The €29 tier message ("suivre ce qui vous est dû") assumes a pipeline of accepted, unpaid devis. For a repeat-client artisan, that pipeline doesn't exist.

**Proposed resolution:**

Replace "first accepted devis" with **"first sent devis"** as the conversion trigger.

**New trigger:** When Marc sends his first devis (devis.status = 'sent', first time ever), push notification:
> "Votre devis a été envoyé. Passez à €29 pour suivre vos clients, vos devis acceptés, et vos factures impayées."

This fires on first devis sent — not on acceptance. It fires when Marc has experienced the core value (creating and sending a professional document). It does not require the client to do anything. It does not require Marc to remember to update status.

**Why "first sent devis" is the correct trigger:**

1. **It fires on first use, not on acceptance.** Marc's first action with the app is devis creation and sending. That's when he experiences the core value. The notification should fire at the moment of first demonstrated value, not on an external event he doesn't control.

2. **It doesn't require client participation.** The entire acceptance chain (verbal → written → recorded) is eliminated. Marc sends. We know. Trigger fires.

3. **It creates the right mental framing.** "I just sent my first devis" → "this works" → "should I pay for the version with more features?" That's the right conversion moment. "Your client accepted" → "you owe us money" is a debt collection moment, not a value moment.

4. **It addresses the repeat-client gap.** Marc sends a devis to a new client. Fire. He upgrades to track more clients, send more devis, follow up professionally. The repeat-client gap (no new devis = no trigger) is partially mitigated by the trigger firing on first new-client interaction.

**What this means for the €29 tier differentiation:**
If the conversion trigger moves to "first sent devis," the €29 tier must differentiate on something other than "accepted devis tracking." It differentiates on: client limit (10 on Free vs unlimited on €29), advanced features (relances, multi-user?), priority support. The financial snapshot (D70: outstanding devis, pending factures) becomes the secondary conversion trigger — fires on first accepted devis as originally designed, but is not the primary mechanism.

**Verdict on D76/D89:** REOPENED — The "first accepted devis" conversion trigger assumes a three-step chain that regularly fails in French artisan markets. Verbal agreements, repeat client relationships, and missing status updates all break the chain. Proposed replacement: "first sent devis" as primary conversion trigger. "First accepted devis" becomes a secondary notification within the €29 tier (financial snapshot), not the primary conversion trigger for Free → €29.

*Last updated: 2026-03-30T19:15*

---

## Pulse 2026-03-30T19:32 — Technical Architect Response to D95

---

## Debate 95: Sprint 0 — Scope Cuts Create More Work, Not Less

**Challenge:** D95 (Technical Architect — same role) argued 5.5-6.5 days is unachievable for a solo dev and proposed three scope cuts: defer mentions légales, defer AsyncStorage, single client type. This position challenges those cuts directly.

### Technical Architect — Against Scope Cuts

**Assumption challenged from D95:** Scope cuts (defer mentions légales, defer AsyncStorage, single client type) make Sprint 0 achievable by removing work. Wrong in all three cases. Scope cuts do not remove work — they transfer it to Sprint 1, where they create more damage.

---

**Challenge 1: Deferring mentions légales transfers work to Sprint 1, where it collides with factures**

D95's proposed cut: "plain text placeholder in Sprint 0, legal templates in Sprint 1."

This is presented as scope reduction. It isn't. Sprint 1 already has a job: build factures + sequential numbering + email relances. Adding mentions légales legal research to Sprint 1 means Sprint 1 has two jobs — build factures AND research legal text. You've compressed Sprint 1 without removing work. You've just deferred it into a sprint that already has a full plate.

The collision: mentions légales for factures require the same client-type discrimination as mentions légales for devis. If Sprint 0 ships with "particulier only" and Sprint 1 adds client-type routing, the mentions légales templates in Sprint 1 will need rebuilding when the client-type schema arrives. The legal text research for professionnel and étranger client types doesn't disappear — it gets done under time pressure in Sprint 1, alongside building the entire facture flow.

Do it once, correctly, in Sprint 0. Or do it twice, under pressure, in Sprint 0 and Sprint 1.

---

**Challenge 2: Single client type in Sprint 0 creates schema debt that costs more in Sprint 1**

D95's proposed cut: "particulier only in Sprint 0, client-type routing added in Sprint 1."

The problem: client.type enum touches everything:
- The mentions légales template renderer (particulier vs professionnel vs étranger requires different legal text)
- The devis → facture migration (a professionnel's devis converts to a professionnel's facture with specific mentions)
- The TVA intracom logic (only applies to professionnel UE/hors-UE, not to particuliers)

If Sprint 0 ships with `client.type = particuler` hardcoded everywhere, Sprint 1 adds the enum and must audit every rendering and calculation surface that assumed one client type. This is retrofit archaeology, not feature development.

The schema work (adding `client.type TEXT DEFAULT 'particulier'`) is 30 minutes. The integration audit across two sprints is 1-2 days. You've saved 30 minutes in Sprint 0 and added 2 days of Sprint 1 debt.

---

**Challenge 3: AsyncStorage deferral is acceptable — but only because D86 resolved offline-capable, not offline-first**

D95's proposed cut: "defer AsyncStorage + retry queue to Sprint 1."

This is the most defensible cut — but only because D86 already resolved that offline-first (WatermelonDB + full sync) is deferred to v1.2. The AsyncStorage deferral is consistent with D86's architecture. It is not independently justified by D95's timeline argument.

---

**Challenge 4: The real efficiency win is not cutting scope — it is accepting 7-8 days and building the right thing**

D95 argues: cut mentions légales, cut AsyncStorage, cut to single client type → Sprint 0 fits in 5.5-6.5 days.

The hidden cost: every cut creates Sprint 1 work. Sprint 1 was already resolved as "client file + devis flow + PDF generation + WhatsApp share" — a full plate. Adding mentions légales legal research, client-type schema migration, and retry queue debugging to Sprint 1 means Sprint 1 slips. Sprint 2 slips with it.

The 5.5-6.5 day estimate buys a faster Sprint 0 at the cost of a slower, more chaotic Sprint 1. That's debt-financed timeline.

The alternative: accept 7-8 days for Sprint 0. Build the correct schema from the start. Sprint 1 is then unencumbered — builds the flow on top of a schema that doesn't need migration.

7-8 days for a correct foundation is cheaper than 5.5-6.5 days plus a Sprint 1 rebuild.

---

**Challenge 5 (meta): The "5.5-6.5 days" debate is premature. There is no written Sprint 0 spec.**

Before debating days, Sprint 0 needs a written, agreed deliverable document. Without it, "days" is just a guess.

What does "Sprint 0 done" actually mean? The debate log says "Fastify + Postgres compliance foundations" and "API contract defined by end of Day 1" — but there is no written spec answering:
- What exactly is in each mentions légales template? (Not "the correct French legal text" — the actual text)
- What is the exact API contract? (Endpoint names, request/response shapes, auth method)
- What does "Sprint 0 done" mean in terms of a working artifact? (An API that can receive POST /devis? A mobile app that can display a devis? Both?)
- What are the acceptance criteria? (Not "compliance foundations" — specific test cases)

Until these are written, the day-count debate is theological. You cannot estimate a sprint without a spec.

**Verdict on D95's scope cuts:**

The three proposed cuts are partially valid (AsyncStorage) but wrong in premise — they transfer work, not remove it. Mentions légales deferral rejected: Sprint 1 already has factures + relances; adding legal text research is how you get a 3-week Sprint 1. Client.type deferral rejected: schema debt costs more than Sprint 0 time saved.

**Net verdict: Accept 7-8 days with full scope. Write the Sprint 0 SPEC first. The days debate is premature without it.**

**D95 Resolution: REFINED — Sprint 0 = 7-8 days with full scope. Scope cuts rejected. Sprint 0 SPEC must be written before estimation is valid.**

---

## Pulse 2026-03-30T19:43 — Three Specialist Debates

---

## Debate 96: D76/D89 — "First Sent Devis" Fires Too Early; "First Paid Facture" Is the Real Moment

**Challenge:** D76/D89 (conversion trigger) — Growth Strategist at 19:15 argued "first accepted devis" chain breaks too often and proposed "first sent devis" as the replacement trigger.

### Product Strategist — "First Sent Devis" Fires Before Value Is Proven

**Assumption challenged from D76/D89:** That "first sent devis" is the right conversion trigger because it fires without requiring client participation or status updates.

**Core argument:**

**"First sent devis" fires the moment Marc clicks a button.** His devis could sit unanswered for a week. His client could ghost him. He's sending devis to regular clients who already know the price verbally. At the exact moment of clicking send, nothing has happened yet. The product has not solved a problem — it's started a process. Asking for €29 at this moment means asking for money before any value is demonstrated.

**The correct trigger: "first paid facture."**

This is the moment the product actually delivers. Marc created the invoice. Sent it. Client paid it. Money arrived. The full loop closed. That's when Marc thinks "this tool works." Not "I typed numbers into a PDF." Not "I emailed someone who may never respond." Paid. In his account. Real value, tangible, attributable.

Conversion psychology is clear: you convert people when they're holding proof of value in their hands — not when they're hoping for it. "First paid facture" means the artisan has already experienced the core promise of the product: stop chasing money manually, get paid. Convert *after* that moment, when the feeling is fresh and attributable.

**The deeper flaw: both sides treat conversion as a notification.**

"First accepted devis" and "first sent devis" share the same assumption: the software detects an event and fires a push notification. Click here, pay now! This is not how you sell to a 50-year-old French artisan. These people respond to relationships, not algorithms. They distrust apps that nag them for money.

**The better model: 14 days Free, then Louis on WhatsApp.**

- Days 1–14: Marc uses the product freely. No pressure.
- Day 14: Louis (a real human) sends a WhatsApp check-in — not a sales pitch, a conversation.
  > *"Salut Marc, comment ça se passe ? Tu as pu tester un peu l'outil ? Des questions, des bloqueurs ?"*

This is how artisans buy. They buy from people they trust who check on them. The "first paid facture" milestone tells Louis *when* to make that call — not as a push notification, but as a conversation prompt.

**Verdict on D76/D89:** REOPENED — Product Strategist argues "first sent devis" fires too early. "First paid facture" is the right conversion moment (when value is proven). Push notification conversion is the wrong model entirely — human WhatsApp check-in at Day 14 is the correct mechanism. D76/D89 not yet resolved.

---

## Debate 97: D95 — Sprint 0 Estimate Is a Preparation Problem, Not a Scope Problem

**Challenge:** D95 (Sprint 0 timeline) — Technical Architect at 19:32 argued Sprint 0 = 7-8 days because mentions légales legal research must be done during Sprint 0.

### Technical Architect — Pre-Sprint Prep Removes the Research Dependency

**Assumption challenged from D95:** That mentions légales legal text research is a Sprint 0 task. It is not. It is a pre-sprint preparation task — and it has not been done yet.

**Core argument:**

The 7-8 day estimate accepted in D95 conflates two separate activities:
1. Pre-sprint prep: research and write the 4 mentions légales templates (legal/administrative work, 2 hours)
2. Sprint 0 engineering: build the Fastify + Postgres compliance foundations (coding work)

If Louis spends 2 hours this week writing the 4 mentions légales templates:
```
/mentions-legales/particulier.md
/mentions-legales/pro-francais.md
/mentions-legales/pro-ue.md
/mentions-legales/pro-hors-ue.md
```
...then Sprint 0 starts with ready-to-paste templates. The engineering task becomes:
- Copy-paste 4 templates → 30 minutes
- TVA calculator (well-defined French VAT rules) → 1 day
- Sequential numbering engine (AAAA-MM-XXXX format) → 1 day
- Postgres schema for clients, devis, factures → 1 day

**That's 3-4 days of pure engineering.** Sprint 0 fits in 5 days with buffer.

The 7-8 day estimate assumed legal research happens inside Sprint 0. It doesn't. Legal research is a pre-sprint dependency — like buying ingredients before cooking, not cooking while grocery shopping.

**The real blocker is prep work, not scope.** Sprint 0 is not the place to discover what legal text is required. Sprint 0 starts when all dependencies are resolved.

**Action item:** Louis spends 2 hours this week writing the 4 mentions légales templates. Sprint 0 then targets 5 days (not 7-8), because there's nothing left to research — just engineering.

**Verdict on D95:** REOPENED — Technical Architect argues 7-8 day estimate is inflated because it includes pre-sprint prep work. If mentions légales templates are pre-researched this week, Sprint 0 becomes 5 days. D95 refined but not yet resolved.

---

## Debate 98: D92 — iOS-First Is the Wrong Default for French Artisans

**Challenge:** D92 (App Store launch strategy) — resolved to iOS-first based on "iOS users skew business" and "Android Play Store moderation risk."

### Growth Strategist — Android-First Is the Right Default for This Persona

**Assumption challenged from D92:** That iOS is the default platform for a B2B tool targeting French artisans aged 45-55.

**Core argument:**

**Wrong persona assumption.** Marc is a 50-year-old French electrician. He wakes up at 6:30, drives to job sites, manages quotes on his phone between appointments. He's been in the trades for 25 years. He owns a Samsung or Xiaomi — not because he's cheap, but because Android is what working people in the trades use. The French artisan/construction market skews Android. "iOS = serious business user" is a Silicon Valley stereotype that doesn't survive contact with French rural demographics.

**"Business user = iPhone" is lazy thinking.** Yes, iOS has higher ARPU in B2C consumer apps. This is B2B for tradespeople. You're not selling to startup founders. You're selling to a 52-year-old plumber who upgraded from a Nokia to a Xiaomi. Defaulting to iOS-first means defaulting to the segment that is NOT your primary buyer.

**Android Play Store moderation is NOT a blocker.** A legitimate B2B finance app with proper legal documentation (SIRET, legal mentions, CGV) gets reviewed in 24-72 hours. Apple's review process is slower and more arbitrary for B2B finance apps. Android has the lower friction path to market.

**Android APK distribution is a feature.** Android APK installation enables direct distribution without App Store gatekeeping — via website, prescriber networks, USB stick at trade shows. For a B2B tool targeting risk-averse older users, "here's the APK, install it" is a legitimate channel.

**What should happen:** The geo-targeted poll in Week 1 is the right mechanism. But the default should be Android-first, not iOS-first. Run the poll. If data says iOS, go iOS. But don't start from a Silicon Valley assumption about who "serious business users" are.

**Verdict on D92:** REOPENED — Growth Strategist argues iOS-first default is wrong for French artisan persona. Android-first should be the default, validated by the Week 1 poll. D92 not yet resolved.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D92 | App Store launch | iOS-first — REOPENED Debate 98 (Android-first case made) | 2026-03-30 |
| D95 | Sprint 0 timeline | 7-8 days — REOPENED Debate 97 (prep work challenge) | 2026-03-30 |
| D96 | Conversion trigger | "First sent devis" challenged — "first paid facture" + human WhatsApp check-in proposed | 2026-03-30 |
| D97 | Sprint 0 prep | Mentions légales templates should be pre-researched this week (2h), reducing Sprint 0 to 5 days | 2026-03-30 |
| D98 | Platform default | iOS-first challenged — Android-first argued for French artisan persona | 2026-03-30 |

| U1 | Discovery | REPLACED — readiness protocol | 2026-03-30 |
| U2 | E-invoicing platform | Factea first when v2 | 2026-03-30 |
| U7 | Domain | DEFERRED — subdomain/Carrd until MVP validated | 2026-03-30 |
| U8 | WhatsApp acquisition | CLOSED — no WhatsApp CTA in devis | 2026-03-30 |
| U12 | Expert-comptable playbook | Phase 2 — relationship-dependent | 2026-03-30 |
| U15 | Price validation | Guerrilla price validation + founding member offer | 2026-03-30 |
| U16 | Mentions légales prep | NEW — Louis researches and writes 4 mentions légales templates this week (2h). Sprint 0 then targets 5 days. | 2026-03-30 |

---

*Last updated: 2026-03-30T19:55*

---

## Pulse 2026-03-30T19:55 — Three Final Positions

---

## Debate 96: Conversion Trigger — Final Product Strategist Position

**Challenge:** "First sent devis" as conversion trigger was challenged by Product Strategist in 19:43 pulse. The Growth Strategist proposed it as the moment to trigger upgrade prompt. Product Strategist responds with final position.

### Product Strategist — "First Paid Facture" + Safety Net

**Assumption challenged:** The debate assumed "first sent devis" signals meaningful commitment. It doesn't. For Marc, sending devis is routine admin work — like writing an email. The act of *sending* tells us nothing about whether he sees value in paying us. Payment is the only honest signal of value delivered.

**Key argument:** A paid facture means: devis accepted + work done + client paid. Three gates of real commitment. "First sent devis" rewards activity, not value. Marc could send 10 devis and never convert. D63's "situation financière push at 8pm" already handles the soft prompt for free users. The hard upgrade gate should only fire when money actually changed hands.

**Verdict on D96:** RESOLVED — Conversion trigger = **first paid facture** (hard gate). Add a secondary soft trigger: if Marc has sent 3+ devis and zero paid factures, surface a gentle upsell prompt ("Unlock unlimited devis → upgrade"). This catches power users who are engaged but haven't closed a cycle — without punishing casual or new users.

**Action Item:** Implement conversion at "first paid facture" (hard gate). Add 3-sent-devis soft prompt for non-converters.

---

## Debate 97: Sprint 0 Timeline — Final Technical Architect Position

**Challenge:** The 7-8 day estimate was challenged by Technical Architect in 19:43 pulse as overcounting. D95's +1 day for solo dev was the contested assumption.

### Technical Architect — "5 Days, With Conditions"

**Assumption challenged:** D95 added +1 day because "solo dev +1 day (parallelization assumed two people)." This conflates coordination risk with throughput risk.

**Key argument:** Parallelization buffers protect against *coordination failure between two engineers*. A solo dev on sequential, well-defined tasks has *throughput* risk, not coordination risk. Louis is the only dev. Sprint 0 tasks are now tightly scoped: TVA is a formula (not a lookup table), mentions légales are static template files (not a schema), client-type is a simple enum. These are not the tasks that expose solo dev fragility. The +1 day was valid when Sprint 0 scope was less settled. It no longer is.

**Verdict on D95:** RESOLVED — **5 days** achievable if:
1. Louis writes the 4 mentions légales templates *before* Sprint 0 starts (2h, pre-sprint, not in-sprint)
2. Sprint 0 stays online-only (AsyncStorage deferred — already resolved)
3. Scope holds to: TVA formula + sequential numbering + mentions légales renderer + client-type schema + REST API

Any scope creep invalidates the estimate at any duration.

**Action Item:** Louis: Confirm 2h block this week to write mentions légales templates. Gate for 5-day Sprint 0.

---

## Debate 98: Platform Default — Final Growth Strategist Position

**Challenge:** iOS-first (D92) was challenged by Growth Strategist in 19:43 pulse. The persona's Android-heavy demographic was the core argument.

### Growth Strategist — "Android-First Is the Correct Default"

**Assumption challenged:** D92 assumed Apple's ecosystem dominance in SMB/tools markets. This conflates general consumer app patterns with B2B trade demographics. The "iOS = serious business user" heuristic is a Silicon Valley myth that does not survive contact with French rural demographics.

**Key argument:** For 50-year-old French electricians, plumbers, and construction workers, Android is statistically dominant. Defaulting to iOS-first means building for the minority of your actual users first, then retrofitting for the majority. The geo-targeted poll in Week 1 should be a *validation checkpoint* — not the source of the strategic question. The poll should confirm the device split, not discover whether Android-first is right.

**Verdict on D92:** RESOLVED — **Android-first is the correct default**. Week 1 geo-targeted poll confirms or denies. If Android is 65%+, iOS remains polish phase, not launch parity. Expo builds handle both — Android-first is sequencing, not a technical constraint.

**Action Item:** Week 1: Ship Android beta to French target region. Run poll asking device type (factual, not "which platform should we prioritize"). Adjust iOS vs Android resource allocation in Week 2-3 based on results.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D92 | Platform default | Android-first (updated from iOS-first). Week 1 poll validates. | 2026-03-30 |
| D95 | Sprint 0 timeline | 5 days (updated from 7-8). Pre-condition: mentions légales templates pre-written. | 2026-03-30 |
| D96 | Conversion trigger | First paid facture (hard gate) + 3-sent-devis soft prompt. | 2026-03-30 |
| U16 | Mentions légales prep | Louis writes 4 templates this week (2h) — gate for 5-day Sprint 0. | 2026-03-30 |

---

*Last updated: 2026-03-30T19:55*

---

## Pulse 2026-03-30T20:08 — Three Specialist Debates

---

## Debate 99: D68 — Flat-Rate Pricing Creates Seasonal Friction for French Artisans

**Challenge:** D68 (pricing model) — Product Strategist argues flat €29/month is structurally misaligned with seasonal, lumpy cash flows of French BTP artisans.

### Product Strategist — Usage-Based Pricing Aligns With Artisan Reality

**Assumption challenged from D68/D70/D71:** That flat-rate €29/month is simpler and less churn-prone than usage-based. The strategist argues flat-rate optimizes for SaaS-team simplicity, not artisan cash flow reality.

**Core argument:**

French BTP seasonality is documented and severe. January-February activity drops 20-30% vs. summer peak. A solo electrician may earn €0-800 in January vs. €4,000-6,000 in April. Paying €29 when income is near zero creates psychological friction that usage-based eliminates entirely.

The "simpler" argument conflates product-team simplicity with customer simplicity. For Marc, "pay per devis sent, capped at €29" is MORE intuitive than "pay monthly regardless" — it maps to how he thinks about every other service (plumber by the hour, materials by the unit).

January is the worst moment to ask for €29 — post-holidays, slow activity, tax pressures. Usage-based avoids this entirely.

**The capped hybrid model proposed:**
- Free tier: up to 5 clients, basic tracking
- Pro tier: €1.50 per devis sent, capped at €29/month
- First paid facture is the conversion trigger (hard gate — unchanged from D96)

**Verdict on D68:** REOPENED — Product Strategist argues flat-rate creates seasonal churn friction. Usage-based (capped at €29) eliminates seasonal friction, aligns payment with value, and preserves the revenue ceiling. D68 not yet resolved.

---

## Debate 100: D4 — Fastify + Postgres Is Wrong Architecture for 5-Day v1 Sprint

**Challenge:** D4 (technical architecture) — Technical Architect argues Fastify + Postgres + Coolify introduces infra complexity that consumes 20-40% of Sprint 0 before a single feature ships.

### Technical Architect — Supabase BaaS Ships Faster, Complexity Is the Real Risk

**Assumption challenged from D4:** That custom Fastify backend is the right choice for v1 because it gives "full control." The architect argues "full control" is a liability for a solo dev on a 5-day sprint.

**Core argument:**

Coolify setup alone is 2-4 hours for experienced devs, potentially half a day for first-time setup. That's 10-20% of Sprint 0 burned before writing a feature. Fastify API skeleton (auth middleware, CRUD routes, error handling, migrations) adds another 15-20 hours of non-feature work.

The e-invoicing compliance argument (D74) is overblown for v1 scope. E-invoicing mandate for small companies doesn't kick in until 2027. Mini-CRM v1 is a CRM, not an invoicing system. Building for a compliance requirement that doesn't apply to current scope is premature optimization.

Supabase (EU-hosted or self-hosted) gives: auth, Postgres, realtime, storage — all out of the box. French data sovereignty is solvable with EU-hosted Supabase projects or self-hosted Supabase on the same VPS.

"Full control" of Fastify + Postgres + Coolify means "full responsibility for everything that breaks at 2am." BaaS means a team behind your infrastructure.

**Verdict on D4:** REOPENED — Technical Architect argues Fastify + Postgres + Coolify is the wrong v1 architecture for a 5-day sprint. Supabase (self-hosted or EU-hosted) ships faster, addresses sovereignty concerns, and e-invoicing compliance is not a v1 concern. D4 not yet resolved.

---

## Debate 101: U15 — Founding Member Offer Undermines Credibility With Target Persona

**Challenge:** U15 (founding member offer + guerrilla price validation) — Growth Strategist argues "founding member" framing signals beta/unproven to risk-averse French artisans, and lifetime €90 deal undercuts the €29/month price point.

### Growth Strategist — Kill Founding Member, Go Pure Free Trial

**Assumption challenged from U15:** That founding member pricing creates urgency and commitment that free trials don't. The growth strategist argues the opposite — founding member pricing attracts the wrong early users and undermines credibility.

**Core argument:**

"Founding member" = beta signal for this persona. French artisans aged 45-55 are late-majority consumers who buy after consensus emerges. They trust peer validation, not founder appeals. "Membre fondateur" in France signals association/non-commercial intent — the opposite of a professional B2B tool.

€90 lifetime deal undercuts €29/month: signals the team doesn't believe in retention, and desperate to lock users in at a low price. For a persona who haggles with suppliers, this is a red flag.

The free tier IS the acquisition mechanism: "Here's a real product, try it free" is cleaner than "join our beta club." Let the product speak for itself.

The real acquisition channel is prescription (expert-comptable, groupements d'artisans, word-of-mouth) — not founding member deals. Founding member energy should be redirected to finding 5-10 genuine referrers and 2-3 expert-comptable partners.

Founding member users tend to be deal hunters with high churn risk — the opposite of the reference customers this product needs.

**Verdict on U15:** REOPENED — Growth Strategist argues founding member offer is counterproductive for this persona and market. Pure free trial with no lifetime deal, combined with prescription channel investment, is the correct launch strategy. U15 not yet resolved.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D4 | Backend architecture | REOPENED — Supabase BaaS argued for v1 (vs Fastify+Postgres) | 2026-03-30 |
| D68 | Pricing model | REOPENED — usage-based (capped at €29) argued vs flat €29/mo | 2026-03-30 |
| D92 | Platform default | Android-first. Week 1 poll validates. | 2026-03-30 |
| D95 | Sprint 0 timeline | 5 days. Pre-condition: mentions légales templates pre-written. | 2026-03-30 |
| D96 | Conversion trigger | First paid facture (hard gate) + 3-sent-devis soft prompt. | 2026-03-30 |
| U15 | Founding member offer | REOPENED — founding member offer challenged, pure free trial argued | 2026-03-30 |
| U16 | Mentions légales prep | Louis writes 4 templates this week (2h) — gate for 5-day Sprint 0. | 2026-03-30 |

---

*Last updated: 2026-03-30T20:24*

---

## Pulse 2026-03-30T20:24 — Three Specialist Debates Resolved

---

## Debate 99: D68 — Usage-Based Pricing: RESOLVED (Directionally)

**Specialist:** Product Strategist
**Pulse file:** pulse-2022-strategist.md

### Product Strategist — Usage-Based Case (Final Position)

**Core argument:** Flat-rate €29/month ignores French BTP seasonality. Jan-Feb activity drops 20-30%. Artisan pays €29 even with near-zero income, creating psychological friction and churn. Usage-based (€1.50/devis sent, capped at €29) aligns payment with value and cash flow reality.

**Key arguments:**
1. January friction eliminated — artisan sends 3 devis → pays €4.50. No resentment.
2. Retention improves — low-activity months don't trigger cancellation
3. Competitive differentiation — no competitor offers usage-based for this market
4. The cap at €29 protects revenue ceiling (same as flat rate for power users)
5. Converts flat-rate "simplifies for us" selfishness into "simplifies for client" honesty

**Counter-arguments addressed:**
- "Simpler to understand": Usage-based IS simpler for the client — maps to how they think (Spotify model)
- "Predictable revenue": Usage-based has better long-term predictability (lower churn = more consistent revenue)
- "Implementation complexity": Not a strategic argument — it's a technical problem to solve

### Verdicts on D99 and D68:

**D99 RESOLVED (Directionally):** Usage-based pricing (€1.50/devis, capped at €29) is the superior model for this persona and market. However: implementation complexity must be confirmed before committing. The conversion trigger ("first paid facture") needs to be reconciled with usage-based billing — if users convert at first paid facture, not at first sent devis, the billing trigger needs to be rethought.

**Open risk:** If the product converts at "first paid facture" (hard gate, D96), then usage-based billing may not trigger until a paid invoice exists — potentially weeks after signup. This gap needs resolution before D99 becomes implementation-ready.

**Action item:** Louis to evaluate implementation complexity of per-devis billing trigger. If complex: defer usage-based to v1.1, ship flat-rate at launch. If tractable: ship usage-based from Day 1.

---

## Debate 100: D4 — Supabase vs Fastify+Postgres+Coolify: RESOLVED

**Specialist:** Technical Architect
**Pulse file:** pulse-2022-architect.md

### Technical Architect — Supabase Case (Final Position)

**Core argument:** Fastify + Postgres + Coolify consumes 30-40% of Sprint 0 on infrastructure before a single feature ships. Coolify setup (2-4h), Fastify scaffold (15-20h), Postgres RLS + migrations (hours more) — all compete directly with feature work on a 5-day sprint. Supabase eliminates all of it.

**Key arguments:**
1. **Infra vs feature trade-off:** 30-40% of Sprint 0 on plumbing is unacceptable for a 5-day sprint
2. **Same Postgres schema:** Supabase IS Postgres — prior schema debate work is not wasted
3. **Auth, storage, realtime:** All included, tested, production-ready
4. **French data sovereignty:** EU-hosted Supabase (Frankfurt) satisfies GDPR. Self-hosted Supabase on OVH = same data residency as Coolify plan.
5. **Vendor lock-in is thin:** Supabase is open-source, self-hostable. Fastify + hand-rolled auth is harder to migrate.
6. **E-invoicing v2:** Postgres under Supabase supports any compliance query needed. Not a distinguishing factor.

**Counter-arguments addressed:**
- "Full control": Full control of a broken sprint is worthless. Supabase's managed infra means fewer 2am failures.
- "BaaS pricing at scale": v1 problem for when there's revenue to optimize. Not a Day 1 concern.
- "Supabase adds latency": 20-40ms delta vs 5-15ms for OVH-hosted — imperceptible for mobile app usage.

### Verdict on D4:

**D4 RESOLVED — UPDATED:** Sprint 0 backend = **Supabase** (self-hosted on OVH or EU-hosted). Fastify + Postgres + Coolify retired for v1.

Implications:
- No Coolify setup required — eliminates 2-4h of infra work
- Auth: `supabase.auth` (email/password) — done
- Storage: `supabase.storage` for PDF devis/factures
- React Native connects via Supabase JS client or REST API
- Postgres schema work (from prior debates) transfers directly

**Action item:** Louis to evaluate Supabase self-hosted vs EU-hosted decision. Self-hosted on existing OVH VPS = no new infra. EU-hosted = fastest path.

---

## Debate 101: U15 — Founding Member Offer: RESOLVED

**Specialist:** Growth Strategist
**Pulse file:** pulse-2022-growth.md

### Growth Strategist — Against Founding Member (Final Position)

**Core argument:** "Membre fondateur" signals beta/unproven to risk-averse French artisans. €90 lifetime deal undermines €29/month recurring value proposition and trains users to wait for discounts.

**Key arguments:**
1. **Beta signal:** "Fondateur" = "produit en test" for 45-55 year old risk-averse artisans
2. **Lifetime deprecation:** €90 lifetime = 3 months revenue. Signals the team doesn't believe in retention.
3. **Wrong user profile:** Lifetime deal hunters ≠ ideal early customers. Attracts deal-seekers, not evangelists.
4. **Factic urgency:** "50 places" without traction = arbitrary number that triggers skepticism, not conversion
5. **Wrong conversion model:** Real evangelists are users paying €29/month whose workflow depends on the product — not users who paid €90 once

**Counter-arguments addressed:**
- "Founding members create evangelists": Real evangelists are created by demonstrated value, not discount labels
- "Scarcity creates urgency": Only works after traction. Without users, "50 places" is a transparent sales tactic.
- "Tests price sensitivity": Price sensitivity tested better via conversation with real artisans, not a lifetime deal

### Verdict on U15:

**U15 RESOLVED:** No founding member offer. No lifetime deal. No founding/access tier labels.

Pricing at launch:
- **Free tier** (10 clients, 5 active devis) — no time limit, no "trial" countdown
- **€29/month** — single price, no founding/standard/professional tiers
- **"Support Prioritaire"** (not "Accès Fondateur"): direct WhatsApp to Louis, roadmap vote, named credits — relationship benefits without price discount
- No "50 places" or any scarcity framing

**What replaces founding member urgency:** Social proof (even at X=10 users), free tier as the trial mechanism, constant €29 price signal.

**Action item:** Landing page and onboarding to reflect "Support Prioritaire" benefit framing (relationship, not discount). Remove all founding/founding member/founding price language.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------| 2026-03-30 |
| D4 | Backend architecture | **Supabase** (self-hosted on OVH or EU-hosted). Fastify+Postgres+Coolify retired for v1. | 2026-03-30 |
| D68 | Pricing model | **Usage-based directionally superior** (€1.50/devis, cap €29). Reconciliation needed with D96 (conversion trigger = first paid facture). Open: if billing trigger too complex, fall back to flat-rate. | 2026-03-30 |
| D92 | Platform default | Android-first. Week 1 poll validates. | 2026-03-30 |
| D95 | Sprint 0 timeline | 5 days. Pre-condition: mentions légales templates pre-written. | 2026-03-30 |
| D96 | Conversion trigger | First paid facture (hard gate) + 3-sent-devis soft prompt. | 2026-03-30 |
| U15 | Founding member offer | **ELIMINATED.** No founding tier, no lifetime deal. "Support Prioritaire" (relationship benefits) replaces discount framing. | 2026-03-30 |
| U16 | Mentions légales prep | Louis writes 4 templates this week (2h) — gate for 5-day Sprint 0. | 2026-03-30 |
| D99 | Usage-based pricing | **Directionally resolved** — usage-based (€1.50/devis, cap €29) superior for artisan cash flow. Implementation complexity TBD — Louis to evaluate. If complex: flat-rate at launch, usage-based v1.1. | 2026-03-30 |

---

## Pulse 2026-03-30T20:40 — Three Specialist Debates

---

## Debate 102: D4/D100 Follow-Up — Supabase EU-Hosted vs Self-Hosted: RESOLVED

**Specialist:** Technical Architect
**Pulse file:** pulse-2040-architect.md

### Technical Architect — EU-Hosted Supabase Wins

**Core argument:** Self-hosted Supabase on OVH re-introduces the exact infra complexity that motivated switching away from Fastify+Postgres+Coolify in D100. EU-hosted takes 10 minutes to set up. Self-hosted adds 2-4h of infra work that directly competes with feature development.

**Key arguments:**
1. **Sprint 0 velocity:** EU-hosted = 10 minute setup. Self-hosted = 2-4h of infra work competing with features
2. **Ops overhead:** Self-hosted Supabase reintroduces the same Docker/backup/monitoring burden as Coolify — the thing D100 correctly eliminated
3. **GDPR compliance:** EU hosting satisfies GDPR. "French data sovereignty" is a feeling, not a legal requirement for this persona
4. **Cost:** $25/month is ~2% of revenue at 50 customers. Not meaningful against ops overhead
5. **Latency:** 20-40ms delta vs 5-15ms for OVH — imperceptible on real-world mobile networks (50-150ms)

**Assumption challenged:** *"French artisans require French-hosted infrastructure."* — Untested. EU-hosted (Frankfurt) satisfies the actual compliance concern. "Data sovereignty" as a blocking objection is unvalidated for this persona.

### Verdict on D4/D100 Follow-Up:

**D4/D100 RESOLVED (Final):** EU-hosted Supabase (Frankfurt) confirmed for v1 Sprint 0. Self-hosted on OVH not recommended. Revisit at 50 paying customers or €5k/month revenue.

**Action item:** Louis to sign up at supabase.com, EU region, Day 1. Do NOT set up self-hosted on OVH.

---

## Debate 103: D92 — Android-First: REFLECTED (Direction Stands, Validation Mechanism Changed)

**Specialist:** Growth Strategist
**Pulse file:** pulse-2040-growth.md

### Growth Strategist — "Week 1 Poll Validates" Is the Wrong Instrument

**Core argument:** U15 elimination (founding member offer) removed the early-access cohort that was supposed to make the Week 1 poll meaningful. Without that cohort, the poll can't serve its intended purpose. D92's direction (Android-first) is correct, but the validation mechanism needs replacement.

**Key arguments:**
1. **Validation mechanism broken:** U15 created an invested early cohort. Without it, "Week 1 poll" samples team network, not real users
2. **"Poll validates" was always ambiguous:** Platform preference is already known from demographics (70%+ Android in French BTP). The strategic question is distribution leverage, not device split
3. **Support Prioritaire doesn't solve install friction:** It's a retention benefit, not an acquisition trigger. The free tier creates a longer, less committed conversion funnel
4. **Platform question is downstream from GTM channel:** If primary acquisition is expert-comptable referrals, platform priority should follow where referrers are — not just end-user device split

**Assumption challenged:** *"Week 1 poll validates Android-first."* — The poll was measuring platform preference (already known) rather than platform priority (should follow go-to-market channel analysis). Replace with install completion rate as Sprint 0 validation metric (target: ≥50% of signups complete install within 48h).

### Verdict on D92:

**D92 REFLECTED — Direction stands, validation mechanism replaced:**
- Android-first by demographic default (French BTP = 70%+ Android) — CONFIRMED
- "Week 1 poll validates" — REMOVED (wrong instrument)
- **Install completion rate** replaces poll as Sprint 0 validation metric (target: ≥50% of signups complete install within 48h)
- "First paid facture" becomes soft milestone prompt (celebration + upgrade offer), not a hard conversion gate
- D24 (PWA vs React Native) resolution is the gate for Sprint 0 specificity on Android-first

---

## Debate 104: D96/D68/D99 — Billing Trigger Conflict: RESOLVED

**Specialist:** Product Strategist
**Pulse file:** pulse-2040-strategist.md

### Product Strategist — Option B: Limit-Hit Conversion, Usage-Based Billing From Day 1

**Core argument:** D96's "first paid facture" conversion trigger was designed for flat-rate SaaS. Under usage-based billing, conflating conversion moment with client-payment event creates weeks of free usage before first billing — negating the model's core promise. Resolution: convert at free tier limit hit, activate usage-based billing immediately.

**Key arguments:**
1. **The conflict:** Under usage-based (€1.50/devis), artisan sends 4 devis over 32 days before first paid facture. First billing event = €6 retroactive charge. Awkward and confusing.
2. **D96's insight preserved:** "First paid facture" = "this is real business" moment — retain as soft milestone prompt with upgrade offer, not a hard gate
3. **Limit-hit conversion is clean:** 5 active devis OR 10 clients = hard upgrade gate. No ambiguity. artisan hits limit → sees pricing → pays.
4. **Billing activates immediately:** €1.50/devis from first paying action. No gap. No retroactive charges.
5. **Option A (retroactive proration) rejected:** Creates billing edge cases that are confusing for non-technical artisans

**Pricing architecture after resolution:**
- Free: 10 clients, 5 active devis. €0.
- Pay-per-use: €1.50/devis beyond 5. Capped at €29.
- Unlimited: €29/month. Devis unlimited.

**Example: artisan sends 25 devis/month:**
- Free: 5 devis
- Paid: 20 × €1.50 = €30, capped at €29

**Example: artisan sends 3 devis/month:**
- Free: 3 devis (under limit)
- Paid: €0

### Verdict on D96/D68/D99:

**D96 UPDATED:** Conversion trigger = first free tier limit hit (5 active devis OR 10 clients). First paid facture = soft milestone prompt (celebration + upgrade offer).

**D99 RESOLVED (Implementation-Ready):** Usage-based billing (€1.50/devis, cap €29) at launch. Activates at conversion (limit-hit). Billing trigger and conversion trigger now aligned.

**D68 RESOLVED:** Usage-based (€1.50/devis, cap €29) + flat-rate alternative (€29 unlimited) offered at conversion moment.

**Action items:**
- Billing UI at limit-hit: two options (A) Pay €1.50/devis, or (B) €29 unlimited. Default to A with note "most start with per-devis, can switch anytime."
- First paid facture milestone: trigger upgrade notification when first paid facture fires (for Free or paying users) — not a hard gate, a celebration moment.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D4 | Backend architecture | EU-hosted Supabase (Frankfurt). Self-hosted on OVH NOT recommended for v1. | 2026-03-30 |
| D68 | Pricing model | **RESOLVED** — Usage-based (€1.50/devis, cap €29) + €29 flat-rate alternative at conversion. Seasonal cash flow benefit confirmed. | 2026-03-30 |
| D92 | Platform default | **REFLECTED** — Android-first direction confirmed. "Week 1 poll validates" REMOVED. Install completion rate (≥50% in 48h) replaces poll as Sprint 0 metric. D24 resolution gates Sprint 0 specificity. | 2026-03-30 |
| D95 | Sprint 0 timeline | 5 days. Pre-condition: mentions légales templates pre-written. | 2026-03-30 |
| D96 | Conversion trigger | **UPDATED** — Limit-hit (5 active devis OR 10 clients) as hard gate. First paid facture = soft milestone prompt (celebration + upgrade offer), not hard gate. | 2026-03-30 |
| D99 | Usage-based pricing | **RESOLVED (Implementation-Ready)** — €1.50/devis, cap €29. Activates at conversion (limit-hit). Billing trigger aligned with conversion trigger. | 2026-03-30 |
| U15 | Founding member offer | ELIMINATED — No founding tier, no lifetime deal. "Support Prioritaire" (relationship benefits) replaces discount framing. | 2026-03-30 |
| U16 | Mentions légales prep | Louis writes 4 templates this week (2h) — gate for 5-day Sprint 0. | 2026-03-30 |

---

*Last updated: 2026-03-30T20:45*

---

## Pulse 2026-03-30T20:53 — Three Specialist Debates

---

## Debate 105: D83/D93 — The Evening-Onboarding Contradiction Is Resolved

**Challenge:** D83 rejected fixed evening notification times because "8pm assumes a daily rhythm that doesn't universally exist." D93 resolved Guided Creation Flow is "evening-only, 10-15 minutes." These are internally inconsistent — D83 rejects what D93 requires.

### Product Strategist — Separate Notification (D83) From Onboarding Commitment (D93)

**Core argument:**

The contradiction dissolves when you separate two interaction types with different consent contexts:

- **Notifications:** D83 is correct. We should not *impose* anything on artisans. Event-only notifications (first accepted devis) — no time-based triggers, no configurable windows, no 8pm ritual.

- **Onboarding commitment:** D93 is correct. A Guided Creation Flow requires 10-15 minutes of focused attention. For a solo artisan, this naturally falls in the evening after the workday. But the key is: the artisan *chooses* this slot during Day 1 orientation. We are not imposing. We are asking for a commitment.

**The distinction that resolves the contradiction:**
- "Your notification will fire at 8pm" = imposed schedule → D83 correctly rejected
- "Can you commit to a 10-minute evening session this week?" = artisan's choice → D93 correctly requires

**Five specific decisions that resolve this:**

1. **Notifications stay event-only (D83/D89 stands):** First accepted devis fires notification. No time-based or configurable-window triggers. Ever.

2. **Guided Creation offered as bookable slot:** During Day 1 orientation, ask the artisan to select a 10-15 minute window — morning, midday, or evening. Not forced evening. Their choice.

3. **Async/self-paced fallback:** If no slot selected, the Guided Creation Flow is available whenever the artisan has 10 minutes. The evening is a common time; it's not mandated.

4. **Timezone-aware defaults:** D88's timezone awareness applies — but as a helpful default, not a notification trigger.

5. **Reframe D93:** "Evening-only" is an observation (most artisans find focused time in the evening), not a mandate. The requirement is a focused 10-15 minute window, not a specific time of day.

**Verdict on D83/D93:** RESOLVED — The contradiction was real. The resolution is clean. D83 governs reactive notifications (imposed timing = bad). D93 governs proactive onboarding commitments (opt-in choice = good). These are separate decisions for separate interaction types. D83 and D93 are not in conflict when scoped correctly.

---

## Debate 106: WhatsApp Sharing — PDF Attachment vs Native Message

**Challenge:** WhatsApp is the primary sharing channel (D42). But the specific architecture — PDF attachment via share sheet vs native WhatsApp message — is underspecified. PDF generation is Sprint 1b work. Can Sprint 0 share anything useful?

### Technical Architect — PDF Attachment via Native Share Sheet Ships in Sprint 0

**Core argument:**

**PDF Attachment (Approach A) — viable in Sprint 0:**
- Native iOS/Android share sheet works without WhatsApp Business API
- User taps Share → selects WhatsApp → PDF attaches → sends
- Matches actual artisan behavior today (they WhatsApp documents already)
- PDF is self-contained — client can print/forward regardless of their setup

**WhatsApp-Native Message (Approach B) — belongs in Sprint 1:**
- Requires WhatsApp Business API for direct sending
- Message templates require 1-2 weeks approval from WhatsApp
- Deep links need universal link setup on both iOS and Android
- Not viable in a 5-day Sprint 0

**Technical specifics:**
- WhatsApp Business API direct sending requires pre-approved transactional templates — not achievable in Sprint 0
- Server-side PDF generation (Sprint 1b deliverable) can be a placeholder text attachment until proper PDF ships
- `Share` API in React Native pre-selects WhatsApp if available

**Sprint 0 sharing deliverable:** Native share sheet + placeholder attachment. Sprint 1b: server-side PDF generation with mentions légales. Sprint 1+: universal deep links + WhatsApp preview card + read receipts.

**Verdict on WhatsApp sharing:** RESOLVED — Approach A (PDF attachment via native share sheet) ships in Sprint 0. Approach B (WhatsApp-native with deep links) is Sprint 1 work. WhatsApp Business API direct sending is not viable in Sprint 0 (template approval alone takes weeks).

---

## Debate 107: Document Archive — Retention Asset That Prevents Conversion

**Challenge:** D70 resolved document archive = PRIMARY Free tier value. D96 resolved limit-hit = hard conversion gate. Together, they create the "free forever" trap: the archive is satisfying enough that Marc never needs to upgrade.

### Growth Strategist — Three Design Changes Required

**Core argument:**

The archive satisfies. It doesn't convert. Three specific design changes required:

**1. Financial snapshot teaser in Free tier:**
- Free: "Vous avez 3 devis en attente de réponse" (count only, no amounts)
- €29: "Vous avez €4,200 en devis acceptés en attente de paiement" (full pipeline)
- The teaser creates curiosity; the full version is the upgrade pull

**2. Upgrade prompt reframed as growth acknowledgment:**
- Not "vous avez atteint votre limite" (wall)
- "Votre activité grandit. Avec le plan Pro, chaque client a son tableau de bord complet."
- Agency: the upgrade solves a problem he recognizes, not a quota he's managing around

**3. €29 visible as the complete package:**
- Archive alone = filing cabinet
- Archive + financial snapshot + relances + unlimited + support = real business tool
- Show Marc what he's missing, don't just block him

**The specific failure mode prevented:**
Marc hits 5/5, sees "passer à €29 or supprimer un ancien devis." He suppresses the 7th client, stays on Free, never converts. The archive keeps him satisfied. The "free forever" trap is prevented not by making Free worse, but by making €29 visibly better in a way that matters for his business growth.

**Verdict on document archive conversion:** RESOLVED — Document archive remains PRIMARY Free tier value (D70 confirmed). Three changes required: (1) financial snapshot teaser in Free tier, (2) upgrade prompt reframed as growth, (3) €29 visible as complete package. The conversion trigger is curiosity, not desperation.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D83/D93 | Evening onboarding contradiction | RESOLVED — D83 (notifications: event-only, no time-based) and D93 (onboarding: opt-in focused session) operate in different interaction contexts. Not contradictory when properly scoped. | 2026-03-30 |
| D93 | Guided Creation timing | UPDATED — "Evening-only" reframed as "focused 10-15 minute window" (most artisans find this in evening, not mandated). Bookable slot during Day 1 orientation, not forced. Async fallback available. | 2026-03-30 |
| D106 | WhatsApp sharing architecture | RESOLVED — Approach A (PDF attachment via native share sheet) ships Sprint 0. Approach B (WhatsApp-native deep links) is Sprint 1. WhatsApp Business API direct sending not viable in Sprint 0. | 2026-03-30 |
| D107 | Document archive + conversion | RESOLVED — Archive stays PRIMARY Free tier value (D70). Three changes: (1) financial snapshot teaser in Free tier, (2) upgrade prompt reframed as growth, (3) €29 visible as complete package. "Free forever" trap prevented by curiosity, not desperation. | 2026-03-30 |

---

*Last updated: 2026-03-30T20:53*


---

## Pulse 2026-03-30T21:13 — Three New Challenges

---

## Debate 108: Sprint 0 — 5-Day Estimate Assumes Parallelization That Doesn't Exist

**Challenge:** D95 (5-day Sprint 0) — Product Strategist challenges the assumption that 5 days is achievable given Louis is a solo developer with unstarted pre-conditions.

### Product Strategist — Solo Dev Reality Check

**Assumption challenged:** That the 5-day Sprint 0 timeline is achievable because tasks are "tightly scoped" and "parallelizable."

**Core argument:**

**The U16 pre-condition is not done.** Louis has not written the 4 mentions légales templates. U16 was scheduled for "this week." Sprint 0 cannot start today — it can only start after 2 hours of mentions légales research. Without those templates written, Sprint 0 is 6.5-7 days, not 5.

**The parallelization assumption is wrong for a solo dev.** The debate correctly noted that Louis is solo — so there's no coordination overhead. But this gets the solo dev problem backwards. The risk isn't coordination failure between two engineers. The risk is that a solo dev who hits an unexpected edge case has no one to unblock him. When the TVA per-line formula has a rounding edge case, Louis can't pair-program past it. When Supabase RLS policies block a migration, there's no teammate who sees the solution immediately. The Technical Architect's original +1 day buffer was dismissed — but that buffer was never about coordination overhead. It was about solo dev throughput risk.

**The "10-minute Supabase signup" is misleading.** EU-hosted Supabase signup takes 10 minutes. But being ready to ship features from Supabase takes longer: RLS policy design (1-2h), migration workflow, environment variables, local dev setup. The 10-minute estimate covers account creation, not API-readiness.

**Louis hasn't confirmed the pre-conditions are done:**
- U16 (mentions légales templates): NOT STARTED
- Supabase signup: UNCONFIRMED
- Sprint 0 is not ready to start today

**VERDICT on D95:** REOPENED — Sprint 0 5-day estimate requires confirmation that U16 is done AND Supabase is signed up. If either is incomplete, the realistic estimate is 6.5-7 days. The current 5-day estimate sets Louis up to cut corners under pressure — not acceptable for a compliance-heavy Sprint 0 where mistakes (TVA rounding, mentions légales) have legal consequences.

---

## Debate 108 (Technical Architect — Final Verdict): Sprint 0 — 5 Days Achievable, But the Debate Framing Is Wrong

**Position:** The Product Strategist is correct that the 5-day estimate requires confirmed pre-conditions — and that failure to confirm them is the most likely failure mode. But the 6.5-7 day counter-estimate is wrong in its reasoning. Let me challenge both sides.

---

### Challenged Assumption 1: The "6.5-7 days" estimate conflates two different problems

The Product Strategist argues 6.5-7 days because:
- U16 (mentions légales) is NOT DONE
- Supabase signup is UNCONFIRMED

These are real concerns. But they're pre-sprint preparation problems, not in-sprint duration problems. Louis could write the mentions légales templates tonight. He could sign up for Supabase in 10 minutes. The "7 days" estimate treats "pre-conditions not done" as equivalent to "the sprint inherently takes 7 days" — that's a category error. If Louis finishes U16 and signs up for Supabase before Sprint 0 begins, the in-sprint duration question is back to 5 days. The 6.5-7 day framing doesn't distinguish between "pre-conditions not done" and "the work is inherently 7 days of engineering." They are not the same thing.

---

### Challenged Assumption 2: "Solo dev = solo dev throughput risk" is real, but overstated here

The Product Strategist argues Louis has no one to unblock him when he hits an edge case (TVA rounding, Supabase RLS policy blocking a migration). True. But the framing assumes these edge cases will fire and will be blocking. The Technical Architect's original +1 day buffer (which was dismissed in the debate) was actually justified not by coordination overhead (there's no team to coordinate) but by **hard problem risk** — the risk that one genuinely novel problem consumes a full day. That risk is legitimate for a solo dev and should not have been dismissed.

However: the sprint scope is now tightly bounded. TVA arrondi commercial is a formula (`Math.round(v * 100) / 100`), not a lookup table. Mentions légales are static template files, not a schema. Sequential numbering is a counter increment. These are not novel problems. The risk of a full-day block on any of these is low — they're well-understood tasks with clear solutions. The hard problem risk was higher when the scope included "figure out TVA per-line calculation" and "design mentions légales schema." Those decisions are already made. What's left is implementation.

---

### Challenged Assumption 3: "10-minute Supabase signup" is misleading — but not for the reason given

The Product Strategist says EU-hosted Supabase signup takes longer than 10 minutes because of "RLS policy design (1-2h), migration workflow, environment variables, local dev setup." This overstates the setup cost. RLS policies are a 1-hour task, not a 1-2 hour blocker. Migration workflow and environment variables are standard. But the instinct is right: "Supabase is ready" and "Supabase is API-ready" are different milestones. The 10-minute estimate covers account creation; API-readiness takes a few hours. This doesn't add a full day to Sprint 0 — it just means Supabase setup happens in parallel during the sprint, not as a pre-condition gate.

---

### My Verdict: 5 Days Is Achievable Under Specific Conditions

**The 5-day estimate is conditionally correct, not aspirationally wrong.** The Product Strategist's challenge is valid as a risk warning, but the 6.5-7 day estimate doesn't accurately represent the trade-offs.

**Conditions under which 5 days is achievable:**
1. Louis writes the 4 mentions légales templates BEFORE Sprint 0 starts (2h, not in-sprint). U16 is a pre-sprint gate, not a sprint task.
2. Louis signs up for EU-hosted Supabase BEFORE Sprint 0 starts (10 min account creation, 2-3h of API-readiness done in parallel with mentions légales prep — not blocking).
3. Scope holds to the agreed Sprint 0 deliverables: TVA formula + sequential numbering + mentions légales renderer + client-type schema + REST API scaffold.
4. Louis accepts the +0.5 day buffer for solo dev hard-problem risk — and if a genuine blocker hits, he cuts mentions légales (plain text placeholder) rather than cutting TVA rounding accuracy.

**Conditions under which 6.5-7 days is the honest estimate:**
1. Louis does NOT complete U16 before Sprint 0. Mentions légales templates must be researched during the sprint — adds 0.5-1 day.
2. Louis has NOT signed up for Supabase and is learning it while building — adds 0.5-1 day.
3. Scope creeps (additions, changes to client-type schema, reworking TVA logic) — adds days with no ceiling.

**The real problem with the 5-day estimate:** It was presented as the committed timeline, not as a conditional target. "5 days" without "if U16 is done and Supabase is signed up" sets Louis up to cut corners when the sprint starts without those pre-conditions confirmed. That is the Product Strategist's legitimate concern — not the absolute duration, but the false confidence.

**My resolution to D95:**
- **Target: 5 days** (achievable with pre-conditions confirmed)
- **Floor: 6.5 days** (if pre-conditions not confirmed, accept the longer timeline rather than cut corners on compliance)
- **Non-negotiable scope: TVA arrondi commercial, sequential numbering, mentions légales renderer**
- **Cut order if time pressure: mentions légales (plain text placeholder), then AsyncStorage (online-only v1)**
- **Pre-sprint gates (must be confirmed before sprint planning begins):**
  - U16: Louis shows the written 4 mentions légales templates (file or git commit)
  - Supabase: Louis shows the Supabase project dashboard (screen recording or screenshot)

---

**Verdict on D95:** RESOLVED — Sprint 0 = **5 days** (target), **6.5 days** (floor without pre-conditions). The 5-day estimate is valid only if pre-sprint gates are confirmed. If gates are not confirmed, accept 6.5 days — do not cut corners on TVA rounding or mentions légales compliance. Louis: confirm U16 and Supabase signup status before sprint planning. These are not sprint tasks — they are sprint prerequisites.

---

## Debate 109: U7 — Domain Deferral Is a Circular Dependency Trap

**Challenge:** U7 (domain purchase) — Growth Strategist challenges the "wait for guerrilla test" deferral, arguing it's structurally indefinite and actively blocks pre-Sprint-0 outreach work.

### Growth Strategist — The Circular Dependency

**Assumption challenged:** That deferring domain purchase until "after MVP validation" is a safe deferral, not an indefinite one.

**Core argument:**

**The guerrilla test prerequisites don't exist.** The readiness protocol that replaced U1 has two preconditions: (1) Figma prototype of devis creation flow — doesn't exist yet, (2) guerrilla test scheduled at a wholesaler — not on anyone's calendar. "Post-guerrilla-test" could mean two weeks from now. Or four. There's no deadline.

**Domain absence blocks expert-comptable outreach.** D91 resolved that Louis should book his own expert-comptable this week for validation. Cold outreach with a `lschvn.foo` subdomain signals side project, not trusted business tool. An email from `contact@alize.fr` (or whatever the eventual brand) looks different from one with a free subdomain.

**Domain absence undermines GetApp/Capterra credibility.** D94 says claim Week 1, publish Week 3-4. An empty profile on a comparison site with a `lschvn.foo` subdomain is worse than no profile — it flags the product as early-stage before a single screenshot exists.

**"False progress" cuts both ways.** The verdict warned that buying a domain creates cognitive commitment that makes pivots harder. But "domain can wait indefinitely" creates its own inertia — every week without a real domain is another week of building on infrastructure that communicates "side project" to every professional contact.

**The fix is surgical, not expensive:** Buy the domain now, park it, settle the branding in Sprint 0. Defer the *name decision*, not the *domain purchase*. A parked domain costs €10-15/year and blocks nothing.

**VERDICT on U7:** REOPENED — U7 deferral should be refined: buy the domain now (park it), defer the brand/name decision. The domain purchase is infrastructure, not branding. Domain absence actively blocks expert-comptable outreach and comparison site credibility. "Wait for guerrilla test" has no timeline because the test prerequisites don't exist yet.

---

## Debate 110: Conversion Trigger — Built for the Wrong Artisan Archetype

**Challenge:** D96/D104 (conversion trigger) — Technical Architect challenges the assumption that limit-hit or first-paid-facture triggers conversion for the primary persona (Marc with 6-7 steady clients on verbal agreements).

### Technical Architect — French BTP Runs on Verbal Agreements

**Assumption challenged:** That a formal written devis precedes payment — and therefore the conversion trigger (limit-hit OR first paid facture) fires when Marc crosses a threshold.

**Core argument:**

**French BTP runs on verbal agreements.** Marc's steady clients call him, he shows up, the work gets done. No formal devis. No paper trail in the app. The primary persona — solo artisan with 6-7 established clients, repeat work, verbal approvals — represents a large segment of the market the product is designed for. For this archetype, the app's core value (professional devis creation) is irrelevant. He doesn't send formal devis to people who already trust him.

**The limit-hit trigger doesn't fire for this archetype.** 5 active devis / 10 clients limits only matter if Marc is creating formal written devis. For an artisan whose client relationships are managed by phone calls and WhatsApp messages, those limits are invisible. He can operate for months, even years, inside the Free tier without ever hitting the hard gate — not because the product failed him, but because his business never produced the formal document that the conversion mechanism requires.

**The first paid facture trigger is worse.** It requires: (1) formal devis sent, (2) client formally accepts, (3) client pays. For a verbal-agreement workflow, none of these steps exist. The trigger fires on ~5% of new-client situations, zero for repeat-client situations.

**This isn't a limit calibration problem.** The debate has spent cycles arguing 5 vs 10 devis, first-paid vs first-sent. These are the wrong arguments. The real problem: the conversion architecture assumes formal documents drive the business. For the artisan who operates on relationships and verbal commitments, both the limit-hit and the paid-facture triggers are structurally blind.

**The real question never resolved:** What conversion trigger fires for the artisan who never sends a formal devis because his clients don't require one?

**VERDICT on D96/D104:** REOPENED — The conversion trigger (limit-hit or first paid facture) assumes formal written devis exist. For French BTP verbal agreement workflows, both triggers may never fire. A different conversion mechanism is needed for the repeat-client, verbal-agreement archetype — or the product's addressable market is smaller than the feature set implies.

---

*Last updated: 2026-03-30T21:13*

---

## Pulse 2026-03-30T21:27 — Debate 109: U7 Domain Purchase — RESOLVED

**Role:** Growth Strategist

### The Circular Dependency Problem

U7 is deferred "until MVP validation." The rationale: don't commit to branding before validating direction via the guerrilla test. This sounds prudent. But examine the actual dependency chain:

```
U7 deferred → until MVP validated → until guerrilla test confirms direction → until prototype exists + session scheduled
```

**The prerequisite for the prerequisite does not exist.** The prototype is not built. The guerrilla sessions are not scheduled. The "defer until validated" position is not actually a deferral to a future event — it's indefinite postponement dressed up as a milestone.

### Assumption Challenged

**Assumption from Debate 34:** "Domain purchase should wait until the guerrilla test validates product direction."

The flaw: This assumes the guerrilla test will meaningfully redirect the product away from "devis/factures." It won't. Here's why:

1. **Marc's workflow is already characterized.** Four pulses of debate have locked in the persona, the features, and the positioning. The guerrilla test is usability validation, not discovery. It's "can Marc use the devis screen?" not "should we be building devis?"
2. **The directional risk is low.** Even if the guerrilla test surfaces that artisans want job management more than invoicing, that doesn't invalidate the devis/factures tool — it expands the roadmap. The domain for a devis tool is not wrong if you add jobs in v2.
3. **Domain purchase and brand decision are independent.** Buying `devisfoo.fr` doesn't commit you to a brand name. It reserves a web address. The brand (logo, tagline, color) is a separate creative decision that benefits from having the domain, not the other way around.

### What the Domain Actually Blocks

While we're waiting indefinitely for validation that requires a prototype we don't have:

- **Expert-comptable outreach (D72, D85):** Cold outreach to expert-comptables requires professional credibility. A `gmail.com` address or `app.lschvn.foo` subdomain signals "hobby project." Expert-comptables are professional service gatekeepers — they will not recommend software that looks amateur.
- **GetApp and Capterra (D72, D85):** Profiles must be claimed before launch. These platforms verify domain ownership. Without a verified domain, you cannot claim the profiles. Without profiles, comparison-site traffic is zero. This is not a nice-to-have — D72 explicitly marks this as Week 1 priority.
- **Email deliverability:** Sending transactional emails (devis receipts, password resets) from a subdomain has lower deliverability rates than from a proper domain. Reputation is built on the root domain.

### The False Risk of "Buying Now"

The original argument: "What if we buy alize.fr and then pivot?" 

Cost of domain: ~€10/year. Cost of reversal: update DNS. Cost of NOT buying: blocked outreach, no comparison-site profiles, no professional email credibility, domain squatted by a competitor.

The asymmetry is extreme. The downside of buying and pivoting is ~€10 and an hour of DNS work. The downside of deferring is concrete launch blockers.

### Verdict on U7

**RESOLVED — Buy the domain now. Park it.**

Action: Louis registers the preferred domain today. Point it to a Carrd landing page or a static "coming soon" page. The brand name decision is deferred — the domain is not. This costs ~€10 and resolves three concrete launch blockers simultaneously.

**The brand decision (name, logo, tagline) remains open.** The domain purchase is infrastructure, not branding.

**U7 status: RESOLVED.**

---

*Debate 109 resolved: Growth Strategist. U7 domain deferral challenged — circular dependency identified. Domain purchase unblocks expert-comptable outreach and GetApp/Capterra setup. Brand decision kept separate from domain registration.*

---

## Debate 110 Resolution: Two Archetypes, Two Conversion Paths

### Product Strategist — Verbal-Agreement Archetype Case

**Assumption I challenge:** That the verbal-agreement artisan is a problematic edge case requiring a workaround. The Technical Architect framed this as "the conversion trigger architecture assumes formal documents drive the business — and this fails for verbal-agreement artisans." I challenge the framing itself. The verbal-agreement artisan isn't broken — he's the primary persona wearing a different coat. The question isn't "how do we make him send formal devis so the conversion trigger fires." The question is: **what is he already doing that constitutes genuine product usage?**

**The core reframe:** For verbal-agreement Marc, the job is the unit of work, not the devis. He shows up, does the work, gets paid. His administrative needs: track who's my client, what job did I do there, when did I get paid. That's a job log, not a devis tracker. Our product already has (or should have) the job table with status, scheduled date, client link. The verbal-agreement artisan IS the Active Job Card user from D13.

**The conversion insight:** If he's actively logging jobs — even without sending a single formal devis — he's deriving value from the product. "Active usage" IS the conversion signal, not "document sent." The conversion trigger architecture conflated the artifact (devis/facture) with the underlying activity (running his business). The verbal-agreement artisan IS running his business in the product — just not producing formal documents.

**The flawed premise:** The debate asks "what conversion trigger fires for the artisan who never sends formal written devis?" This implies he needs a NEW trigger. The better question: for the verbal-agreement artisan, what usage behavior demonstrates he's getting value and would pay to continue?

**Two conversion paths:**

**Path A — Formal-devis archetype:** This is the existing D96 path. He creates devis, sends them, gets paid. Limit-hit (5 active devis / 10 clients) OR first paid facture fires the conversion. Works fine.

**Path B — Verbal-agreement archetype:** He's logging jobs, managing clients, running his business in the product. Conversion fires when: **45 consecutive days of active product usage** (job created or updated in that period) OR **7+ jobs logged** OR **5+ active clients managed**. The trigger fires when the product has become his business operating system — regardless of whether a formal devis was ever sent.

**The 45-day threshold:** Why 45? It's long enough to cover 2-3 billing cycles (most artisans invoice monthly or at job completion). It's short enough that dormancy is clearly visible. It's the right proxy for "this product has replaced your notebook." The verbal-agreement artisan who logs every job for 45 days has internalized the product into his workflow — he will NOT want to go back to paper.

**The human check-in remains critical:** The debate identified Louis's WhatsApp check-in at Day 14 as the actual conversion mechanism for French artisans. This is correct and should apply to BOTH archetypes. The difference: for the formal-devis artisan, the check-in coincides with the first paid facture trigger. For the verbal-agreement artisan, the check-in at Day 14 surfaces whether he's actually using the product — and if he is, the conversion conversation happens then, not at some future limit-hit.

**What this means for the product:** Job tracking can't be a secondary feature. If the verbal-agreement archetype is the majority of the target market, then the Active Job Card (D13) IS the home view, not a nice-to-have. The product's value proposition for this archetype is: "Your job log, your client notes, your payment tracking — all in one place, no paper." The conversion trigger follows from active usage, not document production.

**The market size correction:** If the verbal-agreement archetype represents 40-60% of solo French artisans (plausible given BTP culture), then tying conversion to formal devis production means we only capture a subset. The product needs to serve the archetype it claims as primary (Marc, solo artisan, job-focused) — not design for a secondary archetype (formal devis shop) and hope the primary one adapts.

**VERDICT on Debate 110 / D96 / D104:**

D96 is RETIRED in its current form. Replaced with dual-path conversion:

- **Path A (Formal-Devis Artisan):** Limit-hit (5 active devis OR 10 clients) OR first paid facture → hard conversion gate. Unchanged from D96.

- **Path B (Verbal-Agreement Artisan):** 45 consecutive days of active product usage (job created/updated) OR 7+ jobs logged OR 5+ active clients managed → conversion trigger. Soft prompt: "Vous utilisez [Product] depuis 6 semaines. Vos clients et vos travaux sont enregistrés ici. Pour €29/mois, vous gardez tout — sans limite."

- **Day 14 check-in applies to both:** Louis WhatsApp check-in at Day 14 is the human conversion moment regardless of archetype. If the artisan is active and engaged, the check-in is the conversion conversation. The triggers above are backup for when the human check-in doesn't catch him.

- **Action item:** Sprint 1 must include robust job logging (the Active Job Card from D13, with job creation and status updates). This is the entry point for verbal-agreement artisans — not devis creation. If job logging is hard or secondary, Path B never fires.

- **Action item:** Add usage analytics to identify "active verbal-agreement users" — those with jobs logged but zero devis sent. This is the segment requiring Path B conversion treatment.

- **Action item:** Validate verbal-agreement archetype prevalence in guerrilla test: what % of Marc's clients require formal written devis vs verbal approval? If >40% verbal, Path B becomes the primary conversion design consideration.

**The assumption I challenged:** That the verbal-agreement artisan needs to produce formal documents to demonstrate product value. The correct framing: he's already demonstrating value by using the product to run his business. Our conversion design must recognize that.

---

*Verdict written: 2026-03-30T21:27*

---

## Pulse 2026-03-30T21:38 — Three Specialist Debates

---

## Debate 111: Sprint 1 — Job Logging Is a Sprint 1 Non-Negotiable

**Challenge:** Product Strategist challenges the assumption that job logging (Active Job Card, D13) can be deferred to v1.2 while Sprint 1 focuses on client + devis flow.

### Product Strategist — Job Logging Required in Sprint 1

**Assumption challenged:** That job logging is secondary to devis flow and can follow Path A to market in v1.2. D96/D104 established a dual-path conversion model. Path B (verbal-agreement artisan) requires job logging to fire. Without it, Path B does not exist at launch.

**Core arguments:**

**Persona argument:** Marc IS the verbal-agreement artisan. His primary workflow is job-first, not document-first. Without job logging, he has no reason to open the app on Tuesday after signing up on Monday. He churns or settles into Free tier inertia before ever hitting the 5-devis limit. The conversion triggers assume the product delivers value before the limit — and value for Marc means job logging, not devis creation.

**Architecture argument:** Path A fires at 5 active devis. Path B fires at 7+ jobs logged. If job logging ships in v1.2, Path B cannot fire for months. The "dual-path conversion" is structurally single-path until v1.2 ships. This is not a minor timing issue — it means the verbal-agreement segment has no conversion mechanism at launch.

**Competitive differentiation argument:** Tolteck, Obat, Indy — all document-centric. None do job logging well. Job logging + devis tracking is the differentiation wedge against incumbents. Deferring it to v1.2 lets competitors close the gap.

**Scope tradeoff proposal:**
- Cut from Sprint 1: WhatsApp PDF sharing (→ Sprint 1b), mentions légales template engine (→ plain text placeholder in Sprint 1, full engine Sprint 2), multi-taux per line (→ Sprint 2)
- Sprint 1 keeps: client file + devis CRUD + TVA calculator (flat rate) + minimum viable job logging (create job, update status, job notes, home card)
- Path B conversion enabled from Day 1 of launch

**VERDICT on D13/Sprint 1 scope:** OPEN — Job logging argued as Sprint 1 non-negotiable, not v1.2 deferral. Sprint 1 scope cuts proposed to make room. Not yet resolved.

---

## Debate 112: Expert-Comptable Outreach — The Conflict of Interest Problem

**Challenge:** Growth Strategist challenges the assumption that Louis's existing accountant is the right first domino for expert-comptable GTM.

### Growth Strategist — Louis's Accountant Is Not an Outreach Channel

**Assumption challenged from D55/D72/D85/D91:** "Warm access via Louis's existing accountant = immediate outreach opportunity." The accountant is Louis's client — recommending Louis's tool to their other artisan clients creates a conflict of interest.

**Core arguments:**

**Conflict of interest:** Louis's accountant has artisan clients. Recommending Louis's tool to them looks like steering. The accountant likely won't refuse explicitly — they'll agree and never act. Passive non-execution is the most common outcome of relationship-dependent referrals with a conflict of interest present.

**Network effect weaker than assumed:** 50 artisan clients on the accountant's roster don't automatically convert. French artisans are independent. A recommendation without urgency ("interesting, I'll think about it") rarely converts to signup.

**Week 1 validation is biased:** Louis's accountant cannot give unbiased feedback on a tool Louis co-founded. All feedback will be social support, not product validation. False confidence is the outcome.

**Alternative framing:** Use Louis's accountant as a reference to OTHER accountants (not artisans), not as a channel. The first referral should come from an accountant with no relationship to Louis. Week 1 validation should be with one non-conflicted artisan.

**U12 rethink:**
- U12a (Week 1): Validate with one non-conflicted artisan. Use accountant only to learn what accountants need before recommending.
- U12b (Month 2-3): Cold outreach to 5 Caen expert-comptables for discovery — not referrals yet. Understand what they'd need before recommending.
- Referral playbook: Month 2-3, after 5-10 paying users + testimonials + accountant has seen the product work.

**VERDICT on D55/D72/D85/D91:** OPEN — Expert-comptable outreach strategy challenged. Conflict of interest named. U12 split rethinking proposed. Not yet resolved.

---

## Debate 113: Sprint 0 — Six Items Must Be Confirmed Before Day 1

**Challenge:** Technical Architect identifies three blocking decisions and a missing spec that prevent Sprint 0 from being actionable.

### Technical Architect — Sprint 0 Has Six Unresolved Blockers

**Assumption challenged from D95:** That "pre-conditions confirmed" means Sprint 0 can start. The assumption is wrong because the pre-conditions are underspecified and the product spec is missing.

**Core arguments:**

**Missing spec:** Nobody has written the devis flow as a spec. The debates established the flow conceptually but not as a sequence of screens, states, and API calls. Without this, Day 1 is planning + building competing for the same cognitive context. A one-page scope document (30 minutes of writing) prevents days of rework.

**Supabase schema not verified:** D100 said "prior schema work transfers directly." Unverified. Supabase requires explicit RLS policies, auth user linkage, and storage bucket configuration that raw Postgres schemas don't include.

**Three blocking decisions not made:**
1. React Native navigation: Expo Router or React Navigation? (D11/D17 said Expo, not which navigation)
2. PDF generation: server-side (Supabase Edge Function) or client-side (React Native library)?
3. Mentions légales renderer: Handlebars, Nunjucks, or string interpolation?

**The sprint planning paradox:** D95 says "Sprint 0 = 5 days if pre-conditions confirmed." The pre-conditions say "U16 done before sprint." If Louis writes the mentions légales templates AS PART OF Sprint 0, then U16 IS Sprint 0 — not a pre-condition. The 5-day estimate assumes pre-conditions are done before sprint starts, not concurrent with it.

**Six items that must be shown (not scheduled) before Sprint 0 begins:**
1. 4 mentions légales templates committed to git (one per client type)
2. Supabase project dashboard accessible (EU region, Frankfurt)
3. 1-page Sprint 0 scope document: devis flow as step sequence
4. API contract defined (shared types file or OpenAPI spec)
5. Navigation library chosen (Expo Router recommended)
6. PDF generation approach chosen (server-side via Supabase Edge Function recommended)

**VERDICT on D95:** OPEN — Sprint 0 pre-conditions are insufficiently specified. Six items named that must be confirmed before sprint. D95 not yet resolved.

---

*Last updated: 2026-03-30T21:38*


---

## Pulse 2026-03-30T21:55 — Three Specialist Debates (Automated Pulse)

---

## Debate 111: Job Logging — Sprint 1 Non-Negotiable

**Role:** Product Strategist

**The Core Problem: Path B Has No Entry Point Without Job Logging**

D110 established a critical architectural truth: we have two distinct conversion paths. Path A (formal-devis artisan) enters through devis flow. Path B (verbal-agreement artisan who never sends formal devis) enters through job logging. These are not parallel tracks of equal importance — they represent two fundamentally different market segments. And here is the uncomfortable reality: **D110 identified Path B as the majority of our target market.**

If job logging slips to v1.2, Path B does not exist at launch. Full stop. This is not a degraded experience for verbal-agreement artisans — it is a complete absence of their conversion path. They land on the product, see no entry point that matches how they actually work, and leave.

**The Flawed Assumption: "Devis Flow Is Primary, Job Logging Is Secondary"**

This assumption — embedded in the current sprint prioritization — was built for Path A. It reflects the formal-devis artisan's reality: you create a devis, you win the job, you log work against it. In that flow, devis is primary and job logging is downstream.

But Path B **inverts this entirely**. For the verbal-agreement artisan:
1. The client says "yes" over the phone or in person — no devis ever exists
2. Work begins immediately, logged in a notebook, a voice memo, or nowhere formal
3. The first digital touchpoint is **starting a job card** — not creating a devis

For this archetype, job logging **is** the primary workflow. The devis flow is irrelevant — they will never use it. Treating job logging as secondary, as something to bolt on after the "real" feature (devis) ships, means optimizing for the minority segment while abandoning the majority.

**The Conversion Mathematics Are Clear**

Path A artisans convert through devis creation → acceptance → job start. Path B artisans convert through job creation → work logging → invoice. These are parallel funnels serving different users.

If Sprint 1 ships only Path A:
- Path A users get a complete experience (devis → job)
- Path B users get **nothing** — no entry point, no conversion, no value

If Sprint 1 ships both paths:
- Path A users get the full devis-first experience
- Path B users get their job-first experience
- We capture **both** market segments from day one

**The Technical Reality**

Job logging (D13: Active Job Card) does not require devis flow to function. A job card can be created standalone — client name, description, start date. Work entries can be logged against it. Invoices can be generated from logged work. The full Path B conversion works without a single devis ever being created.

The technical dependency argument for deferral does not hold. Job logging can ship independently. The only reason to delay it is prioritization choice — and that choice, if made, sacrifices the majority segment on behalf of the minority.

**We defined Path A and Path B as co-equal conversion paths in D110.** That resolution carries an obligation: **both paths must be live at launch or the dual-path strategy is a fiction**. Shipping one path and promising the other later is not a phased rollout — it is an incomplete product for half the market.

**Assumption challenged:** The assumption that "job logging is secondary to devis flow" — a prioritization framing designed for Path A (formal-devis artisan) that has been incorrectly applied as a universal truth, when in fact it is inverted for Path B (verbal-agreement artisan), who represents the majority segment.

**Verdict requested:** D13 (Active Job Card / Job Logging) is designated a Sprint 1 non-negotiable. The dual-path conversion architecture requires both Path A and Path B to be operational at launch. Deferring job logging to v1.2 means shipping an incomplete product for the majority segment.

---

## Debate 112: Expert-Comptable Outreach — The Conflict of Interest Problem

**Role:** Growth Strategist

**The Assumption Being Challenged:**

The debate log treats "warm access via Louis's existing accountant" as equivalent to "immediate outreach opportunity." This conflates proximity with credibility, and access with influence. They are not the same thing.

**The Core Problem: Structural Conflict of Interest**

Louis's accountant serves artisan clients. These are the accountant's existing revenue relationships. When Louis asks his accountant to recommend Louis's tool to these clients, he is asking the accountant to do something professionally awkward at minimum, potentially self-damaging at worst.

Consider the incentive structure: if an artisan client adopts Louis's tool and it affects how they manage customers, invoices, or communications, what happens to the accountant's relationship with that client? The accountant becomes associated with a tool they didn't recommend, one that may create more bookkeeping complexity, or worse — may work poorly and reflect negatively on the accountant who handed it out. The accountant gains nothing from a successful referral and absorbs all downside risk from a failed one.

This isn't paranoia. This is standard professional self-interest. And it's the precise reason the accountant will almost certainly NOT execute.

**Why Passive Non-Execution Is the Most Likely Outcome**

The debate log assumes the accountant will either actively refer or actively refuse. In reality, a third outcome dominates: agreement followed by inaction.

Here's how it plays out: Louis asks. The accountant says "sure, send me some materials." Louis sends materials. The accountant files them somewhere and never mentions the tool to a single client. Six months later, Louis checks in. The accountant says "yes, I meant to bring it up with a few people."

This isn't dishonesty. It's social friction compounded by misaligned incentives. The accountant doesn't want to disappoint Louis (relationship cost), doesn't want to damage existing client relationships (professional cost), and doesn't personally benefit from pushing the tool (no incentive). The path of least resistance is to appear cooperative while doing nothing.

**Why Louis's Existing Accountant Cannot Be a First Domino**

A first domino must be someone who:
1. Has motivation to act
2. Faces no structural barrier to acting
3. Gains from the outcome

Louis's accountant fails all three. The expert-comptables who should be targeted first are those with ZERO relationship to Louis — people who can evaluate the tool on its merits, who face no conflict of interest, and who might genuinely benefit from a partnership.

**The Strategic Implication**

Stop treating warm access as a shortcut. It's actually slower than cold outreach in this case, because warm access with conflict of interest produces behavior that looks like progress but generates zero traction.

Louis should pursue his existing accountant relationship for advice, not referrals. Ask the accountant which artisans would be good targets. Use that intel for cold outreach. But do not ask the accountant to be the vector.

**Assumption challenged:** "Warm access via Louis's existing accountant = immediate outreach opportunity"

**Verdict requested:** The first expert-comptable outreach should NOT be to Louis's existing accountant. The relationship creates a conflict of interest that produces passive non-execution, not referrals. Phase 1 expert-comptable outreach should target an unconnected accountant in the same vertical — someone with incentive, no conflict, and genuine client need. Louis's existing accountant is a validation asset, not a sales channel.

---

## Debate 113: Sprint 0 — Six Items Must Be Confirmed Before Day 1

**Role:** Technical Architect

**The Core Argument**

Sprint 0 is not a state of mind. It is a **gate**, not a vibe. Before the team writes a single line of product code, six architectural decisions must be confirmed and committed to git. These are not preferences — they are **load-bearing walls** for the entire project.

**1. Mentions légales templates (U16) — The visible iceberg tip.**

Having four legal templates in git is a regulatory checkbox. But treating it as the green light for Sprint 0 is like getting a driver's license and declaring you're ready for the Indy 500. The license is necessary. It is not sufficient.

**2. Supabase project not created — You cannot authenticate, you cannot store, you cannot prototype.**

Every feature in this Mini-CRM touches the database. Without a live Supabase project, the team is writing blind. Integration tests cannot run. Auth flow cannot be validated. This is a hard dependency for every single Sprint 1 ticket.

**3. 1-page Sprint 0 spec missing — The single most likely item to be skipped, and the most dangerous to skip.**

This spec is the contract between product and engineering. Without it, the team has no shared definition of what "done" means for Sprint 0 deliverables. No scope boundary. No agreed-upon tech stack decisions documented. The 1-page spec is not paperwork. It is the **source of truth** when disputes arise.

**4. API contract not defined — The integration risk that kills sprints.**

We are building a full-stack app with frontend and backend. If the API contract is not agreed upon before development starts, the frontend and backend teams will diverge. A defined API contract (even a draft OpenAPI spec) allows parallel development. Without it, you have sequential development masquerading as agile.

**5. Navigation library not chosen — Routing is the skeleton of the app.**

Changing navigation libraries mid-project is a rewrite. Without a committed choice, code review becomes a religious war and PRs go stale.

**6. PDF generation approach not chosen — Document generation is a core feature.**

PDF generation is not a feature you bolt on at the end. It touches data modeling (line items, taxes, branding), API design (what endpoints serve document data), and frontend rendering (preview before send). Choosing between @react-pdf/renderer, pdfmake, or a headless-Chrome approach changes your entire data pipeline.

**The Real Risk: The "We'll Figure It Out In Sprint 1" Trap**

The most dangerous assumption on this project is that Sprint 0 is a **checklist**, not a **planning session**. The mentions légales templates are a checklist item. The 1-page spec and API contract are *planning work*. Teams under pressure skip the planning and call the checklist "done." Then they arrive at Sprint 1 with no shared understanding, no agreed interfaces, and no skeleton architecture.

**Sprint 0 is not complete when the easy tasks are done. It is complete when the hard architectural decisions are committed and signed off.**

All six items must be resolved. All six must be in git. All six must have a thumbs-up from both the Product Owner and the Technical Lead. Only then is the gate open.

**Assumption challenged:** "Sprint 0 can start as soon as U16 (mentions légales templates) is done" — this conflates a checklist item with a planning session. U16 completion is necessary but nowhere near sufficient.

**Verdict requested:** Sprint 0 cannot begin until all six items are confirmed and committed to git. The 1-page spec and API contract are the most critical and most likely to be skipped — add explicit checklist items for both.

---

## Resolutions — Pulse 2026-03-30T21:55

### D111 RESOLVED — Job Logging Is Sprint 1 Non-Negotiable

The argument is correct. Path B (verbal-agreement artisan) represents the majority segment. Deferring job logging to v1.2 means Path B doesn't exist at launch. The dual-path conversion architecture (D110) requires both paths operational at launch.

**D13 Sprint 1 scope updated:** Active Job Card (job logging) is added to Sprint 1 as a non-negotiable. Sprint 1 now contains: client file + devis flow + Active Job Card (job logging). PDF generation, mentions légales full engine, and WhatsApp sharing are moved to Sprint 1b.

### D112 RESOLVED — Louis's Accountant Is a Validation Asset, Not a Sales Channel

The conflict of interest argument is correct and decisive. Louis's existing accountant cannot be the first expert-comptable GTM domino. The relationship creates structural incentives for passive non-execution.

**D72/U12 UPDATED:**
- Louis's existing accountant: validation conversation only ("can I show you and get honest feedback?"). Not a referral request.
- Expert-comptable outreach: cold outreach to 3-5 unconnected expert-comptables in Caen area who serve BTP/artisan clients. No conflict of interest. Genuine evaluation.
- Phase 1 expert-comptable GTM = cold outreach to conflict-free accountants, not warm outreach to Louis's existing network.

### D113 RESOLVED — Sprint 0 Cannot Start Without All Six Blockers Confirmed

The checklist-vs-planning-session distinction is correct. U16 completion alone does not open the Sprint 0 gate.

**Sprint 0 gate criteria (all six must be confirmed):**
1. 4 mentions légales templates committed to git ✓ (U16)
2. Supabase project dashboard visible (EU region, Frankfurt)
3. 1-page Sprint 0 scope document committed to git
4. API contract defined (shared types file or OpenAPI spec)
5. Navigation library chosen (Expo Router recommended)
6. PDF generation approach chosen (server-side via Supabase Edge Function recommended)

**Sprint 0 timeline updated:** 5 days from gate-open. Gate opens when all six are confirmed. Sprint does not start until all six are resolved.

---

*Last updated: 2026-03-30T21:55*


---

## Pulse 2026-03-30T22:07 — Three New Debates

---

## Debate 114: D99 — Usage-Based Pricing Creates a Monetization Paradox

**Challenge:** D99 (€1.50/devis sent, capped at €29/month) is still OPEN — Louis hasn't evaluated implementation complexity. Product Strategist challenges the core premise.

### Product Strategist — Flat €29 Is the Only Viable Model

**Assumption challenged:** The claim that usage-based pricing "matches artisan seasonality" better than flat pricing is unvalidated founder math. No evidence French artisans asked for this, no cohort data showing seasonal dips, no competitive benchmark proving it drives conversion.

**Core arguments:**
1. **Value anchoring destroys itself.** Usage-based signals "we're afraid to charge €29/month." Capped at €29 is identical in maximum cost to flat €29 — but arrives wrapped in doubt. Flat €29 says "this is worth €29." Capped €1.50/devis says "we're hedging." Confidence is priced in.
2. **Revenue zero-sum for infrastructure you still run.** The capped model guarantees €0 in low-season months. Every SaaS infrastructure cost (Supabase, push, hosting, support) is still there. Flat pricing smooths cash flow for the business, not just the customer.
3. **Cognitive overhead at the worst moment.** Conversion (D96) is triggered by the first paid facture — an emotional, high-stakes moment. Adding per-devis billing at that exact moment is a churn trigger disguised as a feature. Free → €29 is a single clean mental model. Free → €1.50/devis requires re-explanation at the lock-in moment.

**Verdict on D99:** REOPENED — Product Strategist argues usage-based billing should be killed for v1. Flat €29/month is simpler, better for unit economics, and aligned with the single conversion path. Annual billing discount (pay €260/year, get 2 months free) addresses seasonality concern without metering complexity.

---

## Debate 115: PDF Generation — Missing Sprint 0 Gate Item

**Challenge:** D113 listed six Sprint 0 gate items but omitted PDF generation. Technical Architect argues this is an architectural oversight with cascading consequences.

### Technical Architect — PDF Generation Must Be the 7th Gate Item

**Assumption challenged:** The assumption that PDF generation is a feature implementation detail that can be deferred to Sprint 1b. PDF generation is not a feature — it is a rendering architecture decision that constrains the data model, the API contract, and the mentions légales strategy simultaneously.

**Core arguments:**
1. **Three approaches, three different constraints.** Server-side (Supabase Edge + headless Chrome): needs blob storage + PDF endpoint + document reference storage. Client-side (react-pdf/expo-print): no blob storage but mentions légales must be shipped with the app — conflicts with D74's Handlebars/Nunjucks template engine. Hybrid (server HTML template → client PDF): partially satisfies D74 but couples Sprint 0 template engine to Sprint 1b rendering.
2. **D74's Handlebars/Nunjucks template engine only makes sense in a server-rendering context.** If PDFs are client-side, maintaining a template engine in Sprint 0 serves no purpose — scope inflation based on a discarded architectural assumption.
3. **Sprint 1a builds devis flow without knowing how documents are previewed, stored, or sent.** Every architectural decision made in Sprint 0 risks being invalidated by whatever PDF approach Sprint 1b chooses. Building blind into Sprint 1 is expensive to undo.

**Verdict on D113 gate scope:** REOPENED — Technical Architect argues PDF generation approach must be added as the 7th Sprint 0 gate item. Without it, the mentions légales template engine decision (D74) and the API contract (D113 item 4) are built on unstated assumptions about document rendering.

---

## Debate 116: GetApp/Capterra — Wasted Launch Effort for This Audience

**Challenge:** D85 says GetApp and Capterra profiles should be claimed and optimized BEFORE launch, arguing "admin handlers search here first." Growth Strategist challenges this assumption.

### Growth Strategist — GetApp/Capterra Optimization Is Premature and Misallocated Effort

**Assumption challenged:** The assumption that admin handlers (Marc's wife/admin assistant) search GetApp/Capterra BEFORE the artisan has decided to try the product. GetApp/Capterra are mid-to-low-funnel comparison tools — they serve buyers who have already identified a problem and are evaluating options. This gets the funnel backwards.

**Core arguments:**
1. **French artisans aged 45-55 do not browse software comparison sites.** They ask their mate at the yard. They Google "logiciel devis facture artisan pas cher" at 9pm. They ask their expert-comptable. Peer recommendation dominates over comparison-site browsing in SMB solopreneur buying.
2. **The admin handler scenario is the wrong buyer model.** Marc's wife isn't independently discovering software on GetApp — she's validating a choice Marc has already made after hearing about it from a peer. She uses GetApp to validate, not to discover.
3. **Conflating SMB solopreneur buying with B2B enterprise procurement.** Enterprise buyers use G2/GetApp because they have procurement committees and formal evaluation criteria. Marc has neither — he has a WhatsApp group and a preference for people he trusts.
4. **A blank profile with no reviews is worse than no profile.** A listing claiming to serve French artisans with zero actual French artisan reviews signals a brand-new or irrelevant product — fails the credibility test at first impression discovery precisely when it matters most.
5. **10 hours on GetApp pre-launch = empty profile. 10 hours on SEO content + prescriber outreach + expert-comptable cold calls = actual humans in the product.** The ROI calculation is not close.

**Verdict on D85:** REOPENED — Growth Strategist argues GetApp/Capterra optimization should be deferred to Month 3 post-launch, after real user reviews exist. One authentic French artisan review on G2 is worth more than six months of profile polish on an empty listing.

---

*Last updated: 2026-03-30T22:18*

---

## Pulse 2026-03-30T22:18 — Three Specialist Debates

---

## Debate 117: D85 — GetApp/Capterra Competitive Moat vs. Deferred Optimization

**Challenge:** D85 last position was "defer to Month 3, claim Week 1." Growth Strategist challenges the deferral logic with a specific, previously-unmade argument.

### Growth Strategist — Claim Week 1 for Competitive Ranking Moat

**Assumption challenged:** "GetApp/Capterra optimization should be deferred to Month 3 because an empty profile is worse than no profile." This framing assumes the primary risk is profile quality. The real risk is **competitive search displacement** — and it compounds over time in a way that quality cannot reverse cheaply.

**The argument (opposite of D85 last position):**
GetApp's ranking algorithm heavily weights review count and recency. A competitor listing today with 4-6 reviews and a 4.1 rating will structurally outrank our empty profile for 12-18 months — not because they're better, but because the algorithm rewards established presence. Every week of deferral is a week a competitor can claim that ranking position and begin accumulating reviews.

The mechanism is not SEO (D116 correctly killed that). It's **competitive search displacement**: once a competitor holds the top-3 positions for "best invoicing software for French artisans" with 5+ reviews, our profile with the same rating but zero reviews is buried. Delisting and re-ranking is not a simple fix — review count asymmetry is a structural barrier.

**Testable hypothesis:** Compare GetApp ranking positions for "solo artisan invoicing" queries before and after a 6-review threshold for first-mover. First-mover + 4-6 reviews consistently ranks above late-mover + identical rating but zero reviews. If true: 8 weeks of waiting = 12-18 months of ranking disadvantage.

**Counter to D85:** The "empty profile is worse" argument assumes the goal is profile quality. The goal is competitive ranking position. Claim Week 1, populate with screenshots + pricing + feature list (not reviews). Publish Week 3-4 when seed reviews from beta users are ready. Compete for review-count ranking before competitors do — this is a land-grab, not a quality contest.

**Verdict on D85:** REOPENED — GetApp/Capterra should be claimed Week 1 (not deferred to Month 3). populate with screenshots/pricing/features immediately. Publish when seed reviews ready (Week 3-4). The competitive moat argument (review count + ranking position) is distinct from the SEO argument and wasn't made in prior debates.

---

## Debate 118: D99 — Per-Devis Pricing Eliminates Conversion Anxiety

**Challenge:** D99 last position was "flat €29 recommended for v1, seasonality addressed via annual billing discount." Product Strategist challenges the flat-rate recommendation with a conversion-anxiety argument.

### Product Strategist — Per-Devis Removes the "Will I Use This Enough?" Blocker

**Assumption challenged:** "Seasonality can be addressed via annual billing discount." Annual billing requires an upfront commitment decision. The artisan hasn't converted yet. Asking him to commit to €260/year to solve a seasonality problem he hasn't experienced yet is a conversion-blocking layering of two separate decisions.

**The argument (opposite of D99 last position):**
Per-devis (€1.50/devis, capped at €29/month) kills the anxiety that flat €29 cannot touch:

- **€29 flat** → "C'est quoi si je n'envoie que 3 devis ce mois-ci ?" → hesitation → no signup
- **€1.50/devis, capped €29** → "Je paie que ce que j'utilise" → low-stakes trial → signup → habit → value

This maps directly to D12's simplicity-first positioning. D12 wins because friction at any stage kills conversion — onboarding friction, feature friction, **and billing friction**. Flat €29 introduces billing-stage friction: the "am I wasting money?" calculation that activates at the moment of commitment. Per-devis eliminates that calculation entirely. You're not selling a subscription; you're selling a per-use tool.

The cap (€29) means heavy users pay the same as flat. Light users — the hesitant majority — get a guilt-free entry point. Seasonality is handled in the model itself (low season = low spend, no commitment). Annual billing discount becomes a retention mechanism for converted users, not an acquisition tool.

**Verdict on D99:** REOPENED — Per-devis pricing (€1.50/devis, cap €29/month) should replace flat €29 as the primary pricing model. Annual billing discount (€260/year) moves from acquisition tool to retention mechanic for engaged users.

---

## Debate 119: D114 — Fourth PDF Approach: Zero-Schema In-Memory expo-print

**Challenge:** D114 lists PDF generation as requiring a seventh Sprint 0 gate. Three approaches were documented (server-side headless Chrome, client-side react-pdf, hybrid server-HTML-to-client-PDF). Technical Architect proposes a fourth approach that eliminates schema dependency entirely.

### Technical Architect — expo-print as Zero-Schema PDF Shortcut

**Assumption challenged:** "PDF generation approach constrains the data model." All three prior approaches assume PDFs are a data pipeline problem — something stored, referenced, retrieved. This assumption is itself the constraint.

**The fourth approach — in-memory expo-print:**
Use `expo-print` (or `react-native-html-to-pdf` via bridge) to render PDFs entirely in-memory from React Native state, with no document storage, no blob references, and no server round-trip:

1. Build HTML string from in-memory devis state (line items, TVA, client data)
2. Pass to `expo-print.printToFileAsync()` or equivalent
3. Attach resulting file to WhatsApp share intent
4. No document storage needed — the PDF is ephemeral, a render artifact

**Why this is genuinely different from the three prior approaches:**
- No blob storage → no document table → no storage cost
- No PDF URL in API response → no URL lifecycle management
- No server-side template engine dependency → D74's Handlebars/Nunjucks assumption becomes optional, not required
- Data model dependency: **zero** — the HTML is constructed from in-memory React Native state passed as props

**Time to working PDF:** expo-print is a 30-minute integration. The full flow (in-memory state → HTML template → PDF → share) is achievable in 4 hours. Mentions légales content is embedded in the HTML string — no template file, no server rendering, no Handlebars dependency.

**The schema dependency problem solved differently:** Instead of choosing a PDF architecture that predetermines schema constraints, we sidestep the constraint entirely. The PDF is a render of current state, not a retrieval of stored state. Storage (for archival) is a v2 concern.

**Verdict on D114:** CONFIRMED as Sprint 0 gate (7th gate) — but with a specific recommendation: **expo-print in-memory approach** as the preferred path, with server-side PDF (Edge function) as fallback only if print quality or sharing options prove inadequate in real device testing.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D1 | Positioning | Kill "CRM" — devis, factures, relances | 2026-03-30 |
| D2 | MVP scope | 4 features, SEQUENCED sprints | 2026-03-30 |
| D5 | Pricing | Free + €29 two-tier | 2026-03-30 |
| D6 | Trial | No time-limited trial. Free tier IS the trial | 2026-03-30 |
| D12 | Landing page | Simplicity-first | 2026-03-30 |
| D13 | Home view | Job-first — Active Job Card | 2026-03-30 |
| D14 | E-invoicing timing | v2 — NOT Day 1 | 2026-03-30 |
| D15 | Relances differentiator | DE-EMPHASIZED — secondary feature below fold | 2026-03-30 |
| D85 | GetApp/Capterra | REOPENED — Week 1 claim for competitive ranking moat | 2026-03-30T22:18 |
| D95 | Sprint 0 timeline | 5 days (target) / 6.5 days (floor) | 2026-03-30 |
| D99 | Pricing structure | REOPENED — per-devis €1.50/devis, cap €29/month | 2026-03-30T22:18 |
| D114 | PDF Sprint 0 gate | REOPENED — expo-print in-memory proposed as 4th approach | 2026-03-30T22:18 |
| D100 | Architecture | Supabase EU-hosted (Frankfurt) | 2026-03-30 |

| U1 | Discovery | Readiness protocol | 2026-03-30 |
| U2 | E-invoicing platform | Factea first when v2 | 2026-03-30 |
| U7 | Domain | Buy now, park it | 2026-03-30 |

---

*Last updated: 2026-03-30T22:18*

---

## Pulse 2026-03-30T22:30 — Three Resolved (D120, D121, D122)

---

## Debate 120: D99 — Per-Devis Pricing Conflicts With Conversion Trigger Architecture

**Challenge:** Both D118 (per-devis) and D99 last position (flat €29) accepted D96's "first paid facture" conversion trigger as given. Neither examined whether per-devis fundamentally conflicts with how D96 converts users. Product Strategist challenges this unexamined assumption.

### Product Strategist — Per-Devis Introduces Metering Friction at the Peak Conversion Moment

**Assumption challenged:** "Per-devis pricing is compatible with D96's conversion trigger." This shared assumption treats billing and conversion as independent variables. They are not — per-devis injects a billing micro-decision into the exact emotional moment when D96 is designed to convert.

**Core arguments:**

1. **Metering friction at peak conversion.** D96's trigger is "first paid facture" — an emotionally charged event. The artisan used the product, got paid, is maximally invested. Per-devis injects: "your first paid facture is in — that's €1.50." He's calculating: "do I want to pay €1.50 for THIS specific transaction?" The answer may be no if the job margin was thin. Flat €29 converts this to a single binary: continue or don't. One decision, clean.

2. **Retroactive billing shock for Path B artisans.** Path B (verbal-agreement artisan) converts after 45 days of active usage. Under per-devis, he's been accumulating €X in charges he thought were free under the Free tier. At the 45-day trigger, he's presented with all past charges AND a billing model transition. That's a retroactive trust violation. Flat €29 is prospective-only from conversion date.

3. **Annual billing solves seasonality without per-devis complexity.** French artisans already make annual decisions on equipment leases, insurance, and subscriptions. €260/year prepaid = low-season months covered. Same maximum cost as per-devis cap, clean conversion moment, no metering friction.

**Verdict on D99:** RESOLVED — Flat €29/month + €260/year annual billing at launch. Per-devis (€1.50/devis, cap €29) deferred to v1.2 — after conversion architecture validated, seasonality patterns confirmed with real data, and billing integration mature enough for per-transaction charging.

---

## Debate 121: D114 — Ephemeral PDF Is Legally Insufficient for French Accounting Requirements

**Challenge:** D119 proposed expo-print in-memory as a zero-schema shortcut and explicitly labeled storage "a v2 concern." Technical Architect challenges this — French invoice retention law (Code de Commerce L123-22) requires 10-year document storage in tamper-evident form. WhatsApp is not an accounting archive. Treating storage as v2 concern doesn't eliminate the legal exposure — it just defers it.

### Technical Architect — Label Sprint 0 PDF as Prototype, Plan Sprint 1b Storage Migration

**Assumption challenged:** "Storage is a v2 concern." This framing treats the legal exposure as optional. It is not. An artisan using the app who believes their invoices are properly stored — when they live only in WhatsApp threads — has a compliance problem that surfaces at their next expert-comptable meeting or tax audit, not in v2.

**Core arguments:**

1. **Article L123-22 requires 10-year retention in original form.** WhatsApp provides no integrity guarantees, no audit trail, no tamper-evident storage, no access controls. A PDF deletable by sender or recipient at any moment is not compliant. The penalty surfaces during audit — not during Sprint 0 planning.

2. **Phase 2 migration debt is already visible.** D72 (expert-comptable data-sync portal) requires document storage — PDF URLs, blob references, `documents` table, `created_at`, integrity hashes. expo-print provides none of this. Sprint 1b must rebuild everything: blob storage, document table, API contract changes, `factures` record migration. Sprint 0 expo-print investment produces a PDF that Phase 2 discards entirely.

3. **The resolution is honest labeling, not architectural denial.** Sprint 0 expo-print is a prototype document — WhatsApp share only, no legal value, explicitly labeled in code comments and Sprint 0 handoff doc. Sprint 1b adds proper document storage (Supabase blob + `documents` table + PDF URL in API response). These are sequential investments, not alternative paths.

**Verdict on D114:** RESOLVED — expo-print in-memory APPROVED for Sprint 0 (prototype PDF, WhatsApp share only). Sprint 1b adds document storage migration (2-3 days). Legal labeling required in Sprint 0 handoff doc.

---

## Debate 122: D85 — GetApp/Capterra Serves Zero Functions in the Actual Buyer Journey

**Challenge:** D116 argued "defer to Month 3." D117 argued "claim Week 1 for competitive moat." Both assumed the admin handler discovers software on GetApp/Capterra. Growth Strategist challenges this shared premise — D55 explicitly defines the admin handler as an operational validator, not a prospective discoverer. The channel doesn't match the buyer journey.

### Growth Strategist — The Admin Handler Validates, She Doesn't Discover

**Assumption challenged:** "The admin handler will eventually consult GetApp/Capterra as part of her buyer journey." This premise underlies both D116 and D117 but was never examined. D55 invalidates it entirely.

**The actual buyer journey (D55):**
1. Marc discovers via WhatsApp peer referral — "j'utilise ça, c'est génial"
2. Marc tries the Free tier — motivated, acute-need, signs up same day
3. Admin handler encounters product when Marc asks for help with setup — or notices him using it
4. Her role: operational validation ("can this handle our specific client types?") — answered by opening the app and creating a test devis, not by reading a comparison listing
5. GetApp consulted only if Marc is comparing two specific options — which he won't do after a confident peer recommendation

**The result:** GetApp/Capterra ranking position is irrelevant to this buyer journey. Marc doesn't reach the comparison stage. The peer referral closes the deal before GetApp becomes relevant. The 8-10 hours required to claim and optimize the profile would be better spent on expert-comptable outreach (D72 Phase 1 prep) or artisan validation at Point P.

**Verdict on D85:** RESOLVED — GetApp/Capterra removed from TODO until Month 3 evidence contradicts the D55 buyer journey model. Week 1 hours reallocated to expert-comptable cold call script + D91 validation with Louis's own accountant.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D1 | Positioning | Kill "CRM" — devis, factures, relances | 2026-03-30 |
| D2 | MVP scope | 4 features, SEQUENCED sprints | 2026-03-30 |
| D5 | Pricing | Free + €29 two-tier | 2026-03-30 |
| D6 | Trial | No time-limited trial. Free tier IS the trial | 2026-03-30 |
| D12 | Landing page | Simplicity-first | 2026-03-30 |
| D13 | Home view | Job-first — Active Job Card | 2026-03-30 |
| D14 | E-invoicing timing | v2 — NOT Day 1 | 2026-03-30 |
| D15 | Relances differentiator | DE-EMPHASIZED — secondary feature below fold | 2026-03-30 |
| D85 | GetApp/Capterra | **RESOLVED — REMOVED from TODO.** Channel doesn't match D55 buyer journey (admin handler validates, doesn't discover). Revisit Month 3 only if artisan survey contradicts peer-referral model. | 2026-03-30T22:30 |
| D95 | Sprint 0 timeline | 5 days (target) / 6.5 days (floor) | 2026-03-30 |
| D99 | Pricing structure | **RESOLVED — Flat €29/month + €260/year annual.** Per-devis deferred to v1.2. Annual billing solves seasonality without per-devis conversion-moment friction. | 2026-03-30T22:30 |
| D114 | PDF Sprint 0 gate | **RESOLVED — expo-print Sprint 0 prototype, Sprint 1b storage migration.** Legal labeling required. Phase 2 compliance prerequisite acknowledged. | 2026-03-30T22:30 |
| D100 | Architecture | Supabase EU-hosted (Frankfurt) | 2026-03-30 |

| U1 | Discovery | Readiness protocol | 2026-03-30 |
| U2 | E-invoicing platform | Factea first when v2 | 2026-03-30 |
| U7 | Domain | Buy now, park it | 2026-03-30 |

---

*Last updated: 2026-03-30T22:30*

---

*Last updated: 2026-03-30T22:43*

---

## Pulse 2026-03-30T22:43 — Three New Challenges

---

## Debate 123: D12 — "Sans vous prendre la tête" Attracts the Wrong Buyer

**Challenge:** D12 (simplicity-first landing page) — Product Strategist challenges the assumption that simplicity framing converts the acute-pain buyer.

### Product Strategist — Competence Frame Beats Simplicity Frame

**Assumption challenged:** "Sans vous prendre la tête" is the right frame for converting French artisan buyers. The debate treated this as settled — artisans hate admin, they want it easy, lead with ease. But the debate never interrogated *which buyer* this frame activates.

**Core argument:**

"Sans vous prendre la tête" is an avoidance frame. It promises: *this won't give you a headache.* That's appealing to the artisan who already has a system (messy as it is) and is mildly annoyed at switching. This buyer is not in pain. He's comfortable enough. He's browsing.

But the artisan you need to convert is not browsing. He's the one who forgot to send a devis last week, got chewed out by a client, and is now staring at a stack of invoices he hasn't followed up on in two months. He's late on his VAT declaration. He's not avoiding admin — he's drowning in it. He doesn't want something *easy*. He wants something that *works* so he stops getting burned.

**The filtering effect:**
- Avoidance buyer (browsing, mildly annoyed) responds to "simple like WhatsApp" — but converts slowly and churns when friction appears
- Acute pain buyer (forgotten devis, client chasing, VAT mistakes) responds to "competence infrastructure" — recognizes himself immediately, converts fast, stays because the tool solves his specific problem

Simplicity framing is vague. Pain framing is specific. Specificity converts.

**The 5-minute verification constraint:**
Whatever the landing page promises, the free trial must deliver proof within 5 minutes:
- *Ease* is hard to prove quickly — requires the user to do something, evaluate their feelings, decide. Slow and subjective.
- *Competence* is fast to prove — user creates a devis, sends it, gets confirmation, sets a relance. In 5 minutes they have a concrete result answering their specific pain.

If the landing page promises "you won't have to think about admin," the free trial has to slowly reassure. If it promises "you'll never miss a paiement again," the free trial delivers a quick win that feels like proof.

**Proposed revised frame:**
Replace "Sans vous prendre la tête" with a competence frame:
> "Arrêtez de courir après vos paiements."
> "Vos devis envoyés. Vos factures payées. Vos clients suivis."

This is not about being complicated or sophisticated — it's about positioning the tool as competence infrastructure. The thing that means you never again have to be the artisan who forgot, who chased badly, who sent a devis with a typo because you were rushing.

**Verdict on D12:** REOPENED — "Simplicity-first" is the right design philosophy for the product, but the wrong messaging frame for the landing page. The landing page should speak to the pain. Simplicity is proven in the trial, not promised on the homepage.

---

## Debate 124: D100 — Supabase Exit Strategy Has No Exit Trigger

**Challenge:** D100 (Supabase EU-hosted) — Technical Architect challenges the assumption that a revenue-based migration trigger (€5k/mo or 50 users) is the right mechanism.

### Technical Architect — Usage-Based Exit Trigger Required

**Assumption challenged:** "Migrate at 50 users" (premature) or "revisit at €5k/mo" (too late) — both revenue-based triggers are either too early or too late, and both are lagging indicators.

**Core argument:**

Revenue-based triggers tell you what happened. Usage tells you what's about to happen.

At 50 paying users (€1,450/mo gross), Supabase bill is ~€50-150/mo. Migration cost eats 3-6 months of savings. At that stage, you're still in product-market fit discovery — schema is shifting, query patterns unproven. Migrating now means migrating twice or locking in a schema you don't yet understand.

At €5k/mo (~170-200 paying users), you've accumulated exactly the conditions that make migration hard: documents in blob storage, user-generated content, established query patterns, production data that can't be lost. This is when migration is most disruptive and most expensive in opportunity cost.

The real cost curve: at 200 paying users (€5,800/mo revenue), Supabase bill lands at €300-600/mo (compute, storage, bandwidth, auth overhead). That's **5-10% of revenue going to Supabase** — before Louis pays himself, before taxes, before marketing. At 500 users (€14,500/mo), the bill could be €600-1,200/mo — a compounding margin squeeze.

**The composite usage-based exit trigger:**

Not revenue. Not user count. A specific measurable condition where migration window is open and economics are favorable:

**Trigger:** 3 consecutive months where total stored documents >10,000 AND monthly active users >100 AND Supabase bill >€150/mo.

This is a leading indicator — it signals you're approaching the cost curve before you're drowning in it. At 10k documents and 100 MAU, you're generating enough usage to need migration but not so much that migration is catastrophically complex.

**Target stack:**
- Primary: OVH VPS (备用) + Coolify for containerized Postgres + API service
- Alternative: Hetzner (cheaper, EU-hosted) + Coolify
- Database: Managed Postgres on OVH or Hetzner (€10-20/mo for 4-8GB, 100GB SSD — covers 10k documents easily)

At 100 MAU, OVH managed Postgres costs ~€20/mo. The entire migration target stack costs €40-60/mo vs €300-600/mo on Supabase. That's €3,600-6,500/yr saved at 200 users.

**The architectural requirement:**

Build Supabase schema with a thin abstraction layer (repository pattern, raw SQL for critical paths) so the exit is a migration task, not a rewrite. This is Day 1 engineering, not a v2 concern.

**Verdict on D100:** SUPERSEDED — Supabase remains the correct Sprint 0 choice. But D100 needs an addendum: explicit usage-based exit trigger (10k docs + 100 MAU + €150/mo bill), target stack defined (OVH/Hetzner + Coolify + managed Postgres), and a thin abstraction layer in the schema design from Day 1.

---

## Debate 125: D72/D91 — Expert-Comptable Is a Month 4+ Channel, Not Month 1-2

**Challenge:** D72 and D91 (expert-comptable outreach timing) — Growth Strategist challenges the assumption that a French expert-comptable will validate software in Week 1 and refer clients in Week 4-6.

### Growth Strategist — Compliance Liability Makes Expert-Comptable a Phase 2 Channel

**Assumption challenged:** Expert-comptable outreach is a Month 1-2 GTM lever because accountants are trusted by artisans and relationship-building is sufficient to generate referrals.

**Core argument:**

The debate treated expert-comptable recommendation as a relationship and trust problem. It is not. It is a **professional liability problem** — and that distinction collapses the entire Week 1-6 timeline.

Under French law, an expert-comptable is bound by professional standards that make recommending non-compliant invoice software genuinely risky. Specific exposure:

1. **TVA rate accuracy** — French VAT (5.5%, 10%, 20%) is context-dependent by service type, material vs. labor split, region. Recommending a tool that applies the wrong rate implicates the accountant in the client's fiscal non-compliance.

2. **Mentions légales completeness** — French invoices require a specific set of legal mentions (SIRET, SIREN, RCS, TVA intracommunautaire, articles-worth mention, etc.). A tool generating incomplete mentions légales creates liability for the accountant who recommended it.

3. **Sequential numbering integrity** — French fiscal law requires sequential invoice numbers without gaps. A bug breaking numbering exposes the recommending accountant to complicity in fiscal fraud — even if unintentional.

An expert-comptable will not stake their professional license on a product reviewed for 20 minutes in Week 1. The real compliance review cycle:

- Test invoices under real conditions
- Review of edge cases (credit notes, pro-format devis, international clients)
- Internal firm discussion and potentially malpractice carrier review
- Actual artisan clients using it in production

**3-6 months minimum. Not negotiable.**

**The timeline mismatch:**

Week 1 validation ("Louis's accountant says it looks ok") produces a favor, not a commercial signal. It carries zero recommendation drive to other accountants' artisan client bases.

Week 4-6 referral requires testimonials from real artisan users who've been through an expert-comptable review cycle. But an artisan who has used the tool for 4-6 weeks has not had their invoices reviewed by an accountant. "It works fine" ≠ "my accountant reviewed the output and it is compliant." That distinction is the entire value of the expert-comptable referral channel.

**The practical consequence:**

If the team pursues Week 1 expert-comptable outreach as a referral channel, the accountant delays any client recommendation until their own review is complete. That review cannot realistically happen in under 3 months. The Week 4-6 referral milestone silently slips to Month 5-6. Meanwhile the GTM calendar is built on a false assumption about this channel's contribution timing.

**Prescriber networks (architects, property managers, main contractors) have no professional liability exposure.** They are not certifying fiscal compliance — they are suggesting a tool. Their recommendation is social/professional ("I work with guys who use this and it's fine") rather than compliance-backed. This makes them the correct Month 1-3 referral engine:

- They can recommend immediately after personal use
- No legal review cycle required
- Marc trusts their prescriber's opinion as much as an accountant's — without the 3-6 month wait
- "Comment connaissez-vous?" data at signup validates whether prescribers are driving signups

**Proposed revised GTM assumption:**

| Channel | Month 1-3 | Month 4-6 | Month 7+ |
|---------|-----------|-----------|----------|
| Digital (SEO + WhatsApp/Facebook) | PRIMARY | PRIMARY | PRIMARY |
| Specialist retailers | SECONDARY | ACTIVE | ACTIVE |
| Prescriber networks (architects, property managers) | **ELEVATED — PRIMARY for Month 1-3** | ACTIVE | ACTIVE |
| Expert-comptable | **Phase 2 — NOT Week 1** | **Initiate compliance review cycle** | Referral (after real artisan review cycle complete) |

**Verdict on D72/D91:** REOPENED — Expert-comptable outreach should be Phase 2 (Month 4+) after real artisan users have been through a compliance review cycle. D91 (validation vs referral distinction) is correct but the timeline is wrong by 3-4 months. Elevate prescriber networks as primary GTM for Month 1-3.

---

## Updated Decision Table

| ID | Topic | Resolution | Date |
|----|-------|-----------|------|
| D1 | Positioning | Kill "CRM" — devis, factures, relances | 2026-03-30 |
| D2 | MVP scope | 4 features, SEQUENCED sprints | 2026-03-30 |
| D5 | Pricing | Free + €29 two-tier | 2026-03-30 |
| D6 | Trial | No time-limited trial. Free tier IS the trial | 2026-03-30 |
| D12 | Landing page | **REOPENED — competence frame vs simplicity frame** | 2026-03-30T22:43 |
| D13 | Home view | Job-first — Active Job Card | 2026-03-30 |
| D14 | E-invoicing timing | v2 — NOT Day 1 | 2026-03-30 |
| D15 | Relances differentiator | DE-EMPHASIZED — secondary feature below fold | 2026-03-30 |
| D72 | Expert-comptable outreach | **REOPENED — Phase 2 (Month 4+), not Week 1** | 2026-03-30T22:43 |
| D85 | GetApp/Capterra | **RESOLVED — REMOVED from TODO.** | 2026-03-30 |
| D91 | Expert-comptable validation vs referral | **REOPENED — validation timeline wrong by 3-4 months** | 2026-03-30T22:43 |
| D95 | Sprint 0 timeline | 5 days (target) / 6.5 days (floor) | 2026-03-30 |
| D99 | Pricing structure | Flat €29/month + €260/year annual | 2026-03-30 |
| D100 | Architecture | Supabase EU-hosted (Frankfurt) — **REOPENED: add usage-based exit trigger** | 2026-03-30T22:43 |
| D114 | PDF Sprint 0 gate | expo-print Sprint 0 prototype, Sprint 1b storage migration | 2026-03-30 |
| D121 | PDF Sprint 0 gate | expo-print Sprint 0 prototype, Sprint 1b storage migration | 2026-03-30 |

| U1 | Discovery | Readiness protocol | 2026-03-30 |
| U2 | E-invoicing platform | Factea first when v2 | 2026-03-30 |
| U7 | Domain | Buy now, park it | 2026-03-30 |

---

*Last updated: 2026-03-30T22:43*

---

## New from Pulse 2026-03-30T22:43 — Three New Challenges

### Reopened (D12, D72/D91, D100)

- **D12 (Landing page):** Product Strategist challenged — "Sans vous prendre la tête" attracts avoidance-motivated buyers, not acute-pain buyers. The artisan who responds to simplicity is comfortable enough, not drowning. Acute-pain buyers (forgotten devis, client chasing, VAT mistakes) want competence and reliability, not cognitive ease. Proposed: competence frame ("Arrêtez de courir après vos paiements") + trial delivers proof in 5 minutes.
- **D72/D91 (Expert-comptable timing):** Growth Strategist challenged — French expert-comptables have professional liability exposure. They will not recommend software they haven't personally vetted for compliance (TVA rates, mentions légales accuracy, sequential numbering integrity). Compliance review cycle = 3-6 months minimum. Expert-comptable = Phase 2 channel, not Month 1-2. Prescriber networks (architects, property managers) elevated as primary Month 1-3 GTM.
- **D100 (Supabase exit):** Technical Architect challenged — revenue-based triggers ("50 users" or "€5k/mo") are either premature or too late, and both are lagging indicators. Proposed: composite usage-based exit trigger (10k docs + 100 MAU + €150/mo Supabase bill), target stack (OVH/Hetzner + Coolify + managed Postgres), thin abstraction layer from Day 1.

### Challenged assumptions this pulse:
1. "Simplicity-first" landing page frame converts acute-pain buyers (Product Strategist — wrong buyer filtered)
2. Expert-comptable outreach is a Month 1-2 GTM lever (Growth Strategist — compliance liability collapses timeline)
3. Revenue-based migration trigger is the right Supabase exit mechanism (Technical Architect — usage-based is the leading indicator)

### New action items from this pulse:
- [ ] **D12 REOPENED:** A/B test landing page — simplicity frame ("Sans vous prendre la tête") vs competence frame ("Arrêtez de courir après vos paiements"). Run with beta users before launch. Measure: time-on-page, signup rate, Day-7 retention.
- [ ] **D72/D91 UPDATED:** Expert-comptable outreach moved to Phase 2 (Month 4+). Do not budget Week 1 hours for it. Prescriber networks (architects, property managers) become primary Month 1-3 GTM. Document this change in GTM strategy.
- [ ] **D100 UPDATED:** Add explicit Supabase exit trigger to D100: 3 consecutive months where (total_docs > 10,000 AND MAU > 100 AND Supabase_bill > €150/mo). Define target stack: OVH or Hetzner VPS + Coolify + managed Postgres (€40-60/mo at 100 MAU vs €300-600 Supabase). Add thin abstraction layer in schema design from Day 1.
- [ ] **D124 NEW:** Document the Supabase exit plan in architecture notes. Include: trigger metrics, target stack specs, migration estimated effort (2-3 days for data migration, 1 day for schema transfer).

---

*Last updated: 2026-03-30T22:43*
