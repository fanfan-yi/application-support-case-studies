# Case Study 04 — Oracle EBS Procurement Rollout

## Overview

This case study describes my role in the rollout of Oracle E-Business Suite (EBS) Procurement for a new overseas manufacturing entity.

I owned the Oracle EBS Procurement workstream, covering environment and master-data configuration, Forms and Reports localisation, ERP-side workflow integration, testing support, cutover, go-live, and ongoing production support.

The broader ERP program also included infrastructure, network, hardware, and upstream ERP activities managed by other teams. My ownership was specifically focused on Oracle EBS Procurement and the ERP-side integration required by the procurement approval process.

---

## Business Context

A new manufacturing entity required its own Oracle EBS Procurement environment and procurement approval capability.

The rollout involved several challenges:

- Procurement configuration had to be established for the new operating environment.
- Existing Oracle Forms required localisation for the new users.
- Some Oracle Reports required substantial redesign because the existing layouts did not meet local business requirements.
- The existing approval integration was primarily designed around a single-organisation model and required changes to support a Multi-Org environment.
- A large amount of purchasing-category and expense-account configuration had to be completed within the rollout schedule.

The Procurement workstream also depended on upstream ERP and infrastructure readiness before some configuration and testing activities could proceed.

---

## My Ownership

I owned the Oracle EBS Procurement workstream across the implementation and post-go-live lifecycle.

My responsibilities included:

- Oracle EBS Procurement environment configuration
- Procurement master-data setup
- Oracle Forms localisation and modification
- Oracle Reports development and modification
- Developer testing
- User Acceptance Testing (UAT) support
- Procurement cutover and opening-data support
- ERP-side integration changes for the approval workflow
- Go-live support
- Production incident investigation and troubleshooting
- Continuous post-go-live enhancements

The approval application framework itself was converted to support Multi-Org by an external consultant. My responsibility was the Oracle ERP-side integration data layer required to provide organisation-aware data to the approval system.

Infrastructure, network, server, and hardware implementation were handled by other project teams.

---

## Key Actions

### 1. Procurement Environment and Master Data

I prepared and configured the Oracle EBS Procurement environment based on the organisation's implementation procedures.

Configuration and master-data activities included areas such as:

- purchasing suppliers and supplier sites
- supplier types
- requisitioners and approval supervisors
- buyers and buyer supervisors
- ship-to locations
- purchasing categories
- procurement-related account configuration

I also worked with procurement stakeholders to confirm reporting requirements and required changes to existing business processes.

---

### 2. Oracle Forms and Reports

The new environment did not have a complete set of Forms and Reports that could simply be reused without modification.

I worked on:

- localisation of Oracle Forms for the new environment
- modification and redevelopment of Oracle Reports
- developer testing before user testing
- UAT support
- iterative revisions based on user feedback

Some reports required multiple rounds of revision as business requirements became more detailed during testing.

The reporting scope was intentionally delivered in two phases because of the compressed ERP go-live schedule:

**Phase 1 — Pre-Go-Live**

- 7 priority Reports completed before production go-live
- focused on the reports required for initial operations

**Phase 2 — Post-Go-Live**

- 14 additional Reports completed after go-live
- no formal deadline was assigned to this phase
- the planned 21-report scope was completed by 24 June 2025

In total, the rollout included:

- **21 Oracle Reports**
- **7 Oracle Forms**

Enhancements and requirement changes continued after the planned conversion scope was completed.

---

### 3. Multi-Org Approval Integration

The existing approval integration had largely been designed for a single-organisation environment.

To support the new Multi-Org structure, I analysed Oracle EBS data relationships and identified how Operating Unit and Organisation identifiers could be derived and supplied correctly to the approval system.

I restructured the ERP-side integration data layer, including:

- **5 new database Views**
- **10 modified existing Views**
- **5 new custom Tables**

This allowed the ERP integration layer to distinguish organisational data correctly when supporting the Multi-Org approval process.

The approval-system framework changes were handled separately by an external consultant.

---

### 4. Configuration Automation

The rollout required **148 purchasing categories**.

Where possible, I used the existing Oracle standard data-loading approach for repetitive setup.

However, the web-based expense-account-rule configuration could not use the same standard loading mechanism.

Each purchasing category required configuration across seven accounting segments:

```text
148 purchasing categories
× 7 accounting segments
= 1,036 segment-level setup operations
```

To reduce repetitive manual data entry, I developed an Excel-driven browser automation workflow using:
- Python
- Selenium WebDriver
- pandas
- openpyxl
- PyAutoGUI
- pyperclip
The automation read configuration data from Excel and performed repeated Oracle EBS web-interface entry steps.
Because browser-based ERP automation can be affected by page loading and system response times, I executed and verified the configuration in smaller batches rather than treating the process as a single unattended run.
Manual configuration was estimated at approximately two minutes per purchasing category, representing roughly five hours of equivalent manual setup work.
Automation execution time was not formally measured, so no percentage time-saving claim is made.
The technical automation implementation is maintained separately in my Python automation portfolio to keep this case study focused on ERP implementation and Application Support responsibilities.

5. Cutover and Go-Live Support
I supported procurement cutover by preparing and validating opening transaction categories such as:
- requisitioned but not yet ordered
- ordered but not yet delivered
- received but not yet inspected or accepted
- inspected or accepted but not yet invoiced
The Procurement environment went live on 1 May 2025.
I supported the transition from implementation into production and continued handling procurement and approval-related issues after go-live.
Production Support
Post-go-live support included troubleshooting issues across:
- user responsibilities and access
- requisition and purchasing forms
- RFQ processing
- supplier-related reporting
- purchasing configuration
- blanket purchase agreements
- receiving processes
- custom and standard receiving functions
- approval routing and supervisor master data
- Oracle Reports
- user-requested enhancements
My support approach typically involved:
1. confirming the business impact and affected transaction
2. identifying whether the issue originated from configuration, master data, application logic, workflow, or user process
3. tracing the relevant Oracle EBS data and process flow
4. implementing or coordinating the appropriate correction
5. asking users to retest where applicable
6. documenting or explaining the correct operational process when the issue was process-related
This work continued after the initial implementation and remains part of ongoing production support.
## Project Scale

| Area | Scale |
| --- | ---: |
| Oracle Reports | 21 |
| Oracle Forms | 7 |
| ERP integration Views | 15 |
| New custom Tables | 5 |
| Purchasing categories | 148 |
| Expense-account segment setup operations | 1,036 |
| Production go-live | 1 May 2025 |
| Planned report conversion scope completed | 24 June 2025 |


The Procurement system supports purchasing operations for the new manufacturing entity, while purchase requisitions are used across the wider plant rather than only by the Procurement team.
Technology
- Oracle E-Business Suite R12.2
- Oracle Procurement / Purchasing
- Oracle Forms
- Oracle Reports
- PL/SQL
- Oracle Database
- Oracle EBS Multi-Org
- Agentflow BPM integration
- Python
- Selenium WebDriver
- pandas
- openpyxl
- PyAutoGUI
- Excel-based configuration input
Result
The Oracle EBS Procurement environment successfully entered production on 1 May 2025.
The rollout established the Procurement environment, required master data, Forms and Reports, and ERP-side approval integration needed to support the new manufacturing entity.
The reporting scope was deliberately phased around the go-live schedule, with seven priority reports available before go-live and the remaining planned reports completed afterwards.
Following go-live, I continued to own Procurement and approval-related application support, including incident investigation, configuration issues, report changes, process troubleshooting, and new user requirements.
Skills Demonstrated
- Oracle EBS Procurement implementation
- ERP Application Support
- Production support
- Requirements analysis
- Root cause analysis
- Oracle EBS Multi-Org
- PL/SQL and Oracle data analysis
- System integration
- Forms and Reports support
- UAT support
- ERP cutover and go-live support
- Process troubleshooting
- Python automation
- Stakeholder communication
Confidentiality
This case study is based on professional ERP implementation experience.
Company names, internal URLs, credentials, system identifiers, production data, and confidential implementation details have been removed or generalised.
