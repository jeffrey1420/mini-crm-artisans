# D143 Product Strategist — Pulse

**Assumptions challenged:** D40 (channel is secondary), D141 (stay-in-touch digest undefined)
**Pulse timestamp:** 2026-03-31T01:15

---

## Challenge 1: D40 Is Wrong for Path B — Channel IS the Primary Activation Lever

### The Assumptions Being Challenged

**From D40/D43/D46/D63 (resolved):** "Channel is secondary to Free tier output design. First build something worth coming back to, then debate how to reach users. The 'situation financière' snapshot is the Free tier's primary value output. Until it exists, notification channel debates are premature."

**The problem with this framing for Path B:** It assumes the artisan's biggest barrier is that the product doesn't give them enough value to return. For Path A (formal-devis users), this may be true. For Path B (verbal-agreement artisans), it's backwards. The Path B artisan already has value in front of him — his job list, his client notes, his job-site data. The barrier is not product quality. The barrier is that the product lives in a channel (email, app notifications) he doesn't check when he's on a job site.

### The Path B Persona Context

The Path B artisan:
- Age 45-55, French BTP trades (plumber, electrician, roofer, carpenter)
- Primary work environment: job sites, vehicle, supplier yards — not a desk
- Rarely at a computer during working hours
- WhatsApp is his primary business communication channel — with clients, suppliers, and colleagues
- Email is checked once a day at most, usually in the evening at home
- Push notifications from an app he barely opened are invisible to him
- His phone is his business hub, and WhatsApp is the hub within the hub

### The Core Argument

**For Path B, if the engagement channel is not WhatsApp, the Free tier output — however good — is never seen.**

The D40 framework says: design the output first, then pick a channel to deliver it. This treats channel as a delivery problem (last-mile logistics). For Path B, channel is not delivery — it is the entire question. If the product cannot meet the artisan where he already is (WhatsApp), it doesn't matter what the product contains.

Consider the mechanics:
1. Artisan downloads the app, logs 3 jobs in Week 1
2. He's on job sites all day, switching between WhatsApp and phone calls
3. He gets an email from the app: weekly summary, situation financière
4. He sees it at 9pm, is tired, skims it, closes it
5. He doesn't open the app because the notification didn't match his context
6. Week 3: he hasn't opened the app in 10 days, his job list is stale
7. He forgets why he downloaded it

Now compare:
1. Same artisan downloads the app, logs 3 jobs in Week 1
2. He gets a WhatsApp message on Sunday at 7pm: "📊 Votre semaine — 3 devis créés, 2 clients ajoutés"
3. He opens it in WhatsApp, sees his jobs listed, clicks one to check details
4. The app opens. He's back in the product.
5. Habit loop: WhatsApp → product interaction → job logging → WhatsApp

**The channel is not secondary for Path B. The channel IS the activation mechanism.**

### The Engagement Channel Hierarchy for Path B

| Channel | Path B reach | Notes |
|---------|-------------|-------|
| WhatsApp | Near-constant during work hours | Primary business channel |
| Push notification | Only if app is open | Low priority, cleared quickly |
| Email | Once per evening, often not at all | Low urgency, low open rate |
| In-app | Requires deliberate re-opening | Dormancy kills this |

**For Path B, WhatsApp is not "a good channel to add." It is the only reliable channel.**

### Position on D40

**D40 should be REFINED, not RESTATED.** The blanket verdict "channel is secondary" applies to Path A (formal-devis users who have email-checking habits and work at desks occasionally). For Path B, channel IS the primary variable — because the artisan's context prevents him from receiving any output unless it arrives in his existing communication channel.

**Proposed resolution:**
- D40: RESTATED with a caveat — "For Path A (formal-devis), channel is secondary to output design. For Path B (verbal-agreement, job-site artisans), channel IS the primary activation lever. WhatsApp is not optional for Path B — it is the activation mechanism itself. Sprint 0 notification architecture must treat WhatsApp as non-negotiable for Path B."

---

## Challenge 2: The "Stay in Touch" Digest for Path B Was Identified But Never Specified

### What the Debate Log Says

D141 (pulse 00:58) states: "Path B has a separate retention mechanism: The recurring 'stay in touch' digest for dormant Free users (D89) applies to Path B when they've been inactive 14+ days."

D89 states: "Recurring digest for dormant Free users: kept as a separate 'stay in touch' mechanism."

**Neither D89 nor D141 specifies:** what the digest contains, what frequency, what channel, what the conversion mechanism is, or what the activation trigger specifically entails.

The retention mechanism for Path B is undefined. It was identified as the solution and then not designed.

### The Assumptions Being Challenged

**Implicit assumption in D89/D141:** "The 'stay in touch' digest is a known pattern that will be specified later." There is no evidence anyone has defined what it contains or how it drives conversion.

**Second implicit assumption:** "Email is the default digest channel." The debate log never states this, but the absence of WhatsApp in the D89/D141 framing suggests email. This assumption is wrong for Path B.

### The Core Argument: Define the Digest Now

The digest cannot be left as a placeholder. Here is the complete specification:

---

### "Stay in Touch" Digest — Complete Specification

**Trigger conditions (ALL must be true):**
- User is on Free tier
- User has logged at least 1 job ever (distinguishes "downloaded but never used" from "used but dormant")
- User has been inactive for 14+ consecutive days (inactivity = no app open, no job logged)
- User is Path B (verbal-agreement workflow — no formal devis created, no "situation financière" notification ever sent)

**Frequency:** Bi-weekly (every 14 days) while dormant. If user remains dormant after first digest, send again at Day 28, Day 42. Cap at 3 digests, then switch to a "we miss you" final message with a "reply to reactivate" mechanism.

**Channel:** WhatsApp Business API (primary). Not email. Not push.

**Why WhatsApp, not email, for Path B:**
- Email open rates for French artisans on Free tier apps: estimated 15-25% at best
- WhatsApp message open rates: 98% within 4 hours
- WhatsApp messages appear in the artisan's primary business communication channel
- WhatsApp messages survive the evening fatigue that kills email opens ("I'll read that tomorrow" → never)

**Content — what fields and metrics:**

The digest should feel like a friend's check-in, not a product notification. Plain text, short sentences, no marketing language.

```
Sujet: [App Name] — Votre，活
Aucun附件. Simple，活

Bonjour [Prénom],

Voilà ce qu'on a pour vous cette semaine :
• [X] emploi enregistré
• [X] clients dans votre portefeuille  
• [X] devis en attente
• Dernière connexion : il y a [X] jours

👉 [Lien direct vers l'app — "Voir mes emplois"]

Une question ? Appelez-moi — [numéro Louis]

À bientôt,
[App Name]
```

**What this digest does NOT contain:**
- No mention of upgrade or paid features
- No comparison to Premium tiers
- No urgency language ("vos données sont limitées")
- No financial metrics (inappropriate for dormant user who hasn't been using the product)

**What this digest does:**
- Reflects back the user's own data (ownership signal)
- Shows a "last connection: X days ago" (dormancy awareness without blame)
- Provides a single, low-friction re-entry link to the app
- Ends with a human contact (Louis's number) — relationship, not sales
- Never sells in the digest itself

**The conversion mechanism — how it drives upgrade without a formal trigger event:**

This is the hardest part. Path B has no formal devis event to trigger conversion. The digest cannot rely on a "situation financière" moment. The conversion must emerge from the digest's content itself, not from a separate trigger.

**The mechanism:**
1. Digest shows the artisan his dormant job list and client data
2. The artisan sees the value of his data (organized, accessible, not lost on a paper note)
3. He clicks through to the app and starts using it again
4. The re-engagement produces a new job event
5. After 3-4 digests across 6-8 weeks, he has re-established the habit
6. **The upgrade trigger is now the same as Path A:** he hits the Free tier limit (5 clients, 3 jobs, or 2 devis depending on what's actually limiting)
7. OR: he experiences the product's value and voluntarily upgrades because "this is actually useful"

**The digest is not itself a conversion event. It is a re-engagement mechanism that restores the user to a state where the standard limit-hit trigger can fire.** The 14+ day dormancy prevented the natural usage-to-conversion flow. The digest bridges the gap.

**Why no hard conversion ask in the digest:**
A conversion ask in a "stay in touch" digest (e.g., "Upgrade to Premium for €29/month") would destroy the relationship signal. The digest's value is its authenticity — it's Louis checking in, not the product selling. Any sales language breaks the pattern.

### Position on D89/D141

**D89/D141 is RESTATED with full digest specification:**

| Digest parameter | Value |
|---|---|
| Trigger | 14+ days dormant AND ≥1 job logged ever AND Path B (no formal devis workflow) |
| Frequency | Bi-weekly (Day 14, 28, 42) |
| Channel | WhatsApp Business API (primary) |
| Content | Plain text, French, user activity metrics, single re-entry CTA, Louis contact |
| Conversion mechanism | Re-engagement restores user to active state → natural limit-hit trigger fires |
| Hard conversion ask | NONE in digest itself |
| Limit | 3 digests (6 weeks) then final "we miss you" + reactivation reply mechanism |

---

## Summary of Proposed Resolutions

| ID | Topic | Proposed Resolution |
|----|-------|---------------------|
| D40 | Engagement channel | REFINED — Path B: channel IS the primary activation lever. WhatsApp is non-negotiable for Path B. Sprint 0 must build WhatsApp Business API integration as a first-class notification channel, not a nice-to-have. |
| D89/D141 | Stay in touch digest | RESTATED with full specification — WhatsApp bi-weekly digest for 14+ day dormant Path B Free users. Plain text, user data reflected, single re-entry CTA, no sales language. Converts by re-establishing usage habit until natural limit-hit trigger fires. |

---

*Pulse D143 — Product Strategist. Channel question is primary for Path B. Digest is now specified.*
