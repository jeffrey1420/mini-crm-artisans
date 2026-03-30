# Legal & Compliance Roadmap — Mini-CRM

## Objectives

Ensure full legal and regulatory compliance for a French SaaS CRM product serving artisan businesses (plumbers, electricians, carpenters). The product is self-hosted per customer on OVH VPS with tiered pricing (€29/49/79/month). All activities must comply with French law, EU GDPR, CNIL requirements, and French consumer protection standards.

**Primary Objectives:**
- Establish legally sound company structure for Louis's team
- Achieve full GDPR/CNIL compliance for a B2B SaaS serving French artisans
- Protect intellectual property and define clear ownership rights
- Ensure all customer contracts (DPA, ToS, CGV) are legally valid under French law
- Implement required technical and organizational measures for data protection
- Establish security incident response capabilities
- Comply with French invoicing and billing regulations

**Target Outcomes:**
- Company legally formed and registered in France
- All legal documents (Privacy Policy, ToS, CGV, DPA) published and legally reviewed
- CNIL compliance documentation complete
- Security measures implemented and tested
- Ongoing compliance monitoring established

---

## Subdomains

1. **Corporate Structure** — Company formation, entity selection, registration
2. **Data Protection** — GDPR/CNIL compliance, DPA management, privacy documentation
3. **Contract Law** — Terms of Service, CGV, subscription terms, cancellation policies
4. **Consumer Rights** — French consumer law (Droit de la consommation), dispute resolution
5. **Financial Compliance** — Invoicing, mentions obligatoires, TVA, accounting
6. **Security & Breach** — Penetration testing, incident response, cyber insurance
7. **Intellectual Property** — Code ownership, data ownership, licensing
8. **Third-Party Compliance** — Sub-processor management, SCCs, vendor due diligence

---

## Milestones

### Phase 1: Foundation (Month 1-2)
- Complete company formation (SAS or micro-entreprise decision)
- Register with relevant French authorities (INPI, RCS, etc.)
- Obtain necessary business licenses and permits
- Open professional bank account

### Phase 2: Privacy Framework (Month 2-3)
- Draft and publish Privacy Policy (Politique de Confidentialité)
- Draft Data Processing Agreement (DPA) template
- Implement cookie consent solution (Axeptio)
- Create data retention and erasure procedures

### Phase 3: Contract Framework (Month 3-4)
- Draft Terms of Service (Conditions Générales de Vente — CGV)
- Create subscription terms and pricing documentation
- Implement cancellation (résiliation) procedures
- Establish dispute resolution mechanisms

### Phase 4: Security & Compliance (Month 4-6)
- Conduct penetration testing
- Implement security breach response plan
- Obtain cyber insurance
- Complete CNIL compliance documentation

### Phase 5: Ongoing Compliance (Month 6+)
- Annual reviews and updates
- Sub-processor list maintenance
- Security monitoring and testing
- CNIL reporting compliance

---

## Task Categories

---

### Category: Company Formation

#### Task: COMP-001
- **title**: Evaluate micro-entreprise vs SAS structure
- **description**: Analyze pros and cons of micro-entreprise (simplified regime, limits on revenue/expenses, easier administration) vs SAS (more formal, unlimited liability protection, better for growth, investor-ready) for Louis's team. Consider number of founders, expected revenue, need for investors, liability exposure, and administrative burden.
- **inputs**: Team size, expected revenue projections, investment plans, liability requirements
- **outputs**: Recommendation document comparing structures with pros/cons analysis
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Document delivered and reviewed by Louis's team

#### Task: COMP-002
- **title**: Register company name with INPI
- **description**: Conduct trademark search and register the company name/logo with INPI (Institut National de la Propriété Industrielle). Verify name availability and file appropriate trademark applications for classes 42 (software) and 35 (business management services).
- **inputs**: Desired company name, logo files, business activity description
- **outputs**: INPI registration confirmation, trademark certificate
- **dependencies**: [COMP-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Trademark certificate received from INPI

#### Task: COMP-003
- **title**: Register with RCS (Registre du Commerce et des Sociétés)
- **description**: Register the company with the Register of Commerce and Companies via Infogreffe or appropriate RCS registry. Prepare articles of association (statuts), file registration documents, obtain SIREN and SIRET numbers.
- **inputs**: Articles of association, founder identification documents, registered address proof
- **outputs**: SIREN/SIRET numbers, RCS registration certificate, KBis extract
- **dependencies**: [COMP-001, COMP-002]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: legal
- **validation**: KBis extract obtained

#### Task: COMP-004
- **title**: Register for TVA (VAT) with correct regime
- **description**: Determine appropriate TVA regime (franchise en base for micro-entreprise vs normal regime for SAS), register with HMRC equivalent (France: DGFIP), obtain TVA intracommunautaire number if needed for EU transactions, set up TVA accounting.
- **inputs**: Company structure decision, expected revenue, customer types (B2B EU)
- **outputs**: TVA number, registration confirmation, TVA regime documentation
- **dependencies**: [COMP-001, COMP-003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: TVA registration certificate obtained

#### Task: COMP-005
- **title**: Open professional bank account
- **description**: Open a dedicated professional bank account required for SAS. For micro-entreprise, open separate account if turnover exceeds €10,000/year. Research banks offering business accounts for small tech companies (Société Générale, BNP Paribas, Axa Banque, or online banks like Qonto, Manager.io).
- **inputs**: Company registration documents, KBis, identification documents
- **outputs**: Professional bank account opened, IBAN obtained
- **dependencies**: [COMP-003]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Bank account active with IBAN

#### Task: COMP-006
- **title**: Draft articles of association (statuts)
- **description**: Draft legally compliant articles of association for SAS including: company purpose (objet social), share capital (capital social), governance structure, founder rights, decision-making processes, dividend distribution rules, share transfer restrictions, and dissolution procedures. Have reviewed by notarial services or specialized lawyer.
- **inputs**: Founder agreements, share distribution plan, company purpose description
- **outputs**: Signed and dated statuts, certified copies
- **dependencies**: [COMP-001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: legal
- **validation**: Statuts signed by all founders, registered with RCS

#### Task: COMP-007
- **title**: Define share capital and founder equity分配
- **description**: Determine initial share capital amount (minimum €1 for SAS), allocate shares among founders (Louis's team), define vesting schedules if applicable, draft shareholder agreement (accord d'actionnaires) covering drag-along, tag-along, anti-dilution provisions.
- **inputs**: Founder list, roles and responsibilities, expected contributions
- **outputs**: Share allocation table, shareholder agreement document
- **dependencies**: [COMP-001, COMP-006]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: legal
- **validation**: Signed shareholder agreement, share certificates issued

#### Task: COMP-008
- **title**: Register for URSSAF and social contributions
- **description**: Register as employer or self-employed with URSSAF for social security contributions. Determine if founders are salariés (paid employees) or associés (unpaid), register appropriately for each status. Calculate and budget for charges sociales.
- **inputs**: Company structure, founder employment status, expected salary/dividends
- **outputs**: URSSAF registration, social security account numbers
- **dependencies**: [COMP-003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: URSSAF registration confirmation received

#### Task: COMP-009
- **title**: Obtain business insurance (RC Pro)
- **description**: Purchase Responsabilité Civile Professionnelle (RC Pro) insurance mandatory for certain activities and highly recommended for all businesses. Also consider Multirisque Pro insurance for office/staff coverage. Get quotes from multiple insurers (AXA, MMA, Generali, etc.).
- **inputs**: Business activity description, revenue projections, number of employees
- **outputs**: RC Pro insurance policy, certificate of insurance
- **dependencies**: [COMP-003]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Insurance policy active, certificate obtained

#### Task: COMP-010
- **title**: Define legal representation and management roles
- **description**: Appoint legal representative (président for SAS), define powers of the CEO, establish board of directors or directorship structure, create internal governance rules, define approval thresholds for contracts and expenditures.
- **inputs**: Company structure, founder roles, governance preferences
- **outputs**: Appointment documents, internal governance policy
- **dependencies**: [COMP-006]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Legal representative officially registered

#### Task: COMP-011
- **title**: Create legal entity operating checklist
- **description**: Develop comprehensive checklist of ongoing compliance obligations: annual accounts filing, AG (assemblée générale) requirements, statistical declarations (董), RC Pro renewal, TVA declaration schedule, social contributions deadlines. Create calendar with all recurring deadlines.
- **inputs**: Company type, regulatory requirements, filing deadlines
- **outputs**: Compliance calendar, operating checklist document
- **dependencies**: [COMP-003, COMP-004, COMP-008]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Calendar created, reminders configured

#### Task: COMP-012
- **title**: Assess need for DADS (Déclaration Automatisée des Données Sociales)
- **description**: If founders receive salaries, understand DADS/DSN (Déclaration Sociale Nominative) obligations. Set up DSN account if needed, determine filing cadence, budget for payroll if applicable.
- **inputs**: Founder employment structure, salary plans
- **outputs**: DSN registration or exemption confirmation
- **dependencies**: [COMP-008]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: DSN obligations clarified and addressed

#### Task: COMP-013
- **title**: Register domain name and establish online presence legally
- **description**: Register domain name (minicrm.fr or similar) matching company name. Verify WHOIS privacy compliance. Ensure website terms and privacy policy are in place before launching any marketing activities. Review GDPR implications of marketing cookies and analytics.
- **inputs**: Desired domain name, hosting provider (OVH)
- **outputs**: Domain registered, DNS configured, legal notices on website
- **dependencies**: [COMP-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Domain registered, website with legal notices live

#### Task: COMP-014
- **title**: Draft confidentiality and NDA agreements for internal use
- **description**: Create template NDA (accord de confidentialité) for employees, contractors, advisors, and potential investors. Ensure French law compliance, specify duration (typically 2-5 years for business secrets), scope, and permitted disclosures.
- **inputs**: Standard confidentiality terms, French labor law requirements
- **outputs**: NDA template, signing procedure
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: NDA template approved, ready for use

#### Task: COMP-015
- **title**: Develop intellectual property assignment agreements
- **description**: Create IP assignment agreements ensuring company owns all work product created by founders, employees, and contractors. Include copyright assignment, work-for-hire clauses, pre-existing IP carve-outs. Critical for protecting codebase and product.
- **inputs**: List of contributors, IP ownership requirements
- **outputs**: IP assignment agreements, invention assignment documents
- **dependencies**: [COMP-006]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Signed IP assignments from all contributors

---

### Category: GDPR Compliance (CNIL)

#### Task: GDPR-001
- **title**: Appoint Data Protection Officer (DPO) if required
- **description**: Determine if DPO is legally required (mandatory if core activity involves systematic monitoring of individuals or processing of sensitive data at large scale). Even if not mandatory, appoint voluntary DPO for good governance. Define DPO responsibilities, contact information, and ensure independence.
- **inputs**: Processing activities description, data types handled, scale of processing
- **outputs**: DPO appointment decision, DPO contact details, responsibility document
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: DPO appointed (voluntary or mandatory), contact published

#### Task: GDPR-002
- **title**: Conduct complete data mapping (inventaires des traitements)
- **description**: Create comprehensive inventory of all personal data processing activities as required by Article 30 GDPR. Document: data categories, purposes, legal basis, recipients, transfers, retention periods, security measures. Include both automated processing (software) and manual processing.
- **inputs**: System architecture, data flow diagrams, processing activities list
- **outputs**: Data processing register (registre des activités de traitement)
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: legal
- **validation**: Complete register document reviewed and approved

#### Task: GDPR-003
- **title**: Identify and document legal basis for each processing activity
- **description**: For each data processing purpose (customer management, invoicing, marketing, analytics, support), determine applicable legal basis under Article 6 GDPR: consent, contract performance, legal obligation, vital interests, public task, or legitimate interests. Document how each basis is met.
- **inputs**: Data processing register, processing purposes
- **outputs**: Legal basis documentation for each processing activity
- **dependencies**: [GDPR-002]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: legal
- **validation**: Each processing activity has documented legal basis

#### Task: GDPR-004
- **title**: Implement lawful consent mechanisms
- **description**: For processing requiring consent (e.g., marketing emails, non-essential cookies), implement clear, freely given, informed, unambiguous consent mechanisms. Consent must be granular, specific, and easily withdrawable. Implement consent records storage and retrieval.
- **inputs**: Consent requirements per processing activity
- **outputs**: Consent mechanism implemented, consent management system
- **dependencies**: [GDPR-003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Consent mechanism tested and functional

#### Task: GDPR-005
- **title**: Create Privacy Notice (information clause)
- **description**: Draft transparency information to be provided at data collection points per Articles 13-14 GDPR. Must include: identity of controller, DPO contact, purposes and legal basis, data recipients, transfers, retention periods, rights, right to withdraw consent, right to lodge complaint with CNIL, and whether provision is contractual requirement.
- **inputs**: Data processing register, legal basis documentation
- **outputs**: Privacy Notice text for all collection points
- **dependencies**: [GDPR-002, GDPR-003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Privacy Notice reviewed by legal counsel

#### Task: GDPR-006
- **title**: Implement data subject rights procedures
- **description**: Create procedures and technical systems to handle all GDPR data subject rights: right of access (Article 15), right to rectification (Article 16), right to erasure (Article 17), right to restriction (Article 18), data portability (Article 20), right to object (Article 21), and rights related to automated decision-making (Article 22). Define response timelines (1 month).
- **inputs**: List of data subject rights, current system capabilities
- **outputs**: Procedures documented, system capabilities implemented
- **dependencies**: [GDPR-002]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: Rights request handling procedure tested

#### Task: GDPR-007
- **title**: Conduct Data Protection Impact Assessment (DPIA)
- **description**: Perform DPIA as required by Article 35 GDPR for processing likely to result in high risk to individuals. Required for systematic profiling, large-scale processing of special categories, or monitoring of publicly accessible areas. Document methodology, risk assessment, and mitigation measures.
- **inputs**: Processing activities with high risk indicators
- **outputs**: Completed DPIA document with risk mitigation plan
- **dependencies**: [GDPR-002, GDPR-003]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: legal
- **validation**: DPIA documented and reviewed

#### Task: GDPR-008
- **title**: Implement data minimization and purpose limitation
- **description**: Review all data collection points to ensure only data necessary for stated purposes is collected (data minimization principle). Implement purpose limitation controls preventing use of data for incompatible purposes. Document purpose specifications for each data field.
- **inputs**: Data fields collected, stated purposes
- **outputs**: Data minimization audit report, field-by-field review
- **dependencies**: [GDPR-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Audit complete, unnecessary data fields removed or justified

#### Task: GDPR-009
- **title**: Define and implement data retention schedules
- **description**: Establish retention periods for each data category based on legal requirements (invoices: 10 years), contractual requirements, and legitimate business needs. Implement automated deletion for data past retention period. Document retention schedule and deletion procedures.
- **inputs**: Legal retention requirements, data categories, business needs
- **outputs**: Data retention schedule document, automated deletion system
- **dependencies**: [GDPR-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Retention schedule approved, deletion system tested

#### Task: GDPR-010
- **title**: Implement data accuracy procedures
- **description**: Establish procedures to ensure personal data remains accurate and up-to-date. Implement mechanisms for data subjects to exercise right to rectification. Define accuracy checking procedures, especially for customer contact data that changes frequently.
- **inputs**: Data categories, update frequency requirements
- **outputs**: Data accuracy procedures, rectification mechanism
- **dependencies**: [GDPR-006]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Accuracy procedures documented and implemented

#### Task: GDPR-011
- **title**: Establish security measures (Technical and Organizational Measures - TOMs)
- **description**: Implement appropriate technical and organizational security measures per Article 32 GDPR: encryption, access controls, pseudonymization, regular testing, backup procedures, incident response capabilities. Document measures implemented and their effectiveness.
- **inputs**: Risk assessment, current security posture
- **outputs**: Security measures documentation, implementation evidence
- **dependencies**: [GDPR-007]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: Security measures reviewed and approved

#### Task: GDPR-012
- **title**: Implement breach notification procedures
- **description**: Create procedures for detecting, assessing, and reporting personal data breaches within 72-hour timeline to CNIL (Article 33) and without undue delay to data subjects when high risk (Article 34). Define escalation procedures, communication templates, and documentation requirements.
- **inputs**: CNIL breach notification requirements, incident response procedures
- **outputs**: Breach notification procedure, templates, escalation path
- **dependencies**: [GDPR-011]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: legal
- **validation**: Procedure tested, 72-hour notification capability confirmed

#### Task: GDPR-013
- **title**: Conduct Third-Party data transfer assessment
- **description**: Assess all international data transfers (outside EU/EEA) per Chapter V GDPR. Determine transfer mechanisms: adequacy decision, SCCs, BCRs, or specific derogations. Document each transfer, its legal basis, and safeguards applied.
- **inputs**: List of third-party processors, data flow documentation
- **outputs**: Transfer impact assessment documents
- **dependencies**: [GDPR-002]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: legal
- **validation**: All transfers documented with appropriate safeguards

#### Task: GDPR-014
- **title**: Register with CNIL (if required)
- **description**: Determine CNIL registration requirements. While GDPR eliminated general registration requirements, certain processing may still require declaration. Assess if any specific obligations exist. Subscribe to CNIL newsletters and updates for compliance monitoring.
- **inputs**: Processing activities, CNIL guidelines
- **outputs**: CNIL assessment, registration if required, subscription confirmed
- **dependencies**: [GDPR-002]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: CNIL obligations clarified, registration completed if needed

#### Task: GDPR-015
- **title**: Train team on GDPR responsibilities
- **description**: Conduct GDPR training for all team members handling personal data. Cover: principles, rights, obligations, breach procedures, and consequences of non-compliance. Document training completion. Update training when regulations change.
- **inputs**: Training materials, GDPR documentation, team list
- **outputs**: Training completion records, updated materials
- **dependencies**: [GDPR-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: All team members trained, records maintained

#### Task: GDPR-016
- **title**: Implement pseudonymization techniques
- **description**: Where appropriate, implement pseudonymization (encrypting/separating identifying data from other data) to reduce risk and potentially exempt from certain GDPR obligations. Document pseudonymization techniques used.
- **inputs**: Data processing register, technical capabilities
- **outputs**: Pseudonymization implementation documentation
- **dependencies**: [GDPR-002, GDPR-011]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Pseudonymization implemented where applicable

#### Task: GDPR-017
- **title**: Document legitimate interest assessment
- **description**: For processing based on legitimate interest (Article 6(1)(f)), conduct and document three-part test: purpose test (legitimate interest identified), necessity test (processing necessary for that purpose), balancing test (interests overridden by individual rights). Document outcomes.
- **inputs**: Processing activities claiming legitimate interest
- **outputs**: Legitimate interest assessment documents
- **dependencies**: [GDPR-003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: All legitimate interest bases documented and justified

#### Task: GDPR-018
- **title**: Create processor agreements (Article 28 contracts)
- **description**: Draft template Data Processing Agreements for all processor relationships (cloud providers, email services, analytics tools, support software). Ensure all required clauses per Article 28 are included: processing scope, instructions, confidentiality, security, sub-processor controls, assistance with rights, deletion obligations.
- **inputs**: List of processors, Article 28 requirements
- **outputs**: Template DPA, signed agreements with all processors
- **dependencies**: [GDPR-002]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: legal
- **validation**: All processor agreements signed

#### Task: GDPR-019
- **title**: Implement automated decision-making disclosures
- **description**: If any automated processing produces legal/significant effects (e.g., automated subscription decisions), implement required disclosures under Article 22. Provide information to individuals, offer human intervention, and implement right to contest decisions.
- **inputs**: List of automated processing activities
- **outputs**: Article 22 compliance implementation
- **dependencies**: [GDPR-006]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Automated decision disclosures implemented

#### Task: GDPR-020
- **title**: Review and update GDPR documentation annually
- **description**: Establish annual review process for all GDPR documentation: data processing register, DPIA, security measures, consent records, procedures. Ensure documentation remains current with actual practices. Track changes and maintain version history.
- **inputs**: Existing GDPR documentation, review schedule
- **outputs**: Annual review procedure, updated documentation
- **dependencies**: [GDPR-002, GDPR-007, GDPR-011]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Annual review completed and documented

#### Task: GDPR-021
- **title**: Implement privacy by design principles
- **description**: Ensure privacy by design is embedded in product development: default privacy settings, data minimization in architecture, security by default, privacy testing in QA. Document how privacy principles are integrated into development lifecycle.
- **inputs**: Development processes, privacy requirements
- **outputs**: Privacy by design documentation, integration evidence
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Privacy by design review in development workflow

#### Task: GDPR-022
- **title**: Conduct privacy audits and testing
- **description**: Conduct regular privacy audits of data processing systems, test compliance with documented procedures, verify technical measures effectiveness. Include penetration testing, access control verification, data deletion testing.
- **inputs**: Audit schedule, testing procedures
- **outputs**: Audit reports, test results, remediation plans
- **dependencies**: [GDPR-011, GDPR-020]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Audit reports filed, issues remediated

---

### Category: Data Processing Agreement (DPA) Template

#### Task: DPA-001
- **title**: Draft master DPA template for B2B customers
- **description**: Create comprehensive Data Processing Agreement template compliant with Article 28 GDPR for use with business customers (artisans). Include processing scope, subject matter, duration, nature, purposes, data categories, data subject categories, obligations of controller and processor, security measures, sub-processor management, audit rights, breach notification, and cooperation obligations.
- **inputs**: GDPR Article 28 requirements, customer data types, processing purposes
- **outputs**: Master DPA template document
- **dependencies**: [GDPR-002, GDPR-018]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: legal
- **validation**: DPA template legally reviewed and approved

#### Task: DPA-002
- **title**: Define standard processing scenarios and instructions
- **description**: Document standard processing instructions customers are authorizing when they use the service. Cover: data hosting, backup, security scanning, support access (if any), analytics, and any other processing the SaaS performs on customer data.
- **inputs**: System architecture, processing activities
- **outputs**: Processing instructions document annex
- **dependencies**: [DPA-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Instructions documented and included in DPA

#### Task: DPA-003
- **title**: Define sub-processor list and approval process
- **description**: List all approved sub-processors (OVH, monitoring services, email providers, etc.) with their processing purposes and locations. Define process for notifying customers of new sub-processors and customer objection rights. Implement standard 15-day objection period.
- **inputs**: Current sub-processor list, approval workflow
- **outputs**: Sub-processor list, approval process documented
- **dependencies**: [DPA-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Sub-processor list accurate and complete

#### Task: DPA-004
- **title**: Implement DPA execution workflow
- **description**: Create workflow for executing DPAs with new customers: when to send, how to execute (digital signature), version control, storage, and retrieval. Integrate with subscription onboarding process. Define effective date and duration terms.
- **inputs**: Subscription workflow, signature solution
- **outputs**: DPA execution workflow documented
- **dependencies**: [DPA-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Workflow implemented and tested

#### Task: DPA-005
- **title**: Draft DPA annexes (technical and organizational measures)
- **description**: Create TOMs (Technical and Organizational Measures) annex detailing specific security measures implemented: encryption standards, access controls, backup procedures, incident response, staff training, etc. Make it detailed enough for customer audit but practical to maintain.
- **inputs**: Security measures documentation, GDPR-011
- **outputs**: TOMs annex document
- **dependencies**: [GDPR-011, DPA-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: TOMs annex reviewed and approved

#### Task: DPA-006
- **title**: Define audit rights and procedures
- **description**: Document customer audit rights per Article 28(3)(h): scope of audits, notice requirements, audit duration, cost allocation, use of third-party auditors, audit reports. Balance between customer rights and operational feasibility.
- **inputs**: Audit requirements, operational capabilities
- **outputs**: Audit rights clause, audit procedure document
- **dependencies**: [DPA-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Audit clause included in DPA

#### Task: DPA-007
- **title**: Define data return and deletion upon termination
- **description**: Specify what happens to customer data at contract end: data export formats (JSON, CSV), export timeline, deletion timeline (typically 30-60 days post-termination), confirmation of deletion, handling of data beyond retention period.
- **inputs**: Data export capabilities, termination procedures
- **outputs**: Data return/deletion clause, export procedure
- **dependencies**: [GDPR-009, DPA-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Deletion procedures tested and documented

#### Task: DPA-008
- **title**: Create DPA for subprocessors (Article 28(4))
- **description**: If Mini-CRM acts as subprocessor for any upstream controllers (unlikely but review), create appropriate Article 28(4) agreement. Ensure our obligations flow down correctly.
- **inputs**: Subprocessor role determination
- **outputs**: Subprocessor DPA template
- **dependencies**: [DPA-001]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Subprocessor DPA if needed, template available

#### Task: DPA-009
- **title**: Implement DPA version control and change management
- **description**: Establish version control for DPA template, track changes, notify customers of material changes with reasonable notice (30 days), maintain customer acknowledgment records for each version.
- **inputs**: Version control system, customer list
- **outputs**: Version control procedure, change notification template
- **dependencies**: [DPA-004]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Version control implemented

#### Task: DPA-010
- **title**: Review DPA with French consumer law attorney
- **description**: Have French attorney or legal expert review DPA template to ensure compliance with French law specifics beyond GDPR, including requirements from Loi Informatique et Libertés amendments and French court precedents.
- **inputs**: DPA draft, French legal requirements
- **outputs**: Attorney review comments, approved DPA
- **dependencies**: [DPA-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Legal review documented, DPA approved

---

### Category: Privacy Policy (RGPD-Compliant)

#### Task: PP-001
- **title**: Draft comprehensive Privacy Policy (Politique de Confidentialité)
- **description**: Create full Privacy Policy compliant with GDPR Articles 13-14 and French Loi Informatique et Libertés. Must cover: identity of controller and DPO, purposes and legal basis, data categories, recipients, transfers, retention, rights, complaints to CNIL, automated decisions, and specific disclosures required by French law.
- **inputs**: GDPR requirements, data processing register, French law specifics
- **outputs**: Complete Privacy Policy document
- **dependencies**: [GDPR-002, GDPR-003, GDPR-005]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: legal
- **validation**: Privacy Policy reviewed and approved

#### Task: PP-002
- **title**: Include CNIL-specific disclosures in Privacy Policy
- **description**: Add required disclosures per CNIL guidelines: right to withdraw consent, right to portability, right to erasure (with limitations for legal obligations), data breach notification procedures, and CNIL contact information for complaints.
- **inputs**: CNIL guidelines, Privacy Policy draft
- **outputs**: Updated Privacy Policy with CNIL-specific content
- **dependencies**: [PP-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: CNIL disclosures included

#### Task: PP-003
- **title**: Write cookie and tracking technology disclosure
- **description**: Detail all cookies and tracking technologies used: session cookies, analytics cookies, marketing pixels, third-party scripts. Specify purpose, duration, and whether optional or required. Include information about Do Not Track signals and browser settings.
- **inputs**: Cookie audit results, tracking technologies used
- **outputs**: Cookie disclosure section
- **dependencies**: [GDPR-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Cookie disclosure comprehensive and accurate

#### Task: PP-004
- **title**: Create data retention table
- **description**: Create clear table/grid showing retention periods for each data category: customer account data, invoices, support tickets, activity logs, backups. Reference legal basis for each retention period.
- **inputs**: Retention schedule from GDPR-009
- **outputs**: Retention table in Privacy Policy
- **dependencies**: [GDPR-009, PP-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Retention table clear and accurate

#### Task: PP-005
- **title**: Document international data transfers
- **description**: If any data transfers outside EU/EEA occur (OVH may have non-EU infrastructure), disclose: transfer mechanisms (SCCs, adequacy), country, safeguards, and risks. If no transfers, state clearly.
- **inputs**: Data flow documentation, sub-processor locations
- **outputs**: International transfer section in Privacy Policy
- **dependencies**: [GDPR-013]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Transfer disclosures verified accurate

#### Task: PP-006
- **title**: Create data subject rights section with exercise instructions
- **description**: Detail all data subject rights with practical instructions on how to exercise each: contact method, response timeline (30 days), authentication requirements, whether fees may apply, escalation path if no response.
- **inputs**: Rights procedures from GDPR-006
- **outputs**: Rights exercise section
- **dependencies**: [GDPR-006, PP-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Rights section practical and actionable

#### Task: PP-007
- **title**: Publish Privacy Policy on website
- **description**: Publish Privacy Policy on website in accessible location (footer link). Ensure French language version available. Implement versioning with effective date. Add link from signup/onboarding flow. Configure page as non-indexed for crawlers if draft.
- **inputs**: Privacy Policy final version, website structure
- **outputs**: Privacy Policy published, linked from key locations
- **dependencies**: [PP-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Privacy Policy live and accessible

#### Task: PP-008
- **title**: Create short privacy notice for signup flow
- **description**: Create condensed "just-in-time" privacy notice for display during account creation and data collection moments. Should link to full Privacy Policy. Must include: identity of controller, purposes, legal basis, and rights summary.
- **inputs**: Full Privacy Policy, signup flow
- **outputs**: Short privacy notice text
- **dependencies**: [PP-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Short notice implemented in signup flow

#### Task: PP-009
- **title**: Translate Privacy Policy to English if targeting international
- **description**: If marketing to non-French speaking customers or listing in international app stores, create English translation of Privacy Policy. Ensure translations are accurate and legally equivalent.
- **inputs**: French Privacy Policy, target markets
- **outputs**: English Privacy Policy version
- **dependencies**: [PP-001]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Translation reviewed by bilingual legal professional

#### Task: PP-010
- **title**: Review Privacy Policy annually
- **description**: Establish annual review schedule for Privacy Policy. Review after any material changes to data processing, new products, regulatory updates, or CNIL guidance. Track version history and customer notification procedures.
- **inputs**: Review schedule, previous version
- **outputs**: Annual review procedure, updated policy
- **dependencies**: [PP-001, GDPR-020]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Annual review completed and documented

#### Task: PP-011
- **title**: Create privacy policy for employees
- **description**: Draft separate privacy notice for employee data processing covering: HR data, payroll, monitoring, email usage, device policies. Comply with both GDPR and French labor law requirements (Code du Travail).
- **inputs**: Employee data processing activities, labor law requirements
- **outputs**: Employee Privacy Notice document
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Employee privacy notice reviewed and distributed

#### Task: PP-012
- **title**: Implement Privacy Policy change notification
- **description**: Create procedure for notifying customers of Privacy Policy changes: email notification, notice period (recommended 30 days), customer acknowledgment tracking, opt-out/consent for material changes if applicable.
- **inputs**: Version control system, customer communication channels
- **outputs**: Change notification procedure and templates
- **dependencies**: [PP-007, PP-010]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Notification procedure documented and tested

---

### Category: Terms of Service / CGV

#### Task: TOS-001
- **title**: Draft master Terms of Service (Conditions Générales de Vente - CGV)
- **description**: Create comprehensive CGV compliant with French consumer law (Code de la consommation) and e-commerce regulations (Loi pour la Confiance dans l'Économie Numérique - LCEN). Cover: scope, acceptance, products/services description, pricing, ordering, payment, delivery, warranties, liability, and dispute resolution.
- **inputs**: French consumer law requirements, product/service details
- **outputs**: CGV document
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: legal
- **validation**: CGV legally reviewed and approved

#### Task: TOS-002
- **title**: Define service description and specifications
- **description**: Clearly describe Mini-CRM service tiers (€29/49/79/month), features included in each tier, usage limits, storage quotas, user limits, support levels. Ensure descriptions are accurate and not misleading under French consumer law.
- **inputs**: Product tiers, feature matrix
- **outputs**: Service description section for CGV
- **dependencies**: [TOS-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: Service descriptions accurate and complete

#### Task: TOS-003
- **title**: Define pricing, billing, and payment terms
- **description**: Specify pricing (with and without TVA), billing frequency (monthly/annual), payment methods accepted, payment timing, currency (EUR), consequences of failed payments, price change notification and process, applicable discounts or promotions.
- **inputs**: Pricing tiers, payment provider capabilities
- **outputs**: Payment terms section for CGV
- **dependencies**: [TOS-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Payment terms clear and compliant

#### Task: TOS-004
- **title**: Create subscription terms and automatic renewal clause
- **description**: Define subscription model, initial term (monthly/annual), automatic renewal terms, renewal pricing, customer notification before renewal. Ensure compliance with French law on automatic renewals (Code de la consommation Article L221-28).
- **inputs**: Subscription model, renewal capabilities
- **outputs**: Subscription terms section
- **dependencies**: [TOS-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Renewal terms compliant with French law

#### Task: TOS-005
- **title**: Draft cancellation and termination clauses
- **description**: Define cancellation rights under French consumer law (droit de rétractation - 14 days for consumers, but note B2B may not apply), termination for cause, termination without cause (résiliation libre), notice periods, refund policies, data return/deletion upon termination.
- **inputs**: French consumer law, cancellation capabilities
- **outputs**: Cancellation and termination section
- **dependencies**: [TOS-001, DPA-007]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: legal
- **validation**: Cancellation terms legally compliant

#### Task: TOS-006
- **title**: Define liability limitations
- **description**: Draft liability clause with limitations permitted under French law: limitation of indirect damages, liability caps (e.g., 12 months fees paid), force majeure provisions, consequential damages exclusions. Ensure clauses are enforceable under French law.
- **inputs**: French liability law, insurance coverage
- **outputs**: Liability section for CGV
- **dependencies**: [TOS-001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: legal
- **validation**: Liability limitations reviewed by attorney

#### Task: TOS-007
- **title**: Create warranty provisions
- **description**: Define statutory warranties under French law (conformité, vices cachés per Code civil), any commercial warranties offered, warranty claim procedures, remedy options (repair, replacement, refund).
- **inputs**: French warranty law, product capabilities
- **outputs**: Warranty section
- **dependencies**: [TOS-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Warranty terms compliant

#### Task: TOS-008
- **title**: Add intellectual property ownership clauses
- **description**: Define IP ownership: who owns the software (company), who owns customer data (customer), license grant to customer, restrictions on use, reverse engineering prohibitions, trademark usage.
- **inputs**: IP ownership decisions, licensing model
- **outputs**: IP section for CGV
- **dependencies**: [TOS-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: IP clauses clear and enforceable

#### Task: TOS-009
- **title**: Define acceptable use and restrictions
- **description**: Specify acceptable use policy: prohibited activities (illegal use, spam, security violations), usage restrictions, account sharing limits, resource usage limits, consequences of violations (suspension, termination).
- **inputs**: Use cases to restrict, enforcement capabilities
- **outputs**: Acceptable use section
- **dependencies**: [TOS-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Acceptable use clear and enforceable

#### Task: TOS-010
- **title**: Add force majeure clause
- **description**: Create force majeure clause defining events beyond control (natural disasters, pandemics, regulatory changes, provider failures), suspension obligations during force majeure, and termination rights if force majeure exceeds specified duration.
- **inputs**: Standard force majeure events, French law requirements
- **outputs**: Force majeure clause
- **dependencies**: [TOS-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Force majeure clause standard and compliant

#### Task: TOS-011
- **title**: Define notice and communication provisions
- **description**: Specify how communications between parties will occur: email as primary method, notice periods, deemed receipt times, address updates, language (French primary, English optional).
- **inputs**: Communication channels, support system
- **outputs**: Communication provisions section
- **dependencies**: [TOS-001]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Communication provisions clear

#### Task: TOS-012
- **title**: Add assignment and transfer restrictions
- **description**: Define conditions under which contract can be assigned to another party, customer cannot assign without consent, company can assign with notice, procedures for assignment.
- **inputs**: Business requirements
- **outputs**: Assignment clause
- **dependencies**: [TOS-001]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Assignment clause documented

#### Task: TOS-013
- **title**: Create entire agreement and severability clause
- **description**: Draft standard entire agreement clause (整合), severability clause (if one provision is invalid, others remain), and hierarchy of documents (CGV prevail over conflicting terms).
- **inputs**: Standard contract clauses
- **outputs**: Entire agreement and severability clauses
- **dependencies**: [TOS-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Clauses included and standard

#### Task: TOS-014
- **title**: Define governing law and jurisdiction
- **description**: Specify governing law (French law), jurisdiction (French courts, with mandatory mediation attempt per Consumer Code), and any arbitration agreements if applicable.
- **inputs**: French jurisdiction requirements
- **outputs**: Jurisdiction clause
- **dependencies**: [TOS-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Jurisdiction clause legally valid

#### Task: TOS-015
- **title**: Publish CGV on website
- **description**: Publish CGV on website with clear accessibility (direct link in footer). Ensure French version authoritative. Add "last updated" date, version number. Link from order/checkout flow.
- **inputs**: Final CGV, website structure
- **outputs**: CGV published and linked
- **dependencies**: [TOS-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: CGV accessible and linked

#### Task: TOS-016
- **title**: Create Terms of Sale for digital products
- **description**: Create specific terms for digital content/services per EU Consumer Rights Directive and French Consumer Code: right of withdrawal exclusions for digital goods, digital content warranty, compatibility updates obligation.
- **inputs**: Digital product regulations
- **outputs**: Digital terms addendum
- **dependencies**: [TOS-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Digital terms compliant with EU directives

#### Task: TOS-017
- **title**: Create order/invoice specific terms
- **description**: Define terms governing specific orders: order confirmation process, order acceptance, order errors and corrections, special conditions, bespoke terms for large customers.
- **inputs**: Order workflow, common edge cases
- **outputs**: Order terms section
- **dependencies**: [TOS-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Order terms clear

#### Task: TOS-018
- **title**: Review CGV annually
- **description**: Establish annual review schedule for CGV, track regulatory changes, update terms as product evolves, maintain version history and customer notification procedures.
- **inputs**: Review schedule, previous CGV version
- **outputs**: Annual review procedure, updated CGV
- **dependencies**: [TOS-001, TOS-015]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Annual review completed

---

### Category: Cookie Consent (Axeptio or Cookiebot)

#### Task: COOK-001
- **title**: Conduct comprehensive cookie audit
- **description**: Audit all cookies and tracking technologies deployed: first-party (session, functional, analytics), third-party (Google Analytics, Facebook Pixel, support chat, marketing), and any future tracking planned. Document cookie purpose, duration, and data collected.
- **inputs**: Website code, browser testing, network analysis
- **outputs**: Complete cookie inventory
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Full cookie list documented

#### Task: COOK-002
- **title**: Select cookie consent management platform (CMP)
- **description**: Evaluate and select CMP: Axeptio (French company, RGPD-compliant, good EU coverage), Cookiebot (Usercentrics), OneTrust, or other. Compare features, pricing, CNIL compliance, language support, and integration requirements.
- **inputs**: CMP comparison criteria, budget
- **outputs**: CMP selection decision with rationale
- **dependencies**: [COOK-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: product
- **validation**: CMP selected and contracted

#### Task: COOK-003
- **title**: Configure CMP with cookie categories
- **description**: Set up CMP with categories: strictly necessary (no consent required), functional, analytics/performance, marketing, social media. Define which cookies go in each category. Configure consent granular defaults.
- **inputs**: Cookie inventory, CMP admin
- **outputs**: CMP configured with categories
- **dependencies**: [COOK-001, COOK-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: CMP configured and tested

#### Task: COOK-004
- **title**: Implement cookie banner with required disclosures
- **description**: Configure cookie consent banner per CNIL guidelines: clear information about purposes, no pre-checked boxes for non-essential cookies (unless strictly necessary), equal prominence for accept/reject buttons, easy access to preferences.
- **inputs**: CNIL cookie guidelines, CMP configuration
- **outputs**: Cookie banner implemented
- **dependencies**: [COOK-002, COOK-003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Banner compliant with CNIL guidelines

#### Task: COOK-005
- **title**: Implement granular consent mechanism
- **description**: Implement detailed consent interface allowing users to accept/reject each cookie category separately. Ensure users can change preferences later. Save consent records with timestamp and user preferences.
- **inputs**: CMP capabilities, consent recording requirements
- **outputs**: Granular consent UI implemented
- **dependencies**: [COOK-004]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Granular consent working correctly

#### Task: COOK-006
- **title**: Implement consent recording and storage
- **description**: Implement consent record system: store consent timestamp, cookie version, user preferences, method of consent, user ID or anonymous identifier. Ensure records are tamper-proof and retained for required period.
- **inputs**: Consent recording requirements, database design
- **outputs**: Consent storage system
- **dependencies**: [COOK-005]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Consent records stored and retrievable

#### Task: COOK-007
- **title**: Implement cookie blocking before consent
- **description**: Ensure all non-essential cookies are blocked until consent is obtained. Implement pre-consent cookie blocking at site/app level. Verify cookies are not set before consent interaction.
- **inputs**: Cookie implementation, blocking requirements
- **outputs**: Pre-consent blocking implemented
- **dependencies**: [COOK-005]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: No cookies set before consent

#### Task: COOK-008
- **title**: Implement consent refresh/resurface mechanism
- **description**: Configure mechanism to periodically remind users of their consent preferences (e.g., annually or when cookie policy changes). Allow users to easily modify previous consent choices.
- **inputs**: CMP configuration, consent duration
- **outputs**: Consent refresh mechanism
- **dependencies**: [COOK-005]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Consent refresh working

#### Task: COOK-009
- **title**: Add cookie preference center link
- **description**: Add easily accessible link to cookie preferences in website footer, often labeled "Manage cookies" or "Cookie Settings". Ensure consistent access across all pages.
- **inputs**: Website footer, CMP integration
- **outputs**: Cookie settings link in footer
- **dependencies**: [COOK-005]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Link visible and functional

#### Task: COOK-010
- **title**: Document cookie consent legal requirements for documentation
- **description**: Create documentation of cookie consent implementation for legal records: what cookies are used, their purposes, consent mechanism, retention of consent records. This documentation supports compliance demonstration.
- **inputs**: Cookie audit, implementation details
- **outputs**: Cookie consent documentation
- **dependencies**: [COOK-001, COOK-006]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Documentation complete and accurate

#### Task: COOK-011
- **title**: Test cookie consent implementation
- **description**: Test cookie consent flow: initial visit, accept all, reject all, granular preferences, preference changes, banner behavior, consent record storage. Verify no cookies fire before consent.
- **inputs**: Testing checklist, browser tools
- **outputs**: Test results
- **dependencies**: [COOK-007, COOK-008]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: All tests passed

#### Task: COOK-012
- **title**: Implement Google Analytics with consent
- **description**: Configure Google Analytics (or alternative analytics) to wait for consent before setting tracking cookies. Implement consent-mode or equivalent. Ensure analytics data collection only with proper consent.
- **inputs**: GA configuration, consent requirements
- **outputs**: GA consent-gated implementation
- **dependencies**: [COOK-007]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: GA only active with consent

#### Task: COOK-013
- **title**: Implement marketing pixels with consent
- **description**: Configure Facebook Pixel, LinkedIn Insight, or other marketing pixels to respect consent. Block pixels until user opts into marketing cookies. Document which pixels are used and their purposes.
- **inputs**: Marketing pixels, consent requirements
- **outputs**: Marketing pixel consent implementation
- **dependencies**: [COOK-007]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Marketing pixels consent-gated

#### Task: COOK-014
- **title**: Configure CMP for mobile apps if applicable
- **description**: If Mini-CRM has mobile apps, configure CMP for mobile: different UX patterns for apps, SDK consent flows, native app consent dialogs if needed.
- **inputs**: Mobile app platforms, CMP SDK
- **outputs**: Mobile consent implementation
- **dependencies**: [COOK-002]
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Mobile consent working

#### Task: COOK-015
- **title**: Review and update cookie list quarterly
- **description**: Establish quarterly review of cookie list: add new cookies from updates, remove deprecated cookies, update purposes and descriptions. Keep CMP configuration in sync.
- **inputs**: Cookie audit schedule
- **outputs**: Quarterly cookie review
- **dependencies**: [COOK-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Reviews completed on schedule

---

### Category: Invoice Legal Requirements (Factures - Mentions Obligatoires)

#### Task: INV-001
- **title**: Research French invoice legal requirements (mentions obligatoires)
- **description**: Research and document all required mentions for French invoices per French commercial law (Code de commerce) and tax law: company details, customer details, invoice number, date, product/service description, quantity, unit price, total HT, TVA rates and amounts, total TTC, payment terms, due date, late payment penalties.
- **inputs**: French invoice regulations
- **outputs**: Mentions obligatoires checklist
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Complete checklist of requirements

#### Task: INV-002
- **title**: Define invoice numbering scheme
- **description**: Establish sequential invoice numbering system compliant with French requirements: must be sequential, unique, no gaps (or documented reason for gaps), can include year prefix (e.g., 2026-001). Define format and process for voiding invoices.
- **inputs**: Accounting requirements, billing system capabilities
- **outputs**: Invoice numbering policy
- **dependencies**: [INV-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Numbering scheme documented

#### Task: INV-003
- **title**: Implement invoice template with all required mentions
- **description**: Create invoice template including all mandatory mentions: our company details (name, legal form, RCS/SIREN, registered office, TVA intra), customer details (name, address, for professionals: RCS/SIRET), invoice number, date, due date, line items, TVA breakdown by rate, totals HT/TVA/TTC, payment terms, IBAN for bank transfer, late payment terms.
- **inputs**: Mentions checklist, template design
- **outputs**: Compliant invoice template
- **dependencies**: [INV-001, INV-002]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Template reviewed for compliance

#### Task: INV-004
- **title**: Implement TVA calculation and reporting
- **description**: Implement TVA calculation: standard rate (20%), intermediate rate (10%) for certain services, reduced rate (5.5%) if applicable, exempt if micro-entreprise under franchise. Calculate TVA per line and total. Generate TVA declaration data.
- **inputs**: TVA rates, billing logic
- **outputs**: TVA calculation system
- **dependencies**: [COMP-004]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: TVA calculations correct

#### Task: INV-005
- **title**: Set up accounting software integration
- **description**: Set up accounting software (Pennylane, Indy, Sage, etc.) for French market. Configure for French chart of accounts (Plan Comptable Général), TVA reporting requirements, and invoice import/export.
- **inputs**: Accounting software selection
- **outputs**: Accounting integration functional
- **dependencies**: [INV-003, COMP-005]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Invoices flow to accounting software

#### Task: INV-006
- **title**: Implement automatic invoice generation
- **description**: Create automated invoice generation upon subscription creation, renewal, or manual trigger. Include sequential numbering, all required fields, PDF generation, email delivery.
- **inputs**: Billing system, invoice template
- **outputs**: Automated invoice generation
- **dependencies**: [INV-003, INV-004]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: Auto-generated invoices correct

#### Task: INV-007
- **title**: Define credit note procedures
- **description**: Create credit note (avoir) procedure for refunds, corrections. Include: credit note numbering linked to original invoice, reason codes, TVA reversal, customer notification.
- **inputs**: Refund scenarios, invoice system
- **outputs**: Credit note procedure
- **dependencies**: [INV-003]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Credit notes work correctly

#### Task: INV-008
- **title**: Implement electronic invoice format (Chorus Pro if required)
- **description**: If serving public sector or large B2G customers, may need to support Chorus Pro (French e-invoicing platform). Determine applicability and implement EDIFACT or XML format if required. For B2B private sector, optional but recommended to offer.
- **inputs**: Customer types, Chorus Pro requirements
- **outputs**: Chorus Pro integration if required
- **dependencies**: [INV-003]
- **priority**: low
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: E-invoicing compliant if applicable

#### Task: INV-009
- **title**: Define invoice retention policy
- **description**: Per French tax law, invoices must be retained for 10 years (digital retention permitted). Establish document retention policy, backup procedures, and format requirements (must be readable throughout retention period).
- **inputs**: French tax law retention requirements
- **outputs**: Retention policy and procedures
- **dependencies**: [INV-003]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Retention policy documented

#### Task: INV-010
- **title**: Set up separate business account for invoicing
- **description**: Ensure payments for invoices go to dedicated business account (required for SAS). Set up payment matching, reconciliation procedures between bank and invoicing system.
- **inputs**: Business bank account, invoicing system
- **outputs**: Payment reconciliation working
- **dependencies**: [COMP-005, INV-003]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Payments matched to invoices

#### Task: INV-011
- **title**: Create proforma invoice template
- **description**: Create proforma invoice template for quotes and advance billing: includes same information as final invoice but clearly marked as "PROFORMA" and not accounting record. Use for deposits or quotes requiring advance payment.
- **inputs**: Invoice template, quote workflow
- **outputs**: Proforma invoice template
- **dependencies**: [INV-003]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Proforma template ready

#### Task: INV-012
- **title**: Test invoice generation and delivery
- **description**: Test complete invoice flow: generation, PDF rendering, email delivery, payment processing, reconciliation. Verify all mentions appear correctly, TVA calculations are accurate, invoice numbers are sequential.
- **inputs**: Testing scenarios
- **outputs**: Test results
- **dependencies**: [INV-006]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: All invoice tests passed

---

### Category: E-commerce Compliance (French Consumer Law)

#### Task: ECOM-001
- **title**: Review French e-commerce regulations (LCEN)
- **description**: Research and document requirements from Loi pour la Confiance dans l'Économie Numérique (LCEN): information requirements for online services, identity disclosure, hosting obligations,spam compliance, cooling-off period for online purchases.
- **inputs**: LCEN requirements
- **outputs**: LCEN compliance checklist
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Requirements documented

#### Task: ECOM-002
- **title**: Publish required legal notices on website
- **description**: Publish all required legal notices per LCEN: company name, legal form, registered office address, RCS/SIREN number, TVA intra if applicable, contact email, director name (optional but recommended), hosting provider identity.
- **inputs**: Company registration details, LCEN requirements
- **outputs**: Legal notice page published
- **dependencies**: [COMP-003]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Legal notices visible on website

#### Task: ECOM-003
- **title**: Implement right of withdrawal (droit de rétractation)
- **description**: Implement 14-day cooling-off period for consumers (B2C). Create withdrawal form template, define return/refund process, exceptions for digital goods (once delivered with consent). Note B2B may be excluded.
- **inputs**: Consumer law requirements, product type
- **outputs**: Withdrawal process and form
- **dependencies**: [TOS-005]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Withdrawal process functional

#### Task: ECOM-004
- **title**: Create accessible pricing display
- **description**: Ensure prices are clearly displayed: HT and TTC (TVA included), all fees, currency (EUR). No hidden fees at checkout. Display shipping costs before payment. Per consumer law, total price must be visible.
- **inputs**: Pricing display requirements
- **outputs**: Compliant pricing display
- **dependencies**: [TOS-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Pricing displays compliant

#### Task: ECOM-005
- **title**: Implement secure payment processing
- **description**: Ensure PCI DSS compliance for payment processing: use Stripe, PayPal, or other PCI-compliant processor. Do not store card details. Display secure payment indicators. Implement 3D Secure if required.
- **inputs**: Payment provider selection, PCI requirements
- **outputs**: Secure payment implementation
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: PCI compliance verified

#### Task: ECOM-006
- **title**: Create consumer-friendly complaint handling
- **description**: Create complaint procedure for consumers: contact channels, response timeline, escalation process, records of complaints. Required for certain regulations and dispute resolution.
- **inputs**: Consumer protection requirements
- **outputs**: Complaint handling procedure
- **dependencies**: [ECOM-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Procedure documented

#### Task: ECOM-007
- **title**: Implement age verification if required
- **description**: If any products have age restrictions or if needed for compliance, implement age verification at signup. French law may require age verification for certain digital services.
- **inputs**: Age restriction requirements
- **outputs**: Age verification mechanism
- **dependencies**: []
- **priority**: low
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Age verification if needed

#### Task: ECOM-008
- **title**: Review pricing for unfair commercial practices
- **description**: Ensure pricing practices don't constitute unfair commercial practices under French consumer law: no fake discounts, clear reference prices, no misleading "free" offers. Review promotional pricing display.
- **inputs**: French unfair practice regulations
- **outputs**: Pricing review report
- **dependencies**: [ECOM-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Pricing practices reviewed

#### Task: ECOM-009
- **title**: Create distance selling contract requirements
- **description**: Document requirements for contracts concluded at distance (online): information requirements, confirmation copy within 24h, accessibility of contract terms, electronic signature if applicable.
- **inputs**: Distance selling regulations
- **outputs**: Distance contract requirements
- **dependencies**: [ECOM-001, TOS-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Requirements documented

#### Task: ECOM-010
- **title**: Implement product/service availability information
- **description**: Display real-time or accurate availability of subscriptions. Define stock/status indicators. If a tier becomes unavailable, notification process. Avoid "bait advertising" violations.
- **inputs**: Product availability rules
- **outputs**: Availability display implementation
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Availability accurate

---

### Category: Subscription Terms & Cancellation (Résiliation Libre)

#### Task: SUB-001
- **title**: Define subscription tiers and pricing
- **description**: Define three subscription tiers: Starter €29/mo, Pro €49/mo, Business €79/mo. Document features per tier, user limits, storage limits, support levels. Ensure compliance with French pricing regulations.
- **inputs**: Pricing strategy, feature matrix
- **outputs**: Subscription tier documentation
- **dependencies**: [TOS-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Tiers documented and approved

#### Task: SUB-002
- **title**: Implement monthly and annual billing cycles
- **description**: Implement subscription billing: monthly (calendar month) and annual (365 days) billing cycles. Define pro-rata calculations for mid-cycle changes, upgrades, downgrades. Set up billing date tracking.
- **inputs**: Billing cycle requirements
- **outputs**: Billing cycle implementation
- **dependencies**: [SUB-001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: Billing cycles working correctly

#### Task: SUB-003
- **title**: Implement subscription upgrade/downgrade
- **description**: Create upgrade and downgrade flows: immediate effect vs end-of-cycle, proration calculations, invoice generation for upgrades, credits for downgrades. Define what happens to features/data when downgrading.
- **inputs**: Tier change requirements
- **outputs**: Upgrade/downgrade functionality
- **dependencies**: [SUB-002]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: devops
- **validation**: Tier changes work correctly

#### Task: SUB-004
- **title**: Implement résiliation libre (unsubscribe anytime)
- **description**: Implement cancellation with notice period (typically end of current billing period, no cancellation fees for monthly). Per French law, consumer must be able to cancel subscription without penalty. Set up cancellation flow in account settings.
- **inputs**: Cancellation requirements, French consumer law
- **outputs**: Cancellation flow implemented
- **dependencies**: [TOS-005]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Cancellation functional and compliant

#### Task: SUB-005
- **title**: Create cancellation confirmation and communication
- **description**: Send immediate confirmation upon cancellation request, explain what happens to account at end of billing period, confirm data retention policy post-cancellation, provide reactivation option.
- **inputs**: Cancellation workflow
- **outputs**: Confirmation email templates
- **dependencies**: [SUB-004]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Confirmations sent correctly

#### Task: SUB-006
- **title**: Implement account access post-cancellation
- **description**: Define what happens during cancellation notice period: full access continues until end of billing period, then read-only mode or suspension. Document grace period if any.
- **inputs**: Cancellation policy
- **outputs**: Post-cancellation access rules
- **dependencies**: [SUB-004]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: devops
- **validation**: Post-cancellation behavior defined

#### Task: SUB-007
- **title**: Implement automatic renewal notices
- **description**: Send renewal reminder before automatic renewal: 7 days and 1 day before renewal date. Include clear information about renewal date, amount, and easy cancellation link
, ability to cancel with one click, no questions asked
- **inputs**: Current subscription status, customer contact information
- **outputs**: Renewal notice sent, cancellation handled
- **dependencies**: [SUB-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: backend
- **validation**: Notice sent at correct intervals, cancellation works

---

### Category: Data Portability (GDPR Article 20)

#### Task: DP-001
- **title**: Define data export formats
- **description**: Define supported data export formats (JSON, CSV, vCard). Ensure all structured data is exportable: contacts, jobs, invoices, client data. Exclude files (photos, documents) from standard export — offer separate download.
- **inputs**: Database schema, data models
- **outputs**: Export format specifications
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Exported data re-importable into competitor product

#### Task: DP-002
- **title**: Build data export feature (customer self-serve)
- **description**: Customer-initiated data export from settings panel. Export triggers async job, sends download link to email (expires in 24h). Include all data: contacts, jobs, invoices, pipeline stages.
- **inputs**: DP-001 format specs, settings UI design
- **outputs**: Export feature in settings
- **dependencies**: [DP-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Full data export completes, file is valid and complete

#### Task: DP-003
- **title**: Implement data portability in DPA
- **description**: Include data portability clause in DPA — customers have right to receive their data in structured, machine-readable format at any time during contract and for 30 days after termination.
- **inputs**: DP-002, legal templates
- **outputs**: DPA clause for data portability
- **dependencies**: [DP-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: DPA reviewed by lawyer, clause legally valid

---

### Category: Right to Erasure (GDPR Article 17)

#### Task: RE-001
- **title**: Define data retention schedule
- **description**: Define retention periods for each data category: contacts (duration of contract + 30 days), jobs (duration + 1 year), invoices (10 years per French law), logs (90 days), analytics data (anonymized after 13 months).
- **inputs**: French legal requirements, GDPR Article 17
- **outputs**: Data retention schedule document
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Retention schedule reviewed by legal counsel

#### Task: RE-002
- **title**: Build account deletion feature (customer self-serve)
- **description**: Customer-initiated account deletion from settings. Triggers: anonymization of personal data, deletion of non-legal data, scheduled permanent deletion after 30-day retention. Sends confirmation email.
- **inputs**: RE-001 retention schedule, settings UI
- **outputs**: Deletion feature in settings
- **dependencies**: [RE-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: backend
- **validation**: Deletion removes all personal data, invoices retained per legal requirement

#### Task: RE-003
- **title**: Handle erasure requests from non-customers
- **description**: Process Article 17 requests from individuals whose data was submitted by a customer (e.g., a client's contact info in the CRM). Procedure: verify identity, notify customer, assess legitimate interest vs. erasure right.
- **inputs**: RE-001, customer data
- **outputs**: Erasure request procedure document
- **dependencies**: [RE-001]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Procedure documented and staff trained

---

### Category: Security Breach Response

#### Task: SBR-001
- **title**: Define security breach severity levels
- **description**: Define breach classification: Critical (full database compromise), High (unauthorized access to subset), Medium (single account compromised), Low (attempted breach detected and blocked). Define response SLAs for each: Critical = 4h, High = 24h, Medium = 72h, Low = 7 days.
- **inputs**: GDPR Article 33, CNIL guidelines
- **outputs**: Breach classification and response SLA document
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Classification approved by legal counsel

#### Task: SBR-002
- **title**: Build breach detection system
- **description**: Automated detection of: multiple failed login attempts (>10 in 5 min), unusual database query patterns, data export anomalies (>1GB export), unauthorized API access. Trigger alert to on-call team.
- **inputs**: SBR-001 severity levels
- **outputs**: Breach detection alerting system
- **dependencies**: [SBR-001]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: backend
- **validation**: Detection tested with simulated breach scenarios

#### Task: SBR-003
- **title**: Create breach notification template (CNIL)
- **description**: Pre-drafted notification template for CNIL (within 72h of breach discovery). Include: nature of breach, categories/approximate number of data subjects, likely consequences, measures taken. Keep template ready — do not draft during crisis.
- **inputs**: GDPR Article 33, CNIL form
- **outputs**: Breach notification template
- **dependencies**: []
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Template reviewed by legal counsel

#### Task: SBR-004
- **title**: Create breach notification template (data subjects)
- **description**: Pre-drafted notification for affected customers: plain language explanation of breach, what data was exposed, what they should do (change passwords, monitor accounts), how to contact support, compensation if applicable.
- **inputs**: SBR-001, SBR-003
- **outputs**: Customer breach notification template
- **dependencies**: [SBR-003]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Template in French, reviewed by legal counsel

---

### Category: Penetration Testing

#### Task: PT-001
- **title**: Commission external penetration test (pre-launch)
- **description**: Hire certified penetration testing firm (e.g., SEC Consult, Orange Cyberdefense France) to test: authentication system, API endpoints, database access, OVH VPS configuration. Obtain written report with findings.
- **inputs**: Application architecture documentation
- **outputs**: Penetration test report
- **dependencies**: [BACK-001, BACK-006]
- **priority**: high
- **estimated_complexity**: high
- **agent_type**: security
- **validation**: All critical/high findings remediated before launch

#### Task: PT-002
- **title**: Set up vulnerability disclosure policy
- **description**: Publish vulnerability disclosure page (security.txt or dedicated page). Define: what to report, how to report, expected response timeline (72h initial response), bug bounty program consideration.
- **inputs**: PT-001 findings
- **outputs**: Vulnerability disclosure page
- **dependencies**: [PT-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: devops
- **validation**: Disclosure page live, accessible at /security

#### Task: PT-003
- **title**: Schedule annual penetration test
- **description**: Contract with penetration testing firm for annual retest. Add to calendar with 30-day lead time for scheduling. Include: full application test, OVH VPS configuration review, API security test.
- **inputs**: PT-001 report
- **outputs**: Annual pen test contract
- **dependencies**: [PT-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: security
- **validation**: Next pen test scheduled within 12 months of previous

---

### Category: Cyber Insurance

#### Task: CI-001
- **title**: Research cyber insurance requirements for French SMBs
- **description**: Research cyber insurance policies available in France for small tech companies (e.g., AXA Cyber, Société Générale Cyber, Allianz Cyber). Understand: coverage limits, exclusions, prerequisites (pen test, security measures), premium range for €29-79/month SaaS product.
- **inputs**: Market research
- **outputs**: Cyber insurance comparison document
- **dependencies**: []
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: At least 3 policies compared

#### Task: CI-002
- **title**: Evaluate RC Pro (Professional Liability) coverage
- **description**: French RC Pro (Responsabilité Civile Professionnelle) insurance for tech consultants — evaluate whether standard RC Pro covers: data breach costs, legal defense, customer compensation. Determine if specific cyber policy is needed or if RC Pro is sufficient at launch scale.
- **inputs**: CI-001 research
- **outputs**: RC Pro evaluation report
- **dependencies**: [CI-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Decision documented: buy cyber policy or rely on RC Pro

#### Task: CI-003
- **title**: Purchase cyber insurance policy
- **description**: Once policy selected, purchase and implement required security controls (from insurer's prerequisites). Store policy document in company records, share with legal counsel.
- **inputs**: CI-002 decision, CI-001 options
- **outputs**: Cyber insurance policy active
- **dependencies**: [CI-002]
- **priority**: medium
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Policy document received, coverage confirmed

---

### Category: Third-Party Processors

#### Task: TPP-001
- **title**: Create sub-processor register
- **description**: Maintain sub-processor register as required by GDPR Article 28. Include: processor name, purpose, data categories, location, legal basis, security measures. Review annually or when adding new processor.
- **inputs**: All third-party services used
- **outputs**: Sub-processor register document
- **dependencies**: [BACK-001, DEVOPS-001]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Register accurate and complete

#### Task: TPP-002
- **title**: Draft DPA template for sub-processors
- **description**: Standard DPA template for all sub-processors: defines data processing scope, security requirements, audit rights, breach notification obligations, subcontracting restrictions. Use CNIL standard clauses as baseline.
- **inputs**: GDPR Article 28, CNIL DPA template
- **outputs**: DPA template for sub-processors
- **dependencies**: [TPP-001]
- **priority**: high
- **estimated_complexity**: medium
- **agent_type**: legal
- **validation**: Template reviewed by legal counsel

#### Task: TPP-003
- **title**: Review OVH Data Processing Addendum
- **description**: OVH provides DPA for customers using their VPS services. Review OVH's DPA — ensure it covers: data processing scope, security measures, sub-processor restrictions, breach notification, data location (OVH France/Strasbourg). Confirm OVH is DPA-compatible.
- **inputs**: OVH contracts, TPP-002 template
- **outputs**: OVH DPA review document
- **dependencies**: [TPP-002]
- **priority**: high
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: OVH DPA signed and on file

---

### Category: Dispute Resolution

#### Task: DR-001
- **title**: Define jurisdiction and governing law
- **description**: Specify in ToS: jurisdiction = France, governing law = French law, competent court = Tribunal de Commerce de Caen (local relevance for Louis's team). Include SME-friendly dispute resolution clause.
- **inputs**: French procedural law
- **outputs**: Jurisdiction clause for ToS
- **dependencies**: [TOS-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Clause reviewed by legal counsel

#### Task: DR-002
- **title**: Implement mandatory mediation clause
- **description**: Per French consumer law (Code de la consommation), include mandatory mediation for consumer disputes: Médiation de la Consommation (mediator: CM2C or similar). Link to mediation platform in ToS and in confirmation emails.
- **inputs**: DR-001, French consumer code
- **outputs**: Mediation clause and mediator contact in ToS
- **dependencies**: [DR-001, TOS-001]
- **priority**: medium
- **estimated_complexity**: low
- **agent_type**: legal
- **validation**: Mediation clause live and functional

#### Task: DR-003
- **title**: Set up customer complaint procedure
- **description**: Document customer complaint procedure: how to submit complaint (email, form), response timeline (48h acknowledgment, 10 days resolution), escalation path (escalate to mediation if unresolved). Publish in FAQ/help center.
- **inputs**: DR-002
- **outputs**: Complaint procedure document
- **dependencies**: [DR-002]
- **priority**: low
- **estimated_complexity**: low
- **agent_type**: product
- **validation**: Procedure accessible to customers

---

## Orchestrator TODO (Legal & Compliance)

### Phase 1 — Must Complete Before Launch
- [ ] CF-002: Register company (SAS or micro-entreprise)
- [ ] GDPR-003: Register with CNIL (or confirm exemption)
- [ ] PP-001, PP-002, PP-003, PP-004, PP-005, PP-006, PP-007, PP-008: Privacy Policy complete and published
- [ ] TOS-001, TOS-002, TOS-003, TOS-004, TOS-005: Terms of Service complete
- [ ] CGV-001: CGV complete and published
- [ ] COOK-001, COOK-002: Cookie consent implemented
- [ ] INV-001, INV-002, INV-003, INV-004, INV-005: Invoice compliance implemented
- [ ] SUB-001, SUB-002, SUB-003, SUB-004, SUB-005, SUB-006, SUB-007: Subscription terms implemented
- [ ] DP-001, DP-002: Data export implemented
- [ ] RE-001, RE-002: Account deletion implemented
- [ ] SBR-001, SBR-002, SBR-003, SBR-004: Breach response system in place
- [ ] PT-001: Penetration test completed
- [ ] TPP-003: OVH DPA signed

### Phase 2 — Complete Within 6 Months
- [ ] CF-003: Professional liability insurance (RC Pro)
- [ ] CI-001, CI-002, CI-003: Cyber insurance purchased
- [ ] PT-002: Vulnerability disclosure policy published
- [ ] PT-003: Annual pen test scheduled
- [ ] DR-001, DR-002, DR-003: Dispute resolution in place

---

*Legal & Compliance Roadmap — Mini-CRM for French Artisans*
*Last updated: 2026-03-30*
