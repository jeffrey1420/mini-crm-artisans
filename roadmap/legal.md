# Legal & Compliance Roadmap — Mini-CRM

## Objectives

- Establish a fully compliant French legal entity for the Mini-CRM SaaS business targeting French artisans
- Achieve GDPR/CNIL compliance for a B2B self-hosted CRM product serving French businesses (plumbers, electricians, carpenters)
- Publish legally compliant Terms of Service (CGV), Privacy Policy (RGPD), and cookie consent mechanisms
- Implement required data subject rights (erasure, portability, access) with technical enforcement
- Define clear subscription terms, invoicing rules, and dispute resolution procedures under French law
- Establish security and breach response protocols meeting French cyber insurance requirements

## Subdomains

1. Corporate & Business Structure (SARL/SAS/micro-entreprise choice, registration, fiscal)
2. Data Protection & Privacy (GDPR/CNIL compliance, DPA, privacy policy, data rights)
3. Commercial Terms & Consumer Law (CGV, subscription terms, invoicing, cancellation)
4. Technical Security & Breach Response (pentesting, incident response, cyber insurance)
5. Intellectual Property & Ownership (code ownership, data ownership, generated content)
6. Third-Party & Sub-processor Compliance (SCCs, processor list, vendor due diligence)

## Milestones

- **M1 — Corporate Foundation (Week 1–4)**: Finalize company structure decision, begin registration
- **M2 — Core Legal Documents (Week 4–8)**: Draft CGV, Privacy Policy, DPA template, cookie policy
- **M3 — Technical Data Rights (Week 6–12)**: Implement data export, erasure, portability features
- **M4 — Security & Compliance Infrastructure (Week 10–16)**: Pentest, breach response plan, cyber insurance
- **M5 — Publication & Go-Live (Week 14–18)**: Legal pages live, subscription system operational, onboarding compliance

## Task Categories

---

### Category: Company Formation

#### Task: CF_001
- **title**: Research micro-entreprise vs SAS structure for SaaS business
- **description**: Analyze French legal structures (micro-entreprise vs SAS vs SARL) for a B2B SaaS company serving French artisans. Evaluate tax implications (TVA, IR vs IS), social contributions, liability protection, fundraising potential, and administrative burden. Consult a French accountant (expert-comptable) or use official URSSAF/DGFIP resources.
- **inputs**: Business revenue projections, owner salary needs, planned investment, long-term exit strategy
- **outputs**: Decision document comparing structures with recommended choice and rationale
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Document produced with comparison table and recommendation

#### Task: CF_002
- **title**: Verify micro-entreprise thresholds and TVA implications for SaaS
- **description**: Check current French micro-entreprise thresholds (CA maximum: €77,700 for services in 2024). Determine if the SaaS subscription model qualifies as a "prestation de services". Assess optional vs mandatory TVA enrollment thresholds and implications for €29/49/79/month pricing.
- **inputs**: Current French DGFIP threshold figures, business model description
- **outputs**: Threshold analysis document showing at what revenue level TVA becomes mandatory
- **dependencies**: [CF_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Document with current threshold numbers and implications for pricing

#### Task: CF_003
- **title**: Register company with INSEE and obtain SIREN/SIRET
- **description**: Complete French company registration process via INSEE. For SAS: file statuts with greffe du tribunal de commerce. For micro-entreprise: register via guichet-entreprises.gouv.fr or formalites-entreprises.greffier.com. Obtain SIREN (9 digits) and SIRET (14 digits).
- **inputs**: Company name, address, activity description (code NAF/APE), owner identity documents
- **outputs**: SIREN/SIRET numbers, INSEE registration confirmation
- **dependencies**: [CF_001, CF_002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: SIREN/SIRET obtained and confirmed via INSEE directory

#### Task: CF_004
- **title**: Register for TVA (VAT) if threshold exceeded or optional enrollment
- **description**: If revenue exceeds micro-entreprise threshold (€77,700 for services), register for TVA collection. Also evaluate voluntary TVA registration for SAS to reclaim TVA on expenses. Complete Form P0 PL micro-entreprise or Immatriculation RCS for SAS. Get TVA intra-community number for EU transactions.
- **inputs**: SIREN/SIRET, revenue projections, expense estimates
- **outputs**: TVA number (FR + 2 digits + 9 digits + 2 digits), registration confirmation
- **dependencies**: [CF_003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: TVA number obtained from DGFIP

#### Task: CF_005
- **title**: Open dedicated business bank account
- **description**: Open a professional bank account (compte bancaire professionnel) for the SAS or micro-entreprise. Required for SAS; recommended for micro-entreprise to separate finances. Compare offerings from Qonto, Shine, N26 Business, BNP Paribas Pro, Société Générale. Required for Stripe payouts if using payment processing.
- **inputs**: Company registration documents (SIREN, statuts), owner ID, KYB documents
- **outputs**: Business bank account IBAN, account confirmation letter
- **dependencies**: [CF_003]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Bank account opened and documented

#### Task: CF_006
- **title**: Draft and deposit SAS statuts (if SAS chosen)
- **description**: Draft articles of association (statuts) for SAS including: company name, registered office address, share capital (€1 minimum), shareholder(s), president, corporate purpose (objet social), decision-making rules, profit distribution, dissolution clauses. File with greffe du tribunal de commerce. Consider using a legal template or notary for complex share structures.
- **inputs**: Company name, shareholder details, capital structure, management preferences
- **outputs**: Dated and signed statuts, greffe filing receipt, KBis extract
- **dependencies**: [CF_001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: legal
- **validation**: KBis extract received showing company registration

#### Task: CF_007
- **title**: Appoint expert-comptable (French accountant)
- **description**: Hire a French chartered accountant (expert-comptable) for annual accounts, TVA returns (caisses TVA), payroll if applicable, and tax advice. Find via l'Ordre des Experts-Comptables directory. Required for SAS beyond micro-entreprise thresholds. Get quotes from 2-3 for comparison.
- **inputs**: Company structure, expected transaction volume, number of shareholders
- **outputs**: Signed accounting mandate, accountant contact details
- **dependencies**: [CF_001, CF_003]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Engagement letter signed

#### Task: CF_008
- **title**: Register domain name and verify trademark availability
- **description**: Register the company domain name (e.g., minicrm.fr or similar). Check INPI trademark database (marques.inpi.fr) to verify the company/product name is not already registered as a trademark in classes 35 (advertising/commercial management) and 42 (software/IT). File preliminary trademark application if available.
- **inputs**: Desired company/product name, domain options
- **outputs**: Domain registration confirmation, trademark search results
- **dependencies**: [CF_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Domain registered, trademark search documented

#### Task: CF_009
- **title**: Register for French professional insurance (RC Professionnelle)
- **description**: Check if RC Professionnelle (professional liability insurance) is required. For certain activities, this is mandatory. Even if not mandatory for SaaS, obtain quotes from insurers like AXA, MMA, Hiscox, Qover for product liability coverage. Required for some French B2B contracts.
- **inputs**: Business activity description, revenue, any existing coverage
- **outputs**: RC Professionnelle policy or quote documentation
- **dependencies**: [CF_003]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Policy in place or documented quote obtained

#### Task: CF_010
- **title**: Register for URSSAF and social contributions (micro-entreprise)
- **description**: If micro-entreprise: register with URSSAF via secu-entreprises.gouv.fr. Understand payment schedule (mensuelle or trimestrielle). Calculate social contribution rate for "prestations de services" (~22%). Set up automated URSSAF payments. If SAS: register for Rodrigues/URSSAF as employer if hiring.
- **inputs**: Company structure decision, revenue projections, personal ID (SIREN)
- **outputs**: URSSAF registration, payment schedule confirmed
- **dependencies**: [CF_001, CF_003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: URSSAF account active

#### Task: CF_011
- **title**: Determine applicable accounting standards (PCG vs IFRS for SaaS)
- **description**: Determine which French accounting standards apply. Micro-entreprise can use "comptabilité simplifiée" (livre des recettes, registre des achats). SAS must maintain full double-entry accounting per PCG (Plan Comptable Général). Evaluate whether to voluntarily adopt IFRS for scalability if raising funds later.
- **inputs**: Company structure, funding plans, transaction volume
- **outputs**: Accounting standards decision document with implementation requirements
- **dependencies**: [CF_001]
- **priority**: medium
- **agent_type**: legal
- **validation**: Document specifying applicable standards

#### Task: CF_012
- **title**: Publish legal notices on website (mentions légales)
- **description**: Create French "mentions légales" page per Loi pour la Confiance dans l'Économie Numérique (LCEN) requirements. Must include: company name, SARL/SAS/micro-entreprise designation, SIREN, RCS location, capital (for SAS), registered office address, phone, email, director name, VAT number, CNIL declaration (or now RIPD reference), hosting provider. This is mandatory for any French commercial website.
- **inputs**: Company registration details, hosting provider info, director details
- **outputs**: Live mentions légales page on website
- **dependencies**: [CF_003, CF_004]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Page live and accessible, contains all required elements per LCEN

#### Task: CF_013
- **title**: Register with Data Protection Officer service if required
- **description**: For CNIL compliance, determine if a DPO is required. Under GDPR Article 37, DPO required if core activity involves regular and systematic monitoring of individuals OR large-scale processing of special categories. For a B2B CRM, evaluate necessity. Even if not mandatory, designate a privacy contact. Register with CNIL if processing requires (note: CNIL no longer requires broad notification for most processing).
- **inputs**: Data processing description, scale of processing, types of data subjects
- **outputs**: DPO designation decision or privacy contact info
- **dependencies**: [CF_003]
- **priority**: medium
- **agent_type**: legal
- **validation**: DPO decision documented

#### Task: CF_014
- **title**: File for electronic invoicing compliance (CFE/TVA)
- **description**: France is mandating electronic invoicing for B2B transactions (2024-2026 rollout via Chorus Pro). Determine timeline applicability for the Mini-CRM's own B2B purchases/invoices. Also determine if the product itself should support e-invoicing for artisan customers. Monitor government timeline for mandatory e-invoicing.
- **inputs**: B2B invoice volumes, DGFIP e-invoicing timeline
- **outputs**: E-invoicing compliance plan for company operations and/or product feature
- **dependencies**: [CF_004]
- **priority**: medium
- **agent_type**: legal
- **validation**: Compliance timeline documented

#### Task: CF_015
- **title**: Evaluate need for a shareholder agreement (pacte d'actionnaires)
- **description**: If SAS with multiple shareholders, draft a shareholder agreement covering: transfer restrictions (clauses d'agrément, préemption), governance rights, dilution provisions, drag-along/tag-along clauses, deadlock resolution, exit mechanisms. Even for single-shareholder SAS, review whether a future investment might require this.
- **inputs**: Shareholder structure, future fundraising plans
- **outputs**: Shareholder agreement draft or documented decision not to have one
- **dependencies**: [CF_006]
- **priority**: low
- **agent_type**: legal
- **validation**: Agreement drafted or decision documented

#### Task: CF_016
- **title**: Assess applicable commercial court jurisdiction (Tribunal de Commerce)
- **description**: Determine the competent Tribunal de Commerce for disputes related to the company. For SAS, the registered office determines jurisdiction. For commercial disputes with customers, define jurisdiction clause in CGV (must be justified and not unfair per French consumer law). Ensure arbitration/mediation clause is properly drafted.
- **inputs**: Company registered office address
- **outputs**: Jurisdiction clause for CGV, registered office decision
- **dependencies**: [CF_003, CF_006]
- **priority**: medium
- **agent_type**: legal
- **validation**: Jurisdiction correctly determined

#### Task: CF_017
- **title**: Register for self-employed social security (SSI for micro-entreprise)
- **description**: For micro-entreprise, register with the Sécurité Sociale des Indépendants (SSI) via secu-independants.gouv.fr. Understand coverage: maladie, maternité, retraite, invalidité-décès. Compare with general regime for SAS. The SSI replaces the old RSI regime.
- **inputs**: Company structure, owner profile
- **outputs**: SSI registration confirmation
- **dependencies**: [CF_001, CF_010]
- **priority**: high
- **agent_type**: legal
- **validation**: SSI registration complete

#### Task: CF_018
- **title**: Define CIF (Contribution à la Formation Professionnelle) obligations
- **description**: All businesses in France contribute to professional training (CIF). Micro-entreprise and SAS both pay formation professionnelle contributions. Determine the rate applicable to the company structure and register with OPCO if needed. These contributions fund employee training rights.
- **inputs**: Company structure, employee count
- **outputs**: CIF obligations documented, registration with OPCO if needed
- **dependencies**: [CF_001]
- **priority**: low
- **agent_type**: legal
- **validation**: CIF obligations understood and registered

#### Task: CF_019
- **title**: Open Pépite (participation reserve) account if eligible
- **description**: For SAS, the account for "participation des salariés aux résultats" requires a blocked account at a bank or with a notary. Determine if SAS with employees needs this. For micro-entreprise without employees, not applicable.
- **inputs**: Company structure, employee count, revenue
- **outputs**: Participation account opened or documented exemption
- **dependencies**: [CF_001, CF_006]
- **priority**: low
- **agent_type**: legal
- **validation**: Participation account established if required

#### Task: CF_020
- **title**: Obtain mandatory business permits if applicable (申报 business license)
- **description**: Some business activities in France require specific permits or licenses (commercial license, artisan card for certain métiers). As a SaaS business, likely no specific permit needed beyond standard company registration. Document the analysis. However, if serving artisans who must be verified as licensed professionals, determine how to verify their registration.
- **inputs**: Business activity description, list of required French business permits
- **outputs**: Permit requirements analysis document
- **dependencies**: [CF_001]
- **priority**: medium
- **agent_type**: legal
- **validation**: Permit analysis complete and documented

---

### Category: GDPR Compliance (CNIL)

#### Task: GDPR_001
- **title**: Conduct full data mapping (inventory of all personal data processed)
- **description**: Map all personal data flows across the Mini-CRM product. Identify: what data is collected (customer/employee names, emails, phone numbers, addresses, company info, invoice data, usage logs), how it's collected (web forms, API, imports), where it's stored (database, file storage, backups), who can access it (employees, subprocessors), retention periods, and legal basis for each processing activity. Create a data flow diagram.
- **inputs**: Product architecture documentation, database schema, API documentation
- **outputs**: Data inventory document with data flow diagrams, processing register (article 30 GDPR)
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: legal
- **validation**: Article 30 GDPR register created covering all processing activities

#### Task: GDPR_002
- **title**: Identify legal basis for each processing activity (contract, legitimate interest, consent)
- **description**: For each data processing activity identified in GDPR_001, determine the appropriate legal basis under GDPR Article 6: (a) consent, (b) contract, (c) legal obligation, (d) vital interests, (e) public task, (f) legitimate interests. For a B2B CRM: processing to provide the service is typically "contract" (Article 6(1)(b)). Marketing to existing customers may be "legitimate interest" with LPP (Loi Informatique et Libertés) compliance. Document each.
- **inputs**: Data inventory from GDPR_001, product feature descriptions
- **outputs**: Legal basis register mapping each processing activity to GDPR Article 6 basis
- **dependencies**: [GDPR_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Document with legal basis for each of 10+ processing activities

#### Task: GDPR_003
- **title**: Draft Records of Processing Activities (RoPA) per Article 30 GDPR
- **description**: Create formal RoPA document in French and/or English as required by Article 30 GDPR. Must include for each processing activity: name and contact of controller/processor, purposes, categories of data subjects, categories of personal data, categories of recipients, third-country transfers, retention periods, security measures, and legal basis. This is mandatory for companies >250 employees or those processing at scale.
- **inputs**: Data inventory, legal basis register
- **outputs**: RoPA document (Article 30 record), in format suitable for CNIL inspection
- **dependencies**: [GDPR_001, GDPR_002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: RoPA complete and signed by data controller

#### Task: GDPR_004
- **title**: Implement privacy by design in product development workflow
- **description**: Integrate privacy by design (GDPR Article 25) into the product development process. Define default privacy settings (minimize data collection), ensure data minimization in all features, implement pseudonymization where possible, add privacy review step in feature development lifecycle. Create internal "Privacy Review Checklist" for new features.
- **inputs**: Current development workflow documentation
- **outputs**: Privacy by design checklist, updated development workflow with privacy gates
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Checklist exists, developers trained on usage

#### Task: GDPR_005
- **title**: Assess necessity of Data Protection Impact Assessment (DPIA)
- **description**: Per GDPR Article 35, determine if a DPIA is required. DPIA required if processing is likely to result in high risk to rights and freedoms, especially: systematic monitoring, processing of special categories, large-scale profiling. For a B2B CRM storing client contact data, evaluate whether risk is "high". If yes, conduct full DPIA. If no, document the rationale.
- **inputs**: Data inventory, processing scale description, types of data subjects (artisans)
- **outputs**: DPIA requirement decision document with rationale, or completed DPIA
- **dependencies**: [GDPR_001, GDPR_003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Decision documented (DPIA required = yes/no + rationale)

#### Task: GDPR_006
- **title**: Conduct DPIA if required for systematic monitoring of artisans
- **description**: If DPIA deemed necessary (GDPR_005), conduct full DPIA including: description of processing, necessity/proportionality assessment, risk identification, risk mitigation measures, consultation with DPO (if appointed). Publish DPIA summary on website if required by CNIL for high-risk processing.
- **inputs**: DPIA decision, data flows, risk assessment framework
- **outputs**: Completed DPIA document with mitigation measures
- **dependencies**: [GDPR_005]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: legal
- **validation**: DPIA completed, reviewed, and measures implemented

#### Task: GDPR_007
- **title**: Define and document data retention periods for all data categories
- **description**: Define specific retention periods for all personal data categories in the CRM: customer account data (duration of contract + X years for legal), invoice data (10 years per French commercial code), logs (duration TBD based on security needs), backup data (how long backups retain data), data from deleted accounts. Document in retention policy. Implement automated deletion schedules.
- **inputs**: Data inventory, French legal retention requirements (code de commerce 10 ans for invoices)
- **outputs**: Data retention policy document with per-category retention periods
- **dependencies**: [GDPR_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Retention policy documented, automated deletion scheduled in database

#### Task: GDPR_008
- **title**: Implement access controls and least-privilege data access
- **description**: Implement technical and organizational measures per GDPR Article 32. Ensure role-based access control (RBAC) in the CRM application: only collect data needed for each role, no universal admin accounts, audit logs for who accessed what data. Apply principle of least privilege to all internal systems and databases.
- **inputs**: Application architecture, list of user roles
- **outputs**: RBAC implementation, access control matrix document
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Access control tested, no unauthorized access possible in penetration test

#### Task: GDPR_009
- **title**: Implement data encryption at rest and in transit
- **description**: Ensure all personal data is encrypted at rest (AES-256 or equivalent for database, file storage, backups) and in transit (TLS 1.2+ for all connections, HSTS for web traffic). Document encryption key management procedures. For self-hosted deployments, provide encryption guidance to customers.
- **inputs**: Infrastructure documentation, hosting environment details
- **outputs**: Encryption implementation documentation, key management procedures
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Encryption verified in security review or pentest

#### Task: GDPR_010
- **title**: Set up process for handling data subject rights requests (DSR)
- **description**: Create internal workflow for handling GDPR data subject requests (access, rectification, erasure, portability, restriction). Define intake process (email/form), verification of identity, response timeline (1 month per GDPR), escalation procedure. Train relevant staff. Track all DSR requests in a log.
- **inputs**: List of data subject rights under GDPR (Articles 15-22)
- **outputs**: DSR handling procedure, request intake form, response template, tracking log
- **dependencies**: [GDPR_001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Procedure documented and staff trained

#### Task: GDPR_011
- **title**: Create internal GDPR training program for employees
- **description**: Develop GDPR training covering: what personal data is, data subject rights, data breach notification requirements, secure data handling practices, phishing awareness. Record training completion. Update training annually or when regulations change.
- **inputs**: GDPR fundamentals content, company data handling procedures
- **outputs**: Training materials, training completion records for all staff
- **dependencies**: [GDPR_001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Training delivered, completion records on file

#### Task: GDPR_012
- **title**: Implement pseudonymization for appropriate data processing
- **description**: Where full anonymization is not feasible, implement pseudonymization (GDPR Article 4(5)) to reduce identifiability. Replace direct identifiers (names, emails, phone numbers) with tokens in analytics/logs where possible. Document which data is pseudonymized vs anonymized vs encrypted.
- **inputs**: Data inventory, application architecture
- **outputs**: Pseudonymization implementation, documentation of what's pseudonymized
- **dependencies**: [GDPR_001]
- **priority**: medium
- **agent_type**: devops
- **validation**: Pseudonymization implemented and documented

#### Task: GDPR_013
- **title**: Conduct CNIL-specific compliance review
- **description**: CNIL has issued specific guidance beyond GDPR (Loi Informatique et Libertés as amended 2018). Review CNIL's specific recommendations for B2B SaaS: cookie consent requirements, right to be informed (transparency), proportionality of data collected. Cross-reference with CNIL's 2018 reform guidance and existing délibérations.
- **inputs**: CNIL website guidance, GDPR documentation
- **outputs**: CNIL compliance gap analysis document
- **dependencies**: [GDPR_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Gap analysis complete, action items identified

#### Task: GDPR_014
- **title**: Register with CNIL's DPOP (Data Protection Officer registry)
- **description**: Determine if company needs to formally register a DPO with CNIL. While GDPR does not require registration per se, CNIL provides a DPO designation tool for companies that appoint one voluntarily. If DPO appointed (mandatory or voluntary), ensure they are listed on CNIL's registry. Even if not mandatory, document why not applicable.
- **inputs**: DPO appointment decision, company size, processing description
- **outputs**: DPO registration or non-requirement documentation
- **dependencies**: [GDPR_005]
- **priority**: low
- **agent_type**: legal
- **validation**: CNIL DPO registration complete or documented exemption

#### Task: GDPR_015
- **title**: Implement automated DSR response system in CRM product
- **description**: Build technical functionality in the CRM to handle data subject requests automatically or semi-automatically. For self-hosted: provide customers with tools to export their data (CSV/JSON), delete their data, or modify their data directly from the UI. For SaaS components (billing, support): create internal DSR tooling.
- **inputs**: DSR handling procedure, data inventory, application features
- **outputs**: Self-service DSR features in CRM product
- **dependencies**: [GDPR_010, GDPR_001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: DSR features functional and testable

#### Task: GDPR_016
- **title**: Establish lawful transfer mechanism for any US-based sub-processors
- **description**: If using US-based vendors (e.g., SendGrid, Stripe, Google Analytics), verify their compliance with EU-US Data Privacy Framework (DPF, adopted July 2023) or implement Standard Contractual Clauses. For each US vendor: check DPF certification status, document the transfer mechanism, update Privacy Policy accordingly.
- **inputs**: List of US-based vendors, SCC templates
- **outputs**: Transfer mechanism documentation for each US sub-processor
- **dependencies**: [PP_001, SCC_001]
- **priority**: high
- **agent_type**: legal
- **validation**: All US transfers covered by DPF or SCC

#### Task: GDPR_017
- **title**: Define and implement data minimization controls
- **description**: Audit what data is truly necessary for each feature. Remove collection of non-essential personal data fields. Implement collection forms that only request minimum data. Add field-level data classification to identify optional vs required fields. Document data minimization decisions per feature.
- **inputs**: Data inventory, feature list
- **outputs**: Data minimization review per feature, removal of non-essential fields
- **dependencies**: [GDPR_001]
- **priority**: medium
- **agent_type**: product
- **validation**: Data minimization review complete, non-essential fields removed

#### Task: GDPR_018
- **title**: Conduct annual GDPR compliance review
- **description**: Establish an annual GDPR compliance review process. Review: data inventory updates, new processing activities, sub-processor list changes, legal basis changes, retention period adherence, DSR response metrics, breach log, training completion. Document findings and remediation items.
- **inputs**: Previous year's GDPR documentation, DSR logs, incident logs
- **outputs**: Annual GDPR review report with action items
- **dependencies**: [GDPR_001, GDPR_010, GDPR_011]
- **priority**: medium
- **agent_type**: legal
- **validation**: Annual review completed and documented

#### Task: GDPR_019
- **title**: Implement logging and monitoring for GDPR Article 32 security
- **description**: Implement security logging per GDPR Article 32(1)(b): log all access to personal data (who accessed, when, what data), log all administrative actions, implement intrusion detection, set up alerts for anomalous access patterns. Retention of logs must be defined (typically 6-12 months).
- **inputs**: Infrastructure, GDPR Article 32 requirements
- **outputs**: Security logging implementation, log retention policy
- **dependencies**: [GDPR_008, GDPR_009]
- **priority**: high
- **agent_type**: devops
- **validation**: Logging active, tested, logs retained per policy

#### Task: GDPR_020
- **title**: Implement automated vulnerability scanning and patching
- **description**: Per GDPR Article 32(1)(d), implement processes for regular testing, assessing, and evaluating effectiveness of security measures. Set up automated vulnerability scanning (e.g., OWASP ZAP, Snyk, npm audit), dependency vulnerability alerts, and defined patching timelines for critical/high/critical vulnerabilities.
- **inputs**: Application codebase, infrastructure
- **outputs**: Vulnerability scanning setup, patching SLA document
- **dependencies**: [GDPR_008]
- **priority**: high
- **agent_type**: devops
- **validation**: Scanning active, alerts configured, patching SLA defined

---

### Category: Data Processing Agreement (DPA) Template

#### Task: DPA_001
- **title**: Determine controller vs processor role for Mini-CRM
- **description**: Clarify the data protection roles. The Mini-CRM is the "processor" when handling personal data of the customer's clients (artisan's customers). The artisan customer is the "controller". Document this distinction clearly in the DPA. For the artisan's own account data, Mini-CRM acts as controller.
- **inputs**: Product description, customer data flows
- **outputs**: Role determination document specifying when Mini-CRM is controller vs processor
- **dependencies**: [GDPR_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Role determination documented and consistent with GDPR definitions

#### Task: DPA_002
- **title**: Draft GDPR-compliant Data Processing Agreement template
- **description**: Draft a DPA template per GDPR Article 28 requirements. Must include: subject matter and duration of processing, nature and purpose, type of personal data and categories of data subjects, controller's instructions, confidentiality obligations, security measures, sub-processor requirements, assistance with data subject rights, deletion/return obligations, audit rights.
- **inputs**: GDPR Article 28 requirements, product architecture, sub-processor list
- **outputs**: DPA template document in French and English
- **dependencies**: [GDPR_001, DPA_001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: legal
- **validation**: DPA template reviewed by legal counsel, covers all Article 28 elements

#### Task: DPA_003
- **title**: Define scope of processing instructions (what artisans can do with the CRM)
- **description**: Define in the DPA what "processing instructions" the controller (artisan customer) can give. Since it's self-hosted, the artisan controls their own data. Document what Mini-CRM will and will not do with that data. Include restrictions on processing special categories (health, biometric, financial data beyond invoices) unless explicitly agreed.
- **inputs**: Product feature list, data inventory
- **outputs**: Processing scope document defining permitted and prohibited processing types
- **dependencies**: [DPA_001, DPA_002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Scope clearly documented in DPA

#### Task: DPA_004
- **title**: Define sub-processor approval process and list initial sub-processors
- **description**: Per GDPR Article 28(2), the processor must not engage sub-processors without the controller's prior written authorization. Define the process for approving new sub-processors (notification period, objection rights). List initial sub-processors: e.g., cloud hosting provider, email service (SendGrid/Postmark), payment processor (Stripe), analytics provider.
- **inputs**: Current infrastructure, vendor contracts
- **outputs**: Sub-processor list, sub-processor approval clause for DPA
- **dependencies**: [DPA_002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Initial sub-processor list included in DPA or annex

#### Task: DPA_005
- **title**: Draft sub-processor liability and indemnification clauses
- **description**: Draft clauses addressing liability between controller and processor for sub-processor breaches. Per GDPR, processor remains liable to controller for sub-processor failures. Define indemnification for damages arising from processor's breach of DPA. Include limitation of liability carve-out for processor's indemnification obligations.
- **inputs**: GDPR liability framework, standard commercial liability provisions
- **outputs**: Liability and indemnification clauses in DPA
- **dependencies**: [DPA_002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Clause drafted and reviewed

#### Task: DPA_006
- **title**: Define data breach notification procedure and timelines in DPA
- **description**: Per GDPR Articles 33 and 34, define the breach notification procedure in the DPA. Processor must notify controller "without undue delay" (72 hours to CNIL if high risk). Define what constitutes a breach requiring notification, the notification format (must include: nature of breach, categories/approximate number of data subjects, likely consequences, measures taken), and escalation contacts.
- **inputs**: GDPR Articles 33-34, incident response plan
- **outputs**: Breach notification clause in DPA, notification template
- **dependencies**: [DPA_002, BR_001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Clause complete with timelines and content requirements

#### Task: DPA_007
- **title**: Define data deletion and return procedures at contract termination
- **description**: Per GDPR Article 28(3)(g), DPA must cover what happens at contract termination. Define: data return procedure (export format, timeline), data deletion procedure (verification of deletion), retention carve-outs (legal holds, regulatory requirements). Since self-hosted, define how customer exports data before termination.
- **inputs**: Data portability capabilities, GDPR Article 17 requirements
- **outputs**: Deletion/return clause in DPA, customer-facing termination guide
- **dependencies**: [DPA_002, GDPR_010]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Clause drafted, deletion procedures tested

#### Task: DPA_008
- **title**: Define audit rights clause for controller to verify processor compliance
- **description**: Per GDPR Article 28(3)(h), controller must be able to audit processor's compliance. Define: audit trigger conditions (annual, upon breach, upon reasonable request), audit scope (GDPR compliance, not proprietary code), audit format (self-assessment questionnaire / SAS 70 / on-site audit), cost allocation, confidentiality of audit findings.
- **inputs**: Standard audit clause precedents, controller audit needs
- **outputs**: Audit rights clause in DPA, standard audit questionnaire template
- **dependencies**: [DPA_002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Audit clause drafted with practical implementation details

#### Task: DPA_009
- **title**: Create DPA for European Economic Area (EEA) customers
- **description**: For customers outside France but within EEA, ensure DPA covers national variations. GDPR applies uniformly across EEA, but local laws (German BDSG, Austrian DSG, etc.) may add requirements. Create a single DPA that is GDPR-compliant across all EEA member states, referencing GDPR as the harmonized standard.
- **