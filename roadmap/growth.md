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