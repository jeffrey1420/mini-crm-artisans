[Product Strategist — Sprint 1 Job Logging]

## Position: Job Logging Is a Sprint 1 Non-Negotiable

---

## The Assumption Under Attack

The existing debate log treats Sprint 1 scope as settled around: client file + devis flow + PDF generation + mentions légales + WhatsApp sharing + TVA engine. Job logging (D13's Active Job Card) is listed in the TODO as a build item but is not assigned to any sprint — it's effectively deferred to v1.2 by omission.

This is the assumption I am challenging: **that job logging is secondary to devis flow and can follow Path A to market in v1.2**.

This assumption is wrong. It inverts the conversion architecture. D96/D104 established a dual-path conversion model. Path B (verbal-agreement artisan) is not a secondary path — it is half of the conversion architecture. Without Sprint 1 job logging, Path B does not exist at launch. The "dual-path" conversion is a single-path product.

---

## Argument 1: The Persona Argument — Marc IS the Verbal-Agreement Artisan

D3 established Marc as the primary persona: solo artisan, smartphone-native, 45-55 years old. D13 established the Active Job Card as his home anchor. These two decisions are in tension with Sprint 1 scope that defers job logging.

Marc's workflow is not: receive a client inquiry → open the app → create a formal devis. That is the formal-devis flow (Path A). Marc's actual workflow is: talk to a client on the phone → agree on scope verbally → go to the job site → remember what was agreed → do the work. Somewhere between the phone call and the job site, he needs to log what he's doing. Today he does this in WhatsApp messages to himself, or on paper, or in his head.

The Active Job Card (D13) is not "a secondary feature for users who want to track jobs" — it IS the primary interface for the verbal-agreement artisan. If Sprint 1 ships with client file + devis but no job logging:

- Marc opens the app on Monday morning
- He sees: client list (empty), devis (none created), no job context
- He has no reason to return on Tuesday
- He files it under "another app that doesn't fit how I work"
- He churns before ever hitting the 5-devis Free tier limit

**The conversion trigger assumes the product delivers value before the limit**. D96's Path A conversion fires when a user hits 5 active devis. Path B fires when a user has logged 7+ jobs OR managed 5+ active clients for 45+ days. Both assume the user is actively using the product. If the product has no job logging, Marc never logs jobs, never triggers Path B, and never converts. He either churns or settles into Free tier inertia — the worst outcome for a product that needs early traction to build word-of-mouth.

**The core risk**: Path B converts the artisan who never sends formal devis because his clients don't require them. This is a real, significant segment — not a corner case. Artisans doing small repair work, recurring maintenance, or working for property managers often operate on verbal agreements. If job logging ships in v1.2, these users have already formed habits in competing products or in WhatsApp. You cannot unseat a habit at v1.2 launch.

---

## Argument 2: The Conversion Architecture Argument — Dual-Path Is Structurally Incomplete

D96 established dual-path conversion:

- **Path A (Formal-Devis Artisan)**: Hits 5 active devis OR first paid facture → hard conversion gate
- **Path B (Verbal-Agreement Artisan)**: 45 consecutive days of active product usage (job created/updated) OR 7+ jobs logged OR 5+ active clients managed

This is presented as an equal dual-path architecture. But there is a structural problem: Path A's trigger (5 active devis) requires the devis feature to exist and be populated. Path B's trigger (7+ jobs logged) requires the job logging feature to exist and be used.

**If job logging ships in v1.2, Path B has no trigger mechanism for months.** The conversion architecture is Path A only until v1.2 ships. This changes the risk profile dramatically:

- With only Path A active at launch, the product's addressable market is limited to artisans who work from formal devis
- Artisans who operate on verbal agreements cannot convert through Path B — they have no path at all
- The 45-day/7-job Path B trigger means even if job logging ships at v1.2, Path B conversion doesn't fire until months later
- Early traction metrics (Day-30 conversion, Day-60 conversion) will look weak because Path B users are structurally excluded

**The conversion architecture argument is not "job logging is nice to have." It is: "Path B conversion is architecturally impossible without Sprint 1 job logging."**

If the dual-path model is the correct conversion thesis (and D96/D104 argues it is), then Sprint 1 must include job logging. Deferring job logging to v1.2 is equivalent to deferring Path B conversion to v1.2. This should not be a controversial claim — it is simply what the architecture requires.

---

## Argument 3: The Competitive Differentiation Argument — Job Logging Is the Wedge

The competitive landscape (Tolteck, Obat, Indy, Pennylane, Freebe) is document-centric. They sell: better devis, better factures, better admin paperwork. Their primary UI metaphor is the document. They have job logging features, but job logging is secondary to document flow — you create a client, then create a devis, and job tracking is an afterthought buried in project management features that feel like enterprise software.

**Mini-CRM's differentiation thesis should be: "We understand how you actually work."**

The actual workflow of a verbal-agreement artisan is: phone call → job → informal notes → client happy → next job. The formal devis might come later (or never). Competing products force this artisan into the devis-first paradigm because that's all they support in their mobile experience.

**Job logging + devis tracking is the combination that no competitor has nailed.** The artisan who logs jobs in the app throughout the week, then converts to formal devis when a client requests one, has a qualitatively different experience than the artisan who logs in to "create a devis." The former is using the product as a work management tool. The latter is using it as a document tool.

The differentiation wedge is: **"Mini-CRM is the only tool that fits around how you actually work, not how an accountant thinks you should work."**

Deferring job logging to v1.2 means:

- Launching as a devis/facture tool with a worse UX than Tolteck (which has 40k+ users and 5 years of refinement on document flow)
- Leaving the job-logging differentiation entirely on the table for 6+ months
- Allowing competitors to close the gap if they see traction in this segment

**The competitive window is not infinite.** Tolteck has the document flow locked. The job-logging wedge is open right now. Sprint 1 is the moment to plant the flag on "we understand your actual workflow."

---

## Argument 4: The Scope Tradeoff Argument — Minimum Viable Job Logging for Sprint 1

I am not arguing that Sprint 1 needs a full-featured job management system with Kanban boards, scheduling, worker assignment, time tracking, and materials management. D9 explicitly excludes these from MVP. I am arguing for a **minimum viable job logging feature** that enables Path B conversion.

**What minimum viable job logging requires:**

The Active Job Card (D13) data model needs:
- `jobs` table: `id`, `client_id`, `title`, `description`, `status` (pending/in_progress/completed), `scheduled_date`, `created_at`, `updated_at`
- Home query: most recent `in_progress` job, or most recent `pending` job with today's date
- Create job: title + client + scheduled date (2 minutes to log)
- Update status: in_progress ↔ completed (single tap)
- Job notes: free-text addendum to a job

This is not a project management system. It is a work log. The artisan opens the app, sees "what am I working on right now," taps to mark it complete, creates the next one.

**What this enables:**
- Path B conversion trigger (7+ jobs logged)
- D13 Active Job Card home view
- The "job-first" mental model that differentiates from document-centric competitors

**What this does NOT require:**
- Scheduling/calendar integration
- Multi-job Kanban views
- Worker or crew assignment
- Time tracking with billing
- Material/inventory management
- Any of the D9 exclusions

**Scope tradeoff: what to cut from Sprint 1 to make room**

The current Sprint 1 scope (client file + devis flow + PDF + mentions légales + WhatsApp sharing + TVA engine) is overcommitted for a solo developer in a 2-week sprint. The Technical Architect's analysis (D95) confirms this: 5 days with pre-conditions confirmed, 6.5 days floor without them.

Here is what I propose as cuts and rephasings to accommodate minimum viable job logging:

**Cut 1: WhatsApp PDF sharing → defer to Sprint 1b (Day 6-10)**
PDF generation + WhatsApp sharing is a polished feature, not a conversion requirement. The core conversion path for Sprint 1 is: client created → devis created → sent. WhatsApp sharing of a PDF is a nice-to-have for acquisition (the document quality speaks for itself), but it does not block the first conversion. Move WhatsApp PDF sharing to Sprint 1b.

**Cut 2: Mentions légales full template engine → plain text placeholder in Sprint 0/1**
D74/D71 scope: mentions légales template engine with 4 client-type templates using Handlebars/Nunjucks. This is scope that can be deferred. Sprint 1 can use a single plain-text mentions légales block (the correct legal text, just not dynamic per client type). The dynamic template engine is a Sprint 2 or v1.1 feature. Sprint 1 needs: correct mentions légales text, not a template rendering system.

**Cut 3: TVA multi-taux (5.5%, 10%, 20% per line) → flat TVA rate in Sprint 0/1**
D54 resolved TVA arrondi commercial. But the multi-taux complexity (which rate applies to which line item) is a detail most solo artisans don't use at first. A flat 20% TVA with arrondi commercial handles 80% of use cases. Multi-taux per line is a Sprint 2 feature. The TVA calculator (D54) ships in Sprint 0, but the per-line rate selection is deferred.

**Net result:**
- Sprint 0/1 keeps: client file, devis CRUD, TVA calculator (flat rate), sequential numbering, job logging (minimum viable)
- Sprint 0/1 defers: WhatsApp PDF sharing, mentions légales template engine, multi-taux per line, push notification infra (moved to Sprint 2/v1.1 per D50)
- Sprint 1 still delivers a functional client + devis + job logging flow
- Path B conversion is enabled from Day 1 of launch

**The principle:** Cut polish and deferred-value features, not core data flows. Job logging is a core data flow. WhatsApp PDF sharing is polish.

---

## The Definitive Position

**Job logging (Active Job Card, minimum viable) is a Sprint 1 requirement, not a v1.2 deferral.**

The argument is not that job logging is more important than devis flow. The argument is that:

1. **Persona**: Marc's primary workflow is job-first, not document-first. Without job logging, he has no reason to open the app.
2. **Architecture**: D96's dual-path conversion requires job logging for Path B to function. Path B cannot fire without it.
3. **Differentiation**: The job-logging wedge against Tolteck/Obat/Indy is only available at launch. After launch, competitors can close the gap.
4. **Scope**: Minimum viable job logging (job create, status update, job notes, home card) is achievable in Sprint 1 if WhatsApp PDF sharing and mentions légales template engine are deferred to Sprint 1b/v1.1.

**The one thing I am NOT arguing**: Full job management with scheduling, Kanban, multi-user, time tracking. D9 exclusions stand. Minimum viable job logging means: log a job, update its status, see what you're working on right now.

**The assumption I am challenging**: That Path B (verbal-agreement artisan) can wait for v1.2 while Path A (formal-devis artisan) carries Sprint 1. The dual-path model does not support this. Path B is structurally dependent on job logging existing in the product. Without it, the verbal-agreement artisan has no entry point, no habit formation, and no conversion path. He churns or he never converts.

**Recommendation**: Assign minimum viable job logging to Sprint 1. Defer: WhatsApp PDF sharing (Sprint 1b), mentions légales template engine (Sprint 2), multi-taux per line (Sprint 2), push infra (v1.1). These cuts are legitimate scope reductions, not feature amputations. They move non-conversion-critical polish to later sprints while ensuring the conversion architecture is complete at launch.
