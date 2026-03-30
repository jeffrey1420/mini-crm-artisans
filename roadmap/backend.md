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
- **description**: Generate invoice numbers following French legal format: {YEAR}{SEQUENCE}{SEQUENCE}. Example: 2024-0001, 2024-0002. Reset sequence each year. Validate uniqueness per workspace. Allow prefix customization per workspace (default: company name abbreviation). Store invoice sequence per workspace per year.
- **inputs**: Workspace ID, year
- **outputs**: Next invoice number in sequence
- **dependencies**: [BIZ_INVOICE_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Invoice numbers sequential, unique per workspace/year, correct format

#### Task: BIZ_INVOICE_003
- **title**: Implement French TVA (VAT) calculation engine
- **description**: Calculate TVA at 20% standard rate (support 10%, 5.5%, 2.1% for French exemptions). Calculate per line item and total. Support mixed TVA rates on same invoice. Validate TVA rate eligibility based on contact country and invoice type. Store TVA breakdown: total_ht, tva_20, tva_10, tva_5_5, total_ttc.
- **inputs**: Line items with TVA rates, contact country
- **outputs**: TVA breakdown per rate and totals
- **dependencies**: [BIZ_INVOICE_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: TVA calculations correct, different rates handled, French format compliant

#### Task: BIZ_INVOICE_004
- **title**: Implement invoice PDF generation with French legal format
- **description**: Generate PDF invoices following French legal requirements. Include: company details, client details, invoice number, dates, line items with TVA, totals, payment terms, bank details (RIB, IBAN, BIC), mention "TVA non applicable - art. 293 B du CGI" if applicable. Use PDFKit or puppeteer. Generate in A4 format.
- **inputs**: Invoice data
- **outputs**: PDF binary data
- **dependencies**: [BIZ_INVOICE_001, BIZ_INVOICE_002, BIZ_INVOICE_003]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: PDF generated, French format correct, all required fields present

#### Task: BIZ_INVOICE_005
- **title**: Implement invoice reminder and overdue logic
- **description**: Create background job checking invoices daily. Send reminder email 3 days before due date. Send overdue email 1 day after due date. Escalate overdue email after 7 days and 14 days. Update invoice status to overdue. Calculate days overdue.
- **inputs**: Invoice due dates
- **outputs**: Reminder emails sent, status updated
- **dependencies**: [BIZ_INVOICE_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Reminders sent at correct times, overdue status updated, escalation works

#### Task: BIZ_INVOICE_006
- **title**: Implement invoice payment recording
- **description**: Create markAsPaid(invoiceId, paymentDate, paymentMethod, paymentReference) function. Update invoice status to paid, set paid_at. Support partial payments with payment schedule. Record payment history. Trigger related job status update if configured.
- **inputs**: Invoice ID, payment details
- **outputs**: Invoice marked as paid, payment recorded
- **dependencies**: [BIZ_INVOICE_001, BIZ_JOB_002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Payment recorded accurately, partial payments tracked, status updated correctly

#### Task: BIZ_INVOICE_007
- **title**: Implement credit note functionality
- **description**: Create credit notes for invoice cancellations or adjustments. Generate credit note number following format: AV{year}{sequence}. Link credit note to original invoice. Update original invoice status. Calculate credit note totals with TVA. Generate credit note PDF.
- **inputs**: Original invoice ID, credit note reason
- **outputs**: Credit note created, linked to invoice
- **dependencies**: [BIZ_INVOICE_001, BIZ_INVOICE_004]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Credit note created, linked to original, PDF generated, sequence maintained

#### Task: BIZ_INVOICE_008
- **title**: Implement recurring invoice templates
- **description**: Create invoice templates that auto-generate invoices on schedule. Support weekly, monthly, quarterly, yearly recurrence. Define template with line items, contact, payment terms. Track next occurrence date. Auto-generate invoice when due. Send notification before generation.
- **inputs**: Template data, recurrence schedule
- **outputs**: Recurring invoices generated on schedule
- **dependencies**: [BIZ_INVOICE_001]
- **priority**: low
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Recurring invoices generate on schedule, templates work, notifications sent

#### Task: BIZ_PIPELINE_001
- **title**: Design and create pipeline database schema
- **description**: Create pipeline_stages table with id, workspace_id, name, position (integer), color, created_at. Create deals table with id, workspace_id, stage_id, contact_id, name, amount, currency (EUR), expected_close_date, notes, created_at, updated_at, won_at, lost_at. Add indexes on stage_id, contact_id, amount.
- **inputs**: Database connection
- **outputs**: pipeline_stages and deals tables
- **dependencies**: [AUTH_WORKSPACE_001, BIZ_CONTACT_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Tables created, foreign keys enforced, position ordering works

#### Task: BIZ_PIPELINE_002
- **title**: Implement Kanban board data endpoints
- **description**: Create GET /api/v1/pipeline/board returning stages with deals grouped. Each stage includes deal count, total amount. Deals include contact name, next action date. Support deal filtering by stage. Order deals by position within stage. Return pipeline metrics: total value, weighted value, conversion rate.
- **inputs**: Workspace ID
- **outputs**: Kanban board data with stages and deals
- **dependencies**: [BIZ_PIPELINE_001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Board returns correct structure, deals grouped by stage, metrics calculated

#### Task: BIZ_PIPELINE_003
- **title**: Implement deal stage transition with probability
- **description**: Create moveDeal(dealId, targetStageId, probability) function. Log transition with timestamp, from/to stage, user. Default probability per stage (lead 10%, qualified 30%, proposal 60%, negotiation 80%, won 100%). Allow probability override. Calculate weighted pipeline value.
- **inputs**: Deal ID, target stage ID
- **outputs**: Deal moved, probability updated, transition logged
- **dependencies**: [BIZ_PIPELINE_001, BIZ_PIPELINE_002]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Deal moves between stages, probability updates, weighted value calculated

#### Task: BIZ_PIPELINE_004
- **title**: Implement pipeline analytics and forecasting
- **description**: Calculate pipeline metrics: total pipeline value, average deal size, average cycle time (stage to won), conversion rate per stage, win rate. Generate forecast based on historical data and current pipeline. Identify stalled deals (no activity >14 days). Report on deals at risk.
- **inputs**: Pipeline data, historical win data
- **outputs**: Analytics dashboard data, at-risk deals
- **dependencies**: [BIZ_PIPELINE_001, BIZ_PIPELINE_003]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Metrics accurate, forecasts reasonable, stalled deals identified

#### Task: BIZ_PIPELINE_005
- **title**: Implement pipeline duplicate detection
- **description**: Detect potential duplicate deals for same contact. On deal creation/update, check for existing open deals from same contact. Flag as potential duplicate. Allow user to merge or keep separate. Prevent automatic merging without confirmation.
- **inputs**: Deal data, contact ID
- **outputs**: Duplicate suggestions or deal created
- **dependencies**: [BIZ_PIPELINE_001]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Duplicates detected, suggestions shown, merge works correctly

#### Task: BIZ_WORKFLOW_001
- **title**: Implement automated workflow rules engine
- **description**: Create workflow_rules table with workspace_id, name, trigger_event, conditions[], actions[]. Support triggers: contact_created, job_status_changed, invoice_overdue, deal_stage_changed. Conditions: field equals, greater than, contains, is empty. Actions: send_email, add_tag, update_field, create_task, send_webhook.
- **inputs**: Workflow rule definitions
- **outputs**: Automated actions triggered on events
- **dependencies**: [BIZ_CONTACT_001, BIZ_JOB_002, BIZ_INVOICE_005]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Rules fire on correct triggers, conditions evaluated, actions executed

#### Task: BIZ_WORKFLOW_002
- **title**: Implement subscription tier feature gating
- **description**: Create subscription_features table mapping features to tiers. Features: max_contacts (50/500/unlimited), max_jobs_per_month, max_invoices, max_users, api_access, custom_fields, advanced_analytics, priority_support. Check feature access before allowing actions. Return upgrade prompt when limit reached.
- **inputs**: User subscription tier, requested feature
- **outputs**: Feature enabled/disabled, upgrade prompt if needed
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Features gated correctly per tier, limits enforced, upgrade prompts shown

---

### Category: File Handling (vCard import, photo uploads)

#### Task: FILE_VCARD_001
- **title**: Implement vCard 3.0/4.0 parser
- **description**: Create vCard parser supporting vCard 3.0 and 4.0 formats. Parse standard fields: FN, N, EMAIL, TEL, ORG, ADR, NOTE. Handle multi-value fields, property parameters (TYPE=WORK, HOME). Support PHOTO (embedded base64 or URL reference). Return structured contact object.
- **inputs**: vCard string data
- **outputs**: Parsed contact object
- **dependencies**: [BIZ_CONTACT_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: vCard 3.0 and 4.0 parsed correctly, all standard fields extracted, multi-value fields handled

#### Task: FILE_VCARD_002
- **title**: Implement batch vCard import
- **description**: Create POST /api/v1/contacts/import/vcard endpoint accepting multipart file upload. Support .vcf files containing multiple cards. Parse all contacts, validate each, report parsing errors without failing entire import. Return import summary: total, imported, skipped, errors. Process in background for files >50 contacts.
- **inputs**: vCard file upload
- **outputs**: Import result with summary
- **dependencies**: [FILE_VCARD_001, BIZ_CONTACT_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Multi-card files import all contacts, errors reported per card, large files processed async

#### Task: FILE_VCARD_003
- **title**: Implement vCard export functionality
- **description**: Create GET /api/v1/contacts/{id}/vcard endpoint. Generate vCard 3.0 format with all contact fields. Support export all contacts as single .vcf file (multiple cards). Include PHOTO if contact has avatar. Set correct content-type and content-disposition headers.
- **inputs**: Contact ID(s)
- **outputs**: vCard file download
- **dependencies**: [BIZ_CONTACT_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: vCard downloads correctly, opens in contacts app, all fields present

#### Task: FILE_PHOTO_001
- **title**: Implement photo upload storage service
- **description**: Create file storage abstraction supporting local filesystem and S3-compatible storage. Store files with workspace_id/year/month/uuid.filename path. Generate unique filenames preserving extension. Return file metadata: id, url, size, mime_type, dimensions (for images), created_at.
- **inputs**: File binary data, metadata
- **outputs**: Stored file metadata with URL
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Files stored correctly, retrievable via URL, metadata accurate

#### Task: FILE_PHOTO_002
- **title**: Implement image thumbnail generation
- **description**: Create thumbnail generation on upload. Generate sizes: 150x150 (avatar), 400x300 (listing), 800x600 (detail). Use sharp or similar library. Store thumbnails alongside original. Return thumbnail URLs in response. Support JPEG, PNG, WebP.
- **inputs**: Image file
- **outputs**: Original and thumbnail URLs
- **dependencies**: [FILE_PHOTO_001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Thumbnails generated at all sizes, correct dimensions, format preserved

#### Task: FILE_PHOTO_003
- **title**: Implement EXIF metadata extraction for job photos
- **description**: Extract EXIF data from uploaded job photos. Extract: GPS coordinates, timestamp, camera model. Store coordinates as separate lat/lng fields for mapping. Display location on job map view if coordinates present. Handle photos without EXIF gracefully.
- **inputs**: Image file
- **outputs**: EXIF metadata object with coordinates
- **dependencies**: [FILE_PHOTO_001]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: EXIF extracted when present, GPS coordinates stored, photos without EXIF handled

#### Task: FILE_DOCUMENT_001
- **title**: Implement document upload for invoices
- **description**: Create document upload for invoice attachments. Support PDF, images, common office formats (doc, docx, xls, xlsx). Max file size: 25MB. Store in same path structure as photos. Link to invoice via invoice_attachments table. Allow multiple attachments per invoice.
- **inputs**: Document file, invoice ID
- **outputs**: Attachment metadata linked to invoice
- **dependencies**: [BIZ_INVOICE_001, FILE_PHOTO_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Documents upload, linked to invoice, downloadable, size limits enforced

#### Task: FILE_STORAGE_001
- **title**: Implement file deletion and cleanup
- **description**: Create soft delete for files (is_deleted flag, deleted_at). Hard delete after 30 days. Clean up orphaned files not linked to any resource. Implement permanent delete endpoint for admin. Update storage usage metrics.
- **inputs**: File ID or cleanup job
- **outputs**: Files deleted, storage freed
- **dependencies**: [FILE_PHOTO_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Soft delete works, hard delete after 30 days, orphans cleaned, storage calculated

#### Task: FILE_CDN_001
- **title**: Implement CDN integration for file delivery
- **description**: Configure CDN (Cloudflare, OVH CDN) for static assets. Set cache headers: images 1 year, PDFs 1 week. Implement cache invalidation on file delete. Use signed URLs for private files. Configure origin shield for storage.
- **inputs**: File URL, cache rules
- **outputs**: CDN-configured delivery
- **dependencies**: [FILE_PHOTO_001]
- **priority**: low
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: Files served from CDN, cache headers correct, invalidation works

---

### Category: Notifications & Reminders

#### Task: NOTIF_EMAIL_001
- **title**: Implement transactional email service
- **description**: Create email service abstraction supporting SendGrid, Mailgun, OVH Email. Create email templates for: welcome, password_reset, magic_link, invoice_sent, invoice_paid, job_reminder, subscription_upcoming_expiry. Support template variables. Track delivery status via webhooks.
- **inputs**: Email type, recipient, template variables
- **outputs**: Email sent, delivery status tracked
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Emails sent successfully, templates render correctly, delivery tracked

#### Task: NOTIF_EMAIL_002
- **title**: Implement email template localization (FR/EN)
- **description**: Create i18n email templates for French and English. Detect user language preference. Send emails in user's language. Support date/time formatting per locale. Include proper French salutations and formalities.
- **inputs**: User locale, email content
- **outputs**: Localized email
- **dependencies**: [NOTIF_EMAIL_001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: fullstack
- **validation**: French users receive FR emails, English users receive EN, dates formatted correctly

#### Task: NOTIF_SMS_001
- **title**: Implement SMS notification service
- **description**: Create SMS service integration with OVH SMS or SendGrid. Support SMS for: job reminders (24h before), urgent alerts, invoice payment confirmations. Character limit handling (160 GSM). Queue messages for delivery. Track delivery status.
- **inputs**: Phone number, message content
- **outputs**: SMS sent, delivery status
- **dependencies**: [NOTIF_EMAIL_001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: SMS sent, delivery confirmed, character limits handled, French numbers validated

#### Task: NOTIF_PUSH_001
- **title**: Implement Web Push notifications
- **description**: Create Web Push notification service using web-push library. Implement VAPID key pair generation and storage. Store push subscriptions in DB. Send push notifications for: new job assigned, invoice received, payment reminder. Support notification payload with title, body, icon, action buttons.
- **inputs**: Push subscription, notification payload
- **outputs**: Push notification delivered
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: fullstack
- **validation**: Push notifications delivered, subscription management works, click tracking works

#### Task: NOTIF_REMINDER_001
- **title**: Implement job reminder scheduling system
- **description**: Create reminder scheduling for jobs. Allow reminders at: 1 week before, 1 day before, 2 hours before. Store reminder schedule in reminders table. Create background job processing reminders. Send email + SMS + push based on user preferences. Handle missed reminders (job deleted, rescheduled).
- **inputs**: Job ID, reminder times, user preferences
- **outputs**: Reminders scheduled and sent
- **dependencies**: [BIZ_JOB_001, NOTIF_EMAIL_001, NOTIF_SMS_001, NOTIF_PUSH_001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Reminders sent at correct times, preferences respected, missed reminders handled

#### Task: NOTIF_REMINDER_002
- **title**: Implement invoice payment reminder automation
- **description**: Create invoice reminder schedule. Remind 7 days before due, on due date, 3 days overdue, 7 days overdue, 14 days overdue. Each reminder more urgent in tone. Track reminder history per invoice. Allow user to customize reminder schedule.
- **inputs**: Invoice data, user preferences
- **outputs**: Reminder emails sent on schedule
- **dependencies**: [BIZ_INVOICE_005, NOTIF_EMAIL_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Reminders sent on schedule, escalation works, history tracked

#### Task: NOTIF_NOTIFICATION_001
- **title**: Implement in-app notification system
- **description**: Create in-app notifications stored in DB. Create notifications table with user_id, type, title, body, data (JSON), read_at, created_at. Create markAsRead, markAllAsRead endpoints. Real-time delivery via WebSocket when user online. Notification center in frontend.
- **inputs**: User ID, notification data
- **outputs**: In-app notification created
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: fullstack
- **validation**: Notifications stored, real-time delivery works, mark as read works

#### Task: NOTIF_SCHEDULER_001
- **title**: Implement background job scheduler for notifications
- **description**: Create notification queue using Bull or similar. Implement scheduler worker processing queued jobs. Support delayed jobs for scheduled notifications. Implement retry with exponential backoff. Monitor queue health and failed jobs.
- **inputs**: Queued notification jobs
- **outputs**: Notifications processed and delivered
- **dependencies**: [NOTIF_REMINDER_001, NOTIF_REMINDER_002]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Jobs processed on schedule, retries work, failures logged and retried

#### Task: NOTIF_DIGEST_001
- **title**: Implement daily/weekly notification digest
- **description**: Create notification digest feature. Aggregate daily: new contacts, completed jobs, pending invoices. Aggregate weekly: pipeline changes, reminders, activity summary. Send digest email at user-configured time. Allow digest frequency settings: none, daily, weekly.
- **inputs**: User ID, digest preferences
- **outputs**: Digest email sent
- **dependencies**: [NOTIF_EMAIL_001]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Digests aggregate correctly, sent at configured time, preferences respected

---

### Category: Payment Integration (Stripe + CB)

#### Task: PAY_STRIPE_001
- **title**: Implement Stripe customer creation and management
- **description**: Create Stripe customer on user registration or first payment. Store Stripe customer ID in users table. Update customer email/name on sync. Support customer portal link generation. Handle Stripe customer webhook updates.
- **inputs**: User data
- **outputs**: Stripe customer ID, stored in DB
- **dependencies**: [AUTH_DB_SCHEMA_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Customer created in Stripe, linked to user, portal link works

#### Task: PAY_STRIPE_002
- **title**: Implement Stripe subscription management
- **description**: Create subscription management for three tiers: Essential (€29), Pro (€49), Premium (€79). Create Stripe products and prices. Implement subscribe, change_plan, cancel_subscription, reactivate endpoints. Handle subscription lifecycle events. Store subscription status locally.
- **inputs**: User ID, plan selection
- **outputs**: Active subscription, status synced
- **dependencies**: [PAY_STRIPE_001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Subscriptions created in Stripe, plan changes work, cancellations processed

#### Task: PAY_STRIPE_003
- **title**: Implement Stripe Checkout session for payments
- **description**: Create Stripe Checkout integration for subscription payments and invoice payments. Generate checkout session with price ID or custom amount. Support embedded checkout or redirect mode. Handle success and cancel URLs. Store session ID for verification.
- **inputs**: Price ID or amount, success URL, cancel URL
- **outputs**: Checkout session URL
- **dependencies**: [PAY_STRIPE_002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Checkout works, payments processed, success/failure handled

#### Task: PAY_STRIPE_004
- **title**: Implement French CB (Carte Bancaire) payment processing
- **description**: Configure Stripe for French CB payments. Enable Cartes Bancaires as payment method. Handle 3DSecure authentication for CB. Support French cards with CB logo. Test with Stripe test cards simulating French cards.
- **inputs**: Payment intent data
- **outputs**: Payment processed via CB
- **dependencies**: [PAY_STRIPE_003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: CB payments work, 3DS handled, French test cards work

#### Task: PAY_STRIPE_005
- **title**: Implement Stripe webhook handling
- **description**: Create webhook endpoint POST /api/v1/webhooks/stripe. Verify webhook signatures. Handle events: customer.subscription.created, customer.subscription.updated, customer.subscription.deleted, invoice.paid, invoice.payment_failed, checkout.session.completed. Update local subscription/payment state.
- **inputs**: Stripe webhook event
- **outputs**: Local state updated, events logged
- **dependencies**: [PAY_STRIPE_002, PAY_STRIPE_003]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Webhooks verified, all events handled, local state consistent with Stripe

#### Task: PAY_STRIPE_006
- **title**: Implement payment failure handling and retry logic
- **description**: Create retry schedule for failed payments: retry after 1 day, 3 days, 7 days. Send email notification on each retry. After 3 failures, downgrade to free tier. Allow manual retry from user dashboard. Track payment failure history.
- **inputs**: Failed payment event
- **outputs**: Retries scheduled, user notified
- **dependencies**: [PAY_STRIPE_005, NOTIF_EMAIL_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Retries happen on schedule, emails sent, downgrade after 3 failures

#### Task: PAY_STRIPE_007
- **title**: Implement invoice payment via Stripe
- **description**: Create createPaymentIntent(invoiceId) function. Generate Stripe payment intent for invoice amount. Create checkout session or embed payment form. On success, mark invoice as paid. Handle partial payments. Sync payment status with Stripe.
- **inputs**: Invoice ID
- **outputs**: Payment intent, checkout session
- **dependencies**: [BIZ_INVOICE_006, PAY_STRIPE_003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Invoice payments work, partial payments handled, invoice marked paid on success

#### Task: PAY_STRIPE_008
- **title**: Implement Stripe Customer Portal integration
- **description**: Integrate Stripe Customer Portal for self-service billing management. Generate portal session with return URL. Allow users to update payment method, view invoices, cancel subscription, download invoices. Enforce workspace ownership verification.
- **inputs**: User ID, return URL
- **outputs**: Portal session URL
- **dependencies**: [PAY_STRIPE_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Portal accessible, payment method update works, invoices viewable

#### Task: PAY_BILLING_001
- **title**: Implement usage-based billing tracking
- **description**: Track usage metrics for tier limits: contact count, jobs this month, storage used, API calls. Store usage snapshots daily. Alert user at 80% and 100% of tier limits. Block creation when hard limit reached with upgrade prompt.
- **inputs**: Usage metrics per workspace
- **outputs**: Usage report, limit enforcement
- **dependencies**: [BIZ_WORKFLOW_002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Usage tracked accurately, alerts at thresholds, hard limits block creation

#### Task: PAY_BILLING_002
- **title**: Implement subscription upgrade/downgrade logic
- **description**: Create subscription change handlers. Upgrade: prorate remaining days, apply immediately. Downgrade: apply at end of billing period. Track feature access changes. Handle downgrade when features in use (warn user). Generate proration invoice/credit.
- **inputs**: User ID, target plan
- **outputs**: Plan changed, proration calculated
- **dependencies**: [PAY_STRIPE_002, PAY_STRIPE_007]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Upgrades immediate, downgrades delayed, proration correct, features update

#### Task: PAY_REFUND_001
- **title**: Implement refund processing
- **description**: Create refund endpoints for admins. Support full and partial refunds. Create refund reason tracking. Process refunds via Stripe API. Update invoice status for partial refunds. Generate refund confirmation email. Require manager approval for refunds >€50.
- **inputs**: Payment intent ID, amount, reason
- **outputs**: Refund processed, confirmation sent
- **dependencies**: [PAY_STRIPE_007, NOTIF_EMAIL_001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Refunds process correctly, partial refunds update invoice, approvals work

#### Task: PAY_TAX_001
- **title**: Implement French tax compliance for subscriptions
- **description**: Handle French VAT on digital services. Determine tax rate based on customer country (FR: 20%). Generate tax records for Stripe. Configure Stripe Tax for automatic VAT handling. Handle B2B VAT exemption validation (with valid VAT number).
- **inputs**: Customer country, VAT number, subscription amount
- **outputs**: Tax calculated and applied
- **dependencies**: [PAY_STRIPE_002]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: VAT correct for FR customers, VAT exemption validated, tax records accurate

---

### Category: Webhook System

#### Task: WH_EVENT_001
- **title**: Define webhook event catalog
- **description**: Define complete webhook event catalog: contact.created, contact.updated, contact.deleted, job.created, job.updated, job.status_changed, job.completed, invoice.created, invoice.sent, invoice.paid, invoice.overdue, invoice.cancelled, subscription.created, subscription.updated, subscription.cancelled, payment.succeeded, payment.failed. Include event schema for each.
- **inputs**: None
- **outputs**: Event catalog documentation
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: All events documented, schemas defined, events categorized

#### Task: WH_SUB_001
- **title**: Implement webhook subscription management
- **description**: Create webhook_subscriptions table with id, workspace_id, url, events[], secret, is_active, created_at. CRUD endpoints for subscription management. Validate URL format (HTTPS required for production). Rate limit per workspace: max 10 subscriptions.
- **inputs**: Subscription data
- **outputs**: Subscription created, active
- **dependencies**: [WH_EVENT_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Subscriptions created, URL validated, HTTPS enforced, rate limited

#### Task: WH_SUB_002
- **title**: Implement webhook delivery with retry logic
- **description**: Create webhook delivery queue. On event, queue delivery to all matching subscriptions. HTTP POST with JSON body: { event, timestamp, workspace_id, data }. Sign payload with HMAC-SHA256 using subscription secret. Retry failed deliveries: 3 attempts with 1min, 5min, 30min delays. Store delivery attempts and response.
- **inputs**: Event data, subscription URL
- **outputs**: Webhook delivered with signature
- **dependencies**: [WH_SUB_001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Webhooks delivered with correct payload, signatures verified, retries work

#### Task: WH_SUB_003
- **title**: Implement webhook delivery logs and monitoring
- **description**: Create webhook_deliveries table logging all delivery attempts. Store: subscription_id, event, payload, response_status, response_body, attempt_number, delivered_at, created_at. Create admin endpoint to view delivery logs per workspace. Implement health check for webhook URLs.
- **inputs**: Delivery logs
- **outputs**: Logged deliveries, admin view
- **dependencies**: [WH_SUB_002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: All deliveries logged, logs queryable, health checks work

#### Task: WH_SUB_004
- **title**: Implement webhook signature verification for inbound webhooks
- **description**: If receiving webhooks from external services, implement signature verification. Support common patterns: GitHub, Stripe, Zapier. Verify HMAC signature or JWT. Reject invalid signatures with 401. Log verification failures.
- **inputs**: Inbound webhook request
- **outputs**: Verified request or rejection
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Valid signatures accepted, invalid rejected, failures logged

#### Task: WH_FILTER_001
- **title**: Implement webhook event filtering
- **description**: Allow subscription filters based on event data. Support filter expressions: contact.tags contains 'vip', invoice.amount > 1000. Only deliver webhooks matching filters. Store filter expressions in subscription record. Parse and evaluate filter expressions.
- **inputs**: Event data, filter expressions
- **outputs**: Filtered webhook deliveries
- **dependencies**: [WH_SUB_001]
- **priority**: low
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Filters work correctly, only matching events delivered

#### Task: WH_BATCH_001
- **title**: Implement webhook batch delivery
- **description**: For high-frequency events, implement batch delivery. Accumulate events for 5 minutes or 100 events. Deliver as single POST with events array. Include batch metadata: batch_id, event_count, first_event, last_event. Sign batch payload same as individual.
- **inputs**: Accumulated events
- **outputs**: Batch webhook delivered
- **dependencies**: [WH_SUB_002]
- **priority**: low
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Events batched correctly, batch delivered, receiver can process array

---

### Category: Caching & Performance

#### Task: CACHE_REDIS_001
- **title**: Implement Redis caching layer
- **description**: Set up Redis for caching. Cache frequently accessed data: user sessions, subscription data, contact counts, dashboard metrics. Define TTLs per cache type. Implement cache-aside pattern: check cache, on miss fetch from DB, store in cache. Handle cache failures gracefully.
- **inputs**: Cache key, data
- **outputs**: Cached data retrieved/stored
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Redis connected, cache operations work, TTLs respected, misses handled

#### Task: CACHE_REDIS_002
- **title**: Implement query result caching
- **description**: Create cache keys for list endpoints: contacts:list:{workspace_id}:{hash(params)}. Cache dashboard metrics with 5-minute TTL. Cache contact detail with 10-minute TTL. Invalidate cache on relevant CRUD operations. Use cache tags for bulk invalidation.
- **inputs**: Query parameters
- **outputs**: Cached query results
- **dependencies**: [CACHE_REDIS_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Query results cached, cache hit improves response time, invalidation works

#### Task: CACHE_REDIS_003
- **title**: Implement session storage in Redis
- **description**: Store user sessions in Redis. Session data: user_id, workspace_id, permissions, last_activity. Session TTL: 24 hours sliding. Implement session validation middleware. Handle Redis connection failures with fallback to DB.
- **inputs**: Session ID
- **outputs**: Session data
- **dependencies**: [CACHE_REDIS_001, AUTH_SESSION_001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Sessions stored in Redis, session validation fast, fallback works

#### Task: CACHE_CDN_001
- **title**: Configure CDN caching for static assets
- **description**: Configure Cloudflare or OVH CDN for static files. Set cache rules: /uploads/images/* cache 1 year, /assets/* cache 1 week. Implement cachepurge on file delete. Use asset pipeline fingerprints for cache busting.
- **inputs**: Static asset paths
- **outputs**: CDN configured caching
- **dependencies**: [FILE_PHOTO_001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Assets cached by CDN, cache purged on delete, fingerprints work

#### Task: CACHE_QUERY_001
- **title**: Implement database query optimization
- **description**: Analyze slow queries using pg_stat_statements. Add missing indexes based on query patterns. Optimize N+1 query problems using JOINs or batch loading. Implement query result pagination. Optimize count queries with estimated counts for large tables.
- **inputs**: Slow query logs
- **outputs**: Optimized queries
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Slow queries identified, indexes added, N+1 problems resolved

#### Task: CACHE_QUERY_002
- **title**: Implement database connection pooling
- **description**: Set up PgBouncer or pg_pool for connection pooling. Configure pool size based on VPS resources (10-50 connections). Implement transaction-mode pooling. Monitor connection pool utilization. Handle pool exhaustion gracefully.
- **inputs**: Database connection settings
- **outputs**: Connection pool configured
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Pool configured, connections reused, exhaustion handled

#### Task: CACHE_APP_001
- **title**: Implement application-level caching for dashboard data
- **description**: Cache dashboard aggregations: total contacts, jobs this week, pending invoices, pipeline value. Use Redis with 5-minute TTL. Invalidate on relevant data changes. Return cached data immediately when available.
- **inputs**: Dashboard data requests
- **outputs**: Cached dashboard metrics
- **dependencies**: [CACHE_REDIS_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Dashboard loads fast from cache, invalidation works

#### Task: CACHE_LIST_001
- **title**: Implement list endpoint cursor-based pagination
- **description**: Implement cursor-based pagination for all list endpoints. Use keyset pagination (WHERE id < cursor). Return cursor in response: { data, next_cursor, has_more }. Default page size: 20, max: 100. Ensure consistent ordering with indexes.
- **inputs**: Pagination parameters
- **outputs**: Paginated results with cursor
- **dependencies**: [API_REST_002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Pagination works consistently, performance maintained at scale

#### Task: CACHE_RESPONSE_001
- **title**: Implement HTTP response compression
- **description**: Enable gzip and Brotli compression for API responses. Configure compression level based on content type (json: high, images: none). Add Vary: Accept-Encoding header. Monitor compression ratio. Target 70%+ compression for JSON.
- **inputs**: API responses
- **outputs**: Compressed responses
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Responses compressed, ratio monitored, correct headers set

#### Task: CACHE_PRELOAD_001
- **title**: Implement cache warming for frequent queries
- **description**: Implement cache warming for hot data after deployment or cache restart. Preload: popular contact lists, user dashboards, common filter combinations. Schedule warming as background job. Warm incrementally to avoid load spike.
- **inputs**: Cache warming job
- **outputs**: Preloaded cache
- **dependencies**: [CACHE_REDIS_001]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Cache warmed on schedule, hot data available immediately

---

### Category: Logging & Observability

#### Task: LOG_STRUCTURE_001
- **title**: Implement structured JSON logging
- **description**: Replace plain text logs with structured JSON logs. Include fields: timestamp, level (debug/info/warn/error), service, request_id, user_id, workspace_id, message, metadata. Use pino or winston with JSON transport. Ensure all logs machine-readable.
- **inputs**: Log events
- **outputs**: JSON log entries
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Logs are JSON, all required fields present, parseable

#### Task: LOG_REQUEST_001
- **title**: Implement request logging middleware
- **description**: Create middleware logging all HTTP requests. Log: method, path, status_code, response_time_ms, request_id, user_id, workspace_id, user_agent, ip_address. Log request body for POST/PATCH/PUT (sanitize sensitive fields). Use request_id for correlation.
- **inputs**: HTTP request/response
- **outputs**: Request log entries
- **dependencies**: [LOG_STRUCTURE_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: All requests logged, correlation works, sensitive data sanitized

#### Task: LOG_SLOW_001
- **title**: Implement slow query and slow request detection
- **description**: Log warning for requests >500ms, error for >2000ms. Log database queries >100ms. Include stack trace for slow requests. Create metric for p95/p99 response times. Alert on anomalies.
- **inputs**: Request timing data
- **outputs**: Slow request logs and alerts
- **dependencies**: [LOG_REQUEST_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Slow requests identified, alerts triggered, patterns detected

#### Task: LOG_AUDIT_001
- **title**: Implement audit logging for sensitive operations
- **description**: Create audit log entries for: login/logout, password changes, data exports, deletions, permission changes, billing operations. Include: user_id, workspace_id, action, resource_type, resource_id, old_value, new_value, ip_address, timestamp.
- **inputs**: Sensitive operations
- **outputs**: Audit log entries
- **dependencies**: [LOG_STRUCTURE_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: All sensitive ops logged, audit trail complete, logs immutable

#### Task: LOG_ERROR_001
- **title**: Implement global error handler and error logging
- **description**: Create global error handler catching all unhandled exceptions. Log error with: message, stack trace, request context, user context. Sanitize sensitive data (passwords, tokens). Implement error boundary for async errors. Return safe error messages to client.
- **inputs**: Error events
- **outputs**: Error logs and user-safe responses
- **dependencies**: [LOG_STRUCTURE_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: All errors caught and logged, no sensitive data leaked, safe messages returned

#### Task: OBS_METRICS_001
- **title**: Implement Prometheus metrics endpoint
- **description**: Expose /metrics endpoint with Prometheus format. Track: request_count, request_duration_seconds, request_size_bytes, response_size_bytes, active_connections, db_pool_connections, cache_hit_ratio, error_rate. Add custom business metrics: active_subscriptions, invoices_paid_today, contacts_added_today.
- **inputs**: Metrics data
- **outputs**: Prometheus metrics endpoint
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Metrics endpoint returns valid Prometheus format, all metrics exposed

#### Task: OBS_METRICS_002
- **title**: Implement business metrics tracking
- **description**: Track business KPIs: new_subscriptions_per_day, churn_rate, mrr (monthly recurring revenue), contacts_added, jobs_completed, invoices_generated, payment_success_rate. Store daily aggregates. Create metric for conversion funnel: trial → paid.
- **inputs**: Business events
- **outputs**: Business metrics data
- **dependencies**: [OBS_METRICS_001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: KPIs tracked accurately, daily aggregates stored, funnel metrics work

#### Task: OBS_ALERT_001
- **title**: Implement alerting for critical conditions
- **description**: Configure alerts for: error_rate > 5%, p95 latency > 2000ms, payment failures > 10%, subscription cancellations spike, disk usage > 80%, memory usage > 85%. Use PagerDuty or similar for critical alerts. Log warning for near-threshold conditions.
- **inputs**: Metric thresholds
- **outputs**: Alerts triggered
- **dependencies**: [OBS_METRICS_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Alerts fire on threshold breach, critical issues page, warnings logged

#### Task: OBS_DASHBOARD_001
- **title**: Implement Grafana dashboards
- **description**: Create Grafana dashboard for system health: request rate, error rate, latency percentiles, DB connections, cache hit ratio, memory/CPU. Create business dashboard: MRR, subscriptions, invoices, contacts. Include workspace-level drill-down. Set up dashboard provisioning.
- **inputs**: Metrics data sources
- **outputs**: Grafana dashboards
- **dependencies**: [OBS_METRICS_001, OBS_METRICS_002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Dashboards display correctly, data refreshes, alerts visible

#### Task: OBS_TRACING_001
- **title**: Implement distributed tracing
- **description**: Add OpenTelemetry tracing for request tracing. Generate trace_id propagated through all services. Trace DB queries, external API calls, cache operations. Export traces to Jaeger or similar. Include span attributes: user_id, workspace_id, operation.
- **inputs**: Request context
- **outputs**: Distributed traces
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Traces correlated across services, spans detailed, latency contributions visible

#### Task: OBS_HEALTH_001
- **title**: Implement health check endpoints
- **description**: Create /health endpoint returning service status. Include: database connectivity, Redis connectivity, disk space, memory. Create /health/ready for readiness probes and /health/live for liveness probes. Return 503 if unhealthy.
- **inputs**: Health check requests
- **outputs**: Health status JSON
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Health endpoint responds, unhealthy conditions detected, probes work correctly

#### Task: OBS_SLO_001
- **title**: Implement SLO monitoring
- **description**: Define SLIs: availability (target 99.5%), latency (p95 < 500ms), error rate (< 1%). Create SLO dashboard showing current vs target. Alert when SLO at risk. Track SLO budget burn rate. Document SLO definitions.
- **inputs**: Service level data
- **outputs**: SLO dashboard and alerts
- **dependencies**: [OBS_METRICS_001, OBS_ALERT_001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: SLIs tracked, SLO dashboard accurate, alerts on SLO breach risk

---

### Category: Error Handling

#### Task: ERR_GLOBAL_001
- **title**: Implement global error handler middleware
- **description**: Create global error handling middleware catching all errors. Categorize errors: ValidationError, NotFoundError, AuthenticationError, AuthorizationError, BusinessError, InternalError. Format consistent error response: { error: { code, message, details } }. Log with full context.
- **inputs**: Error object
- **outputs**: Safe error response
- **dependencies**: [LOG_ERROR_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: All errors caught, proper HTTP status codes, safe messages to clients

#### Task: ERR_CUSTOM_001
- **title**: Create custom error classes
- **description**: Define custom error classes extending base error: AppError, ValidationError (400), NotFoundError (404), ConflictError (409), UnauthorizedError (401), ForbiddenError (403), RateLimitError (429), InternalError (500). Each with code, message, statusCode, details properties.
- **inputs**: None
- **outputs**: Error class hierarchy
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Errors properly classified, correct status codes, consistent behavior

#### Task: ERR_VALIDATION_001
- **title**: Implement request validation errors
- **description**: Create validation error handling with field-level details. Return 400 with array of field errors: { field, message, value }. Include constraint violated. Aggregate multiple validation errors. Return in consistent format.
- **inputs**: Validation results
- **outputs**: Field-level validation errors
- **dependencies**: [ERR_CUSTOM_001, API_REST_012]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Field errors detailed, multiple errors aggregated, constraint info included

#### Task: ERR_NOT_FOUND_001
- **title**: Implement NotFound error handling
- **description**: Handle 404 for all resource types. Return consistent format: { error: { code: 'NOT_FOUND', message: 'Resource not found', resource_type, resource_id } }. Handle missing relations gracefully. Include suggestion for typos in IDs.
- **inputs**: Request for missing resource
- **outputs**: 404 response
- **dependencies**: [ERR_CUSTOM_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: 404 returned for missing resources, proper format, suggestions included

#### Task: ERR_ASYNC_001
- **title**: Implement async error wrapper
- **description**: Create asyncHandler wrapper for route handlers. Catch promise rejections and pass to error middleware. Prevent unhandled promise rejection crashes. Use at least once wrapper on all async route handlers.
- **inputs**: Async route handlers
- **outputs**: Errors caught and passed to middleware
- **dependencies**: [ERR_GLOBAL_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Async errors handled, no unhandled rejections, crashes prevented

#### Task: ERR_DATABASE_001
- **title**: Implement database error handling
- **description**: Handle PostgreSQL errors: connection failures, constraint violations, deadlock, timeout. Map to appropriate HTTP errors: unique violation → 409, foreign key violation → 400, serialization failure → retry. Log database errors with query context.
- **inputs**: Database errors
- **outputs**: Appropriate HTTP response
- **dependencies**: [ERR_CUSTOM_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: DB errors handled gracefully, proper HTTP codes, deadlocks retried

#### Task: ERR_RETRY_001
- **title**: Implement retry logic for transient failures
- **description**: Implement retry with exponential backoff for transient operations. Retry on: network errors, 503 Service Unavailable, 429 Rate Limited. Max 3 retries with 100ms, 1s, 5s delays. Use jitter to prevent thundering herd. Log retry attempts.
- **inputs**: Failed operations
- **outputs**: Retried operations with backoff
- **dependencies**: [ERR_GLOBAL_001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Transients retried, backoff works, max retries enforced, jitter present

#### Task: ERR_CIRCUIT_001
- **title**: Implement circuit breaker pattern
- **description**: Implement circuit breaker for external services (Stripe, email provider). States: closed (normal), open (failing), half-open (testing). Open after 5 failures in 10 seconds. Half-open after 30 seconds. Reset after success. Return cached response when open.
- **inputs**: External service calls
- **outputs**: Circuit breaker controlled calls
- **dependencies**: [ERR_RETRY_001]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Circuit opens on failures, closes after recovery, cached responses returned

#### Task: ERR_USER_001
- **title**: Implement user-friendly error messages
- **description**: Create mapping from technical errors to user-friendly messages. For example: '23505' (unique violation) → 'A record with this value already exists'. Keep messages in FR and EN. Never expose internal details, stack traces, or table names to users.
- **inputs**: Technical errors
- **outputs**: User-safe messages
- **dependencies**: [ERR_DATABASE_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Messages user-friendly, no internal details leaked, localized

#### Task: ERR_RECOVERY_001
- **title**: Implement panic recovery and graceful shutdown
- **description**: Set up panic recovery for unhandled exceptions. Graceful shutdown on SIGTERM/SIGINT: finish in-flight requests, close DB connections, flush logs. Set memory limit and restart on heap exhaustion. Implement health check draining.
- **inputs**: Shutdown signals
- **outputs**: Graceful shutdown
- **dependencies**: [LOG_STRUCTURE_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Graceful shutdown completes, requests finished, connections closed cleanly

---

### Category: Rate Limiting & Security

#### Task: SEC_RATE_001
- **title**: Implement API rate limiting
- **description**: Implement rate limiting per user/IP: 100 requests/minute for authenticated, 20 requests/minute for unauthenticated. Use sliding window algorithm with Redis. Return X-RateLimit-Limit, X-RateLimit-Remaining, X-RateLimit-Reset headers. Return 429 with Retry-After when exceeded.
- **inputs**: Request
- **outputs**: Rate limit headers and 429 responses
- **dependencies**: [CACHE_REDIS_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Limits enforced, headers correct, 429 returned when exceeded

#### Task: SEC_RATE_002
- **title**: Implement endpoint-specific rate limits
- **description**: Apply stricter limits on sensitive endpoints: /auth/login: 5/min, /auth/password-reset: 3/min, /payments: 10/min, /uploads: 20/min. Implement per-user and per-IP limits independently. Log excessive attempts.
- **inputs**: Endpoint requests
- **outputs**: Endpoint-specific limits
- **dependencies**: [SEC_RATE_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Sensitive endpoints more restricted, combined limits work

#### Task: SEC_CORS_001
- **title**: Implement CORS configuration
- **description**: Configure CORS for PWA access. Allow frontend origin from environment config. Allow credentials. Set max-age 1 hour. Handle preflight requests. Whitelist only necessary methods and headers.
- **inputs**: CORS configuration
- **outputs**: CORS headers on responses
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Preflight handled, correct origins allowed, credentials work

#### Task: SEC_CSP_001
- **title**: Implement Content Security Policy
- **description**: Set CSP headers to prevent XSS. Configure default-src 'self'. Allow scripts from self, styles from self and inline, images from self and CDN, fonts from self and Google. Report violations to /csp-violations endpoint. Use nonce for inline scripts.
- **inputs**: CSP configuration
- **outputs**: CSP headers on responses
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: CSP headers set, XSS prevented, violations reported

#### Task: SEC_HTTPS_001
- **title**: Enforce HTTPS and HSTS
- **description**: Redirect HTTP to HTTPS. Set HSTS header: max-age=31536000; includeSubDomains; preload. Set Strict-Transport-Security for all responses. Include upgrade-insecure-requests directive. Configure at nginx level.
- **inputs**: HTTP requests
- **outputs**: HTTPS enforced
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: HTTP redirects to HTTPS, HSTS header set, preload configured

#### Task: SEC_HEADERS_001
- **title**: Implement security headers
- **description**: Set security headers: X-Content-Type-Options: nosniff, X-Frame-Options: DENY, X-XSS-Protection: 1; mode=block, Referrer-Policy: strict-origin-when-cross-origin, Permissions-Policy: geolocation=(), microphone=(), camera=(). Review and update quarterly.
- **inputs**: Response headers
- **outputs**: Security headers on all responses
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: All security headers present, clickjacking prevented, MIME sniffing prevented

#### Task: SEC_SQL_001
- **title**: Prevent SQL injection attacks
- **description**: Use parameterized queries exclusively (no string concatenation for user input). Validate all input types. Escape special characters in dynamic query parts. Use ORM/query builder for all DB access. Regular code review for injection vulnerabilities.
- **inputs**: User input in queries
- **outputs**: Safe queries
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Parameterized queries used, no injection possible, ORM used throughout

#### Task: SEC_XSS_001
- **title**: Prevent XSS attacks
- **description**: Sanitize user-generated content before storage and display. Use DOMPurify for HTML content. Escape output in templates. Implement CSP to mitigate. Validate input lengths. Implement CSRF tokens for state-changing operations.
- **inputs**: User-generated content
- **outputs**: Sanitized content
- **dependencies**: [SEC_CSP_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: fullstack
- **validation**: XSS payloads sanitized, CSP prevents stored XSS, output escaped

#### Task: SEC_CSRF_001
- **title**: Implement CSRF protection
- **description**: Generate CSRF tokens for authenticated sessions. Validate tokens on state-changing requests (POST, PUT, PATCH, DELETE). Use SameSite=Strict/Lax cookies. Accept tokens in X-CSRF-Token header or body. Reject requests without valid token.
- **inputs**: CSRF token
- **outputs**: Token validation
- **dependencies**: [AUTH_JWT_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: CSRF tokens generated, validation works, invalid tokens rejected

#### Task: SEC_INPUT_001
- **title**: Implement input sanitization and validation
- **description**: Sanitize all user input: trim whitespace, remove control characters, validate types. Use Zod/Yup for schema validation. Validate string lengths. Validate email format, phone format, URL format. Reject input with null bytes or encoded characters.
- **inputs**: User input
- **outputs**: Sanitized, validated input
- **dependencies**: [API_REST_012]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Malformed input rejected, sanitization works, types enforced

#### Task: SEC_SENSITIVE_001
- **title**: Implement sensitive data protection
- **description**: Encrypt sensitive fields at rest: passwords, API keys, bank details. Use AES-256-GCM encryption. Key management with environment variables or secrets manager. Never log sensitive data. Mask fields in responses.
- **inputs**: Sensitive data
- **outputs**: Encrypted storage, masked responses
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Sensitive data encrypted, not logged, masked in responses

#### Task: SEC_INJECT_002
- **title**: Implement NoSQL injection prevention
- **description**: If using MongoDB or similar, prevent NoSQL injection. Validate query structure. Escape special characters in user input. Use type-safe query builders. Never interpolate user input into query operators.
- **inputs**: User input in queries
- **outputs**: Safe queries
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: NoSQL injection attempts fail, queries type-safe

#### Task: SEC_DEP_001
- **title**: Implement dependency vulnerability scanning
- **description**: Set up npm audit and Snyk/Dependabot for dependency scanning. Run on every build. Fail build on high/critical vulnerabilities. Update dependencies monthly. Maintain allowed-list for problematic packages.
- **inputs**: package.json, lock files
- **outputs**: Vulnerability report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Vulnerabilities detected, build fails on critical, updates regular

#### Task: SEC_SECRET_001
- **title**: Implement secrets management
- **description**: Store secrets (API keys, database passwords) in environment variables or secrets manager. Never commit secrets to git. Use .env.example for local development. Rotate secrets quarterly. Implement secret scanning in pre-commit hooks.
- **inputs**: Secret values
- **outputs**: Secrets managed securely
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: No secrets in git, secrets rotated, .env.example exists

#### Task: SEC_IP_001
- **title**: Implement IP allowlisting for workspace
- **description**: Allow admins to whitelist IP addresses for workspace access. Check IP against whitelist on each request. Support CIDR notation. Provide option to block all non-whitelisted IPs. Default: allow all.
- **inputs**: IP address
- **outputs**: IP validation result
- **dependencies**: [AUTH_WORKSPACE_001]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Whitelist enforced, CIDR works, blocked IPs rejected

#### Task: SEC_AUDIT_001
- **title**: Implement security audit logging
- **description**: Log security-relevant events: login attempts, auth failures, permission denials, data exports, admin actions. Include: timestamp, user_id, ip, action, result, context. Store logs securely with immutability. Retain for 1 year.
- **inputs**: Security events
- **outputs**: Security audit log
- **dependencies**: [LOG_AUDIT_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: All security events logged, logs tamper-evident, queryable

#### Task: SEC_PEN_001
- **title**: Implement penetration testing
- **description**: Perform annual penetration testing with third-party service. Test OWASP Top 10 vulnerabilities. Fix critical findings within 48 hours, high within 7 days. Document remediation. Retest after fixes.
- **inputs**: None
- **outputs**: Penetration test report
- **dependencies**: [SEC_SQL_001, SEC_XSS_001, SEC_CSRF_001]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: security
- **validation**: Pen test completed, criticals fixed, report documented

---

### Category: API Versioning

#### Task: VER_SCHEME_001
- **title**: Define API versioning strategy
- **description**: Use URL path versioning: /api/v1/{resource}. Announce deprecation 6 months before sunset. Maintain old versions for 12 months after new version. Document version lifecycle. Communicate breaking changes clearly.
- **inputs**: None
- **outputs**: Versioning policy
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Policy documented, versioning consistent

#### Task: VER_MIGRATE_001
- **title**: Implement v1 to v2 migration path
- **description**: Document breaking changes between v1 and v2. Provide migration guide with code examples. Implement v1 endpoints in v2 as deprecated. Create v2-only features. Offer migration assistance to API consumers.
- **inputs**: Version change documentation
- **outputs**: Migration guide
- **dependencies**: [VER_SCHEME_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Migration guide complete, breaking changes documented

#### Task: VER_DEPRECATE_001
- **title**: Implement deprecation headers
- **description**: Add Sunset header to deprecated endpoints: Sunset: Tue, 01 Oct 2025 00:00:00 GMT. Add Deprecation header: true. Add Link header with successor. Log deprecation warnings for clients using old versions.
- **inputs**: Deprecated endpoint responses
- **outputs**: Deprecation headers
- **dependencies**: [VER_SCHEME_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Sunset header present, Deprecation header present, Link to successor

#### Task: VER_GUARD_001
- **title**: Implement version routing middleware
- **description**: Create routing middleware parsing API version from URL path. Route to appropriate handler based on version. Default to latest stable version. Return 400 for unsupported versions with message pointing to latest.
- **inputs**: Request path
- **outputs**: Routed to versioned handler
- **dependencies**: [VER_SCHEME_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Version parsed correctly, routed to correct handler, unsupported version rejected

#### Task: VER_CONTRACT_001
- **title**: Implement API contract testing
- **description**: Use Pact or similar for contract testing. Define contracts for provider (this API) and consumers (frontend, mobile). Run contract tests in CI. Ensure v1 and v2 contracts maintained separately. Fail builds on contract violations.
- **inputs**: API contracts
- **outputs**: Contract tests passing
- **dependencies**: [VER_SCHEME_001]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Contracts defined, tests run in CI, violations fail build

#### Task: VER_DOC_001
- **title**: Maintain API changelog
- **description**: Maintain CHANGELOG.md documenting all API changes per version. Include: date, change type (added/changed/deprecated/removed), description, migration steps. Group by version. Publish changelog at /changelog endpoint.
- **inputs**: API changes
- **outputs**: Changelog document
- **dependencies**: [VER_SCHEME_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Changelog current, all changes documented, accessible

#### Task: VER_CONSISTENT_001
- **title**: Implement consistent response format across versions
- **description**: Ensure v1 and v2 use same response envelope structure: { data, meta, error }. Keep field naming consistent: snake_case vs camelCase documented per version. Maintain backward compatibility within major version.
- **inputs**: API responses
- **outputs**: Consistent format
- **dependencies**: [API_REST_013]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Format consistent across versions, naming documented

---

### Category: DevOps & Infrastructure

#### Task: DEVOPS_DOCKER_001
- **title**: Create Docker container configuration
- **description**: Create Dockerfile for Node.js backend. Use multi-stage build: builder stage with dependencies, runtime stage minimal. Set non-root user. Configure health check. Build and push to container registry. Support ARM64 and AMD64.
- **inputs**: Dockerfile
- **outputs**: Container image
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Image builds, runs, healthcheck works, ARM64 supported

#### Task: DEVOPS_DOCKER_002
- **title**: Implement docker-compose for local development
- **description**: Create docker-compose.yml with: backend service, PostgreSQL, Redis, nginx. Configure volume mounts for code hot-reload. Set up network between services. Add mailhog for email testing. Document startup commands.
- **inputs**: docker-compose.yml
- **outputs**: Local development environment
- **dependencies**: [DEVOPS_DOCKER_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: All services start, hot reload works, services communicate

#### Task: DEVOPS_K8S_001
- **title**: Create Kubernetes deployment manifests
- **description**: Create K8s manifests: Deployment, Service, Ingress, ConfigMap, Secret. Configure resource limits and requests. Set up horizontal pod autoscaling. Configure liveness and readiness probes. Use rolling update strategy.
- **inputs**: K8s manifests
- **outputs**: Deployment to K8s
- **dependencies**: [DEVOPS_DOCKER_001]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: Manifests apply, pods run, scaling works, healthchecks pass

#### Task: DEVOPS_CI_001
- **title**: Set up CI/CD pipeline
- **description**: Configure GitHub Actions or similar for CI/CD. Pipeline stages: lint, test, build, security scan, deploy to staging, deploy to production. Use environment promotions. Require passing tests. Implement rollback capability.
- **inputs**: GitHub Actions workflow
- **outputs**: CI/CD pipeline
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Pipeline runs on PR/push, all stages pass, deploys work

#### Task: DEVOPS_DB_001
- **title**: Set up PostgreSQL on OVH VPS
- **description**: Install and configure PostgreSQL 15+ on OVH VPS. Configure: max_connections, shared_buffers, effective_cache_size, work_mem. Set up automated backups daily to OVH Object Storage. Test backup restoration quarterly. Enable point-in-time recovery.
- **inputs**: OVH VPS access
- **outputs**: PostgreSQL configured
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: PostgreSQL running, backups working, PITR configured

#### Task: DEVOPS_DB_002
- **title**: Implement database migrations strategy
- **description**: Use database migrations (Drizzle/Knex/Prisma). Version migration files. Run migrations on deployment. Never modify existing migrations. Create rollback strategy for each migration. Test migrations on staging first.
- **inputs**: Migration files
- **outputs**: Migrations applied
- **dependencies**: [DEVOPS_CI_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Migrations run on deploy, rollback works, staging tested first

#### Task: DEVOPS_MONITOR_001
- **title**: Set up infrastructure monitoring
- **description**: Deploy Prometheus, Grafana, node_exporter on VPS. Monitor: CPU, memory, disk, network, container stats. Set up dashboards. Configure alerting for resource exhaustion. Monitor nginx and PostgreSQL.
- **inputs**: Monitoring tools
- **outputs**: Monitoring configured
- **dependencies**: [OBS_METRICS_001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Metrics collected, dashboards visible, alerts fire

#### Task: DEVOPS_LOG_001
- **title**: Set up centralized logging
- **description**: Deploy Loki or Elasticsearch for log aggregation. Configure Promtail/Filebeat to ship logs. Create Grafana dashboards for logs. Set up log retention (30 days for app, 90 for auth). Implement log search.
- **inputs**: Log aggregation tools
- **outputs**: Centralized logs
- **dependencies**: [LOG_STRUCTURE_001]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: Logs aggregated, searchable, retention working

#### Task: DEVOPS_BACKUP_001
- **title**: Implement backup and disaster recovery
- **description**: Define RTO (< 1 hour) and RPO (< 24 hours). Implement daily automated backups: database, uploaded files, application state. Store backups in OVH Object Storage with encryption. Test restore quarterly.Test backup restoration quarterly. Document recovery procedures.
- **inputs**: Backup configuration
- **outputs**: Backup system working
- **dependencies**: [DEVOPS_DB_001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: Backups run daily, stored encrypted, restore tested

#### Task: DEVOPS_nginx_001
- **title**: Configure nginx as reverse proxy
- **description**: Configure nginx as reverse proxy and load balancer. Set up SSL termination. Configure upstream for backend. Set up rate limiting at nginx level. Enable Gzip compression. Configure logging. Set up Let's Encrypt certificates.
- **inputs**: nginx config
- **outputs**: nginx configured
- **dependencies**: [SEC_HTTPS_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: nginx running, SSL working, proxy to backend works

#### Task: DEVOPS_ENV_001
- **title**: Implement environment configuration management
- **description**: Create environment-specific configs: development, staging, production. Use .env files loaded at startup. Validate required environment variables. Document all config options. Never commit secrets to git.
- **inputs**: Environment variables
- **outputs**: Config loaded
- **dependencies**: [SEC_SECRET_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Config loads per environment, secrets not in git, validation works

#### Task: DEVOPS_DOMAIN_001
- **title**: Configure DNS and domain management
- **description**: Configure DNS for api.domain.com pointing to VPS. Set up A record and CNAME. Configure DNS TTL appropriately. Set up DKIM, SPF, DMARC for email deliverability. Use OVH DNS for zone management.
- **inputs**: Domain name
- **outputs**: DNS configured
- **dependencies**: [NOTIF_EMAIL_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: DNS resolves correctly, email authentication works

#### Task: DEVOPS_OVH_001
- **title**: Optimize OVH VPS for Mini-CRM workload
- **description**: Configure VPS based on workload: 4GB+ RAM, 2+ vCPU, 50GB+ SSD. Set up SWAP if needed. Configure kernel parameters for network performance. Set up OVH firewall rules. Monitor VPS performance.
- **inputs**: OVH VPS
- **outputs**: Optimized VPS
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: VPS optimized, performance adequate, firewall configured

#### Task: DEVOPS_SCALE_001
- **title**: Implement horizontal scaling strategy
- **description**: Design scaling strategy for growth: 100 users, 1000 users, 10000 users. Document scaling triggers. Configure auto-scaling rules. Set up load balancer health checks. Plan database scaling (read replicas).
- **inputs**: Scaling requirements
- **outputs**: Scaling strategy
- **dependencies**: [DEVOPS_K8S_001, DEVOPS_nginx_001]
- **priority**: low
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: Strategy documented, scaling triggers defined

#### Task: DEVOPS_SECRET_001
- **title**: Implement secrets rotation
- **description**: Implement automatic secrets rotation for: database password, JWT keys, API keys. Rotate every 90 days. Use secrets manager (HashiCorp Vault or AWS Secrets Manager). Update secrets without downtime. Log rotation events.
- **inputs**: Secrets configuration
- **outputs**: Automated rotation
- **dependencies**: [SEC_SECRET_001]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: Rotation works, no downtime, keys updated

---

### Category: Testing

#### Task: TEST_UNIT_001
- **title**: Implement unit test suite for business logic
- **description**: Create unit tests for all business logic functions. Use Jest or Vitest. Mock external dependencies (DB, Redis). Aim for 80%+ code coverage. Test edge cases and error conditions. Run in CI on every PR.
- **inputs**: Business logic code
- **outputs**: Unit tests passing
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Tests pass, coverage > 80%, CI runs tests

#### Task: TEST_INTEGRATION_001
- **title**: Implement integration tests for API endpoints
- **description**: Create integration tests for all API endpoints. Use supertest or similar. Test with real database (test instance). Test authentication flows. Test error cases. Test pagination and filtering. Run in CI.
- **inputs**: API endpoints
- **outputs**: Integration tests passing
- **dependencies**: [TEST_UNIT_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Tests pass, real DB tested, CI runs tests

#### Task: TEST_E2E_001
- **title**: Implement end-to-end tests for critical flows
- **description**: Create E2E tests for critical user flows: registration, login, create contact, create job, generate invoice, payment flow. Use Playwright. Run against staging environment. Include in CI pipeline.
- **inputs**: Critical user flows
- **outputs**: E2E tests passing
- **dependencies**: [TEST_INTEGRATION_001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: fullstack
- **validation**: E2E tests pass, critical flows covered

#### Task: TEST_PERF_001
- **title**: Implement performance testing
- **description**: Create performance tests with k6 or Artillery. Test: list endpoints with 1000 contacts, search with complex filters, invoice generation. Set performance benchmarks: p95 < 500ms. Run load tests simulating growth. Identify bottlenecks.
- **inputs**: Performance test scripts
- **outputs**: Performance benchmarks
- **dependencies**: [TEST_INTEGRATION_001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Benchmarks set, load tests run, bottlenecks identified

#### Task: TEST_SEC_001
- **title**: Implement security testing
- **description**: Integrate security tests in CI: OWASP ZAP for vulnerability scanning, SQL injection tests, XSS tests. Test authentication bypass attempts. Test authorization enforcement. Fail build on critical findings.
- **inputs**: Security test tools
- **outputs**: Security tests passing
- **dependencies**: [TEST_INTEGRATION_001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: security
- **validation**: Security tests run, criticals fail build

#### Task: TEST_CONTRACT_001
- **title**: Implement contract testing for API
- **description**: Use Pact for consumer-driven contract testing. Define contracts between API provider and frontend consumer. Publish contracts to Pact Broker. Verify contracts on both sides. Include in CI pipeline.
- **inputs**: API contracts
- **outputs**: Contract tests passing
- **dependencies**: [VER_CONTRACT_001]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: fullstack
- **validation**: Contracts defined, tests pass, CI integrated

#### Task: TEST_REGRESSION_001
- **title**: Implement regression test suite
- **description**: Create regression suite for known bugs. Ensure fixes don't regress. Run regression suite before releases. Track regression test coverage. Add regression tests for new bugs.
- **inputs**: Known bugs
- **outputs**: Regression suite
- **dependencies**: [TEST_UNIT_001, TEST_INTEGRATION_001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Regression suite exists, bugs don't regress

#### Task: TEST_FUZZ_001
- **title**: Implement fuzz testing
- **description**: Use fuzzing tools to test API endpoints with random inputs. Test for crashes, memory leaks, unexpected behavior. Focus on input validation. Run continuously in CI. Track discovered issues.
- **inputs**: Fuzzing tools
- **outputs**: Fuzz test results
- **dependencies**: [TEST_INTEGRATION_001]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: security
- **validation**: Fuzzing runs, crashes identified

---

### Category: Documentation

#### Task: DOC_API_001
- **title**: Write comprehensive API documentation
- **description**: Document all API endpoints with: description, authentication, request parameters, request body schema, response schema, error codes, examples. Use OpenAPI spec as source of truth. Publish via Swagger UI or Redoc. Update on every release.
- **inputs**: OpenAPI spec
- **outputs**: API documentation
- **dependencies**: [API_REST_011]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: All endpoints documented, examples work, up to date

#### Task: DOC_SETUP_001
- **title**: Write developer setup documentation
- **description**: Document local development setup: prerequisites, clone repo, install dependencies, configure environment, start services, run migrations, run development server. Include troubleshooting common issues.
- **inputs**: Development environment
- **outputs**: Setup documentation
- **outputs**: Setup documentation
- **dependencies**: [DEVOPS_DOCKER_002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: New developers can setup in < 30 minutes

#### Task: DOC_ARCH_001
- **title**: Document system architecture
- **description**: Create architecture diagram showing: frontend, backend, database, Redis, nginx, services. Document data flow. Document deployment topology. Document external integrations. Keep architecture doc in sync with implementation.
- **inputs**: Architecture decisions
- **outputs**: Architecture documentation
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Architecture clear, diagrams accurate, updated on changes

#### Task: DOC_SEC_001
- **title**: Write security documentation
- **description**: Document security practices: authentication flow, authorization model, data encryption, secrets management, vulnerability reporting. Document GDPR compliance measures. Include security checklist for deployments.
- **inputs**: Security implementation
- **outputs**: Security documentation
- **dependencies**: [SEC_SQL_001, SEC_XSS_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: security
- **validation**: Security practices documented, GDPR compliance clear

#### Task: DOC_RUNBOOK_001
- **title**: Write operational runbooks
- **description**: Create runbooks for: deployment, rollback, database backup restore, scaling, incident response. Each runbook: purpose, prerequisites, steps, verification, rollback. Store in docs/runbooks. Review quarterly.
- **inputs**: Operations tasks
- **outputs**: Runbooks
- **dependencies**: [DEVOPS_CI_001, DEVOPS_BACKUP_001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Runbooks complete, tested, accessible

#### Task: DOC_CHANGELOG_001
- **title**: Maintain changelog
- **description**: Maintain CHANGELOG.md with semantic versioning. Document all changes: Added, Changed, Deprecated, Removed, Fixed, Security. Group by version. Include migration notes for breaking changes. Follow Keep a Changelog format.
- **inputs**: Code changes
- **outputs**: Changelog
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Changelog accurate, follows format, all changes documented
