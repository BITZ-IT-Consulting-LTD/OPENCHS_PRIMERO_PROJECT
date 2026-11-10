# Draft Inception Report D1
## Lesotho Child Helpline 116 and Primero CPIMS Integration

**Document status:** Draft for stakeholder review following Session 3  
**Version:** 0.5  
**Date:** 26 October 2026  
**Prepared for:** UNICEF Lesotho, MGYSD and Child Helpline 116 stakeholders  
**Prepared by:** BITZ OpenCHS project team  
**Initial draft circulation target:** 28 October 2026, close of business, as recorded in Session 3  
**Commercial planning reference:** [Contract-Aligned Delivery Plan](../02_project_management/CONTRACT_ALIGNED_DELIVERY_PLAN.md)

## 1 Executive summary

The integration will support manual referrals from OpenCHS to Primero CPIMS+ and return updates about referred cases to the Child Helpline. Session 3 on 26 October 2026 confirmed this two-way direction, the referral field set, anonymous reporters, optional ABR IDs, service-based routing and Ministry-led UAT. These decisions replace conflicting positions in the earlier drafts.

Child identifying details are required for referral. The case narrative is mandatory when referring a case, rather than when first saving it. An anonymous reporter is permitted, and an unavailable ABR ID must not prevent referral. Attachments and follow-up updates are included in the agreed field set; the helpline case plan is excluded. Configured field identifiers, conditional validation, code lists and attachment controls still require technical mapping.

The API specification supplied by Isaiah is accepted as the build basis unless it changes. Authentication and actual environment access remain outstanding. The Lesotho sandbox checklist was incomplete at the meeting; the agreed fallback is Primero’s global playground if the sandbox is unavailable when the draft is complete. No access, test result or production readiness is asserted by this report.

The initial draft is due on 28 October, with remaining requirements followed up individually. Formal inception approval remains pending. The July 2026 to February 2027 commercial planning reference is retained; Session 3 does not approve a new contract schedule or establish that earlier milestones were completed.

## 2 Purpose and objectives

This report establishes the Workstream 1 baseline for inception, requirements and environment setup. It records agreed business requirements, the proposed technical approach, outstanding decisions, responsibilities and acceptance gates so stakeholders can review the implementation baseline.

The objectives are to document the referral lifecycle and two-way feedback; map the agreed fields and ABR rules; establish authentication, environments and security requirements; define reliability and audit controls; and agree UAT, support and approval responsibilities. Technical implementation and test execution must produce their own evidence after requirements are approved.

## 3 Sources and evidence precedence

The current baseline uses:

- [Session 3 minutes](<../03_meetings/session_3/OpenCHS & Primero CPIMS+ Integration — Session 3 Minutes.pdf>), dated 26 October 2026: sections 3–13, decisions D-005–D-018 and actions A-013–A-025.
- [Session 1 minutes](../03_meetings/session_1/SESSION_1_MINUTES.pdf), 8 October, and [Session 2 minutes](../03_meetings/session_2/SESSION_2_MINUTES.pdf), 9 October, for retained context and earlier actions.
- [Isaiah’s response](../06_correspondence/ISAIAH_RESPONSE_SOURCE_2026-10-26.md), recorded on 26 October; the email’s sent date was not supplied.
- [Primero API reference](https://github.com/primeroIMS/primero/blob/development_v2/app/controllers/api/README.md) and [token documentation](https://github.com/primeroIMS/primero/blob/development_v2/app/controllers/api/v2/docs/tokens/post.md), previously reviewed on 26 October. The development branch does not establish the deployed Lesotho version.
- [Original source documents](../07_source_documents/README.md), [technical reference material](../05_technical_reference/README.md) and the contract-aligned delivery plan for scope and planning context.

Where Session 3 expressly updates an earlier position, Session 3 governs this draft. The source minutes record agreement, not signed approval of the entire report. Technical proposals remain proposals. Earlier facilitation notes and capture templates are historical or working material and must be reconciled before reuse; their older one-way or attachment-deferral statements do not override this report.

The [completion inventory](INCEPTION_COMPLETION_INVENTORY.md) tracks unresolved requirements. The [Session 3 action tracker](../03_meetings/session_3/SESSION_3_ACTION_TRACKER_2026-10-26.xlsx) records actions and contacts. A promised document is not treated as received until evidence is filed. No application-code or live deployment audit was performed for this update.

## 4 Current baseline

| Area | Position recorded | Remaining confirmation |
|---|---|---|
| Direction | Two-way updates for referred cases | Feedback events, permitted fields, mechanism and conflict rules |
| Initiation | Manual action by the handling agent | Escalation, exceptional approvals and cancellation rules |
| Routing | Agent selects a CPIMS+ service; Ministry distributes | Actual service list and configured recipient permissions |
| Identification | Anonymous reporter allowed; child identifying details required | Exact minimum dataset and emergency exceptions |
| ABR ID | Optional; NICR format agreed for initial validation | Examples, authoritative verification and later-update contract |
| API | Supplied specification accepted for the build | Deployment version, authentication and configured operation sequence |
| Environment | Lesotho sandbox, with global playground fallback | Checklist closure and secure access package |
| UAT | Ministry leads; participant roles accepted | Named testers, accounts, dataset and signatories |

## 5 Scope

### 5.1 Agreed integration scope

The scope covers agent-triggered referral; validation of the agreed information; service selection and Ministry receipt/distribution; technical receipt and human acceptance or rejection; OpenCHS follow-up information; and return of CPIMS+ case status and intervention updates to the linked helpline case. It includes the agreed attachments field, optional ABR capture and initial format checks, traceable case linkage, duplicate prevention, audit evidence and operational failure visibility.

Two-way integration is limited to information about referred cases approved for sharing. It does not authorise unrestricted copying of CPIMS+ case files, case plans or unrelated records. Transport, status vocabulary, access controls and update ownership remain to be designed.

### 5.2 Boundaries retained

The helpline case plan is not transmitted. Call recordings and large media not expressly agreed, major workflow redesign, advanced lookup administration, a generic integration marketplace, non-essential analytics and an automated production deployment pipeline remain outside the current baseline unless separately approved. Agreement to attachments does not itself authorise transfer of call recordings or unrestricted files.

There is no X-Road hop between OpenCHS and CPIMS+. API-to-API or OpenFN remains a Ministry/technical architecture choice. Home Affairs ID verification is coordinated through the separate X-Road sessions; participation in those sessions is agreed, but a new live Home Affairs interface is not silently added to BITZ’s implementation scope.

## 6 Referral lifecycle

1. The agent receives the call, records the contact and saves the helpline case. The referral narrative need not be complete at this initial save.
2. The handling agent elects to refer the case and selects an approved CPIMS+ service.
3. OpenCHS validates the referral narrative and required child-identifying information. It allows an anonymous reporter and an absent ABR ID.
4. The integration submits the agreed data and records a system acknowledgement or a failure requiring recovery.
5. The receiving party accepts or rejects the referral through the agreed CPIMS+ workflow. System receipt does not prove human acceptance or immediate case-management commencement.
6. Ministry users distribute/assign the case internally. Selecting a service does not imply that the helpline selects an individual caseworker.
7. OpenCHS sends follow-up information against the linked case. CPIMS+ returns approved status and intervention updates to the helpline.
8. Closure and any correction, cancellation or re-referral retain linkage and an auditable history, with detailed rules still to be agreed.

Existing emergency phone contact with police or first responders continues alongside system referral. The integration records and tracks that response; it does not replace urgent calls.

## 7 Business rules and exceptions

Session 3 accepts the manual referral process as presented. National referral pathways already exist: Rantsala will share them, and Hopolang will resend the SOPs. BITZ will use those documents rather than create a new national pathway.

Anonymous reporting and unidentified children are different situations. A reporter may remain anonymous and be recorded as such in CPIMS+. The child must have identifying details and location sufficient for follow-up. The exact minimum identifying fields, incomplete-child-information scenarios and emergency exceptions must be settled against the SOPs and configured forms. Do not infer that every bio-data field is always mandatory.

Supervisor escalation, refusal reasons, corrections, withdrawal, hoax/prank updates and re-referral need explicit permissions and history rules. An OpenCHS change must not automatically close or overwrite a CPIMS+ case without an agreed update contract.

Outage handling is open under A-021. Durable queueing, retry intervals, operator escalation, safe resubmission and reconciliation are proposed controls pending agreement or testing. No automatic retry count or outage service level is approved by these minutes.

## 8 Technical architecture

The proposed flow is OpenCHS and its integration/API Gateway component to CPIMS+, with an authorised return channel for linked case updates. The Ministry and technical teams must choose API-to-API or OpenFN. The architecture must distinguish system receipt, business acceptance/rejection, assignment and case progress.

A configurable integration provider remains a technical recommendation: mapping, credential handling, job tracking, connection checks and reliability controls should reuse existing capabilities where suitable. Both outbound referrals and agreed inbound feedback are required by the Session 3 scope; feedback is no longer merely a future extension.

Before design sign-off, Peter and Marlon must verify the actual case model, integration framework, queue, role permissions, audit facilities, deployment and secret-management arrangements. Isaiah must confirm receiving-system capabilities, service configuration and permissions. A reference architecture is not evidence that these components are installed or working.

## 9 ABR identifier requirements

Session 3 D-005 and D-014 record the following initial baseline, reported by Hopolang after contact with Home Affairs:

| Attribute | Agreed rule |
|---|---|
| Issuing authority | NICR, Ministry of Home Affairs |
| Length | 12 digits |
| Prefix | First digit is 0 or 1 |
| Gender position | Seventh digit: 1 for male, 2 for female |
| Requiredness | Optional; referral proceeds when unavailable |
| Missing identifier | Receiving caseworker obtains it during follow-up |
| Initial validation | Use the recorded structural rules |

Store the identifier as text to preserve leading zeroes. Structural checks do not establish that the identifier exists or belongs to the child. A-007 remains open for the remaining verification contract: authoritative examples, any checksum or uniqueness rules, invalid-value handling, corrections, update permissions and the live verification route. The minutes do not provide a checksum algorithm or a working Home Affairs endpoint.

UNICEF and Isaiah will invite BITZ to the Primero/X-Road sessions (A-019). Melusi will obtain Berea workshop use cases (A-020). The resulting Home Affairs requirements and responsibilities must be agreed before any additional implementation commitment.

## 10 Referral fields and mapping

Session 3 D-012 confirms the following field set. It is a business payload baseline, not a deployed API schema. Mandatory rules explicitly established by the meeting are identified below; other conditional requiredness and unknown-value handling need mapping confirmation.

| Information | Business requirement | Technical mapping still needed |
|---|---|---|
| Child name and location | Identifying details required to trace the child | Name parts, minimum identity, location hierarchy and exceptions |
| Age, sex, nationality and child contact | Included in the agreed bio-data set | Types, codes, estimated age and unavailable-contact handling |
| Case category | Included; protection-concern mapping needed | Multi-select codes and approved transformations |
| Case narrative | Mandatory at referral, not first save | Target field, length and permitted sensitive content |
| Reporter contact | Included when available; anonymous reporter allowed | Anonymous flag/value, optional contact and privacy rules |
| Perpetrator details | Included in the agreed set | Fields, unknown details, access and conditional validation |
| Attachments | Included | File types, size, scanning, permissions and retention |
| Follow-up updates | Included; linked to the original case | Events, ownership, timestamps and update permissions |
| ABR ID | Optional; structural validation as above | Target field, blank representation and subsequent correction |
| CPIMS+ feedback | Status and interventions returned to helpline | Approved values, minimisation, delivery and reconciliation |
| Helpline case plan | Not transmitted | Exclude from the shared payload |
| External case reference | Proposed technical linkage requirement | Stable identifier, returned case ID and duplicate lookup support |

Prior developer examples such as `abr_id`, `openchs_reference_id`, `name_first`, `name_last`, `protection_concerns`, `location_current` and `referral_notes` remain candidate field names, not confirmed Lesotho schema. Date-of-birth, risk-level, module and referral-source examples require explicit mapping approval before transmission; their presence in earlier technical material does not expand the agreed field set.

Each mapping must identify source and target, direction, datatype, requiredness, validation, transformations, lookup values, sensitivity and approving owner. Isaiah supplies configured definitions and lookup lists; Ministry and OpenCHS stakeholders approve the business mapping. Service vocabulary is due under A-018; a complete field dictionary has no separate confirmed delivery date in the minutes.

## 11 API and authentication


The upstream API documentation supplied by Isaiah describes API v2. Session 3 D-017 accepts this specification as the build basis unless it changes, closing specification receipt for inception. The applicable Lesotho release, base URL, configured schema and operation sequence remain to be captured. The `development_v2` branch is a moving reference; retain a release or commit reference agreed with Primero before implementation.

Documented operations are `POST /api/v2/tokens`, `POST /api/v2/cases`, `PATCH /api/v2/cases/:id`, and `POST /api/v2/cases/:id/referrals`. Case creation and referral are separate operations. The upstream index describes referral as granting an additional user access, and transfer as changing ownership through acceptance/rejection. Primero and Ministry stakeholders must confirm the operation sequence that supports Lesotho’s service-based routing; an endpoint’s existence does not establish that fit.

The token documentation describes a bearer JWT in the response Authorization header, 60-minute expiry, issuance using username/password, and reissue using a valid existing token. Reissue does not invalidate other unexpired tokens. Isaiah prefers SSO where an identity provider is available; username/password is an alternative. The unattended OpenCHS backend flow, recovery after expiry, permissions and secret rotation remain Pending. User SSO choice alone does not settle integration authentication.

Isaiah confirms that the Primero team will set up credentials once implementation is ready. He confirms that network/security controls apply without identifying which controls. Obtain the actual TLS/certificate, VPN, IP allowlisting and other prerequisites; do not infer that every listed control applies.

Isaiah reports no API rate limits and proposes joint performance management. Concurrency, payload limits, timeouts, retry/manual-correction rules and performance acceptance remain to be agreed. Generic examples do not establish configured Lesotho payloads. Detailed case-create/referral schemas and error examples were not verified in this review.

The API contract must provide:

- Sandbox/UAT and production base URLs.
- Authentication endpoint and request schema.
- Token response, expiry, and refresh behaviour.
- Case-creation endpoint and method.
- Required headers and content type.
- Request and response examples.
- Error codes and error-body structure.
- Rate limits and timeout expectations.
- Duplicate/idempotency support.
- Supported lookup and form endpoints, if required.
- TLS, certificate, VPN, IP allowlisting, or firewall requirements.

### 11.1 Configuration and field dictionary dependencies

The Ministry and Child Helpline must supply current SOPs, paper referral forms, approved child-journey use cases and existing referral pathways, with receipt of existing pathways tracked under A-013/A-014. Primero will use these to configure the demo; Isaiah expects API field definitions and lookup/code lists to be available after setup. The teams must jointly capture the resulting integration specification because Isaiah reports no existing interface specification.

Session 3 now establishes ABR issuing authority, structural format and optional status as set out in section 9. The target field, remaining verification contract, duplicate-prevention mechanism and two-way status transport still need technical confirmation.


## 12 Reliability and audit

The proposed delivery design uses durable referral records, a stable correlation reference and auditable transmission attempts. It must distinguish unsent, awaiting system receipt, received, accepted, rejected and later case-progress information without equating technical delivery with case closure. The final state vocabulary is pending.

Retries must not create duplicate cases. The technical teams must agree an external reference or supported idempotency mechanism, lookup/reconciliation after uncertain timeouts, error classification, backoff, operator intervention and dead-letter handling. Apply equivalent controls to repeated or out-of-order feedback events. Conflicting updates need explicit ownership and reconciliation rather than blind overwrites.

Audit records should include case/reference identifiers, timestamps, actor/system, action and transaction outcome. Record response metadata safely; full child payloads, tokens and unrestricted API bodies should not be logged by default. Retention, redaction and audit access remain approval items. A-021 covers the unresolved outage scenario and must produce an agreed requirement or an explicitly accepted testing-stage dependency.

## 13 Data protection and security

UNICEF will supply earlier Ministry data-protection work, data management policy and applicable legal material under A-017. Nelson will complete desk research under A-022. The minutes contain different descriptions of the legal material and its status; the report does not determine which legislation is applicable or in force. Obtain the documents and confirm the legal basis with the responsible Ministry/UNICEF advisers.

The design must establish authorised sharing purposes, minimum necessary fields, consent or other applicable basis, permissions, protected transfer/storage, credential custody, retention, audit access and incident escalation. Reporter anonymity must survive the transfer. Return updates and attachments need equivalent disclosure controls. Confirm required certificates, VPN or allowlisting with Primero rather than assuming every possible control applies.

Use an approved synthetic child-journey dataset as the proposed testing default. A demo environment and the email’s general reference to test data do not establish permission to copy real child records.

## 14 Responsibilities and governance

| Party | Recorded responsibility | Still to be confirmed |
|---|---|---|
| Nelson and BITZ | Coordination, report, requirements follow-up and desk research | Final report approval route and dependency rebaseline |
| Peter and Marlon | Helpline integration, gateway and authentication/test preparation | Detailed design and execution evidence |
| Isaiah | Primero technical coordination, access and service list | Configured contract and authentication |
| Hopolang | Ministry coordination, SOPs and helpline leave cover | Permanent focal person and cover appointment |
| Rantsala | Session 3 chair, pathways and checklist follow-up | Named programme approval authority |
| Melusi | Ministry IT and Berea use-case follow-up | Workshop documents and resulting requirements |
| Ministry and Child Helpline | Workflow ownership and Ministry-led UAT | Named testers, business/security signatories and support ownership |

UNICEF attended Session 3 through Rantsala and Daniel. The action register assigns A-017 and part of A-019 to Lekhanya, while the discussion names Daniel as offering the materials. Confirm the named UNICEF action owner without assuming these names identify the same person. No Child Helpline agent or social worker attended; a Child Protection Services representative spoke for the helpline. Mary Damposi’s attendance and permanent focal-person appointment were not confirmed.

## 15 Environments and readiness

The Lesotho sandbox checklist was incomplete on 26 October. A-015 assigns Rantsala and Isaiah a same-day follow-up. A-016 assigns Isaiah access provision by 28 October. If the Lesotho environment is not ready by draft completion, Session 3 agrees the global playground fallback; neither a URL nor working credentials is supplied in the minutes.

The access package must record environment/version, base URL, named/service accounts, permissions, authentication, network prerequisites and safe test data. Confirm which country configuration and fields the playground supports and which tests will need repeating on the configured Lesotho environment. The earlier primerodev.org option in Isaiah’s email is historical context and does not establish the global playground’s URL.

OpenCHS UAT access, production endpoints, secret rotation and production readiness also need evidence. Environment availability and test success remain separate gates.

## 16 UAT and acceptance

Session 3 closes the UAT leadership and participant-role question for inception: the Ministry leads, with OpenCHS developers, Child Helpline agents, Ministry system administrator, CPIMS+ users, district supervisors and other Ministry users who receive, distribute, investigate or close referrals. Named testers, accounts and authorised signatories remain pending.

The test plan must include manual referral; saving before narrative completion and blocking referral without narrative; identified child with anonymous reporter; ABR present, absent and structurally invalid; minimum-information emergency handling; service routing; separate system receipt and human accept/reject; perpetrator information; attachment permissions; subsequent ABR correction; OpenCHS follow-ups; CPIMS+ status/intervention feedback; duplicate and out-of-order delivery; outages and reconciliation; privacy, access and audit controls.

These are planned acceptance scenarios, not completed tests. Each needs an expected result, tester, environment, evidence and defect outcome. Approve severity and exception rules before execution. UAT execution, training, support handover and go-live acceptance are subsequent delivery gates, not prerequisites for merely circulating the inception draft.

## 17 Delivery plan and dependencies

The Workstream 1 target is an initial draft on 28 October 2026 close of business. The source does not specify an exact hour or timezone. Follow-up on outstanding documents, service list, coordination cover and outage requirements is planned for 26–27 October.

The commercial planning reference remains 1 July 2026 to 28 February 2027, with milestone targets in August, October, November and February. Earlier 14-week and ten-day/two-week technical schedules are historical references, not a newly approved implementation promise. The outstanding August milestone and the effort implications of confirmed two-way updates and attachments require schedule reconciliation by project governance.

The dependency sequence is existing SOPs/pathways and approved use cases → configured environment and access → confirmed mapping/authentication and feedback design → integration and recovery testing → Ministry-led UAT → authorised handover/go-live. Some design work can proceed in parallel. Global playground access can enable preliminary tests but does not eliminate country-configuration validation.

## 18 Risk register

| Risk | Effect | Action and owner |
|---|---|---|
| R-001 Sandbox/access delay | Blocks configured mapping and integration tests | Rantsala/Isaiah close checklist; Isaiah provides access or playground under A-015/A-016 |
| R-002 Country documents not received | Requirements cannot be checked against approved practice | Rantsala pathways, Hopolang SOPs, UNICEF privacy materials; retain receipt evidence |
| R-003 Field and service configuration incomplete | Invalid payloads or misrouting | Isaiah service list A-018; technical and Ministry teams approve mappings |
| R-004 Outage and duplicate recovery unresolved | Lost, repeated or uncertain referrals | Nelson/Peter/Isaiah resolve A-021 and test recovery |
| R-005 ABR verification dependency | Format-valid IDs may remain unverified | Carry A-007; coordinate A-019/A-020; keep missing ABR non-blocking |
| R-006 Two-way design and schedule impact | Extra implementation effort or disclosure risk | Technical teams define bounded feedback; governance reconciles scope, effort and milestones |
| R-007 Privacy and authority gaps | Unauthorised sharing or unclear approvals | UNICEF materials A-017, Nelson research A-022; Ministry confirms approval owners |
| R-008 Focal-person or support gaps | Delayed review, UAT and incident resolution | Hopolang appoints cover A-024 and permanent focal A-002; name support owners |

All risks remain open until evidence supports closure. An action due date is not evidence that the risk is resolved.

## 19 Decisions and actions

The decision identifiers below are the canonical Session 3 minutes identifiers. Earlier v0.4 report-local decision numbering is preserved in the archive and must not be treated as equivalent solely because the numbers match.

| ID | Decision recorded in Session 3 |
|---|---|
| D-005 | ABR optional; receiving caseworker obtains it later if missing |
| D-006 | Manual handling-agent referral and process as presented |
| D-007 | Two-way integration for referred-case updates |
| D-008 | Ministry distribution through helpline selection of CPIMS+ services; list pending |
| D-009 | Ministry-led UAT with the recorded participant roles |
| D-010 | Anonymous reporter allowed |
| D-011 | Child identifying details mandatory for referral |
| D-012 | Field set confirmed; helpline case plan excluded |
| D-013 | Narrative mandatory at referral, not initial save |
| D-014 | NICR identifier format used for initial validation |
| D-015 | Direct API or OpenFN connection; X-Road only for Home Affairs checks |
| D-016 | Separate system receipt and human accept/reject acknowledgements |
| D-017 | Supplied API specification accepted unless it changes |
| D-018 | Global playground fallback if Lesotho sandbox is not ready |

These decisions are agreed in the supplied minutes. Approval of the complete report remains pending.

| ID | Action | Owner | Recorded due |
|---|---|---|---|
| A-013 | Share national referral pathways | Rantsala | 26 Oct 2026 |
| A-014 | Resend case management SOPs | Hopolang | 27 Oct 2026 |
| A-015 | Complete sandbox checklist and post-meeting follow-up | Rantsala, Isaiah | 26 Oct 2026 |
| A-016 | Provide sandbox or playground access | Isaiah | 28 Oct 2026 |
| A-017 | Share Ministry privacy work, policy and legal material | Lekhanya, UNICEF; identity to clarify | 26 Oct 2026 |
| A-018 | Confirm CPIMS+ service list | Isaiah | 28 Oct 2026 |
| A-019 | Invite BITZ to Primero/X-Road sessions | Lekhanya, Isaiah | Next session; date unconfirmed |
| A-020 | Share Berea workshop use cases | Melusi | 27 Oct 2026 |
| A-021 | Agree outage/referral delivery handling | Nelson, Peter, Isaiah | 28 Oct or during testing |
| A-022 | Research data protection requirements | Nelson | 28 Oct 2026 |
| A-023 | Set up API authentication and start test calls | Peter, Marlon | After A-016 |
| A-024 | Name helpline coordination leave cover | Hopolang | 27 Oct 2026 |
| A-025 | Deliver initial inception draft | Nelson, BITZ | 28 Oct, close of business |

All source actions require completion evidence. This v0.5 document provides the revised draft for A-025; circulation and stakeholder receipt are not yet evidenced. A-002, permanent Child Helpline focal person, and A-007, remaining ABR verification rules, carry forward without a newly stated due date. A-019 is dependency coordination and A-023 is subsequent technical execution; neither is represented as a completed Workstream 1 requirement.

## 20 Inception completion gates

The report can be circulated as a draft while disclosed gaps remain. Formal D1 acceptance requires authorised review of the recorded decisions and either closure of outstanding requirements or explicit acceptance of bounded dependencies, with owner, evidence and due milestone.

Outstanding closure work is: receipt and review of pathways/SOPs/privacy materials; service list and configured mapping; minimum-data exceptions; authentication/access prerequisites; two-way feedback and outage requirements; named approval authorities and helpline cover; and a reconciled delivery baseline. Items intentionally left to testing must be identified as such rather than silently marked resolved.

API specification acceptance, UAT participant roles, anonymity, optional ABR and integration direction should not be reopened as wholly unanswered questions. Their detailed implementation and test evidence remain separately tracked in the completion inventory. Training, production operations and go-live checks remain later delivery gates.

## 21 Review and approval

| Approval role | Name | Decision and date |
|---|---|---|
| Ministry business owner | To confirm | Pending |
| UNICEF programme/governance | To confirm | Pending |
| OpenCHS technical authority | To confirm | Pending |
| Primero technical authority | To confirm | Pending |
| Data protection/security authority | To confirm | Pending |
| Ministry UAT signatory | To confirm | Pending |
| Project coordination | Nelson Adagi | Circulation and review tracking pending |

## Revision record

| Version | Date | Change |
|---|---|---|
| 0.4 | 26 Oct 2026 | Sessions 1–2 and Isaiah response; superseded draft preserved in archive |
| 0.5 | 26 Oct 2026 | Session 3 decisions, two-way scope, fields, ABR, routing, actions and close-out dependencies incorporated; formal approval pending |
