DEBATE TA-D142-0529-PULSE
Technical Architect Position — Mentions Legales Gate: Code-Gen vs Manual
Pulse timestamp: 2026-03-31 05:29 UTC

---

REBUTTAL OF TA-0517: CODE-GEN DOES NOT RESOLVE D142

TA-0517 proposes that a code generator producing mentions legales from SIREN/SIRET/RCS/TVA config makes the D142 gate machine-verifiable. I agree that is a better architecture than Louis manually writing four templates. But TA-0517 buries a critical dependency: the generator is useless without inputs.

If Louis does not have his SIREN, SIRET, RCS, or VAT number on day one of Sprint 0, the code generator produces nothing. The gate is not met. The five-day timeline remains conditional. TA-0517's position assumes the data exists. D142 says it does not. That is the actual problem.

What code-gen does not solve:
- Louis not having business registration numbers ready at Sprint 0 start
- Louis not knowing which legal form applies to a client (SAS, SARL, auto-entrepreneur?)
- Legal nuance: some mentions are required only for certain business types or revenue thresholds
- The fact that placeholder values in a generator are functionally identical to a manually written placeholder block — neither is legally valid

Code-gen adds complexity and a dependency that may not be satisfied on day one. It is a good long-term architecture. It is not a sprint-unblocking solution.

---

MINIMUM VIABLE MENTIONS LEGALES

The bare minimum Louis MUST have before any mentions legales block is legally functional:

1. Company name
2. Legal form (SAS, SARL, EI, etc.)
3. Registered address
4. A contact mechanism (email or phone)

Everything else — SIREN, SIRET, RCS, VAT, capital social, director name, activity declaration — can be placeholdered, bracketed, or marked [A COMPLETER] provided the page is not publicly live and the placeholder is clearly tagged for completion before launch.

For Sprint 0 purposes, the gate criterion should be: does the project have a mentions legales component that is non-empty, structurally correct for the intended legal forms, and flagged with all missing fields? If yes, the gate is met. The five-day timeline is not conditional on perfect data — it is conditional on Louis doing the work to document what he has and what he does not.

---

TWO-OPTION DECISION FOR LOUIS

Option A — Partial config now, generate what you can:
Populate whatever business registration data you have TODAY. Even one SIREN number is enough to generate partial mentions. Leave remaining fields as clearly marked placeholders. This is the honest approach: it shows the team exactly what is missing, and it makes the missing data visible and tractable.
Outcome: Gate met in spirit. Sprint 0 proceeds. Missing data is tracked as open items.

Option B — One generic mentions legales block for all client types:
Write a single block of placeholder mentions legales that is structurally valid but intentionally vague. Cover the minimum required fields. Mark everything else as [A COMPLETER]. This defers all client-specific legal nuance to post-Sprint 0.
Outcome: Gate met technically. Sprint 0 proceeds. You have a placeholder that will need full revision per client type.

Recommendation: Option A is architecturally superior and more honest. But Option B is the fallback if Louis genuinely cannot gather any registration data in the next 24 hours. The key constraint is: do not let the absence of perfect data prevent the Sprint 0 kickoff.

---

D142 STATUS: OPEN

D142 is not resolved by TA-0517's code-gen proposal. The gate requires Louis to produce mentions legales — generated or manual, partial or complete — as a deliberate action. The code-gen architecture is a valid long-term position but it does not unblock Sprint 0 today. Louis needs to choose Option A or Option B and execute. Until he does, D142 remains OPEN.
