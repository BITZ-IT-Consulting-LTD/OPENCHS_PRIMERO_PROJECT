# Fourteen-Week OpenCHS–Primero Implementation

## Slide 1 — Fourteen-Week Implementation Plan

### Slide content

- Lesotho Child Helpline 116 / OpenCHS
- Primero CPIMS+ integration
- Fourteen-week implementation window
- Objective: controlled implementation, UAT, training, handover, and go-live

### Speaker notes

The approved planning baseline is approximately fourteen weeks from inception to go-live. Activities overlap by design, but the sequence protects the quality of requirements, development, testing, UAT, training, and handover. The timeline remains subject to formal agreement during inception.

## Slide 2 — Delivery Objective

### Slide content

By the end of Week 14:

- Authorized operator captures ABR ID
- Operator initiates a referral
- OpenCHS validates and queues the referral
- Primero receives the case through the agreed API
- Duplicate referrals are prevented
- Referral status is visible
- Audit evidence is available
- UAT and go-live decision are completed

### Speaker notes

The success criterion is an end-to-end referral that can be demonstrated, tested, audited, accepted by users, supported operationally, and released through an approved go-live decision.

## Slide 3 — Non-Negotiable Preconditions

### Slide content

The sprint cannot start effectively without:

- OpenCHS source-code and environment access
- Primero sandbox/API access
- API documentation and sample payloads
- JWT credentials or test credential process
- ABR specification
- Confirmed field mapping
- Named decision-makers
- UAT participants and sign-off authority

### Speaker notes

These are critical-path dependencies. If any are unavailable, the team must record the item as blocked rather than silently making assumptions. We will use provisional configuration only in the sandbox and will not present it as production-ready.

## Slide 4 — Scope: Must Have vs Deferred

### Slide content

**Must have**

- ABR ID field and validation
- Referral control and authorization
- Primero JWT client
- Case creation endpoint
- Queue and retry handling
- Idempotency protection
- Audit logging
- Referral status
- UAT and operational handover

**Deferred**

- Bi-directional case-status synchronization
- Advanced lookup administration
- Attachments and recordings
- Full generic integration marketplace
- Complex workflow redesign
- Non-essential reporting

### Speaker notes

The fourteen-week plan still requires scope control. The minimum safe outbound referral integration remains the priority. Status synchronization, advanced administration, and other enhancements should remain documented backlog items unless they are contractually mandatory.

## Slide 5 — Target MVP Architecture

### Slide content

```text
Operator
   ↓
OpenCHS Call/Case Form
   ↓
ABR Validation + Referral Permission
   ↓
Durable Referral Queue
   ↓
Primero API Client
   ↓
JWT Authentication
   ↓
Primero CPIMS+ API
   ↓
Case ID + Referral Status + Audit Log
```

### Speaker notes

OpenCHS remains the initiating system. The referral is persisted before transmission, so a temporary Primero outage does not lose the referral. The integration service handles authentication, transmission, retry, idempotency, and status reporting.

## Slide 6 — Governance and Decision Model

### Slide content

| Area | Decision owner |
|---|---|
| Business referral workflow | MGYSD |
| Data protection and sharing | UNICEF / MGYSD |
| ABR definition and rules | MGYSD / relevant authority |
| API and authentication | Primero technical team |
| OpenCHS implementation | Delivery technical team |
| UAT acceptance | Named UNICEF/MGYSD authority |
| Production access | Receiving-system and IT teams |

### Speaker notes

Technical progress depends on business decisions. Every unresolved decision receives an owner and deadline. A decision without an owner is a delivery risk.

## Slide 7 — Weeks 1–2: Mobilize and Freeze the Contract

### Slide content

**Weeks 1–2 outputs**

- Confirm systems and owners
- Confirm outbound or bi-directional scope
- Receive API documentation
- Confirm sandbox access
- Confirm ABR rules
- Approve minimum field mapping
- Approve MVP acceptance criteria
- Create risk and decision register

### Speaker notes

The first two weeks establish the shared baseline. By the end of Week 2, we need enough information to build and test without inventing API fields, ABR rules, or business permissions.

## Slide 8 — Weeks 3–5: Build the Referral Surface

### Slide content

- Add/configure ABR ID field
- Add referral checkbox or action
- Add mandatory-field validation
- Restrict referral initiation by role
- Add duplicate-referral protection
- Add visible referral status
- Create database migration/configuration
- Test the form locally

### Speaker notes

The operator must understand what is required, what failed, and what happened after submission. The interface should prevent accidental duplicate referrals and should not expose administrative integration controls to ordinary operators.

## Slide 9 — Weeks 4–8: Build the Integration Core

### Slide content

In parallel:

- JWT authentication
- Token caching and refresh
- Primero case creation client
- Confirmed payload mapper
- Durable queue
- Retry and failure states
- Idempotency key
- Redacted integration log
- Manual retry mechanism

### Speaker notes

The queue is the reliability boundary. The referral must be stored before the external request is attempted. Authentication failures, validation failures, timeouts, and server errors must be classified differently because they require different retry behavior.

## Slide 10 — Retry and Error Policy

### Slide content

| Failure | Action |
|---|---|
| Invalid OpenCHS data | Do not queue; show validation error |
| Primero validation error | Mark failed; require correction |
| Authentication failure | Refresh token once; then alert |
| Timeout/network failure | Queue and retry |
| Primero server error | Retry with backoff |
| Duplicate response | Reconcile using idempotency key |
| Maximum retries exceeded | Escalate to support |

### Speaker notes

We must select one authoritative retry mechanism. We should not combine competing Celery retries and application-level retries without a clear design, because that can produce duplicate transmissions and confusing retry counts.

## Slide 11 — Weeks 8–10: Technical Testing

### Slide content

Test:

- Valid referral
- Missing ABR ID
- Invalid ABR ID
- Unauthorized referral attempt
- Invalid Primero payload
- Expired JWT
- Primero unavailable
- Timeout and retry
- Duplicate submission
- Manual retry
- Audit log access
- Existing OpenCHS regression

### Speaker notes

Testing must include failure scenarios, not only the successful API response. The most important evidence is that a failed or interrupted transmission does not lose the referral and does not create a duplicate case.

## Slide 12 — Weeks 10–12: UAT Preparation and Execution

### Slide content

UAT participants:

- Child Helpline operators
- Supervisors
- MGYSD representatives
- UNICEF representative
- Primero technical team
- OpenCHS technical team

UAT evidence:

- Test case
- Input data
- Expected result
- Actual result
- Screenshot/log/API evidence
- Pass/fail
- Defect owner
- Retest result

### Speaker notes

UAT should be evidence-based. Each scenario must have a named tester and a recorded result. Verbal confirmation alone is not sufficient for a child-protection integration.

## Slide 13 — Weeks 12–14: Production Readiness Review

### Slide content

Go-live checklist:

- UAT acceptance signed
- Production endpoint confirmed
- Production credentials loaded securely
- SSL verification enabled
- Backup and rollback tested
- Monitoring owner assigned
- Queue support procedure documented
- Operator instructions completed
- Escalation contacts confirmed
- Go-live approval recorded

### Speaker notes

A successful sandbox test does not automatically mean production readiness. Production access, secrets, network connectivity, monitoring, rollback, and support ownership must all be confirmed separately.

## Slide 14 — Go-Live Decision

### Slide content

**Go**

- End-to-end test passed
- No critical defects
- Idempotency verified
- Security controls verified
- Support coverage available
- Business owner signed off

**Conditional go**

- Minor defects have workarounds
- Risks accepted in writing
- Monitoring and rollback are active

**No-go**

- API contract unresolved
- ABR rules unresolved
- Duplicate prevention unverified
- Sensitive-data controls incomplete
- No accountable support owner

### Speaker notes

The go-live decision must be based on evidence, not schedule pressure. If a critical safety, privacy, data-integrity, or duplication issue remains unresolved, the correct decision is no-go or controlled pilot.

## Slide 15 — Risks and Mitigations

### Slide content

| Risk | Mitigation |
|---|---|
| API access delayed | Use mocked contract tests, but do not claim integration success |
| ABR rules unknown | Keep validation configurable and mark provisional |
| Primero lookup mismatch | Retrieve and confirm lookup values before UAT |
| Duplicate cases | Use agreed transaction key and reconciliation |
| Sensitive data leakage | Redact logs and restrict access |
| Scope expansion | Maintain deferred backlog |
| No support after launch | Assign named operational owner |

### Speaker notes

The biggest risk is not coding speed. It is making an unverified assumption that later causes rejected referrals, duplicate cases, or inappropriate disclosure of child-protection information.

## Slide 16 — Daily Operating Rhythm

### Slide content

Every day:

- 08:30 — blocker and dependency review
- 12:30 — technical progress checkpoint
- 16:30 — demonstration or evidence review
- 17:00 — decision/risk register update

Required artefacts:

- Decision log
- Risk register
- API contract
- Mapping table
- Test evidence
- Defect log
- Go-live checklist

### Speaker notes

With only two weeks, issues must be surfaced the same day. The project manager should maintain one visible action register with owner, due date, status, and escalation path.

## Slide 17 — Final Message

### Slide content

Two-week success means:

- Safe minimum scope
- Confirmed API contract
- No hidden assumptions
- Evidence-based UAT
- Controlled production decision
- Clear ownership after go-live

### Speaker notes

The fourteen-week plan provides time for proper requirements closure, configuration, integration development, technical testing, UAT, training, handover, and production readiness. The project should still protect the MVP boundary and refuse to treat unknowns as completed work.

## Source Documents

- `Lesotho_OpenCHS_Technical_Scope_Inception_Brief.pdf`
- `Lesotho_OpenCHS_Implementation_Timeline_Presentation.pptx`
- `docs/docs/platform/reference/OPENCHS_PRIMERO_INTEGRATION_CONTEXT.md`
- `docs/context/12_PRIMERO_CPIMS_CONTEXT.md`
