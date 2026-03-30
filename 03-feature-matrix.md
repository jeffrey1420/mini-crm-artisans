# Feature Matrix — Mini-CRM for French Artisans

## Priority Definitions

| Priority | Meaning | Rationale |
|----------|---------|-----------|
| **MVP** | Day 1 launch | Pain is immediate, solution is simple |
| **Soon** | Within 3 months | Clear need, moderate complexity |
| **Later** | 6+ months | Nice to have, low urgency |
| **Out of Scope** | Not doing | Too complex, wrong audience, not our job |

---

## Feature Categories

### 1. Contact Management

| Feature | Priority | Rationale |
|---------|----------|-----------|
| Add/edit/delete contacts | **MVP** | Core CRM — no contacts = nothing |
| Contact fields: Name, phone, email, address | **MVP** | French address format (rue, code postal, ville) |
| Contact photos | **Soon** | Artisans like visual ID of clients |
| Notes per contact | **MVP** | "Client difficile", "A rappelé 3x" |
| Search contacts | **MVP** | By name, phone, address |
| Import from phone contacts | **Soon** | Reduce friction to get started |
| Contact groups/tags | **Later** | "Clients priorité haute" |

### 2. Pipeline / Project Tracking

| Feature | Priority | Rationale |
|---------|----------|-----------|
| Pipeline stages | **MVP** | Devis → Accepté → En cours → Terminé (4 stages) |
| Move deals between stages | **MVP** | Drag or tap |
| Pipeline view (kanban) | **MVP** | Visual = better than spreadsheet |
| Deal amount (€) | **Soon** | Know how much each project is worth |
| Deal notes/description | **MVP** | What work? Which materials? |
| Multiple contacts per deal | **Later** | Decision maker vs on-site contact |

### 3. Reminders & Tasks

| Feature | Priority | Rationale |
|---------|----------|-----------|
| Create reminder from contact | **MVP** | "Rappeler M. Martin" |
| Push notification | **MVP** | Must interrupt — not just badge |
| Reminder time picker | **MVP** | Tomorrow 9h, in 3 days, specific date |
| Daily reminder summary | **Soon** | Morning push: "Vous avez 3 rappels aujourd'hui" |
| Overdue reminders | **MVP** | Show what's late, highlight it |
| Recurring reminders | **Later** | "Entretien chaUDIÈRE chaque année" |

### 4. Job/Work Tracking

| Feature | Priority | Rationale |
|---------|----------|-----------|
| Log work done (basic) | **MVP** | "Réparation", "Installation", "Devis" |
| Date + duration | **Soon** | Track time spent |
| Materials used | **Later** | Linked to inventory (complex) |
| Attach photos | **Soon** | "Voici ce que j'ai fait" |
| Work history per contact | **Soon** | Full context on return visits |

### 5. Communications

| Feature | Priority | Rationale |
|---------|----------|-----------|
| Call client directly (tap phone number) | **MVP** | Opens phone dialer |
| Send SMS from app | **Soon** | French artisans use SMS heavily |
| WhatsApp direct link | **MVP** | Opens WhatsApp with contact's number |
| Email from app | **Later** | Less common for artisans |
| Email sequences | **Out of Scope** | Too "salesy", not artisanal |

### 6. French-Specific

| Feature | Priority | Rationale |
|---------|----------|-----------|
| French address formatting | **MVP** | Code postal + ville auto-complete |
| French phone number formatting | **MVP** | +33 format |
| CB/Lyf payment integration | **Later** | In-app payment (complex regulatory) |
| French invoices | **Out of Scope** | Separate product (Folgo, Indy exist) |
| Départment auto-detect from phone | **Soon** | UX polish |

---

## Out of Scope (永远不做)

| Feature | Why |
|---------|-----|
| Inventory/stock management | Different product entirely |
| Accounting integration | Indy, Pennylane already exist |
| Project management (tasks, subtasks) | Too complex, wrong audience |
| Email sequences/automation | Artisans don't do drip campaigns |
| API / integrations | MVP first, no one will use it |
| White-label | Future maybe, not now |
| Multi-language | French only for MVP |
| Desktop app | Mobile-first or nothing |

---

## Feature Comparison: MVP vs Full

### MVP Scope (€29/month)
- Contact management (unlimited contacts)
- Pipeline (4 stages, unlimited deals)
- Basic reminders (push notifications)
- 1 user only
- Mobile app (iOS + Android)
- Offline mode

### Pro Tier (€49/month)
- Everything in MVP
- Multi-user (up to 3)
- Work logging with photos
- Daily summary notifications
- 5GB storage

### Business Tier (€79/month)
- Everything in Pro
- Unlimited users
- Advanced reminders (recurring)
- Priority support
- 20GB storage

---

## What Makes Us Different

| Competitor | Weakness | Our Edge |
|------------|----------|----------|
| Excel/Notebook | No reminders, no sync, not shared | Cloud + reminders |
| Salesforce/HubSpot | 100% too complex, enterprise pricing | Artisan-simple UX |
| Ringover/Vitally | Not French artisan focused | Domain-specific features |
| WhatsApp Business | No pipeline, no reminders | Real CRM features |

---

*Last updated: 2026-03-30*
