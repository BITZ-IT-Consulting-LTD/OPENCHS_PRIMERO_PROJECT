# Inception Report Submission Quality Checklist
## D1 Inception Report v0.7

**Date:** 27 October 2026  
**Reviewed document:** [DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO_V0.7.md](DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO_V0.7.md)  
**Result key:** **Pass** — check satisfied; **Fail** — defect needing correction before the stated use; **Pending** — depends on an external input or decision.

## 1 Summary

| Area | Pass | Fail | Pending |
|---|---:|---:|---:|
| Completeness | 13 | 0 | 3 |
| Requirements consistency | 7 | 0 | 0 |
| Technical consistency | 6 | 0 | 2 |
| Contractual alignment | 4 | 0 | 3 |
| Governance consistency | 3 | 0 | 3 |
| Security consistency | 4 | 0 | 2 |
| Traceability | 6 | 0 | 0 |
| Presentation | 5 | 1 | 0 |
| Stakeholder readiness | 1 | 0 | 5 |

The one **Fail** (Word copy not regenerated) blocks circulation only if the draft is circulated in Word. The **Pending** items block formal acceptance, not draft circulation.

## 2 Checks

### 2.1 Completeness

| # | Check | Result | Note |
|---|---|---|---|
| C1 | Cover page and document control | Pass | §1 |
| C2 | Executive summary: achieved, outstanding, to approve | Pass | §2.3–2.8 |
| C3 | Background, system roles, intended outcomes | Pass | §3 |
| C4 | Objectives and expected results | Pass | §4 |
| C5 | Scope and contractual framework | Pass | §5 |
| C6 | Methodology and consultations | Pass | §6 |
| C7 | Categorised requirements with acceptance | Pass | §7; Annex A |
| C8 | Architecture diagrams A–D and supporting figures 1–15 | Pass | List in §1.3; all 18 Mermaid diagrams render with mermaid-cli 11.12 |
| C9 | Implementation methodology mapped to D1–D4 | Pass | §9 |
| C10 | Work plan with baseline, status, parallel work, recovery, decisions | Pass | §10 |
| C11 | Governance, RACI, communication, escalation | Pass | §11 |
| C12 | Security framework | Pass | §12 |
| C13 | UAT plan and acceptance criteria | Pass | §13; Annex H |
| C14 | Field mapping baseline | Pending | Configured definitions not received (Annex C) |
| C15 | Environment-setup evidence | Pending | No access (A-016) |
| C16 | Approval record | Pending | No approvers named (§18) |

### 2.2 Requirements consistency

| # | Check | Result | Note |
|---|---|---|---|
| R1 | All Session 3 decisions D-005–D-018 present with wording consistent with the minutes | Pass | Annex E.1; each ID referenced throughout |
| R2 | Manual agent trigger; no save-triggered referral | Pass | WF-002, FN-003; conflicting plan wording flagged as CD-03 |
| R3 | Two-way updates retained and not absorbed into D3 silently | Pass | §15 |
| R4 | Anonymous reporter allowed; child identity required | Pass | WF-009; F-03, F-04 |
| R5 | ABR optional; NICR structural format | Pass | FN-001/002; Annex C.2 |
| R6 | Narrative at referral; attachments included; case plan excluded | Pass | FN-004, FN-011; Annex C.1 |
| R7 | Superseded positions (direct-to-district routing, anonymous non-referral, one-way scope, attachment deferral) appear only as history | Pass | §6.3; Annex E |

### 2.3 Technical consistency

| # | Check | Result | Note |
|---|---|---|---|
| T1 | Operations in diagrams match Annex B | Pass | |
| T2 | Idempotency (client UUID, 204/409) consistent across §8, Annex B.3, RC-01 | Pass | Verified against local v2.16.0 `doc/api/cases/post.md` |
| T3 | Service routing reflects user-addressed API referrals | Pass | RT-003; Annex B.2 |
| T4 | Return-update options presented as options, with webhook no-retry caveat | Pass | Verified against `app/jobs/webhook_job.rb` |
| T5 | Upstream capability not presented as Lesotho configuration | Pass | §8 banner; Annex B.1 |
| T6 | OpenFN and X-Road shown as option / separate workstream | Pass | Diagram A |
| T7 | Lesotho release and URLs | Pending | GOV-004 |
| T8 | Authentication flow for unattended integration | Pending | API-002; R-013 |

### 2.4 Contractual alignment

| # | Check | Result | Note |
|---|---|---|---|
| K1 | D1–D4 represented with recorded target months | Pass | §5.1; §10.1 |
| K2 | Original D1 milestone shown as passed; D2 window closing | Pass | §10 |
| K3 | Discrepancies identified | Pass | CD-01–CD-07 |
| K4 | New outputs marked as proposed supporting outputs | Pass | §9 |
| K5 | Governing contract dates | Pending | CD-02 |
| K6 | Contract treatment of two-way and attachments | Pending | R-010 |
| K7 | Contract document available for verification | Pending | Not filed; brief used |

### 2.5 Governance consistency

| # | Check | Result | Note |
|---|---|---|---|
| G1 | Action owners and dates match the Session 3 tracker | Pass | Annex F.1 |
| G2 | RACI entries cite evidence or are marked TBC / proposed | Pass | §11.2 |
| G3 | New cadences labelled Proposed | Pass | §11.4 |
| G4 | Named approvers | Pending | GOV-001, GOV-003 |
| G5 | UNICEF action owner identity (Daniel / Lekhanya) | Pending | P-03 |
| G6 | Child Helpline focal person and cover | Pending | A-002, A-024 |

### 2.6 Security consistency

| # | Check | Result | Note |
|---|---|---|---|
| S1 | Consent dependency identified | Pass | DATA-012; R-011 |
| S2 | No legal instrument asserted | Pass | §12.1 |
| S3 | Test-data safeguards stated | Pass | SEC-007; S-08 |
| S4 | Logging excludes tokens and full payloads | Pass | SEC-006; S-03 |
| S5 | Lawful basis | Pending | A-017; A-022 |
| S6 | Network prerequisites from Primero | Pending | OD-P8 |

### 2.7 Traceability

| # | Check | Result | Note |
|---|---|---|---|
| X1 | Decision, action and risk IDs preserved | Pass | D-001–D-018; A-001–A-025; R-001–R-012 |
| X2 | New IDs flagged as proposed additions | Pass | §7 preamble; R-013–R-015 |
| X3 | Every test ID referenced is defined in Annex H | Pass | Script check: 40 defined, none undefined |
| X4 | Sources listed with dates; unavailable sources listed | Pass | Annex I |
| X5 | v0.6 content retained or relocated | Pass | Improvement Log §2 |
| X6 | Internal Markdown links resolve | Pass | Script check |

### 2.8 Presentation

| # | Check | Result | Note |
|---|---|---|---|
| P1 | Section numbering follows recommended structure 1–19 | Pass | |
| P2 | Consistent status classifications | Pass | Legend §1.1 |
| P3 | Acronyms not expanded beyond sources | Pass | Annex I.3 |
| P4 | Low-level API detail in annexes | Pass | Annex B |
| P5 | Diagrams labelled Proposed Architecture | Pass | §8 |
| P6 | Word copy aligned with Markdown | **Fail** | Word copy predates v0.6; regenerate before Word circulation |

### 2.9 Stakeholder readiness

| # | Check | Result | Note |
|---|---|---|---|
| H1 | No unsupported claims of access, testing, approval or completion | Pass | |
| H2 | Distribution list confirmed | Pending | |
| H3 | Review deadline and comment method set | Pending | |
| H4 | README / `inception.md` point to v0.7 | Pending | Still describe v0.5 |
| H5 | Session 3 minutes circulated for correction (S3-N01) | Pending | No evidence filed |
| H6 | Child Helpline frontline review of Session 3 decisions | Pending | No agent or social worker attended Session 3 |

## 3 Incomplete sections that prevent formal acceptance

1. Field mapping (Annex C) — configured definitions and service list outstanding.
2. Environment setup (§8.6) — no access evidence.
3. Review and approval (§18) — no approvers named.
4. Scope and change control (§15) — governance decision outstanding.
5. Work plan (§10.5) — no approved rebaseline.
