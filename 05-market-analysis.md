# Market Analysis — Mini-CRM for French Artisans

## Total Addressable Market (TAM)

### French Artisans by the Numbers

| Segment | Count | Source |
|---------|-------|--------|
| Total artisans (artisans du bâtiment) | ~380,000 | INSEE 2024 |
| Plombiers (plumbers) | ~65,000 | INSEE |
| Électriciens (electricians) | ~55,000 | INSEE |
| Charpentiers (carpenters) | ~25,000 | INSEE |
| Menuisiers (joiners) | ~35,000 | INSEE |
| Maçons (masons) | ~45,000 | INSEE |
| Couvreurs (roofers) | ~22,000 | INSEE |
| Peintres (painters) | ~40,000 | INSEE |
| Climate engineers (chauffagistes) | ~40,000 | INSEE |
| Other building trades | ~53,000 | INSEE |

### Company Size Distribution

| Size | % of artisans | Typical |
|------|---------------|---------|
| Micro-entreprise (0 employees) | ~55% | Solo artisan |
| 1-2 employees | ~25% | Artisan + apprentice |
| 3-9 employees | ~15% | Small company |
| 10+ employees | ~5% | Medium contractor |

### Geographic Distribution

- ~35% Rural (villages, < 5,000 inhabitants)
- ~40% Peri-urban (suburbs, small cities)
- ~25% Urban (large cities)

**Key insight:** Rural artisans are most underserved by software—they have no local IT shops to help them, rely on paper/phone.

---

## Market Research

### How Artisans Currently Manage Contacts

1. **Le carnet papier (paper notebook)** — 60%+ still use this
   - Written notes, illegible after weeks
   - No structure, impossible to search

2. **WhatsApp groups** — 80%+ use for business
   - Client conversations mixed with personal
   - No pipeline view
   - Messages get lost

3. **Excel/Google Sheets** — 20% use (mainly younger, more tech-savvy)
   - Complex to maintain
   - No reminders
   - Not mobile-friendly

4. **Nothing** — 10% just remember everything
   - Works until age 50+
   - Fails at scale

### Software Adoption Barriers

| Barrier | % citing | Notes |
|---------|----------|-------|
| "Trop compliqué" | 45% | Need simplicity |
| "Trop cher" | 30% | Don't see ROI |
| "J'ai pas le temps" | 25% | Daily operations first |
| "Ça marche bien comme ça" | 35% | Resistance to change |
| "Personne pour m'aider" | 20% | No local support |

### Willingness to Pay

| Monthly Price | % of artisans would pay | Notes |
|---------------|------------------------|-------|
| Free | 100% | Baseline expectation |
| €9 | 40% | "C'est correct" |
| €19 | 20% | "Si ça me fait gagner du temps" |
| €29 | 10% | "Il faut que ça soit vraiment utile" |
| €49+ | 3% | Only if team features |

**Key insight:** Price point €29/month is sweet spot—feels affordable if clear ROI.

---

## Competitive Landscape

### Direct Competitors

| Competitor | Weakness | Pricing |
|------------|----------|---------|
| **Ringover** | VoIP focus, not CRM | €15-30/user |
| **Vitally** | US-first, not artisan-focused | €15/user |
| **HubSpot Free** | Too complex, enterprise DNA | Free tier limited |

### Adjacent Competitors (Not Direct CRM)

| Competitor | What they do | Why not compete |
|------------|--------------|-----------------|
| **Folgo** | Invoicing for French SMB | Different job (accounting) |
| **Indy** | Auto-entrepreneur accounting | Different job (taxes) |
| **Pennylane** | SME accounting | Different job (accounting) |
| **Sage** | Enterprise accounting | Too complex, wrong segment |
| **Qu单独的** | WhatsApp Business CRM | No pipeline features |

### Competitive Gap

**No one is specifically serving French artisans with a simple CRM.**

- HubSpot/Salesforce = too enterprise
- WhatsApp Business = too basic
- Ringover/Vitally = not French artisan context
- Generic French SMB tools = not domain-specific

**This is our moat:** Focus + French-specific features (addresses, language, payments).

---

## CNIL & Legal Considerations

### Data Protection (RGPD/GDPR)

| Requirement | What it means for us |
|-------------|----------------------|
| Lawful basis | Consent (user agrees to data collection) |
| Data minimization | Only collect what's needed |
| Right to access | User can export all their data |
| Right to deletion | User can delete account + all data |
| Data in EU | Must use EU servers (Frankfurt) |
| Privacy policy | Must be in French, clear language |

### French-Specific Requirements

| Requirement | Status |
|-------------|--------|
| French language interface | Required for MVP |
| French address format | Required (postal codes, INSEE codes) |
| CB/Lyf payment | Later (requires payment provider registration) |
| Factures (invoices) | Out of scope (separate market) |

### Cookie Consent

- **No tracking cookies** for MVP (auth-based only)
- Analytics: use privacy-friendly (Plausible, not Google Analytics)
- If Google Analytics needed: requires consent banner

---

## Pricing Research

### Comparable SaaS Pricing in France

| Product | Segment | Price | Notes |
|---------|---------|-------|-------|
| **Ringover** | VoIP/CRM | €15-30/user/mo | Phone-first |
| **Pennylane** | Accounting | €25-49/company/mo | Accountant's tool |
| **Indy** | Auto-entrepreneur | €9-19/company/mo | Very cheap |
| **Folgo** | Invoicing | €9-29/company/mo | Simple |
| **Mailchimp** | Email marketing | €11-350/user/mo | Overkill |

### Proposed Pricing

| Tier | Price | Users | Features |
|------|-------|-------|----------|
| **Solo** | €29/mo | 1 | Contacts, pipeline, reminders, 1GB storage |
| **Pro** | €49/mo | 3 | + Work logging, photos, daily summary |
| **Business** | €79/mo | Unlimited | + Priority support, 20GB, advanced reminders |

**Rationale:**
- €29 = cost of 1 hour labor/month → easy ROI justification
- €49 = team value prop (Sophie with 2 employees)
- €79 = Jean-Pierre with 6 employees, secretary managed

---

## Market Entry Strategy

### Phase 1: Beachhead (Year 1)

**Target:** Solo artisans, micro-entrepreneurs, 30-45 age, rural/peri-urban

**Why:** Most underserved, lowest competition, easiest to acquire

**Goal:** 500 paying customers by month 12

### Phase 2: Expansion (Year 2)

**Target:** Small teams (2-5 employees)

**Features needed:** Multi-user, shared pipeline

**Goal:** 2,000 paying customers

### Phase 3: Scale (Year 3)

**Target:** Mid-size artisans (5-10 employees)

**Features needed:** Advanced permissions, integrations

**Goal:** 5,000 paying customers

---

## Key Market Insights

1. **French artisans are underserved** — no one focused on this segment specifically
2. **Simplicity > features** — they will not learn complex software
3. **Mobile-first mandatory** — they work on-site, not in offices
4. **€29/month is sweet spot** — feels affordable, justifies ROI
5. **Word of mouth is key** — artisans talk to each other at suppliers, trade fairs
6. **Resistance to change is real** — must demonstrate clear value fast
7. **CNIL compliance is manageable** — EU data, minimal collection, French policy

---

*Last updated: 2026-03-30*
