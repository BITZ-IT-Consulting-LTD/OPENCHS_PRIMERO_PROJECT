# Section 11 revision record — D1 v2.8 Post-Validation

**Report:** [D1_INCEPTION_REPORT_OPENCHS_PRIMERO_V2.8_POST_VALIDATION.md](D1_INCEPTION_REPORT_OPENCHS_PRIMERO_V2.8_POST_VALIDATION.md), Section 11 (Risks and outstanding decisions)
**Scope of edit:** Section 11 only, in the Markdown file. The Word file has not been changed.
**Governing input:** Section 11 validation decisions RSK-001–RSK-006, cited in the report as [RV11].
**Status:** Revised draft. Not an approval record. Line numbers refer to the Markdown file after the Section 12 edit.

## Deliverable 1 — Revised Section 11

This is in the report: sections 11.1–11.5, Tables 11.1a, 11.1b, 11.3, 11.4 and 11.5, Figure 13, and the closing change log and QA note.

These parts were checked by comparison with the pre-edit file and are unchanged:

- **Table 11.1a**, the 17-risk historical register, matches the original character for character, including the curly quotation marks in R-015.
- **Figure 13**, the heat-map grid, matches the original.
- **The 11.4 and 11.5 decision lists** match the original wording.

## Deliverable 2 — Change-control summary

| Location | Original issue | Revision made | Decision reference | Related source |
|---|---|---|---|---|
| 11.1 | Single register mixing historical mitigations with no reconciliation (R-004 "client UUID", R-006 "webhook role", R-010 "governance decision" only) | Historical register kept unchanged as Table 11.1a. Reconciliation Table 11.1b adds the validated mitigation, actions and decisions, outstanding evidence, decision authority, current verified status ("Open — not reverified" for all 17) and closure evidence. R-004 uses the 1, 5, 30 and 120-minute intervals, described as proposed design parameters and not a contractual service level. R-006 is outbound-only. R-009 keeps the 14-week baseline and treats recovery dates as proposals. R-015 does not claim the wording was amended | RSK-001 | Annex G; Sections 5–10; [CT2] |
| Figure 13 | Captioned "Proposed BITZ assessment, for validation" | Retitled "Historical BITZ-proposed risk assessment, subject to governance validation". All 17 positions, the seven High/High and five externally dependent statements, and the "no Low rating" statement kept. Legend and five reassessment rules added. No current-state map | RSK-002 | Source Figure 13 |
| 11.2 | Four rules referring to an unconstituted "steering review"; no urgent route or closure controls | Rules kept verbatim, with an interpretation note (section 9.5). Lifecycle, immediate incident route (no invented time limits), materialised-risk handling and closure controls added. Closure is separated from residual-risk acceptance and from any approval | RSK-003 | Section 9.5; DSR-10 |
| 11.3 | Realised issues called "current", with no records | CD paragraph kept. "Current issues" relabelled "Historical issues … as recorded at the source assessment", with the original wording kept. CD-09, CD-12, CD-15, CD-16 and CD-17 safeguards added. Issue records IS-01 to IS-05 and a schedule-impact evidence rule added. No finding of breach or entitlement | RSK-004 | Section 2.8; section 8.5; Annex F |
| 11.4 | Decisions 6 and 7 framed as open (inbound mechanism; OpenFN) | Eight decisions kept verbatim. Table 11.4 gives the technical disposition and the outstanding approval separately, using three disposition categories. None is formally approved, so detailed design is not approved | RSK-005 | Sections 5–7; TECH-001; SCOPE-001, SCOPE-002 |
| 11.5 | Global demonstration acceptance ambiguous; no readiness checks | Four decisions kept verbatim. Application notes added: the lost-acknowledgement test, the 11-scenario synthetic dataset, and defect rules aligned to Section 10. Readiness matrix (nine checks, explicitly not new contractual conditions) and eight-step decision sequence added | RSK-006 | Sections 8.7, 10.1–10.4 |

## Deliverable 3 — Outstanding approvals and dependencies

No due date or status has been invented. The table lists only the gate each item affects.

| Outstanding decision | Responsible party | Approval authority | Required evidence | Affected gate | Related risk / action |
|---|---|---|---|---|---|
| Lesotho environment access and configured endpoints | Primero; UNICEF (checklist) | Primero | Authorised test exchange | G2 | R-001, R-012; A-015, A-016 |
| SOP applicability and pathways | Ministry; UNICEF | Ministry | Written applicability; received pathways | G1; UAT | R-002; A-013, A-014 |
| Service catalogue, routing and mapping | Primero; BITZ | Ministry | Approved list and mapping | G2 | R-003; A-018 |
| Primero downtime behaviour and reconciliation semantics | Primero; BITZ | Primero (technical) | RC-01 to RC-04 results | G4 | R-004; A-021 |
| Official ABR specification | Ministry / relevant authority | Ministry | Specification and examples | D2 acceptance | R-005; A-007 |
| Supported Send Update operations and permitted fields | Primero | Ministry (fields); UNICEF (contract) | Verified operations; written confirmation | G3 | R-006, R-010; RT-007 |
| Legal, safeguarding and data-protection approvals | Ministry; UNICEF legal advisers | Ministry | DSR-01 to DSR-05 evidence | Production go/no-go | R-007; A-017, A-022 |
| Focal person, leave cover and support owners | Ministry | Ministry | Nominations | Go-live | R-008; A-002, A-024 |
| Schedule approval and contract end date | BITZ (impact assessment) | UNICEF | Written approval | All | R-009; CD-15, CD-16, CD-17 |
| Formal confirmation of outbound-only scope | BITZ (request) | UNICEF | Written confirmation | G3 | R-010; CR-01, CR-02 |
| Consent, lawful basis and override rules | Ministry | Ministry | Written decision | UAT; production | R-011; DATA-012 |
| Credentials and token renewal | Primero; BITZ | Primero | Authenticated test call | G2 | R-013; A-023 |
| Named approvers (D1, UAT, security) | UNICEF; Ministry | UNICEF; Ministry | Written nominations | G1, G5 | R-014; CD-09 |
| D2 and D4 wording versus explicit referral control | BITZ (request) | UNICEF | Written wording decision | D2, D4 acceptance | R-015; CD-03 |
| Acceptance basis for any non-Lesotho test evidence | BITZ (request) | UNICEF; Ministry | Written confirmation | G4 | R-016; D-018 |
| Hosting, controllers, processors and cross-border access | Ministry; UNICEF | Ministry; UNICEF | Written arrangements | Production go/no-go | R-017; DSR-05, DSR-09 |
| Fault thresholds versus UNICEF acceptance | BITZ (proposal) | UNICEF | Approved thresholds | G5; D4 | CD-12 |
| Approved synthetic test dataset | BITZ (prepare) | Ministry | Approved dataset | Integration testing | UAT-003; DSR-11 |

## Deliverable 4 — Cross-reference verification

### Necessary corresponding amendments (not made)

| # | Location | Required amendment |
|---|---|---|
| S11-1 | Annex G, R-001 (line 3682) | Append to the mitigation: "**Current:** global demonstration for preliminary tests only (TECH-006); Lesotho access required for G2." Keep the historical text and the trigger |
| S11-2 | Annex G, R-004 (line 3685) | The existing **Current** note is consistent. Append "retries at 1, 5, 30 and 120 minutes after the preceding failure (proposed design parameters; not a contractual service level); manual escalation after exhaustion" |
| S11-3 | Annex G, R-006 (line 3687) | The existing **Current** note says inbound is future scope. Append "validated mitigation: explicit Send Update, technical acknowledgements, reconciliation, failed-update handling without new case creation (Table 11.1b)." Replace "webhook role" only within the Current note, never in the historical text |
| S11-4 | Annex G, R-009 (line 3690) | Append "**Current:** 14-week baseline retained; recovery dates proposed; no automatic extension (section 8.3)" |
| S11-5 | Annex G, R-013 (line 3694), R-015 (line 3696) and R-016 (line 3697) | Append Current notes matching Table 11.1b |
| S11-6 | Annex G (general) | Add a "Current verified status" column, or a note, recording "Open — not reverified" for all 17 risks, and the last verified review date (source assessment) |
| S11-7 | Annex F (issue records) | Add IS-01 to IS-05 to the action and issue register, or cross-reference Table 11.3, so that issues are not maintained in two places |
| S11-8 | Annex E, D-015 (line 3571) | Same as Section 6 record N-12: append the TECH-001 current treatment |
| S11-9 | Annex J, API-009 | Same as Section 6 record N-11 |
| S11-10 | Annex H (new scenarios) | The Section 11.5 synthetic-dataset scenarios mostly map to existing IDs (F-02 to F-07, RC-01 to RC-06, S-02, F-13). "Authorisation failure" maps to S-02. No new ID is required beyond those in Section 10 record S10-3 |

### Inconsistent references in Sections 2.8 and 5–10 (checked)

- **Section 2.8, CD-09 to CD-17 (lines 527–531):** consistent with 11.3. CD-16 there "retains the editorial placeholder in section 2.7". Section 8.3 now records where each date appears in the amendment, so section 2.7 may cross-reference it (optional).
- **Sections 5–10:** no conflicts with the revised Section 11. Section 11 cites the Section 6 retry policy, the Section 7 DSR register, the Section 8 gates and timetable, the Section 9 AP register and escalation routes, and the Section 10 defect rules and criteria, all with matching meanings.
- **Retry wording:** Section 11 calls the intervals "proposed design parameters", following the brief, and Section 6 calls them "validated" (TECH-004). These are compatible: validated as design parameters, configurable, subject to Primero validation, and not a contractual service level. Annex J records OPS-002 as "Confirmed — Existing Contractual Obligation" for the retry capability. That refers to the obligation to have retry logic under item 70, not to the specific intervals. Optionally, clarify this in Annex J.

### Earlier records updated

The following are marked resolved in Section 11:

- N-10 (Section 6 record);
- M-8, M-9 and M-10 (Section 7 record; the Annex G part of M-10 remains open);
- S8-6 to S8-9 (Section 8 record; the Annex G parts of S8-6 and S8-9 remain open);
- S9-3 and S9-4 (Section 9 record);
- S10-6 and S10-7 (Section 10 record).

**Optional:**

- O-1: Add [RV11] to Annex I.1.
- O-2: **Version labels (flag only).** The Word header says "Version 2.8", the Word footer says "Version 2.8 — pending formal approval", and the Markdown title block says "Version 2.8 — Post-Validation Revision · 9 November 2026". No new version number has been assigned.

## Final quality-assurance checklist

- [x] All 17 risks present; ratings, owners and Open statuses unchanged (verified against the pre-edit file)
- [x] Figure 13: seven High/High; five externally dependent identifiable
- [x] R-006 outbound-only; R-010 scope controls; R-004 safe retries and reconciliation; R-009 baseline and unapproved recovery
- [x] Immediate safeguarding and security escalation; evidence-based closure; materialised risks linked to issues
- [x] CD-09, CD-12, CD-15, CD-16 and CD-17 traceable
- [x] Eight 11.4 and four 11.5 decision areas preserved verbatim
- [x] No OpenFN or inbound synchronisation reintroduced; global demonstration not equated with Lesotho verification
- [x] Synthetic data and safeguarding explicit; integration approval, UAT, UNICEF acceptance and go/no-go distinct
- [x] No unsupported approvals, closures, dates or results
- [ ] Annex G and F alignment: see S11-1 to S11-7
