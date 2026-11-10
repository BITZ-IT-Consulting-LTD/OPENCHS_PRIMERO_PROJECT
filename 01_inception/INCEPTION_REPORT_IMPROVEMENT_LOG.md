# Inception Report Improvement Log
## D1 v0.6 → v0.7

**Date:** 27 October 2026  
**Prepared by:** BITZ IT Consulting Ltd, OpenCHS project team  
**Source version:** [DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO.md](DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO.md) v0.6 (retained unchanged)  
**Revised version:** [DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO_V0.7.md](DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO_V0.7.md)

No Session 3 decision, decision ID, action ID or risk ID was changed or reopened. All v0.6 technical content was retained, either in the main body or in an annex (table at the end).

## 1 Improvements

| # | Original issue (v0.6) | Improvement made | Affected v0.7 section | Reason | Evidence / source | Remaining concern |
|---|---|---|---|---|---|---|
| 1 | No cover page; document control spread over header lines | Cover table, status classification legend with inventory mapping, version history, companion-output links | 1 | Formal deliverable presentation; consistent status vocabulary | Prompt §4.2; README filing rules | Word copy still at earlier version |
| 2 | Executive summary mixed technical API detail with status; no explicit decisions-required list or readiness verdict | Rewritten: background, activities, achievements, approach, readiness, top risks, decisions table, next steps, explicit circulation vs acceptance verdict | 2 | Executive readers need achieved / outstanding / to approve | Session 3 minutes; inventory | — |
| 3 | No project background or justification | Operational context, system roles table, intended-outcomes table (framed as intended, not proven) | 3 | Required for stakeholder understanding | Sessions 1–3; brief §1 | No baseline metrics exist to measure outcomes |
| 4 | Objectives were one paragraph | Overall objective, seven D1 specific objectives, expected result per deliverable | 4 | Traceability to brief §3 | Brief §§1, 3 | — |
| 5 | Contract context did not classify scope or list discrepancies systematically | Scope classification table (contractual / confirmed / extends contract / proposed / excluded) and contractual discrepancies CD-01–CD-07 | 5 | Prompt §4.3: do not absorb two-way into D3 | Brief; delivery plan; D-006, D-007, D-013, D-014 | CD-03 and CD-05 are newly identified; need governance view |
| 6 | Methodology implicit; session table lacked objectives, participants and outcomes; evidence gaps not consolidated | Methodology table; consultations table with evidence column; limitations subsection | 6 | Prompt Improvement 3; no unsupported consultation claims | Session minutes; email records | 24 Sep and 14 Oct meetings have no minutes |
| 7 | Requirements scattered across sections 6–18 without IDs, priority or acceptance | Eight categories with ID, source, proposed priority, status; full matrix with validation method in Annex A | 7; Annex A | Prompt Improvement 4; testability | Inventory IDs; Session minutes; brief | New IDs (FN, SEC, AUD, WF-010, DATA-012/013, OPS-008, UAT-010) need adding to the inventory; priorities are proposals |
| 8 | Architecture described only in a table | Diagrams A–D (context, sequence, technical, environment) plus implementation/dependency flow; all labelled Proposed; OpenFN, webhook and X-Road shown as options or separate | 8; 9.1 | Prompt Improvement 5 | Annex B; D-015; D-018 | Diagrams not yet validated by Primero |
| 9 | No implementation methodology | Twelve-phase table with objective, activities, outputs, responsibility, dependencies, completion criteria and D1–D4 mapping; supporting outputs marked proposed | 9 | Prompt Improvement 6 | Brief §§3–6; delivery plan | Responsibilities for approval roles remain TBC |
| 10 | Delivery section was narrative; no Gantt, no parallel-work list, no rebaseline decisions | Contract baseline Gantt with recorded events; status per deliverable; dependency table; parallel work while access pending; gate-based recovery sequencing (no invented dates); decisions for rebaseline | 10 | Prompt Improvement 7 | Delivery plan; Session 3 | No dated rebaseline possible until access and R-010 decision |
| 11 | Responsibilities table only; no RACI, approval mechanism, communication framework or escalation | Roles table; RACI with evidence column and TBC / proposed markers; approval mechanism table; proposed communication cadence; proposed escalation path | 11 | Prompt Improvement 8 | Session 3 actions; D-009; checklist; Isaiah response | Most Accountable entries remain TBC |
| 12 | Scope change discussed in several places (sections 1, 3, 20) | Dedicated section with all prompt-required aspects, change procedure and change log CR-01–CR-04 | 15 | Prompt Improvement 9 | Brief §9; D-007; D-012 | No effort estimate (deliberately not invented) |
| 13 | Risk register lacked probability, impact, owner and status columns; no review procedure | Priority risk table with proposed P/I; detailed register in Annex G with escalation triggers; review procedure; realised issues listed. Added R-013 (authentication), R-014 (approval delays), R-015 (save-event wording) | 14; Annex G | Prompt Improvement 10 | v0.6 R-001–R-012 preserved | P/I not formally assessed |
| 14 | Completion gates were narrative | D1 completion matrix separating document preparation, implementation evidence and formal acceptance | 16 | Prompt Improvement 11 | Delivery plan Item 10 gate | — |
| 15 | Privacy text not organised as controls | Legal position; 15-area control framework with status and owner; list of matters for UNICEF/Ministry confirmation | 12 | Prompt Improvement 12 | A-017; A-022; Annex B.6 | Legal instrument unconfirmed (2011 vs 2012 vs under development) |
| 16 | UAT section listed scenarios in one paragraph; no defect classes or thresholds | UAT approach table; test levels; defect classification; proposed measurable acceptance thresholds; Annex H matrix (B, F, S, RC, AU, RG series) with decision-coverage table | 13; Annex H | Prompt Improvement 13 | D-009; Session 2 UAT scope; brief §6 | Thresholds and severity rules need approval (UAT-007) |
| 17 | Action table did not distinguish overdue from future actions | Executive action table with Overdue / Due today / Pending / Awaiting dependency, plus decisions needed before design and before integration testing | 17 | Prompt Improvement 14 | Session 3 action tracker | Status reflects workspace evidence only; owners may have acted without filing |
| 18 | Earlier actions A-001–A-012 not shown | Annex F.2 shows last recorded status and successor treatment | Annex F | Traceability | Session 2 action register | A-004 referral form recorded Completed but not filed |
| 19 | Session 1 numbered decisions not cross-referenced to D-IDs | Annex E.2 maps Session 1 decisions 1–8 and marks decision 6 superseded | Annex E | Prevent superseded positions reappearing | Session 1 minutes | — |
| 20 | Source list did not identify missing sources | Annex I.2 lists twelve referenced-but-unavailable sources, including the contract itself | Annex I | Prompt §2 | Workspace inspection | Contract document not in workspace |
| 21 | Status vocabulary only described in prose | Annex D.3 proposed helpline state diagram mapped to upstream transition statuses | Annex D | RT-006 needs a concrete proposal | Primero v2.16.0 `transition.rb` | Pending Ministry/Child Helpline agreement |

## 2 Retention map (v0.6 → v0.7)

| v0.6 section | v0.7 location |
|---|---|
| 1 Executive summary | 2 (rewritten) |
| 2 Purpose and objectives | 4 |
| 3 Contract context | 5 |
| 4 Sources and evidence precedence | 6.4; Annex I |
| 5 Inception process | 6.2, 6.3 |
| 6 Current baseline | 2.3; 7 |
| 7 Scope | 5.2; 15 |
| 8 Referral lifecycle | Annex D.1, D.2; Diagram B |
| 9 Business rules | 7.1; Annex A.1 |
| 10 Technical architecture | 8.5 |
| 11 ABR | Annex C.2; FN-001/002 |
| 12 Fields and mapping | Annex C |
| 13 API and authentication | Annex B (complete) |
| 14 Reliability and audit | Diagram C; 7.6–7.7; Annex D.4 |
| 15 Data protection | 12 |
| 16 Responsibilities | 11.1 |
| 17 Environments | 8.6; Diagram D |
| 18 UAT | 13; Annex H |
| 19 Delivery plan | 10 |
| 20 Risk register | 14; Annex G |
| 21 Decisions and actions | Annexes E, F; 17.3 |
| 22 Completion gates | 16 |
| 23 Review and approval | 18 |

## 3 Verification performed

- Session 3 decisions D-005–D-018 checked against the minutes' decision log; wording preserved in Annex E.
- Primero claims in Annex B spot-checked against the local v2.16.0 source: `doc/api/cases/post.md` (204/409), `app/models/transition.rb` (statuses), `app/models/referral.rb` (consent check), `app/jobs/webhook_job.rb` (errors logged, no retry).
- All seven Mermaid diagrams rendered successfully with mermaid-cli.
- Annex H test IDs referenced in sections 13 and 15 and Annex A exist in Annex H.

## 4 Not changed

- The v0.6 file, the Word copy, the completion inventory, the action tracker and the delivery plan were not modified. The repository README and `inception.md` still describe v0.5 and should be updated when v0.7 is adopted.

## 5 Revision after review feedback (27 October 2026)

| # | Issue raised | Change made | Affected section |
|---|---|---|---|
| 22 | Executive summary read as a rewrite of the meeting notes; informal citations such as "notes from Isaiah" looked generic | Executive summary restructured to cite the minutes as the primary record rather than restate them. Added a basis-of-report table, and baseline and open-matter tables that cite minute sections and decision or action IDs. Introduced formal source codes ([M1]–[M3], [AT3], [TR1], [RC1], [RQ1], [TB], [DP], [PA], [CI], [R06]) in the Annex I source register. Replaced "Isaiah response" citations throughout with [TR1 §n] | 2; 6.1; 6.2; 7; 11.2; Annex A; Annex B.1; Annex I.1 |
| 23 | Report relied on prose and long lists in several sections; few visuals outside section 8 | Added a list of figures (§1.3) and new visuals. **Diagrams:** current vs target referral flow (Fig. 1), scope boundary (Fig. 2), inception timeline (Fig. 3), governance structure (Fig. 7), escalation path (Fig. 8), data flow (Fig. 9), UAT process (Fig. 10), change control flow (Fig. 12), position against delivery gates (Fig. 13). **Charts:** requirement status table and pie (Fig. 4); completion inventory pie (Fig. 13). **Tables:** current vs target comparison (§3.1), data sensitivity table (§12.3), risk heat map (Fig. 11), ABR ID position table (Fig. 14). Existing diagrams numbered as Figures 5, 6 and 15. Every figure cites its source or is labelled Proposed | 1.3; 3.1; 5.2; 6.2; 7; 11.1; 11.5; 12.3 (new; former 12.3 is now 12.4); 13.2; 14.1; 15.2; 16; Annex C.2 |

## Evidence corrections on 28 October 2026

Revised v0.7 using the newly filed Session 3 SOP, transcript and attendance export. Corrected A-014 receipt status, attendance and attribution; added Form 4 mapping/receipt and consent/UAT implications; retained applicability, configuration and approval gates. Updated the completion inventory, outstanding decisions and acceptance assessment. Previous v0.7 archived. Word regeneration remains outstanding because the required bundled document runtime/dependency loader is unavailable in this session; the existing Word file remains explicitly outdated.

## Version 0.8 exact structure on 28 October 2026

Main sections now follow the agreed twelve-section order exactly. Document control and contents are unnumbered. Objectives and contractual context are consolidated under section 2; consultation findings and the Session 3 evidence update under section 3; scope implications under section 4; business workflow under section 5; technical approach under section 6; data and safeguards under section 7; methodology and work plan under section 8; governance and change control under section 9; testing and D1 acceptance readiness under section 10; risks and outstanding decisions under section 11; approval and immediate actions under section 12.

The former section 7 detailed tables are preserved in Annex J, with concise narrative summaries in the main sections. Annexes A–I, all requirement/action/decision/risk identifiers and all Mermaid blocks remain. Internal references, the figure index, review companions and workspace entry links were updated. Earlier versions remain available. The Word copy remains outdated; this release is the Markdown review version. No approval or live validation is asserted.

## Version 0.9 plain-language review on 28 October 2026

Revised the main report for nontechnical Ministry, UNICEF and programme readers. Added an abbreviation guide; explained the referral process, failed delivery, information protection, responsibilities and tests in everyday terms. Preserved the exact 12-section order. Detailed technical design, diagrams and security specifications are retained in Annex K; Annexes A–J are unchanged. All coded requirements, actions, decisions and risks remain represented. Original v0.8 remains available. Word output is still outdated.

## Version 1.0 contract alignment on 28 October 2026

Recorded the owner-supplied TICAD-2026-001 contract as a planning extract, without representing it as signed. Revised the timetable to distinguish original monthly targets from a conditional recovery plan, with December component tests, January integration/user testing and UNICEF sign-off, and February deployment/training/handover. Added review, reporting, data-sharing, ABR specification, staffing/travel and 90-day support obligations. Expanded discrepancy register to CD-12 and aligned approval roles and companion documents. Retained the exact twelve-section order, plain-language approach and prior versions. No amounts added to report or plan; Word regeneration remains outstanding.

## Version 2.2 contract and minutes review on 29 October 2026

Reviewed v2.1 against the full TICAD-2026-001 contract text (filed at `07_source_documents/contract/`, signature blocks blank) and the Session 1–3 minutes. Word v2.2 and a tracked-changes copy against v2.1 produced; v2.1 retained unchanged.

| # | Finding | Change made | Affected section |
|---|---|---|---|
| 1 | Encrypted transport, retry schedule, token authentication, unique referral reference and offline queue are contract requirements, not proposals | Restated as contract requirements | 1.5; 7; Annex D.4; J (OPS-001, OPS-002, SEC-005); K |
| 2 | Contract specifies a username/password service account for JWT | Authentication no longer "undecided"; credentials and renewal remain outstanding | 1.4; 7; 11.1 R-013; 11.4; G; J API-002; K |
| 3 | Contract requires Primero field names and mappings in a central configuration file | Added as a requirement | 1.5; Annex C.3 |
| 4 | Contract allows an interim ABR rule updatable without redeployment | D-014 format check proposed as the interim rule | CD-05; R-005 |
| 5 | Contract answers most of A-021 (outages) | A-021 narrowed to Primero-side downtime | 1.4; 8.5; 11.1 R-004; 11.5 |
| 6 | Session 1 minutes record a 14-week plan with 8 Oct in week 2 | Contract week references anchored (Week 2: 5–11 Oct … Week 14: 28 Dec–3 Jan) | CD-07; 8.8 |
| 7 | Minutes show UNICEF-facilitated dependencies not available when due | New dependency table with minute citations | 8.5; 1.6; 1.7; 8.4; 11.3; R-009 |
| 8 | Contract requires sandbox testing for Deliverable 3.2; D-018 allows global playground | CD-13, R-016, decision 7 added | 1.8; 2.8; 8.8; 11.1; 11.5; G |
| 9 | Item 40 names UNICEF and the Primero team for user testing | CD-14 added; participants extended | 2.8; 8.8; 10.2 |
| 10 | Data-sharing agreements due September; not discussed in minutes | Explicit request to UNICEF | 1.9 |
| 11 | Contract says ABR validation should follow HMIS/EMIS patterns | HMIS/EMIS proposed as an alternative check-digit source | 8.5; R-005 |
| 12 | No weekly stand-up minutes or monthly reports located; Session 1–2 minutes still draft | Reporting record and remedial commitment added | 9.4 |
| 13 | Contract cites 43332327 as the earlier Lesotho contract; key-personnel substitution rules; CEO name | Recorded | Document control; 1.1; 1.2; 2.7; CD-02; 9.1; Annex I |
| 14 | "so-live" misspelling | Corrected to "go-live" (7 places) | 2.4; 2.7; 4; 10; 11 |

No session decision, requirement status from the minutes, or approval status was changed. Still outstanding: the signed contract, and confirmation of the inferred week anchor by UNICEF.

## Version 2.3 data protection review on 30 October 2026

Reviewed v2.2 against the Data Protection Act, 2011 (Act No. 5 of 2012) [DPA1] and the draft Data Management Policy v1.0 [DMP1], filed at `03_meetings/session_3/data protection /` and received 29 October 2026 under A-017. Word v2.3 and a tracked-changes copy against v2.2 produced; v2.2 retained unchanged.

| # | Finding | Change made | Affected section |
|---|---|---|---|
| 1 | The "2011" and "2012" references are the same Act (short title 2011, Act No. 5 of 2012, gazetted 22 Feb 2012) | Legal position rewritten; instrument identified; how the law applies is still for the Ministry and UNICEF to confirm | 1.2; 1.4; 3.5; 7.2; K.2.2 |
| 2 | The policy is a draft awaiting Cabinet approval and records that the Data Protection Commission was not yet established | Treated as policy direction, not a binding requirement; Commission status drives notification questions | 3.5; 7.2; 7.5 |
| 3 | Child data and health, sexual-life and criminal-behaviour data are sensitive (ss. 29, 34, 36); lawful grounds (s. 15) | Provisions listed; lawful-basis control and SEC-001 sources extended; 7.4 classification annotated | 7.2; 7.3; 7.4; J.5; K.2 |
| 4 | Processing contracts (ss. 21–22), transfers outside Lesotho (s. 52), notification of processing (ss. 25(5), 53); policy hosting direction (DMP 5.6.3, 5.6.7) | Three new control rows; 7.5 items 8–11; decision 8 (1.8); 11.4 item 8; new risk R-017 | 1.8; 7.3; 7.5; 11.1; 11.4; G; K.2 |
| 5 | Breach notification (s. 23); no prescribed retention periods (s. 19) | Incident-handling and retention controls extended; OPS-007 sources extended | 7.3; A; J.6; K.2.3 |
| 6 | A-017 partly received: Act and policy received; earlier Ministry data-protection work outstanding | Status updated in actions, work plan, risks R-007 and Annex I.2; [DPA1] and [DMP1] added to source registers | 1.4; 1.7; 1.9; 3.4; 3.5; 8; 11; F; I |

No session decision, requirement status or approval status was changed. New controls are tracked as Pending Confirmation against section 7.5 and R-017 rather than as new SEC requirement IDs, so the Figure 3 requirement counts (68) are unchanged; add SEC IDs at the next inventory update if wanted. The completion inventory (A-017 row) and outstanding decisions (OD-M4) have not been updated. The scanned Act is partly illegible (parts of ss. 34–35); section references should be checked against the official LesLII text. A PDF copy was not produced, because LibreOffice is not installed in this environment.

## Version 2.4 consultation record review on 30 October 2026

Checked section 3.2 against the Session 1–3 minutes and the Session 3 attendance export [ATT3]. Word v2.4 and a tracked-changes copy against v2.3 produced; v2.3 retained unchanged.

| # | Finding | Change made | Affected section |
|---|---|---|---|
| 1 | Session 3 row listed the Child Helpline as a participant; the minutes record that no helpline agent or social worker attended and a Child Protection Services representative spoke for it | Participants restated by organisation and name from [M3] and [ATT3]; helpline absence stated; format and duration added | 3.2 |
| 2 | Session 3 minutes omit Tiisetso Mohlabi, Lucy Mosesane, Likeleli Ramolapong and Ramoletane Lekhanya (all in [ATT3]); "Daniel" and Melusi are not in [ATT3] under those names | Shown as "per minutes", to be confirmed; limitation added | 3.2; 3.4 |
| 3 | Session 1 row called attendees "Child Helpline social workers"; the minutes do not record their organisations; Mary Damposi and Silepo spoke but are not listed | Roles listed as recorded, organisations marked not recorded; omission noted; Annex E.2 decisions referenced | 3.2; 3.4 |
| 4 | Session 2 minutes attribute the status gap to the Child Helpline but list no helpline attendee, and record no absences | Stated in the participant entry | 3.2; 3.4 |
| 5 | Session 1–2 minutes are drafts for review and correction; evidence column used informal names | Evidence column uses [M1]–[M3] with draft status; explanatory note added below the table | 3.2 |

Figure 2 shows dates, events and decision IDs only and did not need regenerating. Still open: the D-001–D-004 attribution (Session 2 minutes describe D-001–D-009 as Session 1 decisions, while Annex E assigns them to Session 2), and confirmation of attendee lists by UNICEF and the Ministry (P-03). The minutes themselves have not been changed.

## Version 2.5 signed contract and timeline review on 30 October 2026

Reviewed v2.4 against the signed Amendment 3 to contract 43427866 [CT2]. The signed copy is held outside the project repository, and contract amounts are not reproduced in the report. Word v2.5 and a tracked-changes copy against v2.4 produced; v2.4 retained unchanged.

| # | Finding | Change made | Affected section |
|---|---|---|---|
| 1 | Governing contract is 43427866 Amendment 3, signed 15 Sep 2026; integration is items 50–80; D1 is item 50 | Cover, document control, 1.1, 1.2, 2.7 and Annex I updated; CD-02 resolved as to the governing contract | Cover; DC; 1.1; 1.2; 2.7; 2.8; I.1; I.2 |
| 2 | The signed amendment has no integration SOW or deliverable dates; technical requirements and months come only from the unsigned TICAD text [CT1] | TICAD text treated as the agreed technical specification pending UNICEF confirmation that it is the technical annex; new CD-15 and decision 9 | 1.1; 1.4; 1.8; 2.7; 2.8; 8.8 |
| 3 | Original D1 target (August 2026) predates signature; three different end dates in the amendment (7 Jul, 10 Jul, 10 Jun 2027) | CD-15, CD-16; key-dates table | 1.7; 2.8; 8.3 |
| 4 | Late-submission fee reductions (10/20/30%, withheld beyond two months) with no due dates for items 50–80 | CD-17; decision 2 reworded; R-009 mitigation extended; dated baseline requested | 1.8; 2.8; 8.7; 8.8; 11.1; G |
| 5 | 90-day support after a February launch falls within the signed validity | CD-10 partly resolved; 2.7 and 8.3 updated | 1.8; 2.7; 2.8; 8.3 |
| 6 | Data ownership and confidentiality clause | Noted in the legal position | 7.2 |
| 7 | Timelines spread across several tables without dates | 8.3 restructured: Table 8.3a key contract dates, Table 8.3b deliverable timeline with proposed revised dates, original TICAD months retained; 8.7 replaced with a dated recovery timetable with gates G1–G5 (G2 access by 13 Nov 2026 is the critical date) | 8.3; 8.4; 8.7 |

All revised dates are BITZ proposals for UNICEF approval; BITZ must confirm workload and staffing. Lesotho public holidays were not checked. Figure 7 (original monthly Gantt) still shows TICAD item numbers 10–40, as noted in its caption. The contract-aligned delivery plan (`02_project_management/CONTRACT_ALIGNED_DELIVERY_PLAN.md`) has not been updated to the signed item numbers or the dated timetable.

## Version 2.6 signed contract as single source on 30 October 2026

At the owner's direction, the signed Amendment 3 to contract 43427866 [CT2] is the only contractual source. All citations of the unsigned TICAD-2026-001 text [CT1] were removed from the body and annexes; the CT1 rows were removed from sections 1.2 and Annex I.1. Earlier version-history rows still mention it as a historical record. Word v2.6 and a tracked-changes copy against v2.5 produced; v2.5 retained unchanged.

| # | Change | Affected section |
|---|---|---|
| 1 | Requirements named in signed item 70 (JWT authentication, retry logic, offline queue, idempotency, audit logging) cited to [CT2 item 70]. Parameters it does not state (retry intervals, TLS 1.2 minimum, central configuration file, operator alerts, automatic renewal on 401) restated as BITZ proposals | 1.4; 1.5; 7.3; 11.4; 11.5; Annexes A, C, D, J, K |
| 2 | Obligations that existed only in the TICAD text removed or restated as proposals: monthly milestones, Week 2–4 deadlines, sandbox-only testing, UNICEF as user-testing signatory, 90-day free maintenance, weekly stand-ups and monthly reports, hard-copy submission, data-sharing agreements as a contract obligation, two-person team | 1.6–1.9; 2.7; 7.5; 8.4; 8.5; 8.8; 9; 10; 12 |
| 3 | Discrepancies CD-08, CD-10, CD-11, CD-13 and CD-14 withdrawn; CD-02 resolved; CD-05, CD-07, CD-09, CD-12 and CD-15 restated against [CT2] or the minutes | 2.8; 11.3 |
| 4 | Contract obligations now drawn from [CT2]: item titles, trips 1 and 2, reporting formats (section 2.5), personnel acceptance (clause 8), payment withholding and late-submission reductions (section 4), data ownership (section 3.2) | 2.7; 9.1; 9.4; 10 |
| 5 | Timeline: TICAD monthly table removed; Figure 7 replaced with a Gantt chart of the proposed timetable; review steps on 2 and 3 November added to Tables 8.3a and 8.7; 8.3b and 8.4 show "not stated" contract dates and proposed dates | 8.3; 8.4; 8.7 |

Figure 7 was regenerated as an image, so the tracked copy shows the new chart without change marks. Requirement status counts in Figure 3 were not changed. Still open: the consent sentence in section 1.4, and updating the contract-aligned delivery plan.

## Version 2.7 reissue on 30 October 2026

Reissued for review by the Session 3 participants so that the circulated draft has a distinct version number from the earlier v2.6 circulation. Changes: version number, version history row, review-step references in sections 8.3 and 8.7, and "So-live" corrected to "Go-live" in the five places it appeared. No content, decision or approval status changed. Word v2.7 and a tracked-changes copy against v2.6 produced.
