# Product Roadmap — Mini-CRM

## Objectives

1. **Primary**: Enable French artisans (plumbers, electricians, carpenters) to manage clients, jobs, and invoices from a mobile-first application
2. **Acquisition**: Convert 30-day free trial users to paid subscribers at 25%+ activation rate by day 30
3. **Retention**: Reduce churn below 5% monthly by ensuring task completion alignment with artisan workflows
4. **Compliance**: Deliver 100% French legal-compliant invoices (factures conformes) from day one
5. **Market fit**: Achieve NPS ≥ 40 within first 6 months of launch

---

## Subdomains

1. **User Acquisition** — Landing page, trial signup, onboarding
2. **Core CRM** — Client management, job tracking, timeline/kanban
3. **Invoicing** — French-compliant invoice generation, PDF export, numbering
4. **Notifications** — Job reminders, payment due dates, trial lifecycle
5. **Analytics** — Event tracking, activation metrics, churn signals
6. **Self-Hosting** — OVH VPS deployment, updates, backups
7. **Support** — Help center, email support, feedback loops
8. **Localization** — French language, French UX conventions, French legal fields

---

## Milestones

### M1: Foundation (Weeks 1-4)
- User research complete (3 artisan interviews minimum)
- MVP scope locked via MoSCoW
- User journey maps finalized
- Repository and CI/CD bootstrapped

### M2: Core MVP (Weeks 5-10)
- Onboarding flow live
- Client management CRUD
- Job management with Client Timeline view (Kanban decision deferred)
- Basic invoice generation (French legal fields)
- Push notifications for iOS/Android

### M3: Invoicing Deep Dive (Weeks 11-14)
- Full French invoice compliance (TVA, mentions obligatoires)
- Invoice templates (3 styles)
- Payment tracking and reminders
- PDF generation and email sending

### M4: Growth (Weeks 15-20)
- Landing page v1
- Pricing page with tier comparison
- Trial success playbooks (day 7/14/30 emails)
- Analytics and event tracking fully instrumented
- App Store listings submitted

### M5: Polish & Launch (Weeks 21-24)
- Feature flags for gradual rollouts
- Public roadmap page
- Feedback widget live
- Error/empty states complete
- Support workflow operational

---

## Task Categories

### Category: User Research

#### Task: UR-001
- **title**: Define artisan interview protocol
- **description**: Create a semi-structured interview script covering daily workflow, pain points with current tools (WhatsApp/excel), invoice management, and mobile usage habits. Target 45-minute remote sessions.
- **inputs**: Research goals document, artisan contact list
- **outputs**: Interview script (Google Doc), consent form template
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: research
- **validation**: Script reviewed by 2 peers, pilot interview conducted

#### Task: UR-002
- **title**: Interview Marc the plumber (persona)
- **description**: Conduct and transcribe interview with Marc — 38-year-old independent plumber in Lyon, 8-10 clients/week, uses WhatsApp for client comms, frustrated with managing invoices on Excel. Capture specific friction points, vocabulary used, and feature requests.
- **inputs**: Interview script (UR-001), Marc's contact info
- **outputs**: Full transcript, summary notes, highlighted quotes
- **dependencies**: [UR-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: research
- **validation**: Transcript uploaded to research folder, key insights extracted

#### Task: UR-003
- **title**: Interview Sophie the electrician (persona)
- **description**: Conduct and transcribe interview with Sophie — 45-year-old electrician in Bordeaux, runs a 2-person crew, struggles with scheduling and invoice follow-ups. Captures multi-user workflow needs and mobile-first behavior (site visits).
- **inputs**: Interview script (UR-001), Sophie's contact info
- **outputs**: Full transcript, summary notes, highlighted quotes
- **dependencies**: [UR-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: research
- **validation**: Transcript uploaded to research folder, key insights extracted

#### Task: UR-004
- **title**: Interview Jean-Pierre the carpenter (persona)
- **description**: Conduct and transcribe interview with Jean-Pierre — 52-year-old carpenter near Toulouse, project-based work (kitchens, wardrobes), long sales cycles, needs to track quote→order→delivery pipeline. Captures project milestone tracking needs.
- **inputs**: Interview script (UR-001), Jean-Pierre's contact info
- **outputs**: Full transcript, summary notes, highlighted quotes
- **dependencies**: [UR-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: research
- **validation**: Transcript uploaded to research folder, key insights extracted

#### Task: UR-005
- **title**: Synthesize persona profiles
- **description**: Compile interview findings into 3 detailed personas: Marc the plumber, Sophie the electrician, Jean-Pierre the carpenter. Each persona should include: demographics, tech comfort level, current tools, top 3 pain points, desired outcomes, and quotes. Add a 4th "fringe" persona for hobbyist tradespeople.
- **inputs**: Transcripts (UR-002, UR-003, UR-004)
- **outputs**: Persona document (PDF + Figma)
- **dependencies**: [UR-002, UR-003, UR-004]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: research
- **validation**: Persona document reviewed by all stakeholders, approved in Notion

#### Task: UR-006
- **title**: Map competitor landscape
- **description**: Research existing solutions used by French artisans: traditional CRM tools (Salesforce上手?), French-specific tools (Fisy, Kel group?), WhatsApp+Excel workflows, accounting software (Cegid, Sage). Identify gaps and opportunities. Document pricing, features, and user reviews.
- **inputs**: Web research, App Store competitor apps
- **outputs**: Competitor analysis spreadsheet + summary slide deck
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: research
- **validation**: 5+ competitors documented with feature comparison matrix

#### Task: UR-007
- **title**: Survey quantitative pain points
- **description**: Distribute a 10-question Google Forms survey to 50+ French artisans via trade associations, Facebook groups (Artisans du Bâtiment), and LinkedIn. Questions cover: current invoicing time, biggest workflow frustrations, willingness to pay, device usage (iOS vs Android).
- **inputs**: Survey questions, distribution channels list
- **outputs**: Survey results (CSV), analysis summary
- **dependencies**: [UR-005]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: research
- **validation**: Minimum 50 responses received, data cleaned and analyzed

#### Task: UR-008
- **title**: Document mobile usage patterns
- **description**: Analyze how French artisans use mobile devices on job sites — glove-friendly touch targets, outdoor screen brightness, voice input needs, offline requirements. Create a mobile context guide for design decisions.
- **inputs**: Interview insights (UR-002/003/004), survey data (UR-007)
- **outputs**: Mobile context document with design implications
- **dependencies**: [UR-002, UR-003, UR-004, UR-007]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: research
- **validation**: Document shared with design team, 5+ actionable insights extracted

#### Task: UR-009
- **title**: Identify feature request themes
- **description**: Cluster all feature requests from interviews and survey into themes (e.g., "quick invoice from phone", "SMS reminders to clients", "photo attachments on jobs"). Rank by frequency and artisan value.
- **inputs**: Interview notes, survey responses
- **outputs**: Feature theme clusters with priority ranking
- **dependencies**: [UR-002, UR-003, UR-004, UR-007]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: research
- **validation**: At least 10 distinct themes identified, top 5 agreed upon by product team

#### Task: UR-010
- **title**: Validate pricing sensitivity
- **description**: During interviews and survey, test reaction to €29/49/79/month tiers. Identify price anchors, deal-breaker thresholds, and value-perception language used by artisans.
- **inputs**: Interview transcripts, survey data
- **outputs**: Pricing sensitivity report with willingness-to-pay ranges
- **dependencies**: [UR-002, UR-003, UR-004, UR-007]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: research
- **validation**: Report includes at least 3 pricing insights per persona

#### Task: UR-011
- **title**: Document artisan vocabulary and jargon
- **description**: Collect all French trade-specific terminology used by plumbers, electricians, and carpenters. Map to app UI labels. Ensure copy uses language artisans actually use — not corporate French.
- **inputs**: Interview transcripts, industry publications
- **outputs**: Artisan vocabulary glossary (French)
- **dependencies**: [UR-002, UR-003, UR-004]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: research
- **validation**: Glossary has 50+ terms, reviewed by at least one native-speaker artisan

#### Task: UR-012
- **title**: Research OVH VPS technical context
- **description**: Understand the technical comfort level of target users regarding self-hosting. Are they comfortable with SSH? Do they have existing VPS? What are their hosting fears? Document support implications.
- **inputs**: Interview answers about technical setup, survey data
- **outputs**: Self-hosting comfort report
- **dependencies**: [UR-002, UR-003, UR-004, UR-007]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: research
- **validation**: Report includes self-hosting fear map and mitigation strategies

#### Task: UR-013
- **title**: Create jobs-to-be-done framework
- **description**: Frame the product around jobs-to-be-done: When [situation], I want to [motivation], so I can [expected outcome]. Create 10+ JTBD statements covering the core user stories.
- **inputs**: Persona documents, interview insights
- **outputs**: JTBD framework document
- **dependencies**: [UR-005]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: research
- **validation**: At least 10 JTBD statements, voted on by product team for top 5

#### Task: UR-014
- **title**: Research French trade seasonality
- **description**: Identify seasonal patterns in artisan work (e.g., heating engineers busy in autumn, construction slows in August). Map to trial and onboarding timing implications.
- **inputs**: Industry data, interview input
- **outputs**: Seasonality calendar with product implications
- **dependencies**: []
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: research
- **validation**: Calendar created with actionable insights for marketing timing

---

### Category: MVP Scope Definition (MoSCoW)

#### Task: MVP-001
- **title**: Facilitate MoSCoW prioritization workshop
- **description**: Gather product, design, and engineering leads for a 2-hour workshop to categorize all proposed features into Must-have / Should-have / Could-have / Won't-have (this quarter). Use votable dot-mocracy format.
- **inputs**: Feature list from research, JTBD framework
- **outputs**: MoSCoW board (Miro or Notion), final prioritized list
- **dependencies**: [UR-005, UR-013]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: All participants agree on final MoSCoW split, documented in meeting notes

#### Task: MVP-002
- **title**: Define MVP feature set (Must-Haves)
- **description**: Document the final list of Must-Have features that constitute the MVP. These are features without which the product cannot ship. Examples: client creation, job creation linked to client, basic invoice with TVA, mobile-responsive UI.
- **inputs**: MoSCoW board (MVP-001)
- **outputs**: MVP feature list with acceptance criteria per feature
- **dependencies**: [MVP-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Feature list approved by all stakeholders, no more than 15 Must-Have items

#### Task: MVP-003
- **title**: Define Should-Have features (post-MVP)
- **description**: Document Should-Have features that add significant value but aren't blocking launch. These go into the roadmap for versions 1.1+. Examples: recurring invoices, calendar sync, bulk SMS.
- **inputs**: MoSCoW board (MVP-001)
- **outputs**: Should-Have backlog with rough sizing
- **dependencies**: [MVP-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Backlog has at least 20 Should-Have items with rough effort estimates

#### Task: MVP-004
- **title**: Scope technical MVP infrastructure
- **description**: Define the technical scope for MVP: database schema (clients, jobs, invoices), authentication (email+password, magic link), file storage (invoice PDFs), hosting (OVH VPS Docker stack), CI/CD pipeline.
- **inputs**: MVP feature list (MVP-002)
- **outputs**: Technical scope document with ERD draft
- **dependencies**: [MVP-002]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: product
- **validation**: Document reviewed by lead engineer, ERD validated

#### Task: MVP-005
- **title**: Define MVP out-of-scope list
- **description**: Explicitly list what is NOT in MVP to prevent scope creep. Examples: multi-user teams (beyond single artisan), inventory management, accounting software sync, time tracking.
- **inputs**: MoSCoW board (MVP-001)
- **outputs**: Out-of-scope document with rationale for each item
- **dependencies**: [MVP-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Out-of-scope list reviewed and signed off by product lead

#### Task: MVP-006
- **title**: Create MVP milestone timeline
- **description**: Break MVP into 4-week sprints with clear sprint goals. Identify the sprint where each Must-Have feature ships. Establish sprint review cadence.
- **inputs**: MVP feature list, team capacity
- **outputs**: 12-week sprint plan with milestones
- **dependencies**: [MVP-002, MVP-004]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Timeline shared with all stakeholders, no conflicts identified

#### Task: MVP-007
- **title**: Define MVP success metrics
- **description**: Define what "success" looks like for MVP launch: trial-to-paid conversion ≥ 20%, day-7 activation ≥ 40%, NPS ≥ 30, no P0 bugs in first 2 weeks.
- **inputs**: Research insights, business goals
- **outputs**: MVP success metrics dashboard spec
- **dependencies**: [MVP-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Metrics approved by founding team, baseline values set

#### Task: MVP-008
- **title**: Document tier-gating strategy for MVP
- **description**: Map which features are free (trial), which unlock at €29, €49, and €79. Ensure the free trial includes enough to be useful but forces upgrade for power features. Document in a feature matrix.
- **inputs**: Pricing tiers, MoSCoW prioritization
- **outputs**: Feature tier matrix (spreadsheet)
- **dependencies**: [MVP-001, MVP-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Tier matrix reviewed by product and marketing, no conflicts with MoSCoW

#### Task: MVP-009
- **title**: Write MVP user stories
- **description**: Translate each Must-Have feature into user story format: As a [persona], I want to [action], so that [outcome]. Include acceptance criteria written in Gherkin (Given/When/Then).
- **inputs**: MVP feature list, personas
- **outputs**: User story backlog (Notion or Linear)
- **dependencies**: [MVP-002, UR-005]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Each Must-Have has at least one user story with acceptance criteria

#### Task: MVP-010
- **title**: Estimate MVP engineering effort
- **description**: Have engineering leads estimate effort (story points or hours) for each MVP user story. Identify any high-risk items requiringSpikes. Create an effort vs. priority matrix.
- **inputs**: User story backlog (MVP-009)
- **outputs**: Estimated backlog with velocity projection
- **dependencies**: [MVP-009]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: All Must-Have stories estimated, sprint capacity validated against 12-week plan

---

### Category: User Journey Mapping

#### Task: UJM-001
- **title**: Map trial-to-first-paid-job journey stages
- **description**: Create a detailed journey map covering 6 stages: Discovery → Sign-up → Onboarding → First Value → Conversion → Retention. For each stage, document: user actions, touchpoints, emotions, pain points, opportunities.
- **inputs**: Personas, JTBD framework
- **outputs**: Full journey map (Figma or Miro)
- **dependencies**: [UR-005, UR-013]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: product
- **validation**: Journey map reviewed in cross-functional workshop

#### Task: UJM-002
- **title**: Map Marc's complete workflow journey
- **description**: Trace Marc's journey from hearing about the product to completing his first paid job invoice. Every step on his phone, every fear, every moment of delight. Include offline/on-site context.
- **inputs**: Marc persona, journey stages
- **outputs**: Marc-specific journey narrative with screenshots/wireframes
- **dependencies**: [UR-002, UJM-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Journey reviewed with Marc (or similar artisan) for accuracy

#### Task: UJM-003
- **title**: Map Sophie's team workflow journey
- **description**: Trace Sophie's journey including her interactions with her apprentice. Multi-device context (phone on-site, computer in office). Identify where team features would fit in future.
- **inputs**: Sophie persona, journey stages
- **outputs**: Sophie-specific journey narrative
- **dependencies**: [UR-003, UJM-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Journey identifies at least 3 multi-user pain points

#### Task: UJM-004
- **title**: Map Jean-Pierre's project milestone journey
- **description**: Trace Jean-Pierre's journey through a multi-week project (quote → approval → material order → installation → invoice). Long time spans, multiple handoffs, client approval points.
- **inputs**: Jean-Pierre persona, journey stages
- **outputs**: Jean-Pierre-specific journey narrative with timeline visualization
- **dependencies**: [UR-004, UJM-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Journey identifies at least 3 milestone-tracking needs

#### Task: UJM-005
- **title**: Identify journey drop-off points
- **description**: Based on journey maps, identify where users are most likely to abandon: signup form, onboarding checklist, first invoice creation. Prioritize by likelihood and severity.
- **inputs**: Journey maps, competitor UX learnings
- **outputs**: Drop-off risk matrix with severity ratings
- **dependencies**: [UJM-001, UJM-002, UJM-003, UJM-004]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: At least 5 critical drop-off points identified with mitigation strategies

#### Task: UJM-006
- **title**: Map emotional peak moments
- **description**: Identify the 3-5 moments in the journey where the user should feel success, pride, or relief. These are emotional anchors to design around. Examples: first invoice sent, first client thank-you, first payment received.
- **inputs**: Journey maps, artisan interviews
- **outputs**: Peak moment list with design implications
- **dependencies**: [UJM-001, UJM-002, UJM-003, UJM-004]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Peak moments agreed upon, each has a design suggestion

#### Task: UJM-007
- **title**: Define "aha moment" for each persona
- **description**: Identify the specific action each persona must complete to feel the product's value. This is the activation action. Marc: send first invoice. Sophie: schedule a job with reminder. Jean-Pierre: create a project with milestones.
- **inputs**: Personas, journey maps
- **outputs**: Aha moment definition per persona
- **dependencies**: [UR-005, UJM-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Each aha moment is specific, measurable, and achievable within first session

#### Task: UJM-008
- **title**: Map touchpoint inventory
- **description**: Catalog every touchpoint a user has with the product: email (welcome, onboarding, day-7, day-14, day-30), in-app notifications, push notifications, SMS (if applicable), phone/chat support.
- **inputs**: Journey stages, success playbooks
- **outputs**: Touchpoint inventory spreadsheet
- **dependencies**: [UJM-001, SP-001, SP-002, SP-003]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: All touchpoints mapped to journey stages, no gaps

#### Task: UJM-009
- **title**: Create user flow diagrams for core actions
- **description**: Create detailed user flow diagrams for 5 core flows: (1) Sign up for trial, (2) Create first client, (3) Create first job, (4) Generate first invoice, (5) Receive first payment. Each flow shows happy path + error branches.
- **inputs**: Journey maps, MVP features
- **outputs**: 5 user flow diagrams (Figma)
- **dependencies**: [UJM-001, MVP-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Each flow has been walked through with at least one artisan for validity

#### Task: UJM-010
- **title**: Map trial expiration journey
- **description**: Map the journey for users who don't convert — the trial expiration, the "time's up" email, the lock-screen experience, the upgrade prompt. Make this respectful, not aggressive.
- **inputs**: Journey maps, business requirements
- **outputs**: Trial expiration flow diagram
- **dependencies**: [UJM-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Flow designed to minimize frustration, maximize reactivation potential

---

### Category: Onboarding Flow Design

#### Task: ONB-001
- **title**: Design onboarding architecture
- **description**: Decide on onboarding type: interactive product tour, contextual checklists, or a linear wizard. Recommend adaptive checklist that learns from user actions. Define how on/off-boarding state is persisted.
- **inputs**: Journey maps, user research
- **outputs**: Onboarding architecture decision doc
- **dependencies**: [UJM-001, UJM-009]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Architecture approved by product and engineering leads

#### Task: ONB-002
- **title**: Design first-5-minutes experience
- **description**: Design the critical first 5 minutes: welcome screen → account creation (email or FranceConnect) → company profile setup → first client creation walkthrough. Every screen should have one job. Zero cognitive overload.
- **inputs**: Onboarding architecture, personas
- **outputs**: Screen-by-screen wireframes for first 5 minutes
- **dependencies**: [ONB-001, UR-005]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: design
- **validation**: Wireframes tested with 3 artisans, completion rate ≥ 80%

#### Task: ONB-003
- **title**: Design company profile setup step
- **description**: Company name, SIRET number (validate format), address, email, phone, logo upload (optional), trade specialization (multi-select). Keep optional fields minimal — capture essential legal info only.
- **inputs**: Legal requirements, onboarding architecture
- **outputs**: Company profile wireframes, field validation rules
- **dependencies**: [ONB-001, LC-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: All French legal fields captured, SIRET validated with check digit

#### Task: ONB-004
- **title**: Design first client creation walkthrough
- **description**: Guide user through creating their first client during onboarding. Pre-fill with placeholder if user skips. Explain why we need client info. Show how client links to invoice.
- **inputs**: Onboarding wireframes, UJM-009
- **outputs**: First client creation screen designs
- **dependencies**: [ONB-002, UJM-009]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Tested with artisans, understood within 30 seconds

#### Task: ONB-005
- **title**: Design onboarding checklist UI
- **description**: Create a persistent or dismissible onboarding checklist component. Shows progress: "3/5 complete". Items: Setup company, Add first client, Create first job, Send first invoice, Invite team member (or skip). Checklist state persists across sessions.
- **inputs**: Onboarding architecture, MVP features
- **outputs**: Checklist component specs, states (pending/active/complete)
- **dependencies**: [ONB-001, MVP-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Component built and deployed, click-through rate measured

#### Task: ONB-006
- **title**: Design FranceConnect integration
- **description**: Offer FranceConnect as an optional sign-up/login method for users who have it. This is a French government identity provider that simplifies account creation. Design the flow: FranceConnect button → redirect → account linking.
- **inputs**: FranceConnect API docs, design system
- **outputs**: FranceConnect flow wireframes, account linking logic
- **dependencies**: [ONB-002]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: design
- **validation**: FranceConnect flow tested with sandbox credentials

#### Task: ONB-007
- **title**: Design role/usage intent capture
- **description**: During onboarding, capture what the artisan primarily uses the app for: managing clients, scheduling jobs, sending invoices, all of the above. This data powers feature flagging and onboarding personalization.
- **inputs**: Research insights, product strategy
- **outputs**: Intent capture screen, storage schema
- **dependencies**: [ONB-002]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Intent data used to personalize dashboard within 2 weeks of implementation

#### Task: ONB-008
- **title**: Create onboarding copy in French
- **description**: Write all onboarding microcopy in French. Tone: friendly, professional, never corporate. Use "tu" for informal address. Avoid jargon. Every label should match artisan vocabulary (from UR-011 glossary).
- **inputs**: Vocabulary glossary (UR-011), wireframes
- **outputs**: Copy document with translations, approved by native speaker
- **dependencies**: [UR-011, ONB-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Copy reviewed by 3 artisans for comprehension

#### Task: ONB-009
- **title**: Design onboarding progress indicator
- **description**: Design a clear progress indicator for the onboarding wizard (step X of Y). Shows what's completed, what's current, what's remaining. Mobile-friendly tap targets.
- **inputs**: Onboarding wireframes
- **outputs**: Progress indicator component specs
- **dependencies**: [ONB-002]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Progress indicator implemented in prototype, tested

#### Task: ONB-010
- **title**: Design skip vs. required UX patterns
- **description**: Define which onboarding steps are required vs. skippable. Required: company name, at least one client. Skippable: logo, team invite. Design skip affordance clearly — not hidden, not aggressive.
- **inputs**: Onboarding wireframes, product strategy
- **outputs**: Skip/required decision matrix with UI patterns
- **dependencies**: [ONB-002]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Decision matrix approved, implemented in onboarding flow

#### Task: ONB-011
- **title**: Build onboarding analytics events
- **description**: Define analytics events for onboarding: onboarding_started, step_completed, step_abandoned, onboarding_skipped, onboarding_completed. Include properties: step_name, time_on_step, skip_reason if applicable.
- **inputs**: Onboarding wireframes, analytics plan
- **outputs**: Event tracking spec for onboarding
- **dependencies**: [ONB-001, AT-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: All events instrumented in test environment, verified in analytics dashboard

#### Task: ONB-012
- **title**: Design re-onboarding for returning users
- **description**: Design experience for users who signed up but never completed onboarding (dormant accounts). Email re-engagement → return to exactly where they left off. Show "welcome back" context.
- **inputs**: Onboarding flow, email templates
- **outputs**: Re-onboarding flow wireframes
- **dependencies**: [ONB-002, SP-004]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Re-onboarding flow tested with 5 dormant users

---

### Category: Dashboard/Home Screen Design

#### Task: DSH-001
- **title**: Research Client Timeline vs. Kanban approaches
- **description**: Deep-dive into the Client Timeline vs. Kanban debate. Timeline: chronological view of all client interactions. Kanban: column-based job status board. Evaluate pros/cons for mobile-first artisan use case. Test with artisans.
- **inputs**: Product strategy, artisan input
- **outputs**: Decision document with recommendation
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: research
- **validation**: Decision made and documented, no further debate

#### Task: DSH-002
- **title**: Design Client Timeline view
- **description**: If Timeline is chosen: design a reverse-chronological feed of client interactions, jobs, invoices, and notes. Each card shows: client name, job type, status, next action. Filter by: today/tomorrow/this week/all. Quick-add button floating.
- **inputs**: Dashboard architecture, timeline decision
- **outputs**: Timeline wireframes (mobile and tablet)
- **dependencies**: [DSH-001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: design
- **validation**: Timeline tested with 5 artisans, usability score ≥ 4/5

#### Task: DSH-003
- **title**: Design Kanban board view
- **description**: If Kanban is chosen: design a 4-5 column board (Nouveau / En cours / En attente / Facturé / Payé). Drag-and-drop cards between columns. Each card: client name, job description, due date, amount. Mobile-optimized horizontal scroll.
- **inputs**: Dashboard architecture, kanban decision
- **outputs**: Kanban wireframes (mobile and tablet)
- **dependencies**: [DSH-001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: design
- **validation**: Kanban tested with 5 artisans, task completion time measured

#### Task: DSH-004
- **title**: Design hybrid Timeline + Kanban view
- **description**: Design an alternative that combines both: a timeline as the primary view with a collapsible Kanban summary widget. Or a swipe gesture to toggle. This respects the debate outcome.
- **inputs**: Timeline and Kanban wireframes
- **outputs**: Hybrid view wireframes with toggle interaction
- **dependencies**: [DSH-002, DSH-003]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: design
- **validation**: Hybrid tested against single views in A/B test (if time permits)

#### Task: DSH-005
- **title**: Design home screen quick-action bar
- **description**: Bottom action bar on mobile with 4 primary actions: Nouveau client, Nouveau devis/job, Nouvelle facture, Messages. Always visible, thumb-reachable, with haptic feedback.
- **inputs**: Mobile design system, onboarding insights
- **outputs**: Quick-action bar component specs
- **dependencies**: [DSH-001, ONB-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Component built, tap targets verified (min 44x44pt)

#### Task: DSH-006
- **title**: Design search and filter experience
- **description**: Global search bar for clients, jobs, invoices. Voice input option (mobile). Filter chips: by status, date range, amount range, client. Save filter presets. Design for speed — results in <200ms perceived.
- **inputs**: Dashboard wireframes, performance requirements
- **outputs**: Search/filter wireframes and interaction specs
- **dependencies**: [DSH-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Search tested with 50+ client database, results relevant

#### Task: DSH-007
- **title**: Design notification center on dashboard
- **description**: Bell icon with unread count badge. Dropdown shows recent notifications: job reminders, invoice due dates, payment received, trial expiring. Mark as read. Link to relevant item.
- **inputs**: Notification system design (NTF-001)
- **outputs**: Notification center component specs
- **dependencies**: [DSH-001, NTF-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Notification center implemented, badge counts accurate

#### Task: DSH-008
- **title**: Design dashboard KPI widgets
- **description**: Top-of-dashboard widgets showing: Revenue this month, Outstanding invoices (count + amount), Jobs this week, New clients this month. Tappable → drill-down. Customizable order via drag.
- **inputs**: Business metrics, dashboard layout
- **outputs**: KPI widget specs (4 widgets minimum)
- **dependencies**: [DSH-001, SM-002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: KPI data accurate (verified against database), load time <1s

#### Task: DSH-009
- **title**: Design dashboard empty state
- **description**: When no clients/jobs exist yet, show a friendly empty state. Not a blank screen — a welcoming illustration + "Ajoutez votre premier client" CTA. Guide to onboarding completion.
- **inputs**: Empty state guidelines, onboarding flow
- **outputs**: Empty state designs for all dashboard sections
- **dependencies**: [DSH-001, ERR-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Empty state reviewed for tone, CTA click-through rate tracked

#### Task: DSH-010
- **- **title**: Design user preference for default view
- **description**: Allow users to set their default dashboard view (Timeline, Kanban, or Hybrid) as a preference. Store in user settings. First-time users see Timeline by default (product decision).
- **inputs**: Dashboard wireframes, user settings
- **outputs**: Preference toggle component
- **dependencies**: [DSH-001, DSH-002, DSH-003, DSH-004]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Preference saved and applied on next login

#### Task: DSH-011
- **title**: Design tablet-specific dashboard layout
- **description**: Design a responsive dashboard optimized for iPad/tablet. Sidebar navigation + main content area. Artisans may use tablet at home office vs. phone on-site. Adapt KPI widgets and timeline/kanban for wider screens.
- **inputs**: Mobile wireframes, responsive breakpoints
- **outputs**: Tablet layout wireframes
- **dependencies**: [DSH-002, DSH-003]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Layout tested on iPad Air, no horizontal scroll needed

---

### Category: Notification & Reminder UX

#### Task: NTF-001
- **title**: Define notification strategy and types
- **description**: Catalog all notification types: job reminders (24h before, morning of), invoice due (3 days, 1 day, overdue), payment received, trial expiring (14 days, 7 days, 1 day, expired), new client added, weekly summary. Map to channel: push, email, SMS.
- **inputs**: Journey map touchpoints, business rules
- **outputs**: Notification type inventory spreadsheet
- **dependencies**: [UJM-008]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: All notification types mapped to user journey stages

#### Task: NTF-002
- **title**: Design push notification architecture
- **description**: Design push notification system for iOS (APNs) and Android (FCM). Define payload structure, notification categories, action buttons (e.g., "Voir" / "Ignorer"), and deep-link routing to specific screens.
- **inputs**: Notification types, mobile platforms
- **outputs**: Push notification architecture doc
- **dependencies**: [NTF-001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: design
- **validation**: Test notifications received on iOS and Android devices

#### Task: NTF-003
- **title**: Design notification permission request flow
- **description**: Design the native OS permission request experience. Show a contextual in-app explanation screen BEFORE the native prompt ("Pour ne pas manquer vos RDV..."). Offer "Plus tard" option without being annoying.
- **inputs**: Push architecture, Apple/Google guidelines
- **outputs**: Permission request wireframes and trigger logic
- **dependencies**: [NTF-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Permission acceptance rate ≥ 60% (benchmark vs. industry 40%)

#### Task: NTF-004
- **title**: Design job reminder notification UI
- **description**: Design the visual and textual content of job reminder notifications. Title: "RDV demain: [Client Name]". Body: "[Job type] - [Address]". Actions: "Voir détails", "Appeler client". Include rich media: small map thumbnail if location available.
- **inputs**: Notification types, brand guidelines
- **outputs**: Job reminder notification templates (iOS/Android)
- **dependencies**: [NTF-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Notification renders correctly on iOS and Android, tap opens correct screen

#### Task: NTF-005
- **title**: Design invoice due reminder notifications
- **description**: Design invoice payment reminder notifications: 3 days before due, 1 day before, on due date, 3 days overdue, 7 days overdue. Escalating urgency tone. Include one-tap "Relancer le client" action button.
- **inputs**: Notification types, invoicing workflow
- **outputs**: Invoice reminder notification templates with copy variations
- **dependencies**: [NTF-001, INV-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Templates reviewed by native speaker for appropriate tone

#### Task: NTF-006
- **title**: Design in-app notification center
- **description**: Design a dedicated in-app notification center screen (accessible from dashboard bell icon). List all notifications with read/unread state, grouping by date. Allow bulk mark-as-read. Show "No notifications" empty state.
- **inputs**: Notification types, dashboard design
- **outputs**: Notification center screen wireframes
- **dependencies**: [NTF-001, DSH-007]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Notification center loads in <500ms with 100+ notifications

#### Task: NTF-007
- **title**: Design notification quiet hours
- **description**: Allow users to set quiet hours (e.g., 22:00-07:00) during which push notifications are silenced. Urgent notifications (overdue invoice, emergency) override quiet hours. Define in settings with easy toggle.
- **inputs**: Notification types, user preferences
- **outputs**: Quiet hours settings UI and logic spec
- **dependencies**: [NTF-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Quiet hours respected, urgent notifications delivered regardless

#### Task: NTF-008
- **title**: Design notification preferences center
- **description**: Let users granularly control which notifications they receive: toggle per type (job reminders, invoice reminders, marketing, tips). Explain each toggle in plain French. Defaults set to product-recommended levels.
- **inputs**: Notification types, settings UI
- **outputs**: Notification preferences screen
- **dependencies**: [NTF-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Preferences saved correctly, notifications reflect updated preferences

#### Task: NTF-009
- **title**: Design trial expiration notifications
- **description**: Design notification sequence for trial expiration: 14-day warning ("Il vous reste 14 jours"), 7-day warning, 3-day warning, 1-day warning, day-30 expired. Each has escalating urgency. Link to upgrade flow.
- **inputs**: Trial lifecycle, notification strategy
- **outputs**: Trial expiration notification sequence
- **dependencies**: [NTF-001, SP-001, SP-002, SP-003]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Notification sequence tested end-to-end

#### Task: NTF-010
- **title**: Build notification scheduling system
- **description**: Build the backend notification scheduling system. Triggered by events (job created, invoice due date set). Uses cron jobs or queue-based workers. Handles timezone correctly (France = CET/CEST).
- **inputs**: Notification types, backend architecture
- **outputs**: Notification scheduling system spec
- **dependencies**: [NTF-001, NTF-002]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: product
- **validation**: Notifications sent at correct times, timezone respected

---

### Category: Invoice Template Design

#### Task: INV-001
- **title**: Research French invoice legal requirements
- **description**: Thoroughly research all legally required fields for French invoices (factures conformes). Sources: Code général des impôts, Code de commerce. Key mentions: seller details, buyer details, invoice number (numéro de facture), date, line items, TVA rates, total HT/TTC, payment terms, penalty rates.
- **inputs**: French tax code, legal resources
- **outputs**: Invoice legal requirements checklist
- **dependencies**: [LC-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: research
- **validation**: Checklist reviewed by French accountant or legal expert

#### Task: INV-002
- **title**: Design invoice template A: Classic
- **description**: Design a classic, professional invoice template. Clean layout with company logo at top. Sections: seller header, client details, invoice table (description, qty, unit price, TVA%, total), TVA breakdown, total TTC, payment terms, IBAN, footer with legal mentions.
- **inputs**: Legal requirements, brand guidelines
- **outputs**: Invoice Template A (Classic) — Figma mockup + HTML/CSS template
- **dependencies**: [INV-001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: design
- **validation**: Template reviewed by French accountant for legal compliance

#### Task: INV-003
- **title**: Design invoice template B: Modern
- **description**: Design a modern invoice template with accent colors, subtle branding. Same required fields as Template A but with a more contemporary layout. Sans-serif fonts, clear hierarchy.
- **inputs**: Legal requirements, brand guidelines
- **outputs**: Invoice Template B (Modern) — Figma mockup + HTML/CSS template
- **dependencies**: [INV-001]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: design
- **validation**: Template reviewed for readability and print quality

#### Task: INV-004
- **title**: Design invoice template C: Compact
- **description**: Design a compact single-page invoice template optimized for mobile preview and email. Minimal whitespace but all required fields present. A4-compatible but designed for digital-first viewing.
- **inputs**: Legal requirements, mobile-first constraints
- **outputs**: Invoice Template C (Compact) — Figma mockup + HTML/CSS template
- **dependencies**: [INV-001]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: design
- **validation**: Template fits on A4 when printed, all fields legible

#### Task: INV-005
- **title**: Design invoice line item editor
- **description**: Design the UI for adding/editing invoice line items: description (free text), quantity (numeric), unit (hours, units, meters, etc.), unit price (€), TVA rate (0%, 5.5%, 10%, 20%), total auto-calculated. Quick-add from previous invoices.
- **inputs**: Invoice templates, mobile UI constraints
- **outputs**: Line item editor wireframes
- **dependencies**: [INV-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Editor tested on mobile, all fields easily editable

#### Task: INV-006
- **title**: Design TVA (VAT) handling UI
- **description**: Design UI for TVA rate selection per line item. Support French TVA rates: 0% (exonéré), 5.5% (taux réduit — travaux immobilier), 10% (taux réduit — rénovation), 20% (taux normal). Auto-calculate HT from TTC and vice versa.
- **inputs**: French TVA rules, invoice templates
- **outputs**: TVA selection UI and calculation logic
- **dependencies**: [INV-001, INV-005]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: TVA calculations verified against French tax rules

#### Task: INV-007
- **title**: Design invoice preview and PDF generation
- **description**: Design live invoice preview as user fills in details. "Aperçu" button shows rendered invoice. PDF generation using server-side rendering (wkhtmltopdf or similar). Ensure PDF output matches screen exactly.
- **inputs**: Invoice templates, technical stack
- **outputs**: Invoice preview component + PDF generation pipeline
- **dependencies**: [INV-002, INV-003, INV-004]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: design
- **validation**: PDF generated matches preview pixel-perfect, file size <500KB

#### Task: INV-008
- **title**: Design invoice email sending flow
- **description**: Design "Envoyer la facture" flow: compose email with pre-filled subject ("Facture n°[XXX]"), editable body text, attachment of PDF. "Copier le lien" option for WhatsApp sharing. Track open/read receipts if available.
- **inputs**: Invoice template, email system
- **outputs**: Email composer with invoice attachment
- **dependencies**: [INV-007]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Email sent and received with correct PDF attachment

#### Task: INV-009
- **title**: Design invoice payment status tracking
- **description**: Track invoice payment status: Brouillon (draft), Envoyée (sent), Payée (paid), En retard (overdue). Visual status badge on invoice list. Manual "Marquer comme payée" action with optional payment date.
- **inputs**: Invoice workflow, dashboard
- **outputs**: Payment status tracking UI
- **dependencies**: [INV-008]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Status transitions correctly, history maintained

#### Task: INV-010
- **title**: Design invoice numbering system
- **description**: Define invoice numbering convention compliant with French law. Format: [PREFIX]-[YEAR]-[SEQUENTIAL]. Example: "FAC-2026-0042". Must be sequential, no gaps. Provide manual number override with warning about legal compliance.
- **inputs**: French invoice regulations
- **outputs**: Invoice numbering scheme document
- **dependencies**: [INV-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Numbering scheme approved by legal, tested for no duplicates

#### Task: INV-011
- **title**: Design credit note template
- **description**: Design credit note (avoir) template for invoice cancellations or adjustments. Required fields similar to invoice + reference to original invoice number. Same templates A/B/C styles.
- **inputs**: Invoice templates, French legal requirements
- **outputs**: Credit note templates (3 styles)
- **dependencies**: [INV-002, INV-003, INV-004]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Credit note legally compliant, can be sent to client

#### Task: INV-012
- **title**: Design recurring invoice feature
- **description**: Design recurring invoice setup: frequency (monthly, quarterly, annual), start date, auto-generate draft on schedule. Not in MVP but prepare data model.
- **inputs**: Invoice workflow, user research
- **outputs**: Recurring invoice wireframes and data model
- **dependencies**: [INV-001]
- **priority**: low
- **estimated_complexity**: high
- **agent_type**: design
- **validation**: Wireframes complete, data model reviewed by engineering

---

### Category: French Legal Compliance for Invoices

#### Task: LC-001
- **title**: Compile French invoice legal mentions checklist
- **description**: Create a master checklist of all mandatory legal mentions for French invoices. Sources: Articles 289 and 441 of Code général des impôts, Code de commerce L441-3. Include: seller identity (name, address, SIRET), buyer identity, date, invoice number, line items, TVA, total TTC, payment terms, penalty clause, ESC (escompte).
- **inputs**: French tax code, French legal resources
- **outputs**: Legal mentions checklist (Google Sheets)
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: research
- **validation**: Checklist reviewed by French legal expert or accountant

#### Task: LC-002
- **title**: Validate SIRET format and check digit
- **description**: Implement SIRET number validation. SIRET = 14 digits (9-digit SIREN + 5-digit NIC). Last digit is check digit (Luhn algorithm). Validate format on input. SIREN should be verifiable via INSEE API if possible.
- **inputs**: SIRET format rules
- **outputs**: SIRET validation function spec
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Validation correctly accepts valid SIRETs, rejects invalid ones

#### Task: LC-003
- **title**: Implement mention légale footer template
- **description**: Design the "mentions légales" footer section that appears on every invoice. Contains: RCS [ville], SIRET, TVA intracommunautaire (FRXXXXXXXXXXXX), capital social (if applicable), and the "Clause de penalty de retard" text (taux minimal 3x taux BCE + 10pp).
- **inputs**: Legal checklist, French legal templates
- **outputs**: Mentions légales footer text (3 variants based on company type)
- **dependencies**: [LC-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Footer text reviewed by French lawyer, accurate for each company type

#### Task: LC-004
- **title**: Design IBAN and payment details display
- **description**: Design how bank details (IBAN, BIC/SWIFT, nom de la banque) appear on the invoice. French IBAN format validation (FR76 XXXX...). Clear, readable typography. Ensure no accidental truncation.
- **inputs**: French banking formats
- **outputs**: Bank details display spec
- **dependencies**: [LC-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: IBAN correctly formatted, passes French IBAN validation

#### Task: LC-005
- **title**: Implement TVA rate configuration per user
- **description**: Allow users to configure their default TVA rate(s) based on their business type. Plumbers/electricians doing home improvement may use 10% rate, not 20%. Store TVA configuration in company settings.
- **inputs**: French TVA rules, company settings
- **outputs**: TVA configuration UI and schema
- **dependencies**: [LC-001, INV-006]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: TVA configuration correctly applied to new invoices

#### Task: LC-006
- **title**: Design payment terms and late fee display
- **description**: Design how payment terms (e.g., "Paiement sous 30 jours") and late fees (e.g., "Pénalités de retard: 3 fois le taux d'intérêt légal") appear on invoices. French law requires these mentions.
- **inputs**: French payment term regulations
- **outputs**: Payment terms section spec
- **dependencies**: [LC-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Payment terms displayed correctly on all templates

#### Task: LC-007
- **title**: Audit invoice templates for compliance
- **description**: Have a French accountant or lawyer review all three invoice templates (Classic, Modern, Compact) for legal compliance. Fix any missing mentions or incorrect formatting discovered during audit.
- **inputs**: Invoice templates, legal checklist
- **outputs**: Compliance audit report with fixes
- **dependencies**: [INV-002, INV-003, INV-004, LC-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: research
- **validation**: All issues from audit resolved, templates re-reviewed

#### Task: LC-008
- **title**: Implement invoice archive for legal retention
- **description**: French law requires invoice retention for 10 years (comptabilité). Design system to archive generated invoices with immutability guarantees. Cannot be deleted or modified once issued.
- **inputs**: French accounting regulations
- **outputs**: Invoice archive system design
- **dependencies**: [LC-001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: product
- **validation**: Archived invoices cannot be modified, searchable, exportable

#### Task: LC-009
- **title**: Design quote/devis template
- **description**: Design quote (devis) template separate from invoice. Similar layout but clearly marked "DEVIS" and includes validity period. French law: devis must mention "devis établi gratuitment ou payant".
- **inputs**: Invoice templates, French quote regulations
- **outputs**: Devis template with all required mentions
- **dependencies**: [INV-002, LC-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Devis template legally reviewed

#### Task: LC-010
- **title**: Research auto-entrepreneur specific requirements
- **description**: Many target users will be auto-entrepreneurs. Research specific invoicing requirements for auto-entrepreneurs: mention "Auto-entrepreneur", exemption from TVA (or not if over threshold), specific SIRET placement, etc.
- **inputs**: Auto-entrepreneur regulations
- **outputs**: Auto-entrepreneur invoice requirements doc
- **dependencies**: [LC-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: research
- **validation**: Requirements documented, reflected in template variants

---

### Category: Pricing Page Design

#### Task: PRC-001
- **title**: Define tier feature differentiation
- **description**: Define exactly which features are included in each tier (Essentiel €29, Premium €49, Pro €79). Document in a feature matrix. Ensure clear differentiation that justifies price jump.
- **inputs**: MoSCoW prioritization, business model
- **outputs**: Feature tier matrix spreadsheet
- **dependencies**: [MVP-008]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Feature matrix reviewed by founding team, no ambiguity

#### Task: PRC-002
- **title**: Design pricing page layout
- **description**: Design the pricing page: 3-column layout (Essentiel / Premium / Pro), clear feature lists, "Le plus populaire" badge on Premium. Annual/monthly toggle with savings callout ("-20%"). Mobile: stacked cards with recommended tier first.
- **inputs**: Brand guidelines, feature matrix
- **outputs**: Pricing page wireframes (desktop + mobile)
- **dependencies**: [PRC-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Wireframes reviewed by 5 artisans for clarity and decision clarity

#### Task: PRC-003
- **title**: Write pricing page French copy
- **description**: Write all pricing page copy in French. Explain each tier's value proposition in plain language. Use artisan vocabulary. Avoid corporate buzzwords. Include FAQ section addressing common objections ("J'ai juste besoin d'un outil simple").
- **inputs**: Feature matrix, UR-011 vocabulary
- **outputs**: Pricing page copy document
- **dependencies**: [PRC-001, PRC-002, UR-011]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Copy reviewed by native speakers, comprehension tested with artisans

#### Task: PRC-004
- **title**: Design annual/monthly toggle UI
- **description**: Design the billing toggle: monthly (paiement mensuel) vs. annual (paiement annuel -20%). Clear pricing display for both options. Annual shows "Économisez €X/an" badge.
- **inputs**: Pricing page wireframes
- **outputs**: Toggle component specs
- **dependencies**: [PRC-002]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Toggle state persists, prices update correctly

#### Task: PRC-005
- **title**: Design FAQ section
- **description**: Design FAQ accordion on pricing page. Top 8 questions: "Puis-je changer d'abonnement ?", "Que se passe-t-il à la fin de mon essai ?", "Mes données sont-elles sécurisées ?", "Comment fonctionne l'hébergement sur mon VPS ?", etc.
- **inputs**: Common objections, support tickets
- **outputs**: FAQ wireframes
- **dependencies**: [PRC-002, CS-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: FAQ answers reviewed by support team for accuracy

#### Task: PRC-006
- **title**: Design upgrade/downgrade flow
- **description**: Design the in-app upgrade flow: from current tier → new tier selection → payment → confirmation. Also design downgrade flow (effective end of billing period). Handle prorated charges.
- **inputs**: Pricing tiers, billing system
- **outputs**: Upgrade/downgrade flow wireframes
- **dependencies**: [PRC-001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: design
- **validation**: Upgrade flow tested end-to-end with Stripe integration

#### Task: PRC-007
- **title**: Design trial-to-paid conversion UX
- **description**: Design the end-of-trial conversion experience: trial expiring banner in-app, dedicated upgrade screen with benefit summary, one-click upgrade. Make it feel like a natural next step, not a push.
- **inputs**: Trial lifecycle, pricing page
- **outputs**: Conversion flow wireframes
- **dependencies**: [PRC-001, PRC-002, NTF-009]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Conversion flow tested, drop-off rate measured

#### Task: PRC-008
- **title**: Design custom/hidden "Enterprise" tier
- **description**: For large artisan shops (5+ people), design an Enterprise tier or "Contact us" path. Not publicly priced. Capture lead info for sales follow-up.
- **inputs**: Business model, sales process
- **outputs**: Enterprise CTA wireframes
- **dependencies**: [PRC-001]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Enterprise path captures leads in CRM

#### Task: PRC-009
- **title**: Price anchoring and comparison design
- **description**: Position Premium (€49) as the recommended tier. Design visual hierarchy to guide eyes: middle column slightly larger, accent color on recommended tier, "Commencez gratuitement" CTA below recommended.
- **inputs**: Pricing psychology research
- **outputs**: Pricing visual hierarchy spec
- **dependencies**: [PRC-002]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: A/B test different visual hierarchies if time permits

#### Task: PRC-010
- **title**: Design invoice for subscription billing
- **description**: Design the invoice/receipt users receive when they pay their monthly or annual subscription. Must be French-compliant for SaaS subscription. Includes: company details, service description, billing period, amount, TVA.
- **inputs**: Invoice templates, billing system
- **outputs**: Subscription invoice template
- **dependencies**: [INV-002, PRC-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Subscription invoices legally reviewed

---

### Category: Landing Page (Trial Acquisition)

#### Task: LP-001
- **title**: Define landing page value proposition
- **description**: Define the primary headline and subheadline for the landing page. Based on user research: focus on "gagnez du temps" (time savings), "facturez comme un pro" (professional invoices), "plus jamais raccroc" (never miss a job). Test at least 3 variants.
- **inputs**: Personas, pain points, competitor positioning
- **outputs**: 3 headline variants with rationale
- **dependencies**: [UR-005, UR-009]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Headlines tested with target users, highest-converting headline selected

#### Task: LP-002
- **title**: Design landing page hero section
- **description**: Design the above-the-fold hero section: headline, subheadline, email capture form ("Commencez votre essai gratuit — 30 jours"), and hero image/video showing the app on a phone with a French artisan.
- **inputs**: Value propositions, brand guidelines
- **outputs**: Hero section wireframes (desktop + mobile)
- **dependencies**: [LP-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Hero section tested with heatmap, email capture rate ≥ 15%

#### Task: LP-003
- **title**: Design landing page feature highlights
- **description**: Design 3-4 feature highlight sections: (1) Gérez vos clients en unclic, (2) Créez des factures conformes en 2 minutes, (3) Ne manquez plus un RDV. Each with illustration/icon, short description.
- **inputs**: MVP features, UX writing
- **outputs**: Feature highlight wireframes
- **dependencies**: [LP-001, MVP-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Feature sections reviewed for clarity by 3 artisans

#### Task: LP-004
- **title**: Design social proof section
- **description**: Design social proof section: testimonials from 3 artisans (placeholder personas), "Ils高效isent 30min par jour" stat callouts, press logos if any, Trustpilot rating. All in French.
- **inputs**: User research quotes, brand guidelines
- **outputs**: Social proof section wireframes
- **dependencies**: [LP-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Testimonials feel authentic (not corporate), reviewed by French speakers

#### Task: LP-005
- **title**: Design pricing teaser section
- **description**: Mini pricing section on landing page: "À partir de €29/mois". Link to full pricing page. Not the full comparison — just enough to answer "how much does it cost?".
- **inputs**: Pricing page, LP-001
- **outputs**: Pricing teaser wireframes
- **dependencies**: [PRC-002, LP-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Pricing teaser links to full pricing page

#### Task: LP-006
- **title**: Design FAQ section for landing page
- **description**: Expand FAQ section for landing page (vs. pricing page FAQ). Top 5 questions specific to the product: "Dois-je installer quelque chose ?", "Mes données sont-elles en sécurité ?", "Puis-je annuler à tout moment ?"
- **inputs**: Common objections, support insights
- **outputs**: FAQ accordion wireframes
- **dependencies**: [LP-001, CS-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: FAQ answers reviewed for accuracy

#### Task: LP-007
- **title**: Design final CTA section
- **description**: Design the bottom-of-page CTA section: repeat email capture form, urgency element ("Rejoignez X artisans qui gagnent du temps"), reassurance ("Sans carte bancaire — 30 jours gratuits").
- **inputs**: Hero design, conversion optimization
- **outputs**: Final CTA wireframes
- **dependencies**: [LP-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Final CTA tested against variant without urgency element

#### Task: LP-008
- **title**: Write landing page French copy
- **description**: Write all landing page copy in French. Tone: friendly, direct, artisan-to-artisan. Use "tu". Avoid "solution", "plateforme", "écosystème". Reference common scenarios: "Quand vous êtes sur un chantier...".
- **inputs**: LP wireframes, UR-011 vocabulary
- **outputs**: Landing page copy document
- **dependencies**: [LP-001, LP-002, LP-003, LP-004, LP-005, LP-006, LP-007, UR-011]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Copy reviewed by native speakers, passes readability test (score ≥ 70)

#### Task: LP-009
- **title**: Implement landing page in staging
- **description**: Implement the landing page in staging environment using Next.js or similar. Integrate email capture with Mailchimp/Brevo. Set up A/B test framework for headline variants.
- **inputs**: Landing page designs, hosting setup
- **outputs**: Live staging landing page with email capture
- **dependencies**: [LP-001, LP-002, LP-003, LP-004, LP-005, LP-006, LP-007, LP-008]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: product
- **validation**: Page loads in <2s, email capture submits successfully to CRM

#### Task: LP-010
- **title**: Design mobile-optimized landing page
- **description**: Ensure landing page is fully mobile-optimized. Single column layout on mobile, large tap targets, no horizontal scroll. Hero image/video mobile-friendly (autoplay muted or poster image).
- **inputs**: Landing page designs, mobile-first principles
- **outputs**: Mobile-optimized landing page
- **dependencies**: [LP-009]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: Page renders correctly on iPhone SE and iPhone 15, no horizontal scroll

#### Task: LP-011
- **title**: Set up UTM tracking and attribution
- **description**: Set up UTM parameters for all traffic sources to landing page. Define attribution model (first touch). Track in analytics: source, medium, campaign, content, term.
- **inputs**: Analytics plan, marketing channels
- **outputs**: UTM tracking schema and analytics setup
- **dependencies**: [AT-001, AT-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: UTM params captured in analytics, attributed correctly

#### Task: LP-012
- **title**: Create conversion funnel tracking
- **description**: Define conversion funnel: landing page → email submitted → trial signup started → trial signup completed → first client added → first invoice sent. Track each step with events.
- **inputs**: Landing page, onboarding flow, analytics plan
- **outputs**: Conversion funnel event tracking spec
- **dependencies**: [LP-009, ONB-011, AT-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Funnel visualized in analytics dashboard, drop-off points identified

---

### Category: Success Metrics Definition

#### Task: SM-001
- **title**: Define trial activation metrics
- **description**: Define activation metrics: Day 1: account created + email verified. Day 3: first client added. Day 7: first job created. Day 14: first invoice created. Day 30: subscription started. Set target percentages for each.
- **inputs**: Aha moments, onboarding research
- **outputs**: Activation milestone definitions with target %
- **dependencies**: [UJM-007, ONB-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Metrics defined, approved by founding team, instrumented

#### Task: SM-002
- **title**: Define engagement metrics
- **description**: Define engagement metrics beyond activation: weekly active users (WAU), daily active users (DAU), sessions per week, actions per session. Establish baseline at launch.
- **inputs**: Industry benchmarks, product goals
- **outputs**: Engagement metric definitions with baseline targets
- **dependencies**: [SM-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Metrics instrumented, baseline captured in first 30 days

#### Task: SM-003
- **title**: Define conversion metrics
- **description**: Define conversion metrics: trial-to-paid rate (target ≥ 25% by day 30), annual vs. monthly plan selection ratio, upgrade rate from Essentiel to Premium, churn rate (target < 5%/month).
- **inputs**: Business model, industry benchmarks
- **outputs**: Conversion metric definitions with targets
- **dependencies**: [SM-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Metrics tracked from day 1 of launch

#### Task: SM-004
- **title**: Define retention cohort analysis
- **description**: Define retention cohort analysis: monthly cohorts of trial signups, tracked for 30/60/90 day retention. Churn by tier, churn by activation status.
- **inputs**: Analytics system, business model
- **outputs**: Cohort analysis definition document
- **dependencies**: [SM-001, SM-003]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Cohort dashboard live within 30 days of launch

---

### Category: Analytics & Event Tracking

#### Task: AT-001
- **title**: Instrument analytics SDK (PostHog)
- **description**: Install and configure PostHog (self-hosted or cloud) in the mobile app. Set up user identification (anonymous + authenticated), session tracking, and screen view events. Ensure GDPR-compliant data collection (consent banner, data anonymization).
- **inputs**: App codebase, PostHog account, GDPR compliance requirements
- **outputs**: PostHog SDK integrated, base events firing correctly
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: engineering
- **validation**: Events visible in PostHog dashboard for test user

#### Task: AT-002
- **title**: Define and register event schema
- **description**: Define the canonical event schema for all user interactions: trial_signup, onboarding_complete, first_client_added, first_job_created, first_invoice_sent, invoice_viewed, subscription_started, subscription_cancelled, support_contacted. Each event includes user_id, timestamp, properties.
- **inputs**: User journey maps, PostHog setup
- **outputs**: Event schema document, registered events in PostHog
- **dependencies**: [AT-001, UJ-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: engineering
- **validation**: All events fire correctly for test user flows

#### Task: AT-003
- **title**: Build activation and funnel dashboards
- **description**: Create PostHog dashboards for key funnels: signup → onboarding → first meaningful action (FMA) → trial-to-paid conversion. Include trend lines, cohort comparisons, and drop-off points. Set up alerts for anomalous drop-off rates.
- **inputs**: Event schema (AT-002), PostHog workspace
- **outputs**: PostHog dashboard with activation and funnel views
- **dependencies**: [AT-002, SM-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: engineering
- **validation**: Dashboards accessible to product team, updated daily

#### Task: AT-004
- **title**: Set up revenue and churn tracking
- **description**: Integrate Stripe webhooks to track MRR, new subscriptions, upgrades, downgrades, and churned accounts in PostHog. Link revenue events to user properties for cohort revenue analysis.
- **inputs**: Stripe account, PostHog, subscription tiers
- **outputs**: Revenue dashboard in PostHog, churn signal alerts
- **dependencies**: [AT-001, SM-003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: engineering
- **validation**: Revenue numbers match Stripe dashboard within 1% variance

#### Task: AT-005
- **title**: Create NPS and feedback correlation view
- **description**: Link NPS survey responses (AT-007) and in-app feedback submissions to user properties in PostHog. Build a dashboard correlating NPS score with activation status, plan tier, and feature usage patterns.
- **inputs**: NPS responses, in-app feedback, PostHog user properties
- **outputs**: NPS correlation dashboard
- **dependencies**: [AT-002, FL-002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Dashboard live within 60 days of launch

---

### Category: User Feedback Loops

#### Task: FL-001
- **title**: Design in-app feedback widget
- **description**: Integrate a lightweight in-app feedback widget (e.g., Survicate or Typeform embedded) accessible from settings and onboarding completion screen. Capture satisfaction rating (1-5 stars) + optional free text. Trigger contextually (after first invoice sent, after first week).
- **inputs**: App design, feedback tool account
- **outputs**: Feedback widget live in app, star rating + text capture
- **dependencies**: [ON-005]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: engineering
- **validation**: Widget visible in test builds, submissions received

#### Task: FL-002
- **title**: Set up NPS survey (day-30 trial users)
- **description**: Configure automated NPS survey sent via email to trial users on day 28-30. Use Mailchimp/Brevo campaign. Track response rate and score distribution. Set up Slack alert for detractors (score ≤ 6).
- **inputs**: Email tool, trial user list, NPS tool
- **outputs**: NPS campaign live, Slack alerts configured
- **dependencies**: [SP-003]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: NPS survey sent to first cohort, responses tracked

#### Task: FL-003
- **title**: Build feedback triage and closed-loop process
- **description**: Define how feedback is triaged: weekly review of all feedback, bugs filed to GitHub, feature requests added to product board. Auto-tag detractors for customer success outreach. Send follow-up email to user when feedback addressed.
- **inputs**: Feedback submissions, triage schedule, product board
- **outputs**: Triage process documented, SLA for follow-up defined
- **dependencies**: [FL-001, FL-002, CS-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Process followed for 3 consecutive weeks

#### Task: FL-004
- **title**: Track feedback-to-product cycle time
- **description**: Measure and report cycle time from feedback submission to shipped fix/feature. Target: critical bugs < 1 week, minor improvements < 1 month. Report monthly in product metrics.
- **inputs**: Feedback log, GitHub issues, product board
- **outputs**: Monthly cycle time report
- **dependencies**: [FL-003]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Report generated for first month post-launch

---

### Category: Feature Flags

#### Task: FF-001
- **title**: Integrate feature flag system (Flagsmith or Unleash)
- **description**: Set up a feature flag provider (Flagsmith self-hosted or Unleash) integrated into the mobile app via SDK. Configure environments: development, staging, production.
- **inputs**: Flagsmith or Unleash account, app codebase
- **outputs**: Feature flag system operational in all environments
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: engineering
- **validation**: Feature flags toggle correctly in test environment

#### Task: FF-002
- **title**: Define flag naming and management conventions
- **description**: Document naming conventions (e.g., feature_area_description), percentage rollouts, user segment targeting. Establish process for creating, reviewing, and removing flags. Prevent flag debt.
- **inputs**: Feature flag system, engineering team
- **outputs**: Flag management guide, GitHub wiki page
- **dependencies**: [FF-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: engineering
- **validation**: Guide reviewed and followed by 2+ engineers

#### Task: FF-003
- **title**: Roll out onboarding improvements behind flags
- **description**: Use feature flags to gradually roll out onboarding flow improvements (e.g., new step, simplified form). Start with 10% of new users, monitor activation rate, expand to 100% if no degradation.
- **inputs**: Onboarding flow improvements, FF-001
- **outputs**: Gradual rollout config, monitoring dashboard
- **dependencies**: [FF-001, ON-005]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: engineering
- **validation**: Flags toggle correctly, no crashes on rollout

#### Task: FF-004
- **title**: Sunset legacy Kanban feature behind flag
- **description**: If Kanban board is not in MVP scope, keep it behind a feature flag. Gradually enable for power users who opted into beta. Monitor engagement before full rollout.
- **inputs**: Kanban feature code, user beta opt-in list
- **dependencies**: [FF-001]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: engineering
- **validation**: Flag behaves correctly for beta user segment

---

### Category: Public Roadmap / Changelog

#### Task: PR-001
- **title**: Design public roadmap page
- **description**: Create a public product roadmap page (accessible at /roadmap on the marketing site) showing In Progress, Planned, and Shipped features organized by category. Use simple Kanban-style board with emoji indicators.
- **inputs**: Product board, marketing site codebase
- **outputs**: Roadmap page live at /roadmap
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: engineering
- **validation**: Roadmap page accessible, readable on mobile

#### Task: PR-002
- **title**: Define changelog publishing process
- **description**: Define how changelog entries are written (brief, user-focused, no jargon) and published. Use a format: "What's new in [App Name] vX.X — [Feature name]: [2-sentence description]." Publish on website and in-app (settings screen).
- **inputs**: Release process, content guidelines
- **outputs**: Changelog template and publishing SOP
- **dependencies**: [PR-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Changelog published for first post-launch release

#### Task: PR-003
- **title**: Build in-app changelog display
- **description**: Show "What's New" banner in-app after update (dismissible). Link to full changelog. Track how many users tap to read more vs. dismiss.
- **inputs**: Changelog entries, in-app notification system
- **outputs**: In-app changelog banner implemented
- **dependencies**: [PR-002, NO-004]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: engineering
- **validation**: Banner displays after first update post-launch

---

### Category: Localization (French UX)

#### Task: FR-001
- **title**: Audit app for French localization readiness
- **description**: Audit the app codebase for hardcoded strings, date formats (DD/MM/YYYY), number formats (comma decimal), currency display (€), and phone number input. Replace all with i18n-compatible resources.
- **inputs**: App codebase, localization framework (i18n)
- **outputs**: All strings externalized, formats localized
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: engineering
- **validation**: App renders correctly with fr-FR locale in simulator

#### Task: FR-002
- **title**: Translate all UI strings to French
- **description**: Translate all app strings to French. Work with native French speaker (not machine translation) for all user-facing copy. Include onboarding, error messages, invoice labels, notification text.
- **inputs**: String resource files, native French translator
- **outputs**: French translation files (fr-FR), reviewed by native speaker
- **dependencies**: [FR-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: localization
- **validation**: All strings translated, no untranslated strings visible

#### Task: FR-003
- **title**: Adapt UX patterns for French market conventions
- **description**: Adapt UX for French expectations: formal "vous" vs informal "tu" (use "vous" throughout), typical French business hours in scheduling UX, French holiday calendar for reminders, appropriate tone (professional but approachable).
- **inputs**: User research insights, French UX conventions guide
- **outputs**: Tone and style guide for French market
- **dependencies**: [UR-002, UR-003]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Reviewed and approved by French artisan advisor

#### Task: FR-004
- **title**: Set up French App Store localization (ASO)
- **description**: Configure French localization in App Store Connect: French app name, subtitle, description, keyword research for French SEO (App Store Optimization). Target top keywords French artisans search.
- **inputs**: App Store Connect access, French ASO keyword research
- **outputs**: French App Store listing configured
- **dependencies**: [FR-001, FR-002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: French listing visible in App Store (FR locale)

---

### Category: Customer Support Setup

#### Task: CS-001
- **title**: Configure support email and help inbox
- **description**: Set up support@ domain email (via Kuroba email config) as the official support channel. Configure inbox rules, canned responses for common questions (billing, reset password, invoice help), and shared team access.
- **inputs**: Kuroba email config, common FAQ list
- **outputs**: Support inbox operational, canned responses configured
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: operations
- **validation**: Test email to support@ receives response within 24h

#### Task: CS-002
- **title**: Build help center / FAQ page
- **description**: Create a help center at /help with articles covering: getting started, adding a client, creating an invoice, payment FAQ, contacting support. Written in French, clear step-by-step instructions with screenshots.
- **inputs**: Help center platform (Ghost, Notion, or custom), FAQ content
- **outputs**: Help center live with 10+ articles
- **dependencies**: [CS-001, ON-005]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: content
- **validation**: Help center accessible, articles findable via search

#### Task: CS-003
- **title**: Define support triage and escalation paths
- **description**: Define support ticket triage: bug reports → GitHub issue filed automatically, billing questions → escalation to admin, feature requests → product board. Set SLA: urgent (data loss) < 4h, normal < 48h, low < 5 days.
- **inputs**: Support inbox, GitHub, product board
- **outputs**: Triage playbook document, SLA definitions
- **dependencies**: [CS-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: operations
- **validation**: Playbook followed for 10 consecutive tickets

#### Task: CS-004
- **title**: Set up in-app "Contact Support" shortcut
- **description**: Add "Contact Support" button in app settings and on error screens, pre-filling context (screen name, OS version, user ID) in the support email subject/body.
- **inputs**: App settings screen, CS-001
- **outputs**: In-app support shortcut implemented
- **dependencies**: [CS-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: engineering
- **validation**: Support email sent from app includes user context

---

### Category: Success Playbooks

#### Task: SP-001
- **title**: Design day-7 trial success email sequence
- **description**: Create automated email sent on day 7 of trial: personalized ("Bonjour [Name], how's your first week going?"), highlights one key feature they haven't tried, includes short tutorial video or screenshot. Goal: drive first meaningful action.
- **inputs**: Email tool, user data (signup date, name), user activation data
- **outputs**: Email sequence live in email platform, targeting logic configured
- **dependencies**: [AT-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Email sends correctly to day-7 trial users, open rate > 40%

#### Task: SP-002
- **title**: Design day-14 trial check-in email
- **description**: Create automated email on day 14: check if user has added clients and sent invoices. If not, offer 15-min onboarding call (Calendly link). If yes, highlight premium features they're close to unlocking.
- **inputs**: Email tool, activation data (AT-002), Calendly link
- **outputs**: Day-14 email live, call booking link functional
- **dependencies**: [SP-001, AT-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Email sends correctly, Calendly bookings tracked

#### Task: SP-003
- **title**: Design day-28 trial conversion email sequence
- **description**: Create day-28 email sequence (3 emails over 3 days): reminder trial expires soon, social proof (artisan testimonials), last-chance offer (annual plan discount). French language, mobile-optimized.
- **inputs**: Email tool, testimonials, pricing page
- **outputs**: 3-email conversion sequence live
- **dependencies**: [SP-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Sequence fires for day-28 users, conversion tracked

#### Task: SP-004
- **title**: Create onboarding call playbook
- **description**: Design a 15-min discovery call script for trial users: open questions about their business, demo the 3 features most relevant to them, close with a specific next-step commitment. Train Gabin to run these calls.
- **inputs**: User research insights, app demo flow
- **outputs**: Call script, slide deck, Gabin trained
- **dependencies**: [UR-002, UR-003]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: sales
- **validation**: Gabin runs 3 practice calls, feedback incorporated

#### Task: SP-005
- **title**: Define churn prevention playbook
- **description**: Define intervention triggers for at-risk users: no login in 7+ days (trial), invoice overdue > 30 days (paid), NPS detractor. Specific outreach actions for each trigger (email, call, discount offer). Document in CS-003.
- **inputs**: Analytics data, CS-003
- **outputs**: Churn playbook document, automation rules in email tool
- **dependencies**: [AT-004, CS-003]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: operations
- **validation**: Playbook triggered for first at-risk user cohort

---

### Category: Error/Empty State Design

#### Task: EE-001
- **title**: Audit all empty states in the app
- **description**: Identify every screen/section in the app that can be empty: no clients, no jobs, no invoices, no notifications, no search results. Document current state (if any) and design requirements.
- **inputs**: App screens inventory, UX wireframes
- **outputs**: Empty state audit spreadsheet with screen names and requirements
- **dependencies**: [MVP-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: All empty states identified and documented

#### Task: EE-002
- **title**: Design empty state illustrations and copy
- **description**: Design friendly, non-generic empty state screens for each empty state identified. Each includes: French headline, 1-sentence explanation, single primary CTA button. Avoid generic stock art — use simple, warm SVG illustrations.
- **inputs**: Empty state audit (EE-001), French copy guidelines
- **outputs**: Empty state designs (Figma), approved copy
- **dependencies**: [EE-001, FR-003]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Designs reviewed by French artisan advisor for warmth

#### Task: EE-003
- **title**: Design error state screens
- **description**: Design error states for: network offline, API timeout, invoice generation failed, payment declined, session expired. Each error: clear headline, human-readable explanation (not technical), retry action, contact support option.
- **inputs**: App error scenarios, design system
- **outputs**: Error state designs (Figma), copy in French
- **dependencies**: [EE-001, FR-003]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: design
- **validation**: Error states tested with 3 users (no confusion on meaning)

#### Task: EE-004
- **title**: Implement and QA all empty/error states
- **description**: Implement all empty state and error state screens in the app. Test each state manually: trigger the empty state, trigger the error, verify copy is correct, verify buttons navigate correctly.
- **inputs**: Empty/error state designs, app codebase
- **outputs**: All states implemented and tested
- **dependencies**: [EE-002, EE-003]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: engineering
- **validation**: Manual QA complete for all states on iOS and Android

---

### Category: App Store Listing

#### Task: AS-001
- **title**: Prepare iOS App Store listing assets
- **description**: Create all required App Store assets: app icon (1024x1024 + all required sizes), screenshots (6.7" and 6.5" for iPhone, 12.9" for iPad), app preview video (30s showcasing onboarding and invoice creation).
- **inputs**: App design, app preview video recorded
- **outputs**: All App Store assets uploaded to App Store Connect
- **dependencies**: [ON-005, IV-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: design
- **validation**: All assets accepted by App Store Connect validation

#### Task: AS-002
- **title**: Write iOS App Store listing copy
- **description**: Write French App Store listing: app name (catchy, searchable), subtitle (key value prop), description (first 3 lines visible without "more", full description with feature bullets), keywords (100 chars, French artisan CRM terms).
- **inputs**: Product positioning, keyword research
- **outputs**: App Store copy in French, keyword list
- **dependencies**: [FR-004, AS-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Copy reviewed by native French speaker, approved by Gabin

#### Task: AS-003
- **title**: Submit iOS app for review (TestFlight beta)
- **description**: Submit app to App Store Connect for TestFlight beta review. Ensure all required metadata, privacy policies, and export compliance are completed. Target 3+ beta testers before public launch.
- **inputs**: App build, App Store Connect account, privacy policy URL
- **outputs**: App in TestFlight beta review
- **dependencies**: [AS-001, AS-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: engineering
- **validation**: App accepted into TestFlight, available to external testers

#### Task: AS-004
- **title**: Prepare and submit Google Play Store listing
- **description**: Create Google Play Store listing: French listing, screenshots (phone + tablet), feature graphic, store listing copy. Use similar copy to iOS but adapted for Google Play conventions.
- **inputs**: App assets, AS-002 copy
- **outputs**: Google Play listing prepared and submitted
- **dependencies**: [AS-001, AS-002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Listing submitted to Google Play, passes review

#### Task: AS-005
- **title**: Set up App Store Optimization (ASO) tracking
- **description**: Configure ASO tracking (AppFollow or similar) to monitor keyword rankings for French artisan CRM terms. Track competitor app rankings. Report weekly for first 3 months post-launch.
- **inputs**: ASO tool, keyword list
- **outputs**: ASO dashboard live, weekly report scheduled
- **dependencies**: [AS-002, AS-003]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: First ASO report received within 30 days of launchmedium
- **agent_type**: product
- **validation**: Cohort definitions agreed with growth team

#### Task: CA-002
- **title**: Build cohort analysis dashboard
- **description**: Implement cohort tracking in analytics: trial_start_date, first_job_created_date, first_invoice_sent_date, upgrade_date, churn_date. Visualize in dashboard: retention curves, time-to-conversion, LTV by cohort.
- **inputs**: CA-001 definitions, analytics system
- **outputs**: Cohort dashboard in admin panel
- **dependencies**: [CA-001]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Cohort data accurate, retention curves visible

#### Task: CA-003
- **title**: Define conversion funnel metrics
- **description**: Define exact conversion funnel: Signup → Email verified → Profile completed → First contact added → First job created → First invoice sent → Trial ended → Converted/Not converted. Set benchmark percentages for each stage.
- **inputs**: Onboarding data, industry benchmarks
- **outputs**: Funnel definition document with target %s
- **dependencies**: [CA-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Funnel tracked accurately, benchmarks documented

---

### Category: A/B Testing Framework

#### Task: AB-001
- **title**: Define A/B testing platform approach
- **description**: Use PostHog feature flags for A/B testing. Define: minimum sample size calculator, statistical significance threshold (95%), test duration limits, decision criteria (win/lose/continue).
- **inputs**: PostHog setup, statistical methods
- **outputs**: A/B testing protocol document
- **dependencies**: [SM-003]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Protocol documented and team trained

#### Task: AB-002
- **title**: Build hypothesis backlog
- **description**: Create backlog of A/B test hypotheses: e.g., "Showing social proof on pricing page will increase trial signups by 15%." Prioritize by potential impact and implementation effort.
- **inputs**: User research, analytics insights
- **outputs**: Hypothesis backlog (at least 20 hypotheses)
- **dependencies**: [AB-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Backlog populated, top 5 prioritized

#### Task: AB-003
- **title**: Run first onboarding A/B test
- **description**: Test: simplified onboarding (3 steps only) vs. full onboarding. Measure: trial signup completion rate, time-to-first-job, day-7 retention.
- **inputs**: AB-002 hypothesis, frontend capability
- **outputs**: First A/B test results
- **dependencies**: [AB-002, ONB-003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Statistical significance reached, decision made

---

### Category: Community Building

#### Task: COM-001
- **title**: Research French artisan Facebook groups
- **description**: Find active Facebook groups for French artisans: "Artisans du BTP," "Plombiers de France," regional groups. Understand: group size, engagement level, moderator policies on promotion.
- **inputs**: Facebook search
- **outputs**: List of 20+ relevant Facebook groups
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Group list complete with engagement metrics

#### Task: COM-002
- **title**: Create WhatsApp community for trial users
- **description**: Set up WhatsApp group/channel for trial users: share tips, gather feedback, build community. Moderate actively. Start with beta users, expand to all trial users at day 7.
- **inputs**: COM-001 research
- **outputs**: WhatsApp community live with first members
- **dependencies**: [COM-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: 20+ members in first month, 50%+ monthly active

#### Task: COM-003
- **title**: Create ambassador program draft
- **description**: Design informal ambassador program: identify most engaged users, offer: early access to features, eternal discount (10% lifetime), direct access to founders. Formalize via email outreach.
- **inputs**: COM-002 engagement data
- **outputs**: Ambassador program with first 5 ambassadors
- **dependencies**: [COM-002]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: At least 5 ambassadors recruited

---

### Category: Competitor Response

#### Task: CR-001
- **title**: Build competitive monitoring system
- **description**: Set up Google Alerts for competitor names, use SerpAPI to monitor competitor pricing changes, new feature announcements. Review bi-weekly.
- **inputs**: Competitor list (from market analysis)
- **outputs**: Google Alert setup, monitoring calendar
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Alerts active, bi-weekly review scheduled

#### Task: CR-002
- **title**: Define competitor response playbooks
- **description**: For each competitor action (price cut, new feature launch, marketing campaign): define response options (ignore/mirror/ differentiate), decision criteria, approval required (Louis/Gabin decision).
- **inputs**: CR-001 monitoring data
- **outputs**: Response playbook document
- **dependencies**: [CR-001]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Playbook reviewed and approved

---

### Category: Seasonal Campaign Calendar

#### Task: SC-001
- **title**: Build annual campaign calendar
- **description**: Map French artisan seasonal patterns: winter (heating/emergency plumbing), spring (renovations), summer (lighter workload), autumn (pre-winter checks). Plan campaigns around: low season (drive trials), high season (drive upgrades).
- **inputs**: Industry seasonal data
- **outputs**: Annual campaign calendar with themes
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Calendar covers full year with objectives per campaign

#### Task: SC-002
- **title**: Create winter emergency campaign (November-February)
- **description**: "Votre chauffage tombe en panne, on gère vos devis" campaign: target heating engineers, boiler repair services. Push free trial of job management for emergency response teams.
- **inputs**: SC-001 calendar
- **outputs**: Winter campaign plan
- **dependencies**: [SC-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Campaign live by November 1

#### Task: SC-003
- **title**: Create spring renovation campaign (March-May)
- **description**: "Gérez vos chantiers de rénovation" campaign: target all artisan types, renovation project focus. Push trial with focus on project management features.
- **inputs**: SC-001 calendar
- **outputs**: Spring campaign plan
- **dependencies**: [SC-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Campaign live by March 1

---

### Category: Upsell Triggers

#### Task: UT-001
- **title**: Define upgrade trigger events
- **description**: Identify behaviors that signal upgrade readiness: >5 active clients, >3 jobs/month, >2 team members added. Implement trigger detection in analytics.
- **inputs**: User behavior data
- **outputs**: Upgrade trigger event definitions
- **dependencies**: [SM-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Triggers defined and tested

#### Task: UT-002
- **title**: Build in-app upgrade prompts
- **description**: When upgrade trigger fires, show contextual upgrade prompt in app (not intrusive modal): "Vous gérez plus de 5 clients — le plan Pro vous permet de gérer votre équipe." Link to pricing page.
- **inputs**: UT-001 triggers, app UI
- **outputs**: Upgrade prompts in app
- **dependencies**: [UT-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Prompt shown at correct trigger points, upgrade rate >5%

#### Task: UT-003
- **title**: Create annual plan discount campaign
- **description**: Offer annual plan at 2 months free (17% discount). Target: users about to churn, users on month-to-month for 3+ months. Email campaign with limited-time offer (30 days).
- **inputs**: UT-001 trigger data
- **outputs**: Annual plan campaign with 30-day CTA
- **dependencies**: [UT-002]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Campaign conversion rate >10%

---

## Orchestrator TODO (Product)

### MVP — Must Have
- [ ] ONB-001: Simplified onboarding (max 5 steps to first job)
- [ ] ONB-002: Email sequence (3-email drip)
- [ ] ONB-003: Onboarding checklist UI
- [ ] ONB-004: In-app guidance tooltips
- [ ] ONB-005: First-job-in-5-minutes guarantee
- [ ] DSH-001: Dashboard home screen with timeline view
- [ ] DSH-002: Quick action buttons
- [ ] DSH-003: Dashboard KPIs
- [ ] DSH-004: Notification center
- [ ] ERR-001, ERR-002, ERR-003: Error/empty states
- [ ] SM-001: Analytics tracking plan
- [ ] SM-002: PostHog onboarding
- [ ] SM-003: Key events tracked

### Post-Launch — Month 1-3
- [ ] FB-001: In-app feedback widget
- [ ] FF-001, FF-002: Feature flag system
- [ ] FF-003: Beta program setup
- [ ] CA-001, CA-002, CA-003: Cohort analysis
- [ ] AB-001, AB-002, AB-003: A/B testing framework
- [ ] COM-001, COM-002, COM-003: Community building
- [ ] UT-001, UT-002, UT-003: Upsell triggers
- [ ] SC-001, SC-002, SC-003: Seasonal campaigns

### Later — Month 4+
- [ ] LP-001, LP-002, LP-003: Landing page for paid acquisition
- [ ] AS-001, AS-002, AS-003, AS-004: App Store presence
- [ ] RC-001: Public changelog/roadmap page
- [ ] CR-001, CR-002: Competitive monitoring
- [ ] COM-003: Ambassador program

---

*Product Roadmap — Mini-CRM for French Artisans*
*Last updated: 2026-03-30*
