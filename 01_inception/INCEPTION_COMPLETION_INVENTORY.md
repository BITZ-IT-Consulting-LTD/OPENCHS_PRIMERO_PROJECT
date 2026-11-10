# OpenCHS–Primero CPIMS+ Integration
## Inception Completion Inventory

**Project:** Lesotho Child Helpline 116 / OpenCHS integration with Primero CPIMS+  
**Document status:** Working inventory for inception close-out  
**Version:** 0.3  
**Date:** 26 October 2026  
**Source baseline:** Session 3 minutes of 26 October 2026, D1 v0.5, retained Sessions 1–2 evidence and Isaiah’s response.

> Status meanings: **Resolved** means the narrowly stated inception decision is recorded; it does not mean the feature is implemented or production-ready. **Pending** means a concrete decision, owner, evidence, access item, or approval is still required. **Deferred** means it is intentionally outside the current baseline unless a contract or governance decision brings it back into scope.

## 1. Close-out summary

Session 3 provides the business baseline for the initial draft due 28 October 2026 close of business. Formal D1 approval remains pending. Two-way integration, optional ABR, anonymous reporters, narrative required at referral, case-plan exclusion, the API specification and Ministry-led UAT roles are now recorded as agreed. Configured mappings, authentication, access, privacy and recovery detail remain open.

This inventory includes later implementation, UAT and handover items as well as inception requirements. Its counts are not an inception completion percentage; test execution and training are not required merely to circulate the draft. Outstanding design dependencies must be closed or explicitly accepted with owner and milestone before formal D1 approval.

| Status | Items | Follow-up meaning |
|---|---:|---|
| Resolved | 19 | Narrow inception decision recorded; implementation may remain |
| Pending | 44 | Evidence, design, access, approval or later delivery work remains |
| Deferred | 8 | Outside the current agreed implementation baseline |

### Workstream 1 priority follow-up

| Action | Owner | Due and closure evidence |
|---|---|---|
| A-013 national pathways | Rantsala | 26 Oct; received document |
| A-014 SOPs | Hopolang | 27 Oct due; September 2019 SOP now filed; Ministry applicability confirmation and BITZ mapping review pending |
| A-015 sandbox checklist | Rantsala / Isaiah | 26 Oct; completed checklist and remaining blockers |
| A-016 environment access | Isaiah | 28 Oct; secure access package and environment suitability |
| A-017 privacy materials | Lekhanya, UNICEF; confirm identity | 26 Oct; received policy/legal documents; discussion names Daniel |
| A-018 service list | Isaiah | 28 Oct; approved CPIMS+ vocabulary |
| A-020 Berea use cases | Melusi | 27 Oct; workshop requirements for dependency assessment |
| A-021 outage handling | Nelson / Peter / Isaiah | 28 Oct or during testing; agreed requirement or explicit testing dependency |
| A-022 privacy research | Nelson | 28 Oct; documented assessment for responsible-owner review |
| A-024 helpline leave cover | Hopolang | 27 Oct; named reachable representative |
| A-025 draft report | Nelson | 28 Oct close of business; v0.5 prepared, circulation evidence pending |

Dates above are recorded assignments, not evidence of completion. A-002 permanent focal-person appointment and A-007 remaining ABR verification work carry forward without restated dates. A-019 concerns the next X-Road coordination session; A-023 authentication/test execution follows access under A-016. These dependencies remain in the full tracker.

Use the [Session 3 action tracker](../03_meetings/session_3/SESSION_3_ACTION_TRACKER_2026-10-26.xlsx) and [current report](DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO_V1.0.md) for current decisions. Earlier capture forms require reconciliation to Session 3 before reuse; they do not override its agreed two-way scope, attachments or anonymity rules.

## 2. Relevant templates and evidence

Use these editable templates and source records when closing each inventory item:

| Workstream | Relevant template / evidence |
|---|---|
| Governance, roles and ownership | [01 Stakeholder / Responsibility Matrix](../04_templates/01_stakeholder_responsibility_matrix.docx) |
| Referral lifecycle and SOP | [02 Referral Lifecycle Capture](../04_templates/02_referral_lifecycle_capture.docx) |
| ABR ID | [03 ABR ID Requirements](../04_templates/03_abr_id_requirements.docx) |
| Data mapping and privacy | [04 Field-Mapping Worksheet](../04_templates/04_field_mapping_worksheet.docx) |
| Environments and access | [05 API / Environment Matrix](../04_templates/05_api_environment_matrix.docx) |
| API and authentication contract | [06 API Contract Capture](../04_templates/06_api_contract_capture.docx) |
| Reliability, audit and support | [07 Reliability, Logging and Support Controls](../04_templates/07_reliability_logging_support_controls.docx) |
| UAT and acceptance | [08 UAT and Acceptance Matrix](../04_templates/08_uat_acceptance_matrix.docx) |
| Decisions | [09 Decision Register](../04_templates/09_decision_register.docx) |
| Actions | [10 Action Register](../04_templates/10_action_register.docx) |
| Open issues | [11 Open Issues Register](../04_templates/11_open_issues_register.docx) |
| Inception close-out | [12 Inception Close-out Checklist](../04_templates/12_inception_closeout_checklist.docx) |
| Primero sandbox risk | [13 Workstream 1 Risk Record — Primero Sandbox Access](../04_templates/13_workstream_1_risk_record_primero_sandbox.docx) |
| Sponsor escalation | [14 Potential Sponsor Escalation Email — Primero Sandbox Risk](../04_templates/14_potential_sponsor_escalation_email_primero_sandbox.docx) |
| Consolidated capture | [Workstream 1 Inception Capture Workbook](../04_templates/Workstream_1_Inception_Capture_Workbook.xlsx) |
| Latest minutes | [Session 3 minutes](<../03_meetings/session_3/OpenCHS & Primero CPIMS+ Integration — Session 3 Minutes.pdf>) |
| Earlier minutes | [Session 1 minutes](../03_meetings/session_1/SESSION_1_MINUTES.pdf) and [Session 2 minutes](../03_meetings/session_2/SESSION_2_MINUTES.pdf) |
| Baseline report | [D1 Inception Report](DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO_V1.0.md) |

## 3. Inventory by workstream

### A. Governance, scope and ownership

| ID | Requirement to complete inception | Status | Evidence / current position | Closure action or evidence required | Owner |
|---|---|---|---|---|---|
| GOV-001 | Confirm project stakeholders and decision authority | Pending | Isaiah confirmed as Primero technical contact; business, security, technical approval and final sign-off authority remain incomplete | Complete responsibility matrix and confirm approval roles | Project governance |
| GOV-002 | Confirm permanent helpline focal person and leave cover | Pending | A-002 carries forward; Session 3 A-024 assigns temporary cover to Hopolang | Name leave cover by 27 Oct; confirm permanent focal person and contact | Hopolang / Child Helpline management |
| GOV-003 | Confirm UNICEF approval route | Pending | Rantsala and Ramoletane Lekhanya are recorded in the attendance export; the minutes’ Daniel reference needs reconciliation; formal approval authority remains unnamed | Confirm delegate, signatory and escalation route | UNICEF / project governance |
| GOV-004 | Confirm receiving system, version and deployment | Pending | Upstream API v2 documented; exact Lesotho release/deployment unconfirmed | Record agreed release/configuration and actual base URLs with Isaiah | Isaiah / Primero |
| GOV-005 | Confirm direct OpenCHS-to-CPIMS+ scope boundary | Resolved | Minutes and templates record direct integration; X-Road/Home Affairs is separate | Retain written scope boundary and governance evidence | Project governance |
| GOV-006 | Confirm contract-aligned delivery baseline and any accelerated technical package | Pending | Contract planning baseline runs 1 July 2026–28 February 2027 with milestone targets in August, October, November and February; earlier materials record a 14-week technical plan | Approve the contract milestone dates, acceptance gates, owners, and any dependency-driven rebaseline | Project steering authority |
| GOV-007 | Maintain aligned decisions and actions | Pending | Session 3 A-013–A-025 provide owners and milestone dates; current action tracker available | Record receipts and completed actions; assign dates to remaining design decisions | Project manager |
| GOV-008 | Identify Primero technical contact | Resolved | Isaiah Amutavi Osotsi identifies himself as the development/testing technical contact | Retain the email evidence; approval authority remains a separate Pending item | Isaiah / Primero |

### B. Business workflow and referral lifecycle

| ID | Requirement to complete inception | Status | Evidence / current position | Closure action or evidence required | Owner |
|---|---|---|---|---|---|
| WF-001 | Confirm business referral lifecycle | Resolved | Session 3 section 3 and D-006 accept the process as presented | Retain decision; confirm current applicability of the received September 2019 SOP under A-014 and resolve detailed exceptions separately | MGYSD / Child Helpline |
| WF-002 | Confirm referral trigger | Resolved | Session 3 D-006: manual action by handling agent | Preserve manual trigger; system receipt does not establish human acceptance | Child Helpline / MGYSD |
| WF-003 | Confirm supervisor approval or escalation rules | Pending | Agent is not currently restricted to supervisors, but escalation may be used | Define scenarios requiring supervisor review or approval | Child Helpline operations |
| WF-004 | Define minimum-information emergency referral | Pending | Emergency referral without every detail is agreed in principle | Approve minimum dataset, missing-field handling and follow-up task | MGYSD / Child Helpline |
| WF-005 | Define incomplete or partial referral handling | Pending | Partial referrals and later information are supported in principle | Specify required status, missing-field record, owner and completion rule | Project team / MGYSD |
| WF-006 | Define correction, cancellation and re-referral rules | Pending | Questions remain open in the D1 report | Approve who may correct, cancel or re-refer and how history is preserved | MGYSD / technical teams |
| WF-007 | Confirm urgent parallel phone path | Resolved | Direct police/first-responder calls continue alongside system referrals | Document procedure, evidence and reconciliation with system referral | Child Helpline / Ministry |
| WF-008 | Confirm case-plan boundary | Resolved | Session 3 D-012 excludes helpline case plan from transfer | Exclude it in mapping and verify in testing | OpenCHS / Primero teams |
| WF-009 | Confirm anonymous-reporter rule | Resolved | D-010/D-011 allow anonymous reporter but require child identifying details | Capture anonymity in mapping; minimum-child-field exceptions remain WF-004/DATA-005 | Primero / MGYSD / Child Helpline |

### C. Routing, acceptance and status feedback

| ID | Requirement to complete inception | Status | Evidence / current position | Closure action or evidence required | Owner |
|---|---|---|---|---|---|
| RT-001 | Obtain CPIMS+ service list | Pending | Service-based selection agreed; actual list outstanding under A-018 | Isaiah supplies approved list by 28 Oct and teams map service values | Primero technical team |
| RT-002 | Confirm service-based routing boundary | Resolved | D-008: helpline selects CPIMS+ service and Ministry distributes | Do not assume individual caseworker selection; configure actual recipients separately | Primero technical team |
| RT-003 | Define configured Ministry acceptance and distribution | Pending | Ministry distribution agreed; technical recipient/role rules still needed | Document receiving roles, accept/reject reasons and assignment permissions | MGYSD / CPIMS+ stakeholders |
| RT-004 | Define routing for non-Ministry stakeholders | Pending | Police, courts and other stakeholders may be reached through CPIMS+ accounts; configuration is not confirmed | Confirm accounts, service targets and actual availability | MGYSD / Primero team |
| RT-005 | Distinguish technical receipt and human acceptance | Resolved | D-016 closes the two acknowledgement stages for inception | Implement distinct evidence and states; detailed vocabulary remains RT-006 | OpenCHS / Primero teams |
| RT-006 | Define intermediate status vocabulary | Pending | Child Helpline identified a gap between referred/accepted and closed | Approve a small status set, update owner, privacy rules and display | Child Helpline / MGYSD / Primero |
| RT-007 | Define follow-up and return-update contracts | Pending | D-007 confirms two-way updates; outbound follow-up retained | Agree events, endpoints, ownership, reconciliation and permitted feedback fields | OpenCHS / Primero technical teams |
| RT-008 | Confirm two-way referred-case feedback | Resolved | D-007 confirms CPIMS+ status/intervention updates return to helpline | Implement bounded feedback; full unrestricted synchronisation is not authorised | Project steering authority |

### D. ABR ID and data requirements

| ID | Requirement to complete inception | Status | Evidence / current position | Closure action or evidence required | Owner |
|---|---|---|---|---|---|
| DATA-001 | Confirm ABR issuing authority | Resolved | D-014: NICR, Ministry of Home Affairs, as reported by Hopolang | Retain provenance; obtain authoritative examples through remaining A-007 work | Ministry / relevant registration authority |
| DATA-002 | Confirm optional ABR rule | Resolved | D-005: referral proceeds without ABR; caseworker obtains it later | Preserve non-blocking missing-ID behaviour and verify in UAT | MGYSD / Child Helpline |
| DATA-003 | Complete ABR validation and verification contract | Pending | D-014 agrees 12 digits, prefix 0/1, seventh digit 1 male or 2 female for initial checks | Obtain examples, invalid-value policy and any checksum/uniqueness/live-verification rules; A-007 remains open | Relevant authority / technical team |
| DATA-004 | Define subsequent ABR update contract | Pending | D-005 assigns later collection to receiving caseworker | Agree correction permissions, cross-system update event and audit history | MGYSD / OpenCHS / Primero |
| DATA-005 | Approve configured child identity mapping | Pending | D-011 requires child identifying details; D-012 confirms field set | Confirm exact minimum fields, API identifiers, conditional exceptions and mapping approval | Ministry / Isaiah / OpenCHS |
| DATA-006 | Approve nationality, age, sex and location mappings | Pending | Candidate fields and code mappings require CPIMS+ vocabulary | Confirm target fields, codes and partial-date/age rules | Project and Primero teams |
| DATA-007 | Approve protection-concern/category mapping | Pending | Session 2 says CPIMS+ uses multi-select protection concerns; standardized list pending | Obtain approved protection-concern list and mapping layer | Primero / MGYSD |
| DATA-008 | Approve reporter contact and anonymity mapping | Pending | Reporter contact included when available; anonymous reporter allowed | Map anonymous representation, optional contact and permitted disclosure | MGYSD / security / technical teams |
| DATA-009 | Approve perpetrator information mapping | Pending | D-012 includes perpetrator details | Confirm fields, unknown-value handling, conditional requiredness and access controls | MGYSD / technical teams |
| DATA-010 | Configure agreed attachments | Pending | D-012 includes attachments; call recordings and unagreed large media are not added | Agree file types, limits, scanning, consent or other basis, permissions and retention | Project steering authority |
| DATA-011 | Confirm narrative requirement at referral | Resolved | D-013: mandatory at referral, not at first save | Implement referral validation; privacy/redaction remains OPS-005 and configured mapping | Security / MGYSD / technical teams |

### E. API, environment and access

| ID | Requirement to complete inception | Status | Evidence / current position | Closure action or evidence required | Owner |
|---|---|---|---|---|---|
| API-001 | Accept supplied API specification as build basis | Resolved | D-017: BITZ accepts supplied specification unless it changes | Retain accepted reference; version under GOV-004 and configured operations under API-003 | Isaiah / OpenCHS technical lead |
| API-002 | Confirm authentication contract | Pending | Documented bearer JWTs expire after 60 minutes; valid-token reissue described; SSO preferred where an identity provider exists, username/password otherwise | Select user/backend flow, permissions, expiry recovery, secret delivery and rotation | Isaiah / identity / OpenCHS leads |
| API-003 | Confirm referral and follow-up endpoints | Pending | Upstream create, update and referral operations documented separately; Lesotho workflow fit unconfirmed | Agree operation sequence, returned ID, service routing and follow-up payload | Isaiah / Ministry / OpenCHS |
| API-004 | Confirm API errors, rate limits and timeout behaviour | Pending | Operation documentation referenced; Isaiah reports no rate limits and joint performance management | Agree error classes, retry/manual correction, timeouts, concurrency and performance acceptance | Isaiah / OpenCHS |
| API-005 | Confirm OpenCHS test/UAT environment | Pending | Test/UAT environment is being stood up with helpline application and API Gateway | Provide access, roles and connectivity evidence | OpenCHS technical team |
| API-006 | Complete sandbox readiness checklist | Pending | Session 3 records checklist incomplete; A-015 assigns Rantsala/Isaiah | Record checklist closure and blockers; source due 26 Oct | Rantsala / Isaiah |
| API-007 | Provide sandbox or global playground access | Pending | D-018 agrees playground fallback; A-016 assigns Isaiah | Provide URL, secure accounts, permissions and connectivity evidence by 28 Oct; record configuration limitations | Isaiah / Primero / infrastructure |
| API-008 | Confirm production environment and secret management | Pending | Production is not confirmed ready | Define endpoint, credentials, certificates, storage, rotation and rollback | Infrastructure / Primero / OpenCHS |
| API-009 | Confirm X-Road boundary | Resolved | D-015: direct API or OpenFN between systems; X-Road only for Home Affairs checks | Coordinate A-019/A-020; do not assume authorisation to build a new Home Affairs interface | Project governance |
| API-010 | Receive upstream API documentation | Resolved | Isaiah reference received and accepted in D-017 | Retain reference; deployment-specific details remain GOV-004/API-003 | Isaiah / Primero |

### F. Reliability, security and operations

| ID | Requirement to complete inception | Status | Evidence / current position | Closure action or evidence required | Owner |
|---|---|---|---|---|---|
| OPS-001 | Confirm durable queue and outage behaviour | Pending | Session 3 section 7 leaves delivery during outage open | Resolve A-021 by 28 Oct or during testing; record requirement and explicit dependency | OpenCHS technical team |
| OPS-002 | Approve retry and escalation policy | Pending | Retry intervals and error classes remain proposed | Define retryable errors, attempts, backoff, dead-letter and escalation | Technical / support owners |
| OPS-003 | Approve idempotency and duplicate reconciliation | Pending | Required; key and CPIMS+ lookup/reconciliation are open | Agree authoritative key and uncertain-timeout procedure | OpenCHS / Primero teams |
| OPS-004 | Define audit evidence | Pending | Minimum direction is case/reference ID, timestamp, transaction/result and API response | Approve final fields, retention, redaction and access | Security / technical teams |
| OPS-005 | Define sensitive-data masking and log access | Pending | Required controls are identified; exact policy is open | Approve fields to redact, role access and retention | Security / data protection owner |
| OPS-006 | Define monitoring and support ownership | Pending | Queue and referral failure escalation is not assigned | Name first-line, technical and receiving-system support owners | Project / Ministry / technical teams |
| OPS-007 | Confirm incident and outage procedure | Pending | A-021 outage handling open; privacy material due A-017 and research A-022 | Agree contacts, escalation and recovery; verify applicable incident requirements | Security / programme owner |

### G. UAT, acceptance, training and handover

| ID | Requirement to complete inception | Status | Evidence / current position | Closure action or evidence required | Owner |
|---|---|---|---|---|---|
| UAT-001 | Confirm Ministry-led UAT participant roles | Resolved | D-009 closes Ministry leadership and role categories for inception | Retain roles; named testers and signatories tracked under UAT-002 | Ministry / UAT lead |
| UAT-002 | Name UAT testers and signatories | Pending | Roles agreed; individuals, accounts and authorised signatories not supplied | Nominate testers, business and technical approval authorities | Project governance / Ministry |
| UAT-003 | Approve safe test data and environment | Pending | Child-journey use cases recommended; permission to use real child records not established | Approve synthetic dataset as proposed default, access, reset procedure and environment suitability | UAT lead / privacy owner |
| UAT-004 | Approve UAT scenarios | Resolved | Core scenarios are recorded, including manual trigger, ABR present/missing, emergency, routing, updates, rejection and audit | Convert to numbered test cases with expected evidence | UAT lead |
| UAT-005 | Test CPIMS+ service acceptance/rejection | Pending | Session 2 clarified this gate; test contract is not available | Add acceptance/rejection and reason evidence to UAT | Primero / Ministry / Child Helpline |
| UAT-006 | Test anonymity and child identification | Pending | Anonymous reporter permitted; child identifying details mandatory | Test approved minimum identity and exceptions, anonymous representation and safe messages | MGYSD / Primero |
| UAT-007 | Define defect severity and conditional go-live rules | Pending | Acceptance criteria exist but severity/workaround policy is open | Approve critical/high defect and waiver rules | Project steering authority |
| UAT-008 | Complete operator and support training | Pending | Training is required; materials and attendance are not evidenced | Prepare guides, train users and retain attendance/evidence | Project / operations |
| UAT-009 | Complete handover and go-live decision | Pending | Support, rollback, monitoring and sign-off are open | Approve readiness pack and record go/no-go decision | Project steering authority |

### H. Scope classification and previous deferrals

| ID | Scope item | Status | Boundary |
|---|---|---|---|
| DEF-001 | Previous deferral of referred-case feedback superseded | Resolved | D-007 brings two-way referred-case updates into scope; unrestricted synchronisation remains unauthorised |
| DEF-002 | Call recordings and large media not expressly agreed | Deferred | Attachments are now in scope under D-012; do not infer approval for unrestricted media |
| DEF-003 | OpenCHS case-plan synchronisation | Deferred | Each system maintains its own case plan |
| DEF-004 | Advanced Primero lookup administration | Deferred | Use approved lookup values; administration is out of MVP |
| DEF-005 | Generic integration marketplace/administration framework | Deferred | Implement only the configured provider capabilities required for MVP |
| DEF-006 | Major OpenCHS workflow redesign | Deferred | Preserve existing workflow unless an approved requirement requires change |
| DEF-007 | Non-essential reporting and analytics | Deferred | Retain only operational/audit evidence required for acceptance |
| DEF-008 | Automated production deployment pipeline | Deferred | Handle through the approved deployment process later |
| DEF-009 | New live Home Affairs interface implementation | Deferred | A-019/A-020 requirements coordination agreed; separate scope, ownership and implementation approval needed |

## 4. Inception completion gates

Before formal acceptance, receive pathways and privacy material; confirm applicability and complete mapping review of the received SOP; confirm service vocabulary and configured field mapping; resolve minimum-data exceptions, authentication and access prerequisites; agree bounded two-way feedback and outage requirements; name approval authorities and focal cover; and reconcile the implementation schedule. Any design work carried to testing needs explicit owner, milestone and acceptance of the dependency.

Do not reopen the accepted API specification, UAT role categories or agreed business rules as entirely unanswered questions. Their implementation detail and test evidence are separate. UAT execution, training and go-live remain later delivery gates. Formal report sign-off is not established by meeting attendance or by this update.

## 5. Approval record

| Role | Name | Decision | Date |
|---|---|---|---|
| Business owner |  |  |  |
| UNICEF programme/governance owner |  |  |  |
| OpenCHS technical lead |  |  |  |
| Primero technical lead |  |  |  |
| Data protection/security owner |  |  |  |
| UAT sign-off authority |  |  |  |
| Project manager |  |  |  |

Evidence update — 28 October 2026: see the current report’s Session 3 evidence reconciliation. A-014 document receipt is evidenced; applicability remains pending. Separate pathways/privacy actions and formal D1 approval remain open. The historical 26 October spreadsheet tracker has not been rewritten; use this update for the corrected A-014 status.

## Contract evidence update on 28 October 2026

The supplied TICAD-2026-001 text is recorded in the [planning extract](../07_source_documents/TICAD_2026_001_USER_SUPPLIED_CONTRACT_PLANNING_EXTRACT.md), not represented as a signed original. The current report separates original targets from a proposed recovery timetable. Component testing is due December 2026; integration and Ministry-led user testing with UNICEF sign-off are due January 2027; deployment, in-country training and handover are due February. Formal acceptance remains pending.

| Follow-up | Owner | Next action and required evidence |
|---|---|---|
| Contract identity and execution (CD-02) | UNICEF / BITZ | Supply signed governing contract and confirm relationship to earlier reference |
| Access date and week references (CD-07/CD-08) | UNICEF / Primero | Reconcile August/Week 4 requirement and end-November assumption; commit usable access date with test evidence |
| ABR checks (CD-05; A-007) | UNICEF / Home Affairs | Supply official rules, check-digit algorithm and at least 10 valid examples; agree interim treatment if needed |
| User-testing approval (CD-09) | UNICEF / Ministry | Name UNICEF signatory and confirm Ministry endorsement; schedule January tests and corrections |
| Data-sharing agreements | UNICEF / Ministry | Confirm agreement status and authority for real-case sharing before deployment |
| Maintenance after launch (CD-10) | BITZ / UNICEF | Confirm actual launch-based 90-day support dates, contacts and administration beyond February |
| Submission and review (CD-11) | BITZ / UNICEF | Confirm templates and electronic/hard-copy delivery; allow five working days for review and time for corrections |
| Fault acceptance (CD-12) | UNICEF | Confirm resolution to UNICEF satisfaction; earlier waiver proposals are not contractual approval |

Reporting: weekly meetings, minutes within 24 hours, monthly reports on the last working day. Earlier tracker due dates remain historical; no completion or extension is inferred from this update.
