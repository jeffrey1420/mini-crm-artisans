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

#### Task: FTU004
- **title**: Implement time-limited feature unlocks
- **description**: Give free users temporary access to Pro features: "Try Pro features free for 7 days." No credit card required. After trial, revert to free tier. Track trial-to-paid conversion from these unlocks.
- **inputs**: Feature unlock logic, tracking, reversion mechanics
- **outputs**: Feature unlock system live
- **dependencies**: FTU-001
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Feature unlocks drive paid conversions

#### Task: FTU-005
- **title**: Create free tier upgrade prompts at natural limits
- **description**: When free-tier users hit limits (3rd client, 10th job), show upgrade prompt. Make the limit feel constraining. Show exactly what they'd gain with upgrade. Time it exactly at limit, not before.
- **inputs**: Limit tracking, upgrade prompts, timing logic
- **outputs**: Limit-triggered upgrade prompts live
- **dependencies**: FTU-003
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Limit prompts drive upgrades

#### Task: FTU-006
- **title**: Design free tier that creates network effects
- **description**: Make free tier more valuable when team members use it. Free users can invite 1 team member for free. More team invites = more signups. Track virality from team invites.
- **inputs**: Team invite logic, free tier rules
- **outputs**: Network-effect free tier live
- **dependencies**: FTU-003
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Team invites drive network growth

#### Task: FTU-007
- **title**: Implement free-to-paid transition friction reduction
- **description**: When free user upgrades, minimize steps: pre-fill from free account, show their existing data, make payment the only friction. Remove any re-onboarding. Measure drop-off at each step.
- **inputs**: Checkout flow, upgrade path, data migration
- **outputs**: Frictionless upgrade flow live
- **dependencies**: FTU-005
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Upgrade completion rate >85%

#### Task: FTU-008
- **title**: Create free tier abandonment recovery sequence
- **description**: For free users who haven't logged in for 14+ days, send re-engagement sequence: "Your free Mini-CRM is waiting — here's what's new." Include feature highlights and easy re-entry.
- **inputs**: Dormant user data, re-engagement email content
- **outputs**: Re-engagement sequence live
- **dependencies**: FTU-001
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Re-engagement rate measurable

#### Task: FTU-009
- **title**: Test "forever free" vs "free trial" value proposition
- **description**: Create two landing pages: one offering "Forever free plan" and one offering "30 days free trial." Split traffic 50/50. Measure which drives more signups and higher-quality customers.
- **inputs**: Landing page variants, traffic split
- **outputs**: Test results, winning value prop
- **dependencies**: FTU-001, FTU-002
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Clear winner identified

#### Task: FTU-010
- **title**: Build free tier usage analytics
- **description**: Track free tier user behavior: activation rate, feature usage, upgrade rate, and upgrade timing. Identify what separates free users who upgrade from those who don't.
- **inputs**: Free user data, analytics setup
- **outputs**: Free tier analytics dashboard
- **dependencies**: FTU-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Dashboard live, upgrade predictors identified

---

### Category: Monthly/Annual Pricing Strategy

#### Task: MAP-001
- **title**: Calculate monthly vs annual revenue impact model
- **description**: Model revenue impact of annual vs monthly mix: cash flow, churn rate difference, discount cost, administrative savings. Recommend optimal annual/monthly mix target.
- **inputs**: Revenue data, churn by plan type, discount costs
- **outputs**: Annual/monthly revenue model
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Model complete, annual mix target set

#### Task: MAP-002
- **title**: Test annual plan discount levels
- **description**: Test 20% vs 30% vs 40% annual discount. Measure impact on annual plan adoption rate and overall revenue per customer. Find optimal discount level.
- **inputs**: Discount variants, A/B test
- **outputs**: Optimal discount level identified
- **dependencies**: MAP-001
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Discount level optimized

#### Task: MAP-003
- **title**: Implement "best value" badge on annual plans
- **description**: Add visual "Best Value" badge on annual pricing. Show monthly equivalent price prominently. Make annual savings crystal clear: "Save €XXX/year vs monthly."
- **inputs**: Badge design, pricing display
- **outputs**: Badge implemented
- **dependencies**: MAP-002
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Badge impact on annual selection measurable

#### Task: MAP-004
- **title**: Create annual plan upgrade incentives
- **description**: Offer exclusive annual-only benefits: free setup assistance, priority support, early access to new features. Make annual feel premium beyond just discount.
- **inputs**: Annual-only benefits, pricing page
- **outputs**: Annual premium benefits live
- **dependencies**: MAP-002
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Annual upgrade rate increases

#### Task: MAP-005
- **title**: Test month-to-month exit messaging
- **description**: When monthly user cancels, capture reason: "too expensive" vs "not using it" vs "competitor." Use data to address specific exit reasons. Implement targeted retention for "too expensive."
- **inputs**: Cancellation flow, reason capture
- **outputs**: Exit reason analysis, retention tactics
- **dependencies**: MAP-001
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Exit reasons tracked, retention improved for price-sensitive

#### Task: MAP-006
- **title**: Implement mid-year annual plan upgrade option
- **description**: Allow monthly subscribers to switch to annual mid-year: "Switch to annual and get credit for months already paid." Reduce friction for annual commitment.
- **inputs**: Proration logic, upgrade flow
- **outputs**: Mid-year annual switch live
- **dependencies**: MAP-003
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Annual upgrade rate increases

#### Task: MAP-007
- **title**: Build seasonal annual plan promotions
- **description**: Time annual plan promotions around renovation season (Sept-Oct, Jan-Feb). Create urgency: "Annual plan at 40% off — only until end of month." Test if seasonal promotions outperform year-round offers.
- **inputs**: Seasonal calendar, promotion mechanics
- **outputs**: Seasonal promotions deployed
- **dependencies**: MAP-002
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Seasonal promotions outperform baseline

#### Task: MAP-008
- **title**: Create lifetime deal for annual prepayers
- **description**: Offer "lifetime" pricing for customers who prepay 2+ years upfront. Test willingness to pay for 2-year commitment. Track conversion and retention.
- **inputs**: Lifetime pricing model, checkout integration
- **outputs**: Lifetime offer tested
- **dependencies**: MAP-001
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Lifetime offer conversion and LTV measured

#### Task: MAP-009
- **title**: Implement price lock guarantee for annual subscribers
- **description**: Announce: "Lock in your annual rate — we'll never increase your price while you remain a subscriber." Test impact on annual conversion and churn.
- **inputs**: Price lock messaging, guarantee terms
- **outputs**: Price lock implemented
- **dependencies**: MAP-003
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Price lock drives annual conversions

#### Task: MAP-010
- **title**: Analyze annual plan renewal patterns
- **description**: Track annual plan renewals: what % renew, what % downgrade, what % churn. Identify renewal risk factors. Build renewal prediction model.
- **inputs**: Renewal data, churn data
- **outputs**: Renewal prediction model
- **dependencies**: MAP-001
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Renewal model deployed, renewal rate predictable

---

### Category: Win-Back Campaigns (churned customers)

#### Task: WIN-001
- **title**: Segment churned customers by churn reason
- **description**: Classify all churned customers by reason: (1) price, (2) not using it, (3) switched to competitor, (4) went out of business, (5) other. Build segment-specific win-back strategies for segments 1-3.
- **inputs**: Churn reason data, exit surveys
- **outputs**: Churn segmentation with win-back strategies
- **dependencies**: CHR-007
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Segments defined, strategies assigned

#### Task: WIN-002
- **title**: Create win-back email sequence (3-touch)
- **description**: Design 3-email win-back sequence: (1) "We miss you — here's what you've been missing", (2) "Special offer: 50% off for 3 months", (3) "Last chance — your account data expires in 7 days." Each email drives to landing page.
- **inputs**: Churned customer list, email creative, offer variants
- **outputs**: Win-back email sequence live
- **dependencies**: WIN-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Win-back rate >5%, revenue positive from campaign

#### Task: WIN-003
- **title**: Implement personalized win-back offers by segment
- **description**: For price-sensitive churns: heavy discount. For not-using-it churns: re-engagement tips + extended trial. For competitor churns: competitor comparison + migration assistance. Track which works best.
- **inputs**: Segment data, offer variants
- **outputs**: Personalized offers deployed
- **dependencies**: WIN-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Personalized offers outperform generic

#### Task: WIN-004
- **title**: Create win-back landing page
- **description**: Build dedicated landing page for win-back campaign: show what's new since they left, include testimonials, highlight special offer. Track page performance and conversion.
- **inputs**: Landing page design, what's-new content
- **outputs**: Win-back landing page live
- **dependencies**: WIN-002
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Landing page conversion rate >3%

#### Task: WIN-005
- **title**: Implement SMS win-back campaign
- **description**: For churned customers who opted into SMS, send win-back SMS sequence: "Jean, we noticed you left Mini-CRM — we've made X improvements. Here's 50% off your return." Track SMS-to-conversion.
- **inputs**: SMS provider, churned SMS list, message variants
- **outputs**: SMS win-back active
- **dependencies**: WIN-001
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: SMS win-back measurable

#### Task: WIN-006
- **title**: Test "return customer" discount vs "new customer" pricing
- **description**: Test whether offering churned customers "welcome back" pricing (same as new customer trial) outperforms standard win-back discounts. Track LTV of returning customers.
- **inputs**: Offer variants, returning customer tracking
- **outputs**: Test results, winning offer
- **dependencies**: WIN-003
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Returning customer LTV comparable to new customer

#### Task: WIN-007
- **title**: Build reactivation timeline after churn
- **description**: Define optimal timing: send first win-back email at 7 days post-churn, second at 14 days, third at 30 days. Test if 60-day sequence outperforms 30-day.
- **inputs**: Win-back timing data
- **outputs**: Reactivation timeline optimized
- **dependencies**: WIN-002
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Timing optimized for conversion

#### Task: WIN-008
- **title**: Create "we've improved" update campaigns
- **description**: When significant features are released, send "we've improved" email to all churned customers. Show specific improvements relevant to their churn reason. Make case for return.
- **inputs**: Feature release notes, churn reason data
- **outputs**: Improvement update campaigns
- **dependencies**: WIN-001
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Feature-driven win-back measurable

#### Task: WIN-009
- **title**: Implement referral-to-win-back hybrid
- **description**: For churned customers, offer: "Come back and bring a friend — both get 1 month free." Combines win-back with referral acquisition. Track hybrid conversion.
- **inputs**: Hybrid offer mechanics, tracking
- **outputs**: Hybrid campaign active
- **dependencies**: WIN-003
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Hybrid outperforms single-offer

#### Task: WIN-010
- **title**: Build win-back performance analytics
- **description**: Create dashboard tracking: win-back email performance (open, click, conversion), offer performance by segment, returning customer LTV vs new customer LTV, cost per reactivation.
- **inputs**: Win-back data, analytics
- **outputs**: Win-back dashboard live
- **dependencies**: WIN-001
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Dashboard tracks all KPIs

---

### Category: NPS & VOC (Voice of Customer) Program

#### Task: VOC-001
- **title**: Implement NPS survey integration
- **description**: Integrate NPS tool (Wootric, Delighted, or similar) at key touchpoints: 7 days post-signup, 30 days post-signup, 90 days post-signup, and at cancellation. Track scores over time.
- **inputs**: NPS tool, survey triggers
- **outputs**: NPS tracking live
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: NPS data flowing, baseline established

#### Task: VOC-002
- **title**: Create monthly NPS reporting cadence
- **description**: Establish monthly review: NPS score by cohort, by tier, by profession. Identify trends. Set target: NPS >40 (Good) within 12 months. Create action items from insights.
- **inputs**: NPS data, reporting tool
- **outputs**: Monthly NPS report
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Reports generated monthly

#### Task: VOC-003
- **title**: Close the loop with detractors
- **description**: When NPS response is scored 6 or below, trigger immediate alert to CS team. CS reaches out within 48 hours to understand issue and resolve. Track resolution rate and NPS score change.
- **inputs**: NPS tool, CS workflow, alert system
- **outputs**: Detractor outreach active
- **dependencies**: VOC-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Detractors contacted within 48h, NPS lift from outreach measurable

#### Task: VOC-004
- **title**: Analyze NPS comments by theme
- **description**: Implement text analysis of NPS comments. Cluster into themes: pricing, features, UX, support, onboarding. Quantify volume per theme. Identify top pain points.
- **inputs**: NPS text data, text analysis tool
- **outputs**: Theme analysis report
- **dependencies**: VOC-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Top pain points identified, product roadmap influenced

#### Task: VOC-005
- **title**: Create closed-loop feedback system
- **description**: For every NPS response, document action taken. If feature requested: add to backlog. If support issue: improve support. If pricing: adjust pricing tests. Create feedback loop.
- **inputs**: Feedback tracking, product backlog
- **outputs**: Closed-loop process documented
- **dependencies**: VOC-003, VOC-004
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: All feedback acted upon

#### Task: VOC-006
- **title**: Publish NPS results to customers
- **description**: Share NPS results and resulting actions with customers via email/blog: "You told us X was broken — here's what we fixed." Builds trust and shows responsiveness.
- **inputs**: NPS data, action items, communication
- **outputs**: Transparency communication sent
- **dependencies**: VOC-005
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Communication published, customer response measured

#### Task: VOC-007
- **title**: Create in-app feedback widget
- **description**: Add persistent "Feedback" button in app. Click opens short survey (3 questions max). Capture real-time feedback without interrupting workflow. Analyze weekly.
- **inputs**: Feedback tool, survey questions
- **outputs**: In-app feedback widget live
- **dependencies**: VOC-001
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Feedback captured weekly, themes identified

#### Task: VOC-008
- **title**: Build customer advisory board (5-7 members)
- **description**: Recruit 5-7 highly engaged customers (one per region/profession) to quarterly advisory board. Get early feedback on roadmap, pricing changes, and features. Build strong advocates.
- **inputs**: Customer nominations, board structure
- **outputs**: Advisory board formed
- **dependencies**: VOC-002
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: growth
- **validation**: Board meets quarterly, feedback implemented

#### Task: VOC-009
- **title**: Implement social listening for brand mentions
- **description**: Monitor Twitter, Facebook, LinkedIn, Google reviews, and app stores for brand mentions. Track sentiment. Respond to all mentions. Build review response process.
- **inputs**: Social listening tool, response process
- **outputs**: Social monitoring active
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: All mentions responded to within 24h

#### Task: VOC-010
- **title**: Create customer interview program
- **description**: Conduct 5 customer interviews per month: mix of happy customers, unhappy customers, and churned customers. Use for qualitative insights. Document learnings. Share with team.
- **inputs**: Interview guide, customer list
- **outputs**: Monthly interview summaries
- **dependencies**: VOC-002
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: 5+ interviews per month, insights shared

---

### Category: Community Building (French artisans Facebook/WhatsApp groups)

#### Task: CMB-001
- **title**: Identify and map French artisan Facebook groups
- **description**: Research all relevant Facebook groups: plumbers (300+ members), electricians, carpenters, general artisans. Identify group sizes, activity levels, and rules. Prioritize for outreach.
- **inputs**: Facebook search, group analysis
- **outputs**: Group map with priority ranking
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: 20+ relevant groups identified

#### Task: CMB-002
- **title**: Develop community participation guidelines
- **description**: Create guidelines for organic community participation: how to introduce Mini-CRM without spamming, how to answer questions helpfully, how to avoid self-promotion pitfalls. Train community team.
- **inputs**: Community best practices, team training
- **outputs**: Community guidelines document
- **dependencies**: CMB-001
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Guidelines created, team trained

#### Task: CMB-003
- **title**: Launch organic presence in top 5 Facebook groups
- **description**: Join top 5 Facebook groups. Participate genuinely: answer questions, share relevant tips, mention Mini-CRM only when relevant. Build reputation before promotion. Track referral traffic from each group.
- **inputs**: Group access, participation plan
- **outputs**: Active presence in 5 groups
- **dependencies**: CMB-002
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Referral traffic from groups measurable

#### Task: CMB-004
- **title**: Create Mini-CRM branded Facebook group
- **description**: Create and launch "Artisans Mini-CRM Users" Facebook group. Seed with existing customers. Post weekly tips, success stories, and feature highlights. Grow to 500+ members.
- **inputs**: Group creation, content calendar, seed member list
- **outputs**: Branded group live with 500+ members
- **dependencies**: CMB-002
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Group created, 500+ members, weekly engagement

#### Task: CMB-005
- **title**: Build WhatsApp community groups by trade
- **description**: Create WhatsApp groups for plumbers, electricians, carpenters. Use as peer support channels. Moderate actively. Share tips and best practices. Track engagement.
- **inputs**: WhatsApp Business, group management
- **outputs**: 3 WhatsApp groups active
- **dependencies**: CMB-002
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Groups active, daily messages, retention high

#### Task: CMB-006
- **title**: Develop French artisan content marketing strategy
- **description**: Create content calendar for community: weekly tips, monthly success stories, seasonal advice (winterization, summer prep). Distribute via Facebook, WhatsApp, email. Track engagement.
- **inputs**: Content calendar, French artisan industry knowledge
- **outputs**: 6-month content calendar
- **dependencies**: CMB-003, CMB-004
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Content published consistently, engagement tracked

#### Task: CMB-007
- **title**: Create "Artisan of the Month" recognition program
- **description**: Feature outstanding Mini-CRM users in community: "Artisan of the Month" spotlight. Include interview, photo, tips shared. Make it aspirational. Distribute in all community channels.
- **inputs**: Nomination process, spotlight format
- **outputs**: Monthly artisan spotlight
- **dependencies**: CMB-004
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Spotlight published monthly, engagement measured

#### Task: CMB-008
- **title**: Partner with French trade influencers
- **description**: Identify 5-10 French artisan influencers (YouTube, Instagram). Offer free access in exchange for honest review. Track influencer-driven signups.
- **inputs**: Influencer research, outreach
- **outputs**: 3 influencer partnerships
- **dependencies**: CMB-001
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: marketing
- **validation**: Influencer content published, signups tracked

#### Task: CMB-009
- **title**: Build community FAQ and best practices hub
- **description**: Create a Notion or simple page collecting: common questions answered, Mini-CRM tips, artisan workflow best practices. Make it community-editable. Link from all community channels.
- **inputs**: Content, platform selection
- **outputs**: Community hub live
- **dependencies**: CMB-006
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Hub live, contributions tracked

#### Task: CMB-010
- **title**: Host monthly community Q&A sessions
- **description**: Host monthly live Q&A on Facebook/YouTube: "Ask the Mini-CRM team anything." Rotate between French artisan topics and product questions. Record and share highlights.
- **inputs**: Streaming setup, promotion
- **outputs**: Monthly Q&A sessions
- **dependencies**: CMB-004
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Sessions hosted, attendance tracked

#### Task: CMB-011
- **title**: Create shareable French artisan memes/media
- **description**: Develop shareable content: funny artisan memes, relatable situations ("When the client changes their mind for the 5th time"). Artisan humor that shares naturally. Track viral reach.
- **inputs**: Content creation, meme templates
- **outputs**: Regular meme posts
- **dependencies**: CMB-006
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Content shared organically, reach measured

#### Task: CMB-012
- **title**: Build community referral from Facebook groups
- **description**: Within Facebook groups, create referral mechanics: share your referral link, count successful referrals, monthly leaderboard. Make it a competition. Track referral conversions.
- **inputs**: Referral tracking, group mechanics
- **outputs**: Group referral program
- **dependencies**: VIR-001, CMB-003
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Referral program drives signups from groups

#### Task: CMB-013
- **title**: Create regional artisan meetups
- **description**: Organize 4 regional meetups per year in France: Paris, Lyon, Marseille, Bordeaux. Combine Mini-CRM training with peer networking. Track attendance and conversion.
- **inputs**: Venue, logistics, promotion
- **outputs**: 4 meetups per year
- **dependencies**: CMB-004
- **priority**: low
- **estimated_complexity**: high
- **agent_type**: marketing
- **validation**: Meetups hosted, attendance, conversion measured

---

### Category: Cohort Analysis Setup

#### Task: COH-001
- **title**: Define cohort segmentation framework
- **description**: Establish how to segment users: by signup month, by profession, by traffic source, by plan tier, by activation speed, by geography. Build cohort definitions in analytics.
- **inputs**: User data, segmentation options
- **outputs**: Cohort framework documented
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Cohort definitions approved and implemented

#### Task: COH-002
- **title**: Implement cohort retention analysis
- **description**: Build weekly/monthly retention curves for each cohort. Track: what % of users are still active at week 1, month 1, month 3, month 6, month 12. Compare across cohorts.
- **inputs**: Retention data, cohort tool
- **outputs**: Retention curves by cohort
- **dependencies**: COH-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Retention data updated weekly

#### Task: COH-003
- **title**: Create revenue cohort analysis
- **description**: Track revenue per cohort over time: MRR at month 0, 1, 3, 6, 12. Calculate ARPU by cohort. Identify which cohorts generate highest revenue.
- **inputs**: Revenue data, cohort definitions
- **outputs**: Revenue cohort report
- **dependencies**: COH-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Revenue cohorts tracked monthly

#### Task: COH-004
- **title**: Build activation cohort tracking
- **description**: Track activation rate (first job created) by cohort. Identify which signup cohorts activate fastest. Correlate activation speed with long-term retention and revenue.
- **inputs**: Activation data, cohort definitions
- **outputs**: Activation cohort report
- **dependencies**: COH-001, ACT-001
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Activation cohorts tracked, correlation with LTV measured

#### Task: COH-005
- **title**: Analyze feature adoption by cohort
- **description**: Track feature adoption rates across cohorts: which features are adopted faster by newer cohorts? Which features predict retention? Identify feature adoption patterns.
- **inputs**: Feature usage data, cohort definitions
- **outputs**: Feature adoption analysis
- **dependencies**: COH-001
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Feature adoption trends identified

#### Task: COH-006
- **title**: Create churn cohort analysis
- **description**: Analyze churn timing by cohort: when do users churn most often (week 1, month 1, month 3)? Which cohorts have lowest churn? What behaviors predict churn by cohort?
- **inputs**: Churn data, cohort definitions
- **outputs**: Churn cohort analysis
- **dependencies**: COH-001, CHR-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Churn timing patterns identified

#### Task: COH-007
- **title**: Build upgrade cohort tracking
- **description**: Track upgrade rates by cohort: what % upgrade within 30, 60, 90 days? Which cohorts upgrade fastest? What predicts upgrade?
- **inputs**: Upgrade data, cohort definitions
- **outputs**: Upgrade cohort report
- **dependencies**: COH-001, UPG-001
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Upgrade cohorts tracked

#### Task: COH-008
- **title**: Create traffic source cohort analysis
- **description**: Analyze cohorts by traffic source: organic search, paid ads, referral, social. Which sources produce highest-quality customers (best retention, revenue, upgrades)?
- **inputs**: Traffic source data, cohort definitions
- **outputs**: Traffic source cohort report
- **dependencies**: COH-001
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Best traffic sources identified

#### Task: COH-009
- **title**: Implement automated weekly cohort report
- **description**: Set up automated weekly email report: retention curves, key metrics by cohort, week-over-week changes, notable trends. Deliver to growth team every Monday.
- **inputs**: Cohort data, reporting tool, email
- **outputs**: Automated weekly report
- **dependencies**: COH-001, COH-002
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Report delivered weekly

#### Task: COH-010
- **title**: Build LTV cohort model
- **description**: Calculate true LTV by cohort: project future revenue based on observed retention and upgrade rates. Compare LTV by traffic source, profession, and plan tier.
- **inputs**: Cohort data, LTV model
- **outputs**: LTV cohort projections
- **dependencies**: COH-003, LTV-001
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: growth
- **validation**: LTV projections updated quarterly

---

### Category: A/B Testing Framework

#### Task: ABT-001
- **title**: Define A/B testing infrastructure and tools
- **description**: Select and implement A/B testing tool (Optimizely, VWO, or custom). Define test hierarchy: feature flags, frontend changes, email changes. Set up statistical significance calculator.
- **inputs**: Testing tools, technical requirements
- **outputs**: Testing infrastructure operational
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: growth
- **validation**: Testing tool deployed, team trained

#### Task: ABT-002
- **title**: Create test prioritization framework
- **description**: Develop ICE framework (Impact, Confidence, Ease) for prioritizing tests. Create test idea backlog with ICE scores. Review and reprioritize monthly.
- **inputs**: Test ideas, ICE scoring
- **outputs**: Test backlog with priorities
- **dependencies**: ABT-001
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Backlog prioritized, monthly reviews happening

#### Task: ABT-003
- **title**: Document testing best practices and processes
- **description**: Create testing playbook: how to write hypotheses, minimum sample size calculation, minimum test duration, how to interpret results, when to call a test.
- **inputs**: Testing experience, statistical methods
- **outputs**: Testing playbook
- **dependencies**: ABT-001
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Playbook documented, team trained

#### Task: ABT-004
- **title**: Implement test result tracking system
- **description**: Build centralized test results tracker: test name, hypothesis, winner, lift, confidence, revenue impact. Review monthly. Learn from wins and losses.
- **inputs**: Test results, tracking tool
- **outputs**: Test results dashboard
- **dependencies**: ABT-003
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: All tests tracked, learnings documented

#### Task: ABT-005
- **title**: Run pricing page headline tests (10+ variants)
- **description**: Test 10+ headline variants on pricing page. Measure conversion rate per variant. Identify winning headline. Document why it won.
- **inputs**: Headline variants, testing tool
- **outputs**: Headline test results
- **dependencies**: ABT-002, ABT-003
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Winning headline implemented, >10% lift

#### Task: ABT-006
- **title**: Test CTA button variations (color, copy, placement)
- **description**: Test CTA button: red vs green vs blue, "Start Free Trial" vs "Get Started Free" vs "Try Now", above fold vs below feature list. Measure click-through and conversion.
- **inputs**: Button variants, testing tool
- **outputs**: CTA test results
- **dependencies**: ABT-002, ABT-003
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Winning CTA deployed

#### Task: ABT-007
- **title**: Test onboarding flow variations
- **description**: Test onboarding flow variants: step-by-step wizard vs blank canvas, with sample data vs without, with video tutorial vs text only. Measure time-to-activation.
- **inputs**: Onboarding variants, testing tool
- **outputs**: Onboarding test results
- **dependencies**: ABT-002, ACT-002
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Winning onboarding deployed

#### Task: ABT-008
- **title**: Implement multi-page funnel tests
- **description**: Test complete funnel variations: 3-step checkout vs 1-page checkout, with progress bar vs without, with trust signals throughout vs at end. Measure end-to-end conversion.
- **inputs**: Funnel variants, tracking
- **outputs**: Funnel test results
- **dependencies**: ABT-002, TRC-014
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: growth
- **validation**: Winning funnel deployed

#### Task: ABT-009
- **title**: Create email subject line test library
- **description**: Test 20+ email subject line variations. Document open rates by type: question vs statement, emoji vs no emoji, short vs long. Build best-practice library.
- **inputs**: Subject line variants, email data
- **outputs**: Subject line playbook
- **dependencies**: ABT-002
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Subject line best practices documented

#### Task: ABT-010
- **title**: Test social proof placement and format
- **description**: Test social proof variants: testimonials vs logos, single testimonial vs multiple, before CTA vs after CTA. Measure conversion impact.
- **inputs**: Social proof variants, testing tool
- **outputs**: Social proof test results
- **dependencies**: ABT-002
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Optimal social proof placement identified

#### Task: ABT-011
- **title**: Run quarterly testing retrospective
- **description**: Every quarter, review all tests run: wins, losses, nulls. Extract learnings. Update testing roadmap. Celebrate test-driven wins.
- **inputs**: Test results, retrospective framework
- **outputs**: Quarterly retrospective
- **dependencies**: ABT-004
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Retrospectives happening quarterly

---

### Category: Growth Experiments Backlog

#### Task: GEB-001
- **title**: Build centralized experiment backlog
- **description**: Create backlog of all experiment ideas: sourced from team, support tickets, NPS comments, competitor analysis. Prioritize with ICE scores. Maintain in Notion or similar.
- **inputs**: Experiment ideas, prioritization
- **outputs**: Live backlog with 50+ ideas
- **dependencies**: ABT-002
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Backlog active, ideas added weekly

#### Task: GEB-002
- **title**: Document experiment results and learnings
- **description**: After each experiment, document: hypothesis, results, learnings, next actions. Build institutional knowledge. Review learnings when designing new tests.
- **inputs**: Experiment documentation template
- **outputs**: Experiment wiki
- **dependencies**: GEB-001
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: All experiments documented

#### Task: GEB-003
- **title**: Run weekly experiment planning session
- **description**: Weekly 30-min session: review top backlog items, assign owners, confirm test details, schedule for next sprint. Keep experiment velocity high.
- **inputs**: Backlog, meeting cadence
- **outputs**: Weekly planning notes
- **dependencies**: GEB-001
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Weekly sessions happening

#### Task: GEB-004
- **title**: Track experiment velocity and throughput
- **description**: Track: how many experiments launched per week/month, average test duration, % of ideas that get tested. Set velocity targets.
- **inputs**: Experiment data, velocity metrics
- **outputs**: Velocity dashboard
- **dependencies**: GEB-001
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Velocity tracked, >4 experiments/week

#### Task: GEB-005
- **title**: Create experiment templates
- **description**: Standardize experiment templates: hypothesis format, success metrics, minimum sample size calculator, result interpretation guide. Reduce friction for new tests.
- **inputs**: Template design, testing best practices
- **outputs**: Experiment templates ready
- **dependencies**: GEB-001, ABT-003
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Templates used for all new tests

#### Task: GEB-006
- **title**: Identify 20 quick-win experiments
- **description**: From backlog, identify 20 experiments that are low-effort, high-potential: copy changes, button colors, form fields, email timing. Run these first to build momentum.
- **inputs**: Backlog analysis
- **outputs**: 20 quick-win experiments identified
- **dependencies**: GEB-001
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Quick wins prioritized and running

#### Task: GEB-007
- **title**: Map experiments to growth funnel stages
- **description**: Tag all experiments by funnel stage: awareness, acquisition, activation, retention, referral, revenue. Ensure balanced experiment portfolio across all stages.
- **inputs**: Funnel mapping, backlog tags
- **outputs**: Balanced experiment portfolio
- **dependencies**: GEB-001
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: All funnel stages represented

#### Task: GEB-008
- **title**: Build experiment-to-roadmap handoff process
- **description**: When an experiment wins, define process to handoff to product/engineering roadmap. Document requirements, success criteria, and timeline.
- **inputs**: Handoff template, roadmap process
- **outputs**: Handoff process documented
- **dependencies**: GEB-002
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Wins properly handoffered

#### Task: GEB-009
- **title**: Source experiment ideas from customer feedback
- **description**: Monthly review of support tickets, NPS comments, and interviews. Extract experiment ideas directly from customer language. Prioritize ideas that address real customer pain.
- **inputs**: Feedback sources, idea extraction
- **outputs**: Customer-sourced experiments
- **dependencies**: VOC-004
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Ideas extracted monthly

#### Task: GEB-010
- **title**: Create experiment ROI calculation
- **description**: For major experiments, calculate ROI: estimated revenue impact × probability of success − experiment cost. Prioritize high-ROI experiments.
- **inputs**: Experiment data, revenue estimates
- **outputs**: ROI calculations
- **dependencies**: GEB-001
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: ROI factored into prioritization

---

### Category: Competitor Response Playbook

#### Task: CRP-001
- **title**: Map French artisan CRM competitive landscape
- **description**: Identify all competitors: HubSpot, Zoho, Salesforce, Pennypaw, Fieldmate, and any new entrants. Document pricing, features, positioning, market share estimates.
- **inputs**: Competitor research, market data
- **outputs**: Competitor landscape map
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Landscape documented and updated quarterly

#### Task: CRP-002
- **title**: Monitor competitor product changes weekly
- **description**: Set up weekly competitor monitoring: new feature releases, pricing changes, marketing campaigns. Track in a shared doc. Alert team to significant changes.
- **inputs**: Monitoring tools, alert system
- **outputs**: Weekly competitor digest
- **dependencies**: CRP-001
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Weekly monitoring active

#### Task: CRP-003
- **title**: Create competitor feature comparison matrix
- **description**: Build detailed feature matrix: Mini-CRM vs each competitor. Update quarterly. Identify gaps to address in roadmap. Identify advantages to emphasize in marketing.
- **inputs**: Feature data, competitor analysis
- **outputs**: Feature comparison matrix
- **dependencies**: CRP-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Matrix maintained quarterly

#### Task: CRP-004
- **title**: Document competitive positioning statements
- **description**: Create battle cards: how to position against each major competitor. Include competitor's weaknesses, Mini-CRM's advantages, objection handling. Train sales and CS.
- **inputs**: Competitive analysis, positioning
- **outputs**: Battle cards ready
- **dependencies**: CRP-001, CRP-003
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Battle cards complete, team trained

#### Task: CRP-005
- **title**: Define competitor pricing response thresholds
- **description**: If competitor cuts price by X%, define our response: no action, promotional counter, or value-add response. Set thresholds in advance to respond quickly.
- **inputs**: Pricing strategy, competitive data
- **outputs**: Pricing response playbook
- **dependencies**: CRP-001
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Playbook defined, approved

#### Task: CRP-006
- **title**: Build competitor feature response process
- **description**: When competitor releases popular feature, define process: evaluate in 2 weeks, decide build/buy/partner, communicate Mini-CRM advantage. Don't react to everything — choose strategic responses.
- **inputs**: Response process, roadmap integration
- **outputs**: Feature response process
- **dependencies**: CRP-002
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Process defined, responses tracked

#### Task: CRP-007
- **title**: Create win/loss analysis against competitors
- **description**: Track all deal wins and losses where competitor was mentioned. Document why we won or lost. Share learnings with team. Update battle cards.
- **inputs**: Sales data, win/loss tracking
- **outputs**: Win/loss analysis quarterly
- **dependencies**: CRP-004
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Quarterly analysis complete

#### Task: CRP-008
- **title**: Monitor competitor customer reviews
- **description**: Track competitor reviews on G2, Capterra, Google Play, App Store. Identify common complaints. Use to improve Mini-CRM and inform marketing.
- **inputs**: Review monitoring, analysis
- **outputs**: Competitor review analysis
- **dependencies**: CRP-002
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Reviews monitored monthly

#### Task: CRP-009
- **title**: Create competitor messaging response matrix
- **description**: When competitor runs marketing campaign, prepare response: whether to respond, what to say, which channels. Define thresholds for when competitor claims require rebuttal.
- **inputs**: Marketing monitoring, response guidelines
- **outputs**: Messaging response matrix
- **dependencies**: CRP-002
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Response matrix ready

#### Task: CRP-010
- **title**: Develop differentiation narrative per persona
- **description**: Create differentiation story per persona: why plumber should choose Mini-CRM over HubSpot, why electrician should choose us over Pennypaw. Tailor messaging to pain points.
- **inputs**: Persona research, competitive data
- **outputs**: Persona-specific differentiation
- **dependencies**: CRP-003
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Differentiation stories ready for each persona

---

### Category: Seasonal Campaign Calendar (post-winter, renovation season)

#### Task: SCC-001
- **title**: Map French artisan seasonal calendar
- **description**: Research French artisan seasons: post-winter (March-April) emergency repairs, pre-summer (May-June) installations, renovation season (Sept-Nov), year-end (December). Identify peak demand periods.
- **inputs**: Industry research, artisan calendars
- **outputs**: Seasonal calendar document
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Calendar documented

#### Task: SCC-002
- **title**: Build annual campaign calendar
- **description**: Create 12-month campaign calendar aligned with seasonal demand. Plan campaigns 2 months ahead. Include: email campaigns, social content, paid ads, PR.
- **inputs**: Seasonal calendar, marketing inventory
- **outputs**: 12-month campaign calendar
- **dependencies**: SCC-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Calendar approved and distributed

#### Task: SCC-003
- **title**: Create post-winter campaign ("Spring Renovation")
- **description**: Launch March-May campaign targeting post-winter renovation rush. Theme: "Get your business organized before the busy season." Email sequence, social content, paid ads. Track conversions.
- **inputs**: Campaign assets, targeting
- **outputs**: Spring campaign live
- **dependencies**: SCC-002
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Campaign deployed, conversions tracked

#### Task: SCC-004
- **title**: Launch summer installation campaign
- **description**: Launch May-July campaign for summer installation projects. Theme: "Manage more jobs, stress less." Target during home improvement season. A/B test messaging vs spring campaign.
- **inputs**: Campaign assets, testing
- **outputs**: Summer campaign live
- **dependencies**: SCC-003
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Campaign deployed, performance compared to spring

#### Task: SCC-005
- **title**: Create back-to-business September campaign
- **description**: Launch August-September "back to business" campaign. Artisans return from vacation ready to organize. Theme: "New season, new system." Time with annual planning season.
- **inputs**: Campaign assets
- **outputs**: September campaign live
- **dependencies**: SCC-002
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Campaign deployed during September

#### Task: SCC-006
- **title**: Build year-end holiday campaign
- **description**: Launch November-December campaign. Theme: "End the year organized." Offer annual plan discount. Target business planning and tax season. Track annual plan conversions.
- **inputs**: Campaign assets, annual offer
- **outputs**: Year-end campaign live
- **dependencies**: SCC-002, MAP-007
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Year-end campaign deployed, annual conversions tracked

#### Task: SCC-007
- **title**: Create "slow season" engagement campaigns
- **description**: For slower months (July-August, January), create engagement campaigns: tips for using slow season to organize, product tutorial series, community building. Focus on retention, not acquisition.
- **inputs**: Seasonal analysis, content calendar
- **outputs**: Slow-season campaigns
- **dependencies**: SCC-002
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Retention impact during slow season measured

#### Task: SCC-008
- **title**: Implement seasonal upgrade promotions
- **description**: Align upgrade promotions with seasonal demand: in busy season, emphasize efficiency gains; in slow season, emphasize system organization. Test seasonal upgrade messaging.
- **inputs**: Seasonal calendar, upgrade messaging
- **outputs**: Seasonal upgrade campaigns
- **dependencies**: SCC-002, UPG-010
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Seasonal messaging outperforms generic

#### Task: SCC-009
- **title**: Build trade-specific seasonal content
- **description**: Create seasonal content per trade: "Plumber's spring checklist," "Electrician's summer prep guide," "Carpenter's fall project calendar." Distribute in trade communities. Track engagement.
- **inputs**: Trade-specific content, distribution
- **outputs**: Trade content published seasonally
- **dependencies**: SCC-001, CMB-006
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Trade content engagement tracked

#### Task: SCC-010
- **title**: Analyze seasonal campaign performance
- **description**: After each campaign, analyze performance by season: cost per acquisition, conversion rate, revenue. Compare seasons. Update next year's calendar based on learnings.
- **inputs**: Campaign data, analysis
- **outputs**: Seasonal performance analysis
- **dependencies**: SCC-002
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Analysis complete, calendar updated

---

### Category: Upsell Triggers (when to offer Pro/Business)

#### Task: UPT-001
- **title**: Define comprehensive upsell trigger catalog
- **description**: Document all behavioral triggers that indicate upgrade readiness: job volume milestones, team size growth, feature usage patterns, frequent support, time-based milestones. Build trigger library.
- **inputs**: Usage data, upgrade correlation analysis
- **outputs**: Upsell trigger catalog
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Trigger catalog complete with 20+ triggers

#### Task: UPT-002
- **title**: Implement real-time upsell trigger detection
- **description**: Build system to detect upsell triggers in real-time: when user hits trigger, flag for upsell action. Route to appropriate channel: in-app, email, or CS outreach.
- **inputs**: Trigger catalog, detection logic, routing
- **outputs**: Real-time trigger detection
- **dependencies**: UPT-001
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: product
- **validation**: Triggers detected and actioned

#### Task: UPT-003
- **title**: Create trigger-specific upgrade offers
- **description**: For each major trigger, craft specific upgrade offer: "You have 5 team members — Pro includes unlimited team." Make offers feel like solutions, not sales.
- **inputs**: Trigger catalog, offer variants
- **outputs**: Trigger-specific offers
- **dependencies**: UPT-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Offers deployed for each major trigger

#### Task: UPT-004
- **title**: Implement in-app upsell banners at trigger moments
- **description**: When trigger detected in-app, show contextual upsell banner. Example: when adding 3rd team member, banner appears: "Pro includes up to 10 team members. Upgrade free for 30 days." Track clicks and conversions.
- **inputs**: Banner system, trigger detection, offer variants
- **outputs**: In-app upsell banners live
- **dependencies**: UPT-002, UPT-003
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Banners display at correct moments, conversion measurable

#### Task: UPT-005
- **title**: Create trigger-based email sequences
- **description**: For each major trigger, create targeted email: arrives within 24h of trigger detection. Email shows value of upgrade in context of the trigger. Include specific benefit and CTA.
- **inputs**: Trigger data, email templates
- **outputs**: Trigger-based email sequences
- **dependencies**: UPT-003
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: marketing
- **validation**: Emails deploying for triggers, open and click rates tracked

#### Task: UPT-006
- **title**: Build upsell moment tracking dashboard
- **description**: Track all upsell moments: how many triggered, how many presented with offer, how many clicked, how many converted. Calculate offer-to-click and click-to-conversion rates.
- **inputs**: Upsell data, dashboard tool
- **outputs**: Upsell dashboard
- **dependencies**: UPT-002
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Dashboard live, conversion funnel visible

#### Task: UPT-007
- **title**: Test trigger timing optimization
- **description**: Test when to show upsell after trigger: immediately vs 24h vs 7 days. Some triggers may need "cooldown" period. Measure conversion rate by timing.
- **inputs**: Test setup, trigger data
- **outputs**: Optimal timing per trigger type
- **dependencies**: UPT-004
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Timing optimized for each trigger

#### Task: UPT-008
- **title**: Create urgency-based upsell for high-intent users
- **description**: For users showing very strong upgrade intent (visited pricing multiple times, used premium features), add urgency: "This pricing ends in 48 hours." Test urgency impact on conversion.
- **inputs**: Intent signals, urgency messaging
- **outputs**: Urgency upsell deployed
- **dependencies**: UPT-003
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Urgency increases conversion rate

#### Task: UPT-009
- **title**: Implement usage-based billing upgrade path
- **description**: Allow users to start on Solo and automatically upgrade when they exceed usage limits (e.g., auto-charge for overage vs flat upgrade). Test which model customers prefer.
- **inputs**: Usage tracking, billing integration
- **outputs**: Usage-based upgrade tested
- **dependencies**: UPT-001
- **priority**: low
- **estimated_complexity**: high
- **agent_type**: product
- **validation**: Usage billing tested, customer preference known

#### Task: UPT-010
- **title**: Build upsell success story library by trigger
- **description**: Collect success stories tied to specific triggers: "I upgraded when I hit 50 jobs/month" story from a plumber. Use in upsell communications for same trigger.
- **inputs**: Customer interviews, trigger mapping
- **outputs**: Success story library per trigger
- **dependencies**: UPT-003
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Stories available for major triggers

#### Task: UPT-011
- **title**: Create A/B test for upsell messaging variants
- **description**: For each major trigger, test 3+ upsell message variants: benefit-focused vs problem-focused vs social-proof-focused. Identify winning message per trigger.
- **inputs**: Message variants, A/B test setup
- **outputs**: Winning messages per trigger
- **dependencies**: UPT-003
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Optimized messaging deployed

#### Task: UPT-012
- **title**: Implement "upgrade preview" experience
- **description**: When showing upsell, allow users to "preview" Pro features for 7 days before committing. Track if preview increases upgrade conversion vs immediate offer.
- **inputs**: Preview logic, tracking
- **outputs**: Preview experience tested
- **dependencies**: UPG-007
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Preview increases conversion rate

#### Task: UPT-013
- **title**: Build CS-triggered upsell workflow
- **description**: Train CS team to identify upsell opportunities during support calls. When CS sees trigger, they can offer upgrade with special discount. Track CS-attributed upgrades.
- **inputs**: CS training, trigger list, discount approval
- **outputs**: CS upsell workflow
- **dependencies**: UPT-001
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: CS upsell attribution tracked

#### Task: UPT-014
- **title**: Analyze upgrade path friction points
- **description**: Identify where upgrade path breaks: confusing plan differences, slow checkout, unclear billing. Remove friction. Track if friction removal increases upgrade rate.
- **inputs**: Upgrade funnel analysis, user feedback
- **outputs**: Friction points removed
- **dependencies**: UPT-006
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Upgrade funnel conversion improved

#### Task: UPT-015
- **title**: Create annual upgrade promotion at usage peaks
- **description**: At seasonal peaks (spring, fall), when users are busiest, offer annual plan upgrade with bonus: "Upgrade to annual and get 4 months free." Time with natural upgrade readiness.
- **inputs**: Seasonal calendar, annual offer
- **outputs**: Seasonal upgrade promotion
- **dependencies**: SCC-008
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: marketing
- **validation**: Seasonal upgrade promotion drives annual conversions

---

### Additional High-Priority Growth Tasks

#### Task: GRW-001
- **title**: Build growth model and forecast
- **description**: Create comprehensive growth model: MRR forecast, customer count by cohort, upgrade revenue, churn projections. Update monthly. Use for planning and fundraising.
- **inputs**: Historical data, growth assumptions
- **outputs**: Growth model and 12-month forecast
- **dependencies**: LTV-001, COH-003
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: growth
- **validation**: Model live, updated monthly

#### Task: GRW-002
- **title**: Implement OKR tracking for growth
- **description**: Define OKRs for growth team: conversion rate target, activation target, churn target, LTV target. Track weekly. Review monthly.
- **inputs**: OKR framework, current metrics
- **outputs**: OKR dashboard
- **dependencies**: GRW-001
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: OKRs tracked weekly, reviewed monthly

#### Task: GRW-003
- **title**: Create growth team communication rhythm
- **description**: Establish weekly growth team sync: test reviews, metric updates, blocker identification. Monthly leadership review. Quarterly strategy session.
- **inputs**: Meeting cadence, agenda
- **outputs**: Communication rhythm established
- **dependencies**: GRW-002
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Meetings happening on schedule

#### Task: GRW-004
- **title**: Build competitive moat analysis
- **description**: Identify and quantify Mini-CRM's competitive moat: community, network effects, data, brand, integration ecosystem. Prioritize moat-building investments.
- **inputs**: Competitive analysis, market data
- **outputs**: Moat analysis and strategy
- **dependencies**: CRP-001, CMB-001
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: growth
- **validation**: Moat strategy documented

#### Task: GRW-005
- **title**: Create customer data platform foundation
- **description**: Build unified customer data platform: combine signup data, usage data, support data, billing data. Create single customer view. Enable personalized marketing and product decisions.
- **inputs**: Data sources, CDP tool selection
- **outputs**: CDP operational
- **dependencies**: COH-001
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: growth
- **validation**: Single customer view available

#### Task: GRW-006
- **title**: Implement marketing attribution model
- **description**: Define attribution model: first touch, last touch, linear, or time-decay. Implement in analytics. Understand which channels drive qualified signups and conversions.
- **inputs**: Marketing data, attribution tool
- **outputs**: Attribution model live
- **dependencies**: GRW-005
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Attribution data available for decisions

#### Task: GRW-007
- **title**: Build customer segmentation for personalized marketing
- **description**: Create detailed customer segments: by profession, by company size, by usage level, by lifecycle stage, by revenue tier. Enable personalized campaigns per segment.
- **inputs**: Customer data, segment definitions
- **outputs**: Segment library
- **dependencies**: GRW-005
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: growth
- **validation**: Segments available for marketing

#### Task: GRW-008
- **title**: Create self-hosted customer success metrics
- **description**: Since Mini-CRM is self-hosted, track: installation health, version updates applied, data backup frequency. Correlate with churn to identify at-risk self-hosted customers.
- **inputs**: Self-hosted telemetry, churn data
- **outputs**: Self-hosted health scores
- **dependencies**: CHR-001
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: growth
- **validation**: Self-hosted health correlated with retention

#### Task: GRW-009
- **title**: Build growth team hiring plan
- **description**: Assess growth team capacity: what skills missing, what headcount needed to execute roadmap. Create 6-month hiring plan with clear priorities.
- **inputs**: Team assessment, roadmap
- **outputs**: Hiring plan
- **dependencies**: GRW-002
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Hiring plan approved

#### Task: GRW-010
- **title**: Create growth knowledge sharing system
- **description**: Document all growth learnings: test results, campaign performance, customer insights. Make searchable. Onboard new team members quickly.
- **inputs**: Documentation system
- **outputs**: Knowledge base live
- **dependencies**: GEB-002
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: growth
- **validation**: Knowledge base active and used

---

*Document Version: 1.0*
*Last Updated: 2026-03-30*
*Owner: Growth Team*
*Review Cadence: Monthly*
