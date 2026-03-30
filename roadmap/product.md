# Product Roadmap — Mini-CRM

## Objectives

1. Launch a mobile-first CRM targeting French artisans (plumbers, electricians, carpenters) with a frictionless 30-day free trial
2. Achieve product-market fit by interviewing at least 20 artisans before and during beta
3. Deliver legally compliant French invoice generation (factures conformes) out of the box
4. Establish a tiered pricing model (€29/€49/€79/month) that scales with artisan business growth
5. Build trust through transparent data handling (CNIL compliance, Axeptio cookie consent)
6. Reduce artisan churn to <10% at 30 days post-trial by delivering immediate, measurable value
7. Create a product that artisans recommend to peers (word-of-mouth growth engine)

## Subdomains

- **Customer Management**: Contacts, companies, lead tracking
- **Field Operations**: Job scheduling, route-friendly mobile views
- **Financial**: Invoice generation, French-legal facture templates, payment tracking
- **Communication**: Email/SMS reminders, in-app notifications, customer messaging
- **Reporting**: Business dashboard (revenue, jobs, pending invoices)
- **Compliance**: CNIL, RGPD, French accounting standards, cookie consent
- **Growth**: Trial-to-paid conversion, upgrade flows, referral mechanics
- **Support**: Help center, in-app feedback, success playbooks

## Milestones

| Milestone | Target | Description |
|-----------|--------|-------------|
| M1: Discovery | Week 2 | Complete artisan interviews and finalize personas |
| M2: Scope Lock | Week 4 | MVP features frozen via MoSCoW, technical architecture defined |
| M3: Prototype | Week 6 | Clickable onboarding + invoice prototype reviewed by 5 artisans |
| M4: Beta | Week 10 | Private beta with 10 hand-picked artisans, feedback loop active |
| M5: Launch | Week 14 | Public launch: landing page live, trial sign-ups open |
| M6: v1.0 GA | Week 18 | All legal compliance confirmed, production hardened |
| M7: First Expansion | Week 26 | Tier upgrades, referral program, public roadmap published |

## Task Categories

---

### Category: User Research (Artisan Interviews, Personas)

#### Task: UR-001
- **title**: Define artisan interview script
- **description**: Write a semi-structured interview guide covering daily workflows, pain points with current tools (spreadsheets, WhatsApp), invoice management, customer communication, and tech comfort level. Include 15–20 open questions. Pilot with 2 artisans and iterate on the script.
- **inputs**: Research on artisan trade publications, competitor CRM user reviews
- **outputs**: Interview script document (Google Doc), pilot recordings
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: research
- **validation**: Script reviewed and approved by at least 1 domain expert; pilot interviews completed

#### Task: UR-002
- **title**: Recruit 20 artisans for interviews
- **description**: Recruit plumbers, electricians, and carpenters across France (mix of urban/rural, solo/multi-worker, different revenue levels). Use LinkedIn, trade associations (CAPEB, FF Batiment), artisan Facebook groups, and cold outreach. Target 6–8 per trade.
- **inputs**: Trade association contact lists, LinkedIn Sales Navigator access
- **outputs**: List of 20 confirmed interviewees with contact info and scheduling
- **dependencies**: [UR-001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: research
- **validation**: 20 interviews scheduled and confirmed

#### Task: UR-003
- **title**: Conduct artisan discovery interviews
- **description**: Run 45-minute video or in-person interviews with each artisan. Record (with consent), take detailed notes. Probe: job scheduling frustrations, how they track leads, how they send invoices today, what happens when a client does not pay, CRM awareness, willingness to pay (€20–€80/month range), key barriers (complexity, cost, learning curve).
- **inputs**: Interview script (UR-001), recruit list (UR-002)
- **outputs**: 20+ interview transcripts, summary notes per interview
- **dependencies**: [UR-002]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: research
- **validation**: All 20 interviews completed and recordings stored securely

#### Task: UR-004
- **title**: Synthesize interview findings into pain points
- **description**: Review all transcripts. Extract top 10 recurring pain points, top 5 positive surprises, and top 5 negative surprises. Group into themes: scheduling, invoicing, communication, lead tracking, compliance. Create a shared findings presentation.
- **inputs**: Interview transcripts (UR-003)
- **outputs**: Findings deck (PDF/slides), categorized pain point list
- **dependencies**: [UR-003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: research
- **validation**: Findings deck reviewed and approved by founding team

#### Task: UR-005
- **title**: Build primary persona: "Marie la Artisan Solo"
- **description**: Create a detailed persona document for the solo artisan (1–2 person business). Include: demographics (age 35–55, French, rural or peri-urban), goals (win more clients, get paid faster, look professional), frustrations (admin takes time from billable work, forgets to follow up), tech behavior (heavy WhatsApp/SMS user, minimal email, uses smartphone all day), preferred communication (phone + SMS, not email), how they discover software (Google search, peer recommendation, trade shows).
- **inputs**: Interview findings (UR-004)
- **outputs**: Persona document with photo placeholder, quotes, scenario maps
- **dependencies**: [UR-004]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Persona reviewed by at least 3 interviewed artisans (feedback survey)

#### Task: UR-006
- **title**: Build secondary persona: "Thierry l'Artisan Équipé"
- **description**: Create a detailed persona for the small team artisan (3–10 employees, has a secretary or uses an accountant). Include: business complexity (managing multiple crews, larger invoice volumes), goals (coordinate teams, streamline invoicing, maintain client relationships), frustrations (spreadsheets break down, no mobile access for field), tech behavior (uses a computer at office, wants mobile for field), willingness to pay higher tiers.
- **inputs**: Interview findings (UR-004)
- **outputs**: Persona document with scenario maps, upgrade pathway indicators
- **dependencies**: [UR-004]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Persona approved by founding team

#### Task: UR-007
- **title**: Map competitor landscape for French artisan CRMs
- **description**: Research existing solutions: Holded, Pennylane, Zoho CRM, Salesforce for small businesses, Axonaut, Regate. For each: pricing, French invoice compliance, mobile UX, ease of use, common G2/Capterra complaints. Identify gaps our product can fill. Interview 5 users of competing products.
- **inputs**: G2/Capterra reviews, competitor websites, trade press
- **outputs**: Competitive analysis spreadsheet + one-page summary
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: research
- **validation**: Competitive summary presented to founding team

#### Task: UR-008
- **title**: Validate willingness to pay
- **description**: Based on interview responses, compile and analyze price sensitivity data. Segment by: solo vs team, trade type, current tool (spreadsheet vs paid tool). Determine if €29/€49/€79 tiers make sense or need adjustment. Calculate estimated market size (SAM/SOM).
- **inputs**: Interview transcripts with pricing discussions (UR-003)
- **outputs**: Pricing validation report with confidence level per tier
- **dependencies**: [UR-003]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: research
- **validation**: Report with clear recommendation (approve/adjust tiers)

#### Task: UR-009
- **title**: Create artisan empathy map
- **description**: Build empathy maps (see/think/do/feel) for each persona across three scenarios: Monday morning planning, dealing with an overdue invoice, winning a new client. Use quotes from actual interviews.
- **inputs**: Persona docs (UR-005, UR-006), interview transcripts (UR-003)
- **outputs**: Empathy map diagrams (Miro or Figma)
- **dependencies**: [UR-005, UR-006]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Empathy maps reviewed in team workshop

#### Task: UR-010
- **title**: Document UX principles for artisans
- **description**: Based on all research, define 5–7 core UX principles that guide every product decision (e.g., "Zero typing default — tap over text input", "Works offline on bad 4G", "One action per screen"). Write a one-page design principles doc.
- **inputs**: Persona docs, empathy maps, interview pain points
- **outputs**: Design principles document
- **dependencies**: [UR-005, UR-006, UR-009]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Principles approved by founding team and used in design reviews

#### Task: UR-011
- **title**: Create Jobs To Be Done (JTBD) framework
- **description**: Map the top 10 JTBD for French artisans (e.g., "Help me get paid on time", "Make me look professional to my clients", "Remember every client detail so I do not miss follow-ups"). For each JTBD, define the emotional, functional, and social job dimensions.
- **inputs**: Interview findings (UR-004), persona docs
- **outputs**: JTBD framework document with prioritization matrix
- **dependencies**: [UR-004]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: JTBD used as input for feature prioritization session

#### Task: UR-012
- **title**: Research French artisan regulatory environment
- **description**: Research the specific legal obligations for French artisans: mandatory mentions on invoices (SIRET, RCS, TVA), retention requirements (10 years for accounting), DSF (Déclaration de Solvabilité Fiscale) requirements, and any sector-specific rules for plumbers/electricians/carpenters (Certifications, Qualibat, RGE).
- **inputs**: Service-Public.fr, legifrance.gouv.fr, professional trade sites
- **outputs**: Regulatory checklist document
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: research
- **validation**: Checklist reviewed by a French accountant or legal expert

#### Task: UR-013
- **title**: Conduct follow-up interviews post-beta
- **description**: After beta users have used the product for 30 days, conduct 30-minute follow-up interviews with 10 beta users. Focus on: what features they actually use daily, what they abandoned, what they would tell a friend about the product, whether they would pay.
- **inputs**: Beta user list, product usage data
- **outputs**: Follow-up interview transcripts and synthesis report
- **dependencies**: [UR-003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: research
- **validation**: 10 follow-up interviews completed and synthesized

#### Task: UR-014
- **title**: Create persona validation survey
- **description**: Convert persona documents into a 10-question survey to validate persona accuracy with a broader audience (50+ respondents). Distribute via artisan Facebook groups and newsletters. Compare results to original persona assumptions.
- **inputs**: Persona docs (UR-005, UR-006)
- **outputs**: Survey results with persona refinement recommendations
- **dependencies**: [UR-005, UR-006]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: research
- **validation**: Survey distributed; at least 50 responses collected and analyzed

#### Task: UR-015
- **title**: Document artisan daily workflow in detail
- **description**: For each of the 3 artisan trades (plumber, electrician, carpenter), document a typical day/week in detail: when they check phone, when they do admin, typical client interaction types, how they handle emergency calls, how they manage supplies, how they track jobs. Include time-of-day data where available.
- **inputs**: Interview findings (UR-003), trade-specific research
- **outputs**: Workflow documentation per trade (3 documents)
- **dependencies**: [UR-003]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: research
- **validation**: Workflow docs reviewed by at least 2 artisans per trade

#### Task: UR-016
- **title**: Research French artisan seasonal patterns
- **description**: Research how French artisan businesses vary by season: construction sector (busier May–October), heating engineers (busier winter), impact of French holidays (Août, Noël), VAT filing quarters, lead generation seasonality. Understand how this affects product usage patterns and notification timing.
- **inputs**: INSEE data, trade association reports, interview data
- **outputs**: Seasonal pattern report
- **dependencies**: [UR-003]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: research
- **validation**: Report synthesized; informs notification timing decisions

#### Task: UR-017
- **title**: Create artisan technology readiness assessment
- **description**: Assess the typical technology readiness of French artisans: smartphone penetration, internet speed (especially rural), adoption of digital payment (Stripe/Direct+), familiarity with cloud software vs installed software. This informs mobile-first vs offline-first decisions.
- **inputs**: Dar.Cloud, smartphone usage studies, interview data
- **outputs**: Technology readiness report with implications for product
- **dependencies**: [UR-003]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: research
- **validation**: Report used in technical architecture decisions

---

### Category: MVP Scope Definition

#### Task: MS-001
- **title**: Define MVP feature wishlist from research
- **description**: Compile all potential features mentioned in interviews, competitor analysis, and JTBD into a single exhaustive list. Categorize into: Customer Management, Scheduling, Invoicing, Notifications, Reporting, Settings. Aim for 50+ raw features.
- **inputs**: Interview findings (UR-004), JTBD (UR-011), competitor analysis (UR-007)
- **outputs**: Master feature backlog (spreadsheet or Notion)
- **dependencies**: [UR-004, UR-007, UR-011]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Feature backlog contains at least 50 items

#### Task: MS-002
- **title**: Run MoSCoW prioritization workshop
- **description**: Facilitate a 2-hour workshop (with founding team, designers, developers) to categorize all MVP features using MoSCoW: Must have (launch blockers), Should have (significant value), Could have (nice to have), Won't have (future). Use dot-voting and research data as tiebreakers.
- **inputs**: Feature backlog (MS-001), persona docs, research findings
- **outputs**: Prioritized feature list with MoSCoW labels, meeting notes
- **dependencies**: [MS-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: All "Must have" items signed off by full founding team

#### Task: MS-003
- **title**: Define MVP release scope (v1.0)
- **description**: Based on MoSCoW output, define exactly what ships in v1.0 MVP. Must include: customer CRUD, basic invoicing with French legal fields, 30-day trial flow, mobile-responsive UI, email/SMS reminders, dashboard with revenue summary. Define what is explicitly out of scope for v1.0.
- **inputs**: MoSCoW results (MS-002)
- **outputs**: MVP scope document with in-scope/out-of-scope lists
- **dependencies**: [MS-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: MVP scope signed off by all stakeholders; no Must-haves missing

#### Task: MS-004
- **title**: Write MVP user stories
- **description**: For every MVP feature, write 2–3 user stories in format: As a [persona], I want to [action], so that [outcome]. Include acceptance criteria for each story. Stories should map to specific JTBD.
- **inputs**: MVP scope (MS-003), personas (UR-005, UR-006), JTBD (UR-011)
- **outputs**: User story document (Jira/Linear/Notion format)
- **dependencies**: [MS-003, UR-005, UR-006, UR-011]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Each user story has acceptance criteria reviewed by at least one developer

#### Task: MS-005
- **title**: Estimate MVP development effort
- **description**: Work with engineering to estimate story points or ideal days for each user story. Identify the critical path. Flag any high-complexity items that need spiking. Produce a rough MVP timeline.
- **inputs**: User stories (MS-004), engineering team availability
- **outputs**: Estimated sprint plan, critical path document, rough 14-week timeline
- **dependencies**: [MS-004]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: product
- **validation**: Timeline reviewed and committed to by engineering lead

#### Task: MS-006
- **title**: Define MVP technical architecture
- **description**: Define the tech stack decisions for MVP: Nuxt 3 frontend (mobile-first), OVH Postgres per customer (self-hosted), API design (REST vs GraphQL), authentication approach, deployment via Coolify/OVH. Document key architectural decisions.
- **inputs**: MVP scope (MS-003), OVH infrastructure details
- **outputs**: Architecture decision record (ADR) document
- **dependencies**: [MS-003]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: research
- **validation**: ADR reviewed by all developers; no blocking technical questions

#### Task: MS-007
- **title**: Define MVP success metrics
- **description**: Define quantitative success metrics for MVP: trial-to-paid conversion rate (>20% target), time-to-first-invoice (<10 minutes), daily active usage (>3 sessions/week), NPS at 30 days (>30). Map each metric to a specific user story or feature.
- **inputs**: MVP scope (MS-003), industry benchmarks
- **outputs**: MVP success metrics sheet
- **dependencies**: [MS-003]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Metrics approved and instrumented (analytics events defined)

#### Task: MS-008
- **title**: Identify v1.1 post-MVP features
- **description**: Based on MoSCoW output, compile the "Should have" and "Could have" lists as the v1.1 backlog. Prioritize the top 10 v1.1 features. Define entry criteria for when to start v1.1 work (e.g., "when 50 paying customers reached").
- **inputs**: MoSCoW results (MS-002)
- **outputs**: v1.1 backlog with top 10 features and entry criteria
- **dependencies**: [MS-002]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: v1.1 backlog saved and referenced in board-level planning

#### Task: MS-009
- **title**: Lock MVP scope baseline
- **description**: Conduct a formal scope lock meeting. Freeze MVP scope. Any future additions go through change request process. Document the freeze date, agreed scope, and sign-off from all stakeholders.
- **inputs**: MVP scope (MS-003), user stories (MS-004), timeline (MS-005)
- **outputs**: Signed scope lock document
- **dependencies**: [MS-003, MS-004, MS-005]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Document signed by all stakeholders; scope locked

#### Task: MS-010
- **title**: Create MVP Go/No-Go criteria
- **description**: Define clear criteria for when MVP is ready to launch. Include: all Must-have user stories completed, French invoice generation tested and legally compliant, at least 10 beta users active, analytics events firing correctly, support channels operational.
- **inputs**: MVP scope (MS-003), legal requirements (UR-012)
- **outputs**: Go/No-Go checklist with sign-off fields
- **dependencies**: [MS-003, UR-012]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Checklist reviewed; each item assigned an owner

#### Task: MS-011
- **title**: Define MVP database schema
- **description**: Design the Postgres database schema for MVP: tables for users, customers, invoices, invoice_line_items, reminders, notifications, businesses, subscriptions. Define relationships, indexes, and constraints. OVH Postgres per customer architecture means schema must be tenant-aware.
- **inputs**: MVP user stories, technical architecture (MS-006)
- **outputs**: DB schema document (ERD diagram + SQL DDL)
- **dependencies**: [MS-004, MS-006]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: research
- **validation**: Schema reviewed by all backend developers; approved for implementation

#### Task: MS-012
- **title**: Define API endpoints for MVP
- **description**: Document all REST API endpoints needed for MVP: /auth, /customers, /invoices, /reminders, /notifications, /business, /subscription. Define request/response shapes, HTTP methods, status codes, authentication (JWT). Each endpoint maps to a user story.
- **inputs**: User stories (MS-004), DB schema (MS-011)
- **outputs**: API specification document (OpenAPI/Swagger format)
- **dependencies**: [MS-004, MS-011]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: research
- **validation**: API spec reviewed by frontend and backend leads

#### Task: MS-013
- **title**: Create MVP proof of concept
- **description**: Build a functional PoC that demonstrates the core flow: sign up → add customer → create invoice → send → receive payment notification. PoC should be end-to-end testable by founding team within 1 week. Use real OVH Postgres.
- **inputs**: API spec (MS-012), DB schema (MS-011)
- **outputs**: Working PoC deployed on staging environment
- **dependencies**: [MS-012, MS-011]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: research
- **validation**: PoC demoed to founding team; core flow works end-to-end

---

### Category: Feature Prioritization (MoSCoW)

#### Task: FP-001
- **title**: Finalize MoSCoW scoring rubric
- **description**: Define the scoring rubric used for MoSCoW decisions: impact (1–5: how many artisans benefit, how much time/money saved), effort (1–5: dev days), risk (1–5: legal/technical/ux), and revenue impact (1–5: conversion/lift). Items scoring high impact + low effort + low risk = Must have.
- **inputs**: MVP success metrics (MS-007), research findings
- **outputs**: Scoring rubric document with examples
- **dependencies**: [MS-007]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Rubric used consistently in prioritization session

#### Task: FP-002
- **title**: Score all backlog items with MoSCoW rubric
- **description**: Apply the scoring rubric to every item in the feature backlog. Each item gets scores for impact, effort, risk, revenue. Tally totals. Sort by score to inform MoSCoW placement.
- **inputs**: Feature backlog (MS-001), scoring rubric (FP-001)
- **outputs**: Scored backlog with totals and ranking
- **dependencies**: [MS-001, FP-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: All backlog items scored; scores reviewed by engineering

#### Task: FP-003
- **title**: Place all features into MoSCoW tiers
- **description**: Based on scored backlog, place each feature into MoSCoW. Must: top 20% by score, launch blockers, legal requirements. Should: next 30%, significant value, not launch blockers. Could: next 30%, nice to have. Won't: bottom 20%, explicitly deferred.
- **inputs**: Scored backlog (FP-002)
- **outputs**: MoSCoW tier document
- **dependencies**: [FP-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: MoSCoW tiers reviewed and approved

#### Task: FP-004
- **title**: Identify cross-feature dependencies
- **description**: For all Must-have items, map dependencies between features. Some features block others (e.g., authentication blocks all customer management). Create a dependency graph to inform sprint planning.
- **inputs**: MoSCoW tiers (FP-003), user stories (MS-004)
- **outputs**: Feature dependency map (Miro/Figma)
- **dependencies**: [FP-003, MS-004]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Dependency map used in sprint planning

#### Task: FP-005
- **title**: Review MoSCoW with beta artisan advisors
- **description**: Share MoSCoW results with the 5 beta artisan advisors. Gather feedback: does the priority order match their daily experience? Are we missing anything critical? Are any "Must have" items actually less important than we think?
- **inputs**: MoSCoW tiers (FP-003), beta artisan contact list
- **outputs**: Feedback summary with revisions
- **dependencies**: [FP-003]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: research
- **validation**: Feedback collected from at least 3 beta artisans

#### Task: FP-006
- **title**: Document edge cases and exclusions
- **description**: For each Must-have feature, document known edge cases: what happens on Android vs iOS, what if user has no internet, what if invoice total is zero, what if SIRET format is wrong. Define how each edge case is handled or deliberately ignored in MVP.
- **inputs**: MoSCoW Must-have list (FP-003), user stories (MS-004)
- **outputs**: Edge case document per feature
- **dependencies**: [FP-003, MS-004]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Edge case doc reviewed by developer lead

#### Task: FP-007
- **title**: Define Must-have MVP feature acceptance tests
- **description**: For each Must-have feature, write at least 3 automated acceptance tests (or manual test scripts). Tests should cover happy path + 1 error case + 1 edge case per feature. Tests become the definition of done.
- **inputs**: MoSCoW Must-have list (FP-003), edge cases (FP-006)
- **outputs**: Acceptance test suite per feature
- **dependencies**: [FP-003, FP-006]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Tests written for all Must-haves; QA team has reviewed

#### Task: FP-008
- **title**: Define feature usage success criteria
- **description**: For each Must-have feature, define the minimum acceptable usage threshold at 30 days post-launch: e.g., >80% of paying users create an invoice, >60% set up at least 1 reminder. Features below threshold trigger a review.
- **inputs**: Analytics events (AT-001), MVP features
- **outputs**: Feature usage threshold document
- **dependencies**: [AT-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Thresholds documented and monitored in analytics dashboard

#### Task: FP-009
- **title**: Plan feature deprecation policy
- **description**: Define how features that launch but do not perform (low usage, high support burden) will be deprecated. Create a light process: 90-day usage metric review → raise with users → give 60-day notice → remove. Document this policy.
- **inputs**: Product operations learnings
- **outputs**: Deprecation policy document
- **dependencies**: []
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Policy approved by founding team

---

### Category: User Journey Mapping

#### Task: UJ-001
- **title**: Map trial acquisition journey
- **description**: Map the full journey from unknown → landing page → sign-up → email verification → onboarding → first action. Include touchpoints: Google search ad, social post, trade forum mention, landing page, pricing page, trial start, welcome email. Identify friction points at each step.
- **inputs**: Landing page designs, pricing page
- **outputs**: User journey map diagram (Miro/Figma), friction point list
- **dependencies**: [LP-001, PP-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Journey map reviewed by design team

#### Task: UJ-002
- **title**: Map first invoice creation journey
- **description**: Map the detailed journey of a new user creating their first invoice. From entering customer info → adding line items → applying TVA → previewing → sending. Include all possible exit points, error states, and help triggers. This is the highest-stakes moment in the product.
- **inputs**: MVP user stories, onboarding designs
- **outputs**: Step-by-step journey diagram with emotions and pain scores per step
- **dependencies**: [MS-004, OB-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Journey tested with 5 real artisans during beta

#### Task: UJ-003
- **title**: Map customer follow-up journey
- **description**: Map the journey of following up with a client: reminder sent → client sees reminder → client responds (or not) → artisan follows up again → payment received → thank you. Track notification channels (email, SMS, in-app). This journey must be frictionless on mobile.
- **inputs**: Notification designs, invoice features
- **outputs**: Follow-up journey map with channel logic
- **dependencies**: [NU-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Journey reviewed by customer success lead

#### Task: UJ-004
- **title**: Map overdue payment recovery journey
- **description**: Map the journey from invoice due date → first reminder → second reminder → artisan manual call → payment received or abandoned → write-off decision. Define automated touchpoints and manual escalation points. French artisans need culturally appropriate, non-aggressive follow-up language.
- **inputs**: Legal requirements (UR-012), notification logic
- **outputs**: Payment recovery journey with automated flow diagram
- **dependencies**: [UR-012, NU-003]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Flow approved by legal/compliance reviewer

#### Task: UJ-005
- **title**: Map onboarding journey (day 1–7)
- **description**: Map the new user journey from sign-up through first week: email verification → welcome screen → connect first customer → create first invoice → set up reminders → invite team member. Define micro-steps, tooltips, and celebration moments. This must be completable in under 20 minutes.
- **inputs**: MVP scope, onboarding designs
- **outputs**: Onboarding journey map with time estimates per step
- **dependencies**: [MS-003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Onboarding journey tested with 10 beta users; time-to-value measured

#### Task: UJ-006
- **title**: Map upgrade journey from Starter to Pro
- **description**: Map the experience of a Starter tier user hitting limits and upgrading to Pro. Include: limit warning, upgrade CTA placement, pricing page visit, payment flow, instant access to new features. Identify where users drop off in the upgrade flow.
- **inputs**: Pricing tiers defined, analytics baseline
- **outputs**: Upgrade journey map with drop-off points identified
- **dependencies**: [PP-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Journey reviewed by growth/product team

#### Task: UJ-007
- **title**: Map uninstall/churn journey
- **description**: Map the journey of a user who cancels. Include: churn trigger (missed payment, dissatisfaction, found alternative), cancellation flow, exit survey, win-back email sequence, reactivation options. Aim to minimize churn and gather actionable feedback.
- **inputs**: Support ticket analysis, industry churn benchmarks
- **outputs**: Churn journey map with intervention points
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Churn flow implemented; exit survey live

#### Task: UJ-008
- **title**: Create user journey glossary and conventions
- **description**: Standardize terminology for journey mapping: persona names, journey stage names, touchpoint types, emotion scale (1–5). Create a living glossary so all team members use consistent language across all journey maps.
- **inputs**: Persona docs, all journey maps created
- **outputs**: Journey mapping conventions document
- **dependencies**: [UR-005, UR-006]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Glossary used in all subsequent journey mapping work

#### Task: UJ-009
- **title**: Map mobile vs desktop usage differences
- **description**: Based on artisan persona research, map the key differences in how artisans use the product on mobile vs desktop. Identify which journeys are mobile-primary (on-site, with client) vs desktop-primary (end of day admin). Flag any features that are desktop-only but should have mobile equivalents.
- **inputs**: Persona tech behavior (UR-005, UR-006), feature list
- **outputs**: Mobile/desktop journey comparison document
- **dependencies**: [UR-005, UR-006, MS-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Document used in responsive design decisions

#### Task: UJ-010
- **title**: Map customer lifetime journey (first invoice to loyalty)
- **description**: Map the full customer lifecycle: first contact → first job → first invoice → repeat business → referral. Identify key moments that drive loyalty and key moments where customers are at risk of churning. This informs long-term relationship management features.
- **inputs**: Interview data on repeat business, payment history analysis
- **outputs**: Customer lifetime journey map with loyalty drivers
- **dependencies**: [UR-003]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Journey map used in product roadmap planning for retention features

---

### Category: Onboarding Flow Design

#### Task: OB-001
- **title**: Design onboarding information architecture
- **description**: Define the structure of onboarding screens: how many steps, what data is collected at each step, what is deferred to post-onboarding. Design for mobile-first with large touch targets. Information architecture must balance data collection needs vs user friction. Maximum 5 steps for v1.
- **inputs**: User research, MVP scope
- **outputs**: Onboarding IA diagram, screen inventory
- **dependencies**: [MS-003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: IA reviewed by UX team and approved

#### Task: OB-002
- **title**: Design welcome screen and value proposition
- **description**: Design the first screen a new user sees after sign-up. Must clearly state: what this product does, why it is made for them (artisans), the 3 key benefits, and what they can do in the next 5 minutes. Language must be simple, jargon-free, in French. Use visuals of real artisans, not stock photos.
- **inputs**: Design principles (UR-010), persona (UR-005)
- **outputs**: Welcome screen mockups (mobile, desktop)
- **dependencies**: [UR-010, UR-005]
- **priority