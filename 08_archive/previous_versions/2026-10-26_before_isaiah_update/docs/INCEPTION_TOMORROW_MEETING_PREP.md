# OpenCHS–Primero CPIMS+ Integration
## Inception Follow-up Meeting Preparation

**Meeting date:** 14 October 2026  
**Purpose:** Close the highest-priority inception decisions and confirm the evidence, owners and dates required for D1 approval  
**Status:** Draft meeting pack  
**Prepared from:** Session 1 and Session 2 minutes, D1 inception report, completion inventory and Workstream 1 templates

## 1. Meeting objective

By the end of the meeting, the team should either:

1. approve the decision;
2. assign a named owner and due date;
3. defer the item from the accelerated MVP; or
4. escalate the item as a project blocker.

No item should remain as a general discussion without an owner, date and status.

## 2. Decisions that must be prioritised

| Priority | Decision required | Current position | Required meeting outcome |
|---|---|---|---|
| Critical | Referral trigger | Current direction is manual and initiated by the handling agent; escalation, approval and exceptions are open | Approve trigger, authorised role, escalation and exception rules |
| Critical | CPIMS+ routing | Session 2 indicates service/referral-target selection, with Ministry-side distribution | Approve service targets, accept/reject flow, district supervisor/manager distribution and non-Ministry routing |
| Critical | Minimum identification and anonymous reports | CPIMS+ may require identifying information; exceptions are unresolved | Approve minimum identifying dataset, safe refusal/exception process and operator message |
| Critical | Primero sandbox and API access | Critical-path dependency; access package and date remain unconfirmed | Confirm checklist status, blockers, owners, committed date and fallback plan |
| Critical | ABR ID | Optional/non-blocking direction recorded; authority, format and validation remain open | Confirm owner, rule, examples, validation and later-update process |
| High | Field mapping | CPIMS+ required field list and protection-concern vocabulary remain pending | Assign field owners and agree date for signed mapping/API response |
| High | Status and follow-up updates | OpenCHS follow-up updates supported in principle; intermediate statuses and inbound write-back unresolved | Approve status model, update direction, mechanism and privacy limits |
| High | UAT and acceptance | Ministry-led UAT direction recorded; individual testers and sign-off authority not named | Confirm people, test data, scenarios, signatories and defect rules |

## 3. Suggested agenda

| Time | Topic | Output |
|---|---|---|
| 10 min | Welcome, purpose and status review | Confirm that the meeting is decision/action focused |
| 15 min | Sandbox/API readiness | Access status, blockers, owners, date and fallback decision |
| 15 min | Referral trigger and emergency workflow | Approved manual trigger, escalation, minimum dataset and anonymous handling |
| 15 min | CPIMS+ routing and acceptance | Service targets, accept/reject, Ministry distribution and status visibility |
| 10 min | ABR and field mapping | ABR owner/rule and field-mapping owners/dates |
| 10 min | Follow-up updates, audit and support | Status model, update mechanism, audit minimum and support owner |
| 10 min | UAT, training and sign-off | Named testers, signatories, test data and readiness criteria |
| 5 min | Review actions and close | Every pending item has owner, due date and evidence |

**Suggested total:** 90 minutes. If time is limited, protect the four Critical decisions first.

## 4. Questions to ask and capture

### 4.1 Referral trigger and emergency handling

- Is the referral always manually initiated by the handling agent?
- Which role may trigger, cancel, correct or re-refer?
- When is supervisor escalation required?
- What minimum information is required for an urgent referral?
- Which fields may be completed later, by whom and by when?
- What happens if the report is anonymous or lacks the identifying information required by CPIMS+?
- What user message and escalation path should appear when a referral cannot be transmitted?

**Template:** [02 Referral Lifecycle Capture](<../Inception Meeting /temeplate forms/02_referral_lifecycle_capture.docx>)

### 4.2 Routing and CPIMS+ acceptance

- What service/referral targets will OpenCHS present to the handling agent?
- Does OpenCHS select a service only, or can it select a district supervisor/manager?
- Who accepts or rejects the referral in CPIMS+?
- What information is returned for rejection and correction?
- Who distributes an accepted case to a caseworker?
- How are police, courts and other approved stakeholders handled?
- Which statuses must Child Helpline users see between referral and closure?

**Templates:** [02 Referral Lifecycle Capture](<../Inception Meeting /temeplate forms/02_referral_lifecycle_capture.docx>), [06 API Contract Capture](<../Inception Meeting /temeplate forms/06_api_contract_capture.docx>)

### 4.3 ABR and field mapping

- What is the official ABR definition and issuing authority?
- Is blank ABR formally permitted for both case creation and referral?
- What are the valid format, length, uniqueness and validation rules?
- How is an ABR added or corrected after referral?
- Which CPIMS+ protection-concern values correspond to OpenCHS categories?
- Which child, reporter and perpetrator fields are mandatory, optional or excluded?
- Is the OpenCHS case plan excluded from the shared payload?

**Templates:** [03 ABR ID Requirements](<../Inception Meeting /temeplate forms/03_abr_id_requirements.docx>), [04 Field-Mapping Worksheet](<../Inception Meeting /temeplate forms/04_field_mapping_worksheet.docx>)

### 4.4 API, sandbox and technical readiness

- Has the readiness checklist been completed? If not, what remains?
- Who owns each blocker and what is the committed completion date?
- What are the sandbox URL, token endpoint, referral endpoint and follow-up endpoint?
- What JWT claims, scopes, expiry and credential-rotation rules apply?
- What are the success, validation-error, rejection and timeout responses?
- What evidence can be produced from a successful connectivity test?
- If sandbox access is delayed, is a mock/contract-test fallback approved?

**Templates:** [05 API / Environment Matrix](<../Inception Meeting /temeplate forms/05_api_environment_matrix.docx>), [06 API Contract Capture](<../Inception Meeting /temeplate forms/06_api_contract_capture.docx>), [13 Sandbox Risk Record](<../Inception Meeting /temeplate forms/13_workstream_1_risk_record_primero_sandbox.docx>)

### 4.5 UAT and acceptance

- Who are the named Ministry, Child Helpline, technical and district testers?
- Who is the business sign-off authority and who is the technical sign-off authority?
- Is safe test data available and approved?
- Which scenarios are mandatory before go-live?
- What is a critical defect?
- Can a conditional go-live occur with an approved workaround?
- Where will request/response, status and audit evidence be stored?

**Template:** [08 UAT and Acceptance Matrix](<../Inception Meeting /temeplate forms/08_uat_acceptance_matrix.docx>)

## 5. Evidence to request during the meeting

Do not close an item on verbal agreement alone where documentary evidence is required. Request or record:

- approved workflow/SOP or named approver and due date;
- completed sandbox-readiness checklist;
- sandbox URL and secure access arrangement;
- API specification, sample request/response and error catalogue;
- approved ABR rules and valid/invalid examples;
- signed field-mapping worksheet;
- approved service/referral target and routing matrix;
- agreed status and follow-up update model;
- named UAT testers, signatories and safe test-data approval;
- security/data-sharing owner and review date;
- support, incident and escalation contacts.

## 6. Live decision and action log

Complete this table during the meeting. Do not leave owner or due date blank.

| ID | Decision/action | Status: Resolved / Pending / Deferred | Owner | Due date | Evidence / template location |
|---|---|---|---|---|---|
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |

## 7. Close-out test before ending the meeting

- ☐ Every critical decision has a status.
- ☐ Every pending item has one named owner.
- ☐ Every pending item has a due date.
- ☐ Every resolved item has evidence or a recorded approval.
- ☐ Every deferred item has a scope boundary and change-control route.
- ☐ Sandbox/API blockers and fallback arrangements are recorded.
- ☐ UAT participants and sign-off authority are named.
- ☐ The D1 report, completion inventory and registers have the same decisions and IDs.

## 8. Documents to have open

- [D1 Inception Report](DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO.md)
- [Inception Completion Inventory](INCEPTION_COMPLETION_INVENTORY.md)
- [Stakeholder / Responsibility Matrix](<../Inception Meeting /temeplate forms/01_stakeholder_responsibility_matrix.docx>)
- [Decision Register](<../Inception Meeting /temeplate forms/09_decision_register.docx>)
- [Action Register](<../Inception Meeting /temeplate forms/10_action_register.docx>)
- [Open Issues Register](<../Inception Meeting /temeplate forms/11_open_issues_register.docx>)
- [Inception Close-out Checklist](<../Inception Meeting /temeplate forms/12_inception_closeout_checklist.docx>)
