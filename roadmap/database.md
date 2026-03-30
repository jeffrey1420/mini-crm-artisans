# Database Roadmap — Mini-CRM

## Objectives

1. Establish a robust, secure, and performant PostgreSQL database infrastructure on OVH VPS for a multi-tenant Mini-CRM targeting French artisans
2. Design a comprehensive schema supporting users, organizations, contacts, jobs, invoices, and sales pipeline stages across three pricing tiers (€29/49/79/month)
3. Implement enterprise-grade security with Row-Level Security (RLS) policies ensuring complete data isolation between organizations
4. Build a foundation for full-text search in French using PostgreSQL's tsvector capabilities
5. Ensure business continuity through automated backups, point-in-time recovery, and disaster recovery procedures
6. Enable horizontal scalability through connection pooling and performance tuning
7. Support data portability via migration pathways from legacy CRM systems
8. Establish monitoring and alerting infrastructure for proactive database health management
9. Implement archive and retention policies compliant with French data protection regulations (CNPD)

## Subdomains

- **Authentication & Authorization**: User management, role-based access control, organization membership
- **Contact Management**: Lead and customer contact records, address book functionality
- **Job/Project Management**: Work orders, project tracking, status management
- **Financial Transactions**: Invoicing, payment tracking, financial reporting
- **Sales Pipeline**: Deal stages, opportunity tracking, conversion metrics
- **Search & Discovery**: Full-text search, filtering, and advanced queries
- **Data Governance**: Backup, archival, retention, and compliance

## Milestones

### Phase 1: Foundation (Weeks 1-4)
- PostgreSQL installation and initial configuration on OVH VPS
- Core schema design and implementation
- Initial migrations setup with Flyway
- Basic security policies implementation

### Phase 2: Core Features (Weeks 5-8)
- Complete schema implementation (users, organizations, contacts, jobs, invoices, pipeline_stages)
- Row-Level Security policies across all tables
- Connection pooling with PgBouncer
- Initial indexing strategy deployment

### Phase 3: Advanced Capabilities (Weeks 9-12)
- Full-text search implementation with French language support
- Advanced indexing and query optimization
- Comprehensive backup and restore procedures
- Monitoring and alerting setup

### Phase 4: Migration & Polish (Weeks 13-16)
- Legacy data migration tooling and procedures
- Performance tuning based on real-world usage
- Archive and retention policy implementation
- Final security audit and compliance review

## Task Categories

### Category: PostgreSQL Setup on OVH VPS

#### Task: db-ovh-001
- **title**: Create OVH VPS provisioning checklist
- **description**: Document all steps required to provision a new OVH VPS for PostgreSQL deployment including OS selection, network configuration, and initial server hardening
- **inputs**: OVH account credentials, VPS plan specifications
- **outputs**: Comprehensive provisioning checklist document
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Document covers all provisioning steps from account creation to base OS installation

#### Task: db-ovh-002
- **title**: Install PostgreSQL 16 on Ubuntu 22.04 OVH VPS
- **description**: Install PostgreSQL 16 from official PostgreSQL APT repository on Ubuntu 22.04 running on OVH VPS. Include necessary dependencies and verification steps
- **inputs**: SSH access to OVH VPS, Ubuntu 22.04 base installation
- **outputs**: PostgreSQL 16 installed and running, postgres user created
- **dependencies**: [db-ovh-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: `psql --version` returns 16.x, service status shows active

#### Task: db-ovh-003
- **title**: Configure PostgreSQL postgresql.conf for production
- **description**: Optimize postgresql.conf parameters for a Mini-CRM workload on OVH VPS including memory allocation (shared_buffers, effective_cache_size, work_mem), connection settings, and performance tuning specific to the VPS resource constraints
- **inputs**: OVH VPS RAM and CPU specifications, PostgreSQL 16 default postgresql.conf
- **outputs**: Modified postgresql.conf with optimized settings, original backed up
- **dependencies**: [db-ovh-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: PostgreSQL restarts successfully with new configuration, log shows no errors

#### Task: db-ovh-004
- **title**: Configure PostgreSQL pg_hba.conf for secure access
- **description**: Set up pg_hba.conf with appropriate authentication methods including peer authentication for local connections, scram-sha-256 for network connections, and rules for Nuxt 3 frontend server access
- **inputs**: Nuxt 3 server IP range, trusted local networks
- **outputs**: Updated pg_hba.conf with secure authentication rules
- **dependencies**: [db-ovh-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: `pg_hba.conf` reviewed, only allowed connections pass authentication test

#### Task: db-ovh-005
- **title**: Create separate tablespaces for different data types
- **description**: Create separate PostgreSQL tablespaces for tables, indexes, and temporary data to optimize I/O performance on OVH VPS storage
- **inputs**: PostgreSQL superuser access, available mount points on VPS
- **outputs**: Tablespaces: tbl_main, tbl_indexes, tbl_temp created and functional
- **dependencies**: [db-ovh-003]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Tablespace creation queries succeed, pg_tablespace shows new tablespaces

#### Task: db-ovh-006
- **title**: Set up automatic security updates for PostgreSQL
- **description**: Configure unattended-upgrades or similar mechanism to automatically apply PostgreSQL security updates on Ubuntu 22.04 OVH VPS
- **inputs**: Ubuntu 22.04 installation, PostgreSQL APT repository configured
- **outputs**: Automatic update configuration in place, test notification works
- **dependencies**: [db-ovh-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Unattended-upgrades package installed, configuration file exists

#### Task: db-ovh-007
- **title**: Configure firewall (UFW) for PostgreSQL access
- **description**: Set up UFW (Uncomplicated Firewall) on Ubuntu to allow PostgreSQL connections only from authorized sources (Nuxt 3 server IP, admin workstations)
- **inputs**: Authorized IP addresses for PostgreSQL access
- **outputs**: UFW configured and active, only allowed IPs can connect to port 5432
- **dependencies**: [db-ovh-004]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: `sudo ufw status` shows active, only approved rules present

#### Task: db-ovh-008
- **title**: Create DNS hostname for PostgreSQL server
- **description**: Configure a proper DNS A record or update /etc/hosts for the PostgreSQL server hostname to enable consistent connection strings across the application
- **inputs**: OVH VPS public IP, desired hostname (e.g., db.mini-crm.internal)
- **outputs**: DNS record created or /etc/hosts updated on all servers
- **dependencies**: [db-ovh-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: `nslookup` or `host` command resolves hostname to correct IP

#### Task: db-ovh-009
- **title**: Configure PostgreSQL logging for audit trail
- **description**: Set up PostgreSQL logging to capture connection attempts, query duration, slow queries (>100ms), and error conditions for security auditing and performance analysis
- **inputs**: postgresql.conf settings, log storage location
- **outputs**: PostgreSQL logging configured to rotate daily, capturing required events
- **dependencies**: [db-ovh-003]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Log files appear in designated directory, contain expected event types

#### Task: db-ovh-010
- **title**: Install and configure PostgreSQL extensions (pg_trgm, unaccent, hstore, uuid-ossp)
- **description**: Install required PostgreSQL extensions for the Mini-CRM: pg_trgm for fuzzy text matching, unaccent for French diacritic removal, hstore for flexible metadata, uuid-ossp for UUID generation
- **inputs**: PostgreSQL superuser access
- **outputs**: All extensions installed and available in public schema
- **dependencies**: [db-ovh-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: `SELECT * FROM pg_extension` shows all required extensions

#### Task: db-ovh-011
- **title**: Create database and initial schemas
- **description**: Create the main database (mini_crm) and establish initial schema structure including public schema for extensions and core schema for application tables
- **inputs**: PostgreSQL superuser access, database naming convention
- **outputs**: mini_crm database created, schemas established
- **dependencies**: [db-ovh-010]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: `SELECT datname FROM pg_database WHERE datname='mini_crm'` returns database name

#### Task: db-ovh-012
- **title**: Configure SSL/TLS for PostgreSQL connections
- **description**: Generate SSL certificates (self-signed for internal use or Let's Encrypt for production) and configure PostgreSQL to require SSL for all remote connections
- **inputs**: SSL certificate files, PostgreSQL configuration
- **outputs**: PostgreSQL SSL configured, connections fail without valid certificate
- **dependencies**: [db-ovh-004]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: `psql "sslmode=require"` succeeds, `sslmode=disable` connections rejected

#### Task: db-ovh-013
- **title**: Create dedicated PostgreSQL user for Nuxt 3 application
- **description**: Create a dedicated PostgreSQL role (app_user) with restricted permissions for the Nuxt 3 application to use, separate from administrative accounts
- **inputs**: PostgreSQL superuser access, desired role name
- **outputs**: app_user role created with CONNECT privilege on mini_crm database
- **dependencies**: [db-ovh-011]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: `SELECT rolname FROM pg_roles WHERE rolname='app_user'` returns app_user

#### Task: db-ovh-014
- **title**: Set up system-level resource limits for PostgreSQL
- **description**: Configure system-level limits (open files, processes, memory) in /etc/security/limits.conf and systemd service configuration for PostgreSQL to prevent resource exhaustion
- **inputs**: PostgreSQL service configuration, system resource availability
- **outputs**: PostgreSQL service file updated with appropriate ResourceLimits
- **dependencies**: [db-ovh-002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: `cat /proc/$(pgrep postgres)/limits` shows configured limits applied

#### Task: db-ovh-015
- **title**: Create PostgreSQL admin service account with limited sudo
- **description**: Create a dedicated Linux user (postgres_admin) for day-to-day PostgreSQL administration with limited sudo access for specific commands only (pg_ctl, pg_dump, pg_restore)
- **inputs**: Linux sudo access, PostgreSQL installation path
- **outputs**: postgres_admin user created with restricted sudo privileges
- **dependencies**: [db-ovh-002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: postgres_admin can run pg_ctl commands via sudo, cannot run other admin commands

#### Task: db-ovh-016
- **title**: Configure OVH VPS monitoring integration
- **description**: Set up server-level monitoring using available tools to track VPS resource usage (CPU, RAM, disk, network) and integrate with PostgreSQL process monitoring
- **inputs**: OVH VPS metrics API access, monitoring agent installation
- **outputs**: Monitoring agent installed and reporting VPS metrics
- **dependencies**: [db-ovh-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Monitoring dashboard shows VPS resource graphs updating in real-time

#### Task: db-ovh-017
- **title**: Create connection script for database administration
- **description**: Create a ~/bin/pg-connect script that provides convenient database connections with appropriate environment variables and SSL settings pre-configured
- **inputs**: Database host, port, user configurations
- **outputs**: Executable pg-connect script in ~/bin/ directory
- **dependencies**: [db-ovh-013]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Script executes and opens psql session with correct parameters

#### Task: db-ovh-018
- **title**: Document OVH VPS PostgreSQL architecture
- **description**: Create architecture documentation covering server specifications, PostgreSQL configuration decisions, storage layout, and network topology for the Mini-CRM database infrastructure
- **inputs**: All previous configuration decisions, server specifications
- **outputs**: Architecture diagram and documentation in markdown format
- **dependencies**: [db-ovh-005, db-ovh-008, db-ovh-011]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Documentation exists and covers all major infrastructure components

#### Task: db-ovh-019
- **title**: Configure PostgreSQL for remote administration
- **description**: Ensure PostgreSQL is configured to accept remote connections for administration purposes while maintaining security through pg_hba.conf and SSL
- **inputs**: pg_hba.conf, postgresql.conf
- **outputs**: Remote psql connections work from authorized IPs
- **dependencies**: [db-ovh-004, db-ovh-012]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Can connect via psql from remote host with valid credentials

#### Task: db-ovh-020
- **title**: Set up PostgreSQL data directory on dedicated mount
- **description**: If OVH VPS has multiple disks, configure PostgreSQL data directory (PGDATA) on the fastest/most reliable mount point with appropriate permissions
- **inputs**: Mount points, PostgreSQL service user
- **outputs**: PostgreSQL data directory relocated to optimal storage location
- **dependencies**: [db-ovh-002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: `SHOW data_directory` returns configured mount point path

#### Task: db-ovh-021
- **title**: Configure PostgreSQL shared_preload_libraries
- **description**: Add recommended shared_preload_libraries for extensions that require pre-loading like pg_cron, pg_stat_statements, and other performance-related extensions
- **inputs**: postgresql.conf, list of required extensions
- **outputs**: shared_preload_libraries configured with pg_stat_statements and other needed modules
- **dependencies**: [db-ovh-003]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: `SHOW shared_preload_libraries` contains all required libraries

#### Task: db-ovh-022
- **title**: Create backup monitoring check script
- **description**: Create a simple script to verify PostgreSQL is accepting connections, the data directory is accessible, and basic health checks pass
- **inputs**: PostgreSQL connection parameters
- **outputs**: Executable health check script with exit codes for success/failure
- **dependencies**: [db-ovh-011]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Script exits 0 when PostgreSQL is healthy, non-zero when有问题

#### Task: db-ovh-023
- **title**: Configure PostgreSQL wal_level for logical replication
- **description**: Set wal_level to logical in postgresql.conf to enable logical replication capabilities needed for future backup and migration features
- **inputs**: postgresql.conf
- **outputs**: wal_level set to logical, PostgreSQL restarted successfully
- **dependencies**: [db-ovh-003]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: `SHOW wal_level` returns 'logical'

#### Task: db-ovh-024
- **title**: Create PostgreSQL maintenance schedule documentation
- **description**: Document recurring maintenance tasks including VACUUM scheduling, ANALYZE execution, index rebuilds, and log rotation with recommended frequencies
- **inputs**: PostgreSQL documentation, best practices
- **outputs**: Maintenance schedule document with cron job examples
- **dependencies**: [db-ovh-009]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Document includes all maintenance tasks with frequencies and sample cron entries

---

### Category: Schema Design

#### Task: schema-001
- **title**: Create users table with authentication fields
- **description**: Design and create the core users table storing authentication data including email (unique), password_hash (bcrypt), full_name, phone, avatar_url, and account status. Include timestamps for auditing
- **inputs**: PostgreSQL database, app_user permissions
- **outputs**: users table created with all specified columns and constraints
- **dependencies**: [db-ovh-011]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: users table exists with correct columns, email has unique constraint

#### Task: schema-002
- **title**: Create organizations table with tier information
- **description**: Design and create the organizations table storing business organizations that subscribe to Mini-CRM. Include name, slug (unique), billing_email, subscription_tier (starter/professional/enterprise corresponding to €29/49/79), subscription_status, max_users, max_contacts, max_jobs, max_invoices, and metadata (hstore for flexibility)
- **inputs**: PostgreSQL database, app_user permissions
- **outputs**: organizations table created with all specified columns
- **dependencies**: [db-ovh-011]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: organizations table exists with correct columns and tier constraints

#### Task: schema-003
- **title**: Create organization_memberships junction table
- **description**: Design and create the organization_memberships table to establish the many-to-many relationship between users and organizations. Include user_id, organization_id, role (owner/admin/member/viewer), joined_at, and invited_by fields
- **inputs**: users table, organizations table
- **outputs**: organization_memberships table created with proper foreign keys
- **dependencies**: [schema-001, schema-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Junction table exists with correct FK constraints and unique constraint on (user_id, organization_id)

#### Task: schema-004
- **title**: Create contacts table for lead and customer management
- **description**: Design and create the contacts table for managing leads and customers. Include organization_id (FK), first_name, last_name, email (unique per organization), phone, mobile, company, job_title, contact_type (lead/prospect/customer/supplier), source (referral/website/cold_call/other), lifetime_value, tags (array), custom_fields (hstore), notes, is_active, and full-text search vector column
- **inputs**: organizations table, PostgreSQL extensions
- **outputs**: contacts table created with all specified columns and GIN index for full-text search
- **dependencies**: [schema-002, db-ovh-010]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: contacts table exists with all columns, contact_type enum validated

#### Task: schema-005
- **title**: Create addresses table for contact addresses
- **description**: Design and create the addresses table to support multiple addresses per contact. Include contact_id (FK), address_type (billing/shipping/office/other), street_address_1, street_address_2, city, postal_code, state, country (default 'France'), is_primary, and geolocation coordinates (lat/lon)
- **inputs**: contacts table
- **outputs**: addresses table created with all specified columns
- **dependencies**: [schema-004]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: addresses table exists, FK to contacts works, country defaults to 'France'

#### Task: schema-006
- **title**: Create jobs table for project and work order management
- **description**: Design and create the jobs table for managing work orders and projects. Include organization_id (FK), contact_id (FK for customer), title, description, job_type (installation/repair/maintenance/consultation/other), status (draft/pending/in_progress/completed/cancelled), priority (low/medium/high/urgent), scheduled_start, scheduled_end, actual_start, actual_end, estimated_hours, actual_hours, hourly_rate, materials_cost, total_cost, currency (default 'EUR'), tags (array), custom_fields (hstore), notes, and search vector column
- **inputs**: organizations table, contacts table
- **outputs**: jobs table created with all specified columns and proper relationships
- **dependencies**: [schema-002, schema-004]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: jobs table exists with all columns, status transitions validated

#### Task: schema-007
- **title**: Create job_timeline table for job history tracking
- **description**: Design and create the job_timeline table to record all status changes and significant events for jobs. Include job_id (FK), event_type, event_data (JSONB), user_id (who made the change), created_at with automatic timestamp
- **inputs**: jobs table, users table
- **outputs**: job_timeline table created with proper indexes
- **dependencies**: [schema-001, schema-006]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: job_timeline table exists, automatically logs job changes

#### Task: schema-008
- **title**: Create invoices table for financial management
- **description**: Design and create the invoices table for managing invoices. Include organization_id (FK), invoice_number (unique per organization), job_id (FK, nullable for standalone), contact_id (FK), customer_name, customer_email, customer_address (text), subtotal, tax_rate (default 20 for France TVA), tax_amount, total_amount, currency (default 'EUR'), status (draft/sent/paid/overdue/cancelled), issue_date, due_date, paid_date, payment_method, payment_reference, notes, terms_conditions, and search vector column
- **inputs**: organizations table, contacts table, jobs table
- **outputs**: invoices table created with all specified columns and invoice_number unique per organization
- **dependencies**: [schema-002, schema-004, schema-006]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: invoices table exists, invoice_number unique constraint per organization enforced

#### Task: schema-009
- **title**: Create invoice_items table for line item details
- **description**: Design and create the invoice_items table to store line items for invoices. Include invoice_id (FK), description, quantity, unit_price, tax_rate, tax_amount, line_total, sort_order, and product_id (FK to products table, nullable)
- **inputs**: invoices table, products table (future)
- **outputs**: invoice_items table created with proper relationships
- **dependencies**: [schema-008]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: invoice_items table exists, totals can be calculated correctly

#### Task: schema-010
- **title**: Create pipeline_stages table for customizable sales pipeline
- **description**: Design and create the pipeline_stages table to allow organizations to customize their sales pipeline. Include organization_id (FK), name, description, stage_order, color, is_won_stage, is_lost_stage, probability_percentage, stage_type (qualification/proposal/negotiation/closed), created_at, updated_at
- **inputs**: organizations table
- **outputs**: pipeline_stages table created with default stages seeded
- **dependencies**: [schema-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: pipeline_stages table exists, default stages can be seeded per organization

#### Task: schema-011
- **title**: Create pipeline_opportunities table for deal tracking
- **description**: Design and create the pipeline_opportunities table for tracking sales deals/opportunities. Include organization_id (FK), contact_id (FK), title, description, pipeline_stage_id (FK), assigned_user_id (FK), estimated_value, probability, expected_close_date, actual_close_date, actual_value, currency (default 'EUR'), source, lost_reason, won_reason, tags (array), custom_fields (hstore), notes, search vector column, created_at, updated_at, closed_at
- **inputs**: organizations, contacts, users, pipeline_stages tables
- **outputs**: pipeline_opportunities table created with all specified columns
- **dependencies**: [schema-002, schema-004, schema-001, schema-010]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: pipeline_opportunities table exists, relationships work correctly

#### Task: schema-012
- **title**: Create products table for product/service catalog
- **description**: Design and create the products table for managing the product/service catalog. Include organization_id (FK), name, sku, description, product_type (product/service/subscription), unit_price, cost_price, tax_rate, unit (hour/piece/meter/unit), is_active, stock_quantity, low_stock_threshold, barcode, weight, dimensions, custom_fields (hstore), search vector column, created_at, updated_at
- **inputs**: organizations table
- **outputs**: products table created with all specified columns
- **dependencies**: [schema-002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: products table exists, SKU unique per organization enforced

#### Task: schema-013
- **title**: Create activities table for activity tracking
- **description**: Design and create the activities table for logging all activities across the CRM. Include organization_id (FK), user_id (FK), activity_type (call/email/meeting/task/note/system), subject, description, contact_id (FK, nullable), job_id (FK, nullable), opportunity_id (FK, nullable), activity_date, duration_minutes, outcome, custom_fields (hstore), metadata (JSONB), created_at
- **inputs**: organizations, users, contacts, jobs, pipeline_opportunities tables
- **outputs**: activities table created with proper indexes for querying
- **dependencies**: [schema-002, schema-001, schema-004, schema-006, schema-011]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: activities table exists, polymorphic relationships work correctly

#### Task: schema-014
- **title**: Create notifications table for user notifications
- **description**: Design and create the notifications table for user notification management. Include user_id (FK), organization_id (FK), notification_type, title, message, link_url, is_read, read_at, metadata (JSONB), created_at
- **inputs**: users, organizations tables
- **outputs**: notifications table created with proper indexes
- **dependencies**: [schema-001, schema-002]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: notifications table exists, can be queried by user efficiently

#### Task: schema-015
- **title**: Create documents table for file attachments
- **description**: Design and create the documents table for managing file attachments. Include organization_id (FK), user_id (FK), documentable_type (contact/job/invoice/opportunity), documentable_id, filename, original_filename, file_path, file_size, mime_type, category (contract/invoice/photo/document/other), description, created_at
- **inputs**: organizations, users tables
- **outputs**: documents table created with polymorphic relationship support
- **dependencies**: [schema-002, schema-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: documents table exists, polymorphic queries work correctly

#### Task: schema-016
- **title**: Create email_templates table for templated communications
- **description**: Design and create the email_templates table for managing email templates. Include organization_id (FK), name, subject, body (text), body_html, template_type (invoice/quote/reminder/welcome/custom), variables (JSONB for placeholder definitions), is_active, created_at, updated_at
- **inputs**: organizations table
- **outputs**: email_templates table created
- **dependencies**: [schema-002]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: email_templates table exists, templates can be stored and retrieved

#### Task: schema-017
- **title**: Create tags table for unified tagging system
- **description**: Design and create a normalized tags table and taggables junction table for unified tagging across contacts, jobs, invoices, and opportunities. Include name, slug, color, organization_id (FK for custom tags)
- **inputs**: organizations table
- **outputs**: tags and taggables tables created with proper polymorphic relationships
- **dependencies**: [schema-002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Tags can be applied to any taggable entity, queries return correct associations

#### Task: schema-018
- **title**: Create settings table for organization configuration
- **description**: Design and create the settings table for storing organization-level configuration. Include organization_id (FK), settings_key (unique per org), settings_value (JSONB), category (billing/notification/integration/custom), created_at, updated_at
- **inputs**: organizations table
- **outputs**: settings table created
- **dependencies**: [schema-002]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: settings table exists, key-value retrieval works per organization

#### Task: schema-019
- **title**: Create audit_logs table for comprehensive audit trail
- **description**: Design and create the audit_logs table for tracking all significant changes to data. Include organization_id (FK), user_id (FK), table_name, record_id, action (insert/update/delete), old_values (JSONB), new_values (JSONB), ip_address, user_agent, created_at
- **inputs**: organizations, users tables
- **outputs**: audit_logs table created with partitioned design for performance
- **dependencies**: [schema-002, schema-001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: audit_logs table exists, captures changes automatically via triggers

#### Task: schema-020
- **title**: Create api_tokens table for external integrations
- **description**: Design and create the api_tokens table for managing API access tokens for integrations. Include user_id (FK), organization_id (FK), token_name, token_hash, last_used_at, expires_at, scopes (array), ip_whitelist (array), created_at
- **inputs**: users, organizations tables
- **outputs**: api_tokens table created with secure token storage
- **dependencies**: [schema-001, schema-002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: api_tokens table exists, tokens stored securely as hashes

#### Task: schema-021
- **title**: Create scheduler_jobs table for background job tracking
- **description**: Design and create the scheduler_jobs table for tracking background jobs (if using pg_cron or similar). Include organization_id (FK), job_name, job_type, schedule, last_run_at, next_run_at, status, last_result (JSONB), is_active
- **inputs**: organizations table
- **outputs**: scheduler_jobs table created
- **dependencies**: [schema-002]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: scheduler_jobs table exists, can track recurring job execution

#### Task: schema-022
- **title**: Create subscriptions table for billing management
- **description**: Design and create the subscriptions table for tracking organization subscriptions. Include organization_id (FK), plan_name, plan_tier (starter/professional/enterprise), price_cents, billing_cycle (monthly/annual), status (active/trial/past_due/cancelled), trial_ends_at, current_period_start, current_period_end, cancelled_at, created_at, updated_at
- **inputs**: organizations table
- **outputs**: subscriptions table created with proper billing logic support
- **dependencies**: [schema-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: subscriptions table exists, billing cycle calculations work correctly

#### Task: schema-023
- **title**: Create payment_records table for payment history
- **description**: Design and create the payment_records table for tracking payments. Include subscription_id (FK), organization_id (FK), amount_cents, currency, payment_method, payment_provider, provider_transaction_id, status, payment_date, failure_reason, created_at
- **inputs**: subscriptions table, organizations table
- **outputs**: payment_records table created
- **dependencies**: [schema-022, schema-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: payment_records table exists, linked to subscriptions correctly

#### Task: schema-024
- **title**: Create function to generate sequential invoice numbers
- **description**: Create a PostgreSQL function generate_invoice_number(organization_id) that generates sequential invoice numbers per organization in format ORG-SLUG-YYYYMM-NNNN
- **inputs**: organizations table, invoices table
- **outputs**: Function created and tested
- **dependencies**: [schema-008, schema-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Function generates correct format, numbers are unique per organization

#### Task: schema-025
- **title**: Create trigger for automatic audit logging
- **description**: Create PostgreSQL trigger function and triggers on all core tables (contacts, jobs, invoices, opportunities) to automatically log changes to audit_logs table
- **inputs**: audit_logs table, core tables
- **outputs**: Triggers created on all relevant tables
- **dependencies**: [schema-019, schema-004, schema-006, schema-008, schema-011]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Changes to tracked tables appear in audit_logs automatically

#### Task: schema-026
- **title**: Create trigger for job timeline tracking
- **description**: Create PostgreSQL trigger function and triggers on jobs table to automatically record status changes in job_timeline table
- **inputs**: jobs table, job_timeline table
- **outputs**: Triggers created on jobs table
- **dependencies**: [schema-006, schema-007]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Status changes on jobs appear in job_timeline

#### Task: schema-027
- **title**: Create view for contact summary with job and invoice counts
- **description**: Create a PostgreSQL view v_contact_summary that joins contacts with aggregated job count, total job value, invoice count, total invoiced, and outstanding balance
- **inputs**: contacts, jobs, invoices tables
- **outputs**: v_contact_summary view created
- **dependencies**: [schema-004, schema-006, schema-008]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: View returns correct aggregated data per contact

#### Task: schema-028
- **title**: Create view for organization dashboard metrics
- **description**: Create a PostgreSQL view v_org_dashboard that provides organization-level metrics including total contacts, active jobs, pending invoices, total revenue MTD/YTD, pipeline value by stage
- **inputs**: All core tables
- **outputs**: v_org_dashboard view created
- **dependencies**: [schema-002, schema-004, schema-006, schema-008, schema-011]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: View returns comprehensive