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
- **description**: Use VueUse `useSwipe` composable to implement swipe-back gesture on iOS (swipe from left edge to go back). Also implement swipe between tabs. Ensure gestures don't conflict with scroll content.
- **inputs**: VueUse composables
- **outputs**: Swipe gesture navigation
- **dependencies**: [FE-007, FE-202]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Swipe-back navigates to previous page, doesn't conflict with list scrolling

#### Task: FE-205
- **title**: Create sidebar navigation for desktop (md+ breakpoint)
- **description**: Transform bottom nav into left sidebar on desktop (min-width: 768px). Sidebar shows full labels and larger icons. Collapsible to icon-only mode. Top section for logo/business name, bottom for settings.
- **inputs**: Design tokens, CSS media queries
- **outputs**: Responsive sidebar for desktop
- **dependencies**: [FE-201]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Sidebar visible on desktop, collapses to icons, bottom nav hidden

#### Task: FE-206
- **title**: Create page transition animations
- **description**: Implement smooth page transitions using Vue Transition component. Configure different transitions for forward/back navigation (slide left/right). Configure fade transition for modal-like pages.
- **inputs**: Vue Transition, CSS animations
- **outputs**: Page transitions
- **dependencies**: [FE-012]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Pages slide smoothly, no flash of unstyled content

#### Task: FE-207
- **title**: Implement scroll behavior and sticky headers
- **description**: Configure Vue Router scroll behavior to remember scroll position per route. Make page headers sticky on scroll with shadow appearing when scrolled. Use Intersection Observer for header shadow.
- **inputs**: Vue Router config
- **outputs**: Scroll behavior with sticky headers
- **dependencies**: [FE-203]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Scroll position restored on back navigation, header shows shadow when scrolled

#### Task: FE-208
- **title**: Create FAB (Floating Action Button) component
- **description**: Create `FloatingActionButton` positioned bottom-right (above bottom nav on mobile). Primary action per context: "+" on contacts list, "+" on jobs list, "+" on invoices. Animate in on mount. Support expanded state with sub-actions.
- **inputs**: Design tokens
- **outputs**: FAB component
- **dependencies**: [FE-201]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: FAB visible above bottom nav, animates on mount, primary action works

#### Task: FE-209
- **title**: Implement tab bar badge/notification indicators
- **description**: Add badge indicators to bottom nav tabs showing counts (e.g., unread notifications on dashboard). Use `<BaseBadge>` with small dot or count. Support dynamic count updates via Pinia store.
- **inputs**: BaseBadge, Pinia stores
- **outputs**: Badge indicators on nav tabs
- **dependencies**: [FE-107, FE-201, FE-004]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Badges appear with correct counts, update when data changes

#### Task: FE-210
- **title**: Create pull-to-refresh functionality
- **description**: Implement pull-to-refresh on list screens (contacts, jobs, invoices) using Touch events and VueUse `useSwipe`. Show spinner at top while refreshing. Haptic feedback on mobile (if supported).
- **inputs**: VueUse, Touch events
- **outputs**: Pull-to-refresh on list screens
- **dependencies**: [FE-007]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Pull gesture triggers refresh, spinner shows, content reloads

#### Task: FE-211
- **title**: Create breadcrumb navigation for nested pages
- **description**: Implement breadcrumb trail for nested routes (e.g., Dashboard > Contacts > John Doe > Edit). Render as clickable links above page content. Hide on top-level pages.
- **inputs**: Vue Router, design tokens
- **outputs**: Breadcrumb component
- **dependencies**: [FE-203]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Breadcrumbs show correct hierarchy, links navigate correctly

#### Task: FE-212
- **title**: Implement keyboard navigation (Tab, Enter, Escape)
- **description**: Ensure full keyboard navigability throughout the app. Tab order should follow visual order. Enter activates buttons/links. Escape closes modals/dropdowns. Visible focus rings on all interactive elements.
- **inputs**: a11y requirements
- **outputs**: Full keyboard navigation support
- **dependencies**: [FE-108, FE-111]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: All interactions achievable via keyboard, focus visible at all times

#### Task: FE-213
- **title**: Create mobile keyboard-aware layout adjustments
- **description**: Detect mobile keyboard open via `visualViewport` API. Adjust layout to keep focused input visible above keyboard. Scroll content into view automatically.
- **inputs**: VisualViewport API
- **outputs**: Keyboard-aware layout
- **dependencies**: [FE-102]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Input stays visible when keyboard opens on mobile

#### Task: FE-214
- **title**: Implement skeleton loading for all data-fetching screens
- **description**: Wrap all list screens and detail screens with skeleton loaders while data fetches. Use skeleton components from FE-112. Show skeletons for minimum 300ms to prevent flash.
- **inputs**: Skeleton components, data fetching composables
- **outputs**: Skeleton loaders on all data screens
- **dependencies**: [FE-112, FE-015]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Skeletons display while loading, real content replaces after load

#### Task: FE-215
- **title**: Create layout for form pages
- **description**: Create a dedicated form layout `FormLayout.vue` with consistent spacing for all create/edit forms. Center content on desktop, full-width on mobile. Include cancel/submit button footer area.
- **inputs**: Design tokens
- **outputs**: Reusable form layout
- **dependencies**: [FE-018]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Forms use consistent layout, buttons at bottom, proper spacing

#### Task: FE-216
- **title**: Implement responsive grid for desktop data tables
- **description**: Transform list views from stacked mobile cards to table grid on desktop (lg+). Columns: name, status, date, amount. Sortable columns. Sticky header row.
- **inputs**: Design tokens, Vue table library or custom
- **outputs**: Responsive data table
- **dependencies**: [FE-205]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: frontend
- **validation**: Tables display on desktop, cards on mobile, same data source

#### Task: FE-217
- **title**: Create print-specific stylesheet
- **description**: Create `print.css` with styles for printing invoices and job details. Hide navigation, simplify layout, black text on white background. Optimize for A4 paper.
- **inputs**: Print media queries
- **outputs**: Print stylesheet
- **dependencies**: [FE-018]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Print preview shows clean layout, no nav elements

---

### Category: Authentication UI (login, register, password reset)

#### Task: FE-301
- **title**: Create login page with email/password form
- **description**: Build `/login` page with email and password fields, login button, "Mot de passe oublié?" (forgot password) link, and "Créer un compte" (create account) link. Form validation: email required/format, password required (min 8 chars). Show loading state on submit. Redirect to /dashboard on success.
- **inputs**: Design system components, auth store
- **outputs**: Login page
- **dependencies**: [FE-101, FE-102, FE-004]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Form validates, submits to API, redirects on success, shows errors

#### Task: FE-302
- **title**: Create registration page
- **description**: Build `/register` page with full name, email, password, and confirm password fields. Show password strength indicator. Terms of service checkbox (required). "Déjà un compte?" (already have account) link. Redirect to onboarding on success.
- **inputs**: Design system components, auth store
- **outputs**: Registration page
- **dependencies**: [FE-101, FE-102, FE-004]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Form validates, passwords match, submits, redirects to onboarding

#### Task: FE-303
- **title**: Create password reset request page
- **description**: Build `/forgot-password` page with email field only. Show success message after submission ("Email envoyé"). Include "Retour à la connexion" (back to login) link.
- **inputs**: Design system components
- **outputs**: Password reset request page
- **dependencies**: [FE-101, FE-102]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Email validates, success message shows after submit

#### Task: FE-304
- **title**: Create password reset new password page
- **description**: Build `/reset-password` page (accessed via email link) with new password and confirm password fields. Extract token from URL query params. Show success and redirect to login after reset.
- **inputs**: Design system components, auth store
- **outputs**: Password reset new password page
- **dependencies**: [FE-101, FE-102]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Token extracted from URL, form submits, redirects to login

#### Task: FE-305
- **title**: Implement auth store with login/logout/register actions
- **description**: Create Pinia `useAuthStore` with user state, login(), logout(), register(), forgotPassword(), resetPassword() actions. Persist auth token to localStorage. Include currentUser getter. Handle token expiration.
- **inputs**: Pinia, auth API composable
- **outputs**: Auth store with full auth logic
- **dependencies**: [FE-004, FE-015]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Auth state persists across page reloads, logout clears state

#### Task: FE-306
- **title**: Create route middleware for auth protection
- **description**: Create `middleware/auth.ts` that redirects unauthenticated users to /login. Create `middleware/guest.ts` that redirects authenticated users away from /login. Apply to appropriate routes in nuxt.config.
- **inputs**: Nuxt route middleware
- **outputs**: Auth guard middleware
- **dependencies**: [FE-013, FE-305]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Unauthenticated user redirected to login, authenticated user can't visit login

#### Task: FE-307
- **title**: Implement "Remember me" functionality
- **description**: Add "Se souvenir de moi" checkbox to login form. When checked, use persistent localStorage token. When unchecked, use session-only token that clears on browser close.
- **inputs**: Auth store, localStorage
- **outputs**: Remember me functionality
- **dependencies**: [FE-305]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Checkbox checked = token persists across browser close, unchecked = clears

#### Task: FE-308
- **title**: Create auth layout with centered card
- **description**: Build `layouts/auth.vue` with centered white card on brand-colored background. Include logo at top of card. Remove bottom nav. Minimal header with "Retour" link.
- **inputs**: Design tokens
- **outputs**: Auth layout
- **dependencies**: [FE-013]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Login/register pages centered, branded, mobile-friendly

#### Task: FE-309
- **title**: Implement session timeout warning
- **description**: When auth token near expiration (5 min before), show toast warning "Session expirera dans X minutes". Offer "Rester connecté" button to extend session. Auto-logout when expired.
- **inputs**: Auth store, token expiry logic
- **outputs**: Session timeout warning
- **dependencies**: [FE-305, FE-109]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Warning appears before expiry, extend button works, auto-logout at expiry

#### Task: FE-310
- **title**: Create social login buttons (Google, Apple)
- **description**: Add "Se connecter avec Google" and "Se connecter avec Apple" buttons to login page. Implement OAuth flow. Show buttons below primary form divider "ou".
- **inputs**: OAuth config, design tokens
- **outputs**: Social login buttons
- **dependencies**: [FE-301]
- **priority**: low
- **estimated_complexity**: high
- **agent_type**: fullstack
- **validation**: Social buttons render, OAuth flow initiates, user created on callback

#### Task: FE-311
- **title**: Implement logout confirmation dialog
- **description**: When user taps logout, show confirmation dialog "Êtes-vous sûr de vouloir vous déconnecter?" with "Se déconnecter" (danger) and "Annuler" buttons.
- **inputs**: ConfirmDialog, auth store
- **outputs**: Logout confirmation
- **dependencies**: [FE-121, FE-305]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Confirmation shows before logout, cancel returns to app

---

### Category: Dashboard Screen

#### Task: FE-401
- **title**: Create Dashboard page with KPI cards
- **description**: Build `/dashboard` page displaying 4 StatCards: "Travaux en cours" (jobs in progress), "Devis en attente" (pending quotes), "Factures à envoyer" (invoices to send), "Revenus du mois" (monthly revenue). Each card shows value, trend, and comparison to last month.
- **inputs**: StatCard component, dashboard store
- **outputs**: Dashboard with KPI cards
- **dependencies**: [FE-122, FE-004]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Dashboard loads with 4 stat cards, values animate on load

#### Task: FE-402
- **title**: Create recent activity feed on Dashboard
- **description**: Build "Activité récente" section showing last 10 activities (new contact added, job status changed, invoice sent). Each item shows icon, description, timestamp. Click navigates to relevant item.
- **inputs**: Activity types, timeline design
- **outputs**: Recent activity feed
- **dependencies**: [FE-130]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Activity feed shows recent items, timestamps relative (il y a 2h)

#### Task: FE-403
- **title**: Create Quick Actions section on Dashboard
- **description**: Build "Actions rapides" section with 4 buttons: "Nouveau contact" (new contact), "Nouveau devis" (new quote), "Nouvelle facture" (new invoice), "Voir les travaux" (view jobs). Grid layout, icons + labels.
- **inputs**: Design tokens, navigation
- **outputs**: Quick actions section
- **dependencies**: [FE-101, FE-130]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Quick actions navigate to correct pages, icons display

#### Task: FE-404
- **title**: Create "Upcoming jobs" widget
- **description**: Build "Travaux à venir" widget showing next 3 scheduled jobs with date, client name, job type, and status badge. "Voir tout" (see all) link to jobs list filtered by upcoming.
- **inputs**: Jobs store, card component
- **outputs**: Upcoming jobs widget
- **dependencies**: [FE-106, FE-107]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Shows next 3 jobs with correct dates, link filters jobs list

#### Task: FE-405
- **title**: Create Dashboard for pricing tier gating
- **description**: Show upgrade prompt on Dashboard when user is on Basic tier trying to access Pro features (e.g., more than 10 contacts). Use `<UpgradePrompt>` component with tier comparison.
- **inputs**: App config, user tier
- **outputs**: Tier-gated dashboard
- **dependencies**: [FE-010, FE-004]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Upgrade prompt appears when hitting tier limits

#### Task: FE-406
- **title**: Create Dashboard refresh on pull-to-refresh
- **description**: Add pull-to-refresh (FE-210) to Dashboard. Trigger dashboard data re-fetch. Show loading spinner at top while refreshing.
- **inputs**: Pull-to-refresh implementation
- **outputs**: Dashboard refresh on pull
- **dependencies**: [FE-210]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Pull-to-refresh works on Dashboard, data updates

#### Task: FE-407
- **title**: Implement Dashboard period selector
- **description**: Add period selector (Ce mois / Ce trimestre / Cette année) to Dashboard. KPIs and charts update based on selected period. Persist selection to localStorage.
- **inputs**: Period selector, date filtering
- **outputs**: Period selector on Dashboard
- **dependencies**: [FE-104]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Selector changes period, KPIs update, selection persists

#### Task: FE-408
- **title**: Create revenue chart on Dashboard
- **description**: Build SVG or canvas-based line chart showing revenue over selected period. Use chart library (Chart.js or similar). Show monthly data points, tooltips on hover/tap. Responsive sizing.
- **inputs**: Chart library, revenue data
- **outputs**: Revenue chart
- **dependencies**: [FE-407]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: frontend
- **validation**: Chart renders with data, tooltips work, responsive

#### Task: FE-409
- **title**: Create Dashboard skeleton loading state
- **description**: Show skeleton loaders (FE-112) on Dashboard while data fetches. Skeletons for stat cards (4), activity feed (3 items), quick actions (4 items), upcoming jobs (3 items).
- **inputs**: Skeleton components
- **outputs**: Dashboard skeleton loaders
- **dependencies**: [FE-112]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Skeletons display while loading, real content replaces

#### Task: FE-410
- **title**: Create empty Dashboard state for new users
- **description**: When user has no data yet, show welcoming empty state with illustration, "Bienvenue sur [AppName]!" message, and prominent "Créer votre premier client" button.
- **inputs**: EmptyState component
- **outputs**: New user Dashboard empty state
- **dependencies**: [FE-120]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Empty state shows for new users, CTA navigates to create contact

#### Task: FE-411
- **title**: Implement offline Dashboard display
- **description**: Cache Dashboard data in localStorage via service worker. When offline, show last cached data with "Hors ligne" banner. Show timestamp of last update.
- **inputs**: Offline composable, localStorage cache
- **outputs**: Offline Dashboard
- **dependencies**: [FE-701]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Offline shows cached data, banner indicates offline status

---

### Category: Contacts Screen (list, detail, add/edit)

#### Task: FE-501
- **title**: Create Contacts list page with search
- **description**: Build `/contacts` page with search bar at top (FE-116), sorted alphabetically by name. Show contact cards with avatar, name, phone, last job date. Pull-to-refresh enabled. Infinite scroll for pagination.
- **inputs**: Contacts store, list components
- **outputs**: Contacts list page
- **dependencies**: [FE-004, FE-116, FE-131]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Contacts list renders, search filters, infinite scroll works

#### Task: FE-502
- **title**: Create Contact detail page
- **description**: Build `/contacts/:id` page showing full contact info: avatar, name, phone (clickable), email (clickable), address, notes. Show "Travaux" section listing all jobs for this contact. Show "Factures" section with recent invoices. Action buttons: Edit, Delete.
- **inputs**: Contact data, jobs store, invoices store
- **outputs**: Contact detail page
- **dependencies**: [FE-131, FE-132]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Contact detail shows all info, related jobs/invoices listed, actions work

#### Task: FE-503
- **title**: Create Add/Edit Contact form page
- **description**: Build `/contacts/new` and `/contacts/:id/edit` pages with form fields: Prénom*, Nom*, Téléphone*, Email, Adresse (address fields: rue, code postal, ville), Notes (textarea). Use FormLayout. Validate on submit.
- **inputs**: Form components, form layout
- **outputs**: Add/Edit contact form
- **dependencies**: [FE-102, FE-103, FE-215]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Form validates required fields, saves to API, redirects to detail

#### Task: FE-504
- **title**: Create Contact search with filters
- **description**: Add filter panel to contacts list: filter by city (autocomplete), filter by last job date range, sort options (name A-Z, recently added, recently updated). Filters persist during session.
- **inputs**: Select components, date picker
- **outputs**: Contact filtering
- **dependencies**: [FE-104, FE-129]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Filters narrow results, multiple filters combine, sort changes order

#### Task: FE-505
- **title**: Create Contacts list empty state
- **description**: When no contacts exist, show EmptyState with illustration, "Aucun client pour le moment" message, and "Ajouter un client" button linking to /contacts/new.
- **inputs**: EmptyState component
- **outputs**: Contacts empty state
- **dependencies**: [FE-120]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Empty state displays when no contacts, button navigates to create

#### Task: FE-506
- **title**: Implement contact deletion with confirmation
- **description**: Add delete action to contact detail page. Show ConfirmDialog (FE-121) before deletion. On confirm, delete contact and redirect to /contacts with success toast.
- **inputs**: ConfirmDialog, contacts store
- **outputs**: Contact deletion flow
- **dependencies**: [FE-121, FE-109]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Delete shows confirmation, success toast on delete, redirects to list

#### Task: FE-507
- **title**: Create Contact import from phone contacts
- **description**: Implement "Importer des contacts" button that uses Capacitor Contacts API to access phone contacts. Show matching UI, let user select which to import. Duplicate detection by phone number.
- **inputs**: Capacitor Contacts plugin
- **outputs**: Contact import feature
- **dependencies**: [FE-801]
- **priority**: low
- **estimated_complexity**: high
- **agent_type**: mobile
- **validation**: Phone contacts accessed, selection imports, duplicates detected

#### Task: FE-508
- **title**: Create contact duplicate detection
- **description**: When adding contact, check for duplicates by phone or email. If found, show suggestion "Ce contact existe déjà: [Name]" with option to view existing or create anyway.
- **inputs**: Contacts API, duplicate detection logic
- **outputs**: Duplicate detection
- **dependencies**: [FE-503]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Duplicate detected and shown before save, option to merge or create new

#### Task: FE-509
- **title**: Create Contact notes with timestamps
- **description**: Add notes section to contact detail showing all notes with timestamps. Each note shows text, author (if multi-user), timestamp. "Ajouter une note" button opens textarea form.
- **inputs**: Contact detail page, notes data
- **outputs**: Contact notes section
- **dependencies**: [FE-502]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Notes display chronologically, new note saves with timestamp

#### Task: FE-510
- **title**: Create contact quick actions (call, SMS, email)
- **description**: On contact detail, add floating action row with 3 buttons: Appeler (phone icon), SMS (message icon), Email (mail icon). Each triggers native app with pre-filled recipient.
- **inputs**: Capacitor plugins, contact data
- **outputs**: Quick action buttons
- **dependencies**: [FE-502, FE-801]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: mobile
- **validation**: Call button opens dialer, SMS opens messages, Email opens mail client

#### Task: FE-511
- **title**: Create contact avatar upload
- **description**: Add avatar upload to contact form. Support camera and photo library (Capacitor Camera). Crop/rotate before save. Store as base64 or upload to storage. Show initials fallback if no avatar.
- **inputs**: Capacitor Camera, image upload
- **outputs**: Avatar upload
- **dependencies**: [FE-503, FE-801]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: mobile
- **validation**: Camera opens, photo selects, crop works, avatar saves

#### Task: FE-512
- **title**: Create Contact address with map integration
- **description**: Store full address fields for contact. Show "Voir sur la carte" link that opens native maps app with address. On desktop, show embedded map preview.
- **inputs**: Address fields, Capacitor Maps
- **outputs**: Map integration
- **dependencies**: [FE-502, FE-801]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: mobile
- **validation**: Address stored, maps link opens correct location

---

### Category: Jobs Pipeline/Kanban Screen (4 columns: Devis/Accepté/En cours/Terminé)

#### Task: FE-601
- **title**: Create Jobs Pipeline Kanban board
- **description**: Build `/jobs` page as Kanban board with 4 columns: "Devis" (quote, blue), "Accepté" (accepted, yellow), "En cours" (in progress, orange), "Terminé" (completed, green). Each column header shows count. Jobs displayed as draggable cards.
- **inputs**: Kanban board library (vue-draggable or similar)
- **outputs**: Kanban board
- **dependencies**: [FE-106, FE-107]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: frontend
- **validation**: 4 columns display, jobs draggable between columns

#### Task: FE-602
- **title**: Create Job card for Kanban
- **description**: Build `<JobCard>` component for Kanban display. Shows: client name, job title, date, amount (formatted EUR), status badge. Compact card size (150px height). Draggable handle. Click opens job detail.
- **inputs**: Design tokens, draggable library
- **outputs**: Job card
- **dependencies**: [FE-018]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Job card displays info, draggable, clickable

#### Task: FE-603
- **title**: Implement Kanban column scroll
- **description**: Make each Kanban column independently scrollable vertically. Horizontal scroll for entire board on mobile if needed. Column headers sticky at top while scrolling.
- **inputs**: CSS overflow, scroll handling
- **outputs**: Column scrolling
- **dependencies**: [FE-601]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Columns scroll independently, headers sticky

#### Task: FE-604
- **title**: Implement job drag-and-drop between columns
- **description**: Enable dragging job cards between Kanban columns. On drop, update job status in store and API. Optimistic UI update with rollback on error. Show toast "Statut mis à jour".
- **inputs**: Draggable library, jobs store
- **outputs**: Drag-drop status update
- **dependencies**: [FE-601, FE-602]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: frontend
- **validation**: Jobs drag between columns, status updates, toast confirms, rollback on error

#### Task: FE-605
- **title**: Create "Add Job" modal from Kanban
- **description**: When clicking "+" button in any Kanban column, open BottomSheet with job creation form. Pre-select the column as initial status. Fields: client (searchable select), title, description, estimated amount.
- **inputs**: BottomSheet, job form
- **outputs**: Add job modal
- **dependencies**: [FE-113, FE-104]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Modal opens, form submits, job appears in correct column

#### Task: FE-606
- **title**: Create Job search and filter panel
- **description**: Add filter bar above Kanban: search by client/job name, filter by date range, filter by amount range, filter by client. Filters apply to all columns. "Effacer les filtres" button resets.
- **inputs**: Search/filter components
- **outputs**: Job filtering
- **dependencies**: [FE-116, FE-104]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Filters narrow visible jobs, clear resets, filters persist during session

#### Task: FE-607
- **title**: Create column quick-add for jobs
- **description**: Add "+" button in each column header. Click opens job creation with that column pre-selected. Same as FE-605 but accessible per-column.
- **inputs**: Column headers, job creation
- **outputs**: Per-column quick add
- **dependencies**: [FE-605]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: + button in each column header, opens correct status pre-selected

#### Task: FE-608
- **title**: Create Kanban empty column state
- **description**: When a column has no jobs, show subtle dashed border placeholder with "Aucun travail" text. Encourage dropping jobs from other columns.
- **inputs**: Empty state styles
- **outputs**: Empty column state
- **dependencies**: [FE-601]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Empty column shows dashed placeholder, visible but not prominent

#### Task: FE-609
- **title**: Implement Kanban column collapse/expand
- **description**: Allow collapsing Kanban columns to just header (count only) to see overview. Collapsed columns show job count badge. Click header to expand. Persist collapse state.
- **inputs**: Collapsible panel logic
- **outputs**: Collapsible columns
- **dependencies**: [FE-601]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Columns collapse to header only, expand on click, state persists

#### Task: FE-610
- **title**: Create Kanban view toggle (board/list)
- **description**: Add toggle button to switch between Kanban board view and list view. List view shows all jobs in table with filters. Persist preference.
- **inputs**: View toggle, list view
- **outputs**: View toggle
- **dependencies**: [FE-601, FE-216]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Toggle switches between views, preference persists

#### Task: FE-611
- **title**: Create job count badges on tab bar
- **description**: Show badge counts on the Jobs tab in bottom nav showing total "En cours" jobs count. Update in real-time when jobs move through pipeline.
- **inputs**: Bottom nav, jobs store
- **outputs**: Tab bar job count
- **dependencies**: [FE-209, FE-004]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: frontend
- **validation**: Badge shows correct count, updates on job status change

#### Task: FE-612
- **title**: Implement offline Kanban board
- **description**: Cache jobs data locally for offline access. Show offline banner. Allow drag operations offline (queue for sync). On reconnect, sync queue to server and update board.
- **inputs**: Offline storage, sync queue
- **outputs**: Offline Kanban
- **dependencies**: [FE-701, FE-604]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: frontend
- **validation**: Kanban works offline, drag queues for sync, syncs on reconnect

---

### Category: Job Detail Screen

#### Task: FE-701
- **title**: Create Job detail page layout
- **description**: Build `/jobs/:id` page with full job information. Header with client name, job title, status badge (editable), and action menu. Sections: Description, Détails (date, amount, client info), Ligne de travaux (line items), Notes, Documents, Related invoices.
- **inputs**: Job data, layout structure
- **outputs**: Job detail page
- **dependencies**: [FE-106, FE-107]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Job detail shows all sections, information complete

#### Task: FE-702
- **title**: Create job status change component
- **description**: Build inline status changer on job detail. Current status shown as badge. Click opens BottomSheet with 4 options (Devis, Accepté, En cours, Terminé). Confirm changes status with toast.
- **inputs**: Status changer, BottomSheet
- **outputs**: Status change UI
- **dependencies**: [FE-113, FE-107]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Status changer opens, options selectable, status updates and shows toast

#### Task: FE-703
- **title**: Create job line items section
- **description**: Build "Ligne de travaux" section listing all line items for the job. Each item: description, quantity, unit price, total. Support adding/editing/removing items. Calculate job total automatically.
- **inputs**: Line item data, form components
- **outputs**: Line items section
- **dependencies**: [FE-102, FE-135]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: frontend
- **validation**: Line items display, add/edit