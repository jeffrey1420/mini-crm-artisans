[Technical Architect — Sprint 0 Start Blockers]

## Status: URGENT — Sprint 0 is not actionable in its current form

D95 established Sprint 0 = 5 days (target) or 6.5-7 days (floor) depending on pre-conditions. The documented pre-conditions are:
1. U16: Louis writes 4 mentions légales templates (2h pre-work)
2. Supabase signup confirmed

Debate 109 resolved U7 — domain purchase is now "buy now, park it."

**This debate challenges that the two documented pre-conditions are insufficient, that three additional decisions are blocking sprint start, and that the product spec (devis flow) isn't written yet. Sprint 0 cannot begin as planned without resolving these gaps.**

---

## 1. The Missing Spec Problem — Sprint 0 Has No Written Devis Flow

**The assumption:** Sprint 0 builds the schema and infrastructure. Sprint 1 builds the devis flow on top of it.

**The problem:** Nobody has written the devis flow as a spec. The flow exists as debate conclusions (D2: client file → devis → send via WhatsApp) but not as a concrete, agreed sequence of screens, states, and API calls.

**What "Sprint 0 starts" currently means:** Louis opens his editor on Day 1 and... builds what, exactly? The schema? Which fields? In what order? For which client types?

**The Devis Flow is not specified.** The debates have established:
- Marc creates a client (or selects existing)
- Marc adds line items (description, quantity, unit price, TVA rate)
- TVA calculates per-line using arrondi commercial
- Mentions légales render based on client type
- Devis is sent via WhatsApp native share

**What is NOT specified:**
- Exact screen sequence (single scrollable form? multi-step wizard?)
- Client creation inline or separate screen?
- Line item add flow (tap + row appears? modal?)
- TVA rate selection UI (dropdown per line? default assumption?)
- Devis preview before send — is there a preview step?
- What happens on send failure? (retry? saved as draft?)
- Devis status enum values: `draft | sent | accepted | rejected | expired` — are these all in Sprint 0?
- Can Marc edit a sent devis? (legally yes for devis, different from facture)

**Why this matters for the 5-day estimate:**
D90 says "define API contract by end of Day 1" — but that means Day 1 is entirely spent on planning, not building. If the API contract isn't defined BEFORE Sprint 0 starts, the 5-day timeline assumes Day 1 can be both planning AND building. For a solo dev, it can't. Planning and building compete for the same cognitive context.

**Concrete ask:** Before Sprint 0 begins, Louis needs to write a one-page "Sprint 0 Scope: Devis Flow" spec. Not a Figma mockup. Just:
```
Sprint 0 Devis Flow:
1. Create client (name, phone, type: particulier/pro/horsUE)
2. Create devis for that client (line items: description, qty, unit_price, tva_rate)
3. TVA calculates per line: Math.round(qty * unit_price * tva_rate * 100) / 100
4. Mentions légales block renders based on client.type
5. Preview devis (PDF generation)
6. Send via native share (WhatsApp/email)
7. Devis saved as status='sent'
```
This is 30 minutes of writing that prevents days of rework.

---

## 2. The Supabase Schema Isn't Defined — "Transfers Directly" Is Unverified

**D100 resolved:** "EU-hosted Supabase (Frankfurt). Prior Postgres schema work transfers directly to Supabase."

**This is optimistic.** The prior schema work (from when Fastify+Postgres was the plan) was designed for a different ORM, different auth model, and different storage approach. Supabase has specific requirements that may not transfer:

**What "transfers directly" assumes:**
- The schema types (clients, devis, line_items) are ORM-agnostic — probably true
- RLS (Row Level Security) policies from the old schema work in Supabase — unverified
- Auth configuration (Supabase Auth) integrates with the same user model — unverified
- Storage buckets (for PDF archival) have the same structure — unverified
- The `gen_random_uuid()` approach for API keys works identically — probably true

**What Supabase specifically requires that the prior schema may not have:**
1. **RLS policies** — every table needs explicit `RLS` enable + policy definitions. A raw Postgres schema doesn't include these.
2. **Auth user linkage** — `client.user_id` must link to `auth.users()` properly
3. **Storage bucket configuration** — PDFs need a `storage.buckets` entry + upload policy
4. **Realtime subscriptions** — if we want live updates (not in Sprint 0, but prepped)

**Concrete ask:** Before Sprint 0 begins, Louis needs to:
1. Create the Supabase project (supabase.com → EU region) — 10 minutes
2. Run a basic schema migration that creates: `clients`, `devis`, `line_items` tables
3. Enable RLS on all tables
4. Verify the project dashboard is accessible and shareable

**D95's pre-condition #2 says "Louis shows Supabase project dashboard" — this is the correct ask. But it must be verified BEFORE sprint start, not during.**

---

## 3. The Three Blocking Decisions

These are architectural decisions that cannot be made during Sprint 0 without extending it. They must be answered before Day 1.

### 3a. React Native Project Structure — Expo + Which Navigation?

**Decision needed:** Expo project with which navigation library?

Options:
- **Expo Router** (file-based routing, newer, opinionated)
- **React Navigation** (more flexible, larger ecosystem, more boilerplate)

**Time cost of deciding during Sprint 0:** 1-2 days of navigation setup + context confusion if the choice changes mid-sprint.

**Current state:** D11/D17 resolved React Native from Day 1 via Expo. Nobody resolved which navigation library.

**Concrete ask:** Louis picks one before Sprint 0. Recommendation: Expo Router (simpler, less configuration, works well for the single-flow nature of the devis app). But the decision must be made, not deferred.

### 3b. PDF Generation Approach

**Decision needed:** How are devis PDFs generated?

Options:
- **Server-side (backend):** Generate PDF on the Fastify/Supabase side, serve via API
- **Client-side (mobile):** Generate PDF in React Native using a library like `react-native-pdf-lib` or `react-native-html-to-pdf`
- **Hybrid:** Backend generates HTML, client converts to PDF (avoids server load but adds complexity)

**Time cost of deciding during Sprint 0:** If this isn't decided before sprint, the PDF generation workstream is blocked until it is. PDF is in Sprint 0 scope.

**Current state:** D106 resolved "PDF attachment via native share sheet ships in Sprint 0." But the generation method wasn't specified.

**Recommendation:** Server-side PDF generation (Supabase Edge Function or API route) is the cleanest approach for Sprint 0. It keeps the mobile app simple, handles mentions légales rendering server-side, and produces a shareable file URL. React Native just needs to open the share sheet with the URL.

**Concrete ask:** Louis decides: server-side or client-side PDF generation? If server-side: Supabase Edge Function or Fastify route? If client-side: which library? This is a 30-minute decision that prevents a day of rework.

### 3c. Mentions Légales Templates — Written or Pending?

**Current state:** D97 says "Louis writes 4 mentions légales templates this week (2h pre-work) — gate for 5-day Sprint 0."

**The question:** Is this 2h of work DONE or SCHEDULED?

These are different things:
- **Done:** Templates exist as files in a repo, committed to git, ready to be loaded by the mentions légales renderer
- **Scheduled:** "I'll do it this week" — meaning it might not be done before Sprint 0 starts

**Why this matters:** The 5-day Sprint 0 estimate assumes the templates are pre-written. If Louis writes them during Sprint 0:
1. He loses 2h (part of Day 1) from sprint work
2. Sprint 0 effectively becomes 4.5 days of building + 2h of legal writing
3. The pre-condition wasn't "pre" — it was concurrent

**The sprint planning paradox:** D95 says "Sprint 0 = 5 days (target) if pre-conditions confirmed." The TODO says "Sprint 0 starts after U16 is done." U16 = "Louis writes the templates."

If Louis writes the templates as part of Sprint 0, then Sprint 0 hasn't started after U16 — U16 IS part of Sprint 0.

**Concrete ask:** Louis must show 4 template files committed to git BEFORE Sprint 0 begins. Not "I'll write them this week." COMMITTED. The pre-condition gate is a git commit hash, not a calendar entry.

---

## 4. Challenging the D95/D97 "Pre-Conditions Confirmed" Assumption

**The assumption:** "Pre-conditions confirmed" means Louis has done the pre-work (templates written, Supabase signed up) before Sprint 0 starts.

**The challenge:** "Confirmed" is ambiguous. Does it mean:
- **(A)** Louis has completed the work and can show artifacts (git commit hash, Supabase dashboard URL)?
- **(B)** Louis has scheduled the work for "this week" and intends to do it before sprint?
- **(C)** Louis believes he can do it in parallel with Sprint 0?

**Interpretation (A) is what D95 actually requires.** Interpretation (B) or (C) means the pre-conditions are not confirmed — they're aspirational.

**The practical difference:**

| Scenario | Sprint 0 Duration |
|----------|-------------------|
| Templates committed + Supabase project created before Day 1 | 5 days |
| Templates scheduled "this week" but not yet started | 5.5-6 days |
| Templates written during Sprint 0 (Day 1 afternoon) | 6-6.5 days |
| Supabase project created during Sprint 0 (not before) | +0.5-1 day |
| API contract defined during Sprint 0 (not before) | +1 day (parallelization blocked) |

**D95 says "5.5-6.5 days achievable if pre-conditions met." But "met" means DONE, not "scheduled."**

---

## Summary: The Exact Decisions That Must Be Made Before Sprint 0 Can Begin

These are not "nice to have." These are blocking:

**Pre-conditions (must be shown, not just scheduled):**
1. ☐ Louis shows 4 mentions légales template files committed to git (one per client type: particulier, pro-français, pro-UE, pro-horsUE)
2. ☐ Louis shows Supabase project dashboard (EU region, Frankfurt, accessible)

**Spec (must be written before Day 1):**
3. ☐ Louis writes a 1-page Sprint 0 scope document: the devis flow as a sequence of steps (screen → action → next screen)
4. ☐ Louis defines the API contract: what endpoints does the mobile app call, what does each return? (Even a shared types file counts.)

**Decisions (must be made before sprint, cannot be deferred to sprint):**
5. ☐ React Native navigation: Expo Router or React Navigation? (Decision: Expo Router recommended)
6. ☐ PDF generation: server-side (Supabase Edge Function) or client-side (React Native library)?
7. ☐ Mentions légales renderer: Handlebars, Nunjucks, or simple string interpolation? (Template engine choice)

**Nice to have (can be resolved in Sprint 0, but having answers speeds it up):**
8. ☐ Devis status enum confirmed: `draft | sent | accepted | rejected | expired` — all five in Sprint 0 scope?
9. ☐ TVA rate defaults: if Marc doesn't specify a rate, what does the system assume? (Default to 10%? Error if missing?)
10. ☐ Client creation inline (in devis form) or separate screen (client list first)?

---

## Recommendation

**Sprint 0 cannot start on Monday "after U16 is done" if U16 is not yet done.**

Louis should do the following in order:
1. **Today or tomorrow (30 min):** Create Supabase project (EU region). Show the dashboard URL. This is pre-condition #2.
2. **Today or tomorrow (30 min):** Write the 4 mentions légales templates as plain text files. Commit to git. This is pre-condition #1 + decision about template engine.
3. **Today or tomorrow (30 min):** Write the 1-page Sprint 0 scope: the devis flow as steps. This is the missing spec.
4. **Today or tomorrow (15 min):** Pick Expo Router for navigation. This is blocking decision #3a.
5. **Today or tomorrow (15 min):** Pick server-side PDF generation (Supabase Edge Function). This is blocking decision #3b.
6. **Today or tomorrow (15 min):** Define the API contract as a shared types file or OpenAPI spec. This is what D90 requires by "end of Day 1" — move it to "before Day 1."

**Total pre-sprint work: ~2.5 hours.** This is the actual pre-work required, not just the 2h for mentions légales templates.

With these six items confirmed, Sprint 0 is genuinely actionable as 5 days.

Without them, Sprint 0 starts with open questions that consume sprint time — making the 5-day estimate unachievable and the 6.5-day floor the realistic outcome.

---

*Technical Architect — 2026-03-30T21:39 UTC*
