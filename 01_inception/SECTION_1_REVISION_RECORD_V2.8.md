# Section 1 revision record — D1 v2.8 Post-Validation

**Report:** [D1_INCEPTION_REPORT_OPENCHS_PRIMERO_V2.8_POST_VALIDATION.md](D1_INCEPTION_REPORT_OPENCHS_PRIMERO_V2.8_POST_VALIDATION.md), Section 1 (Executive summary)
**Scope of edit:** Section 1 only, in the Markdown file. The Word file has not been changed.
**Governing input:** the Section 1 master editing prompt, cited in the report as [RV1]. The report owner's decision of 9 November 2026 that the final architecture is BITZ's own integration gateway is applied.
**Status:** Revised draft. Not an approval record. Line numbers refer to the Markdown file after the Section 1 edit (Section 1 runs from line 248 to line 491).

## Deliverable 1 — Revised Section 1

This is in the report:

- the [RV1] introduction;
- sections 1.1 to 1.9, with Tables 1.3a and 1.3b and the tables in 1.4, 1.6, 1.7 and 1.8;
- a change log and a QA note at the end.

The nine subsection headings and their numbering are unchanged, so all contents links still work.

**What was kept unchanged:**

- **Table 1.3a** is the previous 1.3 table word for word. Its "System connection" row is restored to the wording recorded at [M4], as the historical record.
- **The six-row [M4] action table in 1.9** is kept. The only additions are the meeting set-up owners and the recorded sign-off parties.
- **The A-020 removal note.**
- **The [M4] facts that were already recorded:** the access target of 13 November, not committed by Primero; the confirmed approvers; the working timetable dates of 5, 12 and 26 February 2027.

## Deliverable 2 — Section 1 change-control matrix

| Subsection | Original position | Revision | Evidence / reference | Approval implication |
|---|---|---|---|---|
| Introduction | None | States that [RV1] is an editorial validation input and that the summary adds no new requirement | [RV1] | None; editorial |
| 1.1 | Purpose and the [M4] paragraphs | Adds a nine-point list of what the report establishes. States that D1 does not establish development, testing, UAT or deployment. Distinguishes the signed titles from the technical requirements. States that no due dates are inferred (CD-15). Flags the inconsistent version labels without changing them | [CT2]; sections 2.6, 2.7; Table 12.5 | Editorial clarification. The version label needs a decision by the report owner |
| 1.2 | Eleven-row source register | Adds a source-type column. Adds [DPA1] and [DMP1]. States that [DP] is not a source of due dates. Removes the words "and amounts" from the [CT2] row; no amount appears anywhere. Flags that [RV1]–[RV12] and [SOP1] are missing from Annex I.1 | Annex I.1 | Editorial. Annex I needs a correction (C1-07) |
| 1.3 | One requirements table | The table is kept as historical Table 1.3a. New Table 1.3b gives the current baseline, the disposition of each historical decision and the outstanding approval. D-007, D-012 (attachments) and D-015 are preserved with their dispositions. Two [M4] discrepancies are flagged and not resolved | TECH-001; SCOPE-002; [M4 sections 5, 6] | **A change to the technical baseline is presented** (outbound-only; attachments excluded; gateway). The contractual disposition of D-007 and the attachments remains outstanding (CD-01, CD-04) |
| 1.4 | Eleven matters in three columns | Twelve matters, in the categories the brief requires, each with reference, responsible party, evidence, impact and verified status. Records the [M4] test-data position beside the Section 10 requirement | Sections 6.7, 7.5, 8.7, 9.3, 12.2 | No status is upgraded; none is closed |
| 1.5 | Outbound first, with inbound updates and attachments described as "subsequent functionality". Retries "proposed". "Direct API versus OpenFN" left to review | Adds the eight-step lifecycle, the gateway responsibilities and the exclusions. Retries are proposed parameters, recorded at [M4] as validated in discussion and not contractual. Inbound updates and attachments are no longer presented as planned later phases. The gateway is stated as the selected architecture | Sections 6.2–6.7; TECH-001, TECH-004; [CT2 item 70] | **A change to the technical baseline is presented.** Removing "subsequent functionality" needs UNICEF's scope disposition to become contractual (decision 8) |
| 1.6 | Three narrative paragraphs | A six-dimension table using the defined status terms. No percentages. Readiness for review is separated from readiness for acceptance | Table 12.5; section 8.6 | Editorial; no readiness is claimed |
| 1.7 | Six narrative risks | Nine risk areas mapped to the risk, action and decision IDs. Realised issues are separated (IS-01 to IS-05). All 17 risks remain Open — not reverified | Tables 11.1a, 11.1b, 11.3 | None. No rating or status is changed |
| 1.8 | Nine decisions | A twelve-decision matrix in priority order, with each row mapped to the original decision number. Decision 6 is narrowed to technical confirmation. Decision 8 is split into controllers and hosting | [M4 C1]; CD-09, CD-12, CD-15, CD-16, CD-17; AP-01 to AP-08 | Changes how the decisions are presented. **Narrowing decision 6 reflects the report owner's position, not a decision by the [M4] decision owners** |
| 1.9 | Six [M4] actions and a list of follow-ups | Keeps the actions. Adds the four dependency chains, the other follow-ups listed as *proposed* next steps, and the later gates in order. Lerato Mokuena is added as a sign-off party, as recorded at [M4 C3 N-15] | Section 12.2; [M4 C3, C6] | None. No recovery schedule is approved |

## Deliverable 3 — Outstanding verification and approval matrix

No completion or approval is inferred.

| Reference | Matter | Current evidenced position | Required verification | Responsible authority | Impact |
|---|---|---|---|---|---|
| A-015, A-016, DSR-15 | Lesotho test environment | Not ready on 4 Nov; target 13 Nov, not committed | Completed checklist; authorised test exchange | Primero; UNICEF | G2; D3 |
| A-023, API-002, R-013 | Integration authentication | JWT required by the contract; credentials not supplied | Authenticated test call; renewal mechanism | Primero; BITZ | G2 |
| AP-02; [M4] decision 6 | Technical confirmation of the BITZ gateway interface | Gateway is the report owner's final position; Primero and Ministry IT have recorded no confirmation | Written technical confirmation after the 10 Nov meeting | Primero technical team; Ministry IT | G2, G3 |
| A-018, RT-001 | CPIMS+ service list and receiving configuration | Agreed in principle; no date | Approved list and codes | Primero; Ministry | D2; G2 |
| P-02, CD-06 | Field mapping | Not verified on the Lesotho schema | Mapping verified on the Lesotho environment | Ministry; Primero | G2; D3 |
| A-007, CD-05 | ABR verification rules | Official rules not received | Specification and examples | Ministry / relevant authority | D2 acceptance |
| DSR-01 to DSR-05, DSR-08 to DSR-10, DSR-12 | Data protection and processing | The Act and the draft policy have been received; no approval | Written decisions and agreements | Ministry; UNICEF | Production go/no-go |
| DSR-06, DSR-07 | Minimum child dataset and emergency exceptions | Minimum recorded at [M4]; emergency fields not itemised | Approved datasets | Ministry; Child Helpline | D2; UAT |
| CD-01, CD-04, P-01, R-010 | Disposition of D-007 (two-way) and attachments | No written disposition | Written scope decision | UNICEF; Ministry | D3, D4 acceptance |
| [M4 section 5]; BR-008 | Status-label set | [M4] agreed eight labels; Section 5.2 uses different ones | Ministry confirmation of one set | Ministry; Child Helpline | D2 status display; UAT |
| [M4 section 5] | Rejection feedback to the helpline | Required at [M4]; no mechanism in the outbound-only design | Agreed mechanism or written disposition | Ministry; UNICEF; Primero | Safeguarding; D2 to D4 |
| A-021, OPS-003 | Interruption handling and retries | Proposal recorded; not validated with Primero | RC-01 to RC-04 results | Primero (technical) | G4 |
| DSR-11, UAT-003 | Synthetic test dataset | [M4]: approved during testing; Section 10: approval before use | Approved dataset; agreed timing | Ministry | Integration testing |
| D-018, R-016 | Evidential use of the global demonstration system | Undecided | Written acceptance basis | UNICEF with Primero | G4 |
| CD-09, CD-12 | UAT signatory; fault thresholds | Tiisetso Mohlabi proposed; thresholds recorded as agreed at [M4] but not reconciled with [CT2 section 4] | Written nomination; written reconciliation | Ministry; UNICEF | G5; D4 |
| AP-01; [M4 C2] | D1 approvers | Rantsala Sanaha and Nelson Adagi recorded as confirmed; Ministry and Primero names pending | Written nominations | Ministry; Primero; UNICEF | G1 |
| CD-15, CD-16, CD-17, CD-07 | Due dates, end date, late submission and timetable | Working baseline agreed at [M4]; not a contract amendment | Written UNICEF confirmation | UNICEF | All deliverables |

## Deliverable 4 — Cross-section consistency findings

These findings are the remaining contradictions between the revised Section 1 and the rest of the report. None was corrected in this edit, because each one sits outside Section 1.

| # | Severity | Location | Finding | Proposed correction |
|---|---|---|---|---|
| C1-01 | High | Section 5.2, Ministry business states (line 1125); Annex A RT-006, FN-007; Annex D.3 (line 3632) | Status labels: [M4] agreed Queued, Received, Accepted, Rejected, In progress, Completed, Withdrawn and Needs action. The body uses two different label sets. This is audit finding CON-002 | The Ministry and Child Helpline confirm one set. Then align Section 5.2, Annex A, Annex D.3 and Annex H F-11 to it |
| C1-02 | High | Sections 5.2, 5.3 and 6; [M4 section 5] | Rejection feedback: [M4] requires a CPIMS+ rejection to reach the helpline, and no initial mechanism is defined. This is audit finding CON-003 | Decide the route (for example a manual Ministry notification procedure, or a scoped inbound status read) and record it in Sections 5 and 6, or record a written disposition |
| C1-03 | High | Document control (line 32); Word header and footer; Table 12.5 | Version labels are inconsistent. This is audit finding CON-004 | The report owner fixes one label and rebuilds the Word file from the Markdown |
| C1-04 | Medium | Section 12, Table 12.2 (lines 3117–3118); section 9.3 | Rantsala Sanaha and Nelson Adagi are shown as "nominees … to confirm", while [M4 C2] records both as "Confirmed today" and Section 1.4 now follows the minutes | Record both as confirmed at [M4] (draft minutes), with written confirmation of authority still to be obtained where [CT2] requires it |
| C1-05 | Medium | Sections 9.3 and 12.1 approver tables | Lerato Mokuena is recorded in [M4 C3 N-15] as a D1 sign-off party and is now named in Section 1.9, but appears nowhere else | Add Lerato Mokuena to Table 12.2 with role and department "to confirm", as [M4] records |
| C1-06 | Medium | Section 8.7 (line 2090); Section 10 DSR-11 (line 1716) | [M4] recorded test data as "approved during testing"; the body requires approval before use | Keep the safeguarding requirement for approval before any use, and record the [M4] position as a difference that the Ministry has to resolve |
| C1-07 | Medium | Annex I.1 (line 3910) | [RV1]–[RV12] and [SOP1] are cited but not registered | Add an Annex I entry for the validation instructions and one for [SOP1] |
| C1-08 | Medium | Section 2.8 CD-01 (line 636); section 4.2 (line 917) | CD-01 still reads "Formal contract variation required: inbound updates". That implies inbound updates are planned for a variation, whereas Section 1.5 now states they are excluded from the initial design and not planned as later phases | Reword the CD-01 treatment so that any inbound capability needs a separately approved scope decision. Keep the historical wording |
| C1-09 | Medium | Section 6 TECH-004 (lines 1336, 1478) | Section 6 describes the retry intervals as "validated"; Section 1.5 calls them proposed parameters, validated in discussion at [M4] | Add "validated as design parameters; not formally approved; not a contractual service level" to Section 6 |
| C1-10 | Low | Section 3 change log (line 862) | Says Sections 1–2 still carry the earlier OpenFN and synchronisation wording. Section 1 is now revised; Section 2 has been harmonised for OpenFN only | Update the log entry when Section 2 is next revised |
| C1-11 | Low | Section 2 (2.1 Figure 1 table; 2.6 D3) | The "inbound synchronisation and attachment exchange are not unconditional D3 obligations" wording is compatible with Section 1 but weaker | Optional alignment with the Section 1.5 exclusion wording |
| C1-12 | Low | Earlier section records (open-corrections table in the Section 12 record) | About 60 corrections to Sections 2–4 and the annexes remain open. The ones for Section 1 (N-1 to N-5 in the Section 6 record; M-1 to M-3 in the Section 7 record) are now resolved by this revision | Mark them resolved in those records |

**Checked and consistent:**

- **Architecture:** the gateway and the absence of OpenFN are stated the same way in Sections 1, 2.2, 3, 4, 6 to 12 and Annexes A, E, J and K, after the edit earlier today.
- **Risk register:** all 17 risks and their statuses match Table 11.1a and Annex G.
- **Actions:** the four dependency chains match the dependency sequencing in Section 12.2.
- **Gates:** G1 to G5 and the production go/no-go match section 8.7.
- **Decision references:** CD-09, CD-12, CD-15, CD-16 and CD-17 match section 2.8.
- **Safeguarding requirements:** DSR-01 to DSR-18 match Table 7.4.
- **Proposed dates:** 5, 12 and 26 February 2027 match section 8.7.

## Final quality checklist

- [x] Sections 1.1–1.9 complete; numbering and anchors unchanged
- [x] Contract and deliverable references accurate (item 50; Amendment 3; 15 Sep 2026); no contract amounts
- [ ] Source references match Annex I: two gaps flagged (C1-07)
- [x] Historical inception decisions preserved (Table 1.3a; D-007, D-012, D-015)
- [x] Subsequent technical dispositions traceable (Table 1.3b)
- [x] Outbound Create Referral and Send Update described consistently
- [x] Primero UUID persistence explicit (1.5 steps 6–7)
- [x] Automatic inbound synchronisation not presented as initial scope
- [x] Attachment and middleware exclusions qualified (scope disposition outstanding)
- [x] Referral routing and Ministry authority clear
- [x] Child safeguarding requirements explicit; real-data exchange not authorised
- [x] API and environment readiness claims evidence-based
- [x] Technical receipt distinguished from human acceptance (six events)
- [x] UAT and contractual acceptance separate
- [x] Original project dates traceable; proposed dates not described as approved
- [x] Principal risks match Section 11
- [x] Outstanding actions match Section 12
- [x] All decision references valid
- [x] No invented approvals or completion statuses
- [ ] Consistent with the full report: status labels, rejection route and version label remain (C1-01 to C1-03)

## Update — precedence of the 9 November revisions over [M4]

The report owner confirmed that the section revisions made on 9 November 2026 update the draft [M4] minutes, which record a facilitated discussion. Section 1 was aligned accordingly:

- a precedence statement was added to the introduction;
- the 1.3 "discrepancies" note now reads "Positions updated since [M4]";
- in 1.4, the approvers are named at [M4] with written confirmation pending, and the test data must be approved before use;
- in 1.5, the retries are described as validated design parameters;
- in 1.6, no role's authority is yet confirmed in writing;
- the status-label follow-up was removed from 1.9.

| Finding | New position |
|---|---|
| C1-01 Status labels | **Resolved.** The section 5.2 vocabulary is current. Annex D.3 and Annex H F-11 alignment remains (audit CON-018, CON-019) |
| C1-02 Rejection feedback | **Medium; open.** No inbound feed is built. The Ministry is to confirm the operational route for communicating rejections |
| C1-03 Version label | Open (High) |
| C1-04 Approver framing | **Resolved.** Section 1 now follows Table 12.2 |
| C1-05 Lerato Mokuena | **Low.** Named in 1.9 as an [M4] sign-off party. The report owner decides whether to list her in Table 12.2 |
| C1-06 Test-data timing | **Resolved.** Approval before use stands |
| C1-09 Retry wording | **Resolved.** Section 1 now matches Section 6 |
| C1-07, C1-08, C1-10 to C1-12 | Unchanged |

