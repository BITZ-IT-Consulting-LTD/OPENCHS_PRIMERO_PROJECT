# Section 5 revision record — D1 v2.8 Post-Validation

**Report:** [D1_INCEPTION_REPORT_OPENCHS_PRIMERO_V2.8_POST_VALIDATION.md](D1_INCEPTION_REPORT_OPENCHS_PRIMERO_V2.8_POST_VALIDATION.md), Section 5 (Business requirements and workflow)
**Scope of edit:** Section 5 only, in the Markdown file. The Word file has not been changed.
**Governing input:** Section 5 business-validation decisions BR-001–BR-010, cited in the report as [RV5].
**Status:** Revised draft. Not an approval record.

> **Note on BR numbering.** The editing brief confirmed BR-001–BR-010 but did not list the text of each decision. The numbering below was derived from the brief's validated rules and must be confirmed by the report owner before circulation.

## Deliverable 1 — Revised Section 5

This is in the report itself. It has subsections 5.1–5.4, Tables 5.1–5.3, and three closing subsections under 5.4: acceptance traceability, change log, and quality assurance.

## Deliverable 2 — Decision implementation matrix

| BR | Decision | Section 5 location | Requirement / decision IDs |
|---|---|---|---|
| BR-001 | Manual, explicit, confirmed referral; saving never sends | Table 5.1 stages 1–2; Table 5.2 manual initiation and confirmation rows; 5.3 referral initiation; Table 5.3 row WF-002 / FN-003 | D-006; WF-002; FN-003 |
| BR-002 | CPIMS+ destination, then Ministry-approved service dropdown; no caseworker selection | Table 5.1 stage 2; Table 5.2 destination and service row; 5.2 destination and service selection; Table 5.3 rows RT-001, RT-002 | D-008; RT-001 / A-018, RT-002; FN-006 |
| BR-003 | Narrative at referral; flexible child identity without fabrication; reporter anonymity; optional ABR with structural checks and audited mismatch override | Table 5.1 stage 3; Table 5.2 narrative, child identity, anonymity and ABR rows; Table 5.3 | D-005, D-010, D-011, D-013, D-014; FN-001, FN-002, FN-004, FN-005; DATA-005, DATA-008 |
| BR-004 | Approved emergency reduced dataset; parallel telephone escalation independent of the API | Table 5.1 stage 3 and the paragraph after it; Table 5.2 emergency rows; 5.3 emergency and partial referrals | D-003; WF-004, WF-007 |
| BR-005 | Authorised partial referrals; completion via Send Update | Table 5.1 stages 3 and 7; Table 5.2 partial referral row; 5.3 emergency and partial referrals | WF-005; FN-009 |
| BR-006 | Supervisor consultation optional and recorded; mandatory only under an approved SOP | Table 5.1 stage 2; Table 5.2; 5.3 supervisor consultation | WF-003 |
| BR-007 | Ministry controls acceptance, rejection, distribution and assignment | Table 5.1 stages 5–6; 5.2 Ministry business decisions | D-016; RT-002–RT-005 |
| BR-008 | Separate technical states (Queued, Sending, Delivered, Failed, Needs Action) and business states (Pending, Accepted, Rejected, Ongoing, Closed) | Table 5.1 stages 4–5; 5.2 technical and business statuses; 5.3 submission feedback | RT-005, RT-006; FN-007, FN-008; DATA-013 |
| BR-009 | Explicit Send Update against the linked UUID; automatic inbound retrieval deferred | Table 5.1 stage 7; 5.3 outbound follow-up updates; Table 5.3 rows FN-009, FN-010, RT-007 | FN-009, FN-010; RT-007; API-003; D-007, D-012 (historical) |
| BR-010 | Controlled corrections, cancellation and withdrawal; justified, linked re-referral; prank handled as a corrective update | Table 5.1 stage 8; 5.3 corrections and case-lifecycle requests | WF-006, WF-010 |

## Deliverable 3 — Cross-reference correction log

None of these corrections has been made. Line numbers refer to the Markdown file after the Section 12 edit. Each correction is minimal.

| # | Location | Current text (abridged) | Conflict | Proposed minimal correction |
|---|---|---|---|---|
| 1 | Section 2.1, Figure 1 table, row "Status visibility" (line 436) | "returned human decisions, progress and interventions require approved scope…" | Doesn't separate the initial outbound display from future inbound updates | Append: "Initially, OPENCHS shows technical states and only verified business statuses from an authorised source (section 5.2)." |
| 2 | Section 7.3, "Anonymous reporters" row (formerly line 1417) | — | **Resolved by the Section 7 revision.** Section 7.3 was replaced by the security-control baseline, and anonymity now covers follow-up updates rather than "return updates" (section 7.6). Annex K.2.3 still has the old wording; see Section 6 record item K-11 | — |
| 3 | Annex A, RT-006 row (line 3245) | Title "Intermediate status vocabulary" | Doesn't name the technical-state set | Append to **Current**: "Gateway technical states Queued, Sending, Delivered, Failed and Needs Action are separate (section 5.2)." |
| 4 | Annex A, WF-003 (line 3232) and Annex J, WF-003 (line 3875) | "Supervisor escalation is optional…" | BR-006 uses "consultation" and requires it to be recorded | Append to **Current**: "Consultation is recorded when used; mandatory approval only where an approved safeguarding SOP requires it." Keep the historical wording unchanged |
| 5 | Annex D.1, items 2, 7 and 8 (lines 3496–3508) | Shorter lifecycle wording; item 8 begins with "Closure" | Item 8 suggests OPENCHS-driven closure; it omits the prank and re-referral rules and the CPIMS+ destination step | Replace items 1–8 with a pointer to Table 5.1, or align item 8 to: "Correction, withdrawal and cancellation requests and justified, linked re-referral preserve linkage and audit history; prank findings never automatically close the CPIMS+ case (WF-006, WF-010)." |
| 6 | Annex D.3, Figure 15 (line 3525) | "queued / sending / technically received / failed / action required" | Different labels from section 5.2 | Change to "Queued / Sending / Delivered / Failed / Needs Action" |
| 7 | Annex H, B-03 (line 3712) | "Agent escalates to supervisor before referral" | Should be optional consultation | Retitle "Optional supervisor consultation recorded before referral"; keep the ID |
| 8 | Annex H, F-11 (line 3728) | "Distinct Received, Accepted / Rejected states" | "Received" isn't a defined state | Replace "Received" with "Delivered (technical)" |
| 9 | Annex H, F-18 (line 3735) | "Helpline sees acceptance and progress" | Implies progress is returned automatically | Qualify: "…only where verified through an authorised source; no automatic progress retrieval." The Initial note already says this; align the expected-result column |
| 10 | Annex H, new scenarios | — | Section 5.4 scenarios 2, 5, 10 and 20 have no Annex H ID | Add: CPIMS+ destination selection; invalid or inactive service blocked; partial referral with later completion (conditional); negative test for the absence of automatic inbound synchronisation |
| 11 | Annex I.1 source register | [RV3], [RV4] and [RV5] are not listed (and PO-01–PO-07 are not listed either) | Citations are undefined in the register | Add entries for RV3, RV4 and RV5 using the in-section definitions |
| 12 | Annex E | BR-001–BR-010 are not recorded | Traceability | Optionally add "E.4 Section 5 business-validation decisions — BR-001–BR-010", modelled on E.3 |
| 13 | Header and footer (Word source) | Header: "Version 2.8"; footer: "Version 2.8 — pending formal approval"; the Markdown title block says "Version 2.8 — Post-Validation Revision · 9 November 2026" | Inconsistent version labels | **Flag only:** reconcile at document-control level. No label has been chosen |

I checked these with no conflict found: section 3.3 (outbound follow-up row), section 4.3–4.7, section 6.4 (retry and reconciliation), section 7.4 (Figure 5 and the status row), Annex J FN-007 to FN-010 and RT-007.

## Deliverable 4 — Outstanding approvals and technical dependencies

**Ministry policy and safeguarding approvals**
- Emergency minimum dataset and exception authority (WF-004), including any emergency narrative exception (FN-004)
- Minimum child-identification field combinations (FN-005, DATA-005)
- Partial-referral minimum fields and completion procedure (WF-005)
- Any SOP-mandated supervisor approval cases (WF-003)
- Approved service catalogue, codes, owner and change process (RT-001 / A-018)
- Routing, recipient roles, rejection reasons and assignment permissions (RT-003)
- Correction, withdrawal, cancellation, re-referral and prank-disposition rules (WF-006, WF-010)
- Lawful basis, consent override authority and the effect of withdrawal on information already sent (DATA-012, SEC-001)
- ABR override roles and the official NICR specification (FN-002)
- Reporter disclosure rules (DATA-008)
- Endorsement of the business status labels (RT-006)

**Primero API and platform verification**
- UUID return and retrieval, duplicate-query and ambiguous-create reconciliation semantics (DATA-013, OPS-003)
- Supported update, correction, withdrawal and cancellation operations, with payloads and permissions (FN-009, WF-006, API-003)
- Mapping from native statuses to the five business labels (RT-006)
- Mandatory fields compatible with the emergency and partial datasets (WF-004, WF-005)
- Validation of the retry intervals (OPS-002)
- Representation of an anonymous reporter (WF-009)
- Service and recipient configuration (RT-002, RT-003)

**BITZ implementation and testing**
- Explicit referral control with a confirmation summary and duplicate prevention (FN-003)
- Service dropdown that blocks invalid or inactive services (FN-006)
- Validation messages (FN-012)
- Gateway idempotency, linkage table and reconciliation (DATA-013, OPS-003)
- Retry, alerting and controlled manual retry (OPS-002, AUD-001)
- The Send Update operation (FN-009)
- Separate technical and business status display, with "not confirmed" handling (FN-007, FN-008)
- Negative payload tests for the case plan and attachments (FN-011)
- Annex H alignment and the four new scenarios (Deliverable 3, items 7–10)

**Child Helpline operational and UAT dependencies**
- Authorised agent and supervisor roles
- Agent procedures for referral, partial completion, prank correction and re-referral
- Emergency escalation contacts, training and the B-02 exercise
- Business UAT participation and endorsement of results

**Future addendum (not initial go-live dependencies)**
- Automatic inbound status and intervention retrieval, including polling, webhooks and subscriptions (FN-010, RT-007, RT-008, SEC-008)
- Electronic attachment transfer (DATA-010; SCOPE-003)
- Direct electronic routing to external providers (RT-004)

## Deliverable 5 — Quality-assurance checklist

| Check | Result |
|---|---|
| All ten BR decisions reflected | Yes. See Deliverable 2; the BR numbering needs owner confirmation |
| Initial outbound-only scope respected; exclusions stated | Yes. Section 5 introduction and 5.3 excluded functionality |
| D-007 and D-012 kept as historical decisions and qualified, not deleted | Yes |
| Technical and business status terminology separate and consistent within Section 5 | Yes. Annex D.3 and H F-11 still need alignment (Deliverable 3) |
| Delivered never implies Accepted | Yes. Stated in Table 5.1 stages 4–5, 5.2 and 5.3 |
| Duplicate prevention and ambiguous-create reconciliation addressed | Yes. Stage 4 and 5.3 duplicate prevention and recovery |
| Retry policy consistent with OPS-002 and section 6.4 | Yes (1, 5, 30 and 120 minutes; four retries after the initial attempt) |
| Emergency telephone escalation preserved and independent of the API | Yes |
| Supervisor consultation optional, with no universal gate | Yes |
| Prank finding never auto-closes; withdrawal never auto-changes the Ministry status | Yes |
| No unverified Primero capability, dataset, catalogue, approver, date, endpoint, mapping or test result presented as approved | Yes. No row is classified "Verified and approved" |
| Section numbering 5–5.4 and Table numbering 5.1–5.3 preserved | Yes. The Contents anchors are unchanged |
| Requirement and decision IDs keep their historical meanings | Yes. Annex J classification remains the controlled record |
| Edits limited to Section 5 | Yes. Cross-references are logged, not edited |
| Header/footer version inconsistency flagged | Yes. Deliverable 3, item 13 |
