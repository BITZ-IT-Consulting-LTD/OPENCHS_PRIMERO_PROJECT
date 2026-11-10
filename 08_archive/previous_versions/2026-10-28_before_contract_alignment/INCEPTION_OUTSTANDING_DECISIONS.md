# Inception Outstanding Decisions Register
## OpenCHS–Primero CPIMS+ Integration — D1

**Date:** 27 October 2026  
**Status:** Working register for D1 v0.9 review  
**Relationship to controlled registers:** The [Inception Completion Inventory](INCEPTION_COMPLETION_INVENTORY.md) remains the controlled source for requirement status, and the [Session 3 action tracker](../03_meetings/session_3/SESSION_3_ACTION_TRACKER_2026-10-26.xlsx) for actions. This register **groups the open decisions by decision-maker** for the D1 review. It links to inventory and action IDs and does not set a separate status. When a decision is made, record it in the inventory or tracker and the decision register, then mark it here.

**Gate:** *Design* = needed before detailed design sign-off; *Test* = needed before integration testing; *D1* = needed for formal D1 acceptance; *Later* = D4 or go-live.

## 1 UNICEF

| Ref | Decision required | Linked IDs | Gate | Notes |
|---|---|---|---|---|
| OD-U1 | Contract treatment of two-way updates and attachments: absorb in D3/D4, contract variation, or phase; acceptance evidence | R-010; CR-01; CR-02; CD-01; CD-04 | Design | Session 3 agreement is not a contract variation (report §9) |
| OD-U2 | Which dates govern milestones, acceptance and payment (10 Mar 2025 – 7 Jul 2027 or 1 Jul 2026 – 28 Feb 2027) | CD-02; GOV-006 | D1 | |
| OD-U3 | D1 status: accepted, conditionally accepted, or resubmit; approval of a rebaselined schedule | R-009; CR-03 | D1 | August target passed |
| OD-U4 | Named UNICEF approver and escalation route | GOV-003; R-014 | D1 | |
| OD-U5 | Confirm owner for A-017/A-019: Daniel, Lekhanya, or both | P-03 | D1 | Attendance export names Ramoletane Lekhanya; minutes discussion names Daniel. UNICEF to reconcile identity and confirm A-017/A-019 ownership |
| OD-U6 | Confirm 14-week plan is historical, contract months govern | CD-07 | D1 | Session 1 minutes say "contracted 14-week window" |
| OD-U7 | Confirm D2/D4 acceptance wording: "save-event trigger" reads as manual referral control | CD-03; R-015; CR-04 | Design | Needed before the D2 demonstration |

## 2 Ministry (MGYSD / Ministry of Social Development) and Child Helpline

| Ref | Decision required | Linked IDs | Gate | Notes |
|---|---|---|---|---|
| OD-M1 | Named business owner and requirements approver | GOV-001 | D1 | |
| OD-M2 | Minimum child-identification dataset and emergency exceptions | WF-004; DATA-005; D-003; D-011 | Design | Do not create fictitious values to satisfy validation |
| OD-M3 | Consent or other lawful basis at referral; who may override CPIMS+ consent | DATA-012; R-011; SEC-001 | Design | Upstream Primero checks consent at referral |
| OD-M4 | Applicable data protection instrument and status (with UNICEF) | A-017; A-022; SEC-001 | D1 | Sources cite 2011, 2012, and "under development" |
| OD-M5 | Direct API or OpenFN connection | API-009; D-015 | Design | D-015 leaves this to the Ministry |
| OD-M6 | Service-to-recipient configuration and accept/reject reason rules | RT-003; D-008 | Design | Depends on A-018 |
| OD-M7 | Helpline-facing status vocabulary | RT-006; Report Annex D.3 | Design | Proposed states in Annex D.3 |
| OD-M8 | Permitted return-update fields (with Primero) | RT-007; SEC-008 | Design | |
| OD-M9 | Supervisor escalation, correction, cancellation and re-referral rules | WF-003; WF-006 | Design | |
| OD-M10 | ABR sex-digit mismatch handling (warn / block / accept) | FN-002; D-014 | Design | |
| OD-M11 | Attachment types, size, retention and permissions | DATA-010 | Design | |
| OD-M12 | Retention for integration data, logs and attachments | OPS-004; OPS-005 | Test | |
| OD-M13 | Named UAT testers, accounts and signatories; confirm checklist positions (CHL supervisor; BITZ test data; MGYSD sign-off) | UAT-002; UAT-010 | Test | |
| OD-M14 | Approve synthetic test dataset | UAT-003; SEC-007 | Test | |
| OD-M15 | Defect severity and conditional go-live rules | UAT-007 | Test | Proposed table in report §10.3 |
| OD-M16 | Permanent Child Helpline focal person and leave cover | A-002; A-024; GOV-002 | D1 | |
| OD-M17 | Support and incident owners | OPS-006; OPS-007 | Later | |
| OD-M18 | Data protection / security approver | Report §12.1 | D1 | |

## 3 Primero

| Ref | Decision or confirmation required | Linked IDs | Gate | Notes |
|---|---|---|---|---|
| OD-P1 | Deployed Lesotho release and base URLs | GOV-004 | Design | |
| OD-P2 | Environment: Lesotho sandbox or global playground, with access package | A-015; A-016; API-007 | Test | Fallback agreed (D-018) |
| OD-P3 | CPIMS+ service list | A-018; RT-001 | Design | |
| OD-P4 | Unattended authentication flow, token renewal, credential issue and rotation | API-002; R-013 | Design | SSO preference concerns users |
| OD-P5 | Operation sequence for create, refer, follow-up, attachments | API-003 | Design | |
| OD-P6 | Client-generated UUID support and `409` reconciliation in the Lesotho deployment | OPS-003 | Design | |
| OD-P7 | Return mechanism: webhook availability, triggering events, role, or polling | RT-007 | Design | Webhook does not retry in v2.16.0 |
| OD-P8 | Network prerequisites: TLS, certificates, VPN, allowlisting | SEC-005 | Test | Isaiah answered "Yes" without detail |
| OD-P9 | Configured consent checks | R-011 | Design | |
| OD-P10 | Lesotho Primero go-live plan | R-012 | D1 | Timelines coupled (Session 1 §10) |
| OD-P11 | Configured field definitions, lookups and protection-concern list | DATA-005–DATA-009 | Design | After sandbox setup |
| OD-P12 | Outage handling (with BITZ) | A-021; OPS-001 | Design | "28 Oct or during testing" |

## 4 BITZ

| Ref | Decision or output required | Linked IDs | Gate | Notes |
|---|---|---|---|---|
| OD-B1 | Circulate v0.9 and track comments | A-025 | D1 | |
| OD-B2 | Propose outage, retry and idempotency design for A-021 session | A-021; OPS-001–003 | Design | Proposals in report §6 and Annex D.4 |
| OD-B3 | Effort and schedule estimate for return updates once mechanism agreed | R-010; CR-01 | Design | Not estimated in v0.9 |
| OD-B4 | Dated rebaseline proposal after A-016 and OD-U1 | R-009 | D1 | |
| OD-B5 | Verify OpenCHS case model, queue, permissions, audit and secret management | Report §6.5 | Design | |
| OD-B6 | Add v0.9 proposed requirement IDs to the inventory | Report Annex J | D1 | FN, SEC, AUD, WF-010, DATA-012/013, OPS-008, UAT-010 |
| OD-B7 | Data protection desk research | A-022 | D1 | |
| OD-B8 | Regenerate Word copy from v0.9 | — | D1 | |

Evidence update — 28 October 2026: see the current report’s Session 3 evidence reconciliation. A-014 document receipt is evidenced; applicability remains pending. Separate pathways/privacy actions and formal D1 approval remain open. The historical 26 October spreadsheet tracker has not been rewritten; use this update for the corrected A-014 status.
