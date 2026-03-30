# Frontend Roadmap — Mini-CRM

## Objectives

Build a mobile-first PWA frontend for a Mini-CRM targeting French solo artisans (plumbers, electricians, carpenters). The app enables artisans to manage contacts, jobs/devis (quotes), and invoices on the go. The UI must be dead-simple, work offline, feel native on mobile, and be fully localized in French.

## Subdomains

1. **Authentication** — Login, registration, password reset, session management
2. **Dashboard** — KPI overview, quick actions, recent activity
3. **Contacts** — CRUD for customer contacts with search/filter
4. **Jobs Pipeline** — Kanban board (Devis → Accepté → En cours → Terminé)
5. **Job Detail** — Full job view with line items, status, notes
6. **Invoices** — Invoice list, creation, PDF preview, sending
7. **Settings** — Profile, business info, pricing tier, preferences
8. **PWA/Native** — Service worker, offline mode, Capacitor iOS/Android
9. **Notifications** — Push notifications for job status changes, reminders
10. **Onboarding** — First-launch wizard for new users

## Milestones

- **M1: Foundation** — Project scaffold, design tokens, base components, routing
- **M2: Auth & Shell** — Login/register flows, app shell with navigation
- **M3: Core Screens** — Dashboard, Contacts, Jobs Pipeline, Job Detail
- **M4: Invoicing** — Invoice creation, list, PDF preview
- **M5: Settings & Profile** — User settings, business info, tier display
- **M6: PWA & Offline** — Service worker, offline data sync, manifest
- **M7: Native Mobile** — Capacitor iOS/Android build, push notifications
- **M8: Polish** — Animations, accessibility audit, i18n, performance

## Task Categories

---

### Category: Project Setup (Nuxt 3, TypeScript, Tailwind/CSS)

#### Task: FE-001
- **title**: Initialize Nuxt 3 project with TypeScript
- **description**: Create a new Nuxt 3 project using `npx nuxi init`, configure TypeScript strict mode, set up `nuxt.config.ts` with proper defaults. Install and configure TypeScript with strict type checking.
- **inputs**: Node.js 18+, npm/yarn/pnpm
- **outputs**: Working Nuxt 3 project with TypeScript enabled
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: `npx nuxi info` shows Nuxt 3 version, `tsc --noEmit` passes with zero errors

#### Task: FE-002
- **title**: Configure Tailwind CSS v4 with Nuxt
- **description**: Install Tailwind CSS v4 via `@nuxtjs/tailwindcss` module, configure `tailwind.config.ts` with the project's color palette, extend theme with custom tokens (brand colors, spacing scale, border radius). Set up CSS custom properties for design tokens.
- **inputs**: Nuxt 3 project, Tailwind CSS v4 package
- **outputs**: Tailwind configured with custom theme tokens
- **dependencies**: [FE-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Tailwind utilities work in components, custom colors accessible via CSS variables

#### Task: FE-003
- **title**: Set up @nuxtjs/google-fonts
- **description**: Install and configure @nuxtjs/google-fonts to load fonts appropriate for French artisans — clean, readable sans-serif (e.g., Inter for UI). Configure font-display: swap.
- **inputs**: Nuxt project, Google Fonts module
- **outputs**: Fonts loaded via link tags with preconnect
- **dependencies**: [FE-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Fonts visible in devtools network tab, no FOUT on load

#### Task: FE-004
- **title**: Configure Pinia for state management
- **description**: Install Pinia (`@pinia/nuxt`), configure the Pinia module in nuxt.config.ts. Set up typed stores for auth, contacts, jobs, invoices, and settings. Create composables for accessing each store.
- **inputs**: Nuxt project, Pinia package
- **outputs**: Configured Pinia with typed stores
- **dependencies**: [FE-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Stores accessible via `useStore()`, TypeScript inference works

#### Task: FE-005
- **title**: Set up Nuxt i18n module with French locale
- **description**: Install `@nuxtjs/i18n`, configure French as default locale, set up locale files in `locales/fr.json`. Configure module to auto-import translation helpers.
- **inputs**: Nuxt project, @nuxtjs/i18n package
- **outputs**: i18n configured, French translations available
- **dependencies**: [FE-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: `useI18n()` works in components, French text renders correctly

#### Task: FE-006
- **title**: Configure @nuxt/image for optimized images
- **description**: Install `@nuxt/image`, configure image providers for avatars, logos, and product images. Set up automatic WebP/AVIF conversion and responsive srcsets.
- **inputs**: Nuxt project, @nuxt/image package
- **outputs**: Image optimization configured
- **dependencies**: [FE-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: `<NuxtImg>` component works with lazy loading and srcset

#### Task: FE-007
- **title**: Set up VueUse for composables
- **description**: Install `@vueuse/nuxt` and `@vueuse/core`. Configure auto-imports for common composables like `useLocalStorage`, `useDark`, `useSwipe`, `useOnline`.
- **inputs**: Nuxt project, VueUse packages
- **outputs**: VueUse composables auto-imported
- **dependencies**: [FE-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: composables like `useLocalStorage` work without imports

#### Task: FE-008
- **title**: Configure ESLint and Prettier for code quality
- **description**: Set up ESLint with `@nuxt/eslint` module, configure Prettier for consistent formatting. Add Husky pre-commit hook to run linting. Configure rules for Vue 3 Composition API style.
- **inputs**: Nuxt project, ESLint/Prettier packages
- **outputs**: Lint and format scripts configured
- **dependencies**: [FE-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: `npm run lint` passes, `npm run format` formats code

#### Task: FE-009
- **title**: Set up Vitest for unit testing
- **description**: Install Vitest, configure for Vue/Nuxt testing. Write tests for utility functions, composables, and store actions. Set up coverage reporting.
- **inputs**: Nuxt project, Vitest package
- **outputs**: Vitest configured with test scripts
- **dependencies**: [FE-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: `npm run test` runs tests, coverage report generated

#### Task: FE-010
- **title**: Create app.config.ts for feature flags
- **description**: Create `app.config.ts` for environment-specific settings: API URL, feature flags for pricing tiers (Basic/Pro/Premium), offline mode toggle, push notification config.
- **inputs**: Nuxt project
- **outputs**: Typed app config with feature flags
- **dependencies**: [FE-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: `useAppConfig()` returns typed config in components

#### Task: FE-011
- **title**: Set up environment variable schema with zod
- **description**: Install `zod` and create a runtime config schema using Nuxt's `runtimeConfig` with proper TypeScript types. Document required env vars: API_BASE_URL, database connection string, NUXT_PUBLIC_* vars.
- **inputs**: Nuxt project, zod package
- **outputs**: Typed runtime config with validation
- **dependencies**: [FE-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Missing env vars cause clear errors at startup, not at runtime

#### Task: FE-012
- **title**: Configure Nuxt routing structure
- **description**: Set up the `pages/` directory structure: `/`, `/login`, `/register`, `/dashboard`, `/contacts`, `/contacts/:id`, `/jobs`, `/jobs/:id`, `/jobs/:id/invoice`, `/invoices`, `/invoices/:id`, `/settings`. Configure nested layouts for authenticated/unauthenticated routes.
- **inputs**: Nuxt project
- **outputs**: Pages directory with all routes scaffolded
- **dependencies**: [FE-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: All routes accessible, navigating to undefined route shows 404

#### Task: FE-013
- **title**: Set up Nuxt layout system
- **description**: Create `layouts/default.vue` (app shell with bottom nav), `layouts/auth.vue` (minimal centered layout for login/register), `layouts/blank.vue` (empty for PDFs/modals). Configure route middleware to enforce auth layout.
- **inputs**: Nuxt project, pages directory
- **outputs**: Layout files and middleware configured
- **dependencies**: [FE-012]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Auth routes use auth layout, app routes use default layout with nav

#### Task: FE-014
- **title**: Create TypeScript types for domain models
- **description**: Create `types/` directory with interfaces for User, Contact, Job, JobStatus, Invoice, InvoiceLineItem, BusinessProfile, PricingTier. Use discriminated unions for JobStatus. Export from `types/index.ts`.
- **inputs**: Nuxt project, domain knowledge
- **outputs**: Full TypeScript type definitions
- **dependencies**: [FE-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: No `any` types in store or component props, full type inference

#### Task: FE-015
- **title**: Set up API composables layer
- **description**: Create `composables/useApi.ts` with typed fetch wrappers for all API endpoints. Implement retry logic, JWT token attachment, and error normalization. Create specific composables: `useContactsApi`, `useJobsApi`, `useInvoicesApi`.
- **inputs**: Nuxt project, TypeScript types
- **outputs**: Typed API composables with error handling
- **dependencies**: [FE-014]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: fullstack
- **validation**: API calls typed, errors return structured { message, code } objects

#### Task: FE-016
- **title**: Configure git hooks with lint-staged
- **description**: Set up `lint-staged` to run ESLint and Prettier only on staged files. Configure Husky for pre-commit and pre-push hooks. Ensure no unlinted code enters the repository.
- **inputs**: Nuxt project, git repository
- **outputs**: Git hooks running lint on commit
- **dependencies**: [FE-008]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Commit fails if lint errors exist, passes with clean lint

#### Task: FE-017
- **title**: Set up Storybook for component development
- **description**: Install and configure Storybook for Vue 3/Nuxt 3. Create stories for all base components (Button, Input, Card, Modal, Badge). Configure Tailwind integration in Storybook.
- **inputs**: Nuxt project, Storybook packages
- **outputs**: Storybook running with component stories
- **dependencies**: [FE-002]
- **priority**: low
- **estimated_complexity**: high
- **agent_type**: frontend
- **validation**: `npm run storybook` starts Storybook dev server

#### Task: FE-018
- **title**: Create design token CSS variables file
- **description**: Create `assets/css/tokens.css` with CSS custom properties for all design tokens: colors (primary, secondary, success, warning, error, neutral), spacing scale, typography scale, border radius, shadows, z-index scale. Reference these in Tailwind config.
- **inputs**: Design specifications, CSS knowledge
- **outputs**: tokens.css file with all CSS variables
- **dependencies**: [FE-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Changing a CSS variable updates all components using it

#### Task: FE-019
- **title**: Set up Docker/docker-compose for local development
- **description**: Create Dockerfile for the Nuxt frontend with multi-stage build (dev + production). Create docker-compose.yml that spins up Nuxt dev server + Postgres + Mailpit for local email testing.
- **inputs**: Docker, docker-compose
- **outputs**: Docker configuration for local dev
- **dependencies**: []
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: fullstack
- **validation**: `docker-compose up` starts all services, app accessible on localhost

#### Task: FE-020
- **title**: Configure Playwright for E2E testing
- **description**: Install Playwright, configure for Nuxt 3 E2E testing. Write tests for critical flows: login, create contact, create job, move job through pipeline, create invoice. Configure CI integration.
- **inputs**: Nuxt project, Playwright
- **outputs**: Playwright tests for E2E coverage
- **dependencies**: [FE-001, FE-012]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: frontend
- **validation**: Playwright tests run against dev server, all pass

---

### Category: Design System & Components

#### Task: FE-101
- **title**: Create Button component (primary, secondary, ghost, danger variants)
- **description**: Build a reusable `<BaseButton>` component with variants: primary (filled brand color), secondary (outlined), ghost (text only), danger (red). Support sizes: sm, md, lg. Support loading state with spinner. Support full-width prop. Use native `<button>` with proper type attribute.
- **inputs**: Design tokens, Vue 3 Composition API
- **outputs**: BaseButton component with all variants
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: All variants render correctly, loading spinner appears, disabled state works

#### Task: FE-102
- **title**: Create Input component with label, error, and helper text
- **description**: Build `<BaseInput>` component wrapping native input. Support types: text, email, password, tel, number, search. Support label above, helper text below, error message with red styling. Support prefix/suffix icons. Use `v-model` with proper types.
- **inputs**: Design tokens, form best practices
- **outputs**: BaseInput component with full validation display
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Input shows error state when `error` prop passed, label always visible

#### Task: FE-103
- **title**: Create Textarea component
- **description**: Build `<BaseTextarea>` component with auto-resize option, character counter, label, error, and helper text. Support rows prop for initial height.
- **inputs**: Design tokens
- **outputs**: BaseTextarea component
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Textarea auto-grows on input, character count updates live

#### Task: FE-104
- **title**: Create Select/Dropdown component
- **description**: Build `<BaseSelect>` component as a custom styled select. Support searchable option for long lists. Support option groups. Support clear button. Support loading state.
- **inputs**: Design tokens
- **outputs**: BaseSelect component with search and clear
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Dropdown opens on click, search filters options, selection closes dropdown

#### Task: FE-105
- **title**: Create Checkbox and Toggle components
- **description**: Build `<BaseCheckbox>` with label, indeterminate state for "select all". Build `<BaseToggle>` as a sliding toggle switch for boolean settings. Both must be keyboard accessible.
- **inputs**: Design tokens, a11y requirements
- **outputs**: BaseCheckbox and BaseToggle components
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Toggle slides smoothly, both respond to Space key, focus ring visible

#### Task: FE-106
- **title**: Create Card component with header, body, footer slots
- **description**: Build `<BaseCard>` component with card title slot, default slot for body, footer slot. Support `flat` and `bordered` variants. Support `clickable` prop for card-as-button pattern with hover state.
- **inputs**: Design tokens
- **outputs**: BaseCard component
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Card renders with header/body/footer sections, clickable variant shows hover state

#### Task: FE-107
- **title**: Create Badge/Pill component for status indicators
- **description**: Build `<BaseBadge>` component with variants: default, success, warning, error, info. Support size sm/md. Used for job status, invoice status, pricing tier badges throughout the app.
- **inputs**: Design tokens
- **outputs**: BaseBadge component
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Badge colors match status semantics (green=success, yellow=warning, etc.)

#### Task: FE-108
- **title**: Create Modal/Dialog component
- **description**: Build `<BaseModal>` component with Teleport to body. Support header with title and close button, body slot, footer slot. Support size variants: sm (400px), md (500px), lg (700px), full. Support backdrop click to close. Trap focus within modal. Close on Escape key.
- **inputs**: Design tokens, a11y requirements
- **outputs**: BaseModal component
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Focus trapped in modal, Escape closes, backdrop click closes

#### Task: FE-109
- **title**: Create Alert/Toast notification component
- **description**: Build `<BaseAlert>` for inline alerts (success, error, warning, info) and `<Toast>` component for transient notifications. Toast should auto-dismiss after 4 seconds, support manual dismiss. Implement toast queue for multiple simultaneous toasts.
- **inputs**: Design tokens
- **outputs**: BaseAlert and Toast components
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Toast appears, auto-dismisses, stacking works for multiple toasts

#### Task: FE-110
- **title**: Create Avatar component
- **description**: Build `<BaseAvatar>` component displaying initials fallback when no image provided. Support sizes: xs (24px), sm (32px), md (40px), lg (64px). Support rounded (circle) and square variants. Use `<img>` with loading="lazy".
- **inputs**: Design tokens
- **outputs**: BaseAvatar component with initials fallback
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Avatar shows initials when no image, correct size applied

#### Task: FE-111
- **title**: Create Dropdown Menu component
- **description**: Build `<BaseDropdown>` component for action menus (e.g., contact card actions). Support trigger slot, menu items with icons, dividers between groups. Support keyboard navigation with arrow keys.
- **inputs**: Design tokens
- **outputs**: BaseDropdown component
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Dropdown opens on click, keyboard navigable, closes on outside click

#### Task: FE-112
- **title**: Create Skeleton loader components
- **description**: Build skeleton components for cards, list items, avatars, text blocks. Use CSS animation for pulse effect. Create `<SkeletonCard>`, `<SkeletonList>`, `<SkeletonText>`, `<SkeletonAvatar>` components.
- **inputs**: Design tokens
- **outputs**: Skeleton components
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Skeletons show pulse animation, match layout of real content

#### Task: FE-113
- **title**: Create Bottom Sheet component for mobile
- **description**: Build `<BottomSheet>` component that slides up from bottom on mobile. Support drag-to-dismiss (swipe down). Support snap points (partial, full). Use Touch events for drag. Backdrop overlay.
- **inputs**: Design tokens, Touch events
- **outputs**: BottomSheet component
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: frontend
- **validation**: Sheet slides up smoothly, draggable, snap points work

#### Task: FE-114
- **title**: Create Tabs component
- **description**: Build `<BaseTabs>` with `<BaseTab>` children. Support scrollable tabs on mobile. Support underline and pill variants. Support lazy rendering of tab content (only mount when active).
- **inputs**: Design tokens
- **outputs**: BaseTabs component
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Tabs switch content on click, scrollable on overflow, underline indicator slides

#### Task: FE-115
- **title**: Create Pagination component
- **description**: Build `<BasePagination>` component for lists. Support page numbers with ellipsis for large sets. Support prev/next buttons. Support items per page selector. Emit `update:page` and `update:perPage` events.
- **inputs**: Design tokens
- **outputs**: BasePagination component
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Pagination renders correct page numbers, emits events on click

#### Task: FE-116
- **title**: Create Search Input component
- **description**: Build `<BaseSearch>` component extending BaseInput with search icon prefix, clear button suffix, and debounced `v-model`. Support `debounce` prop (default 300ms). Show loading spinner during search.
- **inputs**: BaseInput, VueUse composables
- **outputs**: BaseSearch component
- **dependencies**: [FE-102, FE-007]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Search debounced, clear button appears when text entered, loading state works

#### Task: FE-117
- **title**: Create Tag/Chip component for labels
- **description**: Build `<BaseTag>` component for removable labels (e.g., job categories). Support removable prop with X button. Support colored variants matching badge colors. Support clickable for filter interaction.
- **inputs**: Design tokens
- **outputs**: BaseTag component
- **dependencies**: [FE-018]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Tag shows remove X, clickable variant shows hover, colors work

#### Task: FE-118
- **title**: Create Divider component
- **description**: Build `<BaseDivider>` component as a horizontal or vertical separator. Support subtle and strong variants. Support spacing variants (no margin, with margin).
- **inputs**: Design tokens
- **outputs**: BaseDivider component
- **dependencies**: [FE-018]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Divider renders as thin line, vertical variant works

#### Task: FE-119
- **title**: Create Progress Bar and Progress Circle components
- **description**: Build `<BaseProgress>` linear bar and `<BaseProgressCircle>` SVG circle progress. Support determinate and indeterminate states. Support label display. Animate on value change.
- **inputs**: Design tokens
- **outputs**: BaseProgress and BaseProgressCircle components
- **dependencies**: [FE-018]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Progress animates smoothly, indeterminate state loops

#### Task: FE-120
- **title**: Create Empty State component
- **description**: Build `<EmptyState>` component with illustration slot, title, description, and action button. Create reusable illustrations for each domain (contacts empty, jobs empty, invoices empty). Use consistent empty state layout.
- **inputs**: Design tokens, SVG illustrations
- **outputs**: EmptyState component
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Empty state displays with illustration, action button navigates to create flow

#### Task: FE-121
- **title**: Create Confirmation Dialog component
- **description**: Build `<ConfirmDialog>` component extending BaseModal for destructive action confirmations. Support title, message, confirm button (danger style), cancel button. Return Promise for async usage.
- **inputs**: BaseModal, BaseButton
- **outputs**: ConfirmDialog component
- **dependencies**: [FE-108, FE-101]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Promise resolves on confirm, rejects on cancel, works with `await confirmDialog.show()`

#### Task: FE-122
- **title**: Create Stat Card component for Dashboard
- **description**: Build `<StatCard>` component displaying a single KPI: label, value (large), trend indicator (up/down arrow with percentage), and optional icon. Support comparison to previous period.
- **inputs**: Design tokens
- **outputs**: StatCard component
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Stat card shows value, trend arrow points correct direction, percentage displayed

#### Task: FE-123
- **title**: Create Action Menu (three-dot menu) component
- **description**: Build `<ActionMenu>` component for list item actions. Render three-dot icon trigger, dropdown menu with icon+label items. Support destructive item styling (red text). Positioned relative to trigger.
- **inputs**: BaseDropdown
- **outputs**: ActionMenu component
- **dependencies**: [FE-111]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Three dots visible, menu opens on click, items trigger correct actions

#### Task: FE-124
- **title**: Create FormField wrapper component
- **description**: Build `<FormField>` wrapper that combines label, input slot, error message, and helper text into a single component. Reduces boilerplate in forms. Automatically associates label with input via for/id.
- **inputs**: BaseInput components
- **outputs**: FormField component
- **dependencies**: [FE-102]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: FormField renders label above input, error below, accessibility associations correct

#### Task: FE-125
- **title**: Create Responsive Image component
- **description**: Build `<ResponsiveImage>` component wrapping NuxtImg with placeholder blur-up effect. Support aspect ratio box to prevent layout shift. Support lazy loading with intersection observer.
- **inputs**: Nuxt Image module
- **outputs**: ResponsiveImage component
- **dependencies**: [FE-006]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Images load with blur-up, no layout shift, lazy loads when off-screen

#### Task: FE-126
- **title**: Create Rating/Stars component
- **description**: Build `<StarRating>` component for reviews/feedback. Support readonly and interactive modes. Support half-star precision. Support size variants. Emit rating value on interaction.
- **inputs**: Design tokens
- **outputs**: StarRating component
- **dependencies**: [FE-018]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Stars fill on hover/interaction, half-star displays correctly, emits value

#### Task: FE-127
- **title**: Create Chip Input (tag input) component
- **description**: Build `<ChipInput>` component for multi-value input (e.g., job tags). Support typing + Enter to add chips, X to remove. Support paste multiple values. Autocomplete suggestions.
- **inputs**: Design tokens
- **outputs**: ChipInput component
- **dependencies**: [FE-018]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: frontend
- **validation**: Chips appear on Enter, removed on X click, paste adds multiple chips

#### Task: FE-128
- **title**: Create Color Picker component
- **description**: Build `<ColorPicker>` component for customizing invoice colors, category colors. Support preset swatches and custom hex input. Return hex value.
- **inputs**: Design tokens
- **outputs**: ColorPicker component
- **dependencies**: [FE-018]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Color picker opens, swatches selectable, custom color input works

#### Task: FE-129
- **title**: Create Date Picker component
- **description**: Build `<DatePicker>` component for selecting dates (job dates, invoice due dates). Support single date, date range modes. Support French locale formatting (DD/MM/YYYY). Calendar grid view with month navigation.
- **inputs**: Design tokens, date library (date-fns or dayjs)
- **outputs**: DatePicker component
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: frontend
- **validation**: Calendar opens, date selectable, French format displayed

#### Task: FE-130
- **title**: Create Icon component with Heroicons or Lucide
- **description**: Set up Heroicons (or Lucide) as SVG icon library. Create `<Icon>` component that accepts icon name and renders the correct SVG. Support size and color props. Tree-shake unused icons.
- **inputs**: Heroicons/Lucide package
- **outputs**: Icon component
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Icons render at correct size, color inherits from parent

#### Task: FE-131
- **title**: Create List Item component
- **description**: Build `<ListItem>` component for contact lists, job lists. Support avatar/icon left, title, subtitle, optional right accessory (chevron, badge, action menu). Support swipe actions on mobile (delete, edit).
- **inputs**: Design tokens, VueUse gestures
- **outputs**: ListItem component
- **dependencies**: [FE-110, FE-007]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: ListItem renders in list, swipe reveals actions

#### Task: FE-132
- **title**: Create Phone/Email Link components
- **description**: Build `<PhoneLink>` and `<EmailLink>` components that render as styled links and trigger native phone/email apps on click. Support tel: and mailto: protocols. Show confirmation before action.
- **inputs**: Design tokens
- **outputs**: PhoneLink and EmailLink components
- **dependencies**: [FE-018]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Click triggers phone dialer or email client

#### Task: FE-133
- **title**: Create Stepper/Steps indicator component
- **description**: Build `<Stepper>` component for multi-step flows (e.g., invoice creation wizard). Support horizontal on desktop, vertical on mobile. Support completed, active, and pending states. Show step numbers or checkmarks.
- **inputs**: Design tokens
- **outputs**: Stepper component
- **dependencies**: [FE-018]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Steps show correct state, navigation between steps works

#### Task: FE-134
- **title**: Create Loading Spinner component
- **description**: Build `<Spinner>` component as a reusable loading indicator. Support size variants (sm, md, lg). Support inline (for buttons) and fullscreen (for page loads) modes. Use CSS animations, not GIFs.
- **inputs**: Design tokens, CSS animations
- **outputs**: Spinner component
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Spinner animates smoothly, sizes work in different contexts

#### Task: FE-135
- **title**: Create Money/Currency formatted display component
- **description**: Build `<Money>` component for formatting currency values (EUR). Support input as number, format as French locale (1 234,56 €). Support color for positive/negative values. Support inline and block display.
- **inputs**: French locale knowledge
- **outputs**: Money component
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Values formatted correctly with € symbol and French number format

---

### Category: Layout & Navigation (mobile-first, bottom nav, sidebar)

#### Task: FE-201
- **title**: Create app shell with bottom navigation bar
- **description**: Create the main app shell `AppShell.vue` with bottom navigation bar. Include 5 tabs: Tableau de bord (dashboard), Contacts, Travaux (jobs), Factures (invoices), Paramètres (settings). Use Vue Router for tab switching. Active tab highlighted with brand color and label visible.
- **inputs**: Design tokens, icon components
- **outputs**: App shell with bottom nav
- **dependencies**: [FE-130, FE-007]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Bottom nav visible on mobile, 5 tabs with icons and labels, active state clear

#### Task: FE-202
- **title**: Implement bottom nav safe area insets
- **description**: Use CSS `env(safe-area-inset-bottom)` to add padding for notched devices (iPhone X+). Ensure bottom nav doesn't overlap home indicator. Apply to all pages using the default layout.
- **inputs**: Safe area knowledge, CSS custom properties
- **outputs**: Bottom nav with safe area padding
- **dependencies**: [FE-201]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Bottom nav accounts for home indicator on iPhone X simulator

#### Task: FE-203
- **title**: Create mobile-first responsive header
- **description**: Create `AppHeader.vue` with page title (dynamic), optional back button (when nested), and optional right action slot (search, add button). Back button uses `useRouter().back()` or navigation guard history. Title truncates with ellipsis on long names.
- **inputs**: Vue Router, design tokens
- **outputs**: AppHeader component
- **dependencies**: [FE-201]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Header shows correct title per page, back button works, right slot renders

#### Task: FE-204
- **title**: Implement mobile swipe gestures for navigation
- **