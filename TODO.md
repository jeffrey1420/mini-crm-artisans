# Mini-CRM — Resolved Decisions & TODO

> Auto-generated from debate log. Updated by 5-min pulse agents.

## ✅ Resolved Decisions

| ID | Topic | Decision | Source | Date |
|----|-------|----------|--------|------|
| D1 | Mobile-first | Mobile-first, responsive desktop | Product Strategist | 2026-03-30 |
| D2 | Pricing | €29/€49/€89 tiered (Solo €29 unchanged, Pro €49, Business €89 up from €79) | Growth Strategist | 2026-03-30 |
| D3 | Stack | Nuxt 3 + Supabase → REVISED to OVH self-hosted Postgres | Technical Architect | 2026-03-30 |
| D4 | Multi-user | Single-user MVP, multi-user in Q2 | Technical Architect | 2026-03-30 |
| D5 | Offline mode | Online-first MVP, offline within 6 months | Compromise | 2026-03-30 |
| D6 | Payments | Stripe + CB first, Lyf Pay Year 2 | Growth Strategist | 2026-03-30 |
| D7 | Kanban | 4-column (Devis/Accepté/En cours/Terminé), tap-to-move — REVISED: secondary tab only | Debate 14 resolution | 2026-03-30 |
| D14 | Core view | Client Timeline home, Kanban in secondary "Jobs" tab | Debate 14 resolution | 2026-03-30 |
| D8 | Trial length | 30 days (was 14 vs 30) | Growth Strategist | 2026-03-30 |
| D9 | Stack (revisited) | OVH self-hosted Postgres day-one (was Supabase) — REVISED: bare VPS replaced with OVH Cloud SQL managed Postgres | Tech Architect (Debate 13 revision) | 2026-03-30 |
| D13 | Database ops | OVH Cloud SQL managed Postgres (not bare VPS) — self-hosted = not self-operated | Debate 13 resolution | 2026-03-30 |
| D15 | Pricing (revisited) | Keep €29 solo, ROI story in onboarding not on pricing page | Growth Strategist | 2026-03-30 |

## 🔄 Unresolved — Needs Louis Decision

| ID | Topic | Options | blockers |
|----|-------|---------|----------|
| U1 | Contact import MVP | Add vCard + phone import to MVP scope | Was marked "Soon" in feature matrix |
| U2 | PWA vs Native | Capacitor native shell recommended over PWA | "PWA acceptable" needs revisiting |
| U3 | GTM channel | Trade fairs vs digital-first (Google/Facebook) | €1k vs €360 CAC difference |
| U4 | Home view — Dashboard | Client Timeline vs Stats Dashboard as home | Debate 16 — two product identities |

## 📋 Current TODO (from debates)

- [ ] **D9/D13 UPDATE:** Revise `04-technical-architecture.md` — replace all Supabase references with OVH Cloud SQL (managed Postgres, not bare VPS)
- [ ] **D13:** Add OVH Cloud SQL to infrastructure costs — verify free tier limits, plan scaling path (Starter 1vCPU/2GB → Business 2vCPU/4GB)
- [ ] **D14 UPDATE:** Revise `03-feature-matrix.md` — Client Timeline is home view, Kanban moves to secondary "Jobs" tab
- [ ] **D15 UPDATE:** Add ROI framing to onboarding email sequence and in-app usage reports; update landing page secondary copy with ROI proof points
- [ ] **D15 UPDATE:** Revise pricing page — keep €29 solo, €49 Pro, €89 Business; add ROI proof points below fold
- [ ] **U1:** Move contact import (vCard, phone) from "Soon" to MVP scope in `03-feature-matrix.md`
- [ ] **U2:** Reconsider PWA vs Capacitor — update mobile strategy
- [ ] **U3:** Kill trade fair budget, reallocate to Google Ads + Facebook Groups
- [ ] **U4:** Debate 16 — decide between Client Timeline home vs. Dashboard home
- [ ] **Debate 10:** Add import buttons to MVP — update feature matrix
- [ ] **Debate 11:** Capacitor investigation — add to devops/frontend roadmap
- [ ] **Debate 12:** Rebalance GTM — update marketing roadmap with digital-first priority

## 🔜 Next Sprint Decisions

- Referral program design (€20 credit vs cash)
- Stripe + CB integration spec
- vCard parser approach (npm package vs custom)
- Debate 16: Landing page ROI-first ("gagnez 2h/semaine") vs simplicity-first ("simple comme WhatsApp")
- Auth method: magic link vs. phone OTP at signup (phone-first adds friction but enables SMS reminders)

---

*Last updated: 2026-03-30T10:15:00Z*
