## Debate TA-BetaState-0559: "Active Practitioner" Is the Wrong Filter for Sprint 0

**Technical Architect** challenges the beta user state definition from GS-Beta-0547.

---

### 1. "Active client" conflates two different validation questions

Sprint 0 is testing two distinct things:
- **(a) Does the tech work?** — devis creation, PDF generation, WhatsApp dispatch, payment link
- **(b) Does the workflow make sense to a human?** — does an artisan understand what a devis is, why they'd create one, and how it fits into their client communication?

An inactive or part-time artisan can fully validate (b). They have a lived understanding of what a devis is, what information it needs, and what their client expects from it. They don't need an *active* client pipeline to evaluate whether the UI makes sense. GS-Beta-0547's "active client" requirement mixes **product validation** (are we building something usable?) with **business validation** (does this generate revenue?). Sprint 0 should only be testing the former. Business validation belongs in a growth sprint with real commercial pressure.

---

### 2. A retired artisan who has been through the expert-comptable process IS better validation material, not worse

GS-Beta-0547 treats "no forward-looking business" as a disqualifier. This is precisely backwards.

A retired artisan who filed TVA declarations, dealt with missed invoice deadlines, and navigated the expert-comptable relationship has **institutional memory of the pain** that an active artisan may have already worked around. The retired artisan's pain is fresh precisely because they've recently *left* the workforce — they can contrast the before (chaos, missed deadlines, informal tracking) with the after. Their problem diagnosis is deeper.

A currently-active artisan with a full schedule may have already developed informal workarounds: sticky notes, WhatsApp threads, a spreadsheet that "works well enough." Our solution feels less urgent to them. The retired artisan, having just exited the system, knows exactly what we should have built. Sprint 0 wants critics who can see the problem clearly, not practitioners who are too busy surviving it.

---

### 3. The "active client" filter eliminates the best beta users

Who is most likely to respond to "will you test my app for free"?

- **Busy active artisan with full schedule → no time, low engagement,敷衍 (perfunctory) feedback**
- **Retired or part-time artisan with availability → willing, thorough, detailed feedback**

GS-Beta-0547's filter paradoxically selects *against* the users who will give the most rigorous feedback. Sprint 0's enemy is not inactive users — it is shallow engagement. A retired artisan who spends 45 minutes giving structured feedback on the devis workflow is worth ten active artisans who complete the happy path in 5 minutes and move on.

Furthermore: the beta user acquisition channels already identified (Gabin/Maël networks, expert-comptable intros) are *slow enough* without adding an extra filter that eliminates the most reachable segment. The expert-comptable network in particular skews toward clients who have *recently left practice* — they are the ones with messy books needing reconciliation.

---

### 4. "Active" is unmeasurable at signup

GS-Beta-0547 specifies "currently-practicing artisan with at least one active client relationship" — but this criterion cannot be applied consistently at signup.

How does Louis determine if a beta user meets this definition?
- **SIREN lookup?** Active business registration doesn't mean active client relationships
- **Self-declaration?** Any retired artisan will answer "yes" to stay in the beta — the filter adds zero signal
- **Expert-comptable referral?** The expert-comptable doesn't track whether their client has *active clients* — they track tax filings

If the criterion cannot be applied consistently and honestly, it is not a useful filter. It is theater — a criterion that looks rigorous but produces arbitrary inclusion/exclusion decisions. Louis will either spend inordinate time verifying status (slowing Sprint 0) or will apply it inconsistently (corrupting the data).

---

### The Correct Framing

Sprint 0 validates **technical and workflow comprehension** — not commercial momentum. The exit criteria (5 users complete client → devis → WhatsApp PDF send) test whether the product works and whether a human can follow the flow. Neither of these requires an active client pipeline.

The correct filter is: **anyone who has been a practicing artisan and can articulate the problem we're solving.** That is verifiable, sufficient for Sprint 0 validation, and selects for the most critically engaged beta users.

If Sprint 0 produces strong workflow validation from retired and part-time artisans, the next sprint (commercial validation) can recruit active practitioners. Mixing the two validation objectives into one Sprint 0 requirement is how Louis ends up with 5 engaged retirees who "don't count" because they don't have active clients — and an empty Sprint 0 result.

---

### Status
**OPEN — recommendation: any artisan (retired, part-time, or active) is valid for Sprint 0 tech validation; "active client" is a business outcome, not a Sprint 0 validation requirement**
