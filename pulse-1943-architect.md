# Technical Architect Counter-Argument: Sprint 0 Can Be 5 Days

## The False Premise in the 19:32 Debate

The 7-8 day estimate was *accepted* because everyone assumed legal research is **part of Sprint 0**. That assumption is wrong, and it's the root cause of the inflated estimate.

**The debate resolved the wrong question.** It accepted that mentions légales = a sprint task. It doesn't.

---

## The Real Blocker: No One Has Done the Prep Work

Right now, the mentions légales text for French devis/factures **does not exist** in a usable form. Louis hasn't researched:
- What text is required for a **particulier** client
- What text is required for a **professionnel français** (SIRET)
- What text is required for a **professionnel UE** (TVA intracommunautaire)
- What text is required for a **professionnel hors-UE**

This is 2 hours of legal/administrative work. **It is not coding.** It should not be in a coding sprint.

---

## The Correct Sequence

**This week (before Sprint 0):**
Louis spends 2 hours researching and writing the 4 mentions légales templates. He produces:
```
/mentions-legales/particulier.md
/mentions-legales/pro-francais.md
/mentions-legales/pro-ue.md
/mentions-legales/pro-hors-ue.md
```

**Sprint 0 starts with ready-to-paste templates.** The engineering task becomes:
1. Copy-paste 4 templates into the database or config files → 30 minutes
2. Build the TVA calculator (French VAT rules are well-defined) → 1 day
3. Build the sequential numbering engine (AAAA-MM-XXXX format) → 1 day
4. Set up Postgres schema for clients, devis, factures → 1 day

**That's 3-4 days of actual engineering.**

---

## Why 7-8 Days Is Still Wrong

The 7-8 day estimate conflates:
- **Pre-sprint prep** (legal research, this week, 2 hours)
- **Sprint 0 engineering** (copy-paste + 3 components, 3-4 days)

If Louis walks into Sprint 0 with the legal text already written, there's nothing left to research. The sprint is purely mechanical. A 5-day sprint with buffer is more than sufficient.

---

## The Action Item

**Louis: spend 2 hours this week writing the 4 mentions légales templates.**

Not in Sprint 0. **Now.** Before the sprint starts.

Sprint 0 is not the place to discover what legal text is required. That's a pre-sprint dependency. The sprint starts when all dependencies are resolved.

---

**Conclusion:** The 7-8 day estimate is not a scope problem — it's a preparation problem. Resolve the prep, shrink the sprint.
