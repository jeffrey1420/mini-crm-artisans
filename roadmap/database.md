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
organization metrics

#### Task: schema-029
- **title**: Create view for invoice aging report
- **description**: Create a PostgreSQL view v_invoice_aging that categorizes outstanding invoices by age buckets (current, 1-30 days, 31-60 days, 61-90 days, 90+ days)
- **inputs**: invoices table
- **outputs**: v_invoice_aging view created
- **dependencies**: [schema-008]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: View correctly categorizes invoice aging

#### Task: schema-030
- **title**: Create materialized view for pipeline summary with refresh
- **description**: Create a materialized view mv_pipeline_summary that provides pipeline metrics (count and value per stage) with concurrent refresh capability for real-time reporting
- **inputs**: pipeline_opportunities, pipeline_stages tables
- **outputs**: mv_pipeline_summary materialized view with refresh function
- **dependencies**: [schema-010, schema-011]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Materialized view can be refreshed concurrently without blocking reads

#### Task: schema-031
- **title**: Create enum types for status fields
- **description**: Create PostgreSQL enum types for contact_type, job_status, job_type, invoice_status, membership_role, subscription_tier, subscription_status for data integrity
- **inputs**: PostgreSQL database
- **outputs**: All enum types created and usable in table definitions
- **dependencies**: [db-ovh-011]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Enum types exist and can be used in column definitions

#### Task: schema-032
- **title**: Create function to calculate job total cost
- **description**: Create a PostgreSQL function calculate_job_total(job_id) that computes total cost based on actual_hours * hourly_rate + materials_cost
- **inputs**: jobs table
- **outputs**: Function created that returns total cost
- **dependencies**: [schema-006]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Function returns correct calculation for test job

#### Task: schema-033
- **title**: Create function to calculate invoice totals
- **description**: Create a PostgreSQL function recalculate_invoice_totals(invoice_id) that recomputes subtotal, tax_amount, and total_amount from invoice_items
- **inputs**: invoices table, invoice_items table
- **outputs**: Function created that updates invoice totals correctly
- **dependencies**: [schema-008, schema-009]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Function recalculates totals matching expected values

#### Task: schema-034
- **title**: Create trigger to auto-update invoice totals on item change
- **description**: Create PostgreSQL trigger that automatically calls recalculate_invoice_totals when invoice_items are inserted, updated, or deleted
- **inputs**: invoice_items table, invoices table
- **outputs**: Triggers created on invoice_items table
- **dependencies**: [schema-033, schema-009]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Invoice totals update automatically when items change

#### Task: schema-035
- **title**: Create function to get organization slug by ID
- **description**: Create a PostgreSQL function get_org_slug(org_id) that returns the organization slug for use in invoice number generation
- **inputs**: organizations table
- **outputs**: Function created and tested
- **dependencies**: [schema-002]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Function returns correct slug for given organization ID

#### Task: schema-036
- **title**: Create default pipeline stages for new organizations
- **description**: Create a PostgreSQL function create_default_pipeline_stages(org_id) that inserts default sales pipeline stages (Qualification, Proposal, Negotiation, Won, Lost) for new organizations
- **inputs**: organizations table, pipeline_stages table
- **outputs**: Function created, tested with sample organization
- **dependencies**: [schema-002, schema-010]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Function creates correct default stages with proper ordering

#### Task: schema-037
- **title**: Create trigger to auto-assign organization slug
- **description**: Create a PostgreSQL trigger function that automatically generates a URL-safe slug from organization name if slug is not provided during insert
- **inputs**: organizations table
- **outputs**: Trigger created on organizations table
- **dependencies**: [schema-002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Insert without slug generates valid slug from name

#### Task: schema-038
- **title**: Create sequence for organization-scoped invoice numbers
- **description**: Create a PostgreSQL sequence per organization for invoice numbering to ensure uniqueness and proper sequencing within each organization
- **inputs**: organizations table, invoices table
- **outputs**: Sequence creation function and per-org sequence management
- **dependencies**: [schema-002, schema-008]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Each organization gets sequential invoice numbers independent of other orgs

#### Task: schema-039
- **title**: Create function to archive old audit logs
- **description**: Create a PostgreSQL function archive_old_audit_logs(days_to_keep) that moves audit logs older than specified days to an archive table or partition
- **inputs**: audit_logs table
- **outputs**: Function created that successfully archives old records
- **dependencies**: [schema-019]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Function correctly identifies and handles old audit records

#### Task: schema-040
- **title**: Create partitioned audit_logs table by month
- **description**: Convert audit_logs table to partitioned by month for improved query performance and easier data management. Implement using PostgreSQL declarative partitioning
- **inputs**: audit_logs table structure
- **outputs**: Partitioned audit_logs table with monthly partitions
- **dependencies**: [schema-019]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: New audit entries route to correct monthly partition, old data accessible

---

### Category: Indexing Strategy

#### Task: idx-001
- **title**: Create primary indexes on all foreign keys
- **description**: Ensure every foreign key column has a corresponding index for optimal join performance. Review all tables and add indexes on organization_id, user_id, contact_id, job_id, etc. where missing
- **inputs**: All tables with foreign keys
- **outputs**: Indexes created on all FK columns
- **dependencies**: [schema-001, schema-002, schema-003, schema-004, schema-006, schema-008]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: All FK columns are indexed, EXPLAIN shows index usage in joins

#### Task: idx-002
- **title**: Create composite index on contacts for common queries
- **description**: Create composite index on contacts(organization_id, contact_type, is_active) to optimize filtering contacts by type within an organization
- **inputs**: contacts table
- **outputs**: Composite index created
- **dependencies**: [schema-004]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Index used for queries filtering by organization and contact_type

#### Task: idx-003
- **title**: Create composite index on jobs for status filtering
- **description**: Create composite index on jobs(organization_id, status, priority) to optimize job list views filtered by organization and status
- **inputs**: jobs table
- **outputs**: Composite index created
- **dependencies**: [schema-006]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Index used for status filtering queries

#### Task: idx-004
- **title**: Create composite index on invoices for aging reports
- **description**: Create composite index on invoices(organization_id, status, due_date) to optimize invoice aging queries and overdue invoice lookups
- **inputs**: invoices table
- **outputs**: Composite index created
- **dependencies**: [schema-008]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Index used for aging report queries

#### Task: idx-005
- **title**: Create index on pipeline_opportunities by stage
- **description**: Create composite index on pipeline_opportunities(organization_id, pipeline_stage_id, closed_at) for pipeline board queries and won/lost analysis
- **inputs**: pipeline_opportunities table
- **outputs**: Composite index created
- **dependencies**: [schema-011]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Index used for stage-based opportunity queries

#### Task: idx-006
- **title**: Create GIN index on contacts tags array
- **description**: Create GIN index on contacts.tags for efficient array containment queries when filtering contacts by tags
- **inputs**: contacts table
- **outputs**: GIN index on tags column
- **dependencies**: [schema-004]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Tag-based queries use index for filtering

#### Task: idx-007
- **title**: Create GIN index on jobs tags array
- **description**: Create GIN index on jobs.tags for efficient array containment queries when filtering jobs by tags
- **inputs**: jobs table
- **outputs**: GIN index on tags column
- **dependencies**: [schema-006]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Tag-based queries use index for filtering

#### Task: idx-008
- **title**: Create partial index on active contacts
- **description**: Create partial index on contacts WHERE is_active = true to optimize queries for active contacts only
- **inputs**: contacts table
- **outputs**: Partial index created
- **dependencies**: [schema-004]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Active contact queries use partial index

#### Task: idx-009
- **title**: Create partial index on pending invoices
- **description**: Create partial index on invoices WHERE status IN ('sent', 'overdue') for efficient pending invoice lookups
- **inputs**: invoices table
- **outputs**: Partial index created
- **dependencies**: [schema-008]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Pending invoice queries use partial index

#### Task: idx-010
- **title**: Create index on activities for contact timeline
- **description**: Create composite index on activities(contact_id, activity_date DESC) for efficient contact activity timeline queries
- **inputs**: activities table
- **outputs**: Composite index created
- **dependencies**: [schema-013]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Contact timeline queries use index

#### Task: idx-011
- **title**: Create index on activities for user workload
- **description**: Create composite index on activities(user_id, activity_date) for efficient user workload and task queries
- **inputs**: activities table
- **outputs**: Composite index created
- **dependencies**: [schema-013]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: User activity queries use index

#### Task: idx-012
- **title**: Create trigram index on contact names for fuzzy search
- **description**: Create GIN trigram index on contacts(first_name, last_name, company) using pg_trgm extension for fuzzy name searching
- **inputs**: contacts table, pg_trgm extension
- **outputs**: Trigram GIN index created
- **dependencies**: [schema-004, db-ovh-010]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Fuzzy name searches use trigram index

#### Task: idx-013
- **title**: Create trigram index on job titles for fuzzy search
- **description**: Create GIN trigram index on jobs(title) using pg_trgm extension for fuzzy job title searching
- **inputs**: jobs table, pg_trgm extension
- **outputs**: Trigram GIN index created
- **dependencies**: [schema-006, db-ovh-010]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Fuzzy job title searches use trigram index

#### Task: idx-014
- **title**: Create unique index on products SKU per organization
- **description**: Create unique composite index on products(organization_id, sku) to ensure SKU uniqueness within each organization
- **inputs**: products table
- **outputs**: Unique composite index created
- **dependencies**: [schema-012]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Duplicate SKU within same organization is rejected

#### Task: idx-015
- **title**: Create unique index on organization slug
- **description**: Create unique index on organizations(slug) for URL-friendly organization identification
- **inputs**: organizations table
- **outputs**: Unique index on slug column
- **dependencies**: [schema-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Duplicate organization slugs are rejected

#### Task: idx-016
- **title**: Create unique index on users email
- **description**: Create unique index on users(email) for user authentication and uniqueness
- **inputs**: users table
- **outputs**: Unique index on email column
- **dependencies**: [schema-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Duplicate user emails are rejected

#### Task: idx-017
- **title**: Create index on notifications for user delivery
- **description**: Create composite index on notifications(user_id, is_read, created_at DESC) for efficient notification delivery and unread count queries
- **inputs**: notifications table
- **outputs**: Composite index created
- **dependencies**: [schema-014]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: User notification queries use index

#### Task: idx-018
- **title**: Create index on api_tokens for authentication
- **description**: Create index on api_tokens(token_hash) for fast API token lookup during authentication
- **inputs**: api_tokens table
- **outputs**: Index on token_hash column
- **dependencies**: [schema-020]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Token lookup queries use index

#### Task: idx-019
- **title**: Create index on addresses for postal code queries
- **description**: Create composite index on addresses(contact_id, postal_code) for efficient address lookups by location
- **inputs**: addresses table
- **outputs**: Composite index created
- **dependencies**: [schema-005]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Address queries use index

#### Task: idx-020
- **title**: Create BRIN index on audit_logs created_at
- **description**: Create BRIN (Block Range Index) on audit_logs(created_at) for efficient time-range queries on the partitioned audit_logs table
- **inputs**: audit_logs table
- **outputs**: BRIN index created
- **dependencies**: [schema-019]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Time-range queries on audit_logs use BRIN index

#### Task: idx-021
- **title**: Create index on job_timeline for job history
- **description**: Create composite index on job_timeline(job_id, created_at DESC) for efficient job history queries
- **inputs**: job_timeline table
- **outputs**: Composite index created
- **dependencies**: [schema-007]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Job history queries use index

#### Task: idx-022
- **title**: Analyze all indexes for usage patterns
- **description**: Use pg_stat_user_indexes to analyze which indexes are actually being used and identify unused indexes for potential removal
- **inputs**: pg_stat_user_indexes, pg_indexes
- **outputs**: Report of used vs unused indexes
- **dependencies**: [idx-001, idx-002, idx-003, idx-004, idx-005]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Unused indexes identified and documented for review

#### Task: idx-023
- **title**: Document indexing strategy and naming conventions
- **description**: Create documentation covering the indexing strategy, naming conventions (idx_tablename_column_pattern), and guidelines for when to add new indexes
- **inputs**: All created indexes
- **outputs**: Index documentation file
- **dependencies**: [idx-001, idx-022]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Documentation covers all index types and naming conventions used

#### Task: idx-024
- **title**: Create composite index on jobs for calendar views
- **description**: Create composite index on jobs(organization_id, scheduled_start, scheduled_end) for efficient job calendar and scheduling queries
- **inputs**: jobs table
- **outputs**: Composite index created
- **dependencies**: [schema-006]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Calendar range queries use index

#### Task: idx-025
- **title**: Create index on settings for organization config
- **description**: Create unique index on settings(organization_id, settings_key) for efficient organization configuration retrieval
- **inputs**: settings table
- **outputs**: Unique composite index created
- **dependencies**: [schema-018]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Settings queries use unique index

---

### Category: Migrations (Flyway/Drizzt)

#### Task: mig-001
- **title**: Set up Flyway migration directory structure
- **description**: Create the standard Flyway migration directory structure: /db/migrations with subdirectories for each major version and naming convention V#__Description.sql
- **inputs**: Project root directory
- **outputs**: Migration directory structure created
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Directory structure exists and Flyway can discover migrations

#### Task: mig-002
- **title**: Configure Flyway for PostgreSQL connection
- **description**: Create flyway.conf file with PostgreSQL connection settings, SSL configuration, and migration location paths
- **inputs**: Database connection details
- **outputs**: flyway.conf configured and validated
- **dependencies**: [mig-001, db-ovh-012]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Flyway can connect to database and baseline exists

#### Task: mig-003
- **title**: Create initial schema migration V001
- **description**: Create V001__Initial_Schema.sql migration that creates all enum types and base tables (users, organizations, organization_memberships)
- **inputs**: Schema definitions from schema-001, schema-002, schema-003
- **outputs**: V001__Initial_Schema.sql migration file
- **dependencies**: [mig-001, schema-031, schema-001, schema-002, schema-003]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Migration runs successfully, creates all tables

#### Task: mig-004
- **title**: Create contacts and addresses migration V002
- **description**: Create V002__Contacts_and_Addresses.sql migration for contacts, addresses tables and related indexes
- **inputs**: Schema definitions from schema-004, schema-005
- **outputs**: V002__Contacts_and_Addresses.sql migration file
- **dependencies**: [mig-003, schema-004, schema-005]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Migration runs successfully, creates contacts and addresses

#### Task: mig-005
- **title**: Create jobs migration V003
- **description**: Create V003__Jobs.sql migration for jobs, job_timeline tables, indexes, and job-related functions/triggers
- **inputs**: Schema definitions from schema-006, schema-007
- **outputs**: V003__Jobs.sql migration file
- **dependencies**: [mig-004, schema-006, schema-007]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Migration runs successfully, creates jobs tables

#### Task: mig-006
- **title**: Create invoices migration V004
- **description**: Create V004__Invoices.sql migration for invoices, invoice_items tables, indexes, invoice number generation functions
- **inputs**: Schema definitions from schema-008, schema-009, schema-024
- **outputs**: V004__Invoices.sql migration file
- **dependencies**: [mig-005, schema-008, schema-009, schema-024]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Migration runs successfully, creates invoice tables

#### Task: mig-007
- **title**: Create pipeline migration V005
- **description**: Create V005__Pipeline.sql migration for pipeline_stages and pipeline_opportunities tables
- **inputs**: Schema definitions from schema-010, schema-011
- **outputs**: V005__Pipeline.sql migration file
- **dependencies**: [mig-006, schema-010, schema-011]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Migration runs successfully, creates pipeline tables

#### Task: mig-008
- **title**: Create products and activities migration V006
- **description**: Create V006__Products_and_Activities.sql migration for products, activities tables
- **inputs**: Schema definitions from schema-012, schema-013
- **outputs**: V006__Products_and_Activities.sql migration file
- **dependencies**: [mig-007, schema-012, schema-013]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Migration runs successfully, creates products and activities

#### Task: mig-009
- **title**: Create supporting tables migration V007
- **description**: Create V007__Supporting_Tables.sql migration for notifications, documents, email_templates, tags, settings tables
- **inputs**: Schema definitions from schema-014, schema-015, schema-016, schema-017, schema-018
- **outputs**: V007__Supporting_Tables.sql migration file
- **dependencies**: [mig-008, schema-014, schema-015, schema-016, schema-017, schema-018]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Migration runs successfully, creates all supporting tables

#### Task: mig-010
- **title**: Create subscriptions and billing migration V008
- **description**: Create V008__Subscriptions_and_Billing.sql migration for subscriptions, payment_records tables
- **inputs**: Schema definitions from schema-022, schema-023
- **outputs**: V008__Subscriptions_and_Billing.sql migration file
- **dependencies**: [mig-009, schema-022, schema-023]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Migration runs successfully, creates billing tables

#### Task: mig-011
- **title**: Create audit and API migration V009
- **description**: Create V009__Audit_and_API.sql migration for audit_logs (partitioned), api_tokens tables
- **inputs**: Schema definitions from schema-019, schema-020
- **outputs**: V009__Audit_and_API.sql migration file
- **dependencies**: [mig-010, schema-019, schema-020]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Migration runs successfully, creates audit and API tables

#### Task: mig-012
- **title**: Create views and functions migration V010
- **description**: Create V010__Views_and_Functions.sql migration for all views, materialized views, and utility functions
- **inputs**: Schema definitions from schema-027, schema-028, schema-029, schema-030
- **outputs**: V010__Views_and_Functions.sql migration file
- **dependencies**: [mig-011, schema-027, schema-028, schema-029, schema-030]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Migration runs successfully, creates all views

#### Task: mig-013
- **title**: Create indexes migration V011
- **description**: Create V011__Indexes.sql migration for all composite indexes, partial indexes, and special indexes not created by earlier migrations
- **inputs**: Index definitions from idx-001 through idx-025
- **outputs**: V011__Indexes.sql migration file
- **dependencies**: [mig-012, idx-001, idx-002, idx-003]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Migration runs successfully, creates all additional indexes

#### Task: mig-014
- **title**: Create RLS policies migration V012
- **description**: Create V012__Row_Level_Security.sql migration to enable RLS on all organization-scoped tables
- **inputs**: RLS policy definitions
- **outputs**: V012__Row_Level_Security.sql migration file
- **dependencies**: [mig-013, rls-001, rls-002, rls-003]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Migration runs successfully, RLS policies enforced

#### Task: mig-015
- **title**: Create baseline migration for existing database
- **description**: Create baseline migration to mark existing database state as baseline so Flyway can manage future migrations
- **inputs**: Existing database state
- **outputs**: Flyway baseline created successfully
- **dependencies**: [mig-003]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Flyway baseline command succeeds

#### Task: mig-016
- **title**: Create rollback scripts for critical migrations
- **description**: Create undo scripts for critical migrations (V001, V004, V008) in the /db/undo directory following Flyway undo naming convention
- **inputs**: V001, V004, V008 migrations
- **outputs**: Undo scripts created for critical migrations
- **dependencies**: [mig-003, mig-006, mig-010]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Undo scripts can reverse their respective migrations

#### Task: mig-017
- **title**: Configure Flyway CI/CD integration
- **description**: Integrate Flyway into CI/CD pipeline to automatically run migrations on deployment using GitHub Actions or similar
- **inputs**: CI/CD configuration files
- **outputs**: Flyway runs automatically on deployment
- **dependencies**: [mig-015]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Migrations run automatically in CI/CD pipeline

#### Task: mig-018
- **title**: Create seed data migration for development
- **description**: Create V999__Seed_Data_Dev.sql migration with sample data for development including test organizations, users, contacts, jobs, invoices
- **inputs**: Sample data requirements
- **outputs**: V999__Seed_Data_Dev.sql migration file
- **dependencies**: [mig-012]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Seed data creates usable development environment

#### Task: mig-019
- **title**: Create repeatable migration for default pipeline stages
- **description**: Create Flyway repeatable migration R__Default_Pipeline_Stages.sql that creates default pipeline stages for any organization missing them
- **inputs**: schema-036 function
- **outputs**: Repeatable migration file created
- **dependencies**: [mig-007, schema-036]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: New organizations get default pipeline stages automatically

#### Task: mig-020
- **title**: Test migration reproducibility
- **description**: Run full migration sequence on clean database to verify all migrations are deterministic and reproducible
- **inputs**: Clean PostgreSQL database
- **outputs**: All migrations succeed in sequence
- **dependencies**: [mig-017]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Complete migration run succeeds on clean database

---

### Category: Row-Level Security (RLS) Policies

#### Task: rls-001
- **title**: Enable RLS on organizations table
- **description**: Enable Row-Level Security on organizations table. Note: organizations is a special case - all authenticated users can see all orgs in the system for signup/invitation flows
- **inputs**: organizations table
- **outputs**: RLS enabled with appropriate bypass policies for system-level queries
- **dependencies**: [schema-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: RLS enabled, system queries work without row filtering

#### Task: rls-002
- **title**: Create RLS policies for users table
- **description**: Create RLS policies on users table ensuring users can only see their own user record and users within their organization
- **inputs**: users table, organization_memberships table
- **outputs**: RLS policies created and enabled
- **dependencies**: [schema-001, schema-003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Users can only see their own record and org members

#### Task: rls-003
- **title**: Create RLS policies for organization_memberships table
- **description**: Create RLS policies on organization_memberships table ensuring users can only see memberships in organizations they belong to
- **inputs**: organization_memberships table
- **outputs**: RLS policies created and enabled
- **dependencies**: [schema-003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Users can only see memberships for their organizations

#### Task: rls-004
- **title**: Create RLS policies for contacts table
- **description**: Create RLS policies on contacts table ensuring users can only access contacts within their organization
- **inputs**: contacts table
- **outputs**: RLS policies created and enabled
- **dependencies**: [schema-004]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Users can only see and modify contacts in their organization

#### Task: rls-005
- **title**: Create RLS policies for addresses table
- **description**: Create RLS policies on addresses table ensuring addresses are only accessible through their parent contact's organization
- **inputs**: addresses table, contacts table
- **outputs**: RLS policies created and enabled
- **dependencies**: [schema-005, schema-004]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Address access is controlled through contact ownership

#### Task: rls-006
- **title**: Create RLS policies for jobs table
- **description**: Create RLS policies on jobs table ensuring users can only access jobs within their organization
- **inputs**: jobs table
- **outputs**: RLS policies created and enabled
- **dependencies**: [schema-006]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Users can only see and modify jobs in their organization

#### Task: rls-007
- **title**: Create RLS policies for job_timeline table
- **description**: Create RLS policies on job_timeline table ensuring timeline entries are accessible only through parent job ownership
- **inputs**: job_timeline table, jobs table
- **outputs**: RLS policies created and enabled
- **dependencies**: [schema-007, schema-006]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Timeline access follows job ownership

#### Task: rls-008
- **title**: Create RLS policies for invoices table
- **description**: Create RLS policies on invoices table ensuring users can only access invoices within their organization
- **inputs**: invoices table
- **outputs**: RLS policies created and enabled
- **dependencies**: [schema-008]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Users can only see invoices in their organization

#### Task: rls-009
- **title**: Create RLS policies for invoice_items table
- **description**: Create RLS policies on invoice_items table ensuring items are only accessible through parent invoice ownership
- **inputs**: invoice_items table, invoices table
- **outputs**: RLS policies created and enabled
- **dependencies**: [schema-009, schema-008]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Invoice item access follows invoice ownership

#### Task: rls-010
- **title**: Create RLS policies for pipeline_stages table
- **description**: Create RLS policies on pipeline_stages table ensuring users can only access stages within their organization
- **inputs**: pipeline_stages table
- **outputs**: RLS policies created and enabled
- **dependencies**: [schema-010]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Users can only see pipeline stages in their organization

#### Task: rls-011
- **title**: Create RLS policies for pipeline_opportunities table
- **description**: Create RLS policies on pipeline_opportunities table ensuring users can only access opportunities within their organization
- **inputs**: pipeline_opportunities table
- **outputs**: RLS policies created and enabled
- **dependencies**: [schema-011]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Users can only see opportunities in their organization

#### Task: rls-012
- **title**: Create RLS policies for products table
- **description**: Create RLS policies on products table ensuring users can only access products within their organization
- **inputs**: products table
- **outputs**: RLS policies created and enabled
- **dependencies**: [schema-012]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Users can only see products in their organization

#### Task: rls-013
- **title**: Create RLS policies for activities table
- **description**: Create RLS policies on activities table ensuring users can only access activities within their organization
- **inputs**: activities table
- **outputs**: RLS policies created and enabled
- **dependencies**: [schema-013]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Users can only see activities in their organization

#### Task: rls-014
- **title**: Create RLS policies for notifications table
- **description**: Create RLS policies on notifications table ensuring users can only see their own notifications
- **inputs: notifications table
- **outputs**: RLS policies created and enabled
- **dependencies**: [schema-014]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Users can only see their own notifications

#### Task: rls-015
- **title**: Create RLS policies for documents table
- **description**: Create RLS policies on documents table ensuring documents are only accessible through parent entity ownership
- **inputs**: documents table
- **outputs**: RLS policies created and enabled
- **dependencies**: [schema-015]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Document access follows parent entity ownership

#### Task: rls-016
- **title**: Create RLS policies for email_templates table
- **description**: Create RLS policies on email_templates table ensuring users can only access templates within their organization
- **inputs**: email_templates table
- **outputs**: RLS policies created and enabled
- **dependencies**: [schema-016]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Users can only see templates in their organization

#### Task: rls-017
- **title**: Create RLS policies for tags and taggables tables
- **description**: Create RLS policies on tags and taggables tables ensuring tag access follows organization boundaries
- **inputs**: tags table, taggables table
- **outputs**: RLS policies created and enabled
- **dependencies**: [schema-017]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Tag access follows organization boundaries

#### Task: rls-018
- **title**: Create RLS policies for settings table
- **description**: Create RLS policies on settings table ensuring users can only access settings within their organization
- **inputs**: settings table
- **outputs**: RLS policies created and enabled
- **dependencies**: [schema-018]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Users can only see settings in their organization

#### Task: rls-019
- **title**: Create RLS policies for audit_logs table
- **description**: Create RLS policies on audit_logs table ensuring users can only see audit logs within their organization
- **inputs**: audit_logs table
- **outputs**: RLS policies created and enabled
- **dependencies**: [schema-019]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Users can only see audit logs in their organization

#### Task: rls-020
- **title**: Create RLS policies for api_tokens table
- **description**: Create RLS policies on api_tokens table ensuring users can only see and manage their own API tokens
- **inputs**: api_tokens table
- **outputs**: RLS policies created and enabled
- **dependencies**: [schema-020]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Users can only see and manage their own API tokens

#### Task: rls-021
- **title**: Create RLS policies for subscriptions table
- **description**: Create RLS policies on subscriptions table ensuring users can only access subscription info within their organization
- **inputs**: subscriptions table
- **outputs**: RLS policies created and enabled
- **dependencies**: [schema-022]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Users can only see subscription in their organization

#### Task: rls-022
- **title**: Create RLS policies for payment_records table
- **description**: Create RLS policies on payment_records table ensuring users can only access payment records within their organization
- **inputs**: payment_records table
- **outputs**: RLS policies created and enabled
- **dependencies**: [schema-023]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Users can only see payment records in their organization

#### Task: rls-023
- **title**: Create application user for Nuxt with RLS bypass
- **description**: Create a PostgreSQL role for the Nuxt 3 application that bypasses RLS for internal queries while still respecting RLS for user-facing queries
- **inputs**: RLS policies, app_user role
- **outputs**: app_user role with appropriate RLS bypass settings
- **dependencies**: [db-ovh-013, rls-002, rls-004, rls-006, rls-008]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Application functions correctly with RLS enforced

#### Task: rls-024
- **title**: Test RLS isolation between organizations
- **description**: Create test scripts that attempt cross-organization data access and verify RLS policies correctly block unauthorized access
- **inputs**: Multiple test organizations with data
- **outputs**: Test script with all tests passing
- **dependencies**: [rls-023]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Cross-org access is blocked, same-org access works correctly

#### Task: rls-025
- **title**: Document RLS policy architecture
- **description**: Create documentation explaining the RLS policy architecture, how organization_id filtering works, and guidelines for adding RLS to new tables
- **inputs**: All RLS policies
- **outputs**: RLS documentation file
- **dependencies**: [rls-001, rls-024]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Documentation covers all RLS patterns and can guide future development

---

### Category: Backup & Restore Strategy

#### Task: backup-001
- **title**: Configure WAL archiving to local directory
- **description**: Configure PostgreSQL WAL (Write-Ahead Log) archiving to a local directory for point-in-time recovery capability
- **inputs**: postgresql.conf, archive directory
- **outputs**: WAL archiving configured and tested
- **dependencies**: [db-ovh-003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: WAL files appear in archive directory

#### Task: backup-002
- **title**: Set up daily base backup using pg_basebackup
- **description**: Create cron job to run pg_basebackup daily, creating full base backups of the PostgreSQL data directory
- **inputs**: pg_basebackup command, backup directory, cron
- **outputs**: Daily base backup cron job created
- **dependencies**: [backup-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Base backups appear in backup directory daily

#### Task: backup-003
- **title**: Configure retention policy for base backups
- **description**: Create script to retain daily backups for 7 days, weekly for 4 weeks, monthly for 12 months, and yearly for 7 years per French tax requirements
- **inputs**: Backup directory, retention rules
- **outputs**: Retention script created and tested
- **dependencies**: [backup-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Old backups are automatically deleted per retention policy

#### Task: backup-004
- **title**: Create off-site backup transfer script
- **description**: Create script to transfer daily backups to a separate geographic location (different OVH datacenter or S3-compatible storage) for disaster recovery
- **inputs**: Backup directory, remote storage credentials
- **outputs**: Transfer script created and tested
- **dependencies**: [backup-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Backups successfully transferred to remote location

#### Task: backup-005
- **title**: Create point-in-time recovery test procedure
- **description**: Document and test the procedure for recovering the database to a specific point in time using base backup and WAL files
- **inputs**: Base backup, WAL archive
- **outputs**: Recovery procedure documented and tested
- **dependencies**: [backup-001, backup-002]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: Database recovered to specific point in time successfully

#### Task: backup-006
- **title**: Create database restore verification script
- **description**: Create script that verifies restored database integrity by running pg_verifybackup and checking critical table row counts
- **inputs**: Restored database, baseline row counts
- **outputs**: Verification script created
- **dependencies**: [backup-005]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Script correctly identifies successful and failed restores

#### Task: backup-007
- **title**: Configure pgBackRest for advanced backup management
- **description**: Install and configure pgBackRest as an alternative to native PostgreSQL backup tools for more efficient incremental backups
- **inputs**: pgBackRest installation, PostgreSQL
- **outputs**: pgBackRest configured with stanza
- **dependencies**: [backup-001]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: pgBackRest can perform and list backups

#### Task: backup-008
- **title**: Create automated backup verification
- **description**: Create script that automatically verifies backup integrity by restoring to a test environment and running application smoke tests
- **inputs**: Latest backup, test environment
- **outputs**: Automated verification job
- **dependencies**: [backup-006]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: Verification runs automatically and reports results

#### Task: backup-009
- **title**: Create backup monitoring and alerting
- **description**: Configure monitoring to alert if daily backup fails or if WAL accumulation indicates archiving issues
- **inputs**: Backup scripts, monitoring system
- **outputs**: Alerts configured for backup failures
- **dependencies**: [backup-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Alert fires when backup job fails

#### Task: backup-010
- **title**: Document disaster recovery runbook
- **description**: Create comprehensive disaster recovery runbook covering various failure scenarios (database corruption, server loss, ransomware) with step-by-step recovery procedures
- **inputs**: All backup procedures
- **outputs**: DR runbook document
- **dependencies**: [backup-005, backup-009]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: Runbook covers all major disaster scenarios

#### Task: backup-011
- **title**: Test backup restoration quarterly
- **description**: Schedule and execute quarterly backup restoration tests to verify backups are valid and recovery procedures work
- **inputs**: Most recent backup, isolated test environment
- **outputs**: Quarterly test completed with report
- **dependencies**: [backup-005]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: Test restoration completes successfully

#### Task: backup-012
- **title**: Create per-organization database dump capability
- **description**: Create function or script to export all data for a specific organization (for GDPR compliance or tenant migration)
- **inputs**: Organization ID
- **outputs**: Organization data export script
- **dependencies**: [rls-001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Export contains all data for specified organization

#### Task: backup-013
- **title**: Configure tablespace backup handling
- **description**: Ensure pgBackRest or custom scripts correctly handle tablespace layouts with separate tablespaces for tables and indexes
- **inputs**: Tablespace configuration, backup tool
- **outputs**: Tablespaces included in backups and restores
- **dependencies**: [db-ovh-005, backup-007]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Tablespace data restored correctly

#### Task: backup-014
- **title**: Create backup encryption for sensitive data
- **description**: Implement encryption for backups containing sensitive financial data using GPG or similar tool
- **inputs**: Backup files, encryption keys
- **outputs**: Encrypted backups created
- **dependencies**: [backup-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Backups encrypted and can be decrypted

#### Task: backup-015
- **title**: Document backup and restore procedures
- **description**: Create comprehensive backup documentation covering all procedures, schedules, retention policies, and verification steps
- **inputs**: All backup configurations
- **outputs**: Backup documentation file
- **dependencies**: [backup-001, backup-002, backup-003, backup-004]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Documentation complete and accurate

---

### Category: Connection Pooling (PgBouncer)

#### Task: pool-001
- **title**: Install PgBouncer on OVH VPS
- **description**: Install PgBouncer connection pooler on the OVH VPS alongside or on a dedicated server for connection pooling
- **inputs**: Apt or source installation, PgBouncer version
- **outputs**: PgBouncer installed and running
- **dependencies**: [db-ovh-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: PgBouncer service running and accepting connections

#### Task: pool-002
- **title**: Configure PgBouncer for transaction pooling mode
- **description**: Configure PgBouncer in transaction pooling mode (most efficient for connection pooling) with appropriate pool sizes
- **inputs**: PgBouncer config file
- **outputs**: Transaction mode configured
- **dependencies**: [pool-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: PgBouncer connects to PostgreSQL in transaction mode

#### Task: pool-003
- **title**: Configure PgBouncer pool sizes for Mini-CRM workload
- **description**: Set appropriate pool_size, max_client_conn, and server_idle_timeout based on expected concurrent users and OVH VPS resources
- **inputs**: Expected user load, VPS resources
- **outputs**: Pool sizes configured optimally
- **dependencies**: [pool-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Pool handles expected load without exhaustion

#### Task: pool-004
- **title**: Set up PgBouncer authentication with userlist
- **description**: Configure PgBouncer userlist.txt with PostgreSQL user credentials for PgBouncer-to-PostgreSQL authentication
- **inputs**: PostgreSQL user credentials
- **outputs**: PgBouncer userlist configured
- **dependencies**: [pool-001, db-ovh-013]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: PgBouncer can authenticate to PostgreSQL

#### Task: pool-005
- **title**: Configure PgBouncer port and listening address
- **description**: Set PgBouncer to listen on appropriate port (5433 or similar) and bind address for Nuxt 3 application connection
- **inputs**: Network configuration
- **outputs**: PgBouncer listening on configured port
- **dependencies**: [pool-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Nuxt 3 can connect via PgBouncer port

#### Task: pool-006
- **title**: Enable PgBouncer query logging
- **description**: Configure PgBouncer logging to capture connection pool statistics and slow queries for monitoring
- **inputs**: PgBouncer config
- **outputs**: Query logging enabled
- **dependencies**: [pool-002]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Logs show connection pool activity

#### Task: pool-007
- **title**: Create PgBouncer health check endpoint
- **description**: Configure PgBouncer admin interface and create health check script that verifies PgBouncer is functioning
- **inputs**: PgBouncer admin settings
- **outputs**: Health check script created
- **dependencies**: [pool-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Health check passes when PgBouncer is healthy

#### Task: pool-008
- **title**: Configure PgBouncer server_reset_query
- **description**: Set server_reset_query to DISCARD ALL for transaction pooling mode to properly clean up session state between transactions
- **inputs**: PgBouncer config
- **outputs**: server_reset_query configured
- **dependencies**: [pool-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Session state properly discarded between transactions

#### Task: pool-009
- **title**: Test PgBouncer with application connection string
- **description**: Test Nuxt 3 application connection through PgBouncer to verify transaction pooling works correctly with application queries
- **inputs**: Nuxt 3 application, PgBouncer
- **outputs**: Application works correctly through PgBouncer
- **dependencies**: [pool-005]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Application functions correctly with PgBouncer

#### Task: pool-010
- **title**: Configure PgBouncer restart on PostgreSQL connection loss
- **description**: Configure PgBouncer to automatically reconnect to PostgreSQL after connection loss using pause_mode and resume
- **inputs**: PgBouncer config
- **outputs**: Automatic reconnection configured
- **dependencies**: [pool-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: PgBouncer reconnects after PostgreSQL restart

#### Task: pool-011
- **title**: Create PgBouncer monitoring queries
- **description**: Create SQL queries against PgBouncer admin tables to monitor active connections, pool utilization, and client/server connection states
- **inputs**: PgBouncer admin database
- **outputs**: Monitoring queries created
- **dependencies**: [pool-006]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Queries return accurate pool statistics

#### Task: pool-012
- **title**: Document PgBouncer configuration for operators
- **description**: Create documentation covering PgBouncer configuration, monitoring, and troubleshooting procedures for operations team
- **inputs**: PgBouncer configuration files
- **outputs**: Documentation file
- **dependencies**: [pool-001, pool-011]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Documentation complete and accurate

#### Task: pool-013
- **title**: Tune PgBouncer reserve_pool_size
- **description**: Configure reserve_pool_size for handling connection bursts without affecting normal operation
- **inputs**: PgBouncer config
- **outputs**: Reserve pool configured
- **dependencies**: [pool-003]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Burst connections handled by reserve pool

#### Task: pool-014
- **title**: Set up high availability with multiple PgBouncer instances
- **description**: Configure multiple PgBouncer instances with load balancing for high availability
- **inputs**: Multiple servers, load balancer
- **outputs**: HA PgBouncer configuration
- **dependencies**: [pool-001]
- **priority**: low
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: PgBouncer continues working if one instance fails

---

### Category: Full-Text Search (PostgreSQL tsvector for French)

#### Task: fts-001
- **title**: Create French text search configuration
- **description**: Create PostgreSQL text search configuration for French language using unaccent extension and French dictionary
- **inputs**: PostgreSQL extensions, French dictionary files
- **outputs**: french_search configuration created
- **dependencies**: [db-ovh-010]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: French text search configuration works correctly

#### Task: fts-002
- **title**: Add tsvector column to contacts table
- **description**: Add search_vector tsvector column to contacts table and create trigger to automatically update it based on first_name, last_name, company, email, notes
- **inputs**: contacts table, French search config
- **outputs**: search_vector column and trigger created
- **dependencies**: [schema-004, fts-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: search_vector populated and updated automatically

#### Task: fts-003
- **title**: Add tsvector column to jobs table
- **description**: Add search_vector tsvector column to jobs table and create trigger to automatically update it based on title, description, notes
- **inputs**: jobs table, French search config
- **outputs**: search_vector column and trigger created
- **dependencies**: [schema-006, fts-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: search_vector populated and updated automatically

#### Task: fts-004
- **title**: Add tsvector column to invoices table
- **description**: Add search_vector tsvector column to invoices table and create trigger to automatically update it based on invoice_number, customer_name, notes
- **inputs**: invoices table, French search config
- **outputs**: search_vector column and trigger created
- **dependencies**: [schema-008, fts-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: search_vector populated and updated automatically

#### Task: fts-005
- **title**: Add tsvector column to products table
- **description**: Add search_vector tsvector column to products table and create trigger to automatically update it based on name, sku, description
- **inputs**: products table, French search config
- **outputs**: search_vector column and trigger created
- **dependencies**: [schema-012, fts-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: search_vector populated and updated automatically

#### Task: fts-006
- **title**: Create GIN indexes on tsvector columns
- **description**: Create GIN indexes on all search_vector columns for efficient full-text search queries
- **inputs**: contacts, jobs, invoices, products tables
- **outputs**: GIN indexes created on search_vector columns
- **dependencies**: [fts-002, fts-003, fts-004, fts-005]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Full-text queries use GIN index

#### Task: fts-007
- **title**: Create unified search function across entities
- **description**: Create a PostgreSQL function search_all(query text, limit_count int) that searches across contacts, jobs, invoices, and products returning unified results with entity type
- **inputs**: All tsvector-enabled tables
- **outputs**: search_all function created
- **dependencies**: [fts-006]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Function returns unified search results

#### Task: fts-008
- **title**: Create contact-specific search function
- **description**: Create a PostgreSQL function search_contacts(query text, org_id int) that performs weighted full-text search on contacts with French configuration
- **inputs**: contacts table, French search config
- **outputs**: search_contacts function created
- **dependencies**: [fts-002, fts-006]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Function returns relevant contact results

#### Task: fts-009
- **title**: Create job-specific search function
- **description**: Create a PostgreSQL function search_jobs(query text, org_id int) that performs weighted full-text search on jobs with French configuration
- **inputs**: jobs table, French search config
- **outputs**: search_jobs function created
- **dependencies**: [fts-003, fts-006]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Function returns relevant job results

#### Task: fts-010
- **title**: Implement fuzzy search using trigram similarity
- **description**: Create PostgreSQL function fuzzy_search(query text, org_id int) that combines trigram similarity with full-text search for better typo handling
- **inputs**: contacts table, pg_trgm extension
- **outputs**: fuzzy_search function created
- **dependencies**: [idx-012]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Fuzzy search finds matches despite typos

#### Task: fts-011
- **title**: Create search result ranking function
- **description**: Create PostgreSQL function that ranks search results by relevance using ts_rank_cd and returns results ordered by relevance
- **inputs**: Search queries
- **outputs**: Ranking function created
- **dependencies**: [fts-007]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Results ranked by relevance

#### Task: fts-012
- **title**: Create search highlighting function
- **description**: Create PostgreSQL function that highlights search term matches in results using ts_headline for display in UI
- **inputs**: Search queries, text content
- **outputs**: Highlight function created
- **dependencies**: [fts-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Search terms highlighted in results

#### Task: fts-013
- **title**: Backfill search vectors for existing data
- **description**: Create and execute migration to populate search_vector columns for all existing records in contacts, jobs, invoices, products tables
- **inputs**: All tables with search_vector columns
- **outputs**: All existing records have search_vector populated
- **dependencies**: [fts-002, fts-003, fts-004, fts-005]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: All existing records have searchable content

#### Task: fts-014
- **title**: Create search suggestions function
- **description**: Create PostgreSQL function get_search_suggestions(partial_query text) that returns suggested search terms based on trigram similarity
- **inputs**: contacts, products tables
- **outputs**: Suggestions function created
- **dependencies**: [fts-010]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Function returns relevant suggestions

#### Task: fts-015
- **title**: Document full-text search implementation
- **description**: Create documentation covering the full-text search implementation, French configuration, weight assignments, and usage guidelines
- **inputs**: All FTS functions and configurations
- **outputs**: FTS documentation file
- **dependencies**: [fts-001, fts-013]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Documentation complete and accurate

---

### Category: Data Migration from Legacy Systems

#### Task: dmig-001
- **title**: Create legacy data assessment questionnaire
- **description**: Create questionnaire for French artisans to assess their current data sources including Excel spreadsheets, other CRM systems, paper records, accounting software
- **inputs**: Common French artisan CRM data formats
- **outputs**: Assessment questionnaire document
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Questionnaire covers all common data scenarios

#### Task: dmig-002
- **title**: Create CSV import schema documentation
- **description**: Document the expected CSV format for importing contacts, jobs, invoices, and products from legacy systems
- **inputs**: Mini-CRM schema
- **outputs**: CSV import documentation with examples
- **dependencies**: [schema-001, schema-002, schema-004, schema-006, schema-008]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Documentation matches import function requirements

#### Task: dmig-003
- **title**: Create CSV import function for contacts
- **description**: Create PostgreSQL function import_contacts_from_csv(csv_data text, org_id int) that parses CSV data and imports contacts with proper validation
- **inputs**: CSV data, organizations table
- **outputs**: import_contacts_from_csv function created
- **dependencies**: [schema-004, dmig-002]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Function imports CSV contacts correctly

#### Task: dmig-004
- **title**: Create CSV import function for jobs
- **description**: Create PostgreSQL function import_jobs_from_csv(csv_data text, org_id int) that parses CSV data and imports jobs with proper validation
- **inputs**: CSV data, organizations table
- **outputs**: import_jobs_from_csv function created
- **dependencies**: [schema-006, dmig-002]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Function imports CSV jobs correctly

#### Task: dmig-005
- **title**: Create CSV import function for invoices
- **description**: Create PostgreSQL function import_invoices_from_csv(csv_data text, org_id int) that parses CSV data and imports invoices with proper validation
- **inputs**: CSV data, organizations table
- **outputs**: import_invoices_from_csv function created
- **dependencies**: [schema-008, dmig-002]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Function imports CSV invoices correctly

#### Task: dmig-006
- **title**: Create Excel import tool using Python/pandas
- **description**: Create Python script that reads Excel files (.xlsx, .xls) and converts them to CSV format for import, handling French date formats (DD/MM/YYYY) and number formats
- **inputs**: Excel file
- **outputs**: Python script and converted CSV
- **dependencies**: [dmig-002]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Script correctly parses French-formatted Excel files

#### Task: dmig-007
- **title**: Create import staging tables
- **description**: Create temporary staging tables (import_staging_contacts, import_staging_jobs, import_staging_invoices) for data validation before committing to production tables
- **inputs**: Production table structures
- **outputs**: Staging tables created
- **dependencies**: [schema-004, schema-006, schema-008]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Staging tables have all necessary validation columns

#### Task: dmig-008
- **title**: Create data validation functions for imports
- **description**: Create PostgreSQL functions to validate imported data including email format, phone format, date ranges, required fields, and referential integrity
- **inputs**: Staging tables
- **outputs**: Validation functions created
- **dependencies**: [dmig-007]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Validation functions identify all data issues

#### Task: dmig-009
- **title**: Create duplicate detection for contact imports
- **description**: Create PostgreSQL function detect_contact_duplicates(org_id int) that identifies potential duplicate contacts based on email, phone, name similarity
- **inputs**: Contacts table, staging table
- **outputs**: Duplicate detection function created
- **dependencies**: [dmig-007, idx-012]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Function correctly identifies duplicate candidates

#### Task: dmig-010
- **title**: Create merge contacts function
- **description**: Create PostgreSQL function merge_contacts(primary_id int, secondary_id int) that merges duplicate contacts keeping primary and updating foreign keys
- **inputs**: Duplicate contact IDs
- **outputs**: Merge function created
- **dependencies**: [dmig-009]
- **priority**: medium
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Merged contact has all related data

#### Task: dmig-011
- **title**: Create import progress tracking table
- **description**: Create import_jobs table to track ongoing import operations with status, progress percentage, error counts, and rollback capability
- **inputs**: None
- **outputs**: import_jobs table created
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Import progress tracked accurately

#### Task: dmig-012
- **title**: Create import summary report function
- **description**: Create PostgreSQL function generate_import_summary(import_job_id int) that generates a report of imported records, skipped duplicates, and errors
- **inputs**: import_jobs table, staging tables
- **outputs**: Summary report function created
- **dependencies**: [dmig-011]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Report accurately reflects import results

#### Task: dmig-013
- **title**: Create rollback import function
- **description**: Create PostgreSQL function rollback_import(import_job_id int) that removes all records created by a specific import operation
- **inputs**: import_jobs table
- **outputs**: Rollback function created
- **dependencies**: [dmig-011]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: database
- **validation**: Rollback removes all imported records

#### Task: dmig-014
- **title**: Test import with sample French artisan data
- **description**: Create sample data representing typical French artisan (plumber, electrician) contacts, jobs, and invoices for testing import functionality
- **inputs**: Common French artisan business data
- **outputs**: Sample data files
- **dependencies**: [dmig-003, dmig-004, dmig-005]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: database
- **validation**: Sample data imports successfully

#### Task: dmig-015
- **title**: Document import/export procedures for end users
- **description**: Create user-facing documentation explaining how to export data from common systems and import into Mini-CRM
- **inputs**: Import functions
- **outputs**: User documentation file
- **dependencies**: [dmig-003, dmig-004, dmig-005, dmig-006]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Documentation is clear and actionable

#### Task: dmig-016
- **title**: Create API endpoints for bulk data import
- **description**: Create Nuxt API endpoints (or backend endpoints) for bulk data import via file upload with validation and progress tracking
- **inputs**: Import functions, file upload handling
- **outputs**: API endpoints created
- **dependencies**: [dmig-003, dmig-004, dmig-005]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: API accepts and processes file uploads

#### Task: dmig-017
- **title**: Create data export function for portability
- **description**: Create PostgreSQL function export_org_data(org_id int) that exports all organization data to JSON format for data portability
- **inputs**: Organization ID
- **outputs**: export_org_data function created
- **dependencies**: [rls-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: database
- **validation**: Export contains all organization data

#### Task: dmig-018
- **title**: Create common CRM migration adapters
- **description**: Create adapter scripts for common French CRM systems (Sage, Cegid, EBalloon) that transform their export formats to Mini-CRM CSV format
- **inputs**: CRM export format specifications
- **outputs**: Adapter scripts for common CRMs
- **dependencies**: [dmig-