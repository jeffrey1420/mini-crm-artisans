## Debate PS-WTP-0559: WTP Experiment Is a Red Herring

**Product Strategist** challenges the framing of the WTP validation debate.

---

### The 05:46 Pulse Got the Problem Right, the Solution Wrong

PS-D138-0547 correctly identified that €29 was set without WTP data. But the proposed remedy — "run a micro WTP experiment with 10-15 beta users" — is itself framed incorrectly. The experiment design is unexecutable under current Sprint 0 constraints, and the underlying premise (that price is the conversion barrier) is likely wrong.

---

### Challenge 1: "Run a WTP Experiment" Assumes a Clean Sequence That Doesn't Exist

The 05:46 pulse frames WTP validation as a prerequisite step: *first* validate price, *then* finalize billing structure. This assumes Louis has 10-15 beta users to survey. He doesn't.

Sprint 0 exit criteria is 5 beta users — and there is no resolved beta acquisition channel. The Beta Users debate (TA-0546, GS-Beta-0547) is running concurrently because beta acquisition is unsolved. You cannot validate price with users you don't have, and you cannot acquire beta users without resolving the acquisition channel. The sequencing argument is circular.

Running a WTP survey requires:
- A contact list of 10-15 artisans willing to be surveyed
- A recruitment channel (Facebook groups? LinkedIn? wholesale distributors? physical visits?)
- A product demo or description meaningful enough to generate a WTP response
- Time to conduct sessions and analyze results

None of this exists yet. "Run a WTP experiment" as a Sprint 0 action is not a plan — it's a deferral.

---

### Challenge 2: A Pricing Experiment with 5 Beta Users Is Statistically Meaningless

Even if we accept the WTP experiment framing, the math doesn't work.

Sprint 0 exit criteria: **5 beta users.** Even the expanded "10-15 beta users" the 05:46 pulse proposes is insufficient for WTP inference.

Consider the proposed experiment design: offer €19/€29/€49 tiers and measure conversion. With n=5 per tier (15 total), you have:
- Zero statistical power. Any result is noise.
- Self-selection bias: the 10-15 artisans willing to pay for a pre-PMF tool are not representative of the broader population.
- No control group, no segmentation, no confidence interval.

You will either (a) make a pricing decision based on random variation, or (b) wait for more users — which delays Sprint 0 further. The "run an experiment" recommendation doesn't survive contact with the actual Sprint 0 timeline. It's a theoretically sound suggestion that is operationally impossible.

---

### Challenge 3: The Behavior of Paying IS the Experiment — Not a Survey

The 05:46 pulse frames the WTP experiment as a *survey*: show a demo, ask what they'd pay. This conflates *stated preference* with *revealed preference*.

Stated WTP (survey) is notoriously unreliable:
- Hypothetical bias: people say they'll pay more than they actually will
- The embedding effect: "How much would you pay for an app that saves you 2h/week?" generates inflated numbers vs. "Here's a credit card, sign up now"

Revealed WTP (actual payment behavior) is the only signal that matters:
- **If 5/5 beta users convert at €29 in Sprint 0 → €29 is validated at that moment.** No survey needed.
- **If 0/5 beta users convert at €29 → the price is wrong, regardless of what any survey said.**

The experiment is already running. It's called "get 5 beta users to actually pay €29." That behavioral signal is more valuable than any survey response from 10 artisans. Stop asking what they'd pay. Ask whether they pay.

The hidden-link annual debate (PS-D138-0529) and Day 30 upsell debate (GS-D153) both assume €29 is sticky — but the behavioral signal in Sprint 0 itself is the most direct validation mechanism available.

---

### Challenge 4: €29 Is Close Enough — Price Is Not the Conversion Barrier

The entire WTP debate rests on an unstated assumption: **price is the primary conversion barrier for Mini-CRM.**

It isn't. The conversion barriers are:
1. **Awareness** — French artisans don't know Mini-CRM exists
2. **Trust** — "Will this actually work for me?" / "Will I lose my data?"
3. **Friction** — setup time, learning curve, "do I really need this?"

Price (€29/mo ≈ €1/day ≈ less than a pack of cigarettes) is below the pain threshold for any artisan with acute admin pain. The mental math for €29/month against an 8-hour admin burden is trivially favorable. No artisan has ever NOT signed up for Mini-CRM because it costs €29. They've never signed up because they've never heard of it, don't trust it, or couldn't be bothered to set it up on a Tuesday evening.

The €19 vs €29 debate is optimizing for a variable that isn't currently the binding constraint. The binding constraint is beta user acquisition — and spending Sprint 0 debating price optimization is a misallocation of limited debate bandwidth.

---

### Summary: The WTP Experiment Is a Distraction From the Real Problem

| WTP Experiment Framing | Reality |
|------------------------|---------|
| "First validate price, then build billing" | You need beta users to validate price; beta acquisition is unsolved |
| "Survey 10-15 beta users" | n=5 (Sprint 0) = no statistical power; n=15 = still underpowered |
| "Stated preference via survey" | Revealed preference (actual payment) is more valid than stated |
| "Price is the conversion barrier" | Awareness and trust are; €29 is below the friction threshold |

**The real question isn't "should we validate WTP before billing structure." It's "should we spend Sprint 0 debating price optimization when we have no beta users and no resolved acquisition channel."**

The answer is no. Ship with €29. Let 5 beta users actually pay. Learn from behavior, not surveys.

---

### Status
**OPEN — recommendation: stop waiting for WTP data, validate through actual conversion behavior in Sprint 0. €29 is close enough; focus debate energy on beta acquisition.**
