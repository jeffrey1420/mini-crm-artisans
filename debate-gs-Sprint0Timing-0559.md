## Debate GS-Sprint0Timing-0559: Sprint 0 Beta Validation Is Validation Theater

**Growth Strategist** challenges the framing of Sprint 0 beta validation as a gate or milestone.

---

### The Core Challenge

The 05:46 pulse spawned three debates about Sprint 0 beta acquisition — who to recruit, how to define "active" users, and what price to charge them. All three proceed from a shared assumption that Sprint 0 beta validation is a meaningful milestone. It is not.

Sprint 0 is the development phase. It ends when the code is written. It does not end when 5 humans smile at Louis.

---

### Argument 1: Sprint 0 Beta with 5 Users Validates Nothing Commercially

With n=5, every possible outcome is confounded beyond diagnostic value:

- **Sample size is trivially small.** Five users produce enormous variance. Any result — 5/5 converts, 0/5 converts, anything in between — is statistically meaningless. Louis will treat the result as a signal and it will be noise.
- **Self-selected early adopters are not the market.** An artisan who agrees to test a friend's app in week one is categorically different from a cold-trial user who finds Mini-CRM via a Google search. Early adopter data is the worst possible predictor of mainstream demand.
- **Louis's personal involvement poisons the data.** When the founder administers the test, guides the user through the happy path, and is emotionally invested in the outcome, even observational data is biased. Users perform for the founder. They say what they think he wants to hear.
- **Guided test conditions are not the wild.** A user who completes the devis → WhatsApp → PDF flow in a 30-minute session with Louis watching is not the same as a user who encounters the app at 11 PM after a missed payment, in the rain, on a job site. The real product experience cannot be simulated in a guided session.

The 5-beta-user test at Sprint 0 is internal quality assurance. It tells Louis whether the app works and whether a real human can follow the flow. It tells him nothing about market demand, price sensitivity, or whether anyone will pay €29/month in 6 months.

---

### Argument 2: The Real Validation Milestone Is Post-Sprint 1, With Real Distribution

After Sprint 1 ships, the app exists in the world. There is a landing page. There is a real install process. There are real users making real decisions in real contexts. That is when Louis gets data that matters:

- **Real install data:** How many people start the signup flow? Where do they drop? These funnel numbers are the first honest signal of product-market fit.
- **Real dropout funnels:** Which screen do users abandon? Which field causes friction? Louis cannot know this from 5 guided happy-path completions.
- **Real WhatsApp sharing events:** Does anyone actually send a devis via WhatsApp in production? Or do they just say they would in a guided session?
- **Real conversion behavior:** Do users who reach the trial end actually pay? Do they churn before paying? Do they convert after seeing the paywall? These numbers are the only ones that matter for go/no-go on pricing.

Sprint 0 validates the thing builds. Sprint 1 validates the thing sells. These are different questions requiring different data.

---

### Argument 3: The Obsession With Sprint 0 Beta Acquisition Is Founder Ego in Disguise

Louis wants to believe his product will work. He wants to test it with real humans. He wants the emotional relief of a human saying "yes, I like this." That desire is understandable and human — and it is not a valid exit criterion.

The Sprint 0 beta obsession has the following characteristics of validation theater:

- **It feels like progress without being progress.** Recruiting 5 users, scheduling sessions, watching them click through — this feels like validation activity. It produces no durable data asset.
- **It creates commitment that biases future decisions.** If 5/5 beta users say they love it, Louis will anchor on that story. He will cite it in pitch meetings. He will use it to justify continuing down a wrong path. This is sunk cost dressed as evidence.
- **It delays the hard work of real distribution.** The energy spent recruiting, screening, and managing 5 beta users is energy not spent building the landing page, writing the App Store listing, or figuring out how artisans actually discover new tools.

The discipline is to ship Sprint 0, distribute it as broadly as expedient (even a link to 10 people via WhatsApp counts), and wait for behavioral data before declaring anything validated.

---

### Argument 4: The Correct Sprint 0 Exit Question Is Not "Did 5 Beta Users Complete the Happy Path?"

The Sprint 0 exit question currently implied by the debate is some version of: "Did 5 beta users complete the devis → WhatsApp → PDF flow?" This is wrong.

**The correct Sprint 0 exit question is:**

> *"Does the app build, install, and run without crash on a real Android device with a real French SIM card?"*

If the answer is yes, Sprint 0 is done. If the app crashes on a real Pixel 6 running Bouygues firmware, Sprint 0 is not done regardless of how many beta users loved the UI mockup.

Everything beyond "it builds, installs, and doesn't crash" is aspirational bonus for Sprint 0 — not exit criteria. The "5 beta users complete the happy path" metric is a nice-to-have, not a gate. Treating it as a gate creates a false milestone that delays Sprint 1 and generates misleading confidence.

---

### Recommended Sprint 0 Exit Criteria (Revised)

| Criterion | Threshold | Who Validates |
|-----------|-----------|---------------|
| App builds without errors | CI pipeline green | Developer |
| App installs on real Android device (not emulator) | APK installs, app launches | Developer |
| App runs without crash on real device | No Force Close in first 5 minutes of use | Developer |
| Core happy path completes in dev environment | devis → client → WhatsApp PDF works | Developer |
| Mentions légales displayed in footer | Static text renders | Developer |
| **Beta user validation** | **NOT Sprint 0 gate — aspirational bonus only** | **—** |

Beta user validation moves to Sprint 1 as the first real success metric — not as a gate, but as a metric to track alongside real distribution.

---

### Status

**OPEN — recommendation: redefine Sprint 0 exit criteria as "app builds, installs, and runs without crash on real Android device" — not user happiness metrics**

Sprint 0 beta acquisition debates (GS-Beta-0547, expert-comptable channels, Grinto intros) are premature. The real debate is what Louis measures after Sprint 1 ships and the app is in the wild. Until then, the priority is shipping code, not recruiting believers.
