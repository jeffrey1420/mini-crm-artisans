# Technical Architect Position: BaaS (Supabase) is the Right Choice for Mini-CRM v1

## The Core Challenge

The D4 assumption — *"Custom Fastify backend gives full control and is the right long-term choice"* — conflates long-term architectural purity with short-term survival. For a 5-day Sprint 0 with a solo dev, **time-to-ship beats architectural elegance**. The Fastify + Postgres + Coolify stack is a competent architecture that happens to be the wrong architecture for this constraint.

---

## 8-Point Argument Against Fastify + Postgres + Coolify for v1

### 1. Coolify Setup Is Not Trivial — It Competes Directly With Feature Development

Coolify promises "self-hosted Heroku alternative," but the reality for a first-time setup:
- Requires Docker daemon configuration, Docker Compose knowledge
- Requires Redis installation and configuration (not optional for Coolify's job queue)
- Requires Python environment for Coolify's own runtime
- DNS, SSL, and network configuration on the VPS
- Expected setup time for a clean Coolify install: **2–4 hours** for an experienced dev, potentially **half a day** for a first-time setup on a new VPS

That's **10–20% of the entire Sprint 0** burned before writing a single feature. With Supabase, the equivalent is: create account → 5 minutes → done.

### 2. Fastify API Development Time Is Systematically Underestimated

"Fastify is fast to develop with" is true relative to Express, but still:
- Auth middleware: JWT validation, refresh token rotation, session management → **4–6 hours**
- CRUD routes with input validation (JSON Schema or TypeBox) → **3–4 hours per resource**
- Error handling layer (centralized errors, HTTP status codes, error responses) → **2–3 hours**
- Database connection pooling, migrations, seed scripts → **3–4 hours**
- CORS, rate limiting, request logging → **2 hours**

A rough estimate for a basic but production-ready API skeleton: **15–20 hours**. A solo dev in 5 days has ~40 hours of effective coding time. That leaves **20–25 hours for actual features** — barely enough for contacts, companies, and deals at a surface level.

### 3. The BaaS Value Proposition Is Not Hypothetical — It's Measured in Days

Supabase provides out of the box:
- **Auth** (email/password, magic links, OAuth) — built-in, tested, compliant
- **Postgres database** with RLS (Row Level Security) — same database, but auth is handled
- **Realtime subscriptions** — for live updates in the Expo app
- **File storage** — for document uploads
- **Edge Functions** — for server-side logic

This is not "maybe useful someday." This is **every major backend concern for v1 solved before you write a line of code.** The equivalent Fastify implementation of all of the above, even at v1 scope, is easily 3–4 days of work.

### 4. The "E-Invoicing Compliance" Argument Is Overblown for v1 Scope

D74 resolved to Fastify specifically for French e-invoicing compliance control. But:

**The e-invoicing mandate (CGI art. 289)** applies to B2B transactions and has a phased rollout:
- **January 1, 2025**: Large companies (>500 employees) — Phase 1
- **January 1, 2026**: Medium companies (250–499 employees) — Phase 2
- **January 1, 2027**: Small companies (50–249 employees) — Phase 3

Mini-CRM v1 is a CRM, not an accounting or invoicing system. The e-invoicing requirement applies to **invoice issuance**, not CRM contact/company management. If Mini-CRM later adds invoicing features, that is v2 or v3 territory. **Building for a compliance requirement that:**
1. Doesn't apply to the product's current scope
2. Doesn't kick in for small companies until 2027
3. Is only relevant if the feature is actually built

...is textbook **premature optimization** masking as architectural caution.

### 5. French Data Sovereignty: Supabase Has Better Options Than Assumed

The concern that "Supabase data may go to US servers" is valid for the hosted cloud tier, but it ignores:

**Option A: Supabase self-hosted** — Run Supabase on your own Coolify VPS. You get the entire Supabase platform (Auth, Postgres, Realtime, Storage, Edge Functions) on your own infrastructure. The data never leaves your server. This is a genuine option, not a workaround.

**Option B: Supabase EU-hosted projects** — Supabase offers EU-based projects where data is stored in EU data centers (Frankfurt/eu-west-1). This addresses the GDPR data residency concern directly. Combined with standard DPA agreements, this satisfies CNIL requirements for most use cases.

**Option C: Firebase with European data residency** — Firebase has EU-based hosting options and offers Data Residency configurations for GCP-based projects.

The sovereignty concern is solvable with configuration, not a reason to reject BaaS entirely. The Fastify + Postgres stack also doesn't automatically solve sovereignty — if Postgres is on a US-hosted VPS, it has the same problem.

### 6. "Full Control" Is a Liability When You Don't Have an Ops Team

"Full control" of a Fastify + Postgres + Coolify stack means:
- You control the deployment pipeline → you debug the deployment pipeline
- You control the database schema → you write and run migrations
- You control auth → you handle security patches, token refresh bugs, password reset flows
- You control file storage → you manage disk space, backups, CDN

For a solo dev, "full control" often means "full responsibility for everything that breaks at 2am." Supabase's managed service means，沈玉琳 an outage has a team behind it. The tradeoff between control and operational burden is not obvious for a bootstrapped product.

### 7. Expo + Supabase Has Proven Patterns at This Scope

The React Native + Supabase pattern is well-documented:
- `supabase-js` client works in Expo (with dev client or EAS build)
- Auth session management is idiomatic and well-tested
- RLS policies replace custom auth middleware
- Realtime subscriptions work over WebSockets

The argument that "BaaS doesn't integrate well with mobile" was true in 2019. In 2025, Supabase has official React Native support and a published integration guide for Expo projects. The friction is minimal.

### 8. The MVP Definition Matters — v1 Doesn't Need to Be Production-Grade Infra

Mini-CRM Sprint 0 is about validating: **"Does this product concept work? Do users want it?"**

For that goal:
- Auth doesn't need a custom JWT implementation — Supabase Auth is battle-tested
- Database doesn't need custom CRUD — Supabase client with RLS covers it
- File storage doesn't need S3 — Supabase Storage covers it
- Realtime doesn't need a custom WebSocket server — Supabase Realtime covers it

What you need is: something that works, something you can iterate on fast, something that doesn't break when you ship to real users. BaaS delivers all three for v1. The "production-grade infra" argument is for when you have product-market fit and revenue to justify it.

---

## The Assumption I'm Challenging

> D4: "Custom Fastify backend gives full control and is the right **long-term** choice"

The word "long-term" is doing a lot of work here. Fastify + Postgres + Coolify is a fine **long-term** architecture. It is a poor **v1** architecture for a solo dev with 5 days. These are not contradictory — they are different time horizons.

The assumption assumes the long-term choice is also the right v1 choice. It is not. The right v1 choice is the one that gets you to a working prototype in 5 days. **The right long-term choice is made after you have users, revenue, and evidence that the product direction is correct.**

---

## VERDICT

**Use Supabase (self-hosted or EU-hosted) for Mini-CRM v1.**

**Rationale:**
1. Sprint 0's 5-day constraint makes infra complexity a first-order risk, not a second-order concern
2. The e-invoicing compliance argument does not apply to v1 scope — it is a future-facing argument used to justify present-day complexity
3. Supabase gives you the same Postgres database you would have with Fastify + Coolify, plus auth, realtime, and storage — with zero self-hosted overhead
4. French data sovereignty is solvable with Supabase EU projects or self-hosted Supabase on your own VPS
5. "Full control" is only valuable when you have the bandwidth to exercise it — a solo dev with a 5-day deadline does not

**If Fastify + Postgres is chosen over BaaS for v1**, the sprint goal should be restated: this is no longer a 5-day feature sprint — it is a 5-day infrastructure + skeleton sprint, and features will ship in Sprint 1. That is an honest framing. The current assumption that both can happen in 5 days is not.

**Migration path if BaaS is chosen:** Supabase can be self-hosted on the same Coolify VPS later if compliance requirements demand it. The Supabase self-hosted stack runs on Docker, same as the current plan. The product code using `supabase-js` client is portable. Choosing Supabase for v1 does not foreclose the Fastify path — it defers it to when the compliance argument is actually relevant.

**Choose BaaS for v1. Choose self-hosted for v2+ when/if e-invoicing scope is confirmed and French data sovereignty becomes a contractual requirement with a named client.**
