# C Product Strategist — Pulse 0129

## Challenge: The "WhatsApp First" Sprint 0 Assumption (D40)

---

### The Core Assumption Under Fire

D40 states WhatsApp Business API is "non-negotiable" for Path B activation and belongs in Sprint 0. I'm arguing this is backwards — and that committing WhatsApp to Sprint 0 is a classic case of building infrastructure before we know if anyone wants to live in the house.

---

### Sprint 0 Reality Check

WhatsApp Business API is not a checkbox. Here's what Sprint 0 actually entails:

- **Meta Business Verification**: 2–7 business days (sometimes longer)
- **WhatsApp Business Account setup + phone number compliance**: 1–2 days
- **Message templates approval**: Another 1–3 days (if approved at all on first submission)
- **Backend integration + retry logic + opt-out handling**: 2–3 days

That's 6–14 days minimum for a team that thinks it has 5 days. We've already burned Sprint 0 on someone else's platform before shipping a single feature to a real user.

---

### The Value Proposition Hole

What does WhatsApp *do* for v1 Path B users?

- Send digest notifications? → Users are dormant. They don't open the app. Why would they open a WhatsApp message?
- Push upgrade prompts? → D141 explicitly says "no sales language." So what's the message?
- Remind them to send quotes? → Path B users haven't sent a quote in 14+ days. A WhatsApp nudge doesn't fix a broken habit.

At v1, there is **no premium content worth pushing**. The Free tier IS the product. WhatsApp is an empty pipe — we're spending Sprint 0 building a pipeline to deliver nothing.

---

### The Real Activation Channel

Here's what we know about Path B users:
- They downloaded the app (acquisition worked)
- They set up 1-2 clients and sent a few quotes (activation worked)
- They stopped opening the app for 14+ days (retention broke)

The retention problem is an **app problem**, not a **notification problem**. You cannot fix a broken value loop by adding a second broken loop.

If the app doesn't deliver enough recurring value for users to open it voluntarily, no amount of WhatsApp nudges will. The digest goes unread. The notification gets blocked. The user churns quietly.

---

### What Should Actually Be in Sprint 0?

1. **The quote-to-payment loop** — make sure users can actually complete the core job (devis → facture → relance)
2. **Onboarding that creates habits** — the first 7 days matter; build that before building external channels
3. **App notification infrastructure** — push notifications via Expo Notifications are simpler, faster to ship, and directly tied to in-app events

WhatsApp is a *retention channel for a product that's already delivering value*. It's not a magic switch that makes a dormant user care.

---

### The Real Question We Should Be Asking

D40 says WhatsApp is "non-negotiable for Path B activation." But activation already happened — they downloaded and used it. What we actually need is **Path B re-activation**, which is a retention problem.

We're conflating acquisition channels with retention channels. Sprint 0 should solve the problem users actually have: the app not being valuable enough to open. Not building a WhatsApp pipeline to prod silent users.

---

## Summary Table

| ID | Topic | My Position |
|----|-------|-------------|
| D40 | WhatsApp in Sprint 0 | Reject — wrong sprint, wrong problem, Meta verification alone blows the timeline |
| D141 | Bi-weekly WhatsApp digest | Premature — empty pipe with no premium content to deliver |
| D110 | Soft limit friction for Path B conversion | Defer — don't build conversion mechanics until retention works |
