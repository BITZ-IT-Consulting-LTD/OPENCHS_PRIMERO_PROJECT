# OpenCHS–Primero Integration

## Current Lesotho evidence recorded on 26 October 2026

This technical material contains prior design examples and implementation descriptions. The current inception evidence is [D1 v0.4](../01_inception/DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO.md) and [Isaiah’s response](../06_correspondence/ISAIAH_RESPONSE_SOURCE_2026-10-26.md). These do not verify the OpenCHS runtime or a live Primero connection.

- Upstream API v2 documentation is received. Token, case-create/update and referral paths are documented, but the Lesotho deployed release, configured schemas and operation sequence remain Pending.
- Documented bearer JWTs expire after 60 minutes. SSO is preferred where an identity provider exists; username/password is an alternative. Unattended backend authentication and specific network controls require confirmation.
- A configured demo is preferred; a primerodev.org site is a proposed alternative. No actual URL, credentials or committed access date is supplied.
- Country SOPs, paper forms, use cases and referral pathways are configuration inputs. Configured field definitions/lookups follow demo setup; ABR rules must be defined with the use case.
- Isaiah Amutavi Osotsi is the Primero technical contact. Active agency representatives should participate in child-journey UAT; named signatories remain Pending.
- Session 2’s working model is service-based routing with Ministry-side distribution. Direct district/caseworker selection in older examples is unconfirmed. Status write-back is Deferred; duplicate prevention and retry recovery remain Pending.

Example URLs, `abr_id`, sample mappings, validation patterns, and architectural refactors below remain discovery/design material unless explicitly approved. Isaiah reports no rate limits; operating limits and retry policies still require agreement.

## First Meeting Decision Document

**Project:** Lesotho Child Helpline 116 / OpenCHS integration with Primero CPIMS+\
**Meeting purpose:** Close inception decisions and dependencies; two-week sequencing is a technical reference, not a revised contract schedule\
**Prepared by:** Project Management\
**Date:** ____________________\
**Version:** 0.2 – Working decision draft; evidence updated 26 October 2026\

---

## 1. Purpose of This Meeting

This meeting is a decision meeting, not a general briefing. Its purpose is to establish the minimum approved baseline for a safe, testable, and supportable OpenCHS–Primero referral integration within the compressed two-week schedule.

Every unresolved item must leave the meeting with one of the following outcomes:

1. Decision approved.
2. Decision assigned to a named owner with a deadline.
3. Item explicitly deferred from the two-week MVP.
4. Project blocker escalated to the appropriate authority.

No technical assumption should be treated as an approved requirement without an owner and recorded decision.

## 2. Required Meeting Participants

| Role | Name | Organisation | Decision authority |
|---|---|---|---|
| Business owner |  | MGYSD | Referral workflow and business rules |
| Programme owner |  | UNICEF | Programme acceptance and escalation |
| OpenCHS product/technical lead |  |  | OpenCHS implementation |
| Primero technical contact | Isaiah Amutavi Osotsi | UNICEF / Primero | Technical contact confirmed; approval authority to confirm |
| Child Helpline operations lead |  |  | Operator workflow and user acceptance |
| Data protection/security lead |  |  | Data-sharing and security controls |
| Infrastructure/network lead |  |  | Connectivity, environments, and deployment |
| Project manager |  |  | Decisions, risks, actions, and delivery control |

## 3. Proposed Two-Week MVP

The two-week MVP should include only the minimum safe end-to-end referral journey:

- Capture or configure the ABR ID.
- Validate the ABR ID according to an approved rule.
- Allow only authorized users to initiate a referral.
- Save the referral durably before external transmission.
- Authenticate to Primero using the approved JWT process.
- Submit the agreed case payload.
- Prevent duplicate cases through an agreed transaction/idempotency key.
- Retry temporary failures and retain failed referrals.
- Display referral status to authorized OpenCHS users.
- Maintain a redacted audit trail.
- Complete technical testing, UAT, training, and a go-live decision.

The following should be deferred unless contractually required: advanced bi-directional status synchronization, attachments or recordings, complex workflow redesign, non-essential reporting, and a full generic integration administration framework.

## 4. Decisions Required During the Meeting

### Decision 1 — Systems and integration direction

**Question:** Is the receiving system Primero CPIMS+, and what exact version and deployment are being integrated?\

**Questions to answer:**\

- What is the official system name and environment?
- Is the first release outbound-only from OpenCHS to Primero?
- Must Primero status or case identifiers be written back to OpenCHS?
- Is any inbound webhook or polling required in the MVP?

**Decision:** ____________________________________________________________\

**Owner:** ____________________  **Due date:** ____________________

### Decision 2 — Referral workflow

**Question:** What is the approved end-to-end business process from call handling to Primero case creation?\

**Questions to answer:**\

- At what point does an operator decide that a referral is required?
- Is supervisor approval required before transmission?
- Who may initiate a referral?
- Who may cancel or correct a referral?
- Can one OpenCHS case be referred more than once?
- What is the process when a referral is rejected?
- What is the process when Primero is unavailable?

**Decision:** ____________________________________________________________\

**Owner:** ____________________  **Due date:** ____________________

### Decision 3 — ABR ID definition and ownership

**Question:** What does ABR mean in this process, and which system owns the identifier?\

**Questions to answer:**\

- What is the official definition of ABR?
- Who creates or assigns the ABR ID?
- Is it entered manually, generated by OpenCHS, or supplied by another system?
- Is it mandatory for every referral?
- What happens when the child has no ABR ID?
- Is the identifier nationally unique?
- What is the official character set, length, prefix, and check-digit rule?
- Can an ABR ID be corrected after submission?

**Decision:** ____________________________________________________________\

**Owner:** ____________________  **Due date:** ____________________

### Decision 4 — API and authentication contract

**Question:** What exact API contract will the OpenCHS integration use?\

**Questions to answer:**\

- What are the sandbox, UAT, and production base URLs?
- Which API version is active?
- What is the authentication endpoint?
- What request format is required for authentication?
- What is the token lifetime and refresh process?
- What credentials, certificates, or allowlisted IP addresses are required?
- What are the required headers and content types?
- What are the expected success and error response structures?
- Is there a formal API specification or sample request/response pack?

**Decision:** ____________________________________________________________\

**Owner:** ____________________  **Due date:** ____________________

### Decision 5 — Data mapping and mandatory fields

**Question:** Which OpenCHS fields will be transferred to which Primero fields?\

**Questions to answer:**\

- Which child identity fields are mandatory?
- What are the approved sex, age, date, location, and risk-value codes?
- Which protection-concern lookup values are valid in Primero?
- Is ABR a standard Primero field or a configured custom field?
- What is the official referral-source value?
- Which notes and caller details may be shared?
- Are call recordings, phone numbers, names, or free-text notes excluded or restricted?
- What transformations and validation rules apply to each field?

**Decision:** ____________________________________________________________\

**Owner:** ____________________  **Due date:** ____________________

### Decision 6 — Consent, legal basis, and data minimisation

**Question:** What authorises the sharing of child-protection data with Primero?\

**Questions to answer:**\

- Is consent required, and at what point is it captured?
- What alternative legal or safeguarding basis applies when consent cannot be obtained?
- What is the minimum data required for referral?
- Which fields must be masked or excluded from logs?
- Who may view referral payloads and integration logs?
- How long must referral data and logs be retained?
- Are cross-border hosting, VPN, or data-residency constraints applicable?

**Decision:** ____________________________________________________________\

**Owner:** ____________________  **Due date:** ____________________

### Decision 7 — Retry, offline queue, and failure handling

**Question:** How should the system behave when Primero is unavailable or rejects a request?\

**Questions to answer:**\

- Which errors are retryable?
- Which errors must stop immediately and require correction?
- What is the maximum number of retries?
- What back-off schedule is approved?
- How are failed referrals surfaced to supervisors or administrators?
- Who can manually retry a failed referral?
- How is a permanently failed referral escalated?
- What is the required recovery-time expectation?

**Decision:** ____________________________________________________________\

**Owner:** ____________________  **Due date:** ____________________

### Decision 8 — Idempotency and duplicate prevention

**Question:** What unique transaction key guarantees that retries cannot create duplicate Primero cases?\

**Questions to answer:**\

- Which identifier is authoritative: OpenCHS case ID, referral ID, ABR ID, or a composite key?
- Does Primero support an idempotency header?
- Can Primero search for an existing case using the OpenCHS reference?
- What happens if the API times out after creating the case but before returning the response?
- How will the teams reconcile uncertain results?

**Decision:** ____________________________________________________________\

**Owner:** ____________________  **Due date:** ____________________

### Decision 9 — UAT and acceptance

**Question:** What evidence is required for acceptance of the integration?\

**Questions to answer:**\

- Who participates in UAT?
- Who signs off on business acceptance?
- Who signs off on technical acceptance?
- Which happy-path and failure scenarios are mandatory?
- What constitutes a critical defect?
- Are workarounds acceptable for conditional go-live?
- Where will UAT evidence and defects be recorded?

**Decision:** ____________________________________________________________\

**Owner:** ____________________  **Due date:** ____________________

### Decision 10 — Go-live and support

**Question:** Who operates and supports the integration after release?\

**Questions to answer:**\

- What is the production go-live date and time?
- Who owns first-line operator support?
- Who monitors the referral queue?
- Who manages Primero credentials and certificates?
- Who responds to failed referrals and API outages?
- What is the rollback procedure?
- What training must be completed before go-live?
- What support coverage is available during the first operating days?

**Decision:** ____________________________________________________________\

**Owner:** ____________________  **Due date:** ____________________

## 5. Decisions Register

| ID | Decision/action | Owner | Deadline | Status | Evidence/location |
|---|---|---|---|---|---|
| D-001 |  |  |  | Open |  |
| D-002 |  |  |  | Open |  |
| D-003 |  |  |  | Open |  |
| D-004 |  |  |  | Open |  |
| D-005 |  |  |  | Open |  |
| D-006 |  |  |  | Open |  |
| D-007 |  |  |  | Open |  |
| D-008 |  |  |  | Open |  |

**Status values:** Approved / Assigned / Deferred / Blocked / Rejected.\

## 6. Two-Week Delivery Gates

### Gate 1 — End of Day 1

- API access path confirmed.
- MVP scope approved.
- ABR decision owner assigned.
- Minimum field mapping agreed or assigned.
- UAT and sign-off authority confirmed.

### Gate 2 — End of Day 5

- ABR/referral UI available.
- API client can authenticate in the test environment.
- Referral queue and audit records exist.
- First payload mapping test completed.

### Gate 3 — End of Day 7

- Happy-path integration test passes.
- Retry and duplicate-prevention tests are executable.
- UAT environment and test data are ready.

### Gate 4 — End of Day 9

- UAT completed or documented blockers remain.
- Critical defects resolved or formally accepted.
- Production readiness checklist reviewed.

### Gate 5 — Day 10

- Go / conditional go / no-go decision recorded.
- Handover owner confirmed.
- Open risks and deferred scope transferred to the support backlog.

## 7. Immediate Actions After the Meeting

Within two hours of the meeting:

1. Circulate approved decisions and unresolved actions.
2. Share the final API documentation and mapping template.
3. Confirm technical access and credentials through a secure channel.
4. Create the shared UAT test register.
5. Establish the daily blocker and decision review.
6. Freeze non-MVP feature requests.

## 8. Go-Live Decision Rules

### Go

- End-to-end test passed.
- No unresolved critical defects.
- Idempotency verified.
- Sensitive-data controls verified.
- UAT and business sign-off completed.
- Support ownership confirmed.

### Conditional go

- Only minor defects remain.
- Workarounds are documented.
- Risks are accepted in writing.
- Monitoring and rollback are active.

### No-go

- API contract remains unresolved.
- ABR rules remain unresolved.
- Duplicate prevention is unverified.
- Sensitive-data controls are incomplete.
- No accountable support owner exists.

## 9. Source Documents

- `Lesotho_OpenCHS_Technical_Scope_Inception_Brief.pdf`
- `Lesotho_OpenCHS_Implementation_Timeline_Presentation.pptx`
- `docs/docs/platform/reference/OPENCHS_PRIMERO_INTEGRATION_CONTEXT.md`
- `docs/context/12_PRIMERO_CPIMS_CONTEXT.md`
