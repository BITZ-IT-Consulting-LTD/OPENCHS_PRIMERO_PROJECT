# Session 3 facilitation notes

## Lesotho Child Helpline 116 and OpenCHS integration with Primero CPIMS

**Meeting date:** 26 October 2026\
**Facilitator:** Nelson Adagi\
**Purpose:** Final inception requirements and decision meeting\
**Proposed duration:** 120 minutes; start time and time zone to confirm\
**Status:** Draft facilitation pack; all Session 3 decisions and attendance await the meeting

### What we need to leave with

An agreed account of the referral journey, minimum data, integration boundaries, responsibilities and acceptance approach, together with the evidence and dated actions needed to finish the inception report. The final requirements meeting can authorise circulation of an updated draft; formal inception acceptance still depends on its stated approval and evidence requirements.

### Opening words

“We have prefilled the information already provided in Sessions 1 and 2 and Isaiah’s response. Please correct any factual error as we review it. We will focus today on the unresolved details, approvals and delivery evidence needed to finish the inception report, and read back each new decision with its owner and date.”

### Running order

| Elapsed time | Discussion | Required output |
|---|---|---|
| 0–10 min | Attendance, authority and previous actions | Named decision owners; locate shared workflow/form |
| 10–20 min | Recap and reconcile Sessions 1 and 2 | Confirm the working baseline and disputed points |
| 20–45 min | Child journey, referral trigger and routing | Approved workflow and emergency/anonymous handling |
| 45–60 min | Minimum data, privacy and ABR | Data decisions and remaining mapping inputs |
| 60–80 min | API, authentication and environments | Technical decisions, access package and dates |
| 80–90 min | Updates, failures, duplicates and audit | Agreed operating requirements and evidence owners |
| 90–105 min | UAT, responsibilities and delivery | Acceptance plan, signatories and dependency treatment |
| 105–120 min | Read back decisions and report close-out | Dated actions, report review route and closure assessment |

### Facilitation rule

Start with **Already provided** in each topic; ask for corrections, not a repeat of the answer. **Recorded decision** means stated in the minutes; **Provided** means supplied information; **Working assumption** still needs the named confirmation. Address **What remains to resolve**, then record the new outcome as **Confirmed today**, **Pending** or **Deferred**, with person, date and evidence. A provided answer is not automatically approval or live-access evidence.

---

## 1 What we covered in Sessions 1 and 2

Use the Session 1 and Session 2 minutes supplied by Nelson as the meeting records. Carry forward Session 1’s recorded business decisions, apply Session 2’s routing revision and qualifications, and settle the remaining detail. Both records remain Draft for review and correction.

| Topic | Session 1 on 8 October | Session 2 on 9 October and implication for today |
|---|---|---|
| Case intake and referral trigger | OpenCHS demonstrated. Manual referral by the handling agent recorded, not supervisor-only; escalation optional. Emergency phone contact continues alongside referral. | Manual initiation remains the recorded business baseline. Session 2 qualifies the final rule: ratify it and settle the UI event, permissions, validation and exceptions. |
| Referral routing | PDF envisages direct district/stakeholder referral. | CPIMS+ demonstration shows service-based referral and Ministry-side distribution; technical confirmation remains pending. Do not assume individual caseworker selection. |
| Referral data and privacy | Recorded payload includes child bio-data, category, narrative, reporter contact and perpetrator details. Settle field-level requiredness and safe unknown-value handling. | Mapping worksheet started. Protection concerns may be multi-select. Final fields, codes, requiredness and safe sharing remain to be approved. |
| Anonymous reports and case plans | Minimum-information referrals and the broader case workflow discussed. | Summary sounds definitive, but detailed sections qualify identifying-information requirements and separate case plans as matters for confirmation. Decide the minimum dataset and explicit case-plan boundary. |
| ABR identifier | Add an optional ABR field; blank must not block case creation/referral. Validation mechanism deferred; official rules not established. | Definition, authority, format, validation, requiredness and later update remain pending. Approve the business rule and identify the official source. |
| Updates and evidence | Recorded OpenCHS changes, closure and prank re-flags are follow-up pushes to the existing case. Inbound CPIMS+ status feedback was not committed. | Intermediate statuses, duplicate handling and audit requirements explored; final mechanisms, ownership, retention and recovery remain pending. |
| Ownership and access | Focal person, SOP/form sharing and sandbox checklist actions identified. | Technical roles clarified. Sandbox and signatories still outstanding. Action register records workflow and referral-form sharing as completed; locate and validate the versions today. |

### Differences the facilitator must resolve

- **Trigger:** carry forward Session 1 section 6’s manual handling-agent decision. Session 2 sections 1/3 and D-006 qualify the final rule. Ratify the baseline and close its remaining details; do not reopen automatic category-based referral without an explicit change decision. The inventory’s WF-002 label alone is not approval evidence.
- **Anonymous reports and case plans:** use the qualifications in Session 2 page 6 rather than treating its executive summary as final policy. A child may be unknown while a reporter is known, or vice versa; distinguish these situations.
- **Shared documents:** Session 1 assigns SOP sharing to Hopolang and the unified referral form to Isaiah. Session 2 marks workflow and form sharing completed. Verify the versions and approval status; do not infer that sharing the workflow also completed the separate SOP action.
- **Schedule:** meeting references to a remaining 14-week window are historical. Use the current contract-aligned plan; any revised dates need governance approval.

**Evidence:** Session 1 PDF pages 3–8; Session 2 PDF pages 3–10. Direct links are provided on the final page.

---

## 2 Carry forward the Session 2 actions

Use the Session 2 register to open today’s action review. The statuses below are what the 9 October minutes record; they are not evidence that later actions have since been completed. Confirm progress with the owner today.

| Session 2 action and recorded status | Recorded owner | Session 3 follow-up |
|---|---|---|
| A-001 Participant list — Completed | Hopolang | Retain the supplied list. Record today’s attendance and authority separately. |
| A-002 Child Helpline focal person — Pending | Hopolang | Confirm the appointed person, role, contact and any backup. Mary Damposi was only a possible contact. |
| A-003 Referral workflow/process shared — Completed | Tiisetso, subject to confirmation | Locate the shared workflow version; confirm approval and custodian. Check Hopolang’s separate SOP-sharing action. |
| A-004 Referral form shared — Completed | Isaiah Ososti, as recorded | Open the shared form and confirm its version and approval status; use it for the minimum-data discussion. |
| A-005 Form review and field requiredness — Pending | Project team | Agree minimum, mandatory, optional and follow-up fields, with mapping/privacy approval owners. |
| A-006 ABR assistance and validation contact — Pending | Hopolang | Name the relevant authority/contact and the date for official evidence; Home Affairs was suggested, not confirmed. |
| A-007 ABR business and validation rules — Pending | Ministry / relevant authority | Settle the missing-ID rule, ownership and later updates; identify any unresolved official format/validation evidence. |
| A-008 CPIMS+ recipients and routing — Pending | Ministry / CPIMS+ stakeholders | Confirm service targets, district-level receiving role, acceptance/rejection and Ministry distribution with Primero. |
| A-09 Feedback statuses and update mechanism — Pending | Ministry / CPIMS+ / Child Helpline | Agree status meanings, owner, source and mechanism; distinguish the need for feedback from an approved inbound integration scope. |
| A-010 Demo/sandbox and API access — Pending; expected within one week | UNICEF Lesotho / technical teams | API reference is now provided by Isaiah; demo/alternative proposed. Resolve the access package, setup inputs and committed date; do not request the documentation link again. |
| A-011 UAT participation, data and sign-off — Pending | Ministry / Child Helpline / technical teams | Ministry-led UAT and participating agency roles are recorded. Fill the remaining names, signatories, dataset approval and expected evidence. |
| A-012 UNICEF participation/approval route — Pending | UNICEF / project governance | Confirm the authorised representative/delegate and approval route. Do not carry the old Tuesday availability statement forward as a current commitment. |

**Read back:** “Which previously Pending actions are now evidenced as complete? Which remain open, who owns each one and by what date? Do any prevent inception approval?”

Completed sharing actions do not establish that the workflow or form is approved or mapped to the configured API. The register heading mentions A-001–A-013, but the supplied entries end at A-012 and show the feedback item as A-09. Retain those source references; do not invent a missing action.

**Other Session 1 carryovers:** check Hopolang’s SOP, Peter’s ABR/manual-referral form work, Marlon’s Gateway/documentation work and Nelson’s UNICEF escalation. Record progress and evidence without assuming build completion.

**Reconciliation rule:** retain Session 1’s recorded business direction; resolve Session 2’s explicit qualifications on the trigger, routing, identity requirements, case plans, audit and mapping through the decision prompts below.

---

## 3 Preparation and the child journey walkthrough

### Confirm before substantive discussion

**Already provided — roles:** Nelson coordinates the project; Peter leads OpenCHS case-flow development; Marlon leads the Gateway; Hopolang coordinates locally; Isaiah is the Primero technical contact; Tiisetso is the Ministry coordinating partner. These are recorded roles, not assumed approval powers.

**Still needed:** today’s attendance/delegation, appointed Child Helpline focal person, and named business, security and sign-off authorities. Mary Damposi is only a possible focal contact.

Ask someone to screen-share the current SOP, referral workflow and unified referral form. Confirm file location, version, approval status and custodian. Open the field mapping, environment matrix and live decision/action registers. Nominate a note-taker and display the decision log throughout.

### Use one child journey with four variations

Use fictional people and identifiers. This is a requirements walkthrough; it does not count as a passed integration test.

**Journey A  Standard referral.** An agent records a child-protection concern and elects to refer it. Trace the exact user action, minimum validation, service target, API operation, technical response, Ministry acceptance/rejection and subsequent distribution. Confirm what the Child Helpline actually sees.

**Journey B  Emergency with missing information.** The child needs urgent help; ABR and some identifying details are unavailable. Confirm what can be saved, what can be transmitted, what must be escalated, who receives the phone call, and who collects missing information by when. Do not equate a missing ABR with an entirely unidentified child.

**Journey C  Unknown child or anonymous reporter.** Separate a known child with an anonymous reporter from a report that does not identify the child. Confirm the CPIMS+ threshold and a safe operational path when registration/referral cannot proceed. Do not invent placeholder identities to pass validation.

**Journey D  Later change or uncertain delivery.** New information, a later ABR or a prank re-flag arrives after referral; alternatively, the send times out or is double-clicked. Confirm the original reference, correction/update permissions and reconciliation before another create request.

### Ask at every step

1. Who acts, and what event starts this step?
2. What information is essential now, and what may follow later?
3. Which system owns the record, decision and visible status?
4. What happens if it fails, is rejected or the owner is unavailable?
5. What evidence will show that the agreed behaviour works?

**Capture:** [02 Referral Lifecycle](../../04_templates/02_referral_lifecycle_capture.docx), [04 Field Mapping](../../04_templates/04_field_mapping_worksheet.docx), [08 UAT Matrix](../../04_templates/08_uat_acceptance_matrix.docx).

---

## 4 Decisions on workflow routing and minimum data

### S3 01 Finalise the recorded manual referral workflow

**Already provided — Session 1 recorded decisions:** the handling agent manually triggers referral; it is not automatic or supervisor-only. Escalation is available. Urgent cases retain the direct police/first-responder phone call alongside system referral. OpenCHS integrates with CPIMS+; direct Home Affairs/X-Road work is separate.

**Already provided — Session 2 demonstration and working routing model:** the receiving UI selects Internal/External referral type, service, referral reason and expected outcome. Acceptance/rejection is separate from assigning a caseworker. Ministry supervisors/managers distribute internally; the helpline does not need individual-assignment visibility. Direct district selection/API capability and non-Ministry account configuration still need confirmation. Headquarters reporting staff are not the proposed case-management target.

**What remains to resolve — Ministry/Child Helpline, Isaiah, Peter and Marlon:**

- Which explicit UI event implements the recorded manual decision: referral checkbox plus Save, Refer action or another event? Approve permissions and escalation/exception rules; identify what must not send a referral.
- Confirm the actual configured service and receiving role, whether district selection is exposed, and the available non-Ministry pathway. Agree the create/update/referral sequence and returned reference.
- Define the evidence/message for technical delivery versus business acceptance, rejection and later allocation.

**Capture:** “Manual handling-agent referral remains the baseline. The exact send event is ___; exceptions follow ___; configured target/receiving role is ___; acceptance is evidenced by ___.” Record the technical confirmation still outstanding. Use template 02 and D1 sections 5–8.

### S3 02 Complete the field rules around the supplied data groups

**Already provided — Session 1 payload groups:** child name, age, sex, nationality, location and contact details; case category; narrative; reporter contact; and perpetrator details. Reporter contact supports follow-up where the child has no phone; broader reporter identity was not identified as required. Perpetrator information was retained because it affects risk and intervention; the exact CP-module target was not settled.

**Already provided — Session 2:** OpenCHS categories map to multi-select Protection Concerns. A standard Lesotho list is to be supplied. Separate case plans are the working position, qualified in the detailed minutes. The current MVP defers media/recordings and case-plan synchronisation; discussion of attachments did not approve their transfer.

**What remains to resolve — business/privacy owners and technical teams:** mark each field minimum, conditional, optional or later follow-up; settle child-identification/anonymous and emergency exceptions, unknown perpetrator values, consent/legal basis and access/redaction rules. Confirm the case-plan boundary. Obtain configured target fields, codes and transformations when available; do not substitute example values.

**Capture:** an annotated form/mapping with supplied groups retained, exact requiredness and missing-information owner/dates. Use [04 Field Mapping](../../04_templates/04_field_mapping_worksheet.docx); D1 sections 10/13. Inventory: WF-001–009, RT-001–005, DATA-005–011.

---

## 5 Decisions on ABR follow up and status visibility

### S3 03 Complete the ABR rules

**Already provided — recorded business direction:** Session 1 describes ABR as the child’s birth-registration number and records an optional field: case creation/referral can proceed blank. A supplied value should eventually be validated; the mechanism was not designed. Session 2 retains a non-blocking working position while qualifying formal requiredness, authority and validation. Isaiah says the rules need to be defined with the use case.

**What remains to resolve — Ministry, Hopolang, relevant authority and Isaiah:**

- Confirm the official identifier name, issuing authority, target field and evidence source; the Session 1 description is not an official format specification.
- Ratify the optional/non-blocking rule. Decide what an invalid supplied value does: warn, require review or block transmission, including the emergency exception.
- Supply official format/uniqueness/validation evidence and approved fictional examples. Define who adds/corrects a later ABR, how it links to the original case and how it is audited.

**Capture:** “ABR is recorded where available; the blank-ID rule is ___. Official authority/source: ___. Invalid-value handling: ___. Later update owner/process: ___.” Do not invent a regex, checksum, `abr_id` target name or direct Home Affairs integration. Use [03 ABR Requirements](../../04_templates/03_abr_id_requirements.docx); D1 section 9; DATA-001–004.

### S3 04 Complete follow up and status handling

**Already provided — Session 1:** new OpenCHS information, closure and prank/hoax re-flags are follow-up pushes to the original CPIMS+ case, rather than fresh referrals. The agreed direction is OpenCHS to CPIMS+; reverse status flow was desirable but uncommitted. The current scope treats inbound status write-back as Deferred.

**Already provided — Session 2:** Child Helpline identified the gap between referred/accepted and closed and requested a small intermediate status set. Acceptance/rejection, assignment and closure mean different things; the helpline needs acceptance and service-completion information rather than individual caseworker assignment details. Final status names, ownership, mechanism and privacy rules remain pending.

**What remains to resolve — Child Helpline, Ministry and Isaiah:**

- Define the exact update events, fields, permissions and review rules implementing the recorded outbound follow-up direction.
- Approve the status vocabulary, source, update owner, frequency and disclosure limits. Distinguish local queue/delivery states from receiving-system progress.
- If no inbound API is included, agree an operational follow-up process and accountable contact. Any proposed automated inbound write-back needs explicit scope/impact approval.

**Capture:** retain outbound follow-up and the original case link; fill only event/payload, status source, owner, timing and scope decisions. Use templates 02/06/09; D1 sections 7/11; RT-005–008.

---

## 6 Decisions on the API authentication and test environment

### S3 05 Complete the provided API and environment information

**Already provided — documentation:** Isaiah supplied the [Primero API reference](https://github.com/primeroIMS/primero/blob/development_v2/app/controllers/api/README.md). The project’s documentation review records API v2 and these upstream paths: `POST /api/v2/tokens`, `POST /api/v2/cases`, `PATCH /api/v2/cases/:id` and `POST /api/v2/cases/:id/referrals`. These are documented references; Lesotho release, configuration and operation sequence remain unconfirmed. Case creation and referral are separate operations. Generic examples do not establish configured Lesotho payloads.

**Already provided — Isaiah’s environment/configuration response:** configure the demo for testing; if delayed, provide a primerodev.org site. SOPs, paper forms, use cases and referral pathways feed configuration. Field definitions and lookups follow demo setup. No existing interface specification is available; the teams must capture one from the agreed workflow. No actual URL, committed access date or credentials have been supplied in the response.

**What remains to resolve — Isaiah, country input owners and technical leads:**

1. Verify shared workflow/form versions and identify any missing SOP/pathway inputs, owners and dates.
2. Provide the actual release/configuration, base URL, demo delivery date, alternative-selection date and evidence of suitability for required tests/UAT.
3. Date the configured dictionary, lookup lists, representative payloads and mapping approval. Confirm the exact operation sequence and returned case/reference ID.

**Capture:** country inputs → configuration → dictionary/mapping validation → integration testing/UAT, with named hand-offs and dates. Documentation receipt is already recorded; R-001 stays open until access readiness is evidenced. Use [05 Environment Matrix](../../04_templates/05_api_environment_matrix.docx), [06 API Contract](../../04_templates/06_api_contract_capture.docx) and [13 Sandbox Risk](../../04_templates/13_workstream_1_risk_record_primero_sandbox.docx).

### S3 06 Complete authentication and security details

**Already provided — Isaiah:** SSO preferred if an identity provider is available; username/password otherwise. Tokens expire after 60 minutes and the endpoint issues/reissues JWTs. The Primero team provisions credentials once ready. Security/network controls apply, but which controls was not specified. User-login preference does not settle unattended backend authentication.

**Documented reference:** the [token operation](https://github.com/primeroIMS/primero/blob/development_v2/app/controllers/api/v2/docs/tokens/post.md) describes bearer JWTs returned in the response Authorization header, issuance with credentials and reissue with a valid token. Deployment-specific expiry recovery remains to be agreed.

**What remains to resolve — Isaiah, identity/security owners and Marlon:** select the available identity/login setup and unattended backend flow; specify roles/permissions, renewal/expiry recovery, secure issuance/storage/rotation/revocation owners; identify the actual TLS/certificate, VPN, allowlisting or other prerequisites and connectivity-test evidence.

**Capture:** retain the 60-minute documented lifetime and Primero issuance responsibility; fill the selected flow, account scope, control list, owners and dates. Keep secrets out of the notes. D1 sections 8/11/13/15.

---

## 7 Decisions on reliability audit and acceptance

### S3 07 Complete failure recovery duplicate and audit requirements

**Already provided — Session 2:** duplicate scenarios include two agents handling the same caller and a double-click submission. Existing OpenCHS visibility and user review were discussed; no receiving-system duplicate guarantee was agreed. The minutes record one call centre, with any satellite as a VPN-connected extension; this does not establish the Primero network-access controls.

**Already provided — audit/performance:** proposed audit information includes case identifiers, timestamps, transaction results and related events. The CPIMS+ log example was Time / Performed By / Action / Description / Owner. Final fields, access and retention remain pending. Isaiah reports no API rate limits and proposes joint performance management; operation-specific errors are referenced in the documentation. Retry/reconciliation rules were not supplied.

**What remains to resolve — Peter, Marlon, Isaiah, operations and security:**

- Confirm an external reference that CPIMS+ can store/search and the reconciliation process after an uncertain create timeout. Decide how double-click and repeat-reporting scenarios are handled.
- Approve retry/manual-correction classes, queue retention/recovery, single retry controller, limits and authorised manual retry. The earlier retry intervals remain Proposed.
- Set operator-visible failure states, monitoring/escalation/support ownership and operating limits. Approve audit fields, redaction, access, retention and incident procedure.

**Capture:** requirements, accountable contacts and evidence needed for acceptance. Design requirements do not prove implementation. Use [07 Reliability and Support](../../04_templates/07_reliability_logging_support_controls.docx); D1 sections 12–14; OPS-001–007.

### S3 08 Complete the recorded UAT approach

**Already provided — Sessions 1–2:** Ministry-led UAT, involving Child Helpline agents, Ministry/CPIMS+ users and system administration, district supervisors, and OpenCHS developers Peter/Marlon; Isaiah provides Primero technical coordination. The Child Helpline focal appointment remains pending.

**Already provided — scenario coverage:** referral trigger, ABR present/missing, emergency minimum information, perpetrator details, Ministry/district routing and distribution, feedback, incomplete/rejected referrals, audit and access control. Isaiah recommends child-journey use cases and representatives of actively using agencies. His “any data” response does not supply privacy approval for real child records; synthetic data is the proposed default.

**What remains to resolve — Ministry/UAT lead and governance:** name testers, focal person and business/technical signatories; approve expected results, dataset/accounts/reset rules, defect thresholds and acceptance authority. Add proposed token-expiry, uncertain-timeout/duplicate and offline-recovery technical tests to the coverage where agreed. Do not request participating role categories again.

**Capture:** named people, approved scenario/data plan, evidence requirements and dates. Actual UAT execution, training, production/rollback evidence and go-live approval are later gates; agree their owners today. Use [08 UAT Matrix](../../04_templates/08_uat_acceptance_matrix.docx) and [01 Responsibility Matrix](../../04_templates/01_stakeholder_responsibility_matrix.docx); D1 section 16; UAT-001–009/GOV-001–003.

---

## 8 Decide whether the inception report can be completed

### S3 09 Confirm the report package review route and outstanding conditions

**Already provided — delivery/report baseline:** D1 is version 0.4. The contract-aligned plan records 1 July 2026–28 February 2027, with inception in August, ABR/referral form in October, outbound client in November, and testing/UAT/training/go-live in February. Earlier two-week/14-week references do not approve new dates.

**What remains to resolve:** actual milestone/acceptance status, dependency impacts, any authorised rebaseline, named report reviewers/approver, circulation date and response deadline. Review the matrix below; distinguish issuing the next Draft from formal inception acceptance.

| Required inception output | What must be captured today | Where it goes |
|---|---|---|
| Agreed scope and workflow | Trigger, authorised roles, routing, exceptions, system boundaries and deferred scope | D1 sections 5–8; lifecycle/decision register |
| Data and ABR baseline | Minimum dataset, approved sharing, case-plan boundary, ABR rule or explicit blocker; exact mapping gaps owned | D1 sections 9–10 and 13; mapping/ABR forms |
| Technical design and access | API sequence, selected authentication, environment inputs, security prerequisites and readiness evidence/actions | D1 sections 8, 11 and 15; API/environment forms |
| Reliability and operations | Queue/retry/reconciliation, audit, monitoring and support requirements with owners | D1 sections 12–14; reliability form |
| Acceptance approach | UAT scenarios, data, named signatories, defect rules and later training/go-live responsibilities | D1 section 16; UAT/responsibility forms |
| Delivery and dependencies | Named calendar dates, dependency impacts and any governance-approved rebaseline | D1 sections 17–19; contract-aligned plan |
| Report approval | Report owner, reviewers, circulation date, response deadline, approver and acceptance evidence | D1 sections 20–21; close-out checklist |

### Make one explicit closing assessment

**Ready to issue the next Draft:** the report accurately records today’s decisions; remaining assumptions, blockers, owners, dates and impacts are visible; the review route is agreed. Issuing this draft does not close an absent access, mapping or approval gate.

**Ready for formal inception acceptance:** authorised approvers confirm the required report, technical design, mapping baseline, environment evidence and applicable close-out conditions are satisfied. Record the acceptance and supporting evidence explicitly.

**Further closure required:** a critical business rule, authority, data-sharing decision, technical dependency or required evidence remains unresolved. Record it as Pending with its effect on report approval and implementation. A commitment to provide an item is not receipt of the item. Any conditional acceptance must identify the authorised approver, exact outstanding conditions, deadline and written decision; it must not be assumed to waive the existing gates.

**Schedule prompt:** confirm the status of the August inception milestone and the current October/November dependencies against the July 2026–February 2027 contract plan. Do not create a new two-week or 14-week commitment in this meeting without an approved rebaseline.

---

## 9 Live decision and action capture

### Decisions to read back before closing

Provided answers are prefilled in the discussion sections and the starting positions below. Record only the new Session 3 outcome, confirming person and authority in the blank columns; do not imply that the meeting has already approved them.

| ID | Provided starting position | Session 3 outcome and confirming person | Status |
|---|---|---|---|
| S3-01 | Recorded manual referral; routing details pending |  |  |
| S3-02 | Recorded data groups; minimum/exception rules pending |  |  |
| S3-03 | Optional ABR recorded; official rules pending |  |  |
| S3-04 | Outbound updates recorded; status mechanism pending |  |  |
| S3-05 | API reference received; configured access pending |  |  |
| S3-06 | 60-minute token documented; selected flow pending |  |  |
| S3-07 | Audit/performance direction given; controls pending |  |  |
| S3-08 | UAT roles/scenarios given; names/sign-off pending |  |  |
| S3-09 | D1 v0.4 Draft; review/acceptance route pending |  |  |

### Outstanding actions

Use real calendar dates and specify the time zone where a time is agreed. Add rows as needed; link the final record to the relevant template and inventory item.

| Action ID | Next action and required evidence | Named owner | Due date and dependency/approval impact |
|---|---|---|---|
| S3-A01 |  |  |  |
| S3-A02 |  |  |  |
| S3-A03 |  |  |  |
| S3-A04 |  |  |  |
| S3-A05 |  |  |  |
| S3-A06 |  |  |  |

**Recorded contacts:** Nelson, Peter, Marlon, Hopolang, Isaiah and Tiisetso have the roles listed in section 3. **Still capture:** today’s attendance/delegation, note-taker ___; Ministry/Child Helpline approval authority ___; security/privacy authority ___; inception approver/delegate ___; absences/escalation route ___.

---

## 10 Closing read back and report handover

### Closing words

“We have recorded the decisions confirmed today and the items still awaiting evidence. I will read back the remaining actions, their owners and dates. Please confirm whether we can issue the updated inception draft, who will review it, and what still prevents formal approval. The meeting record will distinguish today’s decisions from later implementation and test results.”

### Final check before ending the call

- Read back Session 1’s business decisions with Session 2’s revisions; record the confirming person. Finalise trigger details and exceptions rather than treating a general inventory label as approval.
- Confirm the workflow/SOP/form versions received or identify the retrieval/revision action. Note which document is authoritative and who approves changes.
- Read every open action aloud: person, date, evidence and effect on inception approval or delivery. Keep R-001 and other blockers open until evidenced.
- Confirm deferred scope, including inbound status write-back, case-plan synchronisation, media transfer and direct X-Road/Home Affairs integration unless formally changed.
- Record the selected report outcome, circulation date, reviewer response deadline and final approval route. Do not infer agreement from silence or absence.

### After the meeting

Nelson and the nominated note-taker should produce the Session 3 record, then update the capture templates, registers and workbook before reconciling the inventory and next D1 revision. Keep the current Draft and source minutes for traceability. Correct any inventory status contradicted by today’s confirmed evidence and recount the totals. The starting 7 Resolved / 53 Pending / 11 Deferred snapshot includes later delivery work and is not a vote on inception readiness.

### Source and capture links

- [Session 1 minutes](../session_1/SESSION_1_MINUTES.pdf): pages 3–6 workflow/data/ABR/routing; pages 8–9 actions and UAT.
- [Session 2 minutes](../session_2/SESSION_2_MINUTES.pdf): pages 3–5 qualifications/trigger/routing; pages 6–8 duplicates/anonymous/case plans/audit/ABR/mapping; pages 9–11 UAT/actions/risks.
- [Isaiah response source](../../06_correspondence/ISAIAH_RESPONSE_SOURCE_2026-10-26.md): recorded 26 October; response sent date not supplied.
- [D1 inception report v0.4](../../01_inception/DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO.md), [completion inventory](../../01_inception/INCEPTION_COMPLETION_INVENTORY.md) and [contract-aligned delivery plan](../../02_project_management/CONTRACT_ALIGNED_DELIVERY_PLAN.md).
- [Decision Register](../../04_templates/09_decision_register.docx), [Action Register](../../04_templates/10_action_register.docx), [Open Issues Register](../../04_templates/11_open_issues_register.docx), [Close-out Checklist](../../04_templates/12_inception_closeout_checklist.docx) and [capture workbook](../../04_templates/Workstream_1_Inception_Capture_Workbook.xlsx).

The questions, example states, timings and read-back wording in this pack are facilitation prompts. They are not recorded Session 3 decisions or evidence that access, testing or approval has occurred.
