# Contract-Aligned Delivery Plan
## Lesotho Child Helpline 116 / OpenCHS–Primero CPIMS+ Integration

**Document status:** Working planning baseline — owner-supplied TICAD-2026-001 text; signed status and relationship to earlier contract reference pending  
**Version:** 0.3  
**Prepared:** 14 October 2026  
**Evidence update:** 28 October 2026  
**Contract validity:** 1 July 2026 to 28 February 2027  
**Payment terms:** Within 30 days, due net, against approved deliverables  
**Advance payment:** None unless exceptionally approved against a bank guarantee

> This plan is the commercial delivery baseline supplied for project planning. It does not convert unresolved API, ABR, data-protection, environment, or approval assumptions into verified implementation facts. The existing 14-week plan remains a historical/technical planning reference unless formally rebaselined.

## Evidence update and configuration dependency

Isaiah’s response supplies the upstream API reference and confirms the Primero technical contact. A configured demo is preferred, with a possible primerodev.org alternative. Country SOPs, paper forms, use cases and workflow are configuration inputs; configured fields/lookups follow setup. No access or delivery date is confirmed. ABR rules, backend authentication, security prerequisites, duplicates and named UNICEF user-testing signatory remain Pending.

Record this dependency sequence in delivery planning: country inputs and approved use cases → Primero configuration → configured dictionary and mapping validation → integration testing and UAT. Request named owners and committed dates. This evidence update changes neither the contractual dates nor acceptance/payment gates; any rebaseline requires governance approval. See [current D1 v1.0](../01_inception/DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO_V1.0.md).

## 1. Contract milestone summary

| Item | Contract deliverable | Target month | Approval/payment gate |
|---|---|---:|---|
| 10 | Inception, Requirements & Environment Setup | August 2026 | Approved inception report, technical design, mapping baseline, and environment-setup evidence |
| 20 | ABR ID Field, Validation & Referral Checkbox Development | October 2026 | Demonstrated field, approved/configured validation, referral control, save-event behaviour, and unit-test evidence |
| 30 | Outbound REST API Client — OpenCHS to Primero | November 2026 | API client, authentication, payload, queue/retry, idempotency, TLS, and audit evidence against an approved contract or controlled mock |
| 40 | Testing, UAT, Training & Go-Live | February 2027 | Approved test/UAT results, training and handover evidence, production-readiness decision, and go-live approval |

The contract supplies target months, not exact acceptance dates. The project manager should obtain written confirmation of the due date, approver, invoice trigger, and acceptance evidence for each item.

## 2. Calendar delivery baseline


**Figure 6 — Contractual timetable.** The supplied contract covers 1 July 2026 to 28 February 2027 [CT1 §§3–4]. These are original targets, not a record of completed work. The milestone months group several tasks; an October software task can form part of the November acceptance milestone.

| Period | Required work | Evidence or approval |
|---|---|---|
| July–August 2026 | Inception, design, information mapping, system preparation, repository access and ABR specification | D1 report, design, mapping and setup evidence; August Item 10 milestone |
| September 2026 | Optional ABR field and required number checks | Demonstration and test evidence; part of Item 20 |
| October 2026 | Referral checkbox and initial connection to Primero | Demonstration and software tests; October Item 20 milestone; initial connection contributes to Item 30 |
| November 2026 | Complete connection, activity records, linked Primero case reference and operator alerts | Item 30 evidence and review; usable Primero access needed for subsequent live tests |
| December 2026 | Test individual parts and use a simulated receiving system | Test and coverage reports; simulated tests do not prove live integration |
| January 2027 | Test both systems together, check transferred information, conduct user testing and resolve faults to UNICEF satisfaction | Integration results and UNICEF-executed user-testing sign-off; Ministry leads user testing under D-009 |
| February 2027 | Deploy, check the released system, train staff in Maseru and complete handover | UNICEF launch confirmation, attendance, agreed English/Sesotho materials, manuals, technical report, administrator guide and Service Provider assessment; Item 40 |
| Ninety days after launch | Free maintenance support | Named support owners and recorded support period; end date follows actual launch and requires confirmation |


Original targets above are not evidence of completion. The [report section 8.7](../01_inception/DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO_V1.0.md) contains the proposed recovery timetable: late October/early November decisions and D1 review, November outstanding development and usable access, December component testing, January live testing and UNICEF sign-off, February deployment/training/handover. Exact dates and feasibility require owner confirmation; no extension is approved here.

UNICEF review is within five working days of submission. Allow time for corrections and further review before final acceptance by 28 February. The original August/Week 4 access requirement is distinct from the later end-November access assumption. Neither is verified access evidence.

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

- [Draft D1 Inception Report](../01_inception/DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO.md)
- [Inception Completion Inventory](../01_inception/INCEPTION_COMPLETION_INVENTORY.md)
- [Original 14-week implementation notes](../07_source_documents/planning_presentations/FOURTEEN_WEEK_IMPLEMENTATION_SLIDE_NOTES.md)
- [Two-week project checklist](OPENCHS_PRIMERO_TWO_WEEK_PROJECT_CHECKLIST.md)

The contract-aligned plan should be used for commercial dates and milestone reporting. The technical notes and checklists remain supporting evidence and must not override the contract schedule without approval.

## Contract obligations and unresolved differences

Source: [owner-supplied contract planning extract](../07_source_documents/TICAD_2026_001_USER_SUPPLIED_CONTRACT_PLANNING_EXTRACT.md). No monetary amounts are reproduced in this plan.

- UNICEF executes contractual user-testing sign-off in January; Ministry leads testing under Session 3. The named signatory and Ministry endorsement remain to be confirmed.
- Weekly progress meetings; minutes within 24 hours; monthly reports on the last working day. Use UNICEF templates and plan electronic plus hard-copy submission unless clarified otherwise.
- February training in Maseru includes English/Sesotho materials as agreed and attendance registers. Handover includes technical guidance, manuals, administrator guide and completed Service Provider assessment form.
- Two in-country trips are specified: July/August inception and February training/handover. Do not record the earlier trip as completed without evidence. Confirm staffing against the two-person core team and shared quality assurance arrangement.
- Free maintenance lasts 90 days after launch. Confirm actual dates and administration beyond the February delivery period.
- Obtain official ABR check-digit rules and at least 10 valid examples. Optional ABR entry does not waive these requirements.
- Confirm data-sharing agreements and authority before deployment using real cases.
- Contract identity, Week 14 wording, access-date differences, selected-checkbox/save behaviour, additional two-way scope, submission formats and proposed fault waivers require written reconciliation. The report records CD-01–CD-12.
- Written acceptance precedes invoicing; existing payment conditions remain. No signed acceptance, deployment, test completion or schedule extension is claimed.
