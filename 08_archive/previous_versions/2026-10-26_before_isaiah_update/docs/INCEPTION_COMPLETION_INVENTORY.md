# OpenCHS–Primero CPIMS+ Integration
## Inception Completion Inventory

**Project:** Lesotho Child Helpline 116 / OpenCHS integration with Primero CPIMS+  
**Document status:** Working inventory for inception close-out  
**Version:** 0.1  
**Date:** 13 October 2026  
**Source baseline:** Session 1 and Session 2 minutes, current D1 inception report, Workstream 1 template pack and capture workbook

> Status meanings: **Resolved** means no inception decision or approval is still outstanding for that item; it does not mean the feature is implemented or production-ready. **Pending** means a concrete decision, owner, evidence, access item, or approval is still required. **Deferred** means it is intentionally outside the accelerated MVP unless a contract or governance decision brings it back into scope.

## 1. Close-out summary

The inception is not yet ready for final approval. The business direction is substantially captured, but the following remain critical completion dependencies:

- confirmation of escalation and approval rules for exceptions to the agreed manual referral trigger;
- CPIMS+ service/referral targets, acceptance/rejection and Ministry-side distribution;
- minimum identifying information and anonymous-report handling;
- ABR ownership, validation and missing-ID rules;
- API contract, field mapping and Primero sandbox access;
- intermediate status and follow-up update behaviour;
- named owners, UAT sign-off authority and security/data-sharing approval.

### Status snapshot

| Status | Items | Meaning for follow-up |
|---|---:|---|
| Resolved | 5 | No inception decision remains; implementation evidence may still be needed later |
| Pending | 53 | Must have an owner, next action and closure evidence before inception approval |
| Deferred | 11 | Excluded from the accelerated MVP and controlled through change management |

The snapshot is based on the inventory below and should be refreshed whenever an item changes status.

## 3. Pending follow-up queue

Use this queue during follow-up meetings. Update the linked template first, then copy the decision/evidence back into this inventory and the D1 report.

| Priority | Item ID | Owner | Next action | Template to complete |
|---|---|---|---|---|
| Critical | API-006 / API-007 | Hopolang / UNICEF / Primero | Complete the sandbox readiness checklist and provide the access package | [05 API / Environment Matrix](<../Inception Meeting /temeplate forms/05_api_environment_matrix.docx>), [06 API Contract Capture](<../Inception Meeting /temeplate forms/06_api_contract_capture.docx>), [13 Sandbox Risk Record](<../Inception Meeting /temeplate forms/13_workstream_1_risk_record_primero_sandbox.docx>) |
| Critical | WF-003 | Child Helpline / MGYSD | Approve escalation and approval rules for exceptions to the manual agent trigger | [02 Referral Lifecycle Capture](<../Inception Meeting /temeplate forms/02_referral_lifecycle_capture.docx>), [09 Decision Register](<../Inception Meeting /temeplate forms/09_decision_register.docx>) |
| Critical | RT-001 / RT-002 / RT-003 | Primero / MGYSD | Confirm service targets, accept/reject flow and Ministry-side distribution | [02 Referral Lifecycle Capture](<../Inception Meeting /temeplate forms/02_referral_lifecycle_capture.docx>), [04 Field-Mapping Worksheet](<../Inception Meeting /temeplate forms/04_field_mapping_worksheet.docx>) |
| Critical | DATA-001 / DATA-003 / DATA-004 | MGYSD / Home Affairs | Confirm ABR authority, format, validation and later-update process | [03 ABR ID Requirements](<../Inception Meeting /temeplate forms/03_abr_id_requirements.docx>) |
| Critical | DATA-005 / DATA-007 / DATA-009 | Project / Primero / MGYSD | Complete field mapping, protection-concern mapping and perpetrator-data rules | [04 Field-Mapping Worksheet](<../Inception Meeting /temeplate forms/04_field_mapping_worksheet.docx>) |
| Critical | WF-009 / UAT-006 / DATA-011 | MGYSD / Primero / security | Approve minimum identification, anonymous-report handling and free-text rules | [04 Field-Mapping Worksheet](<../Inception Meeting /temeplate forms/04_field_mapping_worksheet.docx>), [08 UAT and Acceptance Matrix](<../Inception Meeting /temeplate forms/08_uat_acceptance_matrix.docx>) |
| High | RT-005 / RT-006 / RT-007 | OpenCHS / Primero / MGYSD | Define acknowledgement, status, follow-up update and acceptance evidence | [02 Referral Lifecycle Capture](<../Inception Meeting /temeplate forms/02_referral_lifecycle_capture.docx>), [06 API Contract Capture](<../Inception Meeting /temeplate forms/06_api_contract_capture.docx>) |
| High | GOV-001 / GOV-002 / GOV-003 | Project governance | Name decision owners, focal points, UNICEF representation and sign-off path | [01 Stakeholder / Responsibility Matrix](<../Inception Meeting /temeplate forms/01_stakeholder_responsibility_matrix.docx>) |
| High | API-001 / API-002 / API-003 / API-004 | Primero / OpenCHS technical teams | Obtain and approve API, JWT, endpoint, error and rate-limit contract | [06 API Contract Capture](<../Inception Meeting /temeplate forms/06_api_contract_capture.docx>) |
| High | OPS-001 / OPS-002 / OPS-003 | OpenCHS / Primero technical teams | Approve queue, retry, idempotency and uncertain-timeout recovery | [07 Reliability, Logging and Support Controls](<../Inception Meeting /temeplate forms/07_reliability_logging_support_controls.docx>) |
| High | OPS-004 / OPS-005 / OPS-006 / OPS-007 | Security / project / support owners | Finalize audit, redaction, support, incident and outage controls | [07 Reliability, Logging and Support Controls](<../Inception Meeting /temeplate forms/07_reliability_logging_support_controls.docx>) |
| High | UAT-001 / UAT-002 / UAT-003 / UAT-007 | Ministry / project governance | Name testers and signatories, approve safe data and defect/go-live rules | [08 UAT and Acceptance Matrix](<../Inception Meeting /temeplate forms/08_uat_acceptance_matrix.docx>) |
| High | GOV-006 / GOV-007 | Project steering authority / project manager | Approve baseline and reconcile decision, action, risk and issue registers | [09 Decision Register](<../Inception Meeting /temeplate forms/09_decision_register.docx>), [10 Action Register](<../Inception Meeting /temeplate forms/10_action_register.docx>), [11 Open Issues Register](<../Inception Meeting /temeplate forms/11_open_issues_register.docx>) |
| Before UAT | UAT-005 / UAT-008 / UAT-009 | Primero / Ministry / project | Test accept/reject, complete training and approve handover/go-live evidence | [08 UAT and Acceptance Matrix](<../Inception Meeting /temeplate forms/08_uat_acceptance_matrix.docx>), [12 Inception Close-out Checklist](<../Inception Meeting /temeplate forms/12_inception_closeout_checklist.docx>) |

## 2. Relevant templates and evidence

Use these editable templates and source records when closing each inventory item:

| Workstream | Relevant template / evidence |
|---|---|
| Governance, roles and ownership | [01 Stakeholder / Responsibility Matrix](<../Inception Meeting /temeplate forms/01_stakeholder_responsibility_matrix.docx>) |
| Referral lifecycle and SOP | [02 Referral Lifecycle Capture](<../Inception Meeting /temeplate forms/02_referral_lifecycle_capture.docx>) |
| ABR ID | [03 ABR ID Requirements](<../Inception Meeting /temeplate forms/03_abr_id_requirements.docx>) |
| Data mapping and privacy | [04 Field-Mapping Worksheet](<../Inception Meeting /temeplate forms/04_field_mapping_worksheet.docx>) |
| Environments and access | [05 API / Environment Matrix](<../Inception Meeting /temeplate forms/05_api_environment_matrix.docx>) |
| API and authentication contract | [06 API Contract Capture](<../Inception Meeting /temeplate forms/06_api_contract_capture.docx>) |
| Reliability, audit and support | [07 Reliability, Logging and Support Controls](<../Inception Meeting /temeplate forms/07_reliability_logging_support_controls.docx>) |
| UAT and acceptance | [08 UAT and Acceptance Matrix](<../Inception Meeting /temeplate forms/08_uat_acceptance_matrix.docx>) |
| Decisions | [09 Decision Register](<../Inception Meeting /temeplate forms/09_decision_register.docx>) |
| Actions | [10 Action Register](<../Inception Meeting /temeplate forms/10_action_register.docx>) |
| Open issues | [11 Open Issues Register](<../Inception Meeting /temeplate forms/11_open_issues_register.docx>) |
| Inception close-out | [12 Inception Close-out Checklist](<../Inception Meeting /temeplate forms/12_inception_closeout_checklist.docx>) |
| Primero sandbox risk | [13 Workstream 1 Risk Record — Primero Sandbox Access](<../Inception Meeting /temeplate forms/13_workstream_1_risk_record_primero_sandbox.docx>) |
| Sponsor escalation | [14 Potential Sponsor Escalation Email — Primero Sandbox Risk](<../Inception Meeting /temeplate forms/14_potential_sponsor_escalation_email_primero_sandbox.docx>) |
| Consolidated capture | [Workstream 1 Inception Capture Workbook](<../Inception Meeting /temeplate forms/Workstream_1_Inception_Capture_Workbook.xlsx>) |
| Minutes | [Session 1 minutes](<../Inception Meeting /Minutes/OpenCHS & Primero CPIMS+ Integration — Session 1 - Copy.pdf>) and [Session 2 minutes](<../Inception Meeting /Minutes/OpenCHS & Primero CPIMS+ Integration — Session 2.pdf>) |
| Baseline report | [D1 Inception Report](DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO.md) |

## 4. Inventory by workstream

### A. Governance, scope and ownership

| ID | Requirement to complete inception | Status | Evidence / current position | Closure action or evidence required | Owner |
|---|---|---|---|---|---|
| GOV-001 | Confirm project stakeholders and decision authority | Pending | Participants are recorded; business, technical, security and final sign-off authority are not fully named | Complete responsibility matrix and obtain confirmation | Project governance |
| GOV-002 | Confirm Child Helpline focal point(s) for build feedback and testing | Pending | Hopolang is recorded as responsible for naming the focal point(s); Mary Damposi is a possible contact | Name reachable focal point(s), including shift coverage if required | Hopolang / Child Helpline management |
| GOV-003 | Confirm UNICEF Country Office participation or approval route | Pending | UNICEF Country Office was absent; Session 2 says representation may be available later | Confirm participation, delegate, approval authority and escalation route | UNICEF / project governance |
| GOV-004 | Confirm receiving system, version and deployment | Pending | Primero/CPIMS+ is the receiving system; exact version/deployment remains unconfirmed | Record official environment and version with Primero technical owner | Primero technical team |
| GOV-005 | Confirm direct OpenCHS-to-CPIMS+ scope boundary | Resolved | Minutes and templates record direct integration; X-Road/Home Affairs is separate | Retain written scope boundary and governance evidence | Project governance |
| GOV-006 | Confirm contract-aligned delivery baseline and any accelerated technical package | Pending | Contract planning baseline runs 1 July 2026–28 February 2027 with milestone targets in August, October, November and February; earlier materials record a 14-week technical plan | Approve the contract milestone dates, acceptance gates, owners, and any dependency-driven rebaseline | Project steering authority |
| GOV-007 | Maintain decision, action, risk and open-issues registers | Pending | Registers exist in the template pack; owners and due dates are incomplete | Confirm one owner and date for every open item | Project manager |

### B. Business workflow and referral lifecycle

| ID | Requirement to complete inception | Status | Evidence / current position | Closure action or evidence required | Owner |
|---|---|---|---|---|---|
| WF-001 | Approve end-to-end referral lifecycle | Pending | Initiate, validate, transmit, acknowledge, accept/reject, assign, update and close were discussed | Convert the agreed lifecycle into the approved SOP and acceptance model | MGYSD / Child Helpline |
| WF-002 | Confirm referral trigger | Resolved | The handling agent manually triggers the referral; once sent to CPIMS+, case management starts immediately | Record the agreed trigger and immediate CPIMS+ case-management start in the approved workflow/SOP | Child Helpline / MGYSD |
| WF-003 | Confirm supervisor approval or escalation rules | Pending | Agent is not currently restricted to supervisors, but escalation may be used | Define scenarios requiring supervisor review or approval | Child Helpline operations |
| WF-004 | Define minimum-information emergency referral | Pending | Emergency referral without every detail is agreed in principle | Approve minimum dataset, missing-field handling and follow-up task | MGYSD / Child Helpline |
| WF-005 | Define incomplete or partial referral handling | Pending | Partial referrals and later information are supported in principle | Specify required status, missing-field record, owner and completion rule | Project team / MGYSD |
| WF-006 | Define correction, cancellation and re-referral rules | Pending | Questions remain open in the D1 report | Approve who may correct, cancel or re-refer and how history is preserved | MGYSD / technical teams |
| WF-007 | Confirm urgent parallel phone path | Resolved | Direct police/first-responder calls continue alongside system referrals | Document procedure, evidence and reconciliation with system referral | Child Helpline / Ministry |
| WF-008 | Confirm case-plan boundary | Pending | Session 2 working direction is that each system maintains its own case plan | Record exclusion from shared payload and confirm no MVP synchronisation | OpenCHS / Primero teams |
| WF-009 | Confirm handling of anonymous reports | Pending | Session 2 identified that CPIMS+ may require identifying information; exception rules are unresolved | Define minimum identification, refusal/exception path and safe user message | Primero / MGYSD / Child Helpline |

### C. Routing, acceptance and status feedback

| ID | Requirement to complete inception | Status | Evidence / current position | Closure action or evidence required | Owner |
|---|---|---|---|---|---|
| RT-001 | Confirm CPIMS+ service/referral target vocabulary | Pending | Session 2 demonstrated service-type referrals such as CPMS+/Child Protection Service | Obtain approved service list and mapping to OpenCHS values | Primero technical team |
| RT-002 | Confirm whether OpenCHS can select a district or individual | Pending | Session 2 revised the earlier direct-routing assumption; Ministry-side distribution is the working model | Confirm API and UI capability; do not assume caseworker selection | Primero technical team |
| RT-003 | Define Ministry supervisor/manager acceptance and distribution | Pending | Receiving party may accept/reject; supervisors/managers may assign internally | Document acceptance, rejection, allocation and reassignment rules | MGYSD / CPIMS+ stakeholders |
| RT-004 | Define routing for non-Ministry stakeholders | Pending | Police, courts and other stakeholders may be reached through CPIMS+ accounts; configuration is not confirmed | Confirm accounts, service targets and actual availability | MGYSD / Primero team |
| RT-005 | Define technical acknowledgement versus business acceptance | Pending | API acknowledgement and CPIMS+ accept/reject are distinct | Define states, evidence and operator visibility | OpenCHS / Primero teams |
| RT-006 | Define intermediate status vocabulary | Pending | Child Helpline identified a gap between referred/accepted and closed | Approve a small status set, update owner, privacy rules and display | Child Helpline / MGYSD / Primero |
| RT-007 | Define one-way follow-up update mechanism | Pending | OpenCHS follow-up updates are agreed in principle; exact endpoint/event and payload are open | Confirm update endpoint, supported events and status linkage | OpenCHS / Primero technical teams |
| RT-008 | Decide CPIMS+ to OpenCHS status write-back | Deferred | Desirable but not committed for this phase | Record as deferred unless governance explicitly adds it | Project steering authority |

### D. ABR ID and data requirements

| ID | Requirement to complete inception | Status | Evidence / current position | Closure action or evidence required | Owner |
|---|---|---|---|---|---|
| DATA-001 | Confirm ABR definition and issuing authority | Pending | Birth registration number is the working meaning; authority remains open | Confirm official definition, issuing authority and source system | MGYSD / Home Affairs / relevant authority |
| DATA-002 | Confirm ABR optional/non-blocking rule | Pending | Session 1/2 direction is that referral may proceed with ABR blank | Record the formal Ministry rule and test evidence | MGYSD / Child Helpline |
| DATA-003 | Confirm ABR format, uniqueness and validation | Pending | Format, length, uniqueness, check digit and validation mechanism are open | Provide valid/invalid examples and approved validation rule | Relevant authority / technical team |
| DATA-004 | Define later-available ABR update process | Pending | Later update is required in principle | Define correction/update event, permissions and audit history | MGYSD / OpenCHS / Primero |
| DATA-005 | Approve child identity and contact mapping | Pending | Candidate fields identified; requiredness and target schema pending | Complete signed field-mapping worksheet | Project and Primero teams |
| DATA-006 | Approve nationality, age, sex and location mappings | Pending | Candidate fields and code mappings require CPIMS+ vocabulary | Confirm target fields, codes and partial-date/age rules | Project and Primero teams |
| DATA-007 | Approve protection-concern/category mapping | Pending | Session 2 says CPIMS+ uses multi-select protection concerns; standardized list pending | Obtain approved protection-concern list and mapping layer | Primero / MGYSD |
| DATA-008 | Approve reporter contact sharing | Pending | Reporter contact is needed for follow-up in principle; privacy and target field remain open | Confirm fields, legal basis and minimisation rule | MGYSD / security / technical teams |
| DATA-009 | Approve perpetrator information handling | Pending | Important/priority information is supported in principle; exact fields and unknown handling remain open | Define fields, requiredness, safeguarding, access and logging controls | MGYSD / technical teams |
| DATA-010 | Decide attachment and recording scope | Deferred | Attachments, recordings and large media are deferred unless contractually required | Keep outside MVP and record change-control path | Project steering authority |
| DATA-011 | Approve narrative and free-text sharing rules | Pending | Narrative is a candidate field; raw transcript and sensitive free text require review | Define permitted content, redaction and target field | Security / MGYSD / technical teams |

### E. API, environment and access

| ID | Requirement to complete inception | Status | Evidence / current position | Closure action or evidence required | Owner |
|---|---|---|---|---|---|
| API-001 | Receive formal Primero API specification | Pending | Endpoint, request/response schemas and errors are not supplied | Obtain versioned specification and sample payloads | Primero technical team |
| API-002 | Confirm authentication contract | Pending | JWT is the documented requirement; issuer, claims, lifetime and refresh are open | Confirm token endpoint, claims, expiry, secrets and rotation | Primero / OpenCHS technical teams |
| API-003 | Confirm referral and follow-up endpoints | Pending | Candidate `/api/v2/tokens` and `/api/v2/cases` references are discovery-only | Validate paths, methods, create/update semantics and version | Primero technical team |
| API-004 | Confirm API errors, rate limits and timeout behaviour | Pending | Not supplied in Session 1/2 | Obtain error catalogue, limits, retry guidance and maintenance windows | Primero technical team |
| API-005 | Confirm OpenCHS test/UAT environment | Pending | Test/UAT environment is being stood up with helpline application and API Gateway | Provide access, roles and connectivity evidence | OpenCHS technical team |
| API-006 | Complete Primero sandbox readiness checklist | Pending | Sandbox is a critical-path dependency; expected in about one week remains unconfirmed | Confirm checklist completion, blockers, owners and committed access date | Hopolang / UNICEF / Primero |
| API-007 | Confirm sandbox access package | Pending | URL, credentials/JWT setup, scopes, API docs, sample payloads, TLS and allow-listing are incomplete | Provide complete package through a secure channel | UNICEF / Primero technical team |
| API-008 | Confirm production environment and secret management | Pending | Production is not confirmed ready | Define endpoint, credentials, certificates, storage, rotation and rollback | Infrastructure / Primero / OpenCHS |
| API-009 | Confirm X-Road/Home Affairs boundary | Resolved | It is recorded as a separate CPIMS+ workstream, not direct OpenCHS integration | Retain written governance boundary; do not build against it in MVP | Project governance |

### F. Reliability, security and operations

| ID | Requirement to complete inception | Status | Evidence / current position | Closure action or evidence required | Owner |
|---|---|---|---|---|---|
| OPS-001 | Confirm durable queue and offline behaviour | Pending | Required by scope; implementation and retention are unverified | Approve queue states, retention, recovery and operator visibility | OpenCHS technical team |
| OPS-002 | Approve retry and escalation policy | Pending | Retry intervals and error classes remain proposed | Define retryable errors, attempts, backoff, dead-letter and escalation | Technical / support owners |
| OPS-003 | Approve idempotency and duplicate reconciliation | Pending | Required; key and CPIMS+ lookup/reconciliation are open | Agree authoritative key and uncertain-timeout procedure | OpenCHS / Primero teams |
| OPS-004 | Define audit evidence | Pending | Minimum direction is case/reference ID, timestamp, transaction/result and API response | Approve final fields, retention, redaction and access | Security / technical teams |
| OPS-005 | Define sensitive-data masking and log access | Pending | Required controls are identified; exact policy is open | Approve fields to redact, role access and retention | Security / data protection owner |
| OPS-006 | Define monitoring and support ownership | Pending | Queue and referral failure escalation is not assigned | Name first-line, technical and receiving-system support owners | Project / Ministry / technical teams |
| OPS-007 | Confirm incident, breach and outage procedure | Pending | Escalation path is required but not approved | Document contacts, severity, response and reporting rules | Security / programme owner |

### G. UAT, acceptance, training and handover

| ID | Requirement to complete inception | Status | Evidence / current position | Closure action or evidence required | Owner |
|---|---|---|---|---|---|
| UAT-001 | Confirm Ministry-led UAT participants | Pending | Session 2 identifies Ministry users, Child Helpline, technical teams and district supervisors | Name individuals, roles and test accounts | Ministry / project team |
| UAT-002 | Confirm UAT sign-off authority | Pending | Sign-off authority is not named | Nominate business and technical signatories | Project governance |
| UAT-003 | Approve safe test data and environment | Pending | Safe representative test data and stable UAT environment are not confirmed | Approve data set, access and reset procedure | UAT lead / security |
| UAT-004 | Approve UAT scenarios | Resolved | Core scenarios are recorded, including manual trigger, ABR present/missing, emergency, routing, updates, rejection and audit | Convert to numbered test cases with expected evidence | UAT lead |
| UAT-005 | Test CPIMS+ service acceptance/rejection | Pending | Session 2 clarified this gate; test contract is not available | Add acceptance/rejection and reason evidence to UAT | Primero / Ministry / Child Helpline |
| UAT-006 | Test anonymous/insufficient-identification handling | Pending | Minimum identification and exceptions remain unresolved | Resolve business rule before UAT sign-off | MGYSD / Primero |
| UAT-007 | Define defect severity and conditional go-live rules | Pending | Acceptance criteria exist but severity/workaround policy is open | Approve critical/high defect and waiver rules | Project steering authority |
| UAT-008 | Complete operator and support training | Pending | Training is required; materials and attendance are not evidenced | Prepare guides, train users and retain attendance/evidence | Project / operations |
| UAT-009 | Complete handover and go-live decision | Pending | Support, rollback, monitoring and sign-off are open | Approve readiness pack and record go/no-go decision | Project steering authority |

### H. Explicitly deferred from the accelerated MVP

| ID | Deferred item | Status | Boundary |
|---|---|---|---|
| DEF-001 | CPIMS+ to OpenCHS status write-back or full bidirectional synchronisation | Deferred | Revisit only through approved scope change |
| DEF-002 | Attachments, call recordings and large media transfer | Deferred | No transfer unless contractually required and privacy-approved |
| DEF-003 | OpenCHS case-plan synchronisation | Deferred | Each system maintains its own case plan |
| DEF-004 | Advanced Primero lookup administration | Deferred | Use approved lookup values; administration is out of MVP |
| DEF-005 | Generic integration marketplace/administration framework | Deferred | Implement only the configured provider capabilities required for MVP |
| DEF-006 | Major OpenCHS workflow redesign | Deferred | Preserve existing workflow unless an approved requirement requires change |
| DEF-007 | Non-essential reporting and analytics | Deferred | Retain only operational/audit evidence required for acceptance |
| DEF-008 | Automated production deployment pipeline | Deferred | Handle through the approved deployment process later |
| DEF-009 | Direct X-Road/Home Affairs integration from OpenCHS | Deferred | Separate CPIMS+/X-Road workstream and governance decision |

## 5. Inception completion gates

The inception package should not be marked complete until these gates are evidenced:

1. Named owners and decision authorities are confirmed.
2. The manual agent referral trigger and immediate start of CPIMS+ case management are recorded; escalation and approval rules for exceptions are approved.
3. Emergency minimum dataset, anonymous-report and missing-ABR rules are approved.
4. CPIMS+ service/referral targets, acceptance/rejection and Ministry-side distribution are approved.
5. Field mapping and data-minimisation rules are approved.
6. API contract, JWT contract and sandbox access package are received and recorded.
7. Queue, retry, idempotency, audit, security and support controls have owners and acceptance evidence.
8. UAT participants, test data, scenarios and sign-off authority are confirmed.
9. Deferred scope is recorded and change-controlled.
10. The D1 report, decision register, action register, risk register and close-out checklist agree with one another.

## 6. Immediate actions before close-out

| Priority | Action | Required evidence |
|---|---|---|
| Critical | Obtain the Primero sandbox readiness/access package and confirm the date | Checklist, URL, secure credentials/JWT setup, API docs, sample payloads and connectivity evidence |
| Critical | Confirm escalation and approval rules for exceptions to the agreed manual agent referral trigger | Approved workflow/SOP and named authority |
| Critical | Confirm CPIMS+ service targets and Ministry distribution | Routing matrix and Primero technical confirmation |
| Critical | Confirm minimum identification and anonymous-report handling | Approved business rule and user/error handling |
| High | Complete ABR rules and field mapping | Signed ABR worksheet and field-mapping worksheet |
| High | Define status, follow-up update and acceptance/rejection contract | State model, endpoint/payload or operational procedure |
| High | Name UAT sign-off and support owners | Responsibility matrix and approval record |
| High | Reconcile all registers and close-out checklist | Matching IDs, owners, dates and evidence references |

## 7. Approval record

| Role | Name | Decision | Date |
|---|---|---|---|
| Business owner |  |  |  |
| UNICEF programme/governance owner |  |  |  |
| OpenCHS technical lead |  |  |  |
| Primero technical lead |  |  |  |
| Data protection/security owner |  |  |  |
| UAT sign-off authority |  |  |  |
| Project manager |  |  |  |
