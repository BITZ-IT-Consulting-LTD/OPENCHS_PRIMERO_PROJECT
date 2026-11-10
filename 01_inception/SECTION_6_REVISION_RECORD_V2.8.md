# Section 6 revision record — D1 v2.8 Post-Validation

**Report:** [D1_INCEPTION_REPORT_OPENCHS_PRIMERO_V2.8_POST_VALIDATION.md](D1_INCEPTION_REPORT_OPENCHS_PRIMERO_V2.8_POST_VALIDATION.md), Section 6 (Proposed technical approach)
**Scope of edit:** Section 6 only, in the Markdown file. The Word file has not been changed.
**Governing input:** Section 6 technical-validation decisions TECH-001–TECH-007, cited in the report as [RV6].
**Status:** Revised draft. Not an approval record. Line numbers refer to the Markdown file after the Section 12 edit.

## Deliverable 1 — Revised Section 6

This is in the report itself. It keeps subsections 6.1–6.7 and adds Diagram 6.2. Section 6.7 ends with four further subsections: the technical verification register, acceptance traceability, the change log, and quality assurance.

## Deliverable 2 — Technical decision traceability matrix

| TECH | Decision | Section 6 location | Existing identifiers |
|---|---|---|---|
| TECH-001 | Single architecture OPENCHS → BITZ Integration Gateway → Primero CPIMS+ API; no OpenFN; no X-Road referral path; outbound-only initial scope | Introduction (initial-scope boundary); 6.2 components, Diagram 6.2, architecture exclusions and decision history, remaining dependencies | API-001–API-003, API-009; GOV-004; D-015 (historical); SCOPE-006 (conditional OpenFN element superseded); SCOPE-002–SCOPE-005 |
| TECH-002 | Thirteen testable design principles | 6.1 table | D-006, D-008, D-016; WF-002, WF-007; FN-003, FN-006, FN-008, FN-010, FN-011; RT-001, RT-002, RT-005–RT-007; OPS-001–OPS-004; DATA-010, DATA-013; SEC-001, SEC-003–SEC-006; API-002 |
| TECH-003 | Six-step transaction flow; creation and Send Update are distinct transaction types; automatic return step removed | 6.3 steps 1–6 and operation separation | API-003; FN-009; DATA-013; WF-003; SCOPE-001; RT-007 (historical, deferred) |
| TECH-004 | Three failure classes; four retries at 1, 5, 30 and 120 minutes; duplicate prevention; eight-step reconciliation; manual recovery and alerting | 6.4 | API-004; OPS-002, OPS-003, OPS-007; AUD-001, AUD-002; FN-003; WF-007 |
| TECH-005 | Responsibility matrix for BITZ, the Ministry, Primero, Child Helpline 116 and UNICEF; operational-readiness confirmations; return-update row replaced by Send Update | 6.5 | OPS-006, OPS-007; API-008; SCOPE-007; D-006 |
| TECH-006 | Uses and limits of six environments; global demonstration not sufficient; four separate milestones; dated baseline preserved | 6.6 | UAT-003, UAT-007; SEC-007; D-018; A-015, A-016; API-005, API-008; SCOPE-009 |
| TECH-007 | Transaction ledger; technical and business status vocabulary; monitoring; audit; reconciliation; retention | 6.7 | OPS-001, OPS-004, OPS-006, OPS-007; DATA-013; SEC-006; AUD-001, AUD-002 |

## Deliverable 3 — Annex K architecture correction instructions

None of these has been made.

| # | Location | Required change |
|---|---|---|
| K-1 | Annex K introduction and K.1 lead paragraph (line 4090) | Replace "Direct API through BITZ gateway is preferred. OpenFN requires a verified dependency and appropriate approval" with: "The validated architecture is OPENCHS → BITZ Integration Gateway → Primero CPIMS+ API (TECH-001). Direct API connectivity is the sole proposed mechanism. OpenFN is not part of the proposed design, and earlier references to it are historical (D-015; SCOPE-006)." Keep the X-Road exclusion and the future-scope sentence. |
| K-2 | K.1.1 Design principles (line 4092) | Point to section 6.1 as the governing principle set. Add the principles that are missing: approved destination and service, human confirmation, persistent linkage, outbound-only scope and emergency continuity. |
| K-3 | K.1.2 Diagram A (line 4106) | Label the dotted return arrow "technical acknowledgement / error response (to initiated operation only)". Add a separate explicit Send Update arrow. Keep "Future only" as a stand-alone, unconnected note. The diagram should match Diagram 6.2. |
| K-4 | K.1.3 Diagram B (line 4120) | Split it into two sequences, referral creation and Send Update, each with its own operation ID. Add the destination and service selection step. Show the unresolved → reconcile → resume branch from section 6.4. Keep the note that technical receipt is not Ministry acceptance. |
| K-5 | K.1.4 Diagram C (line 4142) | Add the retry schedule (1, 5, 30 and 120 minutes; transient failures only) and the three failure classes. Add a monitoring and alerting node for retry exhaustion and unresolved transactions. Keep "operations unverified until evidenced". |
| K-6 | K.1.5 Component summary (lines 4159–4170) | Rename the "Outbound" layer "BITZ Integration Gateway" and list the TECH-001 gateway responsibilities. Add an "OPENCHS" layer listing the TECH-001 OPENCHS responsibilities. Change "Receiving system" to "Primero CPIMS+ API (direct; sole mechanism)". Keep the "Return channel" row, but retitle it "Future addendum only — not an initial component". |
| K-7 | K.1.6 Diagram D and environment table (lines 4172–4194) | Add the TECH-006 limitation to the global-playground row: "cannot establish Lesotho acceptance or production readiness". Add Joint UAT as a separate environment or stage. Show the four milestones (technical verification, UAT, contractual acceptance, go-live) as separate gates. Keep the 27 October baseline column unchanged. |
| K-8 | K.1.7 (line 4196) | Add the minimum ledger fields from section 6.7 and the reconciliation scope (ambiguous creation, missing UUID, conflicting records, failed updates, duplicate-risk incidents). Retain the "not implemented" qualifier. |
| K-9 | K.2.3 control table, "Processing contracts" row (line 4228) | Replace "(BITZ, hosting provider, OpenFN if used)" with "(BITZ, hosting provider and any other approved processor)". This is a minimal wording change; the legal content is unchanged. The equivalent row in section 7.3 (formerly line 1427) was **resolved by the Section 7 revision**: the matter is now register entry DSR-05, with no OpenFN reference. |
| K-10 | K.2.3, "Authentication" row (line 4221) | The phrase "renewed automatically on a 401 response (proposed)" is an unverified mechanism. Qualify it as "subject to Primero verification (Section 6 technical verification register)". Make no other change. |
| K-11 | K.2.3 "Anonymous reporters" row and K.2.6 | Replace "return updates" with "any future approved inbound exchange", as in Section 5 record item 2. |

## Deliverable 4 — Cross-document correction log

### Necessary corrections (direct conflicts with TECH-001 to TECH-007)

| # | Location | Conflict | Proposed minimal correction |
|---|---|---|---|
| N-1 | Section 1.4, "System connection" row (line 286) | "Direct API versus OpenFN requires technical review" | Change to "Architecture validated as direct Primero API through the BITZ gateway (TECH-001); deployed API verification remains pending. X-Road remains separate." |
| N-2 | Section 1.4, "Technical architecture" row (line 303) | Same OpenFN open position | Change to "Transaction sequence, UUID handling and duplicate-prevention behaviour require Primero verification." Keep Primero's absence from Session 4 as a fact. |
| N-3 | Section 1.6 (line 317) | Retry intervals described as "proposed technical parameters" | Change to "Retry intervals of 1, 5, 30 and 120 minutes are validated (TECH-004; OPS-002), are configurable, and their behaviour is still to be verified in testing." |
| N-4 | Section 1.7 (line 331) | "direct API versus OpenFN" listed as unresolved | Delete that phrase. Keep sequencing, duplicate prevention and recovery as items still to be verified. Change "return mechanisms" to "future return mechanisms (addendum)". |
| N-5 | Section 1.8, decision 6 (line 352) | "Direct API versus OpenFN remains undecided" | Change to "Architecture validated (TECH-001). Confirm service configuration, authentication and the transaction sequence after Primero technical verification." |
| N-6 | Section 2.2 (line 448) | "Direct API versus OpenFN remains a technical decision" | Change to "Direct Primero API through the BITZ gateway is the validated architecture (TECH-001); the earlier API-versus-OpenFN discussion is recorded in D-015." |
| N-7 | Section 3.3 "Architecture" row (line 597) and section 3.6 (line 651) | OpenFN described as allowed if verified and approved | Append: "Superseded by TECH-001: OpenFN is not part of the proposed design." Keep the historical columns. |
| N-8 | Section 4.1 table (line 772) and 4.3 "Gateway boundary" (line 840) | "OpenFN only if a verified dependency requires it…" | Replace with "OpenFN is not part of the proposed design (TECH-001)." Keep "subject to technical verification". |
| N-9 | Section 4 change log (line 920) | "conditional OpenFN" | Leave the historical log row unchanged. Optionally add a row recording that TECH-001 supersedes the conditional OpenFN element. |
| N-10 | Section 11.4, item 7 | — | **Resolved in Section 11 by the Section 11 revision.** The original question is kept verbatim as history; Table 11.4 row 7 records direct integration through the BITZ Gateway, with OpenFN excluded (TECH-001) | — |
| N-11 | Annex A, API-009 (line 3281), and Annex J current row (line 3982) | "introduce OpenFN only if verified…" | Replace the **Current** text with "Use direct Primero API integration through the BITZ gateway as the sole mechanism (TECH-001); OpenFN is not part of the design; exclude X-Road." Keep the historical J row (line 3969) unchanged. |
| N-12 | Annex E.1, D-015 (line 3571) | "Current scope treatment" refers to SCOPE-006 with OpenFN conditional | Append: "TECH-001 [RV6]: direct API is the sole proposed mechanism; OpenFN is not part of the design." |
| N-13 | Annex E.3, SCOPE-006 (line 3602) | "conditional OpenFN" | Keep the row as history. Append "Conditional OpenFN element superseded by TECH-001". Optionally add an E.5 table for TECH-001 to TECH-007 (E.4 is proposed for the BR decisions). |
| N-14 | Annex K | See Deliverable 3, items K-1 to K-11 | — |
| N-15 | Annex B.3 (line 3345) | "Proposed idempotency approach" could be read as a confirmed Primero capability | Append: "Native behaviour in the Lesotho deployment is unverified; where it is unavailable, gateway-side controls and limitations are documented (section 6.4)." |
| N-16 | Annex H, RC-05, RC-07 and F-12 | — | **No change needed (checked during the Section 10 revision).** All are already labelled future scope and excluded from initial UAT | — |

### Checked and consistent (no change needed)

- **Section 5:** the workflow, status vocabulary, retry policy and Send Update separation match Section 6.
- **Section 7.4, Figure 5:** outbound-only, with inbound shown as future.
- **Annex B.5:** labelled "future-phase reference only".
- **Annex B.7:** the dependency list matches the section 6.7 register.
- **Annex D.4:** the retry and reconciliation wording matches.
- **Annex J, AUD-003, SEC-008 and RT-007:** already marked as addendum items.

### Optional improvements

- O-1: Add Diagram 6.2 to the "Diagrams and figures" list (line 80 onward) without renumbering the existing figures.
- O-2: Add [RV3], [RV4], [RV5] and [RV6] to the Annex I.1 source register.
- O-3: In the Annex I.3 acronym list (line 3838), keep OpenFN because historical records still use it.
- O-4: Add the new Section 6.7 scenarios to Annex H: CPIMS+ destination selection, the confirmation-cancel check, failed update without creating a new case, technical status display, the unresolved-transaction alert, and the Lesotho environment-readiness check.
- O-5: **Version labels (flag only).** The Word header says "Version 2.8", the Word footer says "Version 2.8 — pending formal approval", and the Markdown title block says "Version 2.8 — Post-Validation Revision · 9 November 2026". These need reconciling at document-control level. No new version number has been assigned.

## Deliverable 5 — Technical verification and acceptance checklist

**Primero API dependencies** (none resolved)

- [ ] Deployed Lesotho release and matching API documentation (API-001, GOV-004)
- [ ] Authentication flow and integration credentials (API-002)
- [ ] Integration-account permissions (SEC-003)
- [ ] Referral creation operation and response contract (API-003)
- [ ] UUID return or retrieval method (DATA-013)
- [ ] Supported Send Update operations (FN-009), plus contractual confirmation where required (SCOPE-001)
- [ ] Error classes, timeouts and response behaviour (API-004)
- [ ] Native idempotency, or a documented limitation (OPS-003)
- [ ] Authorised reconciliation lookup, or an assisted procedure

**Ministry approvals**

- [ ] Service catalogue and codes (RT-001 / A-018)
- [ ] Required referral fields and emergency minimum dataset (DATA-005, WF-004)
- [ ] Lawful basis and disclosure rules (SEC-001, DATA-012)
- [ ] Retention periods and audit access for the gateway ledger and logs (SEC-006)
- [ ] Routing and permissions (RT-003)
- [ ] Production use of real data and hosting (R-017)

**Environments**

- [ ] Lesotho CPIMS+ test environment: URL, connectivity and readiness check (UAT-003, A-015)
- [ ] OPENCHS test environment with gateway, with access evidence (API-005)
- [ ] Global demonstration access, for preliminary testing only (A-016, D-018)
- [ ] Production endpoints, credentials, certificates and rollback (API-008)

**Security controls**

- [ ] TLS 1.2 or later with certificate verification (SEC-005)
- [ ] Secret store, rotation and separate credentials per environment (SEC-004)
- [ ] Metadata-only audit with redaction (SEC-006, OPS-004)
- [ ] Network prerequisites: allowlisting, VPN and firewall (Annex B.4)

**Test evidence** (none executed)

- [ ] Section 6.7 scenarios 1–20, with conditional scenarios run once the dependencies above are evidenced
- [ ] Regression testing of existing OPENCHS functionality (OPS-008)
- [ ] Lesotho-specific end-to-end verification. Results from the global demonstration environment are not sufficient.

**Go-live prerequisites**

- [ ] Successful Lesotho integration verification
- [ ] Security and data-sharing approvals
- [ ] Named support contacts, incident ownership, an approved runbook and credential custody (OPS-006, OPS-007)
- [ ] Training and handover evidence
- [ ] UAT evidence with Critical and High defects resolved (UAT-007), and the applicable sign-offs
- [ ] Contractual acceptance, recorded separately
- [ ] Explicit go-live authorisation

**Self-check of the revised Section 6**

| Check | Result |
|---|---|
| Subsections 6.1–6.7 preserved | Yes |
| All seven TECH decisions reflected | Yes (Deliverable 2) |
| No OpenFN in any proposed role; history preserved | Yes. Section 6 mentions OpenFN only in the exclusion and in the D-015 / SCOPE-006 history |
| X-Road excluded from the referral path, with Home Affairs context given | Yes |
| No automatic inbound flow in the text, diagram or tests | Yes. Diagram 6.2 shows only responses to initiated operations |
| Technical acknowledgement never treated as acceptance | Yes |
| Referral creation and Send Update kept distinct | Yes |
| No unsafe retry after uncertain creation | Yes |
| No unverified Primero capability, endpoint, threshold, SLA or retention period asserted | Yes |
| Global demonstration not sufficient for Lesotho acceptance | Yes |
| No Ministry-controlled responsibility assigned to BITZ or UNICEF | Yes |
| Consistent with Section 5 | Yes |
| Version-label inconsistency flagged | Yes (O-5) |
