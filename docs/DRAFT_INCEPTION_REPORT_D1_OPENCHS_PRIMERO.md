# Draft Inception Report — D1
## Lesotho Child Helpline 116 / OpenCHS–Primero CPIMS+ Integration

**Document status:** Draft — for inception review and decision  
**Version:** 0.1  
**Date:** 30 September 2026  
**Prepared for:** UNICEF Lesotho / MGYSD / Child Helpline 116 stakeholders  
**Prepared by:** Project Management and Technical Delivery Team  
**Target delivery model:** Two-week accelerated MVP implementation

> This document is a working inception baseline. It does not confirm any item that has not been approved by the responsible business, technical, security, or receiving-system owner. Unconfirmed items are marked **TBD**, **Proposed**, or **To be confirmed**.

---

## 1. Executive Summary

The project will configure and integrate the Lesotho Child Helpline 116 / OpenCHS environment with Primero CPIMS+ to support a controlled outbound child-protection referral workflow.

The immediate delivery objective is a safe minimum viable integration in a compressed two-week implementation window. The MVP will allow an authorised OpenCHS user to capture or validate the ABR ID, initiate a referral, queue the referral, transmit an approved case payload to Primero using JWT authentication, prevent duplicate submissions, display referral status, and retain an appropriate audit trail.

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
- Produce a controlled two-week implementation plan.

## 3. Source Baseline

This draft is based on the following project documents:

1. `Lesotho_OpenCHS_Technical_Scope_Inception_Brief.pdf`
2. `Lesotho_OpenCHS_Implementation_Timeline_Presentation.pptx`
3. `docs/CONTEXT.md`
4. `docs/docs/platform/reference/OPENCHS_PRIMERO_INTEGRATION_CONTEXT.md`
5. `docs/context/12_PRIMERO_CPIMS_CONTEXT.md`
6. `docs/prompts/16-backend-integrations.md`

The current workspace contains documentation and planning material only. The existence, completeness, and runtime status of the described OpenCHS source components must be verified against the actual OpenCHS repository and deployment environment.

## 4. Current Baseline and Evidence Status

| Area | Current documented position | Status |
|---|---|---|
| Helpline platform | OpenCHS v5 case-management and telephony platform | Documented; live environment TBD |
| Receiving platform | Primero CPIMS+ API v2 | Proposed/documented; exact deployment TBD |
| Integration direction | Outbound referral from OpenCHS to Primero | Proposed by scope; final decision required |
| ABR ID | Required referral-related identifier | Format, owner, and validation TBD |
| Authentication | JWT-based API authentication | Documented; live contract TBD |
| Queueing | Offline/durable referral queue | Required by scope; live implementation unverified |
| Idempotency | Required to prevent duplicate cases | Design and key format TBD |
| Audit logging | Required for attempts, responses, and retries | Logging fields and redaction rules TBD |
| UAT | MGYSD/UNICEF and receiving-system participation | Participants and sign-off authority TBD |
| Production support | Required after go-live | Owner and operating model TBD |

## 5. Scope

### 5.1 In scope for the accelerated MVP

- OpenCHS referral initiation workflow.
- ABR ID capture and approved validation.
- Referral permissions and authorised roles.
- Primero API authentication.
- Primero case-creation request.
- Confirmed OpenCHS-to-Primero data mapping.
- Durable referral queue.
- Retry and failure handling.
- Idempotency and duplicate prevention.
- Referral status visibility.
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
- Non-essential reporting and analytics.
- Automated production deployment pipelines.

Any deferred item that is later found to be mandatory must be added to the decision register and assessed for schedule impact.

## 6. Business Problem and Expected Outcome

Child Helpline 116 operators need a controlled way to refer eligible child-protection cases to the receiving case-management platform. The referral process must protect children and callers, avoid duplicate cases, preserve referrals during connectivity failures, provide clear operator feedback, and create sufficient evidence for accountability and support.

The expected outcome is:

```text
OpenCHS call/case
    ↓
ABR ID and referral validation
    ↓
Authorised referral action
    ↓
Durable queue and audit record
    ↓
JWT-authenticated Primero API request
    ↓
Primero case identifier
    ↓
OpenCHS referral status and support trail
```

## 7. Proposed End-to-End Workflow

### 7.1 Normal workflow

1. Operator records or updates the relevant OpenCHS case/call.
2. Operator enters or confirms the ABR ID, subject to the approved rules.
3. Operator confirms the referral decision and any required consent/legal basis.
4. OpenCHS validates required fields and referral permissions.
5. OpenCHS creates a durable referral record before external transmission.
6. The integration service creates an idempotency/transaction key.
7. The integration client authenticates to Primero using the approved JWT flow.
8. OpenCHS submits the confirmed case payload.
9. OpenCHS stores the Primero response and case identifier where successful.
10. OpenCHS displays the referral status to authorised users.

### 7.2 Failure workflow

1. Validation failures are shown to the operator and are not transmitted.
2. Authentication failure triggers one controlled token refresh attempt.
3. Network timeouts and temporary server failures are retained and retried.
4. Primero validation errors are marked failed and require correction or review.
5. A referral that exceeds the retry limit is escalated to the support owner.
6. Any uncertain result after a timeout is reconciled using the transaction key before another create request is issued.

### 7.3 Workflow decisions required

- Is supervisor approval required before transmission? **TBD**
- Is consent required in every referral scenario? **TBD**
- Can an operator cancel a queued referral? **TBD**
- Can a completed referral be corrected or re-submitted? **TBD**
- Is status written back from Primero, or only returned at creation time? **TBD**

## 8. Proposed Technical Architecture

### 8.1 Components

| Component | Responsibility | Status |
|---|---|---|
| OpenCHS frontend | ABR field, referral action, validation, status display | Required; implementation location TBD |
| OpenCHS backend | Referral rules, permissions, queue creation, status API | Required; live code verification pending |
| Integration provider/client | JWT, request construction, response handling | Proposed |
| Durable queue | Preserve referrals through outages and retries | Required |
| Primero CPIMS+ API | Receive child-protection case referral | External dependency |
| Audit log | Record safe transmission and retry evidence | Required |
| Monitoring/support view | Surface failed and pending referrals | Required for operations; design TBD |

### 8.2 Architecture recommendation

The Primero integration should be implemented as a configured integration provider rather than as an isolated special-case workflow. The provider should support credential configuration, mapping, retry policy, connection testing, lookup synchronisation where approved, and job/audit tracking.

The two-week MVP may implement only the provider capabilities required for `push_referral`, while retaining an extension path for `verify_connection`, `sync_lookup`, and `pull_case_status` if those are later approved.

### 8.3 Architecture items to verify

- Current OpenCHS backend and frontend structure.
- Existing referral and case models.
- Existing task/queue infrastructure.
- Existing integration framework, if any.
- Existing role and permission model.
- Existing audit/event model.
- Existing deployment and secret-management approach.

## 9. ABR ID Requirements Baseline

The project documentation identifies ABR as a required field but does not provide an authoritative specification. The example pattern in the technical context is explicitly draft and must not be treated as the production rule.

The following must be confirmed by the responsible authority:

- Meaning and official name of ABR.
- Owning authority and source system.
- Creation or assignment point.
- Required/optional status.
- Length and character set.
- Prefix and structural components.
- Check-digit algorithm, if applicable.
- National or system-specific uniqueness.
- Handling of missing, unknown, corrected, or duplicate identifiers.
- Sample valid and invalid values.

**Interim position:** Do not hard-code the documented example format as final. If a sandbox build needs provisional validation, the rule must be configurable and clearly labelled provisional.

## 10. Data-Mapping Baseline

The following mapping is proposed for review only.

| OpenCHS field | Proposed Primero field | Rule/status |
|---|---|---|
| OpenCHS case/call ID | `openchs_reference_id` | Must be unique; confirm target support |
| ABR ID | `abr_id` | Custom-field assumption; confirm |
| Child first name | `name_first` | Mandatory rule TBD |
| Child last name | `name_last` | Optional rule TBD |
| Child sex | `sex` | Primero code list must be confirmed |
| Date of birth | `date_of_birth` | Format and partial-date handling TBD |
| Age | `age` | Confirm whether numeric/range is accepted |
| Estimated age | `estimated` | Confirm target field |
| Protection concerns | `protection_concerns` | Must use current Primero lookup values |
| Risk level | `risk_level` | Mapping requires business approval |
| Location | `location_current` | Primero hierarchy/code required |
| Case notes | `referral_notes` | Data-minimisation review required |
| Referral source | `referral_source` | Proposed: Child Helpline 116; confirm code |
| Module | `module_id` | Proposed: `primeromodule-cp`; confirm |

### Mapping acceptance rule

No field should be transmitted to production solely because it appears in a developer example. The final mapping must identify source field, target field, requiredness, transformation, validation, privacy classification, and approval owner.

## 11. API and Authentication Requirements

The documented design proposes a Primero API v2 token endpoint and case endpoint. These endpoints remain subject to confirmation by the receiving-system technical team.

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
- Controlled access to failed payloads and retry actions.
- Defined retention period for payloads and integration logs.
- Documented incident and breach escalation path.

**TBD:** final privacy review, data-retention period, approved fields, and security sign-off authority.

## 14. Roles and Responsibilities

| Work area | Primary owner | Supporting parties | Approval required |
|---|---|---|---|
| Business referral workflow | MGYSD | UNICEF, operations | MGYSD |
| ABR definition | MGYSD/relevant authority | Primero team, OpenCHS team | Business owner |
| API contract | Primero technical team | OpenCHS technical team | Receiving-system owner |
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

### Access actions

- Confirm repository and deployment access.
- Confirm database/schema migration process.
- Confirm test accounts and user roles.
- Confirm API sandbox/UAT credentials.
- Confirm network path and allowlisting.
- Confirm production secret-management process.
- Confirm backup and rollback access.

## 16. Testing and Acceptance Strategy

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
2. Enter or obtain an ABR ID.
3. Initiate a valid referral.
4. Confirm receipt and Primero case identifier.
5. Submit an invalid referral.
6. Test Primero unavailability.
7. Confirm referral queue and retry behaviour.
8. Repeat a request and confirm no duplicate case.
9. Verify referral status and audit trail.
10. Confirm operator and support procedures.

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

## 17. Two-Week Implementation Plan

| Period | Main activities | Gate/output |
|---|---|---|
| Day 1 | Decision meeting, access, scope freeze, API and ABR decisions | Approved baseline or escalated blockers |
| Days 2–3 | ABR/referral UI, permissions, workflow configuration | Referral surface available |
| Days 2–5 | API client, authentication, mapping, queue, audit, idempotency | First technical integration path |
| Days 6–7 | Technical tests, failure tests, regression testing | Test evidence and defect list |
| Days 8–9 | UAT execution, fixes, readiness review | UAT result and acceptance recommendation |
| Day 10 | Training, handover, go/no-go, controlled release if approved | Go-live decision and D4 evidence |

## 18. Risks and Mitigations

| ID | Risk | Impact | Mitigation | Owner | Status |
|---|---|---|---|---|---|
| R-001 | Primero API access is delayed | Critical-path delay | Obtain sandbox access on Day 1; use contract tests only as interim evidence |  | Open |
| R-002 | ABR rules are not confirmed | Incorrect validation and rejected referrals | Assign decision owner; keep rule configurable |  | Open |
| R-003 | Primero lookup values differ from examples | Payload rejection | Obtain live lookup values before UAT |  | Open |
| R-004 | Idempotency is not supported as assumed | Duplicate case risk | Agree transaction/reconciliation method with receiving team |  | Open |
| R-005 | Sensitive data is over-logged | Privacy and safeguarding risk | Redact payloads and restrict access |  | Open |
| R-006 | Two-week scope expands | Delivery failure | Freeze MVP and maintain deferred backlog |  | Open |
| R-007 | No post-go-live support owner | Unmanaged failures | Name queue and incident owner before go-live |  | Open |

## 19. Decision and Action Register

| ID | Decision/action | Owner | Deadline | Status | Evidence |
|---|---|---|---|---|---|
| D-001 | Confirm receiving system and version |  | Day 1 | Open |  |
| D-002 | Confirm outbound-only or bi-directional scope |  | Day 1 | Open |  |
| D-003 | Approve ABR definition and validation owner |  | Day 1 | Open |  |
| D-004 | Provide API specification and sandbox credentials |  | Day 1 | Open |  |
| D-005 | Approve minimum data mapping |  | Day 1 | Open |  |
| D-006 | Approve privacy and legal-basis rules |  | Day 1 | Open |  |
| D-007 | Agree idempotency approach |  | Day 1 | Open |  |
| D-008 | Agree retry and escalation policy |  | Day 1 | Open |  |
| D-009 | Confirm UAT participants and sign-off authority |  | Day 1 | Open |  |
| D-010 | Confirm post-go-live support owner |  | Day 1 | Open |  |

## 20. D1 Acceptance Criteria

D1 will be considered ready for approval when:

- ☐ Project stakeholders and decision owners are named.
- ☐ MVP scope is approved.
- ☐ Referral workflow is approved or has assigned decisions.
- ☐ ABR ownership and rules are approved or formally blocked.
- ☐ API and authentication requirements are documented.
- ☐ Environment and access requirements are documented.
- ☐ Field-mapping baseline is approved or assigned for closure.
- ☐ Retry, offline, idempotency, and audit requirements are documented.
- ☐ Security and data-sharing requirements have an owner and review date.
- ☐ UAT participants, scenarios, and sign-off authority are confirmed.
- ☐ Two-week plan and delivery gates are accepted.
- ☐ Risks and unresolved actions have owners and deadlines.

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
- Actual Primero API endpoints and response schema.
- ABR official format and check-digit rules.
- Primero lookup and protection-concern codes.
- Production authentication and secret-management arrangements.
- Network connectivity and firewall configuration.
- Production monitoring and support procedures.

## Appendix B — Immediate Day-1 Meeting Agenda

1. Confirm participants and decision authority.
2. Confirm systems, versions, and environments.
3. Approve two-week MVP scope.
4. Confirm outbound or bi-directional integration direction.
5. Resolve ABR ownership and rules.
6. Review API documentation, endpoints, and credentials.
7. Approve minimum field mapping.
8. Approve privacy, consent, and data-minimisation rules.
9. Approve retry, offline, idempotency, and audit approach.
10. Confirm UAT, training, go-live, and support owners.
11. Review risks and blockers.
12. Sign the D1 baseline and issue the action register.
