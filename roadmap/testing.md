# Testing Roadmap — Mini-CRM

## Objectives

- Ensure complete test coverage for all Mini-CRM features used by French artisans
- Validate French localization (accents, dates, currency formatting)
- Verify mobile-first PWA functionality across devices and offline scenarios
- Secure payment flows with Stripe test mode validation
- Achieve 90%+ code coverage on unit tests
- Validate accessibility compliance (WCAG 2.1 AA)
- Establish robust CI/CD pipeline with automated testing gates
- Prepare for beta testing program with real French artisan users

## Subdomains

- **Authentication & Authorization**: Login, registration, role-based access
- **Client Management**: CRUD operations for artisan clients
- **Quote Management**: Create, send, accept/reject quotes
- **Invoice Management**: Generate, send, track payment status
- **Appointment Scheduling**: Calendar, reminders, availability
- **Notification System**: Email, SMS, push notifications
- **Offline Mode**: Data persistence, sync mechanisms
- **Payment Processing**: Stripe integration, webhooks, refunds
- **French Localization**: i18n, formatting, cultural adaptation

## Milestones

### Milestone 1: Foundation (Week 1-2)
- Unit testing framework setup (Vitest + Jest)
- Test fixtures and factories created
- CI/CD pipeline skeleton
- First batch of unit tests for core utilities

### Milestone 2: Feature Testing (Week 3-4)
- Integration tests for all API routes
- E2E tests for critical user flows
- French locale validation tests
- Security vulnerability scanning

### Milestone 3: Platform Validation (Week 5-6)
- PWA functionality testing
- Offline mode comprehensive testing
- Cross-device and cross-browser testing
- Payment flow testing with Stripe test cards

### Milestone 4: Performance & Accessibility (Week 7-8)
- Load testing and performance profiling
- Accessibility audit with axe-core
- Beta testing program launch
- Final test suite optimization

## Task Categories

---

### Category: Unit Testing (Vitest for Frontend, Jest for Backend)

#### Task: UNIT-FRONT-001
- **title**: Configure Vitest with Vue Test Utils
- **description**: Set up Vitest testing framework with Vue Test Utils for Nuxt 3 components. Configure tsconfig paths, aliases, and global mocks for $router, $store, and $i18n.
- **inputs**: package.json, nuxt.config.ts, vite.config.ts
- **outputs**: vitest.config.ts, setup files, working test environment
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Run `npx vitest --run` and confirm all tests execute without configuration errors

#### Task: UNIT-FRONT-002
- **title**: Write unit tests for useAuth composable
- **description**: Test all authentication-related logic including login, logout, token refresh, session persistence, and protected route guards.
- **inputs**: composables/useAuth.ts, auth store
- **outputs**: tests/composables/useAuth.spec.ts
- **dependencies**: [UNIT-FRONT-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: All 12+ test cases pass covering login, logout, token expiry, and redirect scenarios

#### Task: UNIT-FRONT-003
- **title**: Write unit tests for useClients composable
- **description**: Test client management composable covering CRUD operations, search, filtering, pagination, and error handling.
- **inputs**: composables/useClients.ts, client types
- **outputs**: tests/composables/useClients.spec.ts
- **dependencies**: [UNIT-FRONT-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Tests cover add, edit, delete, search, filter, and pagination with mock API responses

#### Task: UNIT-FRONT-004
- **title**: Write unit tests for useQuotes composable
- **description**: Test quote creation, editing, status updates, PDF generation trigger, and email sending logic.
- **inputs**: composables/useQuotes.ts, quote types
- **outputs**: tests/composables/useQuotes.spec.ts
- **dependencies**: [UNIT-FRONT-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: 15+ test cases covering full quote lifecycle

#### Task: UNIT-FRONT-005
- **title**: Write unit tests for useInvoices composable
- **description**: Test invoice generation, payment status tracking, due date calculations, and reminder triggers.
- **inputs**: composables/useInvoices.ts, invoice types
- **outputs**: tests/composables/useInvoices.spec.ts
- **dependencies**: [UNIT-FRONT-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: All invoice lifecycle scenarios covered including overdue handling

#### Task: UNIT-FRONT-006
- **title**: Write unit tests for useCalendar composable
- **description**: Test appointment scheduling, time slot availability, conflict detection, and reminder scheduling.
- **inputs**: composables/useCalendar.ts, appointment types
- **outputs**: tests/composables/useCalendar.spec.ts
- **dependencies**: [UNIT-FRONT-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Tests cover booking, cancellation, rescheduling, and availability checks

#### Task: UNIT-FRONT-007
- **title**: Write unit tests for useOffline composable
- **description**: Test offline detection, queue management, data persistence, and sync triggers.
- **inputs**: composables/useOffline.ts, IndexedDB service
- **outputs**: tests/composables/useOffline.spec.ts
- **dependencies**: [UNIT-FRONT-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Test offline/online transitions, queue processing, and conflict resolution

#### Task: UNIT-FRONT-008
- **title**: Write unit tests for French date formatting utilities
- **description**: Test date formatting for French locale including jour/mois/année, relative dates, and business day calculations.
- **inputs**: utils/dateFormat.ts, i18n files
- **outputs**: tests/utils/dateFormat.spec.ts
- **dependencies**: [UNIT-FRONT-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Verify "1er janvier 2026", "14 février 2026", and relative date formats

#### Task: UNIT-FRONT-009
- **title**: Write unit tests for French currency formatting utilities
- **description**: Test Euro (€) formatting with French locale rules: space before symbol, proper decimal handling.
- **inputs**: utils/currencyFormat.ts
- **outputs**: tests/utils/currencyFormat.spec.ts
- **dependencies**: [UNIT-FRONT-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Verify "1 234,56 €" format, large numbers, and zero/negative cases

#### Task: UNIT-FRONT-010
- **title**: Write unit tests for form validation composables
- **description**: Test all form validation logic including email (French domains), phone (French format), SIRET/SIREN, and required field checks.
- **inputs**: composables/useValidation.ts, validation rules
- **outputs**: tests/composables/useValidation.spec.ts
- **dependencies**: [UNIT-FRONT-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Test French-specific validations: 06 XX XX XX XX, SIRET 12345678901234

#### Task: UNIT-FRONT-011
- **title**: Write unit tests for notification composable
- **description**: Test notification triggering, queuing, and display logic for email, SMS, and push notifications.
- **inputs**: composables/useNotification.ts
- **outputs**: tests/composables/useNotification.spec.ts
- **dependencies**: [UNIT-FRONT-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Test notification preferences, rate limiting, and fallback behavior

#### Task: UNIT-FRONT-012
- **title**: Write unit tests for Vue components: ClientCard
- **description**: Test ClientCard component rendering, props handling, emits, and interaction states.
- **inputs**: components/Client/ClientCard.vue
- **outputs**: tests/components/Client/ClientCard.spec.ts
- **dependencies**: [UNIT-FRONT-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Component renders correctly with all prop combinations

#### Task: UNIT-FRONT-013
- **title**: Write unit tests for Vue components: QuoteForm
- **description**: Test QuoteForm component with line items, totals calculation, French formatting, and validation.
- **inputs**: components/Quote/QuoteForm.vue
- **outputs**: tests/components/Quote/QuoteForm.spec.ts
- **dependencies**: [UNIT-FRONT-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Form validation, calculation accuracy, and submission handling tested

#### Task: UNIT-FRONT-014
- **title**: Write unit tests for Vue components: InvoicePDFPreview
- **description**: Test invoice PDF preview component rendering and data binding.
- **inputs**: components/Invoice/InvoicePDFPreview.vue
- **outputs**: tests/components/Invoice/InvoicePDFPreview.spec.ts
- **dependencies**: [UNIT-FRONT-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: PDF preview renders with correct French formatting

#### Task: UNIT-FRONT-015
- **title**: Write unit tests for Vue components: CalendarGrid
- **description**: Test calendar grid component with appointments, time slots, and navigation.
- **inputs**: components/Calendar/CalendarGrid.vue
- **outputs**: tests/components/Calendar/CalendarGrid.spec.ts
- **dependencies**: [UNIT-FRONT-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Calendar displays correctly with French day/month names

#### Task: UNIT-FRONT-016
- **title**: Write unit tests for Vue components: PaymentForm
- **description**: Test Stripe payment form component with card validation and error handling.
- **inputs**: components/Payment/PaymentForm.vue
- **outputs**: tests/components/Payment/PaymentForm.spec.ts
- **dependencies**: [UNIT-FRONT-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Card validation, error states, and loading states tested

#### Task: UNIT-FRONT-017
- **title**: Write unit tests for Pinia stores: auth store
- **description**: Test authentication Pinia store with persistence, token refresh, and user state management.
- **inputs**: stores/auth.ts
- **outputs**: tests/stores/auth.spec.ts
- **dependencies**: [UNIT-FRONT-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Store state transitions and persistence tested

#### Task: UNIT-FRONT-018
- **title**: Write unit tests for Pinia stores: clients store
- **description**: Test clients Pinia store with CRUD actions, filtering, and selection state.
- **inputs**: stores/clients.ts
- **outputs**: tests/stores/clients.spec.ts
- **dependencies**: [UNIT-FRONT-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: All store actions and getters tested with mock API

#### Task: UNIT-FRONT-019
- **title**: Write unit tests for Pinia stores: quotes store
- **description**: Test quotes Pinia store with quote lifecycle management and status tracking.
- **inputs**: stores/quotes.ts
- **outputs**: tests/stores/quotes.spec.ts
- **dependencies**: [UNIT-FRONT-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Quote creation, updates, and status transitions tested

#### Task: UNIT-FRONT-020
- **title**: Write unit tests for Pinia stores: invoices store
- **description**: Test invoices Pinia store with payment tracking and overdue handling.
- **inputs**: stores/invoices.ts
- **outputs**: tests/stores/invoices.spec.ts
- **dependencies**: [UNIT-FRONT-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Invoice generation, payment updates, and reminders tested

#### Task: UNIT-BACK-001
- **title**: Configure Jest for backend testing
- **description**: Set up Jest testing framework for Node.js backend with TypeScript support, database mocking, and environment configuration.
- **inputs**: package.json, tsconfig.json
- **outputs**: jest.config.ts, setupTestFramework.ts
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Run `npx jest` and confirm test environment initializes correctly

#### Task: UNIT-BACK-002
- **title**: Write unit tests for auth service
- **description**: Test authentication service covering password hashing, JWT generation/verification, and token refresh logic.
- **inputs**: services/authService.ts
- **outputs**: tests/services/authService.spec.ts
- **dependencies**: [UNIT-BACK-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: 15+ test cases for auth operations with mock database

#### Task: UNIT-BACK-003
- **title**: Write unit tests for client repository
- **description**: Test client data access layer with CRUD operations, search, filtering, and pagination queries.
- **inputs**: repositories/clientRepository.ts
- **outputs**: tests/repositories/clientRepository.spec.ts
- **dependencies**: [UNIT-BACK-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: All database operations tested with mock query builder

#### Task: UNIT-BACK-004
- **title**: Write unit tests for quote repository
- **description**: Test quote data access with line items, status management, and PDF generation data preparation.
- **inputs**: repositories/quoteRepository.ts
- **outputs**: tests/repositories/quoteRepository.spec.ts
- **dependencies**: [UNIT-BACK-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Quote lifecycle queries tested with mock database

#### Task: UNIT-BACK-005
- **title**: Write unit tests for invoice repository
- **description**: Test invoice generation, payment recording, and due date calculation queries.
- **inputs**: repositories/invoiceRepository.ts
- **outputs**: tests/repositories/invoiceRepository.spec.ts
- **dependencies**: [UNIT-BACK-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Invoice queries and calculations tested

#### Task: UNIT-BACK-006
- **title**: Write unit tests for appointment repository
- **description**: Test appointment scheduling queries including availability checks and conflict detection.
- **inputs**: repositories/appointmentRepository.ts
- **outputs**: tests/repositories/appointmentRepository.spec.ts
- **dependencies**: [UNIT-BACK-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Scheduling logic and conflict detection tested

#### Task: UNIT-BACK-007
- **title**: Write unit tests for Stripe service
- **description**: Test Stripe integration service covering payment intent creation, webhook handling, and refund processing.
- **inputs**: services/stripeService.ts
- **outputs**: tests/services/stripeService.spec.ts
- **dependencies**: [UNIT-BACK-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Stripe API interactions mocked and verified

#### Task: UNIT-BACK-008
- **title**: Write unit tests for notification service
- **description**: Test email/SMS/push notification dispatching with queue management and retry logic.
- **inputs**: services/notificationService.ts
- **outputs**: tests/services/notificationService.spec.ts
- **dependencies**: [UNIT-BACK-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Notification delivery and fallback tested

#### Task: UNIT-BACK-009
- **title**: Write unit tests for French business number validators
- **description**: Test SIRET, SIREN, and TVA validation utilities with French-specific algorithms.
- **inputs**: utils/validators.ts
- **outputs**: tests/utils/validators.spec.ts
- **dependencies**: [UNIT-BACK-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: SIRET checksum (Luhn algorithm) and TVA number validation tested

#### Task: UNIT-BACK-010
- **title**: Write unit tests for PDF generation service
- **description**: Test invoice/quote PDF generation with French formatting and template rendering.
- **inputs**: services/pdfService.ts
- **outputs**: tests/services/pdfService.spec.ts
- **dependencies**: [UNIT-BACK-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: PDF content and French layout verified

#### Task: UNIT-BACK-011
- **title**: Write unit tests for sync service (offline)
- **description**: Test data synchronization logic for offline mode including conflict resolution and delta updates.
- **inputs**: services/syncService.ts
- **outputs**: tests/services/syncService.spec.ts
- **dependencies**: [UNIT-BACK-001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Sync operations, conflict handling, and rollback tested

#### Task: UNIT-BACK-012
- **title**: Write unit tests for email template renderer
- **description**: Test French email templates with variable interpolation and formatting.
- **inputs**: templates/emails/*.hbs
- **outputs**: tests/templates/emailRenderer.spec.ts
- **dependencies**: [UNIT-BACK-001]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: All French email templates render correctly with test data

---

### Category: Integration Testing (API Routes, Database Queries)

#### Task: INT-API-001
- **title**: Set up test database with Docker
- **description**: Create PostgreSQL test container with schema migrations and seed data for integration testing.
- **inputs**: docker-compose.test.yml, migrations
- **outputs**: Running test database, schema applied
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Database accessible, schema verified with pg_dump inspection

#### Task: INT-API-002
- **title**: Configure Supertest for API testing
- **description**: Set up Supertest with Jest for HTTP API integration testing against the Express/Nuxt server.
- **inputs**: package.json, jest.config.ts
- **outputs**: Configured test agent, base test setup
- **dependencies**: [INT-API-001, UNIT-BACK-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Can make HTTP requests to test server in Jest environment

#### Task: INT-API-003
- **title**: Integration test POST /api/auth/register
- **description**: Test user registration endpoint with valid/invalid data, duplicate email handling, and password validation.
- **inputs**: API route handler, request payloads
- **outputs**: tests/integration/auth.spec.ts with register tests
- **dependencies**: [INT-API-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: 10+ test cases for registration scenarios

#### Task: INT-API-004
- **title**: Integration test POST /api/auth/login
- **description**: Test login endpoint with valid credentials, wrong password, non-existent user, and rate limiting.
- **inputs**: API route handler, auth middleware
- **outputs**: tests/integration/auth.spec.ts with login tests
- **dependencies**: [INT-API-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: All authentication scenarios tested including JWT response

#### Task: INT-API-005
- **title**: Integration test POST /api/auth/refresh
- **description**: Test token refresh endpoint with valid/expired tokens and concurrent refresh handling.
- **inputs**: API route handler, JWT service
- **outputs**: tests/integration/auth.spec.ts with refresh tests
- **dependencies**: [INT-API-004]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Token refresh flow works correctly

#### Task: INT-API-006
- **title**: Integration test CRUD /api/clients
- **description**: Test all client CRUD endpoints with authentication, validation, pagination, and search.
- **inputs**: Client API routes, client repository
- **outputs**: tests/integration/clients.spec.ts
- **dependencies**: [INT-API-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Full client CRUD tested with 403, 401, and 400 error codes

#### Task: INT-API-007
- **title**: Integration test GET /api/clients/:id with relations
- **description**: Test client retrieval with related quotes, invoices, and appointments eager loaded.
- **inputs**: Client API routes, query optimization
- **outputs**: tests/integration/clients.spec.ts with relation tests
- **dependencies**: [INT-API-006]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Related data returned correctly in single query

#### Task: INT-API-008
- **title**: Integration test CRUD /api/quotes
- **description**: Test quote creation with line items, status updates, and PDF generation trigger.
- **inputs**: Quote API routes, quote repository
- **outputs**: tests/integration/quotes.spec.ts
- **dependencies**: [INT-API-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Quote lifecycle fully tested with 20+ test cases

#### Task: INT-API-009
- **title**: Integration test POST /api/quotes/:id/send
- **description**: Test quote email sending endpoint with client notification and delivery tracking.
- **inputs**: Quote API routes, notification service
- **outputs**: tests/integration/quotes.spec.ts with send tests
- **dependencies**: [INT-API-008]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Quote sent successfully and status updated

#### Task: INT-API-010
- **title**: Integration test POST /api/quotes/:id/accept
- **description**: Test quote acceptance workflow converting quote to invoice automatically.
- **inputs**: Quote API routes, invoice generation logic
- **outputs**: tests/integration/quotes.spec.ts with accept tests
- **dependencies**: [INT-API-008]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Quote accepted and invoice created in database

#### Task: INT-API-011
- **title**: Integration test CRUD /api/invoices
- **description**: Test invoice generation, payment recording, and status tracking endpoints.
- **inputs**: Invoice API routes, invoice repository
- **outputs**: tests/integration/invoices.spec.ts
- **dependencies**: [INT-API-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Invoice lifecycle tested with payment scenarios

#### Task: INT-API-012
- **title**: Integration test POST /api/invoices/:id/pay
- **description**: Test invoice payment recording with Stripe payment intent integration.
- **inputs**: Invoice API routes, Stripe service
- **outputs**: tests/integration/invoices.spec.ts with payment tests
- **dependencies**: [INT-API-011]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Payment processed and invoice status updated to "paid"

#### Task: INT-API-013
- **title**: Integration test GET /api/invoices/:id/pdf
- **description**: Test invoice PDF download/generation endpoint with French formatting.
- **inputs**: Invoice API routes, PDF service
- **outputs**: tests/integration/invoices.spec.ts with PDF tests
- **dependencies**: [INT-API-011]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: PDF generated with correct French invoice format

#### Task: INT-API-014
- **title**: Integration test CRUD /api/appointments
- **description**: Test appointment creation with availability checking and conflict detection.
- **inputs**: Appointment API routes, calendar service
- **outputs**: tests/integration/appointments.spec.ts
- **dependencies**: [INT-API-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Appointment booking with conflict detection tested

#### Task: INT-API-015
- **title**: Integration test GET /api/appointments/availability
- **description**: Test availability endpoint returning available time slots for given date range.
- **inputs**: Appointment API routes, availability logic
- **outputs**: tests/integration/appointments.spec.ts with availability tests
- **dependencies**: [INT-API-014]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Available slots returned correctly excluding booked times

#### Task: INT-API-016
- **title**: Integration test POST /api/notifications/send
- **description**: Test notification dispatch endpoint supporting email, SMS, and push channels.
- **inputs**: Notification API routes, notification service
- **outputs**: tests/integration/notifications.spec.ts
- **dependencies**: [INT-API-002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Notifications dispatched to correct channel

#### Task: INT-API-017
- **title**: Integration test POST /api/webhooks/stripe
- **description**: Test Stripe webhook endpoint handling payment_intent.succeeded and other events.
- **inputs**: Stripe webhook handler, event types
- **outputs**: tests/integration/webhooks.spec.ts
- **dependencies**: [INT-API-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Webhook events processed and database updated correctly

#### Task: INT-API-018
- **title**: Integration test offline sync endpoint
- **description**: Test data synchronization endpoint for offline mode with delta updates and conflict resolution.
- **inputs**: Sync API routes, sync service
- **outputs**: tests/integration/sync.spec.ts
- **dependencies**: [INT-API-002]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Sync operations handle creates, updates, deletes correctly

#### Task: INT-API-019
- **title**: Database query performance testing
- **description**: Test and benchmark slow queries identified in N+1 detection, missing indexes, and complex joins.
- **inputs**: Query logs, slow query config
- **outputs**: tests/integration/performance/queries.spec.ts
- **dependencies**: [INT-API-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: All critical queries execute under 100ms with EXPLAIN ANALYZE

#### Task: INT-API-020
- **title**: Database transaction rollback testing
- **description**: Test that failed operations properly rollback database transactions.
- **inputs**: Transaction boundary code
- **outputs**: tests/integration/transactions.spec.ts
- **dependencies**: [INT-API-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Failed operations leave database in consistent state

#### Task: INT-API-021
- **title**: API rate limiting integration test
- **description**: Test rate limiting middleware on all public endpoints with various request patterns.
- **inputs**: Rate limit config, Redis
- **outputs**: tests/integration/rateLimit.spec.ts
- **dependencies**: [INT-API-002]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Rate limiting returns 429 after threshold exceeded

#### Task: INT-API-022
- **title**: API pagination integration test
- **description**: Test cursor-based and offset pagination on list endpoints with various page sizes.
- **inputs**: Pagination middleware, list endpoints
- **outputs**: tests/integration/pagination.spec.ts
- **dependencies**: [INT-API-002]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Pagination returns correct page, total count, and next/prev cursors

---

### Category: E2E Testing (Playwright for Critical Flows)

#### Task: E2E-001
- **title**: Configure Playwright for E2E testing
- **description**: Set up Playwright with Nuxt 3 including page object models, test fixtures, and CI configuration.
- **inputs**: package.json, playwright.config.ts
- **outputs**: Playwright test setup, base fixtures, page objects
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Playwright tests run successfully against dev server

#### Task: E2E-002
- **title**: E2E test user registration flow
- **description**: Test complete user registration flow including form filling, email verification link, and first login.
- **inputs**: Registration page, email testing utilities
- **outputs**: tests/e2e/auth/register.spec.ts
- **dependencies**: [E2E-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: User can register, verify email, and access dashboard

#### Task: E2E-003
- **title**: E2E test user login flow
- **description**: Test login with valid credentials, wrong password, account lockout, and "forgot password" flow.
- **inputs**: Login page, password reset utilities
- **outputs**: tests/e2e/auth/login.spec.ts
- **dependencies**: [E2E-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Login works correctly, error states display properly

#### Task: E2E-004
- **title**: E2E test client creation flow
- **description**: Test creating a new client with all fields, validation errors, and success confirmation.
- **inputs**: Client creation page, form components
- **outputs**: tests/e2e/clients/create.spec.ts
- **dependencies**: [E2E-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Client created and appears in client list

#### Task: E2E-005
- **title**: E2E test client editing and deletion flow
- **description**: Test editing existing client data and deleting client with confirmation dialog.
- **inputs**: Client detail page, edit form
- **outputs**: tests/e2e/clients/edit.spec.ts
- **dependencies**: [E2E-004]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Client updates persist and deletion removes from database

#### Task: E2E-006
- **title**: E2E test client search and filtering
- **description**: Test client search by name, email, and filter by tags, date range, and status.
- **inputs**: Client list page, search functionality
- **outputs**: tests/e2e/clients/search.spec.ts
- **dependencies**: [E2E-004]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Search returns correct results with highlighting

#### Task: E2E-007
- **title**: E2E test quote creation flow
- **description**: Test creating a quote with line items, tax calculation, validity period, and client selection.
- **inputs**: Quote creation page, product catalog
- **outputs**: tests/e2e/quotes/create.spec.ts
- **dependencies**: [E2E-001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: Quote created with correct totals and French formatting

#### Task: E2E-008
- **title**: E2E test quote sending via email
- **description**: Test sending quote to client email with PDF attachment and tracking pixel.
- **inputs**: Quote send dialog, email testing
- **outputs**: tests/e2e/quotes/send.spec.ts
- **dependencies**: [E2E-007]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Email sent with correct quote PDF attachment

#### Task: E2E-009
- **title**: E2E test quote acceptance flow
- **description**: Test client receiving quote email, viewing quote page, and accepting quote with digital signature.
- **inputs**: Quote public page, acceptance form
- **outputs**: tests/e2e/quotes/accept.spec.ts
- **dependencies**: [E2E-008]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: Quote accepted and invoice auto-generated

#### Task: E2E-010
- **title**: E2E test quote rejection flow
- **description**: Test client rejecting quote with reason and artisan receiving notification.
- **inputs**: Quote public page, rejection form
- **outputs**: tests/e2e/quotes/reject.spec.ts
- **dependencies**: [E2E-008]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Quote status updated to rejected with reason stored

#### Task: E2E-011
- **title**: E2E test invoice generation from quote
- **description**: Test automatic invoice generation when quote is accepted, including invoice numbering.
- **inputs**: Invoice list page, quote acceptance
-