# Backend Roadmap — Mini-CRM

## Objectives

- Provide a robust, scalable backend API for the Mini-CRM targeting French solo artisans (plumbers, electricians, carpenters)
- Enable seamless mobile-first PWA experience via RESTful API endpoints
- Support tiered subscription model (€29/€49/€79/month) with feature gating
- Ensure GDPR compliance for French market data handling
- Integrate with French payment infrastructure (Stripe + CB)
- Host on customer OVH VPS with PostgreSQL self-management
- Achieve <200ms API response times for common operations
- Provide 99.5% uptime SLA capability

## Subdomains

1. **auth-service** — Authentication, authorization, session management
2. **contact-service** — Contact management, vCard import/export
3. **job-service** — Job/work order management, scheduling
4. **invoice-service** — Invoice generation, PDF, French legal compliance
5. **pipeline-service** — Sales pipeline, Kanban-style tracking
6. **notification-service** — Email, SMS, push notifications, reminders
7. **payment-service** — Stripe integration, subscription management
8. **file-service** — Photo uploads, document storage
9. **webhook-service** — Outbound webhooks for integrations
10. **analytics-service** — Usage metrics, business intelligence

## Milestones

- **M1: Foundation** — Auth, database schema, API skeleton, error handling
- **M2: Core CRM** — Contacts, jobs, invoices, pipeline CRUD operations
- **M3: File & Import** — vCard import, photo uploads, document management
- **M4: Payments** — Stripe integration, subscription tiers, CB payments
- **M5: Notifications** — Email, SMS, push, reminders, scheduling
- **M6: Webhooks & Integrations** — Outbound webhooks, third-party integrations
- **M7: Performance & Scale** — Caching, rate limiting, observability, optimization

## Task Categories

---

### Category: Authentication & Authorization

#### Task: AUTH_DB_SCHEMA_001
- **title**: Design and create PostgreSQL auth schema
- **description**: Create users table with id, email, password_hash, created_at, updated_at, last_login, is_active, is_verified fields. Add indexes on email and created_at. Implement row-level security policies for multi-tenancy.
- **inputs**: PostgreSQL connection, migration tool (Drizzle/Knex)
- **outputs**: users table with RLS policies
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Table created with proper indexes, RLS policies enforced, query returns expected columns

#### Task: AUTH_PASSWORD_001
- **title**: Implement secure password hashing with bcrypt/argon2
- **description**: Implement password hashing using bcrypt (cost factor 12) or argon2id. Create utility functions hashPassword(plain) and verifyPassword(plain, hash). Never store plain passwords. Handle password reset flow securely.
- **inputs**: User plain password string
- **outputs**: Hashed password string, boolean verification result
- **dependencies**: [AUTH_DB_SCHEMA_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Unit tests verify hash uniqueness, verification works, same password produces different hashes (salt)

#### Task: AUTH_JWT_001
- **title**: Implement JWT access token generation and validation
- **description**: Create JWT access tokens with 15-minute expiry containing user_id, email, role, subscription_tier claims. Use RS256 algorithm with rotating public/private keys. Implement token validation middleware for protected routes.
- **inputs**: User object (id, email, role, tier)
- **outputs**: JWT access token string, token validation middleware
- **dependencies**: [AUTH_DB_SCHEMA_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Token generated with correct claims, middleware rejects expired/invalid tokens, token verifiable with public key

#### Task: AUTH_JWT_002
- **title**: Implement JWT refresh token rotation
- **description**: Create refresh tokens with 30-day expiry stored in database. Implement refresh token rotation — each use generates new refresh token and invalidates old one. Store refresh_token hash, user_id, device_info, ip_address, expires_at. Clean up expired tokens via scheduled job.
- **inputs**: User id, device info, IP address
- **outputs**: Refresh token record in DB, new access token
- **dependencies**: [AUTH_DB_SCHEMA_001, AUTH_JWT_001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Refresh token grants new access token, old token invalidated after use, expired tokens cleaned up

#### Task: AUTH_MAGIC_LINK_001
- **title**: Implement magic link email authentication
- **description**: Create magic link generation endpoint POST /auth/magic-link sending time-limited (15min) signed URL to user email. Generate signed token containing user_id, email, expiry. Verify signature and exchange for JWT on click. Log magic link usage for security audit.
- **inputs**: User email address
- **outputs**: Magic link email sent, verification endpoint functional
- **dependencies**: [AUTH_DB_SCHEMA_001, AUTH_JWT_001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: fullstack
- **validation**: Magic link received in email, clicking link grants JWT, expired links rejected

#### Task: AUTH_MFA_001
- **title**: Implement TOTP-based 2FA
- **description**: Add TOTP (RFC 6238) support for 2FA. Generate secret on enrollment, store encrypted in DB. Provide QR code for authenticator app setup. Verify 6-digit TOTP codes with 30-second window and 1-step tolerance. Allow users to enable/disable 2FA. Support recovery codes (10 one-time codes).
- **inputs**: User request to enable 2FA, TOTP secret
- **outputs**: QR code URI, encrypted TOTP secret, recovery codes
- **dependencies**: [AUTH_DB_SCHEMA_001, AUTH_JWT_001]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: QR code scannable by Google Authenticator, valid codes grant access, invalid codes rejected, recovery codes work once each

#### Task: AUTH_SESSION_001
- **title**: Implement session management with device tracking
- **description**: Create sessions table tracking active sessions per user. Store session_id, user_id, device_type, device_name, ip_address, last_active, created_at. Limit concurrent sessions based on subscription tier (1/3/unlimited). Invalidate sessions on logout or security event.
- **inputs**: User id, device info, request metadata
- **outputs**: Session record, session list for user
- **dependencies**: [AUTH_DB_SCHEMA_001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Sessions listed per user, old sessions cleaned up, concurrent limit enforced per tier

#### Task: AUTH_OAUTH_001
- **title**: Implement Google OAuth 2.0 login
- **description**: Add Google OAuth 2.0 as social login option. Create OAuth state parameter with CSRF protection. Exchange code for tokens, fetch user profile. Link Google account to existing user or create new account. Store oauth_providers table with provider, provider_user_id, user_id.
- **inputs**: Google authorization code, state parameter
- **outputs**: JWT for authenticated user, linked OAuth provider record
- **dependencies**: [AUTH_DB_SCHEMA_001, AUTH_JWT_001]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: fullstack
- **validation**: Google login flow completes, new user created or existing user linked, JWT returned

#### Task: AUTH_RBAC_001
- **title**: Implement role-based access control (RBAC) system
- **description**: Define roles: owner, admin, member, viewer. Create permissions table with resource and action pairs. Create role_permissions junction table. Assign roles to users per workspace. Implement middleware checking user role against required permission for each endpoint.
- **inputs**: User id, resource, action
- **outputs**: Permission granted/denied decision
- **dependencies**: [AUTH_DB_SCHEMA_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Owner has all permissions, viewer has read-only, unauthorized requests return 403

#### Task: AUTH_WORKSPACE_001
- **title**: Implement multi-workspace tenant isolation
- **description**: Add workspace_id foreign key to all user-facing tables. Implement workspace context in request — extract from JWT or subdomain. Create workspace_members table for user-workspace assignments. Ensure all queries filtered by workspace_id to prevent data leakage.
- **inputs**: JWT claims, request context
- **outputs**: Workspace-scoped data queries
- **dependencies**: [AUTH_DB_SCHEMA_001, AUTH_RBAC_001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Users see only their workspace data, cross-workspace queries return empty, workspace切换 works correctly

#### Task: AUTH_PASSWORD_POLICY_001
- **title**: Implement password policy enforcement
- **description**: Enforce minimum 8 characters, require at least 1 uppercase, 1 lowercase, 1 number, 1 special character. Check new passwords against HaveIBeenPwned database (k-anonymity). Reject passwords matching user email or common weak patterns. Return clear error messages for policy violations.
- **inputs**: New password, user email
- **inputs**: New password, user email
- **outputs**: Validation result with specific error messages
- **dependencies**: [AUTH_PASSWORD_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Weak passwords rejected with specific errors, common breached passwords blocked, valid passwords accepted

#### Task: AUTH_LOCKOUT_001
- **title**: Implement account lockout after failed login attempts
- **description**: Track failed login attempts per user in cache/DB (attempt_count, locked_until). Lock account after 5 failed attempts for 15 minutes. Implement exponential backoff for repeated failures. Send security alert email on lockout. Allow admin to unlock manually.
- **inputs**: Login attempt, user identifier
- **outputs**: Account locked status, security alert
- **dependencies**: [AUTH_DB_SCHEMA_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: 5 failed attempts trigger lockout, locked user cannot login, lockout expires after 15 minutes

#### Task: AUTH_VERIFICATION_001
- **title**: Implement email verification flow
- **description**: Generate email verification token on user creation, send verification email with link. Token expires after 24 hours. On verification, set is_verified=true, clear token. Resend verification email on request (rate limited to 1/hour). Queue verification reminders for unverified accounts after 3 days.
- **inputs**: User email
- **outputs**: Verification email sent, verified status updated
- **dependencies**: [AUTH_DB_SCHEMA_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: fullstack
- **validation**: Verification link works once, expired links rejected, unverified users can login but see prompt

#### Task: AUTH_FORGOT_PASSWORD_001
- **title**: Implement forgot password flow
- **description**: Create password reset request endpoint accepting email. Generate signed reset token (1-hour expiry) stored hashed in DB. Send reset email with signed URL. On reset, validate token, require new password meeting policy, invalidate all refresh tokens. Log reset event.
- **inputs**: User email
- **outputs**: Password reset email sent, all sessions invalidated on reset
- **dependencies**: [AUTH_DB_SCHEMA_001, AUTH_JWT_002, AUTH_PASSWORD_POLICY_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: fullstack
- **validation**: Reset email received, valid token resets password, expired tokens rejected, all sessions terminated

#### Task: AUTH_API_KEY_001
- **title**: Implement API key authentication for integrations
- **description**: Create api_keys table with key_hash, user_id, workspace_id, name, last_used_at, created_at, expires_at. Generate random 32-byte keys, show only once on creation. Validate API key in Authorization: Bearer header or X-API-Key header. Log all API key usage.
- **inputs**: API key from request header
- **outputs**: Authenticated user context for API request
- **dependencies**: [AUTH_DB_SCHEMA_001, AUTH_WORKSPACE_001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Valid API key grants access, invalid key returns 401, key usage logged, last_used_at updated

#### Task: AUTH_AUDIT_001
- **title**: Implement authentication audit logging
- **description**: Create audit_logs table for auth events: login, logout, failed_login, password_change, 2fa_enable, 2fa_disable, password_reset, session_revoked. Log timestamp, user_id, ip_address, user_agent, device_info, event_type, metadata. Implement log retention policy (90 days for auth events).
- **inputs**: Auth event data
- **outputs**: Audit log entry
- **dependencies**: [AUTH_DB_SCHEMA_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: All auth events logged, logs queryable by user/time/event type, sensitive data redacted

---

### Category: API Design (REST/GraphQL)

#### Task: API_REST_001
- **title**: Design RESTful API resource naming conventions
- **description**: Define consistent REST conventions: /api/v1/{resource} for collections, /api/v1/{resource}/{id} for items. Use plural nouns (contacts, jobs, invoices). Use kebab-case for multi-word resources (sales-pipelines). Define standard error response format with code, message, details fields.
- **inputs**: API specification requirements
- **outputs**: API style guide document
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: All endpoints follow conventions, style guide enforced via linting

#### Task: API_REST_002
- **title**: Implement CRUD endpoints for contacts resource
- **description**: Create REST endpoints: GET /api/v1/contacts (list), POST /api/v1/contacts (create), GET /api/v1/contacts/{id} (read), PATCH /api/v1/contacts/{id} (update), DELETE /api/v1/contacts/{id} (delete). Implement pagination with cursor-based approach (limit, cursor). Support field filtering via query params.
- **inputs**: Contact data, query parameters
- **outputs**: JSON response with contact(s), pagination metadata
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: All CRUD operations work, pagination returns correct cursors, filtered fields work

#### Task: API_REST_003
- **title**: Implement CRUD endpoints for jobs resource
- **description**: Create REST endpoints for jobs: GET /api/v1/jobs, POST /api/v1/jobs, GET /api/v1/jobs/{id}, PATCH /api/v1/jobs/{id}, DELETE /api/v1/jobs/{id}. Jobs have status (pending/in_progress/completed/cancelled), scheduled_date, contact_id, description, estimated_duration, actual_duration.
- **inputs**: Job data, query parameters
- **outputs**: JSON response with job(s) and pagination
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Jobs CRUD works, status transitions enforced, jobs linked to contacts

#### Task: API_REST_004
- **title**: Implement CRUD endpoints for invoices resource
- **description**: Create REST endpoints for invoices: GET /api/v1/invoices, POST /api/v1/invoices, GET /api/v1/invoices/{id}, PATCH /api/v1/invoices/{id}, DELETE /api/v1/invoices/{id}. Invoice has invoice_number (auto-generated), client info, line_items, total_ht, total_tva (20%), total_ttc, status (draft/sent/paid/overdue/cancelled).
- **inputs**: Invoice data, query parameters
- **outputs**: JSON response with invoice(s), total calculations
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Invoices CRUD works, French invoice format compliant, TVA calculations correct

#### Task: API_REST_005
- **title**: Implement CRUD endpoints for pipeline resource
- **description**: Create pipeline stages and deals endpoints. GET/POST /api/v1/pipeline/stages, GET/POST /api/v1/pipeline/deals. PATCH /api/v1/pipeline/deals/{id} for moving between stages. Deals have name, contact_id, amount, stage_id, expected_close_date, notes.
- **inputs**: Pipeline stage/deal data
- **outputs**: Pipeline data with stages and deals
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Pipeline stages CRUD works, deals can move between stages, deal amounts calculated

#### Task: API_REST_006
- **title**: Implement query parameter filtering system
- **description**: Build generic filtering system for list endpoints. Support operators: eq, ne, gt, gte, lt, lte, in, contains, starts_with. Parse filter from query: filter[status][eq]=active. Support sort by field: sort=-created_at. Support date range: created_at[gte]=2024-01-01&created_at[lte]=2024-12-31.
- **inputs**: Query parameters (filter, sort, date range)
- **outputs**: Filtered and sorted results
- **dependencies**: [API_REST_002, API_REST_003, API_REST_004]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Complex filters work, multiple operators combine correctly, pagination works with filters

#### Task: API_REST_007
- **title**: Implement search functionality across resources
- **description**: Implement full-text search using PostgreSQL tsvector. Create search endpoint GET /api/v1/search?q={query}&resource={contacts|jobs|invoices}. Search across name, email, phone, description fields. Return relevance-ranked results with highlighted matches. Support fuzzy matching for typos.
- **inputs**: Search query string
- **outputs**: Ranked search results with highlights
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Search returns relevant results, typos handled, results ranked by relevance

#### Task: API_REST_008
- **title**: Implement bulk operations endpoints
- **description**: Create bulk action endpoints: POST /api/v1/{resource}/bulk-delete, POST /api/v1/{resource}/bulk-update, POST /api/v1/{resource}/bulk-attach. Accept array of IDs and action payload. Process in background for large batches (>100 items). Return job ID for tracking long-running bulk operations.
- **inputs**: Array of resource IDs, bulk action data
- **outputs**: Bulk operation result or job ID
- **dependencies**: [API_REST_002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Bulk delete/update works, large bulk operations processed async, results returned when complete

#### Task: API_REST_009
- **title**: Implement file upload endpoints
- **description**: Create multipart form upload endpoint POST /api/v1/uploads. Support image/* (jpg, png, webp) and application/pdf. Max file size: 10MB for images, 25MB for PDFs. Generate unique filename, store in S3-compatible storage (or local on VPS). Return file URL and metadata.
- **inputs**: Multipart file upload
- **outputs**: File metadata, URL, size, MIME type
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Files upload successfully, size limits enforced, valid types accepted, invalid types rejected

#### Task: API_REST_010
- **title**: Implement batch file upload for job photos
- **description**: Create batch upload endpoint POST /api/v1/jobs/{id}/photos. Accept up to 20 images per request. Associate all photos with job record. Generate thumbnails (150x150). Return array of uploaded photo metadata.
- **inputs**: Array of image files, job ID
- **outputs**: Array of photo metadata with URLs
- **dependencies**: [API_REST_003, API_REST_009]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Multiple photos upload in single request, all associated with job, thumbnails generated

#### Task: API_REST_011
- **title**: Implement OpenAPI 3.0 specification
- **description**: Write comprehensive OpenAPI 3.0 spec for all endpoints. Document request/response schemas, authentication requirements, error codes. Generate spec from code annotations or write manually. Validate spec with spectral. Keep spec in sync with implementation.
- **inputs**: All endpoint definitions
- **outputs**: OpenAPI 3.0 JSON/YAML spec file
- **dependencies**: [API_REST_002, API_REST_003, API_REST_004, API_REST_005]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Spec validates against OpenAPI 3.0, all endpoints documented, spec passes spectral rules

#### Task: API_REST_012
- **title**: Implement API request validation middleware
- **description**: Create request validation middleware using Zod or Yup. Validate path params (UUID format), query params (types, required), body (schema). Return 400 with detailed validation errors. Define schemas for each endpoint. Validate content-type header.
- **inputs**: Request path, query, body
- **outputs**: Validated request data or 400 error
- **dependencies**: [API_REST_002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Invalid requests return 400 with field-specific errors, valid requests pass through

#### Task: API_REST_013
- **title**: Implement API response serialization layer
- **description**: Create consistent response serializer. Always return { data, meta, error } envelope. Support includes (embedding related resources): ?include=contact,client. Implement sparse fieldsets: ?fields[contacts]=id,name,email. Transform dates to ISO 8601. Null values omitted by default.
- **inputs**: Response data, query params for shaping
- **outputs**: Serialized JSON response envelope
- **dependencies**: [API_REST_002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Responses consistently shaped, includes work, sparse fieldsets work, dates in ISO format

#### Task: API_REST_014
- **title**: Implement HTTP methodOverride for browser clients
- **description**: Support X-HTTP-Method-Override header for clients that cannot send DELETE/PATCH. Support header override for PUT (update), DELETE, PATCH. Log method overrides for security monitoring. Reject overrides to GET/POST.
- **inputs**: Request with X-HTTP-Method-Override header
- **outputs**: Request processed as overridden method
- **dependencies**: [API_REST_012]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Override header respected, GET/POST overrides rejected, original method logged

#### Task: API_REST_015
- **title**: Implement conditional requests with ETag/If-Match
- **description**: Support ETags on all resources. Return ETag header with GET responses. Accept If-Match header on PATCH/DELETE for optimistic locking. Return 412 if ETag doesn't match. This prevents lost updates in concurrent editing scenarios.
- **inputs**: ETag in request header
- **outputs**: 200 OK with new ETag, or 412 Precondition Failed
- **dependencies**: [API_REST_002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: ETags returned on GET, stale ETags rejected on PATCH/DELETE, race conditions prevented

#### Task: API_REST_016
- **title**: Implement HATEOAS links in responses
- **description**: Add _links object to all responses with related resources. Include self, canonical, collection, related links. For example, contact response includes links to associated jobs and invoices. Allow optional _links via ?include_links=true param.
- **inputs**: Resource data
- **outputs**: Response with _links object
- **dependencies**: [API_REST_013]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Responses include correct HATEOAS links, navigation works via links

#### Task: API_REST_017
- **title**: Implement webhook event subscription endpoints
- **description**: Create CRUD for webhook subscriptions: GET/POST /api/v1/webhooks, DELETE /api/v1/webhooks/{id}. Each subscription has url, events[] (array), secret. Subscribe to events: contact.created, job.updated, invoice.paid, etc. Deliver webhooks with HMAC signature.
- **inputs**: Webhook subscription data
- **outputs**: Created webhook with ID, event deliveries logged
- **dependencies**: [API_REST_002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Webhooks CRUD works, events delivered to URL with signature, retries on failure

#### Task: API_REST_018
- **title**: Implement resource export endpoints
- **description**: Create export endpoints: GET /api/v1/contacts/export?format=csv|xlsx, GET /api/v1/invoices/export?format=pdf. Support filtering on export. Generate file asynchronously for large exports (>1000 records), return job ID. Send email with download link when ready.
- **inputs**: Export parameters, format
- **outputs**: Exported file or export job ID
- **dependencies**: [API_REST_006]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: fullstack
- **validation**: CSV/XLSX exports contain all filtered data, PDF invoices formatted correctly, large exports processed async

#### Task: API_REST_019
- **title**: Implement idempotency keys for POST requests
- **description**: Support Idempotency-Key header on POST endpoints. Store idempotency records with key, endpoint, response, created_at. Return cached response for duplicate keys within 24 hours. Reject keys used on different endpoints. Essential for payment/retry safety.
- **inputs**: Idempotency-Key header
- **outputs**: Original response cached and returned for duplicate keys
- **dependencies**: [API_REST_002, API_REST_004]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Duplicate POST with same key returns same response, different endpoints with same key rejected, keys expire after 24h

#### Task: API_REST_020
- **title**: Document French legal compliance endpoints
- **description**: Create endpoints for French legal requirements: GET /api/v1/invoices/{id}/facture-pdf (French-formatted PDF), GET /api/v1/invoices/{id}/mention-legales (legal mentions), GET /api/v1/data-export (GDPR data export). Ensure invoice numbers follow French sequence rules (year numeric prefix).
- **inputs**: Invoice ID, request parameters
- **outputs**: French-formatted documents, GDPR export
- **dependencies**: [API_REST_004]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: French invoice format compliant, sequential numbering enforced, GDPR export complete

---

### Category: Business Logic (jobs, contacts, invoices, pipeline)

#### Task: BIZ_CONTACT_001
- **title**: Design and create contacts database schema
- **description**: Create contacts table with id, workspace_id, first_name, last_name, email, phone, mobile, company, address, city, postal_code, country (default FR), notes, tags[], created_at, updated_at. Add full-text search index on name, email, company. Add indexes on workspace_id, email, phone.
- **inputs**: Database connection
- **outputs**: contacts table with indexes and constraints
- **dependencies**: [AUTH_WORKSPACE_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Table created, indexes improve search performance, RLS prevents cross-workspace access

#### Task: BIZ_CONTACT_002
- **title**: Implement contact deduplication logic
- **description**: Create duplicate detection on contact creation/update. Check for matches on email (case-insensitive), phone (normalized), company+name combination. Suggest merge candidates when duplicate detected. Allow force-create with override. Log duplicate detection events.
- **inputs**: New contact data
- **outputs**: Duplicate suggestions or created contact
- **dependencies**: [BIZ_CONTACT_001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Duplicates detected on email match, phone normalization catches format variants, suggestions shown

#### Task: BIZ_CONTACT_003
- **title**: Implement contact tagging system
- **description**: Create tags table and contact_tags junction table. Support CRUD on tags within workspace. Add/remove tags from contacts. Query contacts by tag: GET /contacts?tag=prospect,vip. Tag autocomplete on contact forms. Limit tags per workspace to 100.
- **inputs**: Tag data, contact-tag associations
- **outputs**: Tag management, filtered queries by tag
- **dependencies**: [BIZ_CONTACT_001]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Tags CRUD works, contacts filterable by tag, autocomplete works

#### Task: BIZ_CONTACT_004
- **title**: Implement contact activity timeline
- **description**: Create activities table logging all contact-related events: email_sent, call_logged, meeting_scheduled, job_created, invoice_sent, note_added. Each activity has contact_id, type, metadata (JSON), created_at. Provide timeline endpoint: GET /contacts/{id}/timeline. Support pagination and filtering by activity type.
- **inputs**: Activity events from various sources
- **outputs**: Chronological activity timeline per contact
- **dependencies**: [BIZ_CONTACT_001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: All activities logged, timeline chronological, filterable by type

#### Task: BIZ_CONTACT_005
- **title**: Implement contact merge functionality
- **description**: Create mergeContacts(primaryId, secondaryId) function. Merge all data from secondary into primary: combine tags, merge notes, keep earliest created_at, update all FK references. Create merge history record. Delete secondary contact after merge. Require confirmation for merge.
- **inputs**: Primary contact ID, secondary contact ID
- **outputs**: Merged primary contact, secondary archived
- **dependencies**: [BIZ_CONTACT_002, BIZ_CONTACT_003, BIZ_CONTACT_004]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: All data merged correctly, FK references updated, merge history recorded

#### Task: BIZ_JOB_001
- **title**: Design and create jobs database schema
- **description**: Create jobs table with id, workspace_id, contact_id, title, description, status (enum: pending, in_progress, completed, cancelled), scheduled_date, scheduled_time, estimated_duration_minutes, actual_duration_minutes, location_address, notes, created_at, updated_at, completed_at. Add indexes on workspace_id, contact_id, status, scheduled_date.
- **inputs**: Database connection
- **outputs**: jobs table with proper indexes
- **dependencies**: [AUTH_WORKSPACE_001, BIZ_CONTACT_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Jobs table created, foreign key to contacts enforced, status enum enforced

#### Task: BIZ_JOB_002
- **title**: Implement job status workflow engine
- **description**: Create job status transition rules. Valid transitions: pending→in_progress, in_progress→completed, in_progress→cancelled, pending→cancelled, pending→in_progress. Log all transitions with from_status, to_status, user_id, timestamp. Prevent invalid transitions. Allow admin override.
- **inputs**: Job ID, target status
- **outputs**: Updated job or transition error
- **dependencies**: [BIZ_JOB_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Valid transitions succeed, invalid transitions rejected with error, all transitions logged

#### Task: BIZ_JOB_003
- **title**: Implement job scheduling and availability logic
- **description**: Create job scheduling system. Check for double-booking conflicts (same day, overlapping time for same artisan). Suggest next available slot when conflict detected. Support recurring jobs (weekly, biweekly, monthly). Calculate next occurrence based on recurrence rule.
- **inputs**: Job date/time, duration, recurrence rule
- **outputs**: Scheduling confirmation or conflict suggestion
- **dependencies**: [BIZ_JOB_001, BIZ_JOB_002]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: No double bookings, conflicts detected and reported, recurring jobs generate correct occurrences

#### Task: BIZ_JOB_004
- **title**: Implement job costing and profitability tracking
- **description**: Create job costs tracking: materials_cost, labor_cost, travel_cost, other_costs. Calculate profit margin: (invoice_amount - total_cost) / invoice_amount * 100. Generate profitability report per job, per period. Track budgeted vs actual costs.
- **inputs**: Cost data per job
- **outputs**: Profitability metrics per job and period
- **dependencies**: [BIZ_JOB_001, BIZ_INVOICE_001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Costs tracked accurately, margins calculated correctly, reports show profitability trends

#### Task: BIZ_JOB_005
- **title**: Implement job templates system
- **description**: Create job_templates table. Templates have name, description, default_duration, checklist_items[], required_photos[]. Allow user to create job from template. Pre-fill job fields from template. Support template CRUD. Include common artisan templates (installation, repair, maintenance).
- **inputs**: Template data, job creation from template
- **outputs**: Job pre-filled from template
- **dependencies**: [BIZ_JOB_001]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: fullstack
- **validation**: Templates save correctly, job creation from template pre-fills fields, checklists work

#### Task: BIZ_JOB_006
- **title**: Implement job checklist system
- **description**: Create job_checklist_items table linked to jobs. Each item has text, is_completed, completed_at, completed_by_user_id. Support adding/removing items from checklist. Auto-populate from job template if used. Mark job complete only when all required checklist items done.
- **inputs**: Checklist items for job
- **outputs**: Checklist tracking per job
- **dependencies**: [BIZ_JOB_001, BIZ_JOB_005]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Checklist items add/remove/complete, required items block job completion

#### Task: BIZ_INVOICE_001
- **title**: Design and create invoices database schema
- **description**: Create invoices table with id, workspace_id, invoice_number (varchar, unique per workspace), contact_id, issue_date, due_date, status (enum: draft, sent, paid, overdue, cancelled), subtotal_ht, tva_rate (default 20), total_tva, total_ttc, notes, payment_terms, bank_details, created_at, updated_at, paid_at. Create invoice_line_items table with id, invoice_id, description, quantity, unit_price_ht, tva_rate, total_ht, total_ttc.
- **inputs**: Database connection
- **outputs**: invoices and invoice_line_items tables
- **dependencies**: [AUTH_WORKSPACE_001, BIZ_CONTACT_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Invoice schema correct, French TVA calculation accurate, sequential numbering enforced

#### Task: BIZ_INVOICE_002
- **title**: Implement French invoice number generation
- **description**: Generate invoice numbers following French legal format: {YEAR}{SEQUENCE}