# Technical Architect — D100 Final Position

## Core Argument

**Complexity is the enemy of shipping. Fastify + Postgres + Coolify is not a stack — it's a part-time job.**

A 5-day Sprint 0 with a 4-feature MVP is already scope-constrained. The decision to use Fastify + Postgres + Coolify introduces infra work that directly competes with feature work for the same 5 days:

- **Coolify setup:** 2-4 hours for an experienced dev, half a day for anyone learning it. That's 10-20% of Sprint 0 before the first feature ships.
- **Fastify scaffold:** Auth middleware, CRUD routes, error handling, database migrations — easily 15-20 hours of non-feature boilerplate.
- **Postgres schema:** Row-Level Security policies, connection pooling, backup configuration — hours more.

That's **30-40% of Sprint 0** burned on infrastructure plumbing before a single devis can be created.

**Supabase changes the math entirely:**

| Task | Fastify + Postgres + Coolify | Supabase |
|------|------------------------------|----------|
| Auth (email/password, JWT) | Build or integrate + test | `supabase.auth` — done |
| Database schema + RLS | Write migrations + policies | `supabase db` — done |
| API CRUD routes | Write each manually | Generated, or write in ~20 lines |
| File storage (PDFs) | S3 config + presigned URLs | `supabase.storage` — done |
| Realtime subscriptions | WebSocket setup | `supabase.channel` — done |
| Admin panel | Build from scratch | Included |
| Migration tooling | Write + test manually | Built in |

**The "full control" argument is backwards for v1.** Full control means full responsibility for every failure mode — connection pool exhaustion, migration bugs, Coolify update breaking your deployment, a 2am P0 because you touched the wrong ENV variable. For a solo dev on a 5-day sprint, ops burden is existential risk. Supabase means a team behind your infrastructure. At v1 scale, that team is worth more than theoretical control.

**The French artisan context reinforces this.** Marc doesn't care about the backend architecture. He cares whether his devis arrives in WhatsApp. Shipping a slightly "simpler" stack that actually ships beats a "more control" stack that ships late or doesn't ship at all.

**E-invoicing is a v2 problem.** The French e-invoicing mandate for small artisans doesn't bite until 2027 at earliest. Building for compliance that doesn't apply to v1 scope is premature optimization. If it becomes relevant, Supabase has Postgres under the hood — you can run any SQL you need.

**French data sovereignty is solvable.** The anti-Supabase argument always reaches for "French data sovereignty" as a trump card. It's not:
1. **Supabase EU-hosted** (Frankfurt) — GDPR-compliant, data stays in EU. This is sufficient for a French artisan tool at v1 scale.
2. **Self-hosted Supabase** on the same OVH VPS already provisioned — same data residency as the Coolify plan, minus the Coolify complexity.
3. The alternative (Fastify + Postgres + Coolify) still puts data on OVH, same VPS provider. The sovereignty argument doesn't favor Coolify over Supabase — it favors OVH, which both options can use.

The choice is not "Supabase vs sovereignty." It's "Supabase (EU-hosted or self-hosted) vs Fastify + Postgres + Coolify" — and on sovereignty grounds, they're equivalent.

## Rebuttals

### "Vendor lock-in"

**Lock-in to what?** Supabase is open-source. You can self-host on any Postgres-compatible infrastructure tomorrow. There's no lock-in — there's a convenience layer on top of Postgres, which is exactly what you're using anyway.

The real lock-in risk is building a bespoke Fastify API so tightly coupled to your domain that migrating to any other backend takes 6 months. With Supabase, you can rip out `supabase.auth` and replace it with Clerk. You can migrate to plain Postgres + Prisma in a weekend. The abstraction is thin and reversible.

Fastify + hand-rolled auth + custom CRUD = that's where real lock-in lives. At least Supabase's lock-in is to SQL and REST — the two most portable interfaces in existence.

### "Data sovereignty — French artisans need data in France"

Solved by EU-hosted Supabase (Frankfurt) or self-hosted on OVH. This is not a distinguishing factor between Supabase and Fastify+Postgres — it's a solved problem for both.

The sovereignty argument is strongest against US-hosted cloud services (AWS US-East, Heroku, etc.). Supabase EU-hosted is equivalent to OVH-hosted Postgres on this dimension.

### "'Full control' means we own our destiny"

"Full control" of a 5-day sprint's infrastructure is an illusion. You control it until it breaks at 2am, then you *suffer* it. The real question: what failure modes do you have capacity to handle during Sprint 0?

- Coolify update breaks your deployment mid-sprint → 4 hours lost
- Postgres connection pool misconfigured under load → debugging while features wait
- Migration bug rolls back production data → game over

Supabase's managed service means these failure modes have engineering teams behind them. Your 5 days of sprint capacity goes entirely into features. The trade is correct for v1.

### "BaaS pricing at scale will kill us"

This is a future problem for a v1 that doesn't exist yet. At 100 paying users (€2,900/month revenue), pricing is a rounding error on your infrastructure budget. At 1,000 paying users (€29,000/month), you're profitable enough to absorb any pricing change or migrate off.

The "BaaS pricing at scale" argument is the same genre as "what if Postgres can't handle 10 million rows?" — technically interesting, practically irrelevant at v1. Ship first. Optimize pricing when you have revenue to optimize.

### "Supabase adds latency"

Supabase EU (Frankfurt) → French end users: ~20-40ms round trip. Fastify on OVH VPS (France) → French end users: ~5-15ms round trip. The delta is imperceptible to a human using a mobile app. This is not a real concern for the target audience.

## Verdict

**D4 is OVERRULED. Sprint 0 architecture = Supabase (self-hosted on OVH or EU-hosted).**

Specific resolution:

1. **Use Supabase** — either EU-hosted (fastest path, same data residency as OVH) or self-hosted on the existing OVH VPS (no new infra dependency)
2. **Keep the same Postgres schema design** — Supabase IS Postgres. The schema work from previous debates is not wasted.
3. **Auth:** `supabase.auth` with email/password for v1. Magic links optional.
4. **Storage:** `supabase.storage` for PDF devis/facture generation pipeline
5. **No Coolify dependency** — eliminates 2-4 hours of setup and one permanent ops concern
6. **React Native connects via REST** — Supabase REST API is standard, or use the JS client directly
7. **E-invoicing:** v2 concern. When it becomes relevant, Postgres under Supabase supports any compliance query you need.

**The constraint is shipping speed, not architectural purity.** Supabase lets a solo dev ship a 4-feature MVP in 5 days without owning a part-time ops job. That's the right trade for this sprint.

D4 updated: Fastify + Postgres + Coolify is retired. Supabase is the Sprint 0 backend.
