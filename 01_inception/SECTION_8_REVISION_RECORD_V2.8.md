# Section 8 revision record — D1 v2.8 Post-Validation

**Report:** [D1_INCEPTION_REPORT_OPENCHS_PRIMERO_V2.8_POST_VALIDATION.md](D1_INCEPTION_REPORT_OPENCHS_PRIMERO_V2.8_POST_VALIDATION.md), Section 8 (Implementation plan)
**Scope of edit:** Section 8 only, in the Markdown file. The Word file has not been changed.
**Governing input:** Section 8 implementation-plan validation decisions IMP-001–IMP-008, cited in the report as [RV8].
**Status:** Revised draft. Not an approval record. Line numbers refer to the Markdown file after the Section 12 edit.

## Where each deliverable is

| Brief deliverable | Location in the report |
|---|---|
| 1 — Revised Section 8 | Sections 8.1–8.8, ending with the change log and QA note |
| 2 — Work-plan table | Table 8.1: 12 phases, objectives, activities, outputs, responsible and approving parties, dependencies, evidence-based criteria and D1–D4 mapping |
| 3 — Figures | Figure 6, now an editable dependency model with Workstreams A and B and the G2 gate. Figure 7, now an editable Gantt chart with a legend for proposed, dependent, approved and achieved milestones (none approved or achieved). The original images are linked as history |
| 4 — Delivery and dependency registers | Table 8.4 (delivery status, with the 30 Oct baseline kept above it); Table 8.5 (14 critical dependencies) |
| 5 — Approval and milestone registers | Table 8.2 (gate accountability); Table 8.7 (G1–G5 plus the production go/no-go); Table 8.8 (approval register: original decisions 1–8 plus checkpoint 9) |
| 6 — Change and consistency report | This file |

## Deliverable 6 — Change and consistency report

### Material changes

1. **Phase 2:** the automatic return-path design is removed; it now covers Create Referral and Send Update design only.
2. **Phase 5:** "Build the integration client and return path … referrals, updates and attachments" is now the gateway scope in TECH-001, including the 1, 5, 30 and 120-minute retry schedule and reconciliation.
3. **Phases 6–8:** security verification, Lesotho integration testing and Ministry-led UAT are now separate.
4. **Phases 10–12:** each now requires a written go/no-go decision, hypercare evidence or written handover acceptance.
5. **Section 8.3 date-shifting:** "Later dates move by the same number of working days" is replaced by notification, impact assessment, mitigation, proposed dates and formal approval. The same wording in section 8.7 is replaced in the same way.
6. **Section 8.5:** "BITZ proposes to raise this in the X-Road sessions (A-019)" is replaced. A-019 is now recorded as historical ABR coordination and not a referral dependency.
7. **New items:**
   - a production go/no-go checkpoint, separate from G5;
   - three evidence levels (L1–L3);
   - six distinct delivery states;
   - five schedule-governance categories (Table 8.3c).
8. **Section 8.8:** decision 3 now reads "Confirm the validated outbound-only scope and outstanding Primero API capability details", replacing "Agree the effort and contract treatment of two-way updates and attachments…". The original references (CD-01, CD-03, CD-04) are kept.

### Historical facts preserved

- Every date in Table 8.3a.
- The 30 Oct 2026 status table, unchanged.
- The minutes-based "inputs needed before development" table, unchanged.
- Every proposed recovery date and gate G1–G5.
- The five-working-day review assumption, the holiday contingency, the February trip 2 and the English and Sesotho materials.
- The R-009 invoicing and acceptance question.
- CD-07, CD-15, CD-16 and CD-17.
- The v2.7 rows dated 30 Oct to 6 Nov, now annotated with the meeting held on 4 Nov [M4].

### Verified definitions (checked against the source registers)

- **R-009** is "Milestone slippage". The D1 invoicing and acceptance question sits within it; it is not a separate risk.
- **A-019** is "Invite BITZ to Primero / X-Road sessions".
- **A-023** is "Configure API authentication; begin test calls" (Peter / Marlon, after A-016).
- **A-021** is "Agree handling of referrals during outages".
- **A-014** was received [SOP1]; closure was recorded at [M4], and its applicability is still pending.
- **A-007** is "Confirm ABR format, ownership, rules". The structure only was received on 26 Oct.
- **R-010** is "Contract scope change (two-way, attachments)".

### CD-16, contract end date

The signed Amendment 3 itself contains all three dates:

- **7 July 2027** in the header block, the operative "not later than" clause and the "Contract valid to" line;
- **10 July 2027** in the "Amendment 03" heading;
- **10 June 2027** in the narrative justification paragraph.

Table 8.3a now records where each date appears, but none is selected. CD-16 stays open until UNICEF confirms in writing or a corrective amendment is issued.

### Outstanding verifications and unresolved decisions

- **UNICEF:** CD-16; approval of the timetable (CD-15, CD-17); scope confirmation (CD-01, CD-03, CD-04); confirmation of the 14-week plan relationship (CD-07); the role of global demonstration evidence (D-018); training and support arrangements; the R-009 governance decision.
- **Ministry:** the UAT signatory (CD-09); the datasets and lawful basis (DSR register); safeguarding approval for go/no-go; SOP applicability (A-014).
- **Primero:** Lesotho access (A-015, A-016; G2); credentials (A-023); the service catalogue (A-018); field names and the protection-concern list; supported Send Update operations (R-010 / RT-007); validation of the retry policy (A-021).

### Cross-document corrections (not made)

**Necessary:**

| # | Location | Conflict | Proposed minimal correction |
|---|---|---|---|
| S8-1 | Section 9.3, "Go-live" row | — | **Resolved by the Section 9 revision.** The historical row is kept; approval register entry AP-07 now provides the written go/no-go decision (Ministry and UNICEF, as confirmed) | — |
| S8-2 | Section 9.4, "Review and approval" row | — | **Resolved by the Section 9 revision.** The row is now marked "(subject to agreement)" | — |
| S8-3 | Section 10.5, operator training | — | **Resolved by the Section 10 revision.** Training Track 1 covers technical status and explicit Send Update; "returned updates" removed | — |
| S8-4 | Section 10.7, "Technical requirements" row | — | **Resolved by the Section 10 revision.** The historical row is kept; readiness register Table 10.7 classifies the return mechanism as excluded (X) | — |
| S8-5 | Section 10.7, Figure 12 | — | **Resolved by the Section 10 revision.** Figure 12 is kept as a dated historical snapshot; the current gate position is shown separately | — |
| S8-6 | Section 11.1, R-001 | — | **Resolved in Section 11 by the Section 11 revision.** Table 11.1b. **The Annex G R-001 row is still outstanding** (Section 11 record) | — |
| S8-7 | Section 11.1, R-016 | — | **Resolved in Section 11 by the Section 11 revision.** Table 11.1b: global demonstration testing preliminary only; explicit acceptance needed for any alternative | — |
| S8-8 | Section 11.5, item 1 | — | **Resolved in Section 11 by the Section 11 revision.** The item is kept verbatim; the application note and Table 11.5 align it with TECH-006 | — |
| S8-9 | Section 11.1, R-009 | — | **Resolved in Section 11 by the Section 11 revision.** Table 11.1b: no automatic extension; recovery dates proposed. **The Annex G R-009 row is still outstanding** | — |
| S8-10 | Section 12.1 | — | **Resolved by the Section 12 revision.** Now reads "consider the proposed dates in section 8.7 for formal UNICEF approval (section 8.8, decision 2)" | — |
| S8-11 | Section 12.2 heading | — | **Resolved by the Section 12 revision.** Heading kept as dated history; Table 12.4 reconciles each action and Table 12.3 holds the current outstanding conditions | — |
| — | Section 7 record, M-10 (R-006 and R-010) | Still applicable | Still outstanding |

**Optional:**

- O-1: Add [RV8] to Annex I.1, alongside RV3–RV7.
- O-2: Add an Annex E table for IMP-001–IMP-008.
- O-3: In Annex F.3, cross-reference Table 8.5 so that dependency status is not maintained twice.
- O-4: Update the D1_ACCEPTANCE_READINESS.md link target in section 10.7 when that file is next revised.
- O-5: **Version labels (flag only).** The Word header says "Version 2.8", the Word footer says "Version 2.8 — pending formal approval", and the Markdown title block says "Version 2.8 — Post-Validation Revision · 9 November 2026". No new version number has been assigned.

**Consistency with Sections 5–7 (checked):**

- **Section 5:** BR-001–BR-010 are covered by Phase 4 (interface, dropdown, confirmation, ABR, partial and emergency referrals, status display, Send Update permissions) and Phases 7–8 (scenarios).
- **Section 6:** the architecture, ledger, retries, reconciliation, environments and the limits of the global demonstration are reflected in Phases 2, 3, 5 and 7, G2–G4 and decision 7.
- **Section 7:** the lawful basis, datasets, anonymity, access controls and synthetic-only testing are dependencies (Phases 1, 6 and 8; Table 8.5 A-017 / A-022; decision 5; go/no-go checklist).

## Final acceptance checklist

- [x] All eight subsections revised
- [x] IMP-001 to IMP-008 implemented (Section 8 change log)
- [x] All 12 phases traceable to D1–D4
- [x] Outbound-only architecture consistent; no OpenFN, inbound synchronisation or attachments in the plan
- [x] Parallel development permitted with controls; evidence levels L1–L3
- [x] Historical and proposed dates distinguishable (Tables 8.3a–8.3c; Figure 7 legend)
- [x] CD-16 flagged pending verification
- [x] No automatic schedule extension
- [x] G1–G5 have measurable evidence (Table 8.7)
- [x] Production go-live requires separate written authorisation
- [x] Ministry-led UAT and safeguarding preserved
- [x] Eight original decisions traceable (Table 8.8, rows 1–8)
- [ ] Figures, tables and registers reconciled **within Section 8**: yes. Annex and Section 9–12 references: see the corrections above
- [x] No unsupported progress or approval claims
