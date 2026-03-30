# Growth Roadmap — Mini-CRM

## Objectives

1. Increase trial-to-paid conversion rate from current baseline to 25%+ within 12 months
2. Reduce average time-to-first-job from onboarding completion to <48 hours
3. Decrease monthly churn rate to <5% for all tiers
4. Increase average revenue per user (ARPU) by 40% through upgrade pathways
5. Build sustainable referral loop achieving 15% of new customers from referrals
6. Establish Mini-CRM as the dominant CRM for French artisans (5,000+ paying customers)
7. Maximize customer LTV across all tiers with targeted engagement programs
8. Create defensible moat through community and network effects

## Subdomains

- **Activation & Onboarding**: Get artisans to first value moment quickly
- **Monetization**: Optimize pricing, packaging, and upgrade triggers
- **Retention**: Prevent churn through predictive interventions
- **Expansion**: Drive upgrades and LTV growth
- **Acquisition**: Leverage viral and referral loops
- **Insights**: Build data infrastructure for decision-making
- **Community**: Build artisan network effects
- **Market Intelligence**: Monitor competitors and market trends

## Milestones

### Q1: Foundation
- Complete cohort analysis infrastructure
- Launch NPS program with monthly reporting
- A/B testing framework operational
- Baseline metrics established for all key funnels

### Q2: Activation Excellence
- Time-to-first-job reduced to <48 hours for 80% of trials
- Onboarding flow redesigned based on activation research
- In-app guidance system implemented
- Activation email sequence fully deployed

### Q3: Monetization & Retention
- Churn prediction model deployed
- Upgrade path optimization complete
- Win-back campaign system live
- Pricing psychology tests completed

### Q4: Scale & Community
- Referral program achieving 15% of acquisitions
- Artisan community hubs established
- Seasonal campaign calendar fully operational
- Competitor response playbook automated

## Task Categories

---

### Category: Trial-to-Paid Conversion Optimization

#### Task: TRC-001
- **title**: Audit current trial-to-paid conversion funnel
- **description**: Analyze the complete trial user journey from signup to conversion or churn. Map all touchpoints, identify drop-off points, measure current conversion rate by cohort, tier, and traffic source. Document findings in a conversion audit report.
- **inputs**: Analytics data, trial user flow data, CRM logs
- **outputs**: Conversion audit report with drop-off map, quantified conversion rates by segment
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Report produced with actionable insights documented

#### Task: TRC-002
- **title**: Implement trial expiry warning sequence
- **description**: Create a 5-email warning sequence starting 14 days before trial expiry, then 7 days, 3 days, 1 day, and on expiry day. Each email must emphasize value created during trial, not fear of losing access. Include clear CTA to subscribe.
- **inputs**: Trial user data, email templates, ESP configuration
- **outputs**: Live email sequence in ESP, configured in automation
- **dependencies**: TRC-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Emails firing correctly, open rates >40% for day-1 email

#### Task: TRC-003
- **title**: Design paywall that drives upgrades without frustrating users
- **description**: Create a contextual paywall system that appears when users attempt to use premium features. The paywall should highlight the value of the feature they're trying to use, show social proof (e.g., "500 artisans use this feature"), and present a clear upgrade path. Must NOT block core job management features.
- **inputs**: Feature usage data, current paywall implementations, user feedback
- **outputs**: Redesigned contextual paywall UI and logic
- **dependencies**: TRC-001
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: product
- **validation**: Paywall live, upgrade conversion rate from paywall view >3%

#### Task: TRC-004
- **title**: Create urgency-based conversion messaging
- **description**: Develop conversion messaging framework using urgency triggers: limited-time pricing locks, "X spots remaining" for annual plans, seasonal discounts tied to renovation season. Test each message variant for conversion lift.
- **inputs**: Pricing data, seasonal calendar, conversion copy
- **outputs**: Library of urgency messaging variants with performance data
- **dependencies**: TRC-001
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Urgency messages live in product, measurable conversion lift documented

#### Task: TRC-005
- **title**: Optimize trial start page for commitment
- **description**: Redesign the post-signup "getting started" page to immediately engage users with a mini-tutorial and first-job creation prompt. Remove distractions, add progress indicators, and celebrate small wins. Test against current page with A/B test.
- **inputs**: Current onboarding page analytics, user feedback, design assets
- **outputs**: Redesigned start page, A/B test results after 2 weeks
- **dependencies**: TRC-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: A/B test shows >15% improvement in trial completion rate

#### Task: TRC-006
- **title**: Implement in-trial usage scoring system
- **description**: Build a scoring model that predicts conversion likelihood based on in-trial behavior (feature usage, sessions, jobs created, settings completed). Score updates daily. Use scores to trigger targeted interventions for low-scoring trials.
- **inputs**: User behavior data, conversion outcomes
- **outputs**: Live usage scoring system, daily score updates for all trials
- **dependencies**: TRC-001, TRC-002
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: growth
- **validation**: Scoring model deployed, intervention triggers working

#### Task: TRC-007
- **title**: Create conversion-focused help content
- **description**: Identify the top 10 objections users have before converting (from exit surveys and sales calls). Create targeted help content that addresses each objection with value-focused messaging. Publish as a guide accessible during trial.
- **inputs**: Exit survey data, sales call recordings, objection list
- **outputs**: 10-piece help content series, integrated into trial experience
- **dependencies**: TRC-001
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Content published and linked from trial dashboard

#### Task: TRC-008
- **title**: Deploy live chat for trials in critical window
- **description**: Add live chat (Crisp or similar) with proactive trigger when trial user visits pricing page during last 7 days of trial. Chat script should address common objections and offer 1-on-1 demo scheduling.
- **inputs**: Chat tool integration, trigger rules, chat scripts
- **outputs**: Live chat deployed, chat transcripts being logged
- **dependencies**: TRC-001
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Chat triggers correctly, >10% of triggered trials engage with chat

#### Task: TRC-009
- **title**: A/B test trial length variations (14 vs 21 vs 30 days)
- **description**: Run a controlled experiment testing three trial lengths to identify optimal duration for conversion. Segment by traffic source and tier intent. Measure 30-day conversion rate and revenue per trial.
- **inputs**: Current trial data, A/B testing infrastructure
- **outputs**: Statistical results on trial length impact by segment
- **dependencies**: TRC-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Test complete, optimal trial length determined with 95% confidence

#### Task: TRC-010
- **title**: Build trial-to-paid email retargeting for website visitors
- **description**: Install pixel tracking on pricing page. Create retargeting audiences for users who visited pricing but didn't convert. Deploy Facebook/Google retargeting ads with social proof and value prop messaging. Exclude converted users.
- **inputs**: Pixel integration, ad creative, retargeting platform access
- **outputs**: Retargeting campaigns live, conversion tracking configured
- **dependencies**: TRC-001
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Retargeting campaigns active, measurable ROAS >3x

#### Task: TRC-011
- **title**: Implement sales pipeline for high-intent trials
- **description**: Define criteria for "high-intent" trials (visited pricing 3+ times, used 80%+ of trial features, requested demo). Route these trials to a human sales follow-up via email sequence offering 1-on-1 call. Track conversion rate and revenue.
- **inputs**: Usage data, email sequences, sales script
- **outputs**: Automated handoff to sales, CRM pipeline for trials
- **dependencies**: TRC-006
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Sales pipeline active, conversion rate from human outreach >20%

#### Task: TRC-012
- **title**: Create social proof notifications in product
- **description**: Implement in-app notifications showing real-time social proof: "Jean-Pierre from Lyon just created his 50th job" or "A plumber in Marseille upgraded to Pro today." Trigger during moments of low engagement to re-activate interest.
- **inputs**: Real user data (anonymized), notification system, trigger rules
- **outputs**: Social proof notification system live
- **dependencies**: TRC-003
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Notifications displaying correctly, measurable engagement lift

#### Task: TRC-013
- **title**: Test limited-time annual discount offers
- **description**: During trial period, offer a limited-time annual plan discount (e.g., 2 months free). Create urgency via countdown timer. Measure annual vs monthly conversion split and LTV impact.
- **inputs**: Pricing structure, discount percentages, countdown timer implementation
- **outputs**: Annual offer live, conversion data by plan type
- **dependencies**: TRC-004
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Annual uptake rate >30% of paid conversions

#### Task: TRC-014
- **title**: Optimize credit card form for frictionless checkout
- **description**: Audit current checkout flow. Reduce form fields to absolute minimum. Add Apple Pay / Google Pay buttons. Auto-fill where possible. Test single-page vs multi-page checkout. Target checkout completion rate >85%.
- **inputs**: Current checkout flow, payment provider docs, UX audit
- **outputs**: Streamlined checkout, A/B test results
- **dependencies**: TRC-003
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Checkout completion rate >85%, measured over 500 attempts

#### Task: TRC-015
- **title**: Implement value reminder dashboard widget
- **description**: Create a persistent dashboard widget showing trial users their "value created" — number of jobs managed, clients tracked, invoices sent. Update in real-time. Position near upgrade CTA. Make it emotionally engaging ("Your business runs smoother with Mini-CRM").
- **inputs**: User activity data, dashboard design specs
- **outputs**: Value reminder widget live in dashboard
- **dependencies**: TRC-005
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Widget live, users who view it convert at higher rate

#### Task: TRC-016
- **title**: Build objection handling knowledge base
- **description**: Create internal knowledge base of top 20 trial objections with scripted responses for chat, email, and phone. Include pricing objections, feature missing objections, and "need to think" objections. Train support team.
- **inputs**: Sales call recordings, support tickets, objection list
- **outputs**: Knowledge base, support team trained, objection handling scripts
- **dependencies**: TRC-001
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: KB live, support team certified, objection resolution rate improved

#### Task: TRC-017
- **title**: Deploy exit intent survey for trial non-converts
- **description**: When a trial user shows exit intent (mouse moving to close tab), trigger a micro-survey: "What's preventing you from subscribing?" with 4 quick options. Capture response, then show targeted offer based on answer.
- **inputs**: Exit intent tool, survey questions, offer variants
- **outputs**: Exit intent survey active, data being collected
- **dependencies**: TRC-001
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Survey capturing >500 responses, top objections identified

#### Task: TRC-018
- **title**: Create comparison landing page vs competitors
- **description**: Build a dedicated landing page comparing Mini-CRM against direct competitors (HubSpot, Zoho, etc.) specifically for artisan trades. Highlight simplicity, French market focus, and value. Target keywords for comparison searches.
- **inputs**: Competitor feature data, SEO keyword research, design templates
- **outputs**: Live comparison page, SEO ranking for target keywords
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Page live, organic traffic to page, measurable trial conversions from page

#### Task: TRC-019
- **title**: Test money-back guarantee offer
- **description**: Create a 30-day money-back guarantee offer for annual subscribers. Test if guarantee increases conversion rate vs no-guarantee control. Measure refund rate and overall impact on conversion and retention.
- **inputs**: Refund policy draft, checkout integration, test setup
- **outputs**: Guarantee offer live, refund rate measured
- **dependencies**: TRC-014
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Conversion lift measurable, refund rate <10%

#### Task: TRC-020
- **title**: Implement concierge onboarding for high-value trials
- **description**: For trials with high usage scores (TRC-006) who haven't converted by day 20, offer a 15-minute personalized onboarding call. Goal is to answer questions and demonstrate value. Track conversion rate of called trials vs control.
- **inputs**: High-intent trial list, sales calendar, call script
- **outputs**: Concierge program active, conversion data collected
- **dependencies**: TRC-006
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Calls booked within 48h of trigger, call-to-paid rate >40%

#### Task: TRC-021
- **title**: Create trial extension offer for near-converters
- **description**: Develop a process to offer 7-day trial extensions to trials who engaged significantly but didn't convert. Criteria: visited pricing page, used 50%+ features, but no credit card entered. Test if extension improves final conversion.
- **inputs**: Extension criteria, email sequence, offer mechanics
- **outputs**: Extension offer system, extension-to-paid conversion tracked
- **dependencies**: TRC-006, TRC-017
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Extension offer deployed, lift in final conversion measured

#### Task: TRC-022
- **title**: Build trust signals throughout trial experience
- **description**: Add visible trust signals during trial: security badges, "Data encrypted" indicators, customer count ("Trusted by 2,000+ artisans"), media mentions, certifications. Place on signup page, dashboard, and checkout.
- **inputs**: Trust asset library, badge designs, legal disclaimers
- **outputs**: Trust signals installed across all key pages
- **dependencies**: []
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Trust signals visible, conversion lift from trust signals measurable

#### Task: TRC-023
- **title**: Test pricing page layout optimization
- **description**: A/B test different pricing page layouts: 3-column vs 2-column, recommended plan highlighted vs not, price shown with/without annual toggle visible by default. Measure plan selection rate and overall conversion.
- **inputs**: Current pricing page, A/B test framework, traffic levels
- **outputs**: A/B test results with statistical significance
- **dependencies**: TRC-001
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Winning layout implemented, >10% conversion lift

#### Task: TRC-024
- **title**: Implement scarcity messaging for annual plan
- **description**: Create limited-quantity messaging for annual plan ("Only 50 annual plans available at this price — X remaining"). Rotate monthly. Track impact on annual plan uptake and conversion timing.
- **inputs**: Inventory system (or simulated scarcity), messaging templates
- **outputs**: Scarcity messaging live, conversion timing data
- **dependencies**: TRC-004
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Annual plan uptake increased measurably

#### Task: TRC-025
- **title**: Create post-trial grace period conversion sequence
- **description**: For trials that expire without converting, implement a 7-day grace period where they can still access read-only data. During this period, send a targeted 3-email sequence emphasizing data preservation anxiety and easy path back.
- **inputs**: Expired trial data, email sequences, access level logic
- **outputs**: Grace period system live, email sequence deployed
- **dependencies**: TRC-002
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Grace period conversions measurable, >5% win-back during grace

---

### Category: Activation Rate Optimization (time to first job created)

#### Task: ACT-001
- **title**: Map and measure current activation funnel
- **description**: Track the complete user journey from signup to first job creation. Identify average time, drop-off points, and common blockers. Set baseline metric: "X% of users create first job within 24h". Segment by traffic source, profession, and company size.
- **inputs**: User signup data, feature usage events, job creation timestamps
- **outputs**: Activation funnel report with time-to-first-job metrics by segment
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Baseline established, funnel bottlenecks identified

#### Task: ACT-002
- **title**: Redesign onboarding checklist for immediate activation
- **description**: Create a prominent onboarding checklist that guides users through: (1) Create your profile, (2) Add your first client, (3) Create your first job, (4) Invite a team member (optional). Checklist must be visible on dashboard until completed. Celebrate completion.
- **inputs**: Current onboarding flow, checklist component, celebration animations
- **outputs**: Onboarding checklist widget live
- **dependencies**: ACT-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Checklist completion rate >70%, time-to-first-job reduced by 50%

#### Task: ACT-003
- **title**: Implement progressive onboarding with role detection
- **description**: During signup, ask user to select their trade (plumber, electrician, carpenter, etc.) and company size. Use this to customize the onboarding experience — relevant templates, relevant feature highlights, and relevant example content for their specific trade.
- **inputs**: Signup form, role selection data, customized content library
- **outputs**: Role-detected onboarding flow live
- **dependencies**: ACT-002
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: product
- **validation**: Relevant onboarding shows higher completion rate vs generic flow

#### Task: ACT-004
- **title**: Create pre-filled sample data for first job
- **description**: After profile setup, offer to pre-fill sample job data so users can see the product "live" immediately. "Start with a sample plumbing repair job" vs "Start from scratch." Let users choose. Measure which path leads to faster second job creation.
- **inputs**: Sample data templates per trade, choice UI
- **outputs**: Sample data feature live, completion rates measured
- **dependencies**: ACT-003
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Users with sample data create real jobs faster

#### Task: ACT-005
- **title**: Build in-app guided tour for first job creation
- **description**: Create an interactive tour that walks users through job creation step-by-step on their first attempt. Tour highlights key fields, shows tooltips, and celebrates completion. Triggered on first job creation attempt, not on signup.
- **inputs**: Tour tool integration, step-by-step content, tooltip library
- **outputs**: Guided tour live, completion rate measured
- **dependencies**: ACT-004
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: First job completion rate >85% with tour vs without

#### Task: ACT-006
- **title**: Implement onboarding email sequence (7-day sprint)
- **description**: Create a 7-email sequence delivered over the first week: Day 0 (welcome + quick win), Day 1 (profile setup reminder), Day 2 (first job tutorial), Day 3 (social proof story), Day 4 (tip/feature highlight), Day 5 (common question answered), Day 7 (upgrade nudge if high engagement).
- **inputs**: Email templates, ESP automation, user onboarding status
- **outputs**: Email sequence live, open and click rates tracked
- **dependencies**: ACT-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Email sequence deployed, day-7 activation rate improved

#### Task: ACT-007
- **title**: Add push notifications for onboarding milestones
- **description**: Implement browser/app push notifications that fire at key activation milestones: "You created your profile! 1/4 steps complete." "Add your first client to unlock automatic reminders." Time notifications to morning hours when artisans typically check phones.
- **inputs**: Push notification tool, milestone triggers, notification copy
- **outputs**: Push notifications active, opt-in rate and engagement measured
- **dependencies**: ACT-002
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Push-enabled users activate faster

#### Task: ACT-008
- **title**: Create video tutorial series for each artisan trade
- **description**: Produce 3 short videos (2-3 min each) specifically for plumbers, electricians, and carpenters showing real-world Mini-CRM usage. Include common scenarios: emergency call management, quote follow-up, client anniversary reminders. Host on YouTube, embed in onboarding.
- **inputs**: Script outlines, video production, trade-specific scenarios
- **outputs**: 3 videos live on YouTube, embedded in onboarding
- **dependencies**: ACT-003
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: marketing
- **validation**: Videos produced, engagement and activation impact measured

#### Task: ACT-009
- **title**: Implement instant value milestones with rewards
- **description**: Create a micro-reward system: when user creates first job → "Job Creator" badge. First 5 jobs → "Productive Week" badge. First client added → "Client Collector" badge. Badges display on profile, unlocking optional cosmetic rewards (color themes, etc).
- **inputs**: Gamification engine, badge assets, reward catalog
- **outputs**: Badge system live, engagement metrics tracked
- **dependencies**: ACT-005
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Badge earners activate subsequent features at higher rate

#### Task: ACT-010
- **title**: Optimize mobile onboarding experience
- **description**: Many artisans will onboard on mobile. Audit mobile onboarding flow for friction. Ensure all forms are mobile-friendly, key CTAs are thumb-accessible, and the experience doesn't require desktop. Test on iOS and Android.
- **inputs**: Mobile UX audit, device testing, form optimization
- **outputs**: Mobile onboarding optimized, mobile activation rate measured
- **dependencies**: ACT-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Mobile activation rate parity with desktop achieved

#### Task: ACT-011
- **title**: Build "quick wins" sidebar in dashboard
- **description**: Add a persistent sidebar showing 3 immediate actions to complete. Updates based on onboarding progress. Each quick win is <2 min to complete. Gamifies early engagement. Remove sidebar once onboarding complete.
- **inputs**: Dashboard design, quick win action library, progress logic
- **outputs**: Quick wins sidebar live
- **dependencies**: ACT-002
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Sidebar click rate >40%, time-to-activation reduced

#### Task: ACT-012
- **title**: Create FAQ specific to onboarding blockers
- **description**: Analyze top support tickets related to onboarding. Create dedicated FAQ section addressing: "How do I add my first client?", "What fields are required for a job?", "Can I import existing clients?". Target these FAQs at the exact moments users encounter blockers.
- **inputs**: Support ticket analysis, FAQ content, context-aware help
- **outputs**: Onboarding FAQ live, help article views tracked
- **dependencies**: ACT-001
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: FAQ live, support ticket volume for onboarding issues reduced 30%

#### Task: ACT-013
- **title**: Implement in-app messaging support during onboarding
- **description**: Add a chat widget accessible from onboarding screens. Users can ask questions and get real-time answers. Messages route to support team. Track questions asked to identify remaining onboarding friction.
- **inputs**: Chat tool, routing rules, support team availability
- **outputs**: Chat available during onboarding, question themes analyzed
- **dependencies**: ACT-002
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Chat available on all onboarding screens, question volume analyzed

#### Task: ACT-014
- **title**: A/B test single-field vs multi-field signup forms
- **description**: Test reducing signup form to just email + password (everything else on next step). Current form has many fields. Measure signup rate and activation rate separately. Ensure reducing fields doesn't hurt activation quality.
- **inputs**: Current signup form, split test setup, signup and activation data
- **outputs**: Test results showing impact on signup rate and activation rate
- **dependencies**: ACT-001
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Statistical results available, form optimized

#### Task: ACT-015
- **title**: Create SMS onboarding sequence for France market
- **description**: French artisans respond well to SMS. Implement opt-in SMS sequence: Day 1 (welcome + link to mobile app), Day 2 (quick tip), Day 3 (reminder to complete onboarding). Include French-language messages with clear CTAs.
- **inputs**: SMS provider, French copy, opt-in mechanism
- **outputs**: SMS sequence live, opt-in rate and activation impact measured
- **dependencies**: ACT-006
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: SMS open rate >90%, activation lift measurable

#### Task: ACT-016
- **title**: Implement one-click social proof imports
- **description**: Allow users to import contacts from phone via one-click permission (iOS contacts API, Android permissions). Pre-fill client list from existing phone contacts. Reduces data entry friction. Measure impact on time-to-first-client.
- **inputs**: Contact import APIs, permission UI, import flow
- **outputs**: Contact import feature live
- **dependencies**: ACT-004
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: product
- **validation**: Import feature used by >30% of new users, time-to-first-client reduced

#### Task: ACT-017
- **title**: Build template library per trade
- **description**: Create pre-built job templates for each trade: "Bathroom Renovation" for plumbers, "Electrical Rewiring" for electricians, "Kitchen Installation" for carpenters. Templates pre-fill common fields. Users can customize or start from scratch.
- **inputs**: Template research per trade, template data structure, UI
- **outputs**: Template library with 10+ templates per trade
- **dependencies**: ACT-003
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Templates used by >50% of activation, time-to-first-job <24h

#### Task: ACT-018
- **title**: Monitor activation cohort weekly
- **description**: Set up weekly dashboard showing activation rate by cohort. Track week-over-week trends. Create alert if activation drops >10% from baseline. Identify which changes caused drops or improvements.
- **inputs**: Analytics setup, cohort definitions, dashboard tool
- **outputs**: Weekly cohort report, alert system configured
- **dependencies**: ACT-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Dashboard live, weekly reviews happening

#### Task: ACT-019
- **title**: Create success-based onboarding triggers
- **description**: Instead of time-based sequences, trigger next onboarding step only when previous step completed. If user completed profile → show "Add first client" prompt. If client added → show "Create your first job" prompt. Personalized to their pace.
- **inputs**: Event tracking, trigger logic, personalized messaging
- **outputs**: Success-triggered onboarding flow live
- **dependencies**: ACT-002
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: product
- **validation**: Triggered onboarding shows higher completion rate than time-based

#### Task: ACT-020
- **title**: Implement "ask a peer" community widget
- **description**: During onboarding, show a widget: "Stuck? Ask a peer." Connect new users with experienced Mini-CRM users (mentors) via chat. Artisans trust other artisans. Measure if peer support accelerates activation vs standard support.
- **inputs**: Mentor roster, chat tool, matching logic
- **outputs**: Peer support widget live
- **dependencies**: ACT-002
- **priority**: low
- **estimated_complexity**: high
- **agent_type**: growth
- **validation**: Peer connections made, activation lift from peer support measurable

---

### Category: Churn Prediction & Prevention

#### Task: CHR-001
- **title**: Define churn risk signals and scoring model
- **description**: Identify behavioral signals that predict churn: declining weekly logins, no jobs created in 14+ days, support tickets filed, NPS score dropped, payment method failed. Build a composite churn risk score (0-100) updated daily per customer.
- **inputs**: Historical churn data, behavioral data, scoring methodology
- **outputs**: Churn prediction model with documented risk thresholds
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: growth
- **validation**: Model deployed, risk scores updating daily

#### Task: CHR-002
- **title**: Implement early warning alert system
- **description**: When a customer hits churn risk threshold (score >70), trigger internal alert to customer success team. Include customer's usage data, risk factors, and recommended action. Review alerts daily.
- **inputs**: Churn model output, alert system, CS team workflow
- **outputs**: Alert system live, daily alert review process established
- **dependencies**: CHR-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Alerts firing correctly, CS team responding within 24h

#### Task: CHR-003
- **title**: Create re-engagement email sequence for at-risk users
- **description**: Design a 4-email re-engagement sequence triggered when churn score crosses threshold: (1) "We noticed you haven't logged in lately" — empathetic, not salesy, (2) "Here are 3 features you haven't tried", (3) "A client success story from someone like you", (4) "Is there something we can fix?" with survey link.
- **inputs**: At-risk user list, email creative, ESP automation
- **outputs**: Re-engagement sequence live, engagement lift measured
- **dependencies**: CHR-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Sequence deploys for at-risk users, re-engagement rate >20%

#### Task: CHR-004
- **title**: Build win-back offer mechanics for churned users
- **description**: Define concrete win-back offers: 50% off next 3 months, free upgrade to higher tier for 1 month, extended free trial for new features. Test each offer's effectiveness and cost. Create eligibility criteria.
- **inputs**: Churn history, offer成本s, competitive analysis
- **outputs**: Win-back offer framework with performance data
- **dependencies**: CHR-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Offers tested, best-performing offer identified

#### Task: CHR-005
- **title**: Implement cancellation flow with retention offers
- **description**: When user initiates cancellation, interrupt flow with retention offer screen: "Before you go — would a 30% discount for 3 months change your mind?" Test different discount levels and offers. Record which offers prevent cancellation.
- **inputs**: Cancellation flow, retention offer variants, tracking
- **outputs**: Retention offer screen live, offer effectiveness measured
- **dependencies**: CHR-004
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Cancellation-to-retention rate >15%, best offer identified

#### Task: CHR-006
- **title**: Create customer health score dashboard for CS team
- **description**: Build internal dashboard for customer success showing all customers sorted by health score. Include: days since last login, jobs this month, support tickets open, plan tier, MRR. Allow CS to filter, sort, and take action.
- **inputs**: Data pipeline, dashboard tool, CS team input
- **outputs**: CS health dashboard live and in daily use
- **dependencies**: CHR-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Dashboard used daily by CS team, churn rate impacted

#### Task: CHR-007
- **title**: Analyze churned customers by cohort and segment
- **description**: Conduct deep analysis of churned customers: by signup month, by profession, by plan tier, by traffic source, by activation speed. Identify which segments have highest churn. Create segment-specific prevention strategies.
- **inputs**: Churned customer data, cohort analysis tool
- **outputs**: Churn analysis report with segment-level insights
- **dependencies**: CHR-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Report produced, segment-specific strategies developed

#### Task: CHR-008
- **title**: Implement payment failure retry logic
- **description**: Build smart retry logic for failed payments: retry on days 1, 3, 7, 14. Send email before each retry. If final retry fails, trigger customer success outreach before cancellation. Reduce churn from payment failures to <2%.
- **inputs**: Payment retry rules, email templates, CS workflow
- **outputs**: Retry logic deployed, payment failure churn reduced
- **dependencies**: CHR-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Failed payment recovery rate >80%, payment-related churn <2%

#### Task: CHR-009
- **title**: Create competitor defense messaging
- **description**: When a customer shows signs of considering competitor (visits comparison pages, contacts support with competitor questions), trigger targeted messaging: "Here's why 500 artisans chose Mini-CRM over [competitor]." Address specific competitor concerns.
- **inputs**: Competitor intel, objection data, trigger logic
- **outputs**: Competitor defense messaging deployed
- **dependencies**: CHR-001
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Defense triggers working, competitor-switching reduced

#### Task: CHR-010
- **title**: Build voluntary vs involuntary churn classification
- **description**: Classify all churn as voluntary (user主动取消) or involuntary (payment failure, email bounce). Track separately. Focus retention efforts on voluntary churn.
- **inputs**: Churn classification data, payment failure data, cancellation data
- **outputs**: Churn classification dashboard, involuntary churn rate tracked
- **dependencies**: CHR-001
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Classification accurate, involuntary churn tracked separately

#### Task: CHR-011
- **title**: Implement 30-day check-in survey for new customers
- **description**: Send a short survey 30 days after signup asking: "How's it going? Any features not meeting expectations?" Use responses to identify customers at risk of early churn. Route high-risk responses to CS for outreach.
- **inputs**: Survey tool, survey questions, routing logic
- **outputs**: 30-day survey live, response analysis
- **dependencies**: CHR-001
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Survey deployed, at-risk customers identified and contacted

#### Task: CHR-012
- **title**: Build annual subscriber VIP retention program
- **description**: Create a special program for annual subscribers: dedicated support line, early access to features, quarterly check-in call, anniversary discount offer at renewal. Goal: reduce annual churn to <15%.
- **inputs**: VIP program design, support escalation path, renewal data
- **outputs**: VIP program launched, annual retention rate tracked
- **dependencies**: CHR-001
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: VIP program active, annual churn rate for VIPs <15%

#### Task: CHR-013
- **title**: Create usage decline triggers with automated outreach
- **description**: If a customer's weekly active usage drops >50% compared to their first 4 weeks, automatically trigger: (1) in-app notification, (2) email with re-engagement tips, (3) flag for CS team if drop persists 2+ weeks.
- **inputs**: Usage tracking, trigger logic, automated outreach tools
- **outputs**: Usage decline alerts live
- **dependencies**: CHR-001, CHR-002
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Alerts firing, at-risk users re-engaging at higher rate

#### Task: CHR-014
- **title**: Analyze seasonal churn patterns
- **description**: Study churn by month/season to identify patterns specific to artisan trades (e.g., January downturn after holiday spending, summer slowdowns). Build seasonal churn forecasts. Pre-emptively launch seasonal campaigns.
- **inputs**: Historical churn data, seasonal calendar, artisan industry data
- **outputs**: Seasonal churn report with predictions
- **dependencies**: CHR-007
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Seasonal patterns identified, proactive campaigns launched

#### Task: CHR-015
- **title**: Implement customer advisory calls for high-value accounts
- **description**: For top 50 customers by MRR, schedule quarterly advisory calls. Goal: relationship building, early warning of issues, product feedback. Track retention rate of called accounts vs control.
- **inputs**: Customer list, call script, CS calendar
- **outputs**: Advisory call program active
- **dependencies**: CHR-006
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Quarterly calls happening, retention lift measurable

---

### Category: Upgrade Path (Solo → Pro → Business)

#### Task: UPG-001
- **title**: Define clear feature gates between tiers
- **description**: Audit current feature distribution across Solo/Pro/Business tiers. Ensure each tier has distinct, compelling value. Feature gates should feel natural, not arbitrary. Document rationale for each gate.
- **inputs**: Current feature matrix, user feedback, pricing strategy
- **outputs**: Revised feature matrix with clear differentiation
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Feature matrix approved, communicated clearly

#### Task: UPG-002
- **title**: Implement in-app upgrade prompts at feature gates
- **description**: When a Solo user attempts a Pro feature, show a contextual upgrade prompt highlighting the benefit they want. Don't block the feature entirely — show a teaser and offer upgrade. Include social proof ("Join 200+ artisans on Pro").
- **inputs**: Feature usage data, upgrade prompt copy, paywall logic
- **outputs**: Upgrade prompts at all feature gates
- **dependencies**: UPG-001, TRC-003
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Upgrade prompts live, upgrade conversion rate measurable

#### Task: UPG-003
- **title**: Create upgrade email sequence for upgrade-ready users
- **description**: Identify users who are hitting Solo limits (e.g., 10 clients, 5 jobs/month). Send a personalized email: "You're approaching your [limit] — here's what Pro unlocks." Include specific usage data. Test frequency and timing.
- **inputs**: Usage data, email tool, personalized content
- **outputs**: Upgrade email sequence live
- **dependencies**: UPG-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Emails sent at limit approach, upgrade rate measured

#### Task: UPG-004
- **title**: Build upgrade tracking dashboard
- **description**: Create internal dashboard showing upgrade funnels: which features are triggering upgrades, average time from feature encounter to upgrade, upgrade rate by tier and profession. Track weekly.
- **inputs**: Upgrade event data, dashboard tool
- **outputs**: Upgrade dashboard live
- **dependencies**: UPG-002
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Dashboard in use, upgrade patterns identified

#### Task: UPG-005
- **title**: Test annual upgrade pricing with loyalty discount
- **description**: Offer existing Solo users upgrading to Pro: "Upgrade now and lock in 40% annual discount — never pay more." Test if annual commitment increases upgrade rate and reduces downgrade rate.
- **inputs**: Upgrade pricing structure, annual discount mechanics
- **outputs**: Annual upgrade offer live, upgrade and retention rates measured
- **dependencies**: UPG-003
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Annual upgrade uptake >40% of upgrades, downgrade rate reduced

#### Task: UPG-006
- **title**: Implement milestone-triggered upgrade offers
- **description**: When a user hits significant milestones on Solo (50th job, 20th client), celebrate and offer: "You've outgrown Solo — Pro grows with you." Make the upgrade feel like a natural progression, not a sales push.
- **inputs**: Milestone tracking, celebration UI, upgrade offer
- **outputs**: Milestone upgrade offers live
- **dependencies**: UPG-003
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Milestone offers trigger at correct thresholds, upgrade rate measurable

#### Task: UPG-007
- **title**: Create Pro feature preview for Solo users
- **description**: Allow Solo users to "preview" Pro features for 7 days. Show a "Pro" badge on features they can't access fully. Tease functionality. After preview, show upgrade CTA. Track preview-to-upgrade conversion.
- **inputs**: Feature preview logic, preview tracking, upgrade CTA
- **outputs**: Pro preview feature live
- **dependencies**: UPG-002
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Previews used, preview-to-upgrade rate >15%

#### Task: UPG-008
- **title**: Build team-size upgrade triggers
- **description**: When Solo user attempts to invite a second team member, prompt: "Pro includes up to 5 team members. Upgrade to keep growing your team." Track team-invite upgrades.
- **inputs**: Team invite flow, upgrade logic, trigger rules
- **outputs**: Team upgrade prompts live
- **dependencies**: UPG-002
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Team upgrade prompts working, team upgrades measurable

#### Task: UPG-009
- **title**: Develop upgrade success stories by profession
- **description**: Collect and publish upgrade success stories: "How this Lyon plumber doubled his jobs with Pro." Create profession-specific case studies. Include specific metrics. Distribute via email, in-app, and social.
- **inputs**: Customer interviews, case study template, distribution channels
- **outputs**: 6 case studies published (2 per profession)
- **dependencies**: UPG-003
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Case studies published, measurable traffic and upgrade influence

#### Task: UPG-010
- **title**: Test trade-specific upgrade messaging
- **description**: A/B test upgrade messaging tailored by trade: plumbers get "Never miss an emergency call again" vs generic "Upgrade to Pro." Measure which messages drive higher upgrade rates per profession.
- **inputs**: A/B testing framework, trade-specific copy
- **outputs**: Winning messages per profession identified
- **dependencies**: UPG-003
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Trade-specific messages outperform generic, messages deployed

#### Task: UPG-011
- **title**: Implement downgrade protection program
- **description**: For customers considering downgrade, trigger retention flow: "Downgrade means losing X, Y, Z. Can we offer you a 20% discount to stay on Pro for 3 more months?" Track what prevents downgrade.
- **inputs**: Downgrade flow, retention offer logic
- **outputs**: Downgrade protection active
- **dependencies**: UPG-002, CHR-005
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Downgrade prevention rate measurable, net revenue impact positive

#### Task: UPG-012
- **title**: Create upgrade ROI calculator
- **description**: Build an in-product ROI calculator: "Based on your 20 jobs/month, Pro's scheduling features save you 3 hours/week = €X saved/month." Make upgrade feel financially rational. Allow input of specific numbers.
- **inputs**: Calculator logic, product integrations, ROI assumptions
- **outputs**: ROI calculator live in product
- **dependencies**: UPG-002
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Calculator used by >20% of upgrade-interested users, upgrade lift measurable

#### Task: UPG-013
- **title**: Build "Pro Benefits" education campaign
- **description**: Create a multi-touch campaign to educate Solo users on Pro benefits: weekly email tips featuring one Pro feature, in-app feature spotlights, YouTube tutorials. Goal: desire-building before upgrade ask.
- **inputs**: Email tool, content calendar, feature highlights
- **outputs**: Pro education campaign live
- **dependencies**: UPG-001
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Campaign running, Pro feature trial rate increased

#### Task: UPG-014
- **title**: Implement time-limited upgrade offer for dormant upgrades
- **description**: For users who showed upgrade intent (visited pricing) but didn't upgrade within 7 days, send limited-time offer: "Your upgrade discount expires in 48 hours." Test urgency impact on conversion.
- **inputs**: Upgrade intent tracking, countdown timer, urgency offer
- **outputs**: Limited-time upgrade offer deployed
- **dependencies**: UPG-003
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Urgency offers convert at higher rate vs no-deadline offers

#### Task: UPG-015
- **title**: Create referral-accelerated upgrade path
- **description**: Allow users to "earn" a free Pro month for each new customer they refer who converts. Accumulate credits over time. Make earning feel achievable. Track referral-funded upgrades.
- **inputs**: Referral tracking, credit system, upgrade integration
- **outputs**: Referral upgrade credits live
- **dependencies**: UPG-002
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: growth
- **validation**: Credits used by >10% of Solo users, referral conversion measurable

---

### Category: Customer LTV Maximization

#### Task: LTV-001
- **title**: Calculate current LTV by tier and cohort
- **description**: Build LTV model: average revenue per user (ARPU) × average customer lifespan × gross margin. Calculate for each tier (Solo/Pro/Business), each cohort (signup month), and each segment (profession). Establish baseline LTV.
- **inputs**: Revenue data, churn data, cohort definitions
- **outputs**: LTV model with segment breakdowns
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: LTV model complete, baseline metrics established

#### Task: LTV-002
- **title**: Identify LTV extension opportunities per customer lifecycle stage
- **description**: Map customer lifecycle: Onboarding → Active → Engaged → At-Risk → Churned. For each stage, identify 2-3 tactics to extend LTV: upsells for active, re-engagement for at-risk, referrals for engaged.
- **inputs**: Customer lifecycle data, LTV model
- **outputs**: Lifecycle stage tactic map
- **dependencies**: LTV-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Tactic map complete, tactics being executed

#### Task: LTV-003
- **title**: Implement usage-based expansion revenue triggers
- **description**: Track usage patterns that correlate with upgrade readiness: high job volume, multiple team members, multiple locations. When users demonstrate "enterprise-level" usage on lower tier, proactively offer upgrade with white-glove migration.
- **inputs**: Usage tracking, expansion signals, sales outreach
- **outputs**: Expansion revenue triggers live
- **dependencies**: LTV-001, UPG-008
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Expansion opportunities identified, migration revenue tracked

#### Task: LTV-004
- **title**: Build annual vs monthly LTV comparison model
- **description**: Calculate true LTV difference between annual and monthly subscribers. Include discount cost, churn difference, and admin cost. Use to optimize annual pricing and incentives.
- **inputs**: Payment data, churn data by plan type
- **outputs**: Annual vs monthly LTV analysis
- **dependencies**: LTV-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: LTV difference quantified, annual pricing optimized

#### Task: LTV-005
- **title**: Create premium add-on feature roadmap
- **description**: Identify 3-5 premium add-ons that can be sold above base tier: advanced reporting, API access, custom integrations, white-labeling. Price each add-on. Create desire through education. Track addon adoption.
- **inputs**: Feature wishlist data, development costs, pricing model
- **outputs**: Add-on pricing and roadmap
- **dependencies**: LTV-001
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Add-ons available, addon ARPU contribution measurable

#### Task: LTV-006
- **title**: Implement customer appreciation lifecycle emails
- **description**: Send relationship-building emails: 1-week post-signup ("Welcome to the family"), 3-month ("How's it going?"), 6-month ("Thank you for being part of our community"), annual ("Happy Anniversary — here's a gift"). Non-promotional, pure relationship.
- **inputs**: Email tool, customer milestones, gift/offer ideas
- **outputs**: Lifecycle appreciation emails live
- **dependencies**: LTV-002
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Emails deployed, retention lift from appreciation measurable

#### Task: LTV-007
- **title**: Build cross-sell opportunity identification model
- **description**: Identify cross-sell opportunities: Solo users with high mobile usage → mobile app upsell. Users not using invoicing → invoicing tutorial + feature push. Users with no team → team collaboration push. Personalize outreach.
- **inputs**: Feature usage data, cross-sell mapping
- **outputs**: Cross-sell trigger system live
- **dependencies**: LTV-002
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Cross-sell triggers firing, cross-sell revenue tracked

#### Task: LTV-008
- **title**: Create LTV-focused customer success playbook
- **description**: Document CS playbook: how to identify expansion opportunities, how to conduct renewal conversations, how to address at-risk customers. Train entire CS team on LTV maximization.
- **inputs**: CS team input, best practices, training materials
- **outputs**: CS playbook, team trained
- **dependencies**: LTV-002, CHR-006
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Playbook complete, CS team certified, LTV impact measurable

#### Task: LTV-009
- **title**: Implement net revenue retention (NRR) tracking
- **description**: Track NRR monthly: (Revenue at start of month + Expansion - Contraction - Churn) / Revenue at start of month. Target NRR >110%. Create dashboard showing NRR trend and drivers.
- **inputs**: Revenue data, expansion/contraction data
- **outputs**: NRR dashboard live
- **dependencies**: LTV-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: NRR >110%, drivers of NRR understood

#### Task: LTV-010
- **title**: Create loyalty reward program for long-term customers
- **description**: After 12 months, offer loyalty rewards: priority support, free feature previews, annual discount renewal. Track impact on 12-month retention and LTV.
- **inputs**: Loyalty program design, eligibility rules
- **outputs**: Loyalty program launched
- **dependencies**: LTV-006
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Loyalty program active, 12-month retention improved

---

### Category: Viral/Referral Loop Design

#### Task: VIR-001
- **title**: Design referral program mechanics
- **description**: Define referral program: referrer gets 1 month free per successful referral, referee gets 50% off first month. Set eligibility (must be paying customer). Create referral link, share cards, and tracking system.
- **inputs**: Referral program templates, discount structures, legal requirements
- **outputs**: Referral program mechanics documented
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Referral program live, referral rate >10% of customers

#### Task: VIR-002
- **title**: Implement in-product referral sharing
- **description**: Add "Invite a colleague" button in dashboard header. One-click share to email, WhatsApp, Facebook. Create pre-written message: "I've been using Mini-CRM — it's transformed how I manage my jobs. Here's your exclusive trial link." Track shares.
- **inputs**: Sharing tools, pre-written copy, tracking
- **outputs**: In-product referral sharing live
- **dependencies**: VIR-001
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Share button used by >20% of customers, referral conversions tracked

#### Task: VIR-003
- **title**: Create referral achievement milestones
- **description**: Gamify referrals: 1 referral = badge + 1 month free, 3 referrals = badge + 3 months free, 5 referrals = "Top Referrer" status + lifetime discount. Celebrate publicly (with permission) on social media.
- **inputs**: Referral tracking, badge system, celebration mechanics
- **outputs**: Referral milestones live
- **dependencies**: VIR-001
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Milestone achievements tracked, referral velocity increased

#### Task: VIR-004
- **title**: Build automated referral reward fulfillment
- **description**: Automate referral credit application: when referee converts, automatically apply credit to referrer's account. Send confirmation email. Avoid manual fulfillment — automate entirely.
- **inputs**: Referral tracking, billing integration, email automation
- **outputs**: Automated reward fulfillment live
- **dependencies**: VIR-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Credits applied automatically, fulfillment errors <1%

#### Task: VIR-005
- **title**: Create artisan community referral stories
- **description**: Interview top referrers. Publish case studies: "How Jean-Luc referred 8 colleagues and saved €300/year." Distribute in artisan Facebook groups and WhatsApp communities. Make referral feel community-building.
- **inputs**: Referrer interviews, case study template
- **outputs**: 5 referral case studies published
- **dependencies**: VIR-003
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Case studies published, referral rate from case study views measurable

#### Task: VIR-006
- **title**: Implement "Join your colleague" onboarding
- **description**: When referee signs up via referral link, show: "Your colleague [Name] uses Mini-CRM — here's what they love about it." Provide peer validation. Pre-populate some setup from peer's configuration (with permission).
- **inputs**: Referral data, peer data sharing, onboarding customization
- **outputs**: Peer-referral onboarding live
- **dependencies**: VIR-001, VIR-002
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: product
- **validation**: Referral trial-to-paid rate improved vs non-referral trials

#### Task: VIR-007
- **title**: Create trade-specific referral collateral
- **description**: Build referral materials per trade: plumber-specific email templates, electrician social cards, carpenter WhatsApp messages. Make it easy for referrers to share in their professional networks.
- **inputs**: Trade-specific copy, design assets, sharing platforms
- **outputs**: Trade-specific referral materials ready
- **dependencies**: VIR-002
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Materials available in-app, usage tracked by trade

#### Task: VIR-008
- **title**: Run referral program promotion campaign
- **description**: Launch a targeted campaign to promote referral program: email to all customers, in-app banners, social media posts. Time it around renovation season when artisans are networking. Track referral spike.
- **inputs**: Customer email list, in-app banner placement, social calendar
- **outputs**: Referral campaign launched
- **dependencies**: VIR-001
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Campaign launched, referral rate spike measurable

#### Task: VIR-009
- **title**: Build referral analytics dashboard
- **description**: Create dashboard showing: referrals by referrer, referral conversion rate, revenue attributed to referrals, top referrers leaderboard. Update weekly. Share with team.
- **inputs**: Referral data, dashboard tool
- **outputs**: Referral dashboard live
- **dependencies**: VIR-001
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Dashboard in use, referral program ROI calculable

#### Task: VIR-010
- **title**: Test referral incentive variations
- **description**: A/B test referral incentives: 1 month free vs 2 months free vs 50% off vs Amazon gift card. Identify which incentive drives highest referral volume and quality (quality = referral retention).
- **inputs**: A/B testing framework, incentive variants
- **outputs**: Winning incentive identified
- **dependencies**: VIR-001
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Test complete, best incentive deployed

#### Task: VIR-011
- **title**: Create "referral partnership" program with trade associations
- **description**: Partner with French trade associations (Companies, CAPEB, etc.). Offer association members exclusive discount. Association promotes to members. Track member signups.
- **inputs**: Association contacts, partnership terms, tracking links
- **outputs**: 3 partnership agreements signed
- **dependencies**: VIR-001
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: marketing
- **validation**: Partnerships active, association-driven signups tracked

#### Task: VIR-012
- **title**: Implement shareable achievement cards
- **description**: When a user hits a milestone (100th job, 1 year anniversary), generate a shareable card: "I've managed 100 jobs with Mini-CRM!" with app branding. One-click share to WhatsApp, Facebook, Instagram Stories.
- **inputs**: Card generation tool, milestone triggers, sharing integration
- **outputs**: Achievement cards live
- **dependencies**: ACT-009
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Cards shared >1000 times, organic reach measurable

#### Task: VIR-013
- **title**: Build testimonial collection systematization
- **description**: After successful job completion, prompt user: "Share how Mini-CRM helped you?" Collect video testimonials and written reviews. Make collection effortless. Offer small reward for testimonial.
- **inputs**: Testimonial prompt logic, collection workflow, review platforms
- **outputs**: Systematic testimonial collection active
- **dependencies**: VIR-002
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Testimonials collected monthly, reviews on key platforms growing

#### Task: VIR-014
- **title**: Create viral loop from shared job cards
- **description**: When a job is completed, generate a shareable "job complete" card for the artisan to send to client. Card includes subtle Mini-CRM branding. Client sees card, potentially becomes user. Track card shares and conversions.
- **inputs**: Card template, share mechanism, branding
- **outputs**: Job completion cards live
- **dependencies**: []
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Cards shared, client signups tracked

---

### Category: Pricing Psychology & Packaging

#### Task: PRC-001
- **title**: Conduct full pricing psychology audit
- **description**: Review current pricing from psychological perspective: price points vs competitor, tier naming (Solo/Pro/Business), anchoring, decoy effects, bundling. Identify friction points and opportunities. Benchmark against SaaS best practices.
- **inputs**: Current pricing page, competitor pricing, pricing psychology framework
- **outputs**: Pricing audit report with recommendations
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Audit complete, recommendations prioritized

#### Task: PRC-002
- **title**: Test tier naming alternatives
- **description**: A/B test tier names: "Solo/Pro/Business" vs "Starter/Professional/Team" vs "Essentials/Premium/Enterprise." Measure impact on plan selection and conversion.
- **inputs**: Name variants, A/B testing framework, traffic levels
- **outputs**: Winning tier names implemented
- **dependencies**: PRC-001
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Test complete, conversion impact measured

#### Task: PRC-003
- **title**: Implement price anchoring with Business tier
- **description**: Make Business tier the first/most prominent tier (even if most expensive). Research shows highest price shown first makes others feel more affordable. Test "Business first" vs "Solo first" layout.
- **inputs**: Pricing page layout variants, A/B test setup
- **outputs**: Anchoring test results, winning layout deployed
- **dependencies**: PRC-001
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Test complete, anchoring impact quantified

#### Task: PRC-004
- **title**: Create decoy tier strategy
- **description**: Introduce a "Team" tier positioned between Pro and Business with pricing designed to make Business seem like better value. Test if decoy increases Business tier selection.
- **inputs**: Decoy tier pricing, feature matrix for decoy
- **outputs**: Decoy tier live, Business upgrade rate tracked
- **dependencies**: PRC-001
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Decoy increases Business selection by >20%

#### Task: PRC-005
- **title**: Test monthly vs annual toggle default
- **description**: Test which default pricing view drives higher annual plan adoption: show annual by default with monthly as option vs monthly by default with annual as option. Measure annual selection rate.
- **inputs**: Pricing page variants, toggle logic
- **outputs**: Test results, optimal default identified
- **dependencies**: PRC-001
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Annual plan uptake optimized

#### Task: PRC-006
- **title**: Optimize per-seat vs per-user pricing psychology
- **description**: Test per-seat pricing vs flat-tier pricing. For trades with 1-3 person teams, per-seat may feel fairer. Test both approaches for conversion and perceived value.
- **inputs**: Pricing variants, user research
- **outputs**: Pricing model test results
- **dependencies**: PRC-001
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Winning pricing model deployed

#### Task: PRC-007
- **title**: Implement value-based pricing messaging
- **description**: Shift pricing page messaging from features to outcomes: "From €29/month — Never miss a client call again." "From €49/month — Double your jobs without doubling your stress." Test outcome-based vs feature-based messaging.
- **inputs**: Outcome-oriented copy, A/B testing framework
- **outputs**: Outcome messaging live, conversion lift measured
- **dependencies**: PRC-001
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Outcome messaging outperforms feature messaging

#### Task: PRC-008
- **title**: Create "getting started" vs "growing" packaging test
- **description**: Test packaging by life stage: "Getting Started (1-5 clients)" and "Growing (5+ clients)" instead of Solo/Pro. Match packaging to customer journey stage. Measure conversion and upgrade rates.
- **inputs**: Life-stage packaging concepts, A/B test setup
- **outputs**: Test results, winning packaging deployed
- **dependencies**: PRC-001
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Life-stage packaging converts better

#### Task: PRC-009
- **title**: Test bundling vs add-on pricing for extras
- **description**: Test whether features like SMS reminders, advanced reporting, and API access should be bundled into tiers or sold as add-ons. Measure revenue per user and conversion impact.
- **inputs**: Bundle variants, add-on pricing model
- **outputs**: Test results, optimal bundling strategy
- **dependencies**: PRC-001
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Bundle strategy maximizes ARPU

#### Task: PRC-010
- **title**: Implement price increase communication strategy
- **description**: When planning price increases, develop communication framework: early notice (60 days), value delivery emphasis ("we've added X, Y, Z"), legacy pricing lock option for loyal customers. Test messaging to minimize churn from increase.
- **inputs**: Price increase plan, customer segments, communication calendar
- **outputs**: Price increase playbook
- **dependencies**: PRC-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Playbook complete, price increase executed with <5% churn

#### Task: PRC-011
- **title**: Create Freemium vs Premium trial comparison study
- **description**: Research artisan preferences: do they prefer limited free tier (always free, capped features) or time-limited trial (full access, 30 days)? Test both models for acquisition and conversion.
- **inputs**: Test setup, traffic split, conversion tracking
- **outputs**: Model comparison with clear winner
- **dependencies**: PRC-001
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: growth
- **validation**: Optimal model identified and implemented

#### Task: PRC-012
- **title**: Implement reciprocal pricing offer
- **description**: Offer existing customers a reciprocal deal: "Refer 1 customer and get your next month free." Combine referral and retention. Test different reciprocal offers for conversion.
- **inputs**: Reciprocal offer variants, tracking
- **outputs**: Reciprocal offers tested
- **dependencies**: PRC-001, VIR-010
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Reciprocal offers drive both referrals and retention

#### Task: PRC-013
- **title**: Test "first month at 1€" vs "30 days free" messaging
- **description**: Test whether "first month for €1" converts better than "30 days free before you pay." Include all terms clearly. Measure conversion and early churn.
- **inputs**: Offer variants, checkout integration, terms display
- **outputs**: Winning offer message implemented
- **dependencies**: PRC-001
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Offer conversion measured, early churn tracked

#### Task: PRC-014
- **title**: Create price-tier comparison table optimization
- **description**: Optimize the feature comparison table: use checkmarks/X marks effectively, highlight recommended tier, use hover tooltips for feature explanations, include "most popular" badge. A/B test table layouts.
- **inputs**: Table design variants, A/B test setup
- **outputs**: Optimized comparison table
- **dependencies**: PRC-001
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Table optimization improves plan selection rate

#### Task: PRC-015
- **title**: Implement regional pricing for France regions
- **description**: Test pricing for different French regions (Paris vs provinces). Consider purchasing power differences. May justify regional pricing for lower-income areas. Track by billing address.
- **inputs**: Regional pricing model, implementation
- **outputs**: Regional pricing tested
- **dependencies**: PRC-001
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Regional pricing impact on conversion and volume measured

---

### Category: Freemium vs Free Trial Optimization

#### Task: FTU-001
- **title**: Define freemium vs free trial success metrics
- **description**: Establish KPIs for both models: free trial (conversion rate, time to convert, trial length optimization) and freemium (activation rate, upgrade rate, free-tier retention). Set baseline targets.
- **inputs**: Industry benchmarks, current data
- **outputs**: Success metrics framework
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Metrics framework approved

#### Task: FTU-002
- **title**: Analyze competitor models in French artisan market
- **description**: Survey what competitors offer: free tier, free trial, or paid-only. Map competitor positioning. Identify white space in the market.
- **inputs**: Competitor analysis, market research
- **outputs**: Competitor model comparison
- **dependencies**: FTU-001
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Competitor landscape mapped

#### Task: FTU-003
- **title**: Test hybrid model: freemium + trial
- **description**: Test offering permanent free tier (limited to 3 clients, 10 jobs/month) PLUS 30-day full-access trial when they hit limits. Measure if hybrid drives more acquisitions than trial-only.
- **inputs**: Hybrid model specs, test setup
- **outputs**: Hybrid model test results
- **dependencies**: FTU-001, FTU-002
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: growth
- **validation**: Hybrid model compared to trial-only

#### Task: FTU