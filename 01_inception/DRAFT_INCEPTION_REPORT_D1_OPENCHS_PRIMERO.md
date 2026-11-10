# Draft Inception Report D1
## Lesotho Child Helpline 116 and Primero CPIMS Integration

**Document status:** Draft for stakeholder review following Session 3  
**Version:** 0.6  
**Date:** 27 October 2026  
**Contract reference:** UNICEF Lesotho Contract No. 43427866, Amendment 3 — Workstream 1 / Deliverable D1  
**Prepared for:** UNICEF Lesotho, MGYSD and Child Helpline 116 stakeholders  
**Prepared by:** BITZ IT Consulting Ltd, OpenCHS project team  
**Initial draft circulation target:** 28 October 2026, close of business, as recorded in Session 3  
**Commercial planning reference:** [Contract-Aligned Delivery Plan](../02_project_management/CONTRACT_ALIGNED_DELIVERY_PLAN.md)

## 1 Executive summary

The integration will support manual referrals from OpenCHS to Primero CPIMS+ and return updates about referred cases to the Child Helpline. Session 3 on 26 October 2026 confirmed this two-way direction, the referral field set, anonymous reporters, optional ABR IDs, service-based routing and Ministry-led UAT. These decisions replace conflicting positions in the earlier sessions and drafts.

Child identifying details are required for referral. The case narrative is mandatory when referring a case, rather than when first saving it. An anonymous reporter is permitted, and an unavailable ABR ID must not prevent referral. Attachments and follow-up updates are included in the agreed field set; the helpline case plan is excluded. Configured field identifiers, conditional validation, code lists and attachment controls still require technical mapping.

The API specification supplied by Isaiah is accepted as the build basis unless it changes. For this version the upstream Primero v2.16.0 source and API documentation were reviewed directly (section 13). They show three capabilities relevant to the open design questions: a client-generated case identifier that the API rejects as a conflict if repeated, a referral status model with acceptance, rejection and completion outcomes, and configurable outbound webhooks that could carry return updates. These are product capabilities, not evidence of the Lesotho configuration. They also show that an API referral is addressed to a receiving user, so the agreed service-based routing must be translated into configured recipients.

Authentication and actual environment access remain outstanding. The Lesotho sandbox checklist was incomplete at the meeting; the agreed fallback is Primero’s global playground if the sandbox is unavailable when the draft is complete. No access, test result or production readiness is asserted by this report.

Two governance matters need attention alongside review of this draft. First, the contract scope describes an outbound integration; Session 3 confirmed two-way updates, which adds design and effort that the contract milestones do not yet reflect. Second, the contract validity recorded in the technical scope brief differs from the delivery baseline in the contract-aligned plan (section 3). Both need reconciliation by project governance. Formal inception approval remains pending; Session 3 does not approve a new contract schedule or establish that earlier milestones were completed.

## 2 Purpose and objectives

This report establishes the Workstream 1 baseline for inception, requirements and environment setup. It records agreed business requirements, the proposed technical approach, outstanding decisions, responsibilities and acceptance gates so stakeholders can review the implementation baseline before Workstreams 2–4 proceed.

The objectives are to document the referral lifecycle and two-way feedback; map the agreed fields and ABR rules; establish authentication, environments and security requirements; define reliability and audit controls; and agree UAT, support and approval responsibilities. Technical implementation and test execution must produce their own evidence after requirements are approved.

## 3 Contract context and workstreams

The technical scope brief prepared for the 24 September 2026 inception meeting describes the assignment under Contract No. 43427866, Amendment 3. The work strengthens the Child Helpline 116 / OpenCHS environment through requirements definition, configuration, outbound API integration, testing, user acceptance, capacity building and go-live support, within a continuing support-and-maintenance TOR.

| Workstream / deliverable | Contract scope | Contract-aligned target | Relationship to this report |
|---|---|---|---|
| D1 Inception, Requirements & Environment Setup | Business and technical requirements, architecture, environments, access, workflow and implementation plan | August 2026 | This report and its supporting registers |
| D2 ABR ID Field, Validation & Referral Checkbox UI | ABR field, validation rules, referral control and status display in OpenCHS | October 2026 | Requirements in sections 8, 9, 11 and 12 |
| D3 Outbound REST API Client | JWT authentication, retries, offline queue, idempotency and audit logging | November 2026 | Requirements in sections 10, 13 and 14 |
| D4 Testing, UAT, Training & Go-Live | Technical testing, UAT, operator and IT training, deployment and handover | February 2027 | Requirements in sections 17 and 18 |

The brief expects the inception phase to produce an inception report, a requirements specification, an integration design and field-mapping document, and an action register for unresolved items. This report combines the requirements baseline and integration design. The field-mapping document cannot be completed until Isaiah supplies configured field definitions (section 12). The completion inventory and Session 3 action tracker serve as the action and open-issue registers.

The brief records contract validity as 10 March 2025 to 7 July 2027. The contract-aligned delivery plan uses 1 July 2026 to 28 February 2027 as the delivery baseline, based on dates supplied by the project owner. These may describe the overall contract and the Amendment 3 delivery window respectively, but no source in the workspace says so. Project governance should confirm which dates govern milestones, acceptance and payment.

The brief anticipated an outbound-only integration and asked inception to confirm whether status information must be written back into OpenCHS. Session 3 D-007 now confirms two-way updates for referred cases. This answers the brief’s question but extends D3 beyond its contract description; the change in effort, milestones and acceptance evidence requires a governance decision (R-010).

## 4 Sources and evidence precedence

The current baseline uses:

- [Session 3 minutes](<../03_meetings/session_3/OpenCHS & Primero CPIMS+ Integration — Session 3 Minutes.pdf>), dated 26 October 2026: sections 3–13, decisions D-005–D-018 and actions A-013–A-025.
- [Session 1 minutes](../03_meetings/session_1/SESSION_1_MINUTES.pdf), 8 October, and [Session 2 minutes](../03_meetings/session_2/SESSION_2_MINUTES.pdf), 9 October, for retained context, decisions D-001–D-004 and earlier actions.
- [Isaiah’s response](../06_correspondence/ISAIAH_RESPONSE_SOURCE_2026-10-26.md), recorded on 26 October; the email’s sent date was not supplied.
- The [annotated requirement checklist](<../03_meetings/CHL intergration with Primero Requirement Checklist.docx>) filed for Session 3. Its remarks record the NICR ABR format, proposed UAT participants and sign-off, and a data protection reference. The author and date of the remarks are not recorded, so they are treated as positions for confirmation.
- The [technical scope brief](../07_source_documents/Lesotho_OpenCHS_Technical_Scope_Inception_Brief.pdf) of 24 September 2026 and the contract-aligned delivery plan for scope and planning context.
- The Primero source repository held locally at version 2.16.0 (commit `622e0d2d6d`, 19 October 2026), including its API documentation under `doc/api/`. The [public API reference](https://github.com/primeroIMS/primero/blob/development_v2/app/controllers/api/README.md) was reviewed on 26 October. Neither establishes the release or configuration deployed for Lesotho.
- [Technical reference material](../05_technical_reference/README.md) for prior design context only.

Where Session 3 expressly updates an earlier position, Session 3 governs this draft. The source minutes record agreement, not signed approval of the entire report. Technical proposals remain proposals. Earlier facilitation notes, slides and capture templates are historical or working material. Their older one-way or attachment-deferral statements do not override this report; the Session 3 facilitation deck, for example, proposed deferring attachments, which the meeting then included.

The [completion inventory](INCEPTION_COMPLETION_INVENTORY.md) tracks unresolved requirements. The [Session 3 action tracker](../03_meetings/session_3/SESSION_3_ACTION_TRACKER_2026-10-26.xlsx) records actions and contacts. A promised document is not treated as received until evidence is filed. As at 27 October no receipt of the pathways, SOPs, privacy material, sandbox checklist or service list is filed in the workspace. No OpenCHS application-code or live deployment audit was performed for this update.

## 5 Inception process and evolution of requirements

Workstream 1 requirements were gathered through a scope briefing and three facilitated sessions:

| Date | Session | Focus and participation |
|---|---|---|
| 24 Sep 2026 | Inception meeting (brief) | Technical scope, workstreams and decisions to close |
| 8 Oct 2026 | Session 1 — Business and workflow | OpenCHS walkthrough; Child Helpline social workers, supervisors and the CPIMS focal person attended; UNICEF absent |
| 9 Oct 2026 | Session 2 — Technical architecture | Live CPIMS+ referral demonstration; smaller technical group |
| 14 Oct 2026 | Technical follow-up call | Referenced in Nelson’s circulated requirements email; no minutes or outcome filed |
| 26 Oct 2026 | Session 3 — Closing requirements | Final confirmations; UNICEF, Ministry IT, Primero and BITZ attended; no Child Helpline agent or social worker attended |

Several positions changed during inception. The table records the progression so that reviewers do not rely on superseded material.

| Topic | Earlier position | Current position |
|---|---|---|
| Routing | S1: helpline refers directly to the district supervisor | S2/S3 D-008: agent selects a CPIMS+ service; the Ministry distributes |
| Feedback | S1: one-way follow-up push; return of status not committed | S3 D-007: two-way updates for referred cases |
| Anonymity | S2: anonymous reports cannot be referred | S3 D-010/D-011: anonymous reporter allowed; child identifying details required |
| ABR ID | S1: optional; validation deferred | S3 D-005/D-014: optional; NICR structural format for initial validation |
| Attachments | Session 3 deck: deferred unless approved | S3 D-012: included in the field set |
| Narrative | Required, timing not stated | S3 D-013: mandatory at referral, not at first save |
| UNICEF participation | S1/S2: absent; escalation raised | S3: Rantsala chaired and Daniel attended; approval route still to confirm |

## 6 Current baseline

| Area | Position recorded | Remaining confirmation |
|---|---|---|
| Direction | Two-way updates for referred cases | Feedback events, permitted fields, mechanism and conflict rules |
| Initiation | Manual action by the handling agent | Escalation, exceptional approvals and cancellation rules |
| Routing | Agent selects a CPIMS+ service; Ministry distributes | Actual service list and the configured receiving user or agency for each service |
| Identification | Anonymous reporter allowed; child identifying details required | Exact minimum dataset and emergency exceptions |
| ABR ID | Optional; NICR format agreed for initial validation | Examples, authoritative verification and later-update contract |
| API | Supplied specification accepted for the build | Deployment version, authentication and configured operation sequence |
| Duplicate prevention | Required | Adoption of the client-generated case identifier or another agreed key |
| Environment | Lesotho sandbox, with global playground fallback | Checklist closure and secure access package |
| UAT | Ministry leads; participant roles accepted | Named testers, accounts, dataset and signatories |
| Contract scope | Outbound client in contract; two-way confirmed in Session 3 | Governance decision on scope, effort and milestones |

## 7 Scope

### 7.1 Agreed integration scope

The scope covers agent-triggered referral; validation of the agreed information; service selection and Ministry receipt/distribution; technical receipt and human acceptance or rejection; OpenCHS follow-up information; and return of CPIMS+ case status and intervention updates to the linked helpline case. It includes the agreed attachments field, optional ABR capture and initial format checks, traceable case linkage, duplicate prevention, audit evidence and operational failure visibility. Referral status must be displayed clearly to operators, as the brief requires for D2.

Two-way integration is limited to information about referred cases approved for sharing. It does not authorise unrestricted copying of CPIMS+ case files, case plans or unrelated records. Transport, status vocabulary, access controls and update ownership remain to be designed.

The existing support-and-maintenance obligations continue alongside the integration, including bug fixing, dependency maintenance, quality assurance after changes and training of IT personnel. Regression testing must show that existing OpenCHS functionality is not adversely affected.

### 7.2 Boundaries retained

The helpline case plan is not transmitted. Call recordings and large media not expressly agreed, major workflow redesign, advanced lookup administration, a generic integration marketplace, non-essential analytics and an automated production deployment pipeline remain outside the current baseline unless separately approved. Agreement to attachments does not itself authorise transfer of call recordings or unrestricted files.

There is no X-Road hop between OpenCHS and CPIMS+. API-to-API or OpenFN remains a Ministry/technical architecture choice. Home Affairs ID verification is coordinated through the separate X-Road sessions; participation in those sessions is agreed, but a new live Home Affairs interface is not silently added to BITZ’s implementation scope. Session 1 recorded that the CPIMS+ to X-Road bridge is a separate piece of work with its own funding question.

## 8 Referral lifecycle

1. The agent receives the call, records the contact and saves the helpline case. The referral narrative need not be complete at this initial save.
2. The handling agent elects to refer the case and selects an approved CPIMS+ service. The agent may first escalate to a supervisor where they judge it necessary.
3. OpenCHS validates the referral narrative and required child-identifying information. It allows an anonymous reporter and an absent ABR ID.
4. The integration submits the agreed data and records a system acknowledgement or a failure requiring recovery.
5. The receiving party accepts or rejects the referral through the agreed CPIMS+ workflow. System receipt does not prove human acceptance or immediate case-management commencement.
6. Ministry users distribute/assign the case internally. Selecting a service does not imply that the helpline selects an individual caseworker.
7. OpenCHS sends follow-up information against the linked case. CPIMS+ returns approved status and intervention updates to the helpline.
8. Closure and any correction, cancellation or re-referral retain linkage and an auditable history, with detailed rules still to be agreed.

The Session 2 demonstration showed the native CPIMS+ mechanism that this lifecycle must fit. A user opens the Services panel, chooses an Internal or External referral and a service such as case management or medical service, and records the reason and expected outcome. The recipient sees the referral as pending and must accept it, which opens the case file, or reject it with a reason. Assignment of a caseworker by a district manager is a separate, later step. The helpline needs visibility of acceptance and later service completion or closure, not of internal assignment.

Existing emergency phone contact with police or first responders continues alongside system referral, because CPIMS+ users may not see a system notification immediately. The integration records and tracks that response; it does not replace urgent calls. Lesotho operates a single call centre; any satellite site is a VPN-connected extension of it.

## 9 Business rules and exceptions

Session 3 accepts the manual referral process as presented. National referral pathways already exist: Rantsala will share them, and Hopolang will resend the SOPs. BITZ will use those documents rather than create a new national pathway. Session 1 recorded that the SOPs are being revised to cover all CPIMS+ stakeholders, and that a near-final unified national referral form covers all child-protection categories. Session 2 records the form as shared under A-004, but no copy is filed in the workspace. The form should be filed and used as the reference for field design.

The Session 2 decisions not superseded by Session 3 remain in force: referrals are supported to CPIMS+/MGYSD and other approved stakeholders (D-001); the SOP covers the wider referral ecosystem (D-002); emergency referrals need not capture every detail first (D-003); and perpetrator information is important to risk assessment (D-004). Session 1 included perpetrator details after Child Helpline participants explained that whether a perpetrator lives with the child affects urgency and intervention.

Anonymous reporting and unidentified children are different situations. A reporter may remain anonymous and be recorded as such in CPIMS+. The child must have identifying details and location sufficient for follow-up. The exact minimum identifying fields, incomplete-child-information scenarios and emergency exceptions must be settled against the SOPs and configured forms. Do not infer that every bio-data field is always mandatory, and do not create fictitious names, dates of birth or identifiers to satisfy validation.

Supervisor escalation, refusal reasons, corrections, withdrawal, hoax/prank updates and re-referral need explicit permissions and history rules. Session 1 agreed that a case later found to be a prank is reported to CPIMS+ as a follow-up update, not left unsynchronised. An OpenCHS change must not automatically close or overwrite a CPIMS+ case without an agreed update contract.

The scope brief’s inception questions on referral control remain partly open: whether a referral can be cancelled or corrected, whether the same case can be referred more than once, and whether any role other than the handling agent may initiate referral. These belong to WF-003 and WF-006 in the inventory.

Outage handling is open under A-021. Durable queueing, retry intervals, operator escalation, safe resubmission and reconciliation are proposed controls pending agreement or testing. No automatic retry count or outage service level is approved by these minutes.

## 10 Technical architecture

The proposed flow is OpenCHS and its integration/API Gateway component to CPIMS+, with an authorised return channel for linked case updates. The Ministry and technical teams must choose API-to-API or OpenFN. The architecture must distinguish system receipt, business acceptance/rejection, assignment and case progress.

| Layer | Proposed component | Evidence status |
|---|---|---|
| Intake | OpenCHS case form with ABR field and referral control | D2 build; form engine to verify |
| Outbound | Integration service via the API Gateway, with durable queue, retry and idempotency controls | D3 build; framework and queue to verify |
| Authentication | Primero JWT bearer tokens; integration account to be agreed | Upstream documented; Lesotho flow pending |
| Receiving system | Primero CPIMS+ API v2: case create, update, referral and attachments | Upstream documented; configuration pending |
| Return channel | Primero webhook to an OpenCHS endpoint, or OpenCHS polling of case and referral status | Candidate options; to be agreed |
| Controls | Audit log, monitoring and operator alerts | Design pending |

A configurable integration provider remains a technical recommendation: mapping, credential handling, job tracking, connection checks and reliability controls should reuse existing capabilities where suitable. Both outbound referrals and agreed inbound feedback are required by the Session 3 scope; feedback is no longer merely a future extension. The OpenCHS development environment is internal; the test/UAT environment combines the helpline application and the API Gateway, which onboards and authenticates Primero as a connected system.

Before design sign-off, Peter and Marlon must verify the actual case model, integration framework, queue, role permissions, audit facilities, deployment and secret-management arrangements. Isaiah must confirm receiving-system capabilities, service configuration and permissions. Earlier technical reference material describes referral being created automatically when a case is saved; this conflicts with the agreed manual trigger and must not be implemented as written. A reference architecture is not evidence that these components are installed or working.

## 11 ABR identifier requirements

Session 3 D-005 and D-014 record the following initial baseline, reported by Hopolang after contact with Home Affairs. The annotated requirement checklist records the same format.

| Attribute | Agreed rule |
|---|---|
| Meaning | Birth registration number issued at birth; persists through national ID, passport and school records (Session 1) |
| Issuing authority | NICR, Ministry of Home Affairs |
| Length | 12 digits |
| Prefix | First digit is 0 or 1 |
| Gender position | Seventh digit: 1 for male, 2 for female |
| Requiredness | Optional; referral proceeds when unavailable |
| Missing identifier | Receiving caseworker obtains it during follow-up |
| Initial validation | Use the recorded structural rules |

Store the identifier as text to preserve leading zeroes. Structural checks do not establish that the identifier exists or belongs to the child. Where the recorded sex conflicts with the seventh digit, the handling rule (warning, block or accept) must be agreed rather than assumed. A-007 remains open for the remaining verification contract: authoritative examples, any checksum or uniqueness rules, invalid-value handling, corrections, update permissions and the live verification route. The minutes do not provide a checksum algorithm or a working Home Affairs endpoint. The delivery plan’s reference to checksum validation for D2 therefore applies only if the authority supplies one.

UNICEF and Isaiah will invite BITZ to the Primero/X-Road sessions (A-019). Melusi will obtain Berea workshop use cases (A-020). The resulting Home Affairs requirements and responsibilities must be agreed before any additional implementation commitment.

## 12 Referral fields and mapping

Session 3 D-012 confirms the following field set. It is a business payload baseline, not a deployed API schema. Mandatory rules explicitly established by the meeting are identified below; other conditional requiredness and unknown-value handling need mapping confirmation.

| Information | Business requirement | Technical mapping still needed |
|---|---|---|
| Child name and location | Identifying details required to trace the child | Name parts, minimum identity, location hierarchy and exceptions |
| Age, sex, nationality and child contact | Included in the agreed bio-data set | Types, codes, estimated age and unavailable-contact handling |
| Case category | Included; maps to CPIMS+ protection concerns, which are multi-select | Approved concern list, multi-value codes and transformations |
| Case narrative | Mandatory at referral, not first save | Target field, length and permitted sensitive content |
| Reporter contact | Included when available, so the Ministry can reach someone when the child has no phone; anonymous reporter allowed | Anonymous flag/value, optional contact and privacy rules |
| Perpetrator details | Included in the agreed set | Fields, unknown details, access and conditional validation |
| Attachments | Included | File types, size, scanning, permissions and retention |
| Follow-up updates | Included; linked to the original case | Events, ownership, timestamps and update permissions |
| ABR ID | Optional; structural validation as above | Target field, blank representation and subsequent correction |
| Selected service | Agent selects from the CPIMS+ service list | Service codes and the receiving user or agency for each |
| Consent and disclosure | Not discussed in the sessions | Whether CPIMS+ consent fields must be set for referral (section 15) |
| CPIMS+ feedback | Status and interventions returned to helpline | Approved values, minimisation, delivery and reconciliation |
| Helpline case plan | Not transmitted | Exclude from the shared payload |
| External case reference | Proposed technical linkage requirement | Client-generated case identifier or other stable key; returned case ID |

Primero will produce one standardised protection-concern list aligned across both systems from what is already agreed for Lesotho (Session 2). The OpenCHS Services Offered value sent on referral is a label such as “CPIMS+” or “Child Protection Service”.

Prior developer examples such as `abr_id`, `openchs_reference_id`, `name_first`, `name_last`, `protection_concerns`, `location_current` and `referral_notes` remain candidate field names, not confirmed Lesotho schema. Date-of-birth, risk-level, module and referral-source examples require explicit mapping approval before transmission; their presence in earlier technical material does not expand the agreed field set.

Each mapping must identify source and target, direction, datatype, requiredness, validation, transformations, lookup values, sensitivity and approving owner. Isaiah supplies configured definitions and lookup lists; Ministry and OpenCHS stakeholders approve the business mapping. The Primero API accepts only the fields the integration account is permitted to set, so the account’s role must cover the approved mapping and no more. Service vocabulary is due under A-018; a complete field dictionary has no separate confirmed delivery date in the minutes.

## 13 API and authentication

### 13.1 Specification and version

The upstream API documentation supplied by Isaiah describes API v2. Session 3 D-017 accepts this specification as the build basis unless it changes, closing specification receipt for inception. The applicable Lesotho release, base URL, configured schema and operation sequence remain to be captured. The public `development_v2` branch is a moving reference. This version reviewed the v2.16.0 source and documentation held locally; the deployed Lesotho release must still be confirmed with Primero and recorded before implementation.

### 13.2 Operations relevant to the integration

| Purpose | Operation | Documented behaviour (v2.16.0) |
|---|---|---|
| Obtain or renew token | `POST /api/v2/tokens` | Username/password, or an existing valid token; token returned in the Authorization header |
| Invalidate token | `DELETE /api/v2/tokens` | Expires the token presented |
| Create case | `POST /api/v2/cases` | `data` object; optional client-generated UUID in `data.id` |
| Update case | `PATCH /api/v2/cases/:id` | Merges submitted fields; subform arrays are merged and appended |
| Refer case | `POST /api/v2/cases/:id/referrals` | Addressed to a receiving user (`transitioned_to`); also accepts service, agency, notes and consent-override fields |
| Read referral outcomes | `GET /api/v2/cases/:id/referrals`, `GET /api/v2/cases/:id/transitions` | Lists referrals and other transitions for a case |
| Attach file | `POST /api/v2/cases/:id/attachments` | Base64 file with field name, type and content type; requires permission on that field |
| Read history | `GET /api/v2/cases/:id/record_history` | Change history for a case |

Case creation and referral are separate operations. The documentation describes referral as granting another user access to the record; transfer changes ownership through acceptance or rejection. Because an API referral is addressed to a user, the agreed service-based routing needs a configured mapping from each service to a receiving user or agency. Primero and Ministry stakeholders must confirm the operation sequence that supports Lesotho’s routing; an endpoint’s existence does not establish that fit.

### 13.3 Case creation and duplicate protection

The case-create operation accepts an optional client-generated UUID as the record identifier. When it is supplied, the API returns `204 No Content` on success and `409 Conflict` if a case with that identifier already exists. Other documented errors are `403 Forbidden` and `422 Unprocessable Entity`, the latter naming the invalid field. Errors share a structure with code, resource and message.

This gives a candidate idempotency mechanism: OpenCHS generates and stores the UUID before the first attempt and reuses it on every retry, so a repeated request after a lost response produces a conflict rather than a second case. The trade-off is that a `204` response returns no case content, so the case display identifier must be read separately. Adoption requires confirmation that the Lesotho deployment behaves as documented and agreement on how a `409` is reconciled (OPS-003).

### 13.4 Authentication

The token documentation describes a bearer JWT in the response Authorization header, 60-minute expiry, issuance using username/password, and reissue using a valid existing token. Reissue does not invalidate other unexpired tokens. Isaiah prefers SSO where an identity provider is available; username/password is an alternative. The unattended OpenCHS backend flow, recovery after expiry, permissions and secret rotation remain Pending. User SSO choice alone does not settle integration authentication.

Isaiah confirms that the Primero team will set up credentials once implementation is ready. He confirms that network/security controls apply without identifying which controls. Obtain the actual TLS/certificate, VPN, IP allowlisting and other prerequisites; do not infer that every listed control applies. The delivery plan’s proposed minimum is HTTPS with TLS 1.2 or higher and certificate verification outside local environments.

Isaiah reports no API rate limits and proposes joint performance management. Concurrency, payload limits, timeouts, retry/manual-correction rules and performance acceptance remain to be agreed. Generic examples do not establish configured Lesotho payloads.

### 13.5 Return updates

Primero supports outbound webhooks that send a case’s data to an external URL when it is created or updated, authenticated by API key or basic authentication. The fields sent are limited to those permitted to a configured role, and each delivery is logged in Primero’s audit log. Webhooks are enabled per module by configuration. The v2.16.0 connector does not retry failed deliveries.

Webhooks are therefore a candidate return channel for D-007, with the role mechanism supporting minimisation. Because failed deliveries are not retried, OpenCHS would also need periodic reconciliation against the referral and transition endpoints. Polling alone is the alternative. Primero and the Ministry must confirm whether webhooks can be enabled for Lesotho, which role and fields apply, and whether referral status changes trigger a webhook.

### 13.6 API contract still required

The API contract must provide, for the Lesotho deployment:

- Sandbox/UAT and production base URLs and the deployed release.
- Integration account, authentication flow and permissions.
- Token expiry and renewal handling for the unattended backend.
- Agreed operation sequence for create, referral, follow-up and attachments.
- Configured request and response examples for the Lesotho forms.
- Confirmation of client-generated identifier support and conflict handling.
- Error classes, timeouts and retry/manual-correction rules.
- Service-to-recipient configuration and lookup/form endpoints, if required.
- Return-update mechanism, payload and delivery guarantees.
- TLS, certificate, VPN, IP allowlisting or firewall requirements.

### 13.7 Configuration and field dictionary dependencies

The Ministry and Child Helpline must supply current SOPs, paper referral forms, approved child-journey use cases and existing referral pathways, with receipt of existing pathways tracked under A-013/A-014. Primero will use these to configure the demo; Isaiah expects API field definitions and lookup/code lists to be available after setup. The teams must jointly capture the resulting integration specification because Isaiah reports no existing interface specification.

Session 3 now establishes ABR issuing authority, structural format and optional status as set out in section 11. The target field, remaining verification contract, duplicate-prevention mechanism and two-way status transport still need technical confirmation.

## 14 Reliability and audit

The proposed delivery design uses durable referral records, a stable correlation reference and auditable transmission attempts. It must distinguish unsent, awaiting system receipt, received, accepted, rejected and later case-progress information without equating technical delivery with case closure.

The upstream referral model provides a starting vocabulary: in progress, accepted, rejected (with reason), done and revoked, with a successful or not-successful outcome and whether the service was implemented. The Child Helpline identified the gap between “referred” and “closed” in Session 2; the final helpline-facing vocabulary should be agreed from these values rather than invented separately. The final state vocabulary is pending (RT-006).

Retries must not create duplicate cases. The technical teams must agree an idempotency key, with the client-generated case identifier as the leading candidate (section 13.3), plus reconciliation after uncertain timeouts, error classification, backoff, operator intervention and dead-letter handling. The delivery plan proposes retries at 1 minute, 5 minutes, 30 minutes and 2 hours before marking a referral failed and alerting an administrator; this remains a proposal. Apply equivalent controls to repeated or out-of-order feedback events. Conflicting updates need explicit ownership and reconciliation rather than blind overwrites. Agent double-submission must also be prevented in the referral control.

Audit records should include case/reference identifiers, ABR ID where available, timestamps, actor/system, action, endpoint, transaction outcome and retry history. Session 2 agreed in principle to model the log on CPIMS+’s own structure: time, performed by, action, description and owner. Record response metadata safely; full child payloads, tokens and unrestricted API bodies should not be logged by default. Retention, redaction and audit access remain approval items. A-021 covers the unresolved outage scenario and must produce an agreed requirement or an explicitly accepted testing-stage dependency.

## 15 Data protection and security

UNICEF will supply earlier Ministry data-protection work, data management policy and applicable legal material under A-017. Nelson will complete desk research under A-022. The sources describe the legal position differently: in discussion Rantsala said such laws are under development; the action register refers to the Data Protection Act 2011; and the annotated requirement checklist refers to the Lesotho Data Protection Act 2012. This report does not determine which legislation applies or is in force. The desk research must confirm the correct instrument, year and commencement status with the responsible Ministry/UNICEF advisers.

The design must establish authorised sharing purposes, minimum necessary fields, consent or other applicable basis, permissions, protected transfer/storage, credential custody, retention, audit access and incident escalation. Reporter anonymity must survive the transfer. Return updates and attachments need equivalent disclosure controls. Confirm required certificates, VPN or allowlisting with Primero rather than assuming every possible control applies.

Consent is a specific dependency. In the upstream child-protection module, a user referral checks that the case records consent for disclosure to other organisations and consent for services, unless consent is overridden. No consent capture for this purpose was discussed or agreed in the sessions, and the corresponding OpenCHS fields have not been verified. The Ministry must decide how consent, or another lawful basis, is captured at the helpline and represented in CPIMS+, and who may override it.

Use an approved synthetic child-journey dataset as the proposed testing default. A demo environment and the email’s general reference to test data do not establish permission to copy real child records.

## 16 Responsibilities and governance

| Party | Recorded responsibility | Still to be confirmed |
|---|---|---|
| Nelson and BITZ | Project management, report, requirements follow-up and desk research | Final report approval route and dependency rebaseline |
| James, BITZ / IQ Consulting | Executive Director; attended Session 3 | No individual action assigned |
| Peter and Marlon | Helpline-side development; API Gateway and integration; authentication/test preparation | Detailed design and execution evidence |
| Isaiah | Primero technical coordination, sandbox, access and service list | Configured contract and authentication |
| Hopolang | Host, Ministry IT coordination, SOPs and helpline leave cover | Permanent focal person and cover appointment |
| Tiisetso Mohlabi | Child Protection Officer and CPIMS focal person; Ministry-level coordination with Isaiah | Role in approval; Session 3 attendance not established |
| Rantsala | Session 3 chair, pathways and checklist follow-up | Named programme approval authority |
| Daniel, UNICEF | Technology for Development Specialist; X-Road coordination and privacy materials offered | Relationship to the action owner Lekhanya |
| Melusi | Ministry IT and Berea use-case follow-up | Workshop documents and resulting requirements |
| Ministry and Child Helpline | Workflow ownership, Ministry-led UAT and sign-off | Named testers, business/security signatories and support ownership |

UNICEF attended Session 3 through Rantsala and Daniel, which addresses the participation gap raised in Sessions 1 and 2 (A-012). The action register assigns A-017 and part of A-019 to Lekhanya, while the discussion names Daniel as offering the materials. Confirm the named UNICEF action owner without assuming these names identify the same person.

Child Helpline social workers, supervisors and a research analyst took part in Session 1. No Child Helpline agent or social worker attended Session 3; a Child Protection Services representative spoke for the helpline. Mary Damposi was discussed as the testing contact, but her attendance and appointment were not confirmed. Rantsala asked the Ministry to ensure at least one coordination representative attends every meeting.

## 17 Environments and readiness

| Environment | Owner | Status as recorded |
|---|---|---|
| OpenCHS development | BITZ | Internal; not shared |
| OpenCHS test/UAT with API Gateway | BITZ | Being stood up; access evidence pending |
| Lesotho CPIMS+ sandbox/demo | Isaiah, Primero | Checklist incomplete; configuration depends on country inputs |
| Primero global playground | Isaiah, Primero | Agreed fallback (D-018); URL and access pending |
| Production (both systems) | Infrastructure owners | Not confirmed |

The Lesotho sandbox checklist was incomplete on 26 October. Isaiah reported no progress since Session 2, when he expected configuration within about a week of the checklist being closed. A-015 assigns Rantsala and Isaiah a same-day follow-up. A-016 assigns Isaiah access provision by 28 October. If the Lesotho environment is not ready by draft completion, Session 3 agrees the global playground fallback; neither a URL nor working credentials is supplied in the minutes.

The access package must record environment/version, base URL, named/service accounts, permissions, authentication, network prerequisites and safe test data. Confirm which country configuration and fields the playground supports and which tests will need repeating on the configured Lesotho environment. The earlier primerodev.org option in Isaiah’s email is historical context and does not establish the global playground’s URL.

OpenCHS UAT access, production endpoints, secret rotation and production readiness also need evidence. Environment availability and test success remain separate gates.

## 18 UAT and acceptance

Session 3 closes the UAT leadership and participant-role question for inception: the Ministry leads, with OpenCHS developers, Child Helpline agents, Ministry system administrator, CPIMS+ users, district supervisors and other Ministry users who receive, distribute, investigate or close referrals. The annotated requirement checklist adds three positions for confirmation: the Child Helpline supervisor participates, BITZ provides test data and scenarios, and MGYSD signs off. Named testers, accounts and authorised signatories remain pending.

The test plan must include manual referral; saving before narrative completion and blocking referral without narrative; identified child with anonymous reporter; ABR present, absent, structurally invalid and inconsistent with recorded sex; minimum-information emergency handling; service routing; separate system receipt and human accept/reject; perpetrator information; attachment permissions; subsequent ABR correction; OpenCHS follow-ups including prank re-flags; CPIMS+ status/intervention feedback; duplicate and out-of-order delivery, including retry with the same case identifier; token expiry and renewal; outages, queued referrals and reconciliation; privacy, consent, access and audit controls; and regression of existing OpenCHS functionality.

These are planned acceptance scenarios, not completed tests. Each needs an expected result, tester, environment, evidence and defect outcome. Approve severity and exception rules before execution. Mock or contract tests may evidence client behaviour while access is pending but must not be described as live integration. UAT execution, training, support handover and go-live acceptance are subsequent delivery gates, not prerequisites for merely circulating the inception draft.

Training under D4 should cover, for operators and social workers, the ABR field, referral workflow, validation messages, referral status, failure handling and escalation; and for IT staff, architecture, API configuration, authentication, monitoring, logging, queue management, retries, troubleshooting and support escalation.

## 19 Delivery plan and dependencies

The Workstream 1 target is an initial draft on 28 October 2026 close of business. The source does not specify an exact hour or timezone. Follow-up on outstanding documents, service list, coordination cover and outage requirements was planned for 26–27 October.

The commercial planning reference remains 1 July 2026 to 28 February 2027, with milestone targets in August (D1), October (D2), November (D3) and February (D4). As at 27 October, the D1 target month has passed without approval and the D2 target month ends in four days. D2 design inputs are now largely available (ABR format, manual trigger, narrative rule), but D3 depends on access, authentication and configured mapping that are not yet supplied. Earlier 14-week and ten-day/two-week technical schedules are historical references, not a newly approved implementation promise. Session 1 also noted that the OpenCHS timeline is coupled to Primero’s own CPIMS+ go-live. The outstanding August milestone and the effort implications of confirmed two-way updates and attachments require schedule reconciliation by project governance.

The dependency sequence is existing SOPs/pathways and approved use cases → configured environment and access → confirmed mapping/authentication and feedback design → integration and recovery testing → Ministry-led UAT → authorised handover/go-live. Some design work can proceed in parallel, including ABR field build, referral control, queue and idempotency design and synthetic test design. Global playground access can enable preliminary tests but does not eliminate country-configuration validation.

## 20 Risk register

| Risk | Effect | Action and owner |
|---|---|---|
| R-001 Sandbox/access delay | Blocks configured mapping and integration tests | Rantsala/Isaiah close checklist; Isaiah provides access or playground under A-015/A-016 |
| R-002 Country documents not received | Requirements cannot be checked against approved practice | Rantsala pathways, Hopolang SOPs, UNICEF privacy materials; file the unified referral form; retain receipt evidence |
| R-003 Field and service configuration incomplete | Invalid payloads or misrouting | Isaiah service list A-018 and service-to-recipient configuration; technical and Ministry teams approve mappings |
| R-004 Outage and duplicate recovery unresolved | Lost, repeated or uncertain referrals | Nelson/Peter/Isaiah resolve A-021; confirm client-generated identifier support and test recovery |
| R-005 ABR verification dependency | Format-valid IDs may remain unverified | Carry A-007; coordinate A-019/A-020; keep missing ABR non-blocking |
| R-006 Two-way design | Disclosure risk or lost updates | Technical teams define bounded feedback; confirm webhook role and reconciliation |
| R-007 Privacy and authority gaps | Unauthorised sharing or unclear approvals | UNICEF materials A-017, Nelson research A-022; Ministry confirms approval owners |
| R-008 Focal-person or support gaps | Delayed review, UAT and incident resolution | Hopolang appoints cover A-024 and permanent focal A-002; name support owners |
| R-009 Milestone slippage | D1 overdue against August target; D2/D3 windows at risk | Governance confirms D1 status and approves any rebaseline in writing |
| R-010 Contract scope change | Two-way updates exceed the outbound D3 description | Governance decides scope, effort and acceptance evidence for return updates |
| R-011 Consent requirement in CPIMS+ | Referrals blocked or made without an agreed basis | Ministry defines consent capture and override; Isaiah confirms configured checks |
| R-012 Primero go-live dependency | OpenCHS delivery pushed outside its window | Isaiah reports Primero country go-live plan; governance tracks the coupling |

All risks remain open until evidence supports closure. An action due date is not evidence that the risk is resolved.

## 21 Decisions and actions

Decision identifiers continue the Session 1–2 register; where Session 3 updated an earlier decision, it kept the earlier ID. Earlier v0.4 report-local decision numbering is preserved in the archive and must not be treated as equivalent solely because the numbers match.

| ID | Decision | Source and status |
|---|---|---|
| D-001 | Support referrals to CPIMS+/MGYSD and other approved stakeholders | Session 2; agreed in principle |
| D-002 | SOP covers the broader referral ecosystem and role-holders | Session 2; agreed in principle |
| D-003 | Emergency referrals do not require every detail first | Session 2; agreed direction; minimum dataset pending |
| D-004 | Perpetrator information is important; assess requiredness | Session 2; included in field set by D-012 |
| D-005 | ABR optional; receiving caseworker obtains it later if missing | Session 3; agreed |
| D-006 | Manual handling-agent referral and process as presented | Session 3; agreed |
| D-007 | Two-way integration for referred-case updates | Session 3; agreed |
| D-008 | Ministry distribution through helpline selection of CPIMS+ services | Session 3; agreed, service list to confirm |
| D-009 | Ministry-led UAT with the recorded participant roles | Session 3; agreed |
| D-010 | Anonymous reporter allowed | Session 3; agreed |
| D-011 | Child identifying details mandatory for referral | Session 3; agreed |
| D-012 | Field set confirmed; helpline case plan excluded | Session 3; agreed |
| D-013 | Narrative mandatory at referral, not initial save | Session 3; agreed |
| D-014 | NICR identifier format used for initial validation | Session 3; agreed |
| D-015 | Direct API or OpenFN connection; X-Road only for Home Affairs checks | Session 3; agreed |
| D-016 | Separate system receipt and human accept/reject acknowledgements | Session 3; agreed |
| D-017 | Supplied API specification accepted unless it changes | Session 3; agreed |
| D-018 | Global playground fallback if Lesotho sandbox is not ready | Session 3; agreed |

These decisions are agreed in the supplied minutes. Approval of the complete report remains pending.

| ID | Action | Owner | Recorded due | Status at 27 Oct |
|---|---|---|---|---|
| A-013 | Share national referral pathways | Rantsala | 26 Oct 2026 | No receipt filed |
| A-014 | Resend case management SOPs | Hopolang | 27 Oct 2026 | No receipt filed |
| A-015 | Complete sandbox checklist and post-meeting follow-up | Rantsala, Isaiah | 26 Oct 2026 | Outcome not recorded |
| A-016 | Provide sandbox or playground access | Isaiah | 28 Oct 2026 | Pending |
| A-017 | Share Ministry privacy work, policy and legal material | Lekhanya, UNICEF; identity to clarify | 26 Oct 2026 | No receipt filed |
| A-018 | Confirm CPIMS+ service list | Isaiah | 28 Oct 2026 | Pending |
| A-019 | Invite BITZ to Primero/X-Road sessions | Lekhanya, Isaiah | Next session; date unconfirmed | Pending |
| A-020 | Share Berea workshop use cases | Melusi | 27 Oct 2026 | No receipt filed |
| A-021 | Agree outage/referral delivery handling | Nelson, Peter, Isaiah | 28 Oct or during testing | Proposals in sections 13–14 |
| A-022 | Research data protection requirements | Nelson | 28 Oct 2026 | In progress; legal instrument to confirm |
| A-023 | Set up API authentication and start test calls | Peter, Marlon | After A-016 | Awaiting access |
| A-024 | Name helpline coordination leave cover | Hopolang | 27 Oct 2026 | No confirmation filed |
| A-025 | Deliver initial inception draft | Nelson, BITZ | 28 Oct, close of business | v0.6 prepared; circulation pending |

All source actions require completion evidence. A-002, permanent Child Helpline focal person, and A-007, remaining ABR verification rules, carry forward without a newly stated due date. Session 2 records A-001, A-003 and A-004 as completed; Session 3 lists only A-002 and A-007 as open from the earlier register. A-019 is dependency coordination and A-023 is subsequent technical execution; neither is represented as a completed Workstream 1 requirement.

## 22 Inception completion gates

The report can be circulated as a draft while disclosed gaps remain. Formal D1 acceptance requires authorised review of the recorded decisions and either closure of outstanding requirements or explicit acceptance of bounded dependencies, with owner, evidence and due milestone. The contract-aligned plan also requires technical design, a mapping baseline and environment-setup evidence for D1.

Outstanding closure work is: receipt and review of pathways/SOPs/referral form/privacy materials; service list, service-to-recipient configuration and configured mapping; minimum-data exceptions and consent handling; authentication/access prerequisites; two-way feedback mechanism and outage requirements; named approval authorities and helpline cover; the scope decision on return updates; and a reconciled delivery baseline. Items intentionally left to testing must be identified as such rather than silently marked resolved.

API specification acceptance, UAT participant roles, anonymity, optional ABR and integration direction should not be reopened as wholly unanswered questions. Their detailed implementation and test evidence remain separately tracked in the completion inventory. Training, production operations and go-live checks remain later delivery gates.

## 23 Review and approval

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
| 0.6 | 27 Oct 2026 | Added contract and workstream context, inception history and requirement evolution, Session 2 decisions D-001–D-004, annotated checklist positions, Primero v2.16.0 API findings (idempotency, referral statuses, webhooks, consent), environment table, new risks R-009–R-012 and action status; Word copy not yet updated |
