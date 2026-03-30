# Debate: Supabase EU-Hosted vs Self-Hosted on OVH — Technical Architect Position

**Date:** 2026-03-30
**Pulse file:** pulse-2040-architect.md
**Source debates:** D4 (Debate 100 resolved), open question from verdict
**Status:** DECISIVE — EU-hosted Supabase wins

---

## The Unresolved Question

D4 (Debate 100) resolved: Supabase replaces Fastify+Postgres+Coolify for v1 Sprint 0.

The verdict explicitly deferred: *"Louis to evaluate Supabase self-hosted vs EU-hosted decision. Self-hosted on existing OVH VPS = no new infra. EU-hosted = fastest path."*

This document provides the Technical Architect's definitive recommendation.

---

## Recommendation: EU-Hosted Supabase (Frankfurt)

**Position: Go EU-hosted. Do not self-host Supabase on OVH for v1.**

Self-hosted Supabase on OVH is the wrong choice for a 5-day Sprint 0. It adds meaningful ops overhead with no compensating benefit for the target persona.

---

## Technical Trade-Offs

### Operational Overhead

| Dimension | EU-Hosted Supabase (Frankfurt) | Self-Hosted Supabase on OVH |
|---|---|---|
| Docker/infra management | None — fully managed | Full responsibility: updates, monitoring, restart scripts |
| Backups | Automated by Supabase | Louis must configure and test backup rotation |
| SSL/certificates | Handled | Handled (via existing OVH VPS setup) |
| Supabase Studio | Included | Requires separate Docker deployment |
| Scaling | Automatic | Manual — resize VPS, reconfigure resources |
| Time cost in Sprint 0 | ~0h additional | 2-4h of infra work (directly competes with feature work) |

**Key point:** Self-hosting Supabase reintroduces the exact infra complexity that motivated the switch away from Fastify+Postgres+Coolify in the first place. The ops overhead of self-hosted Supabase is comparable to the Coolify setup that Debate 100 correctly identified as consuming 10-20% of Sprint 0.

### Cost

| Dimension | EU-Hosted | Self-Hosted on OVH |
|---|---|---|
| Supabase compute | ~$25/month (free tier available, paid from Day 1 revenue) | $0 to OVH (uses existing VPS, but VPS already paid for) |
| OVH VPS | Already paid (used for Nuxt SSR) | Already paid |
| Net incremental cost | ~$25/month | ~$0/month (but uses resources from existing VPS) |
| Cost when 50 customers | ~$75/month Pro plan | ~$0 (but shared VPS resources) |

**Self-hosted appears cheaper — but this is misleading.** The $25/month Supabase cost doesn't kick in until meaningful revenue exists. At 50 customers paying €29/month, that's €1,450/month revenue. The $300/year Supabase cost is ~2% of revenue. This is not a meaningful trade-off against the ops burden.

### Compliance and Data Sovereignty

This is where the self-hosted argument is loudest — and weakest for this product.

**The assumption being challenged (from prior debates):** *"French artisans require data residency in France, and EU-hosted cloud (Frankfurt) may not satisfy them."*

This assumption was likely held without validation. Let me challenge it directly:

**The assumption is probably wrong.** Here's why:

1. **GDPR does not require France-only hosting.** It requires EU-only hosting. Frankfurt is EU. This is settled law. Any French artisan who cites "French data sovereignty" as a reason to reject Frankfurt-hosted data is expressing a feeling, not a legal requirement.

2. **The real data concern of this persona is different.** French artisans aged 45-55 worry about:
   - *"If the startup disappears, do I lose access to my devis and factures?"*
   - *"Can my expert-comptable easily get my data?"*
   - *"Can the tax authorities access my invoices?"*

   None of these concerns are addressed by OVH hosting vs Frankfurt hosting. They are addressed by: contractual data portability guarantees, easy PDF export, and a product that doesn't go bankrupt. EU-hosted Supabase satisfies all three.

3. **If "data in France" were truly a hard blocker,** the question would have surfaced during persona research — not as a backend infrastructure debate. It hasn't surfaced because the real objections (trust, simplicity, payment reliability) are elsewhere.

4. **OVH is not more sovereign than Frankfurt.** OVH is a French hosting company, yes. But Supabase EU-hosted in Frankfurt is operated by a EU-based entity under EU law. The practical difference in data sovereignty is zero for this use case.

5. **Self-hosting on OVH introduces a false sense of security.** Louis managing his own Postgres backup on OVH is not more reliable than Supabase's managed backups. If anything, Supabase (a company whose entire product is reliable data storage) is more likely to have robust DR than a solo dev's bash scripts.

### Performance

| Metric | EU-Hosted (Frankfurt) | Self-Hosted (OVH France) |
|---|---|---|
| Latency from France (mobile) | 20-40ms | 5-15ms |
| Perceived performance impact | Negligible | Slightly better |
| Supabase API overhead | +20-30ms | 0ms |
| Real-world mobile network latency | 50-150ms | 50-150ms |
| **Delta as % of total request time** | **~20-25%** | **~10-15%** |

**The latency argument is a red herring.** This is a mobile app used by artisans on 4G/LTE connections in the field. The delta between Frankfurt and OVH-hosted Supabase (5-25ms) is lost in the noise of real-world mobile latency. No user will perceive "EU-hosted feels slower than self-hosted." They will perceive "the app is fast/slow" based on their network, their device, and app optimization — not server geography.

---

## Assumption Being Challenged

**Challenged assumption (from prior debates):** *"French artisans will be skeptical of EU-hosted (Frankfurt) cloud data storage and may require or prefer French-hosted infrastructure."*

This assumption is untested and likely incorrect.

**Evidence against:**
- Zero mention of hosting location in any persona research or user interviews (the debate log shows personas talk about "trust," "simplicity," "paying faster" — not server geography)
- GDPR satisfied by EU hosting — France-specific hosting is not a legal requirement
- The assumption appears to be held by the development team projecting their own technical preferences onto the persona
- The "OVH = French = good, Frankfurt = German/EU = uncertain" is a cultural bias, not a user requirement

**What French artisans actually care about regarding data:**
1. Access to their own data (devis, factures) — not where it lives, but that they can get to it
2. Reliability — the app doesn't lose their data
3. Professional credibility — the company behind the app seems legitimate
4. Exit possibility — they can get their data out if they leave

None of these require OVH vs Frankfurt. EU-hosted Supabase satisfies all of them.

---

## The Self-Hosted Case (Steel-Man)

I must address why self-hosted was seriously considered:

1. **No new vendor dependency** — true, but Supabase is open-source. The "vendor lock-in" concern applies equally to OVH (another vendor).
2. **Cost** — marginal $25/month saving is real but not meaningful at revenue stage.
3. **Full control** — self-hosted gives Louis control over Postgres config, indexes, extensions. Valid for a database-heavy product. But Supabase IS Postgres — the schema is identical.
4. **Future e-invoicing compliance** — Supabase (Frankfurt or self-hosted) is Postgres under the hood. No difference in compliance capability.

The only legitimate reason to self-host is if Louis specifically wants to learn Supabase self-hosting operations for future skill-building. That's a personal preference, not a product requirement.

---

## Decision Matrix

| Criterion | EU-Hosted | Self-Hosted OVH | Winner |
|---|---|---|---|
| Sprint 0 velocity | Fastest path | Adds 2-4h infra work | EU-Hosted |
| Ops overhead | ~0 | 2-4h/month ongoing | EU-Hosted |
| Compliance (GDPR) | ✅ EU | ✅ France | Tie |
| Compliance (perceived) | ✅ EU | ✅ France | Tie |
| Latency | 20-40ms | 5-15ms | Self-hosted (marginal) |
| Cost | ~$25/month | ~$0 | Self-hosted (marginal) |
| Data sovereignty (real) | ✅ | ✅ | Tie |
| Data sovereignty (perceived) | ✅ | ✅ | Tie |
| Vendor lock-in | Thin (open source) | Thin (OVH + open source) | Tie |
| **Overall for v1** | **Strongly preferred** | **Not recommended** | **EU-Hosted** |

---

## Action Items

### For TODO.md

```
## Supabase Hosting Decision

- [ ] CONFIRMED: EU-hosted Supabase (Frankfurt) for v1 Sprint 0
  - Reason: fastest path, zero ops overhead, full GDPR compliance
  - No self-hosting on OVH for v1 (reintroduces infra complexity)
  - Revisit self-hosting only when: revenue > €5k/month AND ops bandwidth exists

## Post-Launch Supabase Evaluation

- [ ] At 50 paying customers: evaluate self-hosted Supabase migration
  - Metrics to track: Supabase bill, OVH VPS load, ops time spent
  - Decision gate: if Supabase bill > €100/month AND OVH VPS has headroom → migrate
- [ ] Document data portability: ensure PDF export works well before any migration conversation
```

### For Louis (Sprint 0 Gate)

1. **Sign up for Supabase EU-hosted project today** (Frankfurt region). This is a 10-minute action.
2. **Do NOT set up self-hosted Supabase on OVH.** The "no new infra" argument is a trap — self-hosted Supabase IS new infra relative to EU-hosted.
3. **Do NOT over-index on "French data sovereignty" in customer conversations.** If a prospect asks "where is my data?", answer: "In Frankfurt, Germany — fully EU-compliant under GDPR. Your data never leaves the EU." If they push back on Frankfurt specifically, that's a red flag about the prospect, not the architecture.
4. **Reassess at €5k/month revenue.** That's when infrastructure costs become meaningful and self-hosting ROI becomes worth evaluating.

---

## Summary

The self-hosted vs EU-hosted debate is a false choice for v1. EU-hosted Supabase is:
- **Faster to set up** (10 minutes vs 2-4 hours of infra work)
- **Legally compliant** (EU hosting = GDPR satisfied)
- **Operationally simpler** (zero maintenance burden in Sprint 0)
- **Practically equivalent** for the persona's actual data concerns

Self-hosting on OVH trades Sprint 0 velocity for marginal cost savings and a false sense of data sovereignty. The only winner of self-hosting is Louis's learning journey. The loser is shipping on time.

**Go EU-hosted. Ship Sprint 0. Let revenue fund the ops complexity later.**

---

*Technical Architect — pulse-2040-architect*
*Next: Watch for "data residency" objections in first 10 user conversations. If any surface organically, log and revisit.*
