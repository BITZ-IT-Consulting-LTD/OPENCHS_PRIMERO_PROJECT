# Contract-Aligned Delivery Plan
## Lesotho Child Helpline 116 / OpenCHS–Primero CPIMS+ Integration

**Document status:** Working planning baseline — contract dates supplied by project owner; formal approval pending  
**Version:** 0.1  
**Prepared:** 14 October 2026  
**Contract validity:** 1 July 2026 to 28 February 2027  
**Payment terms:** Within 30 days, due net, against approved deliverables  
**Advance payment:** None unless exceptionally approved against a bank guarantee

> This plan is the commercial delivery baseline supplied for project planning. It does not convert unresolved API, ABR, data-protection, environment, or approval assumptions into verified implementation facts. The existing 14-week plan remains a historical/technical planning reference unless formally rebaselined.

## 1. Contract milestone summary

| Item | Contract deliverable | Target month | Approval/payment gate |
|---|---|---:|---|
| 10 | Inception, Requirements & Environment Setup | August 2026 | Approved inception report, technical design, mapping baseline, and environment-setup evidence |
| 20 | ABR ID Field, Validation & Referral Checkbox Development | October 2026 | Demonstrated field, approved/configured validation, referral control, save-event behaviour, and unit-test evidence |
| 30 | Outbound REST API Client — OpenCHS to Primero | November 2026 | API client, authentication, payload, queue/retry, idempotency, TLS, and audit evidence against an approved contract or controlled mock |
| 40 | Testing, UAT, Training & Go-Live | February 2027 | Approved test/UAT results, training and handover evidence, production-readiness decision, and go-live approval |

The contract supplies target months, not exact acceptance dates. The project manager should obtain written confirmation of the due date, approver, invoice trigger, and acceptance evidence for each item.

## 2. Calendar delivery baseline

| Period | Planned work | Required gate / evidence | Current status as at 14 October 2026 |
|---|---|---|---|
| 1–31 July 2026 | Contract mobilisation, governance, access requests, inception preparation, decision and risk registers | Named owners, kickoff date, access request record, approved working method | Historical period; evidence to reconcile |
| 1–31 August 2026 | Item 10: kickoff workshop; inception report; technical design; field-mapping baseline; environment configuration | Item 10 approval and invoice eligibility | Target month has passed; approval/payment status must be confirmed |
| September 2026 | Close inception decisions; obtain API/JWT/sandbox package; approve ABR and mapping rules; prepare development | D1 closure, API/access readiness, approved build backlog | Dependency closure required |
| 1–31 October 2026 | Item 20: ABR field, validation and referral checkbox/save-event development; unit tests | Demonstration and unit-test acceptance | Active delivery window; exact acceptance date to confirm |
| 1–30 November 2026 | Item 30: REST client, JWT, payload, retry, queue, idempotency, audit and TLS controls | Integration evidence against approved API contract/mock | Planned |
| December 2026–January 2027 | Integration hardening, technical testing, defect correction, UAT preparation, training materials, deployment rehearsal | Test evidence, defect register, UAT pack, rollback/readiness checklist | Planned |
| 1–28 February 2027 | Item 40: end-to-end testing, UAT, training, production deployment, technical handover and user/admin manuals | Signed UAT, go-live decision, handover pack, approved deliverable | Planned; must complete before 28 February 2027 |

## 3. Deliverable acceptance detail

### Item 10 — Inception, Requirements & Environment Setup

Required outputs:

- Kickoff workshop with UNICEF LCO, Ministry of Social Development, Child Helpline/OpenCHS, and Primero representatives.
- Approved or review-ready inception report.
- Detailed technical design, clearly separating confirmed facts, proposed design, and `To confirm` dependencies.
- OpenCHS-to-Primero data-mapping document, subject to UNICEF/Primero inputs.
- Environment configuration evidence for OpenCHS and API development tools.
- Decision, risk, action, dependency, and open-issue registers.

Acceptance cannot be represented as complete solely because documents exist. The approval record, named approver, environment evidence, and outstanding dependency treatment must be retained.

### Item 20 — ABR ID Field, Validation & Referral Checkbox Development

Required outputs:

- Non-mandatory ABR ID input on the OpenCHS call-intake form.
- Approved format and checksum validation rules matching confirmed HMIS/EMIS patterns, if applicable.
- Referral checkbox UI element with the agreed save-event trigger.
- Verification against the actual OpenCHS form engine.
- Unit-test evidence covering valid, invalid, blank, corrected, and duplicate values as applicable.

The ABR rule must remain configurable/provisional until the responsible authority supplies and approves the official format, checksum, ownership, and missing-ID process. A blank field must not be treated as a defect if the approved business rule keeps it non-mandatory.

### Item 30 — Outbound REST API Client — OpenCHS to Primero

Required outputs:

- REST `POST /api/v2/cases` client, subject to confirmation of the live Primero endpoint and contract.
- JWT bearer authentication and agreed refresh behaviour after a 401 response.
- Approved structured JSON payload and mapping transformations.
- Exponential retry schedule of 1 minute, 5 minutes, 30 minutes, and 2 hours, subject to technical approval and one authoritative retry controller.
- Durable offline queue with automatic send on connectivity restoration.
- Idempotency using a unique OpenCHS referral reference, plus reconciliation where a response is lost after case creation.
- Audit logging of timestamp, redacted payload summary, HTTP response code, Primero case ID, and retry count.
- HTTPS with TLS 1.2 or higher and certificate verification in non-local environments.

If sandbox access or the final API contract is unavailable, mock/contract tests may evidence client behaviour, but must not be described as successful live integration.

### Item 40 — Testing, UAT, Training & Go-Live

Required outputs:

- Unit tests against a mock API endpoint.
- End-to-end integration test: OpenCHS save → API call → Primero case with correct approved field values.
- Idempotency and duplicate-prevention evidence.
- Field-mapping validation and defect resolution record.
- UAT with UNICEF LCO, Ministry/Child Helpline users, and Primero representatives.
- Training for social workers/helpline operators, IT personnel, and supervisors.
- Production deployment evidence, or a documented no-go/conditional-go decision if readiness gates are not met.
- Technical handover report, user manual, and system administrator guide.

## 4. Dependencies and no-silent-rebaseline rules

The following are critical dependencies and require an owner, due date, and evidence:

- Primero sandbox/UAT and production URLs, credentials/JWT process, API documentation, sample payloads, scopes, and network/TLS prerequisites.
- Official ABR definition, owner, format, checksum, requiredness, and missing-ID process.
- Approved field mapping, protection-concern lookup values, minimum identification, anonymous-report handling, and free-text/privacy rules.
- Named UAT participants and sign-off authority.
- Production secret storage, backup/rollback, queue monitoring, incident escalation, and post-go-live support ownership.

If a dependency delays a milestone, record the impact in the risk and decision registers and seek written rebaseline approval. Do not silently move a deliverable, claim live integration from a mock, or invoice an unapproved deliverable.

## 5. Payment administration

Payment is tied to approved deliverables, not merely the target month. For each milestone retain:

1. Submitted deliverable package and version.
2. Acceptance comments and signed/email approval from the authorised approver.
3. Evidence index linking requirements, tests, demonstrations, and unresolved exceptions.
4. Invoice date and payment-due date calculated as net 30 from the applicable approved-deliverable trigger.
5. Any written conditional acceptance, waiver, or approved change request.

No advance payment should be assumed. Any exceptional advance requires separate written approval and a bank guarantee.

## 6. Control documents

- [Draft D1 Inception Report](DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO.md)
- [Inception Completion Inventory](INCEPTION_COMPLETION_INVENTORY.md)
- [Original 14-week implementation notes](FOURTEEN_WEEK_IMPLEMENTATION_SLIDE_NOTES.md)
- [Two-week project checklist](OPENCHS_PRIMERO_TWO_WEEK_PROJECT_CHECKLIST.md)

The contract-aligned plan should be used for commercial dates and milestone reporting. The technical notes and checklists remain supporting evidence and must not override the contract schedule without approval.
