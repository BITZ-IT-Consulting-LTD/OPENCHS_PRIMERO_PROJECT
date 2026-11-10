# Section 10 revision record — D1 v2.8 Post-Validation

**Report:** [D1_INCEPTION_REPORT_OPENCHS_PRIMERO_V2.8_POST_VALIDATION.md](D1_INCEPTION_REPORT_OPENCHS_PRIMERO_V2.8_POST_VALIDATION.md), Section 10 (Testing and acceptance)
**Scope of edit:** Section 10 only, in the Markdown file. The Word file has not been changed.
**Governing input:** Section 10 testing-and-acceptance validation decisions TST-001–TST-007, cited in the report as [RV10].
**Status:** Revised draft. Not an approval record. Line numbers refer to the Markdown file after the Section 12 edit.

> **Matter for the report owner — deliverable descriptions.** The brief summarised D2 as "applicable design and implementation", D3 as "integration and testing" and D4 as "training and handover". The signed items and section 2.6 define them as:
>
> - **D2 (item 60):** ABR ID field, checks and referral control
> - **D3 (item 70):** outbound REST API client
> - **D4 (item 80):** testing, UAT, training and go-live
>
> Section 10 uses the signed descriptions and does not redefine contractual scope.

## Where each output is

| Brief output | Location in the report |
|---|---|
| 1 — Revised Section 10 | Sections 10.1–10.7, ending with the change log and QA note |
| 2 — Testing framework | Table 10.1 (six categories, levels, environments, evidence levels) and the test evidence matrix |
| 3 — UAT framework | Section 10.2 table, scope reconciliation of Annex H, and Figure 11 |
| 4 — Defect procedure | Section 10.3: severities, register, lifecycle and exceptions |
| 5 — Acceptance criteria matrix | Table 10.4 (AC-01 to AC-09 original; AC-10 to AC-18 added) |
| 6 — Training and handover | Table 10.5 (three tracks), exercises, handover package and evidence |
| 7 — Evidence register | Table 10.6 (EV-01 to EV-07) |
| 8 — D1 readiness assessment | Historical table (unchanged) and Table 10.7 register |
| 9 — Figures | Figure 11 redrawn as an editable diagram. Figure 12 kept as the historical 27 Oct snapshot, with the current gate position shown in text |
| 10 — Change and consistency report | This file |

## Output 10 — Change and consistency report

### Changes made

1. **Test levels.** The six source categories are mapped to unit, simulated, Lesotho integration, security and safeguarding, regression and UAT levels. Each is tied to the section 8.6 evidence levels. Mock results are labelled preliminary; the global demonstration environment is preliminary only.
2. **UAT.** The source table is expanded with preparation, functional and recovery scope, evidence fields and sign-off contents. Excluded Annex H scenarios are marked for scope reconciliation.
3. **Defects.** Severity examples are aligned to Create Referral and Send Update. The register fields, lifecycle and written-exception content are added.
4. **Acceptance criteria.** The nine originals are kept with their thresholds, and nine traceable criteria are added. AC-05's "transmissions and return updates" is replaced by the validated operation set, with the 100% threshold unchanged. AC-08 (RT-007) is kept as Pending Confirmation and marked as future scope only.
5. **Training.** Three role-based tracks, practical exercises, handover-package additions and training evidence. "Returned updates" is removed from operator training.
6. **Evidence.** Seven evidence packages with explicit evidence statuses. Conditional acceptance is not assumed to be available under [CT2].
7. **D1 readiness.** A register with five classifications is added beside the unchanged historical table. The current gate position is stated separately from Figure 12.

### Historical information preserved

- All six test categories.
- The source participant groups, with the Child Helpline supervisor still Pending Confirmation.
- The four severities and their go-live rules.
- The nine criteria and their proposed thresholds.
- The [CT2 section 4] statements.
- Item 80, [CT2 section 2.5.4], the February 2027 proposal, the English and Sesotho materials and the source handover materials.
- D-009, UAT-002, SEC-007, CD-09, Annex H and Annex J.8.
- The ten-area historical D1 table, unchanged.
- Figure 12 (27 Oct 2026) and the unlabelled inventory chart.
- The historical counts: 19 Resolved, 44 Pending, 8 Deferred.
- The historical assessment conclusion: ready for stakeholder review, not accepted.

### Outstanding approval decisions

- Approval of every proposed threshold (AC-01 to AC-18).
- The UAT signatory (CD-09) and named testers (UAT-002).
- The synthetic dataset (DSR-11).
- The competency threshold for training.
- Training dates, travel and languages (section 8.8, decision 8).
- Whether any alternative to the Lesotho environment is an authorised acceptance basis (section 8.8, decision 7).
- The Ministry approvers for D1 (AP-01).

### Unresolved test and environment dependencies

- Lesotho environment access, credentials, field IDs, code lists and service catalogue (G2: A-015, A-016, A-018, A-023).
- Supported Send Update operations (FN-009).
- Primero reconciliation and idempotency behaviour (OPS-003).
- Retry validation (A-021).
- The security approver (DSR-12).

### Contractual acceptance issues

- Whether [CT2] permits conditional acceptance.
- How the late-submission clause applies (CD-17).
- Undated integration deliverables (CD-15).
- The contract end date (CD-16).
- Waivers of High defects need UNICEF's written agreement [CT2 section 4].

### Cross-references updated in the earlier records

- Marked resolved: S8-3, S8-4 and S8-5 (Section 8 record) and S9-1 and S9-2 (Section 9 record).
- Marked no change needed: M-13 (Section 7 record) and N-16 (Section 6 record). Annex H already labels F-12, F-15, S-04, S-07, RC-05 and RC-07 as future scope, excluded from initial UAT.

### Cross-document corrections still needed (not made)

| # | Location | Conflict | Proposed minimal correction |
|---|---|---|---|
| S10-1 | Annex H, F-11 (line 3728) | Expected result "Distinct Received, Accepted / Rejected states" | Replace "Received" with "Delivered (technical)". This is the same item as Section 5 record item 8 |
| S10-2 | Annex H, B-03 (line 3712) | Titled "escalates" | Retitle as optional supervisor consultation. This is the same item as Section 5 record item 7 |
| S10-3 | Annex H (new scenarios) | Sections 5.4, 6.7 and 7.6 list scenarios marked *new* with no Annex H ID | Add IDs for: destination selection; invalid service blocked; partial referral and completion; no-inbound negative test; confirmation-cancel; failed update without a new case; technical status display; unresolved-transaction alert; Lesotho readiness; lawful-basis recording; encryption at rest; secrets; environment isolation; retention |
| S10-4 | Annex H.6 coverage table (line 3771 onward) | Maps decisions to scenarios but not to AC-01 to AC-18 | Optionally add an AC column |
| S10-5 | Annex J.8 (line 4060 onward) | Requirement-level statuses | Check that UAT-004 and UAT-007 match AC-01 and AC-02 as proposed thresholds. No status change |
| S10-6 | Section 11.1, R-016 and 11.5, item 1 | — | **Resolved in Section 11 by the Section 11 revision.** See S8-7 and S8-8 | — |
| S10-7 | Section 11.2 | — | **Resolved in Section 11 by the Section 11 revision.** See S9-3 | — |
| S10-8 | D1_ACCEPTANCE_READINESS.md (linked from 10.7) | An external file last updated 28 Oct | Refresh against Table 10.7 when it is next revised |

**Consistency with Sections 5–9 (checked):**

- **Section 5:** manual initiation (AC-10), Send Update (AC-12), optional ABR and validation (AC-07), emergency handling (AC-16) and disclosure (AC-17).
- **Section 6:** gateway, UUID, idempotency, retry, reconciliation and audit (AC-03 to AC-05, AC-11 to AC-14; Table 10.1).
- **Section 7:** synthetic data, minimisation, access controls and incident escalation (Table 10.1 security row; AC-06, AC-15 to AC-17; EV-03).
- **Section 8:** D1–D4, G1–G5, evidence levels and the proposed timetable (Tables 10.1, 10.6 and 10.7).
- **Section 9:** RACI rows 11, 13, 21, 23 and 26; AP-04, AP-05, AP-07 and AP-08; the Critical escalation route.

**Optional:**

- O-1: Add [RV10] to Annex I.1.
- O-2: **Version labels (flag only).** The Word header says "Version 2.8", the Word footer says "Version 2.8 — pending formal approval", and the Markdown title block says "Version 2.8 — Post-Validation Revision · 9 November 2026". No new version number has been assigned.

### Remaining risks

- G2 is not met, so no Level 3 evidence is possible yet. Every acceptance criterion except AC-08 depends on it.
- No UAT signatory, security approver or Ministry D1 approver has been named (R-014).
- If conditional acceptance is not permitted under [CT2], D1 acceptance may require every P-class item in Table 10.7 to be closed.

## Final acceptance checklist

- [x] TST-001 to TST-007 implemented; Sections 10.1–10.7 complete
- [x] Six test categories retained; mock and Lesotho evidence distinguished
- [x] Create Referral and Send Update tested; automatic inbound synchronisation excluded
- [x] Ministry-led UAT preserved; Annex H reconciled (excluded scenarios marked); synthetic data controls included
- [x] Four severities; zero open Critical; High exceptions need written approval
- [x] Nine original criteria retained; RT-007 Pending Confirmation; duplicate prevention and reconciliation testable
- [x] D4 contractual training preserved; three tracks; training and handover evidence specified
- [x] UAT, contractual acceptance and go/no-go separate
- [x] Ten D1 areas retained; 19/44/8 retained; Figure 12 date retained; D1 and later-stage items distinguished
- [x] No unsupported completion or approval claims
- [ ] Annex H additions and Section 11 alignment: see S10-1 to S10-7
