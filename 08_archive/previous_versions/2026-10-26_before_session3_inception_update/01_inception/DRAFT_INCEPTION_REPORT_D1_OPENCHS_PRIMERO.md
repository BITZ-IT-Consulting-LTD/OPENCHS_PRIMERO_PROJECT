# Draft Inception Report — D1
## Lesotho Child Helpline 116 / OpenCHS–Primero CPIMS+ Integration

**Document status:** Draft — updated after Sessions 1 and 2 and Isaiah’s technical response; for inception review and decision\
**Version:** 0.4\
**Date:** 26 October 2026\
**Prepared for:** UNICEF Lesotho / MGYSD / Child Helpline 116 stakeholders\
**Prepared by:** Project Management and Technical Delivery Team\
**Target delivery model:** Contract-aligned delivery from 1 July 2026 to 28 February 2027, with milestone targets in August 2026, October 2026, November 2026, and February 2027; the 14-week plan remains a technical reference unless formally rebaselined\
**Commercial planning reference:** [Contract-Aligned Delivery Plan](../02_project_management/CONTRACT_ALIGNED_DELIVERY_PLAN.md)\

> This document is a working inception baseline. It does not confirm any item that has not been approved by the responsible business, technical, security, or receiving-system owner. Unconfirmed items are marked **TBD**, **Proposed**, or **To be confirmed**.

---

## 1. Executive Summary

The project will configure and integrate the Lesotho Child Helpline 116 / OpenCHS environment with Primero CPIMS+ to support a controlled outbound child-protection referral workflow.

The immediate delivery objective is a safe minimum viable integration within the agreed implementation baseline. The MVP will support an approved agent-triggered referral workflow, minimum-information emergency referrals subject to CPIMS+ identification rules, missing or unavailable ABR IDs where permitted, durable queueing, transmission of an approved case payload to Primero using JWT authentication, duplicate prevention, agreed follow-up/status handling, and an appropriate audit trail.

Isaiah has supplied the upstream API documentation, confirmed himself as the Primero technical contact, and described a preferred configured demo with a possible primerodev.org alternative. Country SOPs, paper forms, use cases and referral pathways are inputs to configuration. Environment access, approved mappings and deployment-specific authentication remain pending.

The project cannot be considered implementation-ready until the receiving-system API contract, ABR rules, field mapping, privacy requirements, environments, credentials, and acceptance authority are confirmed. This report therefore separates the current documented baseline from decisions still required.

## 2. Purpose and Objectives

### 2.1 Purpose

This inception report establishes the shared requirements, architecture, responsibilities, dependencies, risks, implementation approach, and acceptance baseline for D1 — Inception, Requirements and Environment Setup.

### 2.2 Objectives

The inception phase will:

- Confirm the systems, owners, and integration direction.
- Define the minimum safe referral workflow.
- Confirm ABR ownership and validation requirements.
- Establish the OpenCHS-to-Primero field-mapping baseline.
- Confirm API, authentication, environment, and connectivity requirements.
- Define queueing, retry, offline, idempotency, and audit expectations.
- Confirm security, consent, data-minimisation, and access-control requirements.
- Define UAT, go-live, training, support, and handover requirements.
- Produce a controlled implementation plan and accelerated MVP work package.

## 3. Source Baseline

This draft is based on the following project documents:

1. `Lesotho_OpenCHS_Technical_Scope_Inception_Brief.pdf`
2. `Lesotho_OpenCHS_Implementation_Timeline_Presentation.pptx`
3. `docs/CONTEXT.md`
4. `docs/docs/platform/reference/OPENCHS_PRIMERO_INTEGRATION_CONTEXT.md`
5. `docs/context/12_PRIMERO_CPIMS_CONTEXT.md`
6. `docs/prompts/16-backend-integrations.md`
7. `Inception Meeting/SESSION_1_MEETING_REPORT_DRAFT.md`
8. `Inception Meeting/temeplate forms/README.md` and the Workstream 1 template pack
9. `Inception Meeting/temeplate forms/Workstream_1_Inception_Capture_Workbook.xlsx`
10. `Inception Meeting/Minutes/OpenCHS & Primero CPIMS+ Integration — Session 1 - Copy.pdf`
11. `Inception Meeting/Minutes/OpenCHS & Primero CPIMS+ Integration — Session 2.pdf`

12. [Isaiah response source record](../06_correspondence/ISAIAH_RESPONSE_SOURCE_2026-10-26.md) — recorded 26 October 2026; response sent date not supplied.
13. [Upstream Primero API documentation](https://github.com/primeroIMS/primero/blob/development_v2/app/controllers/api/README.md) and [token operation documentation](https://github.com/primeroIMS/primero/blob/development_v2/app/controllers/api/v2/docs/tokens/post.md) — reviewed 26 October 2026; development branch, not evidence of the Lesotho deployed release.

The current workspace contains documentation and planning material only. The existence, completeness, and runtime status of the described OpenCHS source components must be verified against the actual OpenCHS repository and deployment environment.

### 3.1 Cross-document reconciliation note

The template pack and minutes are working materials, not themselves an approved requirements baseline. Session 2 supersedes earlier meeting assumptions where it records a clear revision. Isaiah’s subsequent response supplies technical evidence and configuration dependencies; it does not approve unresolved business rules or change deferred scope. Pending items remain subject to owner confirmation. The following reconciliation points apply:

- The referral trigger is manual and initiated by the handling agent; once the case is sent to CPIMS+, case management starts immediately. Escalation and approval rules for exceptions remain subject to confirmation.
- Isaiah Amutavi Osotsi is now the confirmed Primero technical contact. Earlier notes use Isiah/Ososti spellings. Ministry workflow/form ownership, including references to Tiisetso and Silepo, still requires confirmation.
- The templates record one-way OpenCHS follow-up updates in principle, but no committed CPIMS+ to OpenCHS status write-back.
- Session 2 revises direct district/stakeholder routing: the working assumption is that OpenCHS selects a CPIMS+ service/referral target and Ministry-side supervisors or managers distribute cases internally. Primero technical confirmation remains pending.
- X-Road/Home Affairs integration is recorded as a separate scope boundary, and the emergency phone path remains an operational parallel path rather than a replacement for urgent response.

## 4. Current Baseline and Evidence Status

| Area | Current documented position | Status |
|---|---|---|
| Helpline platform | OpenCHS v5 case-management and telephony platform | Documented; live environment TBD |
| Receiving platform | Upstream API documentation describes Primero API v2 | Documentation received; exact Lesotho release/configuration TBD |
| Integration direction | Outbound referral from OpenCHS directly to Primero/CPIMS+ and other approved stakeholders | Agreed in principle; final routing and receiving-system contract TBD |
| Referral trigger | The handling agent manually initiates the referral; case management starts immediately in CPIMS+ once the case is sent | Agreed; escalation and approval rules for exceptions TBD |
| ABR ID | Referral-related identifier where available | May be blank when unavailable; official rule and validation TBD |
| Authentication | Documented bearer JWTs with 60-minute expiry; SSO preferred if an identity provider exists, username/password otherwise | Selected user/backend authentication and deployment contract Pending |
| Queueing | Offline/durable referral queue | Required by scope; live implementation unverified |
| Idempotency | Required to prevent duplicate cases | Design and key format TBD |
| Audit logging | Required for attempts, responses, and retries | Logging fields and redaction rules TBD |
| UAT | Ministry-led, child-journey scenarios; active agency representatives to participate; Isaiah is the Primero technical contact | Named testers, safe dataset, accounts and signatories Pending |
| Primero test environment | Preferred configured demo; possible primerodev.org alternative if delayed | Proposed options; URL, delivery date, suitability and access Pending |
| Configuration inputs | In-country SOPs, paper forms, use cases and referral pathways | Inputs required; configured fields and lookups expected after demo setup |
| Production support | Required after go-live | Owner and operating model TBD |

## 5. Scope

### 5.1 In scope for the accelerated MVP

- OpenCHS referral initiation workflow.
- Manual agent-triggered referral workflow, including escalation and approval rules.
- Minimum-information emergency referrals and follow-up capture.
- ABR ID capture and approved validation.
- Referral submission when the ABR ID is unavailable, subject to the approved Ministry process and CPIMS+ identification requirements.
- Referral permissions and authorised roles.
- Primero API authentication.
- Primero case-creation request.
- Confirmed OpenCHS-to-Primero data mapping.
- Durable referral queue.
- Retry and failure handling.
- Idempotency and duplicate prevention.
- Referral status visibility.
- Outbound referral/update status visibility; CPIMS+ status write-back remains Deferred unless approved through change control.
- CPIMS+ service/referral-target selection with Ministry-side supervisor/manager distribution, subject to technical confirmation.
- Parallel emergency phone contact with police/first responders where required by operational procedure.
- Redacted audit logging.
- Technical testing and UAT.
- Operator and technical training.
- Go-live readiness and handover.

### 5.2 Explicitly deferred unless contractually required

- Full bi-directional case-status synchronisation.
- Attachments, call recordings, and large media transfer.
- Advanced Primero lookup administration.
- Broad generic integration marketplace capabilities.
- Major OpenCHS workflow redesign.
- OpenCHS case-plan transfer or case-plan synchronisation with CPIMS+.
- Non-essential reporting and analytics.
- Automated production deployment pipelines.

Any deferred item that is later found to be mandatory must be added to the decision register and assessed for schedule impact.

## 6. Business Problem and Expected Outcome

Child Helpline 116 operators need a controlled way to refer eligible child-protection cases to the receiving case-management platform. The referral process must protect children and callers, avoid duplicate cases, preserve referrals during connectivity failures, provide clear operator feedback, and create sufficient evidence for accountability and support.

The expected outcome is:

```text
OpenCHS call/case
    ↓
Minimum referral information and approved referral condition
    ↓
Handling agent reviews and manually triggers referral
    ↓
ABR ID validation where available, with missing-ID follow-up record
    ↓
JWT-authenticated Primero API request
    ↓
Primero case identifier
    ↓
OpenCHS referral status, follow-up updates and support trail
```

## 7. Proposed End-to-End Workflow

### 7.1 Normal workflow

1. Operator records or updates the relevant OpenCHS case/call.
2. The handling agent reviews the case and manually triggers the referral using the approved service/referral target; whether escalation or approval is required remains to be confirmed.
3. OpenCHS validates the minimum information required for the referral scenario and permits an emergency/partial referral where approved.
4. OpenCHS captures or confirms the ABR ID where available; a missing ABR ID is recorded for follow-up rather than blocking an approved referral.
5. OpenCHS creates a durable referral record before external transmission.
6. The integration service creates an idempotency/transaction key.
7. The integration client authenticates to Primero using the approved JWT flow.
8. OpenCHS submits the approved case payload to the agreed CPIMS+ service/referral target.
9. OpenCHS stores the Primero response and case identifier where successful.
10. OpenCHS records and sends agreed follow-up updates where approved; any CPIMS+/MGYSD feedback or status return remains subject to the agreed contract.
11. OpenCHS displays referral and available follow-up/status information to authorised users.

### 7.2 Failure workflow

1. Validation failures are shown to the operator and are not transmitted.
2. Authentication failure triggers one controlled token refresh attempt.
3. Network timeouts and temporary server failures are retained and retried.
4. Primero validation errors are marked failed and require correction or review.
5. A referral that exceeds the retry limit is escalated to the support owner.
6. Any uncertain result after a timeout is reconciled using the transaction key before another create request is issued.

### 7.3 Session 1 direction incorporated

- Session 2 records the current direction as a manual referral initiated by the handling agent, with no automatic category-based rule currently assumed. Final escalation, approval, exception and validation rules remain open.
- Emergency referrals should support minimum information and allow additional information to be collected later.
- The workflow should support an ABR ID being blank when unavailable, subject to the approved Ministry process.
- The workflow should support referrals to CPIMS+/MGYSD and other approved stakeholders, with OpenCHS selecting an approved service/referral target and Ministry-side distribution where required.
- The workflow should support closed-loop follow-up and status handling. One-way OpenCHS follow-up updates are supported in principle; CPIMS+ to OpenCHS status write-back is not committed.

### 7.4 Workflow decisions required

- Is supervisor approval required before transmission? **TBD**
- Is consent required in every referral scenario? **TBD**
- Can an operator cancel a queued referral? **TBD**
- Can a completed referral be corrected or re-submitted? **TBD**
- Which service/referral target and protection-concern selections are available to the handling agent? **TBD**
- Is supervisor escalation or approval required in any referral scenario? **TBD**
- Which perpetrator fields are mandatory or priority fields, and how are unknown values handled? **TBD**
- Are follow-up updates sent one-way from OpenCHS, returned from Primero/MGYSD, or supported through a combined process? **TBD**
- Which CPIMS+ service/referral targets and Ministry-side distribution rules apply? **TBD**
- Can CPIMS+ expose district supervisor/manager options through the API, or does Ministry-side distribution always occur after receipt? **TBD**

## 8. Proposed Technical Architecture

### 8.1 Components

| Component | Responsibility | Status |
|---|---|---|
| OpenCHS frontend | ABR field, referral action, validation, status display | Required; implementation location TBD |
| OpenCHS backend | Referral rules, permissions, queue creation, status API | Required; live code verification pending |
| Integration provider/client | JWT, request construction, response handling | Proposed |
| Durable queue | Preserve referrals through outages and retries | Required |
| Primero CPIMS+ API | Receive child-protection case referral | External dependency |
| Emergency phone path | Preserve urgent phone contact with police/first responders alongside system referral | Agreed operational principle; procedure and evidence TBD |
| CPIMS+ routing | Select a service/referral target; Ministry-side supervisor/manager accepts, rejects or distributes internally | Session 2 working assumption; Primero technical confirmation pending |
| Audit log | Record safe transmission and retry evidence | Required |
| Monitoring/support view | Surface failed, pending and follow-up referrals | Required for operations; design TBD |
| Feedback/status mechanism | Record one-way follow-up updates and agreed intermediate/acceptance/closure status where available | Intermediate statuses and direction, mechanism and status vocabulary TBD |

### 8.2 Architecture recommendation

The Primero integration should be implemented as a configured integration provider rather than as an isolated special-case workflow. The provider should support credential configuration, mapping, retry policy, connection testing, lookup synchronisation where approved, and job/audit tracking.

The two-week MVP may implement only the provider capabilities required for `push_referral`, while retaining an extension path for `verify_connection`, `sync_lookup`, and `pull_case_status` if those are later approved.

The Session 1 template pack records the direct OpenCHS-to-CPIMS+ path. X-Road/Home Affairs integration is recorded as a separate workstream and must not be assumed to be part of this integration scope without a governance decision.

Session 2 records that CPIMS+ referrals are service-type-based: the receiving party may accept or reject before opening the case file, and a supervisor/manager may later assign the case to a caseworker. The integration must distinguish technical acknowledgement, business acceptance/rejection, assignment, service completion and closure; it must not assume that OpenCHS selects an individual caseworker.

### 8.3 Architecture items to verify

- Current OpenCHS backend and frontend structure.
- Existing referral and case models.
- Existing task/queue infrastructure.
- Existing integration framework, if any.
- Existing role and permission model.
- Existing audit/event model.
- Existing deployment and secret-management approach.

## 9. ABR ID Requirements Baseline

The project documentation identifies ABR as a referral-related identifier, but Session 1 recorded that a referral may need to proceed with the ABR ID blank when it is unavailable. The example pattern in the technical context is explicitly draft and must not be treated as the production rule.

The following must be confirmed by the responsible authority:

- Meaning and official name of ABR.
- Owning authority and source system.
- Creation or assignment point.
- Required/optional status.
- Missing-ID and follow-up process, including the MGYSD facilitation route.
- Length and character set.
- Prefix and structural components.
- Check-digit algorithm, if applicable.
- National or system-specific uniqueness.
- Handling of missing, unknown, corrected, or duplicate identifiers.
- Sample valid and invalid values.

**Interim position:** Do not hard-code the documented example format as final. If a sandbox build needs provisional validation, the rule must be configurable and clearly labelled provisional.\

## 10. Data-Mapping Baseline

The following mapping is proposed for review only.

| OpenCHS field | Proposed Primero field | Rule/status |
|---|---|---|
| OpenCHS case/call ID | `openchs_reference_id` | Must be unique; confirm target support |
| ABR ID | `abr_id` | Custom-field assumption; confirm |
| Child first name | `name_first` | Mandatory rule TBD; identifying information may be required for CPIMS+ registration |
| Child last name | `name_last` | Optional rule TBD |
| Child sex | `sex` | Primero code list must be confirmed |
| Child nationality | `nationality` | Candidate field from Session 2; target field and requiredness TBD |
| Date of birth | `date_of_birth` | Format and partial-date handling TBD |
| Age | `age` | Confirm whether numeric/range is accepted |
| Estimated age | `estimated` | Confirm target field |
| Protection concerns | `protection_concerns` | Must use current Primero lookup values |
| Protection concerns/category | Primero protection-concern/service vocabulary | OpenCHS case category may map to multiple CPIMS+ protection concerns; standardized list pending |
| Risk level | `risk_level` | Mapping requires business approval |
| Location | `location_current` | Primero hierarchy/code required |
| Case notes | `referral_notes` | Data-minimisation review required |
| Reporter contact details | Primero reporter/contact field(s) | Candidate requirement for follow-up contact; exact field and privacy rule TBD |
| Referral source | `referral_source` | Proposed: Child Helpline 116; confirm code |
| Module | `module_id` | Proposed: `primeromodule-cp`; confirm |
| Perpetrator information | Primero perpetrator-related field(s) | Important priority; exact fields and requiredness TBD |
| Missing ABR ID | Null/blank or agreed omission | Must not block approved emergency referral; target contract and follow-up rule TBD |
| Feedback/status | OpenCHS referral status or linked feedback fields | Closed-loop requirement agreed in principle; mechanism TBD |
| Case plan | Not transmitted in MVP | Session 2 working direction: each system maintains its own case plan; confirm mapping exclusion |

### Mapping acceptance rule

No field should be transmitted to production solely because it appears in a developer example. The final mapping must identify source field, target field, requiredness, transformation, validation, privacy classification, and approval owner.

Session 2 also identified the following mapping constraints for confirmation: OpenCHS case category may map to multiple CPIMS+ protection concerns; the referral service value may be a label such as `CPIMS+` or `Child Protection Service`; attachments and follow-up updates require explicit scope decisions; and anonymous OpenCHS reports may not be referable to CPIMS+ unless the receiving-system minimum-identification and exception rules are approved.

## 11. API and Authentication Requirements

The upstream API documentation supplied by Isaiah describes API v2. Record the documentation as received, while the applicable Lesotho release, base URL, configured schema and approved workflow remain Pending. The `development_v2` branch is a moving reference; retain a release or commit reference agreed with Primero before implementation.

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

The Ministry and Child Helpline must supply current SOPs, paper referral forms, approved child-journey use cases and existing referral pathways, or identify missing pathway documentation. Primero will use these to configure the demo; Isaiah expects API field definitions and lookup/code lists to be available after setup. The teams must jointly capture the resulting integration specification because Isaiah reports no existing interface specification.

ABR business rules must be defined with the use case. The response does not establish ABR ownership, format, requiredness or target field. Retain the optional/non-blocking working direction subject to formal confirmation. The response also does not answer duplicate-prevention or status-transport questions.

## 12. Queue, Retry and Idempotency Design

### 12.1 Proposed referral states

`Draft → Pending → Processing → Completed`

Failure states:

`Pending/Processing → Failed → Manual review or controlled retry`

### 12.2 Retry policy

The existing documentation proposes delays of 1 minute, 5 minutes, 30 minutes, and 2 hours. This remains **Proposed** until approved.

The final policy must define:

- Retryable errors.
- Non-retryable errors.
- Maximum attempts.
- Back-off intervals.
- Operator/admin notification.
- Manual retry authority.
- Dead-letter or permanent-failure handling.

Only one authoritative retry mechanism should control retry counts and scheduling. Combining overlapping application and task-level retries without a clear design must be avoided.

### 12.3 Idempotency

The project must agree a stable transaction key before development completion. The preferred approach is a unique OpenCHS referral identifier, optionally combined with the OpenCHS case identifier and receiving-system context.

The design must address the scenario where Primero creates a case but the response is lost. The integration must reconcile the existing case before issuing another create request.

## 13. Security, Privacy and Safeguarding

The integration handles sensitive child-protection information and must apply minimum-necessary sharing and access control.

Required controls:

- Approved data-sharing and legal-basis decision.
- Role-restricted referral initiation.
- Secure storage of API credentials.
- TLS certificate verification enabled in non-local environments.
- No credentials in source code or committed environment files.
- Redaction of sensitive payload fields in logs.
- Role-restricted access to integration logs.
- Audit of referral initiator and status changes.
- Minimum audit evidence should include the case/reference ID, timestamp, transaction/result information and relevant API response, subject to redaction and retention rules.
- Controlled access to failed payloads and retry actions.
- Defined retention period for payloads and integration logs.
- Documented incident and breach escalation path.

**TBD:** final privacy review, data-retention period, approved fields, and security sign-off authority.\

## 14. Roles and Responsibilities

| Work area | Primary owner | Supporting parties | Approval required |
|---|---|---|---|
| Business referral workflow | MGYSD | UNICEF, operations | MGYSD |
| ABR definition | MGYSD/relevant authority | Primero team, OpenCHS team | Business owner |
| API contract | Isaiah Amutavi Osotsi — confirmed Primero technical contact | OpenCHS technical team | Receiving-system approval authority to confirm |
| OpenCHS configuration | OpenCHS technical team | Operations | Product/technical lead |
| Data mapping | Joint technical and business team | Security/data protection | Joint approval |
| Security and privacy | UNICEF/MGYSD security owner | Technical teams | Security owner |
| UAT execution | Operations/UAT lead | UNICEF, MGYSD, technical teams | Named sign-off authority |
| Production access | Infrastructure/receiving-system teams | OpenCHS team | IT owner |
| Go-live decision | Project steering authority | All workstream leads | Named authority |
| Post-go-live support | To be confirmed | Technical and operational teams | Programme owner |

## 15. Environment and Access Plan

| Environment | Purpose | Required access | Status |
|---|---|---|---|
| Development | Build and unit testing | OpenCHS developers; test integrations | TBD |
| Integration test | API and queue testing | OpenCHS and Primero technical teams | TBD |
| UAT | Business acceptance | Operators, MGYSD, UNICEF, technical teams | TBD |
| Production | Live referrals | Restricted operational and support users | TBD |

The preferred Primero test environment is a configured demo. If delayed, Isaiah proposes a primerodev.org site; no specific URL, access date, credentials or UAT suitability evidence has been supplied. Agree minimum configuration inputs, delivery owner and a committed date, including when to select the alternative. An alternative Primero site is distinct from mock testing; neither proposal closes readiness without evidence.

### Access actions

- Confirm repository and deployment access.
- Confirm database/schema migration process.
- Confirm test accounts and user roles.
- Confirm API sandbox/UAT credentials.
- Confirm network path and allowlisting.
- Confirm production secret-management process.
- Confirm backup and rollback access.

## 16. Testing and Acceptance Strategy

Use child-journey use cases to link each UAT scenario to requirements and expected evidence. Isaiah recommends active representatives from agencies using the system. His reference to “any data” does not establish approval to use real child records; use synthetic data as the proposed default, subject to UAT/privacy approval. Named business and technical signatories remain Pending; Isaiah’s technical-contact role does not assign him sign-off authority.

### 16.1 Technical tests

- ABR validation tests.
- Permission and role tests.
- JWT authentication and refresh tests.
- Payload mapping tests.
- Primero success and validation-error tests.
- Network timeout and retry tests.
- Duplicate/idempotency tests.
- Queue recovery tests.
- Audit-log redaction and access tests.
- Regression tests for existing OpenCHS workflows.

### 16.2 UAT scenarios

1. Create or update a case.
2. Review the case and verify the manual handling-agent referral trigger behaviour.
3. Submit a minimum-information emergency referral.
4. Enter or obtain an ABR ID where available.
5. Submit a referral where the ABR ID is missing and verify follow-up handling.
6. Verify perpetrator information handling, including unknown or unavailable values.
7. Test an anonymous or insufficiently identified report and record the approved handling outcome.
8. Confirm service/referral-target receipt, CPIMS+ accept/reject behaviour, and case identifier where returned.
9. Test Ministry-side distribution and district supervisor/manager handling where configured.
10. Test Primero unavailability.
11. Confirm referral queue and retry behaviour.
12. Repeat a request and confirm no duplicate case.
13. Verify intermediate/follow-up status handling and audit evidence.
14. Verify the parallel emergency phone procedure where applicable.
15. Confirm operator and support procedures.

### 16.3 Acceptance evidence

Every UAT scenario should record:

- Scenario identifier.
- Tester and date.
- Input/test data reference.
- Expected result.
- Actual result.
- API or system evidence.
- Defect identifier, if applicable.
- Retest result.
- Business acceptance decision.

## 17. Implementation Baseline and Accelerated MVP Plan

| Period | Main activities | Gate/output |
|---|---|---|
| Days 1–2 | Session 1 decisions, access, scope freeze, API, referral workflow, routing, and ABR decisions | Approved baseline or escalated blockers |
| Days 2–3 | ABR/referral UI, permissions, workflow configuration | Referral surface available |
| Days 2–5 | API client, authentication, mapping, queue, audit, idempotency | First technical integration path |
| Days 6–7 | Technical tests, failure tests, regression testing | Test evidence and defect list |
| Days 8–9 | Technical/UAT preparation, Ministry-led UAT, fixes, readiness review | UAT result and acceptance recommendation |
| Day 10 | Training, handover, go/no-go, controlled release if approved | Go-live decision and D4 evidence |
| Remaining baseline period | Operational rollout, feedback/routing refinement, support, and agreed post-MVP work | D4/D5 evidence and operational handover |

## 18. Risks and Mitigations

| ID | Risk | Impact | Mitigation | Owner | Status |
|---|---|---|---|---|---|
| R-001 | Primero sandbox/API access is delayed | Critical-path delay to configuration, testing and UAT | Supply SOPs/forms/use cases; agree demo delivery and alternative-site decision dates, access package and connectivity evidence; continue draft mapping and mock preparation. A 48-hour escalation response remains proposed | Isaiah / Primero, coordinated with Ministry / UNICEF | Open — upstream docs received; demo/alternative proposed; access date unconfirmed |
| R-002 | ABR rules are not confirmed | Incorrect validation and rejected referrals | Assign decision owner; keep rule configurable |  | Open |
| R-003 | Primero lookup values differ from examples | Payload rejection | Obtain live lookup values before UAT |  | Open |
| R-004 | Idempotency is not supported as assumed | Duplicate case risk | Agree transaction/reconciliation method with receiving team |  | Open |
| R-005 | Sensitive data is over-logged | Privacy and safeguarding risk | Redact payloads and restrict access |  | Open |
| R-006 | Accelerated MVP scope expands | Delivery failure | Freeze MVP and maintain deferred backlog against the 14-week baseline |  | Open |
| R-008 | CPIMS+ service-based routing does not match direct district/stakeholder assumptions | Wrong recipient or delayed allocation | Confirm service targets, acceptance/rejection behaviour, district supervisor/manager distribution and API capabilities with Primero technical team | Primero/Ministry stakeholders | Open |
| R-007 | No post-go-live support owner | Unmanaged failures | Name queue and incident owner before go-live |  | Open |

## 19. Decision and Action Register

| ID | Decision/action | Owner | Deadline | Status | Evidence |
|---|---|---|---|---|---|
| D-001 | Confirm receiving system and deployed release | Isaiah / Primero | To confirm | Pending | Upstream API v2 documented; Lesotho release/configuration unconfirmed |
| D-002 | Confirm outbound referral and one-way follow-up update scope; decide whether inbound status write-back is included |  | Days 1–2 | Open | One-way follow-up updates supported in principle; inbound write-back not committed |
| D-003 | Approve manual handling-agent trigger, escalation/approval rules, and authorised role |  | Days 1–2 | Open | Session 2 records manual agent trigger; final rules remain pending |
| D-004 | Approve emergency minimum-information and partial-referral rules |  | Days 1–2 | Open | Session 1 agreed direction; field rules pending |
| D-005 | Approve ABR definition, validation owner, and missing-ID process |  | Days 1–2 | Open | Session 1 recorded missing ABR may be allowed |
| D-006 | Complete the configured API contract and sandbox access package | Isaiah / Primero; OpenCHS lead supporting | To confirm | Pending | Upstream documentation received; deployment schema, credentials and access outstanding |
| D-007 | Approve minimum data mapping, including perpetrator information |  | Days 1–3 | Open |  |
| D-008 | Approve privacy and legal-basis rules |  | Days 1–3 | Open |  |
| D-009 | Agree CPIMS+ service/referral targets, acceptance/rejection, Ministry distribution, and district-handling rules |  | Days 1–3 | Open | Session 2 revised the direct-routing assumption; technical confirmation pending |
| D-010 | Agree idempotency, retry, and escalation policy |  | Days 1–3 | Open |  |
| D-011 | Confirm Ministry-led UAT participants and sign-off authority | Ministry / UAT lead | Before UAT; date to confirm | Pending | Active agency representatives recommended; Isaiah confirmed as technical contact only |
| D-012 | Confirm post-go-live support owner |  | Before go-live | Open |  |
| D-013 | Confirm that X-Road/Home Affairs integration is outside this direct OpenCHS-to-CPIMS+ scope |  | Days 1–2 | Open | Template pack records it as a separate workstream |
| D-014 | Define minimum identifying information, anonymous-report handling, and CPIMS+ accept/reject rules |  | Before UAT | Open | Session 2 identified this as unresolved |

## 20. D1 Acceptance Criteria

D1 will be considered ready for approval when:

- ☐ Project stakeholders and decision owners are named.
- ☐ MVP scope is approved.
- ☐ Referral workflow is approved or has assigned decisions.
- ☐ Authorised referral role and referral-trigger rules are approved or assigned.
- ☐ Manual handling-agent trigger, escalation and approval rules are resolved.
- ☐ CPIMS+ service/referral targets, acceptance/rejection and Ministry-side distribution rules are resolved.
- ☐ Anonymous/insufficient-identification referral handling is resolved.
- ☐ Emergency minimum-information and missing-ABR referral rules are approved or assigned.
- ☐ ABR ownership and rules are approved or formally blocked.
- ☐ API and authentication requirements are documented.
- ☐ Environment and access requirements are documented.
- ☐ Field-mapping baseline is approved or assigned for closure.
- ☐ Retry, offline, idempotency, and audit requirements are documented.
- ☐ Security and data-sharing requirements have an owner and review date.
- ☐ Ministry-led UAT participants, scenarios, and sign-off authority are confirmed.
- ☐ Implementation baseline and delivery gates are accepted.
- ☐ Risks and unresolved actions have owners and deadlines.
- ☐ Primero sandbox readiness, escalation owner, and fallback test approach are recorded.

## 21. Approval and Sign-Off

Approval of this document confirms that it is the working D1 baseline. It does not approve unmarked assumptions for production use.

| Approval role | Name | Signature | Date |
|---|---|---|---|
| Business owner |  |  |  |
| UNICEF programme owner |  |  |  |
| OpenCHS technical lead |  |  |  |
| Primero technical lead |  |  |  |
| Data protection/security owner |  |  |  |
| UAT sign-off authority |  |  |  |
| Project manager |  |  |  |

## Appendix A — Items Not Yet Verified

The following must not be described as implemented or production-ready until verified in the actual OpenCHS and Primero environments:

- OpenCHS repository structure and current code state.
- Existing referral and integration models.
- Lesotho deployment confirmation of upstream-documented API paths and configured request/response schemas.
- ABR official format and check-digit rules.
- Primero lookup and protection-concern codes.
- Production authentication and secret-management arrangements.
- Network connectivity and firewall configuration.
- Production monitoring and support procedures.
- Final referral-trigger mode and category rules.
- CPIMS+ service/referral target vocabulary and acceptance/rejection contract.
- Minimum identifying information and anonymous-report exception handling.
- CPIMS+ status write-back remains Deferred unless approved through change control.
- X-Road/Home Affairs scope boundary and any related funding/governance decision.

## Appendix B — Immediate Day-1 Meeting Agenda

1. Confirm participants and decision authority.
2. Confirm systems, versions, and environments.
3. Approve the accelerated MVP work package and implementation baseline.
4. Confirm outbound or bi-directional integration direction.
5. Resolve referral trigger, emergency minimum-information, and ABR rules.
6. Review API documentation, endpoints, and credentials.
7. Approve minimum field mapping, including perpetrator information.
8. Approve routing, Ministry distribution, district handling, and closed-loop feedback.
9. Approve privacy, consent, and data-minimisation rules.
10. Approve retry, offline, idempotency, and audit approach.
11. Confirm Ministry-led UAT, training, go-live, and support owners.
12. Review risks and blockers.
13. Sign the D1 baseline and issue the action register.

## Revision record

| Version | Date | Change | Approval status |
|---|---|---|---|
| 0.4 | 26 October 2026 | Incorporated Isaiah’s response, upstream API/token evidence, configuration dependencies, contact, environment options and outstanding decisions | Draft; no new business, security or UAT approval inferred |
