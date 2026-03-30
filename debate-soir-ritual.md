## Debate: The 8pm "Soir Ritual" Push Is Unvalidated Stereotyping

**Challenged Decision:** D83 — "situation financière = server-computed push notification at 8pm Paris" as "the soir ritual"

**Position:** The 8pm fixed notification is a **cultural stereotype** masquerading as user research. It assumes Marc does admin in a dedicated evening slot — and that assumption was never validated with real artisans.

---

### Core Argument

D83 resolved: "The appointment comes to him. 8pm Paris delivery = his natural admin time, after kids are in bed, when he's doing chiffrage and devis work."

This framing is doing enormous work. It claims to know Marc's evening routine with precision — 8pm, after the children are asleep, during a dedicated admin window. But where does this claim come from? Not from observing Marc. Not from guerrilla research. It comes from a PBN (Product-Built Narrative) that conflates "what would be convenient for us to send" with "what the user's actual evening looks like."

French artisans in construction and trades have a different reality. A plumber or electrician working in rural Normandy or the Paris suburbs typically starts at 7am, finishes job sites between 6-7pm, drives home in traffic, eats dinner with family as late as 8:30-9pm, and is exhausted. Admin doesn't happen in a dedicated ritual slot — it happens in fragments: five minutes between jobs checking WhatsApp, a quick devis update during lunch, a invoice sent from the van before driving to the next site.

The "soir ritual" framing assumes the user has a quiet, predictable evening window for administrative work. Most artisans don't. The 8pm notification is timed for a user who doesn't exist in sufficient numbers to anchor a feature.

---

### Four Specific Challenges to D83

**Challenge 1: The 8pm assumption is invented, not observed.**

Nobody ran a time-use study on French artisans' evening routines. The "after kids are in bed, doing chiffrage" detail is vivid but fabricated — it sounds like a user description, but it's a product manager's imagination. If Louis had watched five artisans at the end of a workday, he would have seen:疲惫 (exhaustion), fragmented phone usage, dinner at varying times, and admin squeezed in when it had to be, not at a scheduled ritual. 8pm is an anchor we invented because it's convenient for our server cron job.

**Challenge 2: The 8pm notification fires at the worst possible time for an exhausted artisan.**

8pm on a Tuesday is dinner time or just-after-dinner time. Marc has been on his feet all day. He's with his family. He's not thinking about administration — he's decompressing. A push notification at this moment doesn't interrupt a quiet admin session. It interrupts dinner. Notification psychology is clear: interruptions during high-value personal time generate irritation, not engagement. A notification that arrives when Marc is relaxed and off-duty is a notification he'll swipe away and resent.

**Challenge 3: Push notifications that miss user context get disabled — and one bad notification can trigger uninstall.**

Mobile app research consistently shows that poorly-timed push notifications are the primary driver of push opt-out. "You have 3 outstanding devis" arriving at 8pm when Marc is eating with his family — or worse, at 8pm on a Saturday during dinner — is the kind of notification that gets disabled permanently. Disabled push = zero notification reach. D83's entire rationale collapses if the notification is disabled before the habit forms.

For a product where relances and financial snapshots are core retention mechanics, losing push permission is catastrophic. We're betting the retention of the entire product on a single fixed-time notification that has never been validated against actual user schedules.

**Challenge 4: "8pm Paris" is timezone-ignorant for a product targeting all of France.**

"Paris time" as the send time assumes all French artisans live on Paris time. They don't. Marseille is 25 minutes behind Paris. Strasbourg is 1 hour ahead. An 8pm Paris notification fires at 7:35pm in Marseille and 9pm in Strasbourg. For artisans in Alsace, a notification sent at what we call "8pm" arrives at 9pm — during the late dinner, after the children went to bed, when Marc is reaching for his phone to check one last thing before sleep. That's not an admin moment. That's a do-not-disturb moment.

---

### Proposed Resolution

Replace the fixed 8pm notification with two changes:

**Change 1: Configurable notification window in onboarding.**

During Free tier setup, ask Marc: *"Quand voulez-vous recevoir vos rappels?"* with three options: Morning (8-9am), Midday (12-1pm), Evening (7-9pm). Default to his stated preference. This respects that artisans have different schedules and work in different time zones across France. The "soir ritual" may be real for some — it just shouldn't be assumed for all.

**Change 2: Contextual trigger, not time-based.**

The notification should fire when there's something to do, not on a schedule that assumes a routine we haven't verified. Replace "8pm daily regardless of content" with:

*"Vous avez un devis en attente depuis 3 jours"* — fires only when a devis has been waiting for 3+ days without a response. Or: *"Cette facture est impayée depuis 15 jours"* — fires only when a specific invoice crosses the aging threshold.

This is meaningfully different from a scheduled digest. It's an event-driven notification tied to actual business events. It answers the question "should I follow up with this client?" — not "here's your nightly financial summary whether you need it or not."

The situational financière snapshot still exists — as an in-app report Marc opens when he wants business intelligence. The push notification is reserved for actionable events that require his attention now.

---

### Verdict on D83

**D83 is REFINED, not accepted as written.**

The "situation financière push at 8pm Paris" concept is directionally right (push > pull, notification > dashboard) but the implementation is wrong. Fixed-time push for a passive financial digest assumes a user rhythm we never validated and ignores the real diversity of French artisan schedules.

D83 should be updated to:
1. Configurable notification window (morning/midday/evening) — user choice in onboarding
2. Event-driven push triggers — contextual ("devis en attente depuis 3 jours"), not time-scheduled
3. Time zone awareness — send time adjusts for French regions, not just "Paris time"
4. Night mode guardrail — never send push after 10pm local time

The underlying insight of D83 — that the notification should come to Marc, not wait for him to open the app — is correct. The execution assumed too much about when and how Marc's evenings work.
