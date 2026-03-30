# Technical Architecture — Mini-CRM

## Stack Recommendation

### Primary Option: Nuxt 3 + Supabase

**Rationale:**
- Nuxt 3 = Vue 3 + SSR + great DX
- Supabase = PostgreSQL + Auth + Real-time + Edge Functions
- Both have generous free tiers
- Both are well-documented in French community
- Supabase handles offline sync potential

### Why Not Alternatives

| Option | Why NOT |
|--------|---------|
| Pure Firebase | Lock-in, expensive at scale, French clients worry about US data |
| MariaDB + custom API | More ops work, no real-time, harder to iterate |
| PocketBase | Too new, smaller community, less French adoption |
| Strapi | Overkill for simple CRM, headless CMS focus |
| Shopify-style | Wrong model, monthly cost |

### Architecture Diagram

```
┌─────────────────────────────────────────────────────────┐
│                    CLIENT LAYER                         │
│  ┌─────────────────┐     ┌─────────────────┐            │
│  │   Nuxt 3 App    │     │   Capacitor      │            │
│  │  (Web + Mobile) │ ←── │  (iOS/Android)   │            │
│  └────────┬────────┘     └─────────────────┘            │
│           │                                               │
└───────────┼───────────────────────────────────────────────┘
            │ HTTPS
┌───────────┴───────────────────────────────────────────────┐
│                   SUPABASE LAYER                          │
│  ┌──────────────────────────────────────────────────┐     │
│  │  PostgreSQL Database                              │     │
│  │  - contacts                                      │     │
│  │  - deals                                         │     │
│  │  - reminders                                     │     │
│  │  - work_logs                                     │     │
│  │  - users                                         │     │
│  └──────────────────────────────────────────────────┘     │
│  ┌────────────┐  ┌────────────┐  ┌────────────────┐       │
│  │   Auth      │  │ Real-time  │  │ Edge Functions │       │
│  │  (Magic     │  │ (presence, │  │  (notifications│       │
│  │   links)    │  │  sync)     │  │   push)        │       │
│  └────────────┘  └────────────┘  └────────────────┘       │
└───────────────────────────────────────────────────────────┘
            │
┌───────────┴───────────────────────────────────────────────┐
│                   HOSTING (Coolify)                       │
│  - Nuxt app deployed on Coolify                           │
│  - Supabase Cloud (or self-hosted Postgres)               │
│  - Objective: migrate to self-hosted later                │
└───────────────────────────────────────────────────────────┘
```

---

## Database Schema

### Tables

```sql
-- Users (Supabase Auth handles this)
-- Extended with profile
CREATE TABLE profiles (
  id UUID PRIMARY KEY REFERENCES auth.users(id),
  full_name TEXT NOT NULL,
  phone TEXT,
  subscription_tier TEXT DEFAULT 'free', -- free, pro, business
  created_at TIMESTAMPTZ DEFAULT now()
);

-- Contacts (clients)
CREATE TABLE contacts (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES profiles(id),
  
  -- Basic info
  first_name TEXT NOT NULL,
  last_name TEXT,
  company_name TEXT,
  
  -- Contact
  phone TEXT,
  email TEXT,
  
  -- French address
  address_line1 TEXT,
  address_line2 TEXT,
  postal_code TEXT,
  city TEXT,
  department TEXT, -- auto-extracted from postal_code
  
  -- Meta
  notes TEXT,
  photo_url TEXT,
  tags TEXT[], -- ['priority', 'urgent']
  
  created_at TIMESTAMPTZ DEFAULT now(),
  updated_at TIMESTAMPTZ DEFAULT now()
);

-- Deals / Pipeline
CREATE TABLE deals (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES profiles(id),
  contact_id UUID REFERENCES contacts(id),
  
  title TEXT NOT NULL, -- "Rénovation salle de bain Martin"
  amount_cents INTEGER, -- store as cents, display as euros
  stage TEXT NOT NULL DEFAULT 'devis', -- devis, accepte, en_cours, termine
  stage_order INTEGER DEFAULT 0, -- for ordering within stage
  
  notes TEXT,
  
  created_at TIMESTAMPTZ DEFAULT now(),
  updated_at TIMESTAMPTZ DEFAULT now(),
  stage_changed_at TIMESTAMPTZ DEFAULT now()
);

-- Reminders
CREATE TABLE reminders (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES profiles(id),
  contact_id UUID REFERENCES contacts(id),
  deal_id UUID REFERENCES deals(id),
  
  title TEXT NOT NULL, -- "Rappeler pour devis"
  due_at TIMESTAMPTZ NOT NULL,
  completed_at TIMESTAMPTZ,
  
  recurrence TEXT, -- null, 'daily', 'weekly', 'monthly', 'yearly'
  
  created_at TIMESTAMPTZ DEFAULT now()
);

-- Work Logs
CREATE TABLE work_logs (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES profiles(id),
  contact_id UUID REFERENCES contacts(id),
  deal_id UUID REFERENCES deals(id),
  
  work_type TEXT NOT NULL, -- 'devis', 'intervention', 'installation', 'repair'
  description TEXT,
  
  duration_minutes INTEGER,
  occurred_at DATE DEFAULT now(),
  
  photo_urls TEXT[],
  
  created_at TIMESTAMPTZ DEFAULT now()
);

-- FCM Push Tokens (for mobile notifications)
CREATE TABLE push_tokens (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES profiles(id),
  token TEXT NOT NULL,
  device_type TEXT NOT NULL, -- 'ios', 'android'
  created_at TIMESTAMPTZ DEFAULT now()
);
```

### Indexes

```sql
CREATE INDEX idx_contacts_user ON contacts(user_id);
CREATE INDEX idx_deals_user ON deals(user_id);
CREATE INDEX idx_deals_stage ON deals(user_id, stage);
CREATE INDEX idx_reminders_user_due ON reminders(user_id, due_at) WHERE completed_at IS NULL;
CREATE INDEX idx_work_logs_contact ON work_logs(contact_id);
```

---

## API Design (Supabase Edge Functions)

### Key Endpoints via Supabase Client SDK

**Contacts:**
- `GET /rest/v1/contacts?user_id=eq.{id}` — List user's contacts
- `POST /rest/v1/contacts` — Create contact
- `PATCH /rest/v1/contacts?id=eq.{id}` — Update contact

**Deals:**
- `GET /rest/v1/deals?user_id=eq.{id}&select=*,contact:*` — List with contact info
- `POST /rest/v1/deals` — Create deal
- `PATCH /rest/v1/deals?id=eq.{id}` — Update deal (including stage change)

**Reminders:**
- `GET /rest/v1/reminders?user_id=eq.{id}&completed_at=is.null&due_at=lte.{tomorrow}` — Overdue + today's
- `POST /rest/v1/reminders` — Create reminder
- `PATCH /rest/v1/reminders?id=eq.{id}` — Mark complete

### Push Notifications (Edge Function)

```typescript
// supabase/functions/send-reminder-notification/index.ts
// Triggered by cron every 15 minutes
// Queries reminders due in next 15 min
// Sends FCM push via firebase-admin
```

---

## Offline-First Strategy

### Phase 1: Optimistic UI (MVP)
- All writes go to local state immediately
- Sync to server in background
- If offline, queue writes
- On reconnect, push to server

### Phase 2: PWA with Service Worker (3 months)
- Cache app shell + recent data
- Full offline reads
- Background sync for writes

### Phase 3: Native App via Capacitor (6 months)
- Capacitor wraps Nuxt PWA into native iOS/Android
- Local SQLite via `@capacitor-community/sqlite`
- Bidirectional sync when online

---

## MVP Technical Scope

### Must Have for Launch
- [ ] Supabase project (free tier)
- [ ] Nuxt 3 app with SSR
- [ ] User auth (magic link email)
- [ ] CRUD for contacts, deals, reminders
- [ ] Pipeline kanban view
- [ ] Basic push notifications (web push)
- [ ] French address formatting
- [ ] Responsive mobile-first CSS

### Skip for MVP
- [ ] Mobile apps (PWA is fine for launch)
- [ ] Offline mode (launch online-only)
- [ ] FCM push for iOS (complex, web push first)
- [ ] Multi-user sync (single user MVP)
- [ ] File uploads (photos) — later

---

## Deployment (Coolify)

```yaml
# docker-compose.yml for Nuxt
services:
  nuxt:
    build: .
    ports:
      - "3000:3000"
    environment:
      - SUPABASE_URL=${SUPABASE_URL}
      - SUPABASE_ANON_KEY=${SUPABASE_ANON_KEY}
```

```bash
# Deploy commands
cd /data/workspace/mini-crm-research
# Assuming Nuxt app is in ./app directory
# coolify deploy --name mini-crm --repo jeffrey1420/mini-crm-artisans
```

---

## Security Considerations

### Row-Level Security (Supabase)
```sql
-- Enable RLS on all tables
ALTER TABLE contacts ENABLE ROW LEVEL SECURITY;

-- Users can only see their own data
CREATE POLICY "Users see own contacts" ON contacts
  FOR ALL USING (auth.uid() = user_id);

CREATE POLICY "Users see own deals" ON deals
  FOR ALL USING (auth.uid() = user_id);

CREATE POLICY "Users see own reminders" ON reminders
  FOR ALL USING (auth.uid() = user_id);
```

### CNIL Compliance
- French users → data stored in EU (Supabase has Frankfurt region)
- No cookies for tracking without consent (use auth only)
- User can export/delete their data
- Privacy policy in French required

---

*Last updated: 2026-03-30*
