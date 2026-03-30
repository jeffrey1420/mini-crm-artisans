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
-- **title**: E2E test invoice generation from quote
- **description**: Test automatic invoice generation when quote is accepted, including invoice numbering.
- **inputs**: Invoice list page, quote acceptance
- **outputs**: tests/e2e/invoices/generate.spec.ts
- **dependencies**: [E2E-009]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Invoice auto-generated with correct number sequence

#### Task: E2E-012
- **title**: E2E test invoice payment with Stripe
- **description**: Test full Stripe checkout flow for invoice payment including card entry and 3D secure.
- **inputs**: Invoice payment page, Stripe Elements
- **outputs**: tests/e2e/invoices/payment.spec.ts
- **dependencies**: [E2E-011]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: Payment processed and invoice marked as paid

#### Task: E2E-013
- **title**: E2E test invoice PDF download
- **description**: Test downloading invoice PDF with French legal requirements and proper formatting.
- **inputs**: Invoice detail page, PDF download button
- **outputs**: tests/e2e/invoices/pdf.spec.ts
- **dependencies**: [E2E-011]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: PDF downloaded with correct French invoice format

#### Task: E2E-014
- **title**: E2E test appointment booking flow
- **description**: Test selecting time slot, entering details, and receiving confirmation for appointment.
- **inputs**: Calendar page, booking form
- **outputs**: tests/e2e/appointments/booking.spec.ts
- **dependencies**: [E2E-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Appointment booked and appears in calendar

#### Task: E2E-015
- **title**: E2E test appointment rescheduling
- **description**: Test changing appointment time including conflict detection and client notification.
- **inputs**: Appointment detail page, reschedule dialog
- **outputs**: tests/e2e/appointments/reschedule.spec.ts
- **dependencies**: [E2E-014]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Appointment rescheduled and confirmation sent

#### Task: E2E-016
- **title**: E2E test appointment cancellation
- **description**: Test canceling appointment with reason and cancellation policy enforcement.
- **inputs**: Appointment detail page, cancel dialog
- **outputs**: tests/e2e/appointments/cancel.spec.ts
- **dependencies**: [E2E-014]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Appointment canceled and status updated

#### Task: E2E-017
- **title**: E2E test dashboard navigation
- **description**: Test all dashboard navigation elements, quick actions, and recent activity feeds.
- **inputs**: Dashboard page, sidebar navigation
- **outputs**: tests/e2e/dashboard/navigation.spec.ts
- **dependencies**: [E2E-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: All navigation links work and load correct content

#### Task: E2E-018
- **title**: E2E test mobile menu and navigation
- **description**: Test hamburger menu, drawer navigation, and back button behavior on mobile.
- **inputs**: Mobile viewport, responsive design
- **outputs**: tests/e2e/mobile/navigation.spec.ts
- **dependencies**: [E2E-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Mobile navigation works correctly on small screens

#### Task: E2E-019
- **title**: E2E test settings page
- **description**: Test updating profile, changing password, notification preferences, and business settings.
- **inputs**: Settings pages, form components
- **outputs**: tests/e2e/settings/profile.spec.ts
- **dependencies**: [E2E-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Settings persist after page refresh

#### Task: E2E-020
- **title**: E2E test French locale toggle
- **description**: Test switching between French and other locales with all text, dates, and currency updating.
- **inputs**: Locale switcher, i18n implementation
- **outputs**: tests/e2e/i18n/locale.spec.ts
- **dependencies**: [E2E-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: All UI text updates to selected language

#### Task: E2E-021
- **title**: E2E test offline mode indicator
- **description**: Test offline mode detection and visual indicator showing app is offline.
- **inputs**: Service worker, offline detection
- **outputs**: tests/e2e/offline/indicator.spec.ts
- **dependencies**: [E2E-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Offline indicator appears when network disconnected

#### Task: E2E-022
- **title**: E2E test data persistence in offline mode
- **description**: Test creating and editing data while offline with local storage persistence.
- **inputs**: Offline mode, IndexedDB
- **outputs**: tests/e2e/offline/persistence.spec.ts
- **dependencies**: [E2E-021]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: Data persists locally when offline and syncs when online

#### Task: E2E-023
- **title**: E2E test PWA installation
- **description**: Test installing app as PWA on iOS Safari and Android Chrome with install prompt.
- **inputs**: PWA manifest, service worker
- **outputs**: tests/e2e/pwa/install.spec.ts
- **dependencies**: [E2E-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: PWA installs and launches from home screen

#### Task: E2E-024
- **title**: E2E test push notification permission
- **description**: Test push notification permission request, acceptance, and denial handling.
- **inputs**: Notification permission API
- **outputs**: tests/e2e/notifications/permission.spec.ts
- **dependencies**: [E2E-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Permission flow handled correctly

#### Task: E2E-025
- **title**: E2E test push notification display
- **description**: Test receiving and displaying push notifications for quotes, invoices, and appointments.
- **inputs**: Push notification service, browser notifications
- **outputs**: tests/e2e/notifications/display.spec.ts
- **dependencies**: [E2E-024]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Push notifications display correctly with French text

#### Task: E2E-026
- **title**: E2E test session timeout and refresh
- **description**: Test session timeout warning, automatic refresh, and forced logout after inactivity.
- **inputs**: Session management, inactivity timer
- **outputs**: tests/e2e/auth/session.spec.ts
- **dependencies**: [E2E-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Session refresh works and timeout redirects to login

---

### Category: API Contract Testing

#### Task: CONTRACT-001
- **title**: Define OpenAPI specification for all endpoints
- **description**: Create comprehensive OpenAPI 3.0 specification documenting all API endpoints, request/response schemas, and authentication.
- **inputs**: API routes, existing documentation
- **outputs**: openapi.yaml, schema definitions
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: OpenAPI spec validates against API using swagger-cli

#### Task: CONTRACT-002
- **title**: Set up Dredd for contract testing
- **description**: Configure Dredd API testing framework with OpenAPI hooks for contract validation.
- **inputs**: openapi.yaml, Dredd config
- **outputs**: dredd.yml, hooks file
- **dependencies**: [CONTRACT-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Dredd runs against live API and validates responses

#### Task: CONTRACT-003
- **title**: Contract test auth endpoints
- **description**: Test auth endpoints against OpenAPI spec ensuring request/response matches contract.
- **inputs**: Auth endpoints, openapi.yaml
- **outputs**: tests/contract/auth.spec.ts
- **dependencies**: [CONTRACT-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: All auth contract tests pass

#### Task: CONTRACT-004
- **title**: Contract test client endpoints
- **description**: Test client CRUD endpoints against OpenAPI spec with all field validations.
- **inputs**: Client endpoints, openapi.yaml
- **outputs**: tests/contract/clients.spec.ts
- **dependencies**: [CONTRACT-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: All client contract tests pass

#### Task: CONTRACT-005
- **title**: Contract test quote endpoints
- **description**: Test quote endpoints against OpenAPI spec including line items and status transitions.
- **inputs**: Quote endpoints, openapi.yaml
- **outputs**: tests/contract/quotes.spec.ts
- **dependencies**: [CONTRACT-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: All quote contract tests pass

#### Task: CONTRACT-006
- **title**: Contract test invoice endpoints
- **description**: Test invoice endpoints against OpenAPI spec with payment status and PDF generation.
- **inputs**: Invoice endpoints, openapi.yaml
- **outputs**: tests/contract/invoices.spec.ts
- **dependencies**: [CONTRACT-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: All invoice contract tests pass

#### Task: CONTRACT-007
- **title**: Contract test appointment endpoints
- **description**: Test appointment endpoints against OpenAPI spec including availability and conflicts.
- **inputs**: Appointment endpoints, openapi.yaml
- **outputs**: tests/contract/appointments.spec.ts
- **dependencies**: [CONTRACT-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: All appointment contract tests pass

#### Task: CONTRACT-008
- **title**: Validate response time in contract tests
- **description**: Add performance assertions to contract tests ensuring response times meet SLA.
- **inputs**: Dredd hooks, performance基准
- **outputs**: Updated contract tests with timing assertions
- **dependencies**: [CONTRACT-002]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Contract tests fail if response exceeds 500ms threshold

#### Task: CONTRACT-009
- **title**: Generate API client from OpenAPI spec
- **description**: Use OpenAPI generator to create TypeScript client library from spec.
- **inputs**: openapi.yaml, OpenAPI generator
- **outputs**: Generated client in /lib/api-client
- **dependencies**: [CONTRACT-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Generated client compiles and matches spec exactly

#### Task: CONTRACT-010
- **title**: Test webhook contracts
- **description**: Test Stripe webhook payload structure against expected contract and handle all event types.
- **inputs**: Stripe webhooks, event schemas
- **outputs**: tests/contract/webhooks.spec.ts
- **dependencies**: [CONTRACT-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: All webhook event types handled correctly

---

### Category: Mobile/PWA Testing

#### Task: PWA-001
- **title**: Verify PWA manifest validity
- **description**: Test PWA manifest.json for required fields, correct icons, theme colors, and display mode.
- **inputs**: manifest.json, Lighthouse
- **outputs**: Lighthouse PWA audit report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Lighthouse PWA score above 90

#### Task: PWA-002
- **title**: Test service worker caching strategies
- **description**: Verify service worker caches static assets, API responses, and handles cache invalidation.
- **inputs**: Service worker file, caching config
- **outputs**: Service worker test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Assets cached correctly and served from cache offline

#### Task: PWA-003
- **title**: Test PWA on iOS Safari
- **description**: Test PWA functionality on iOS Safari including installation, add to home screen, and push notifications.
- **inputs**: iOS device or simulator, Safari
- **outputs**: iOS PWA test report
- **dependencies**: [PWA-001, PWA-002]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: PWA works on iOS Safari with all features functional

#### Task: PWA-004
- **title**: Test PWA on Android Chrome
- **description**: Test PWA functionality on Android Chrome including installation, notifications, and background sync.
- **inputs**: Android device or emulator, Chrome
- **outputs**: Android PWA test report
- **dependencies**: [PWA-001, PWA-002]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: PWA works on Android Chrome with all features functional

#### Task: PWA-005
- **title**: Test app shell rendering
- **description**: Verify app shell architecture renders correctly with skeleton loaders during content load.
- **inputs**: App shell components, loading states
- **outputs**: App shell test report
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: App shell renders instantly without layout shift

#### Task: PWA-006
- **title**: Test push notifications on mobile
- **description**: Test push notification delivery on iOS and Android with notification permission flow.
- **inputs**: Push notification service, mobile devices
- **outputs**: Push notification test report
- **dependencies**: [PWA-003, PWA-004]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: Push notifications delivered on both platforms

#### Task: PWA-007
- **title**: Test background sync on mobile
- **description**: Test background sync API for offline data submission when connection restored.
- **inputs**: Background sync API, offline actions
- **outputs**: Background sync test report
- **dependencies**: [PWA-002]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: Offline actions sync when connection restored

#### Task: PWA-008
- **title**: Test PWA update flow
- **description**: Test app update notification, service worker update, and refresh to new version.
- **inputs**: Version management, update flow
- **outputs**: Update flow test report
- **dependencies**: [PWA-002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: App updates correctly when new version available

#### Task: PWA-009
- **title**: Test standalone display mode
- **description**: Verify PWA opens in standalone mode without browser chrome when launched from home screen.
- **inputs**: PWA manifest, display settings
- **outputs**: Standalone mode test report
- **dependencies**: [PWA-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: PWA opens fullscreen without URL bar

#### Task: PWA-010
- **title**: Test device orientation handling
- **description**: Verify app handles portrait and landscape orientations correctly without layout breaks.
- **inputs**: Responsive design, orientation handling
- **outputs**: Orientation test report
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Layout adapts correctly to both orientations

#### Task: PWA-011
- **title**: Test touch interactions on mobile
- **description**: Verify all touch interactions work correctly including swipe, tap, long press, and pinch zoom.
- **inputs**: Touch event handlers, gesture handling
- **outputs**: Touch interaction test report
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: All touch interactions work as expected

#### Task: PWA-012
- **title**: Test biometric authentication on mobile
- **description**: Test Face ID / Touch ID / fingerprint authentication for app unlock on supported devices.
- **inputs**: WebAuthn API, biometric providers
- **outputs**: Biometric auth test report
- **dependencies**: []
- **priority**: low
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: Biometric authentication works on supported devices

#### Task: PWA-013
- **title**: Test offline page functionality
- **description**: Verify offline fallback page displays correctly when network unavailable and cached content exhausted.
- **inputs**: Offline fallback page, service worker
- **outputs**: Offline page test report
- **dependencies**: [PWA-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Offline page displays with retry functionality

#### Task: PWA-014
- **title**: Test PWA on slow 3G connection
- **description**: Test PWA loading and functionality on slow 3G network throttled in DevTools.
- **inputs**: Network throttling, Lighthouse
- **outputs**: Slow connection test report
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: App usable on slow connection with progressive loading

---

### Category: Offline Mode Testing

#### Task: OFFLINE-001
- **title**: Test IndexedDB data persistence
- **description**: Verify all client, quote, invoice, and appointment data persists in IndexedDB when offline.
- **inputs**: IndexedDB implementation, offline data
- **outputs**: IndexedDB persistence test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Data persists in IndexedDB and survives browser restart

#### Task: OFFLINE-002
- **title**: Test offline client creation
- **description**: Test creating a new client while offline and verifying it saves to IndexedDB.
- **inputs**: Client creation form, offline mode
- **outputs**: Offline client creation test report
- **dependencies**: [OFFLINE-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Client created offline appears in local database

#### Task: OFFLINE-003
- **title**: Test offline quote creation
- **description**: Test creating a quote with line items while offline and saving to IndexedDB.
- **inputs**: Quote creation form, offline mode
- **outputs**: Offline quote creation test report
- **dependencies**: [OFFLINE-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Quote created offline with all line items saved locally

#### Task: OFFLINE-004
- **title**: Test offline data sync queue
- **description**: Verify offline actions are queued and display pending sync indicator.
- **inputs**: Sync queue implementation, queue UI
- **outputs**: Sync queue test report
- **dependencies**: [OFFLINE-002, OFFLINE-003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Offline actions queued with visual indicator

#### Task: OFFLINE-005
- **title**: Test automatic sync on reconnection
- **description**: Test that queued offline actions sync automatically when connection restored.
- **inputs**: Network detection, sync service
- **outputs**: Auto-sync test report
- **dependencies**: [OFFLINE-004]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: Queued actions sync without manual intervention

#### Task: OFFLINE-006
- **title**: Test conflict resolution on sync
- **description**: Test conflict detection when same record edited offline and online before sync.
- **inputs**: Conflict resolution logic, sync service
- **outputs**: Conflict resolution test report
- **dependencies**: [OFFLINE-005]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: Conflicts detected and resolution UI shown to user

#### Task: OFFLINE-007
- **title**: Test sync failure handling
- **description**: Verify sync failures display error message and allow retry.
- **inputs**: Error handling, retry logic
- **outputs**: Sync failure test report
- **dependencies**: [OFFLINE-005]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Sync failures shown with retry option

#### Task: OFFLINE-008
- **title**: Test partial sync with large datasets
- **description**: Test syncing large client lists with pagination and chunked sync operations.
- **inputs**: Large dataset, pagination
- **outputs**: Large dataset sync test report
- **dependencies**: [OFFLINE-005]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: Large datasets sync in chunks without timeout

#### Task: OFFLINE-009
- **title**: Test offline image/file uploads
- **description**: Test uploading client attachments while offline with queue and retry.
- **inputs**: File upload service, offline queue
- **outputs**: Offline file upload test report
- **dependencies**: [OFFLINE-004]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: Files queued offline and uploaded when online

#### Task: OFFLINE-010
- **title**: Test IndexedDB storage limits
- **description**: Test behavior when IndexedDB storage quota approached or exceeded.
- **inputs**: Storage quota API, large file handling
- **outputs**: Storage limits test report
- **dependencies**: [OFFLINE-001]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: App handles storage limits gracefully with warning

#### Task: OFFLINE-011
- **title**: Test offline accessibility
- **description**: Verify offline mode doesn't break accessibility features and screen readers.
- **inputs**: Accessibility tools, offline mode
- **outputs**: Offline accessibility test report
- **dependencies**: [OFFLINE-001]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Accessibility maintained in offline mode

---

### Category: Payment Flow Testing (Stripe Test Mode)

#### Task: PAY-001
- **title**: Configure Stripe test mode
- **description**: Set up Stripe in test mode with test API keys and verify test card numbers work.
- **inputs**: Stripe dashboard, test API keys
- **outputs**: Stripe test configuration verified
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Test mode enabled and test cards accepted

#### Task: PAY-002
- **title**: Test successful card payment
- **description**: Test complete payment flow with Stripe test card 4242424242424242.
- **inputs**: Payment form, Stripe Elements
- **outputs**: tests/e2e/payments/success.spec.ts
- **dependencies**: [PAY-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Payment succeeds with test card ending 4242

#### Task: PAY-003
- **title**: Test declined card payment
- **description**: Test payment decline with Stripe test card 4000000000000002.
- **inputs**: Payment form, declined test card
- **outputs**: tests/e2e/payments/decline.spec.ts
- **dependencies**: [PAY-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Decline message displayed correctly

#### Task: PAY-004
- **title**: Test insufficient funds payment
- **description**: Test insufficient funds scenario with Stripe test card 4000000000009995.
- **inputs**: Payment form, insufficient funds card
- **outputs**: tests/e2e/payments/insufficient.spec.ts
- **dependencies**: [PAY-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Insufficient funds message displayed correctly

#### Task: PAY-005
- **title**: Test 3D Secure authentication
- **description**: Test 3D Secure authentication flow with Stripe test card 4000002500003155.
- **inputs**: Payment form, 3D Secure test card
- **outputs**: tests/e2e/payments/3ds.spec.ts
- **dependencies**: [PAY-001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: 3D Secure modal appears and payment succeeds after authentication

#### Task: PAY-006
- **title**: Test Stripe webhook delivery
- **description**: Test payment_intent.succeeded webhook delivered and invoice status updated.
- **inputs**: Stripe CLI, webhook endpoint
- **outputs**: Webhook delivery test report
- **dependencies**: [PAY-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Webhook received and invoice marked paid

#### Task: PAY-007
- **title**: Test Stripe webhook signature verification
- **description**: Verify webhook signatures are properly verified and invalid signatures rejected.
- **inputs**: Webhook handler, signature verification
- **outputs**: Webhook signature test report
- **dependencies**: [PAY-006]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Invalid signatures return 400 error

#### Task: PAY-008
- **title**: Test partial refund flow
- **description**: Test partial refund processing with Stripe test refund flow.
- **inputs**: Refund API, invoice with payment
- **outputs**: tests/e2e/payments/refund.spec.ts
- **dependencies**: [PAY-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Partial refund processed and invoice updated

#### Task: PAY-009
- **title**: Test full refund flow
- **description**: Test full refund processing for cancelled invoice or satisfied client.
- **inputs**: Refund API, paid invoice
- **outputs**: tests/e2e/payments/full-refund.spec.ts
- **dependencies**: [PAY-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Full refund processed and payment reversed

#### Task: PAY-010
- **title**: Test payment receipt email
- **description**: Verify payment receipt email sent by Stripe after successful payment.
- **inputs**: Stripe email receipts, test payment
- **outputs**: Payment email test report
- **dependencies**: [PAY-002]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Receipt email received with correct amount

#### Task: PAY-011
- **title**: Test French invoice with Euro pricing
- **description**: Test Stripe displays correct Euro (€) amounts on payment form.
- **inputs**: Invoice in Euros, Stripe Elements localization
- **outputs**: Euro pricing test report
- **dependencies**: [PAY-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Payment form shows correct Euro formatting

#### Task: PAY-012
- **title**: Test payment idempotency
- **description**: Verify duplicate payment attempts are handled idempotently.
- **inputs**: Payment retry logic, Stripe idempotency
- **outputs**: Idempotency test report
- **dependencies**: [PAY-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Duplicate requests don't create duplicate charges

#### Task: PAY-013
- **title**: Test payment intent creation API
- **description**: Test backend payment intent creation with correct amount and currency.
- **inputs**: Payment intent API, Euro currency
- **outputs**: tests/api/payment-intent.spec.ts
- **dependencies**: [PAY-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Payment intent created with correct EUR amount

#### Task: PAY-014
- **title**: Test saved card payment
- **description**: Test payment using previously saved card for returning customers.
- **inputs**: Saved cards, returning customer flow
- **outputs**: Saved card payment test report
- **dependencies**: [PAY-002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Saved card used without re-entering details

#### Task: PAY-015
- **title**: Test subscription payment flow
- **description**: Test recurring subscription payment if applicable with Stripe subscriptions.
- **inputs**: Subscription API, recurring payments
- **outputs**: Subscription payment test report
- **dependencies**: [PAY-001]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: Subscription payments process on schedule

---

### Category: Notification Testing

#### Task: NOTIF-001
- **title**: Test email notification delivery
- **description**: Test all email notifications (quote sent, invoice paid, appointment reminder) are delivered.
- **inputs**: Email service, notification triggers
- **outputs**: tests/notifications/email.spec.ts
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Emails delivered to inbox with correct content

#### Task: NOTIF-002
- **title**: Test French email templates
- **description**: Verify all email templates render correctly with French text and proper formatting.
- **inputs**: Email templates, French translations
- **outputs**: French email template test report
- **dependencies**: [NOTIF-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Email content in French with proper accents

#### Task: NOTIF-003
- **title**: Test SMS notification delivery
- **description**: Test SMS notifications are sent via configured provider with correct French formatting.
- **inputs**: SMS provider, notification service
- **outputs**: tests/notifications/sms.spec.ts
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: SMS delivered with correct French text

#### Task: NOTIF-004
- **title**: Test push notification delivery
- **description**: Test Web Push notifications are delivered to subscribed browsers.
- **inputs**: Push service, notification API
- **outputs**: tests/notifications/push.spec.ts
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Push notification received in browser

#### Task: NOTIF-005
- **title**: Test notification preference management
- **description**: Test users can enable/disable email, SMS, and push notifications per type.
- **inputs**: Notification settings page
- **outputs**: tests/notifications/preferences.spec.ts
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Notification preferences saved and respected

#### Task: NOTIF-006
- **title**: Test notification scheduling
- **description**: Test appointment reminders are scheduled at correct times before appointment.
- **inputs**: Scheduler, appointment times
- **outputs**: Notification scheduling test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Reminders sent at configured intervals before appointment

#### Task: NOTIF-007
- **title**: Test notification retry on failure
- **description**: Verify failed notification delivery retries with exponential backoff.
- **inputs**: Retry logic, failure simulation
- **outputs**: Retry test report
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Failed notifications retried up to max attempts

#### Task: NOTIF-008
- **title**: Test notification rate limiting
- **description**: Verify notification rate limiting prevents spam and respects provider limits.
- **inputs**: Rate limit config, provider limits
- **outputs**: Rate limiting test report
- **dependencies**: []
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Rate limits enforced without breaking functionality

#### Task: NOTIF-009
- **title**: Test quote accepted notification to artisan
- **description**: Test artisan receives email and push when client accepts quote.
- **inputs**: Quote acceptance, notification triggers
- **outputs**: tests/notifications/quote-accepted.spec.ts
- **dependencies**: [NOTIF-001, NOTIF-004]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Artisan notified immediately on quote acceptance

#### Task: NOTIF-010
- **title**: Test invoice overdue notification
- **description**: Test client receives reminder when invoice becomes overdue.
- **inputs**: Overdue invoice, reminder scheduler
- **outputs**: tests/notifications/overdue.spec.ts
- **dependencies**: [NOTIF-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Overdue reminder sent at correct time

#### Task: NOTIF-011
- **title**: Test email unsubscribe
- **description**: Test email unsubscribe link works and stops marketing emails.
- **inputs**: Unsubscribe link, preference center
- **outputs**: tests/notifications/unsubscribe.spec.ts
- **dependencies**: [NOTIF-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Unsubscribed users removed from marketing list

#### Task: NOTIF-012
- **title**: Test notification logging
- **description**: Verify all notification attempts logged for debugging and audit.
- **inputs**: Notification logging service
- **outputs**: Notification log test report
- **dependencies**: []
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Notification logs stored with status and metadata

---

### Category: French Locale Testing

#### Task: FR-001
- **title**: Test French date formatting everywhere
- **description**: Verify all dates display in French format (jour mois année) throughout the application.
- **inputs**: Date display components, French locale
- **outputs**: tests/i18n/fr/dates.spec.ts
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: All dates show "1er janvier 2026" format

#### Task: FR-002
- **title**: Test French month names
- **description**: Verify all 12 French month names display correctly with proper accents.
- **inputs**: Month name translations, date formatting
- **outputs**: tests/i18n/fr/months.spec.ts
- **dependencies**: [FR-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Months display as "janvier", "février", "décembre" etc.

#### Task: FR-003
- **title**: Test French day names
- **description**: Verify French day names (lundi, mardi, etc.) display in calendar and date pickers.
- **inputs**: Day name translations, calendar components
- **outputs**: tests- **inputs**: Day name translations, calendar components
- **outputs**: tests/i18n/fr/days.spec.ts
- **dependencies**: [FR-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Days show as "lundi", "mardi", "dimanche" in calendar

#### Task: FR-004
- **title**: Test French currency formatting (Euros)
- **description**: Verify Euro currency displays with correct French formatting: space before symbol, comma for decimals.
- **inputs**: Currency formatting utilities, invoice totals
- **outputs**: tests/i18n/fr/currency.spec.ts
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: "1 234,56 €" displays correctly everywhere

#### Task: FR-005
- **title**: Test French number formatting
- **description**: Verify numbers use French locale (space as thousands separator, comma for decimals).
- **inputs**: Number formatting, French locale config
- **outputs**: tests/i18n/fr/numbers.spec.ts
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Large numbers show with spaces: "1 234 567"

#### Task: FR-006
- **title**: Test French address formatting
- **description**: Verify French address format (Code postal, Ville) in client and invoice addresses.
- **inputs**: Address templates, French formatting
- **outputs**: tests/i18n/fr/addresses.spec.ts
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Addresses show "75001 Paris" format correctly

#### Task: FR-007
- **title**: Test French phone number formatting
- **description**: Verify French phone numbers display with correct format (06 XX XX XX XX or +33 6 XX XX XX XX).
- **inputs**: Phone formatting, French numbers
- **outputs**: tests/i18n/fr/phone.spec.ts
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: French mobile numbers formatted correctly

#### Task: FR-008
- **title**: Test French business number validation (SIRET)
- **description**: Verify SIRET number validation using Luhn algorithm and proper 14-digit format.
- **inputs**: SIRET validation, test numbers
- **outputs**: tests/i18n/fr/siret.spec.ts
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Valid SIRET accepted, invalid rejected

#### Task: FR-009
- **title**: Test French business number validation (SIREN)
- **description**: Verify SIREN number validation with proper 9-digit format and checksum.
- **inputs**: SIREN validation, test numbers
- **outputs**: tests/i18n/fr/siren.spec.ts
- **dependencies**: [FR-008]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Valid SIREN accepted, invalid rejected

#### Task: FR-010
- **title**: Test French TVA number validation
- **description**: Verify French TVA (VAT) number validation with FR prefix and 2-digit checksum.
- **inputs**: TVA validation, test numbers
- **outputs**: tests/i18n/fr/tva.spec.ts
- **dependencies**: [FR-008]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: French TVA numbers validated correctly

#### Task: FR-011
- **title**: Test French invoice legal mentions
- **description**: Verify French invoice includes required legal mentions (numéro TVA, SIRET, RCS).
- **inputs**: Invoice template, French legal requirements
- **outputs**: French invoice legal test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Invoice includes all required French legal mentions

#### Task: FR-012
- **title**: Test French quote legal mentions
- **description**: Verify French quote includes validity period and required mentions.
- **inputs**: Quote template, French quote requirements
- **outputs**: French quote legal test report
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Quote includes validity period and correct legal text

#### Task: FR-013
- **title**: Test French greetings in emails
- **description**: Verify email templates use appropriate French greetings and formal/informal tone.
- **inputs**: Email templates, French locale
- **outputs**: tests/i18n/fr/emails.spec.ts
- **dependencies**: [NOTIF-002]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Emails open with appropriate French greeting

#### Task: FR-014
- **title**: Test French accent handling in database
- **description**: Verify French accents (é, è, ê, ë, à, â, ô, û, ç) store and retrieve correctly.
- **inputs**: Database encoding, test data with accents
- **outputs**: Accent handling test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: French accents preserved in database and display

#### Task: FR-015
- **title**: Test French relative date expressions
- **description**: Verify French relative dates like "hier", "aujourd'hui", "demain", "dans 3 jours" display correctly.
- **inputs**: Relative date translations, date logic
- **outputs**: tests/i18n/fr/relative-dates.spec.ts
- **dependencies**: [FR-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Relative dates display in correct French form

#### Task: FR-016
- **title**: Test French pluralization rules
- **description**: Verify French pluralization (1 élément, 2 éléments) works correctly in UI.
- **inputs**: i18n plural rules, French locale
- **outputs**: Pluralization test report
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Plural forms correct for all count scenarios

#### Task: FR-017
- **title**: Test French time formatting
- **description**: Verify time displays in French format (21h30, 14h45) and 24-hour clock.
- **inputs**: Time formatting, French locale
- **outputs**: tests/i18n/fr/time.spec.ts
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Times show in 24h French format

#### Task: FR-018
- **title**: Test French document titles
- **description**: Verify PDF document titles use French terminology (Devis, Facture, Contrat).
- **inputs**: Document templates, French terminology
- **outputs**: French document title test report
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Documents titled correctly in French

#### Task: FR-019
- **title**: Test French payment terms
- **description**: Verify payment terms display in French (30 jours nets, à réception).
- **inputs**: Payment terms, French translations
- **outputs**: tests/i18n/fr/payment-terms.spec.ts
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Payment terms display in correct French form

#### Task: FR-020
- **title**: Test RTL consideration for future locales
- **description**: Verify UI layout handles potential RTL languages in future without breaking French layout.
- **inputs**: CSS direction properties, layout structure
- **outputs**: RTL consideration test report
- **dependencies**: []
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: CSS supports dir="rtl" without French breaking

---

### Category: Performance & Load Testing

#### Task: PERF-001
- **title**: Set up Lighthouse CI
- **description**: Configure Lighthouse CI in CI pipeline for automated performance auditing.
- **inputs**: Lighthouse CI, CI config
- **outputs**: lighthouseci.yml, CI integration
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Lighthouse runs in CI and reports scores

#### Task: PERF-002
- **title**: Run Lighthouse performance audit
- **description**: Execute Lighthouse performance audit and verify score meets threshold (>85).
- **inputs**: Lighthouse, production build
- **outputs**: Lighthouse report with scores
- **dependencies**: [PERF-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Performance score above 85 on mobile

#### Task: PERF-003
- **title**: Test First Contentful Paint (FCP)
- **description**: Measure and optimize FCP time targeting under 1.8 seconds.
- **inputs**: Lighthouse, performance metrics
- **outputs**: FCP optimization report
- **dependencies**: [PERF-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: FCP under 1.8s on mobile

#### Task: PERF-004
- **title**: Test Largest Contentful Paint (LCP)
- **description**: Measure and optimize LCP time targeting under 2.5 seconds.
- **inputs**: Lighthouse, LCP elements
- **outputs**: LCP optimization report
- **dependencies**: [PERF-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: LCP under 2.5s on mobile

#### Task: PERF-005
- **title**: Test Time to Interactive (TTI)
- **description**: Measure and optimize TTI targeting under 3.5 seconds.
- **inputs**: Lighthouse, interactive time
- **outputs**: TTI optimization report
- **dependencies**: [PERF-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: TTI under 3.5s on mobile

#### Task: PERF-006
- **title**: Test Cumulative Layout Shift (CLS)
- **description**: Measure and optimize CLS targeting score under 0.1.
- **inputs**: Lighthouse, layout stability
- **outputs**: CLS optimization report
- **dependencies**: [PERF-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: CLS score under 0.1

#### Task: PERF-007
- **title**: Test bundle size
- **description**: Verify JavaScript bundle size stays under 200KB gzipped for initial load.
- **inputs**: Bundle analyzer, webpack config
- **outputs**: Bundle size report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Initial bundle under 200KB gzipped

#### Task: PERF-008
- **title**: Test API response times
- **description**: Measure API endpoint response times and identify slow endpoints (>500ms).
- **inputs**: API endpoints, performance tools
- **outputs**: API response time report
- **dependencies**: [INT-API-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: All API endpoints respond under 500ms

#### Task: PERF-009
- **title**: Configure k6 for load testing
- **description**: Set up k6 load testing tool with scripts for API endpoints.
- **inputs**: k6, load test scenarios
- **outputs**: k6 configuration and scripts
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: k6 runs and produces load test results

#### Task: PERF-010
- **title**: Load test authentication endpoints
- **description**: Run load test on login and auth endpoints with 100 concurrent users.
- **inputs**: k6 scripts, auth endpoints
- **outputs**: Auth load test report
- **dependencies**: [PERF-009]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Auth handles 100 concurrent users without errors

#### Task: PERF-011
- **title**: Load test client list endpoint
- **description**: Run load test on client list with pagination under load.
- **inputs**: k6 scripts, client endpoints
- **outputs**: Client list load test report
- **dependencies**: [PERF-009]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Client list handles load with acceptable response time

#### Task: PERF-012
- **title**: Load test quote creation
- **description**: Run load test on quote creation endpoint with complex line items.
- **inputs**: k6 scripts, quote endpoints
- **outputs**: Quote creation load test report
- **dependencies**: [PERF-009]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Quote creation handles load without timeout

#### Task: PERF-013
- **title**: Load test PDF generation
- **description**: Run load test on PDF generation with concurrent requests.
- **inputs**: k6 scripts, PDF endpoint
- **outputs**: PDF generation load test report
- **dependencies**: [PERF-009]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: PDF generation handles concurrent requests

#### Task: PERF-014
- **title**: Stress test to failure
- **description**: Identify breaking point by gradually increasing load until errors spike.
- **inputs**: k6, stress test config
- **outputs**: Stress test report with breaking point identified
- **dependencies**: [PERF-009]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: Breaking point identified and documented

#### Task: PERF-015
- **title**: Test database connection pooling
- **description**: Verify database connections properly pooled and released under load.
- **inputs**: Database config, connection pooling
- **outputs**: Connection pool test report
- **dependencies**: [PERF-009]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Connections pooled correctly without leaks

#### Task: PERF-016
- **title**: Test memory usage patterns
- **description**: Monitor memory usage during load tests for leaks or excessive consumption.
- **inputs**: Memory profiling tools, load tests
- **outputs**: Memory usage report
- **dependencies**: [PERF-009]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Memory stable under sustained load

#### Task: PERF-017
- **title**: Test image optimization
- **description**: Verify images served in correct formats (WebP) with proper compression.
- **inputs**: Image assets, image optimization config
- **outputs**: Image optimization test report
- **dependencies**: []
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Images optimized and served in WebP format

#### Task: PERF-018
- **title**: Test lazy loading
- **description**: Verify off-screen images and components lazy load correctly.
- **inputs**: Lazy loading implementation
- **outputs**: Lazy loading test report
- **dependencies**: []
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Images below fold load on scroll

#### Task: PERF-019
- **title**: Test cache effectiveness
- **description**: Verify caching headers set correctly and assets cached by browser.
- **inputs**: Cache headers, CDN config
- **outputs**: Cache effectiveness report
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Static assets cached with long TTL

#### Task: PERF-020
- **title**: Test third-party script impact
- **description**: Measure impact of third-party scripts (Stripe, analytics) on page load time.
- **inputs**: Script loading, performance timeline
- **outputs**: Third-party impact report
- **dependencies**: [PERF-001]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Third-party scripts don't block main thread

---

### Category: Security Testing (SQL Injection, XSS, CSRF)

#### Task: SEC-001
- **title**: Set up security scanning tools
- **description**: Configure OWASP ZAP and npm audit for automated security scanning.
- **inputs**: OWASP ZAP, security tools
- **outputs**: Security scan configuration
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Security tools run and produce reports

#### Task: SEC-002
- **title**: SQL injection testing on all inputs
- **description**: Test all user inputs for SQL injection vulnerabilities using common payloads.
- **inputs**: Input fields, SQL injection payloads
- **outputs**: SQL injection test report
- **dependencies**: [SEC-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: No SQL injection successful, inputs sanitized

#### Task: SEC-003
- **title**: XSS testing on all inputs
- **description**: Test all user inputs and output fields for cross-site scripting vulnerabilities.
- **inputs**: Input fields, XSS payloads
- **outputs**: XSS test report
- **dependencies**: [SEC-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: No XSS successful, output encoded

#### Task: SEC-004
- **title**: CSRF token validation
- **description**: Test that all state-changing operations require valid CSRF tokens.
- **inputs**: CSRF implementation, form submissions
- **outputs**: CSRF test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: CSRF attacks blocked, valid tokens accepted

#### Task: SEC-005
- **title**: Authentication bypass testing
- **description**: Test authentication mechanisms for bypass vulnerabilities.
- **inputs**: Auth endpoints, session handling
- **outputs**: Auth bypass test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: No auth bypass vulnerabilities found

#### Task: SEC-006
- **title**: Authorization/access control testing
- **description**: Test that users can only access their own data and role-based access enforced.
- **inputs**: User roles, permission system
- **outputs**: Authorization test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: Users can't access other users' data

#### Task: SEC-007
- **title**: Session management testing
- **description**: Test session fixation, session hijacking, and timeout handling.
- **inputs**: Session management, cookies
- **outputs**: Session test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Sessions properly secured and expire correctly

#### Task: SEC-008
- **title**: Password policy enforcement
- **description**: Test password requirements enforced (length, complexity, common passwords).
- **inputs**: Password validation, registration
- **outputs**: Password policy test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Weak passwords rejected

#### Task: SEC-009
- **title**: Input validation testing
- **description**: Test that all inputs properly validated server-side, not just client-side.
- **inputs**: Input validation, request fuzzing
- **outputs**: Input validation test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Invalid inputs rejected server-side

#### Task: SEC-010
- **title**: Sensitive data exposure testing
- **description**: Test that sensitive data not exposed in API responses, logs, or error messages.
- **inputs**: API responses, error messages
- **outputs**: Data exposure test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: No sensitive data leaked in responses

#### Task: SEC-011
- **title**: HTTPS/TLS enforcement
- **description**: Test that all traffic served over HTTPS and HSTS headers set correctly.
- **inputs**: HTTPS config, security headers
- **outputs**: HTTPS test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: HTTPS enforced, HSTS header set

#### Task: SEC-012
- **title**: Cookie security testing
- **description**: Test cookies have correct security flags (HttpOnly, Secure, SameSite).
- **inputs**: Cookie configuration
- **outputs**: Cookie security test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Cookies have all security flags set

#### Task: SEC-013
- **title**: Security header testing
- **description**: Test security headers (CSP, X-Frame-Options, X-Content-Type-Options) configured.
- **inputs**: Security headers, server config
- **outputs**: Security header test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: All security headers present

#### Task: SEC-014
- **title**: File upload vulnerability testing
- **description**: Test file uploads for path traversal, malicious files, and size limits.
- **inputs**: File upload endpoint, malicious files
- **outputs**: File upload test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Malicious uploads blocked, valid accepted

#### Task: SEC-015
- **title**: Rate limiting security testing
- **description**: Test rate limiting prevents brute force attacks on login and sensitive endpoints.
- **inputs**: Rate limiting, brute force attempts
- **outputs**: Rate limit test report
- **dependencies**: [INT-API-021]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Brute force blocked after threshold

#### Task: SEC-016
- **title**: JWT token security testing
- **description**: Test JWT tokens properly signed, not tampered, and expire correctly.
- **inputs**: JWT implementation, token manipulation
- **outputs**: JWT security test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Invalid/tampered tokens rejected

#### Task: SEC-017
- **title**: Dependency vulnerability scanning
- **description**: Run npm audit and Snyk to identify vulnerable dependencies.
- **inputs**: package.json, dependency scanner
- **outputs**: Dependency vulnerability report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: No high/critical vulnerabilities in dependencies

#### Task: SEC-018
- **title**: Error handling security testing
- **description**: Test that error messages don't expose stack traces or sensitive information.
- **inputs**: Error handling, error pages
- **outputs**: Error handling test report
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Errors show user-friendly messages only

#### Task: SEC-019
- **title**: CORS configuration testing
- **description**: Test CORS headers properly configured to allow only trusted origins.
- **inputs**: CORS configuration
- **outputs**: CORS test report
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: CORS allows only whitelisted origins

#### Task: SEC-020
- **title**: Webhook signature verification
- **description**: Test Stripe and other webhooks verify signatures correctly.
- **inputs**: Webhook handlers, signature verification
- **outputs**: Webhook security test report
- **dependencies**: [PAY-007]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Invalid webhook signatures rejected

#### Task: SEC-021
- **title**: Business logic vulnerability testing
- **description**: Test business logic edge cases (negative amounts, future dates, duplicate submissions).
- **inputs**: Business logic, edge cases
- **outputs**: Business logic test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: Business logic properly validates edge cases

---

### Category: Accessibility Testing (axe-core)

#### Task: A11Y-001
- **title**: Integrate axe-core with Playwright
- **description**: Configure axe-core accessibility testing in Playwright E2E tests.
- **inputs**: playwright-axe, test config
- **outputs**: Axe integration with Playwright
- **dependencies**: [E2E-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Axe runs in Playwright tests

#### Task: A11Y-002
- **title**: Accessibility audit on login page
- **description**: Run axe audit on login page and fix all critical and serious violations.
- **inputs**: Login page, axe report
- **outputs**: Accessibility report for login page
- **dependencies**: [A11Y-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Zero critical/serious violations on login page

#### Task: A11Y-003
- **title**: Accessibility audit on dashboard
- **description**: Run axe audit on dashboard and fix all critical and serious violations.
- **inputs**: Dashboard page, axe report
- **outputs**: Accessibility report for dashboard
- **dependencies**: [A11Y-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Zero critical/serious violations on dashboard

#### Task: A11Y-004
- **title**: Accessibility audit on client forms
- **description**: Run axe audit on client creation and edit forms.
- **inputs**: Client forms, axe report
- **outputs**: Accessibility report for client forms
- **dependencies**: [A11Y-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Zero critical/serious violations on client forms

#### Task: A11Y-005
- **title**: Accessibility audit on quote forms
- **description**: Run axe audit on quote creation and editing forms.
- **inputs**: Quote forms, axe report
- **outputs**: Accessibility report for quote forms
- **dependencies**: [A11Y-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Zero critical/serious violations on quote forms

#### Task: A11Y-006
- **title**: Accessibility audit on invoice forms
- **description**: Run axe audit on invoice generation and payment forms.
- **inputs**: Invoice forms, axe report
- **outputs**: Accessibility report for invoice forms
- **dependencies**: [A11Y-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Zero critical/serious violations on invoice forms

#### Task: A11Y-007
- **title**: Accessibility audit on calendar
- **description**: Run axe audit on calendar and appointment scheduling interfaces.
- **inputs**: Calendar page, axe report
- **outputs**: Accessibility report for calendar
- **dependencies**: [A11Y-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Zero critical/serious violations on calendar

#### Task: A11Y-008
- **title**: Keyboard navigation testing
- **description**: Test all interactive elements reachable and usable via keyboard only.
- **inputs**: Keyboard navigation tools
- **outputs**: Keyboard navigation test report
- **dependencies**: [A11Y-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: All functionality accessible via keyboard

#### Task: A11Y-009
- **title**: Screen reader compatibility testing
- **description**: Test with NVDA (Windows) and VoiceOver (macOS) screen readers.
- **inputs**: Screen reader software, testing checklist
- **outputs**: Screen reader compatibility report
- **dependencies**: [A11Y-001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: All content readable with screen readers

#### Task: A11Y-010
- **title**: Color contrast testing
- **description**: Test color contrast ratios meet WCAG AA (4.5:1 for text, 3:1 for large text).
- **inputs**: Color contrast analyzer, design
- **outputs**: Color contrast test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: All text meets contrast requirements

#### Task: A11Y-011
- **title**: Focus indicator visibility testing
- **description**: Verify focus indicators visible on all interactive elements.
- **inputs**: Focus styles, CSS
- **outputs**: Focus indicator test report
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Focus indicators clearly visible

#### Task: A11Y-012
- **title**: Form label association testing
- **description**: Verify all form inputs have properly associated labels.
- **inputs**: Form markup, accessibility inspector
- **outputs**: Form label test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: All inputs have associated labels

#### Task: A11Y-013
- **title**: Error message accessibility testing
- **description**: Test form error messages announced by screen readers and linked to inputs.
- **inputs**: Error messages, aria-live regions
- **outputs**: Error message accessibility test report
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Errors announced and linked to inputs

#### Task: A11Y-014
- **title**: ARIA landmark testing
- **description**: Verify page uses proper ARIA landmarks for navigation, main, and footer.
- **inputs**: ARIA landmarks, page structure
- **outputs**: ARIA landmark test report
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Proper landmarks present on all pages

#### Task: A11Y-015
- **title**: Skip navigation link testing
- **description**: Test skip navigation link present and functional for keyboard users.
- **inputs**: Skip link, navigation
- **outputs**: Skip link test report
- **dependencies**: [A11Y-008]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Skip link appears on focus and works

#### Task: A11Y-016
- **title**: Alt text for images testing
- **description**: Verify all images have appropriate alt text.
- **inputs**: Image assets, alt text
- **outputs**: Alt text test report
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: All images have alt text or empty alt if decorative

#### Task: A11Y-017
- **title**: Heading hierarchy testing
- **description**: Verify correct heading hierarchy (h1-h6) without skipping levels.
- **inputs**: Heading structure, page content
- **outputs**: Heading hierarchy test report
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: Headings follow logical hierarchy

#### Task: A11Y-018
- **title**: Mobile accessibility testing
- **description**: Test accessibility on mobile devices including touch targets and zoom.
- **inputs**: Mobile device testing, accessibility
- **outputs**: Mobile accessibility test report
- **dependencies**: [A11Y-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: QA
- **validation**: Touch targets 44x44px minimum, zoom works

#### Task: A11Y-019
- **title**: Reduced motion preference testing
- **description**: Test that animations respect prefers-reduced-motion media query.
- **inputs**: CSS animations, motion preferences
- **outputs**: Reduced motion test report
- **dependencies**: []
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Animations disabled when preference set

---

### Category: Cross-Device Testing

#### Task: DEVICE-001
- **title**: Test on iPhone Safari
- **description**: Test application on iPhone with Safari browser including PWA functionality.
- **inputs**: iPhone device or simulator
- **outputs**: iPhone Safari test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: App works correctly on iPhone Safari

#### Task: DEVICE-002
- **title**: Test on iPad Safari
- **description**: Test application on iPad with Safari including split view and keyboard.
- **inputs**: iPad device or simulator
- **outputs**: iPad Safari test report
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: App works correctly on iPad Safari

#### Task: DEVICE-003
- **title**: Test on Android Chrome
- **description**: Test application on Android device with Chrome including push notifications.
- **inputs**: Android device, Chrome
- **outputs**: Android Chrome test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: App works correctly on Android Chrome

#### Task: DEVICE-004
- **title**: Test on Samsung Internet
- **description**: Test application on Samsung Internet browser.
- **inputs**: Samsung device, Samsung Internet
- **outputs**: Samsung Internet test report
- **dependencies**: []
- **priority**: low
- **estimated_complexity**: high
- **agent_type**: QA
- **validation**: App works correctly on Samsung Internet

#### Task: DEVICE-005
- **title**: Test on Windows Chrome
- **description**: Test application on Windows with Chrome browser.
- **inputs**: Windows PC, Chrome
- **outputs**: Windows Chrome test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: App works correctly on Windows Chrome

#### Task: DEVICE-006
- **title**: Test on Windows Firefox
- **description**: Test application on Windows with Firefox browser.
- **inputs**: Windows PC, Firefox
- **outputs**: Windows Firefox test report
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: App works correctly on Windows Firefox

#### Task: DEVICE-007
- **title**: Test on macOS Safari
- **description**: Test application on macOS with Safari browser.
- **inputs**: Mac device, Safari
- **outputs**: macOS Safari test report
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: QA
- **validation**: App works correctly on macOS Safari

#### Task: DEVICE-008
- **title**: Test on macOS Chrome
- **description**: Test application on macOS with Chrome browser.
- **inputs**: Mac device, Chrome
- **outputs**: macOS Chrome test report
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: