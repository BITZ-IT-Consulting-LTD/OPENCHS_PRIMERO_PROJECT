# D1 Acceptance Readiness Assessment
## Inception, Requirements & Environment Setup

**Date:** 27 October 2026  
**Assessed version:** [D1 Inception Report v0.9](DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO_V0.9.md)  
**Acceptance gate (delivery plan, Item 10):** approved inception report, technical design, mapping baseline and environment-setup evidence. The delivery plan also says acceptance cannot be shown solely by the existence of documents; the approval record, named approver, environment evidence and treatment of outstanding dependencies must be kept.

## 1 Verdict

| Question | Answer |
|---|---|
| Ready for **draft circulation** to stakeholders? | **Yes**, subject to the circulation conditions in section 2 |
| Ready for **formal D1 acceptance**? | **No** |
| Could D1 be **conditionally accepted**? | Possibly, if approvers accept the open items in section 2.2 as bounded dependencies with owner and milestone. That is a governance decision, not a BITZ determination |

## 2 Assessment against the Item 10 gate

| Gate element | Evidence available | Assessment |
|---|---|---|
| Approved inception report | v0.9 draft; no approver named; no approval recorded | **Not met** |
| Technical design | Proposed architecture, diagrams and API analysis (report §6, Annex B); not validated against an environment; no technical approver | **Partly met** (prepared, not validated or approved) |
| Mapping baseline | Business field set confirmed (D-012); configured field definitions, service list and code lists not received | **Not met** (business baseline only) |
| Environment-setup evidence | OpenCHS test/UAT being stood up; no Primero access; no authenticated test call | **Not met** |
| Decision, risk, action, dependency and issue registers | Annexes E–G; inventory; action tracker | **Met** (maintained; to be kept current) |
| Kickoff workshop with UNICEF, Ministry, Child Helpline, Primero | Sessions 1–3 held; UNICEF attended Session 3 only; 24 Sep meeting has no minutes | **Substantially met**; evidence gap for 24 Sep |

## 3 Conditions for formal acceptance

### 3.1 Must be closed

1. Named approvers for requirements and the report (OD-U4, OD-M1).
2. Governance decision on contract treatment of two-way updates and attachments, or explicit acknowledgement that it will be decided before D3 design sign-off (OD-U1).
3. Governing contract dates and D1 status confirmed (OD-U2, OD-U3).
4. Confirmation of current applicability and mapping review of the received September 2019 SOP (A-014), and receipt/review of national pathways (A-013), with any changes to report Annex J recorded.
5. Environment-setup evidence: Primero sandbox or playground access, and an authenticated test call, **or** written acceptance that environment evidence moves to a later gate (A-015, A-016, A-023).
6. Stakeholder comments on v0.9 resolved and a version issued for approval.

### 3.2 May be accepted as bounded dependencies (each needs owner, milestone and approver agreement)

| Item | Owner | Proposed milestone |
|---|---|---|
| Configured field mapping and service-to-recipient configuration (P-02, A-018, RT-003) | Isaiah / Ministry / BITZ | Before D3 design sign-off |
| Minimum dataset and emergency exceptions (WF-004) | Ministry | Before D2 acceptance |
| Consent / lawful basis (DATA-012, A-017, A-022) | Ministry / UNICEF | Before integration testing |
| Authentication flow (API-002) | Primero / BITZ | Before integration testing |
| Return-update mechanism (RT-007) | Primero / BITZ / Ministry | Before D3 design sign-off |
| Outage handling (A-021) | Nelson / Peter / Isaiah | Before integration testing (minutes allow "during testing") |
| Residual ABR verification (A-007) | Ministry / relevant authority | Not blocking (ABR optional) |
| Named UAT testers and signatories (UAT-002) | Ministry | Before UAT preparation |

## 4 Conditions for draft circulation

| Condition | Status |
|---|---|
| All Session 3 decisions reflected without change | Met (QA checklist) |
| No unsupported claims of access, testing, approval or completion | Met (QA checklist) |
| Distribution list confirmed | **Pending** — Session 3 attendees plus Tiisetso Mohlabi and the Child Helpline focal person or cover are suggested |
| Covering note states the review deadline and how to comment | **Pending** |
| Format: Markdown, or Word/PDF regenerated from v0.9 | **Pending** — Word copy is out of date |
| README and `inception.md` updated to point to v0.9 | **Pending** |

## 5 Evidence gaps that weaken acceptance even after approval

- Contract No. 43427866 Amendment 3 is not filed; scope is taken from the brief.
- No minutes for the 24 September inception meeting or the 14 October technical call.
- Frontline Child Helpline representation in Session 3 requires role confirmation against the attendance export.
- Unified national referral form (A-004) recorded as shared but not filed.

Evidence update — 28 October 2026: see the current report’s Session 3 evidence reconciliation. A-014 document receipt is evidenced; applicability remains pending. Separate pathways/privacy actions and formal D1 approval remain open. The historical 26 October spreadsheet tracker has not been rewritten; use this update for the corrected A-014 status.
