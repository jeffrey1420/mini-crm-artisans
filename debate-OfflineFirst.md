## Debate: Offline-First — Required at Launch or v2?

### Challenge
D9's "no offline" decision was made before the mobile stack was chosen. React Native changes the calculus — offline capability is no longer a complex infrastructure problem but a client-side storage problem that Expo solves in hours, not sprints.

### Your Argument

**Position: Offline capability is REQUIRED at launch. Not v2. Not "nice to have."**

The "no offline" decision in D9 made sense for a web-based Nuxt 3 application where every interaction is an API call. For a React Native mobile app used by artisans on job sites — basements, rural properties, areas with dead zones — connectivity dependency is a product-killing failure mode, not a minor inconvenience.

**5 core points:**

1. **The product fails at exactly the moments it matters most.** Marc's worst admin day is when he's at a job site with no signal, standing in front of a client, and needs to pull up a devis or create a new one. If the app shows "no connection" at that moment, the product has failed its core job. You cannot build a mobile-first CRM for field workers on a connectivity-dependent architecture.

2. **"v2 offline" is how you lose your first 100 users.** Early adopters are the most forgiving and the most vocal. If Marc downloads the app, uses it successfully for 3 weeks, then loses a client meeting because his phone had no signal — he doesn't say "I'll try v2 when they add offline." He leaves a 1-star review and tells his WhatsApp group "that app doesn't work on job sites." First impressions with this demographic are unrecoverable.

3. **The stack change invalidates the original "no offline" reasoning.** D9's offline exclusion was justified by complexity: "no Kanban, no multi-user, no offline, no API keys." The complexity argument for offline was that it required solving conflict resolution, sync algorithms, and distributed state. But with React Native + Expo, offline is solved at the framework level. WatermelonDB, expo-sqlite, and AsyncStorage handle local persistence. The sync logic for a single-user app is dramatically simpler than D9's framers assumed.

4. **Sprint 0 scope is not the constraint you think it is.** The debate log shows Sprint 0 = "minimum devis flow (3-5 days, minimal schema)." Offline-first architecture doesn't add to Sprint 0 scope — it changes WHERE data is stored (local SQLite first, sync to API second). The API endpoints remain identical. The Fastify backend requires zero changes for Day 1 offline capability. The mobile app stores writes locally and syncs when connectivity returns.

5. **Offline-first is the correct default for mobile CRUD apps, not an advanced feature.** Industry standard: any mobile app that manages user-generated data (clients, devis, factures) should use offline-first architecture. This isn't controversial in mobile development — it's table stakes. The burden of proof should be on "no offline" for a mobile app, not on "offline" for a web app.

### Challenged Assumption
- **Assumption (D9):** "No offline" — offline capability excluded from MVP as too complex for Sprint 0
  **Challenge:** D9 was decided before D17 (React Native from Day 1 via Expo) was resolved. The "offline = complex" argument applied to a web-stack architecture. With React Native + Expo, offline-first is the default pattern, not an engineering Everest. The decision was correct for the stack it was made under. It no longer applies.

- **Assumption (D78):** API-key auth requires live connectivity to validate
  **Challenge:** API-key auth is actually MORE compatible with offline than JWT. API keys can be stored securely on-device and used for sync operations when connectivity returns. No token refresh race conditions. No expiry during dead zones. The switch from JWT → API key (D78) accidentally makes offline EASIER, not harder.

### Technical Specifics

**React Native + Expo offline implementation (realistic for Sprint 0):**

- **Local storage:** WatermelonDB or expo-sqlite for structured data (clients, devis, factures). AsyncStorage for session/auth tokens. Total setup: 2-4 hours with WatermelonDB + Expo.
- **Sync strategy:** Last-write-wins with conflict detection UI. For a solo artisan, conflicts are rare and trivially resolvable — show both versions, let Marc pick. No distributed consensus needed.
- **Backend changes:** Zero. The Fastify API receives the same payloads whether they originate online or offline. Add a `sync_timestamp` field to each record; server accepts the latest write.
- **API key storage:** SecureStorage on device (expo-secure-store). API key never expires, no refresh token to manage.
- **Offline indicator UI:** Subtle "pending sync" badge on records modified offline. No scary error messages. Sync happens silently in background when connectivity returns.
- **What CAN'T be done offline at launch:** Viewing other users' shared data (not applicable — solo users), real-time notifications (already deferred to v2 per D17/D41).
- **What CAN be done offline at launch:** Create/edit clients, create/edit/send devis and factures, view all cached data, manage relance reminders (stored locally).

**Fastify backend implications:**
- Endpoint contract unchanged
- Add `updated_at` timestamp to all entities — used for sync conflict resolution
- Optional: add `client_uuid` as primary key (not server-generated UUID) so offline-created records have stable IDs before sync
- No new infrastructure needed; Postgres handles concurrent writes fine for solo users

### Verdict
**RESOLVED — Offline capability REQUIRED at launch. D9 is REOPENED for the offline component.**

**Specific decision:** Sprint 0 architecture must be offline-first. React Native mobile app uses WatermelonDB/expo-sqlite for local-first data storage. Fastify API adds `updated_at` timestamps and accepts client-generated UUIDs. Sync is last-write-wins with simple conflict UI. No changes to API endpoint contracts. No additional infrastructure.

**Rationale:** The combination of D17 (React Native via Expo) + D78 (API key auth) makes offline-first the correct default, not an advanced feature. D9's exclusion of offline was appropriate for the web-stack era. The mobile stack decision invalidates that reasoning. Building a mobile-first CRM for field artisans without offline capability is a known failure mode — not a theoretical risk.

**What this means for Sprint 0:**
- Mobile app: WatermelonDB integration (half a day) + sync layer (1 day) + conflict UI (half a day) = ~2 days mobile work
- Backend: `updated_at` on all entities + accept client UUIDs = ~2 hours backend work
- Net Sprint 0 impact: +2 days, acceptable given 5-day sprint

**D9 updated:** "No offline" is REMOVED from D9. Replace with: "Offline-first with background sync. Conflict resolution via last-write-wins with manual override for serious conflicts."
