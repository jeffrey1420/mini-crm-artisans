# Pulse 2026-03-30T17:29 — Technical Architect

## Debate 78: JWT Is the Wrong Auth Primitive for a Solo Artisan App

**Challenge:** D74 resolved Sprint 0 JWT scope = contract + stubs + @fastify/jwt config (0.5-1 day). Full auth (Keychain, refresh rotation, logout) deferred to Sprint 1. The assumption challenged: JWT is the right auth mechanism for a solo artisan app.

### Core Argument

**The Flawed Premise:**

D74 assumes JWT is the right auth primitive. It isn't — for this app, that assumption is wrong.

**The target user is a solo French artisan.** One person. One phone. One device. The auth surface is a single-user, single-device model. JWT was designed for distributed stateless auth across microservices and multi-user sessions. We're hammering a finishing nail with a sledgehammer.

### What D74 Got Wrong

D74 deferred "full auth" (Keychain, refresh rotation, logout) to Sprint 1, treating JWT setup as cheap "scaffolding." But even the scaffold costs 0.5–1 day and delivers **zero user-facing value**. The artisan doesn't care if we use JWT or UUIDs — they care about creating their first devis.

**JWT introduces hidden complexity:**
- `@fastify/jwt` dependency and configuration
- Token generation, signing, verification logic
- TTL management (when does it expire? what happens then?)
- Refresh endpoint or rotation strategy
- Logout = token blacklist or shorter TTL = more complexity

### The API Key Alternative

For a solo artisan, **API key auth is objectively sufficient:**

```js
// Server: single endpoint to validate token
GET /api/auth/verify → { valid: true, artisanId: 'uuid' }

// Client: one UUID stored in Expo SecureStore
Authorization: Bearer <uuid>

// That's it. No library. No TTL. No refresh.
```

**Time comparison:**
- JWT scaffold: 0.5–1 day (D74's own estimate)
- API key auth: ~2 hours

That's 2–6 hours of Sprint 0 capacity reclaimed. For a 5-day sprint building French compliance foundations, that's meaningful.

### When JWT Makes Sense (Not Here)

JWT earns its complexity when you need:
- Stateless auth across multiple services
- Multi-user sessions with different permission levels
- Token sharing across devices/sessions
- Short-lived tokens with no server state

None of these apply to a solo artisan on one device.

### Verdict

**API key auth should replace JWT for Sprint 0.** JWT should be reconsidered for Sprint 2 only if multi-user or admin handler sharing becomes a real requirement.

The "contract + stubs + @fastify/jwt config" is not free scaffolding — it's technical debt masquerading as preparation.

### New Action Items

1. **Override D74**: Replace JWT with API key auth in Sprint 0 scope
2. **Schema add**: `artisan.api_key UUID DEFAULT gen_random_uuid()` — replaces the JWT user-token table
3. **Sprint 0 auth scope**: `/api/auth/verify` endpoint + SecureStore stub in Expo, ~2 hours
4. **Re-evaluate JWT**: Sprint 2 backlog item, triggered only by multi-user requirement
