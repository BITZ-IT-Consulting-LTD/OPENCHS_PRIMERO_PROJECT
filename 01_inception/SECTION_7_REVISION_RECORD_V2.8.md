# Section 7 revision record — D1 v2.8 Post-Validation

**Report:** [D1_INCEPTION_REPORT_OPENCHS_PRIMERO_V2.8_POST_VALIDATION.md](D1_INCEPTION_REPORT_OPENCHS_PRIMERO_V2.8_POST_VALIDATION.md), Section 7 (Data and safeguarding requirements)
**Scope of edit:** Section 7 only, in the Markdown file. The Word file has not been changed. Two QA sentences that I wrote in the revised Sections 5 and 6 were also updated, because they listed section 7.3 items that this revision has resolved.
**Governing input:** Section 7 validation decisions DATA-SEC-001–DATA-SEC-006, cited in the report as [RV7].
**Status:** Revised draft. Not an approval record. Line numbers refer to the Markdown file after the Section 12 edit.

> **Matter for the report owner — data-sharing agreements.** The brief asked to preserve "the contractual requirement concerning data-sharing agreements among MSD, MoH, MoE and UNICEF". That wording appeared in v1.0 citing [CT1], the unsigned TICAD-2026-001 text. Version 2.6 adopted signed Amendment 3 [CT2] as the only contractual source, and a text search of the signed amendment found no such clause. Section 7.2 therefore keeps the existing wording, which refers to the ministries concerned and UNICEF without naming them, and does not reintroduce the unsigned source. If the clause exists in another signed instrument, please supply it and the reference can be added.

## Deliverable 1 — Revised Section 7

This is in the report itself. It keeps subsections 7.1–7.6 and their titles, and contains:

- **Table 7.1** — information categories
- **Table 7.2** — security-control baseline
- **Figure 5** — redrawn, keeping its existing number
- a trust-boundary table
- **Table 7.3** — proposed classification matrix
- **Table 7.4** — approval register with 18 entries, DSR-01 to DSR-18
- three closing subsections: acceptance traceability, change log, and quality assurance

## Deliverable 2 — Decision traceability matrix

| DATA-SEC | Decision | Location | Existing IDs | Annexes |
|---|---|---|---|---|
| DATA-SEC-001 | Approved minimum outbound dataset with field-level mapping; routine, partial and emergency datasets; optional ABR with structural checks and preserved formatting; nothing fabricated; 2019 SOP applicability to be confirmed | 7.1; Table 7.1 | D-004, D-005, D-011–D-014; DATA-002–DATA-013; FN-001, FN-002, FN-005, FN-011; WF-004, WF-005 | C, J.3 |
| DATA-SEC-002 | Legal references kept but qualified and dated; BITZ analysis marked as planning only; lawful basis per disclosure scenario; four consent states with lawful basis recorded separately; data-sharing, controller, processor and hosting confirmations; legal review by Ministry and UNICEF advisers | 7.2 | SEC-001; DATA-012; A-017, A-022; R-007, R-011, R-017; [DPA1]; [DMP1]; [CT2 sections 3.1–3.2] | I (sources) |
| DATA-SEC-003 | Eleven-control baseline; OPENCHS, gateway and Primero boundaries; evidence requirements | 7.3; Table 7.2 | SEC-002–SEC-007; API-002, API-008; OPS-004, OPS-006, OPS-007; AUD-001, AUD-002. Encryption at rest and tamper-evident audit have **no existing Annex J ID** | K.2.3, J.5 |
| DATA-SEC-004 | Outbound-only data flow; six permitted operations; four trust boundaries; proposed classification; gateway minimisation | 7.4; Figure 5; Table 7.3 | OPS-004, OPS-005; DATA-010; RT-007; TECH-001 | K.2.4 |
| DATA-SEC-005 | Formal register with milestone impact (DEV, TIT, UAT, PROD, GL); synthetic data only in testing | 7.5; Table 7.4 | Every ID cited in the register; R-007, R-011, R-014, R-017; A-013, A-015–A-017, A-022 | E, F, J, K |
| DATA-SEC-006 | Safeguarding-first model; six-step emergency escalation independent of the API; recorded exceptions; anonymity end to end; Ministry ownership; withdrawal never presented as confirmed; twelve training and UAT scenarios | 7.6 | WF-004–WF-007, WF-010; SEC-002; UAT-001, UAT-010 | J.5, H |

## Deliverable 3 — Data-flow and classification corrections

1. **Figure 5 (section 7.4), done.** Redrawn with four trust-boundary subgraphs. The only arrows back towards OPENCHS are the technical acknowledgement, error or UUID and the technical status. The stand-alone "Automatic inbound statuses / interventions" and attachment notes were removed from the diagram; those exclusions are stated in text and in Table 7.3. The historical image link is retained and relabelled as showing earlier inbound and attachment flows.
2. **Trust-boundary table, done.** It sets out what crosses each of the four boundaries and the permissions required.
3. **Classification matrix (Table 7.3), done.** It adds rows for approved service and referral linkage, the CPIMS+ UUID, technical transaction metadata and security credentials. Attachments, recordings and the case plan are now one excluded row, and the "Referral status and interventions" row is now "not transferred initially". Labels are proposed pending the national classification policy (DSR-13).
4. **Annex K.2.4 diagram and table, not done.** Replace the Annex K.2.4 Mermaid diagram (line 4235 onward) and its classification table with the new Figure 5 and Table 7.3, or with a pointer to section 7.4. The current K.2.4 diagram still shows the "Automatic inbound statuses / interventions" node, and its table still has the inbound "Referral status and interventions" row.
5. **Annex K Diagrams A–C, not done.** These are covered by Section 6 record items K-3 to K-5. When redrawing them, use the trust boundaries from Figure 5 as well.

## Deliverable 4 — Legal, safeguarding and approval dependency register

This is in the report as Table 7.4 (DSR-01 to DSR-18). In summary:

| Status | Entries |
|---|---|
| Under Review | DSR-01 (A-022 desk research in progress; [DPA1] and [DMP1] received) |
| Pending Confirmation | DSR-02 to DSR-17 |
| Blocked | DSR-18, final production data-exchange authorisation, which depends on DSR-01 to DSR-17 |
| Confirmed | None |

| Milestone | Entries that block it |
|---|---|
| Preliminary development (DEV) | None. Development may proceed with synthetic data |
| Technical integration testing (TIT) | DSR-06 (mapping), DSR-09 (network), DSR-11, DSR-14, DSR-15 |
| Joint UAT (UAT) | DSR-02, DSR-03, DSR-06, DSR-07, DSR-11, DSR-12, DSR-15, DSR-16 |
| Production exchange (PROD) | DSR-01 to DSR-05, DSR-08 to DSR-10, DSR-13, DSR-18 |
| Final acceptance or go-live (GL) | DSR-01, DSR-12, DSR-17, DSR-18 |

The only named persons are those already recorded in the action register: Isaiah, and Rantsala. The only target date is the 13 November 2026 environment target recorded at [M4], which is explicitly not guaranteed.

## Deliverable 5 — Cross-document correction log

None of these has been made.

### Mandatory consistency corrections

| # | Location | Conflict | Proposed minimal correction |
|---|---|---|---|
| M-1 | Section 1.4, "Consent capture" row (line 289) and "Consent at referral" row (line 306) | "Transmission of consent status to CPIMS+ is proposed" with no lawful-basis distinction | Append: "Consent states (Given, Declined, Withdrawn, Not Obtainable) are recorded separately from the applicable lawful basis; consent is not the only lawful basis (section 7.2)." |
| M-2 | Section 1.7 (line 335) and 1.8, decision 4 (line 350) | Consent framed as the main open item | Add "and the lawful basis for each disclosure scenario (section 7.2; DSR-02, DSR-03)". |
| M-3 | Section 3.3, "Consent and withdrawal" row (line 590) | "[RV3] specifies given, declined, withdrawn, not obtainable or approved alternative lawful basis" | Keep the historical row unchanged. Append: "Refined by DATA-SEC-002: four consent states, with lawful basis recorded separately." |
| M-4 | Section 5, Table 5.2, "Consent and lawful basis" row (line 990) | Lists five "states", including lawful basis | Change to "…using the consent states Given, Declined, Withdrawn or Not Obtainable, with the applicable lawful basis recorded separately (section 7.2)…". Note that I wrote this row in the Section 5 revision. |
| M-5 | Section 8.1 work plan, "API integration" row (formerly lines 1774–1778) | — | **Resolved by the Section 8 revision.** Phase 5 is now "BITZ Gateway and Primero API integration", with no return path or attachments | — |
| M-6 | Section 8.8, item 3 (formerly line 1986) | — | **Resolved by the Section 8 revision.** Decision 3 now reads "Confirm the validated outbound-only scope and the outstanding Primero API capability details" | — |
| M-7 | Section 9.7 change log, CR-01 (formerly line 2137) | — | **Resolved by the Section 9 revision.** Table 9.7 records the outbound-only technical disposition and keeps the historical row | — |
| M-8 | Section 11.4, item 2 | — | **Resolved in Section 11 by the Section 11 revision.** Table 11.4 row 2 links DATA-012 to DSR-02 and DSR-03 and the four consent states | — |
| M-9 | Section 11.4, item 8 | — | **Resolved in Section 11 by the Section 11 revision.** Table 11.4 row 8 links DSR-05 and DSR-09 | — |
| M-10 | Section 11.1, R-006 and R-010 | — | **Resolved in Section 11 by the Section 11 revision.** Table 11.1b gives the outbound-only mitigations. **Annex G R-006 and R-010 rows still need the same qualification** (see Section 11 record) | — |
| M-11 | Annex A, DATA-012 (line 3271), and Annex J, DATA-012 current row (line 3957) | "consent given, declined, withdrawn or not obtainable, or an approved alternative lawful basis" | Append to **Current**: "Lawful basis is recorded separately from the consent state (DATA-SEC-002)." The wording is otherwise consistent. |
| M-12 | Annex C.1, "Consent and disclosure" row (line 3419) | "states defined in [RV3]" | Change to "states defined in section 7.2 (DATA-SEC-002)". |
| M-13 | Annex H, S-04 and S-07 | — | **No change needed (checked during the Section 10 revision).** Both are already labelled "Future — contract addendum required … excluded from initial UAT / acceptance" | — |
| M-14 | Annex K.2.1–K.2.6 (lines 4202–4288) | A duplicate of the pre-revision Section 7: the old 7.3 control table with "OpenFN if used", "return updates" and the old inbound flow | Replace with "Annex K.2 — Detailed data safeguards: see section 7 (revised); implementation-specific evidence to be added here as it is produced." Alternatively, replace each K.2 subsection with the matching revised Section 7 text. This also covers Section 6 record items K-9 to K-11. |
| M-15 | Annex J (new requirements) | Encryption at rest and tamper-evident audit have no requirement ID | Record them as DATA-SEC-003 validation references in an Annex E table. Optionally propose new SEC IDs; the 68-item baseline count would then change, so this needs the owner's decision. |

### Checked and consistent

- **Section 4.4:** attachments are excluded and SCOPE-003 metadata is conditional, which matches Table 7.1.
- **Section 5:** anonymity, the datasets, Send Update and Ministry ownership all match. The only exception is the consent row, item M-4.
- **Section 6:** the architecture, ledger, minimisation and retention wording match.
- **Section 8.5:** "Real case data will not be exchanged until…" is consistent; it was retained in the Section 8 revision.
- **Annex D.4:** no conflict.
- **Annex A and J SEC-001 to SEC-007:** consistent.

### Optional improvements

- O-1: Add [RV7] to the Annex I.1 source register, alongside RV3–RV6.
- O-2: Add "Annex E.6 — DATA-SEC-001–DATA-SEC-006" for traceability, following the pattern of E.3.
- O-3: Add Tables 7.1–7.4 to the front-matter lists if a tables list is introduced.
- O-4: **Version labels (flag only).** The Word header says "Version 2.8", the Word footer says "Version 2.8 — pending formal approval", and the Markdown title block says "Version 2.8 — Post-Validation Revision · 9 November 2026". No new version number has been assigned.

## Deliverable 6 — Safeguarding and security UAT checklist

None of these has been executed. "Cond." means the test is conditional on the register entry shown.

| # | Scenario | Expected result | Evidence required | Annex H / cond. |
|---|---|---|---|---|
| 1 | Anonymous reporter referral | No reporter identifiers in the payload, ledger, logs or support views | Payload capture; log extract | F-03 |
| 2 | Missing child identity (approved partial) | Referral accepted with the missing items recorded, the exception category and the actor | Ledger and OPENCHS record | New; DSR-06 |
| 3 | Emergency referral with reduced dataset | Accepted only with the approved emergency fields; exception recorded | Test log | F-05; DSR-06 |
| 4 | Consent Declined, and Not Obtainable | Disclosure follows the approved rule; lawful basis recorded separately; no automatic final determination | Test log; audit record | S-06; DSR-03 |
| 5 | Approved lawful-basis exception | Exception authorised by an approved role; reason recorded | Audit record | New; DSR-02 |
| 6 | Sensitive allegation narrative | Narrative is not in the ledger or logs; only authorised roles can view it | Log extract; role test | S-03 |
| 7 | Failed electronic delivery | Technical state Failed or Needs Action; alert raised; telephone escalation unaffected | Alert record; exercise record | RC-04, B-02 |
| 8 | Telephone escalation during an API outage | Escalation completed without waiting for electronic submission | Exercise record | B-02 |
| 9 | Duplicate submission and uncertain outcome | One CPIMS+ case; reconciliation recorded | Ledger | RC-01, RC-02 |
| 10 | Supplementary update | Send Update against the existing UUID; no new case | Ledger; Primero record | F-13; DSR-14 |
| 11 | Authorised correction and withdrawal request | Audited; not shown as a confirmed Ministry action until confirmed | Audit record; UI capture | F-19 |
| 12 | Delivered compared with Accepted | Delivered never shown as acceptance | UI capture | F-11 |
| 13 | Role-based permissions | Unauthorised users cannot initiate, amend, view or recover | Role test matrix | S-02; new |
| 14 | Authentication | Approved mechanism only; token renewal behaves as verified | Test log | S-01, RC-08; DSR-14 |
| 15 | TLS and certificates | Invalid certificate rejected; TLS 1.2 or higher | Scan or test output | S-05 |
| 16 | Encryption at rest | Sensitive gateway records and backups encrypted | Configuration evidence | New |
| 17 | Secrets | No secrets in code, logs or configuration exports; rotation demonstrated | Review record | New |
| 18 | Audit-log redaction and tamper evidence | Sanitised logs; tampering detectable | Log extract; integrity check | S-03, AU-01; new |
| 19 | Environment isolation and synthetic data | No real records in test; environments separated | Data check | S-08; DSR-11 |
| 20 | Retention and deletion | Applied as approved | Retention configuration | New; DSR-08 |
| 21 | Absence of automatic inbound updates | No inbound status or intervention channel exists | Negative test | New (S-04 and S-07 future) |
| 22 | Absence of attachments, recordings and case plan | None in the payload | Payload capture | F-16 |
| 23 | Lesotho-specific verification | All of the above repeated in the Lesotho environment; global demonstration results not sufficient | Environment record | New; DSR-15 |

Security testing also requires documented remediation of relevant vulnerabilities before production (Table 7.2, "Verification" row). No penetration-testing result or certification has been assumed.
