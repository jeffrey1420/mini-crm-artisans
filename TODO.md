# Mini-CRM → Devis & Factures — Resolved Decisions & TODO

> **Pivot applied 2026-03-30** — Based on external review. Full pivot from "CRM for artisans" to "devis/factures/relances tool."

## ✅ Resolved Decisions

| ID | Topic | Decision | Source | Date |
|----|-------|----------|--------|------|
| D1 | Positioning | Kill "CRM" — sell "devis, factures, relances" | External review | 2026-03-30 |
| D2 | MVP scope | 4 features only: client file, quote, invoice, reminder | External review | 2026-03-30 |
| D3 | Primary persona | Marc — solo smartphone-native artisan | External review | 2026-03-30 |
| D4 | Stack | Single managed Postgres, NOT per-customer VPS | External review | 2026-03-30 |
| D5 | Pricing | €29/€49/€79 tiered (kept from previous) | Previous debate | 2026-03-30 |
| D6 | Trial | 30 days (kept from previous) | Previous debate | 2026-03-30 |
| D7 | Architecture | Nuxt 3 + OVH managed Postgres | Updated | 2026-03-30 |
| D8 | E-invoicing | v2 feature (Chorus Pro compatible) | External review | 2026-03-30 |
| D9 | Not MVP | No Kanban, no multi-user, no offline, no API keys | External review | 2026-03-30 |
| D10 | Buyer trigger | "Admin pain" not "CRM need" | External review | 2026-03-30 |

## 🔄 Still Unresolved

| ID | Topic | blockers |
|----|-------|----------|
| U1 | Real discovery | Need to watch 10 artisans do admin tasks before building |
| U2 | E-invoicing platform | Which Chorus Pro alternative for MVP? |
| U3 | Landing page angle | ROI vs simplicity framing |

## 📋 Current TODO

### Before Building (Do First)
- [ ] Go watch 10 artisans create quotes and chase payments (NOT more docs)
- [ ] Pick one: Tolteck competitor or Tolteck complement?
- [ ] Define e-invoicing approach (Chorus Pro API vs private provider)
- [ ] Buy domain (not alize, something memorable)

### MVP Build (After Discovery)
- [ ] Client file feature
- [ ] Quote/devis feature (create, send via WhatsApp)
- [ ] Invoice/facture feature (French-legal, sequential numbering)
- [ ] Reminder/relance feature

### NOT Building Until Post-Launch
- [ ] Multi-user
- [ ] Kanban pipeline
- [ ] Per-customer VPS
- [ ] Offline mode
- [ ] API keys/webhooks
- [ ] E-invoicing (v2 only)

## 🚫 What We Deleted

The following were overengineered or wrong:
- Per-customer VPS architecture (too expensive, too complex)
- Kanban as primary view (imposes PM thinking on people who don't manage projects)
- Full multi-tenant architecture (not needed at launch)
- OAuth/MFA for launch
- Inventory management
- Fancy analytics

---

| U3 | Landing page | ROI vs simplicity framing | New: Product Strategist argues against "Simple comme WhatsApp" — ROI-first + control framing stronger |
| U4 | Home view | Client Timeline vs Dashboard | New: Growth Strategist argues Dashboard-first creates daily habit, Timeline is passive |
| U5 | PWA vs Native | Capacitor from day one | REVISED: PWA first (launch), native within 6 months — Debate 11 revision |

---

## New from Pulse 2026-03-30T10:19

- **Debate 11 revision:** PWA first at launch, native app within 6 months post-launch (Capacitor hidden costs underestimated at 3-person MVP)
- **Landing page (U3):** Product Strategist challenges "Simple comme WhatsApp" — attracts wrong customer, signals low value vs free; proposes "Gagnez 2h/semaine" + "ras-le-bol de courir" emotional hook
- **Home view (U4):** Growth Strategist argues Dashboard-first ("À suivre", "Relances dues", "Devis en attente", "Ce mois-ci") creates daily habit vs Timeline's passive archive behavior

---

*Last updated: 2026-03-30T10:19*
