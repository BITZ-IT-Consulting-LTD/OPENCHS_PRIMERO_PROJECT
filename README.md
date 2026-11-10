# Lesotho OpenCHS – Primero CPIMS+ integration

Project workspace for the electronic referral integration between **OPENCHS** (Child Helpline 116, Lesotho) and **Primero CPIMS+** (Ministry of Gender, Youth and Social Development), delivered by BITZ IT Consulting.

> **This repository is public.** Contracts, meeting minutes, transcripts, attendance records, correspondence and client-internal policies are deliberately excluded (see [.gitignore](.gitignore)). Never commit real child data, credentials, tokens or contract amounts.

## What is being built

```
OPENCHS  →  BITZ Integration Gateway  →  Primero CPIMS+ API (Lesotho)
```

- **OPENCHS:** an agent explicitly chooses **Refer to CPIMS+**, selects a Ministry-approved service, and confirms the referral. Saving a case never sends a referral. **Send Update** is a separate action for follow-up information.
- **Gateway:** JWT authentication, mapping of the minimum necessary data, a persistent queue with retries (1, 5, 30 and 120 minutes), duplicate prevention, reconciliation of uncertain outcomes, and a metadata-only audit log.
- **Primero CPIMS+:** the Ministry accepts or rejects referrals, distributes them and assigns caseworkers.
- **Out of scope for the initial delivery:** automatic inbound status updates, attachments, case plans, direct routing to service providers, and OpenFN or X-Road. Bringing any of these in would need a contract addendum.

## Deliverables and agreed dates

| Deliverable | Content | Agreed date | Milestone |
|---|---|---|---|
| **D1** | Inception, requirements and environment set-up | 13 Nov 2026 | [D1](https://github.com/BITZ-IT-Consulting-LTD/OPENCHS_PRIMERO_PROJECT/milestone/1) |
| **D2** | Optional ABR ID field and checks; explicit referral control | 20 Nov 2026 | [D2](https://github.com/BITZ-IT-Consulting-LTD/OPENCHS_PRIMERO_PROJECT/milestone/2) |
| **D3** | Outbound REST API client: JWT, retry, offline queue, idempotency, audit | 11 Dec 2026 | [D3](https://github.com/BITZ-IT-Consulting-LTD/OPENCHS_PRIMERO_PROJECT/milestone/3) |
| **D4** | Testing, Ministry-led UAT, training (Maseru), go-live and handover | 26 Feb 2027 | [D4](https://github.com/BITZ-IT-Consulting-LTD/OPENCHS_PRIMERO_PROJECT/milestone/4) |

**Delivery gates:**
- **G1:** D1 approved (13 Nov)
- **G2:** Lesotho test environment and credentials in place (13 Nov)
- **G3:** D3 evidence submitted (11 Dec)
- **G4:** Lesotho integration verified (22 Jan)
- **G5:** UAT signed off (5 Feb)
- **Go/no-go:** written production decision before go-live (8–12 Feb)

Support continues under the existing support provisions until 7 Jul 2027.

The work is tracked in [GitHub Issues](https://github.com/BITZ-IT-Consulting-LTD/OPENCHS_PRIMERO_PROJECT/issues). Each issue maps to requirement IDs in Annex A of the inception report. Labels:
- **Deliverable:** `D1`–`D4`
- **Item type:** `gate`, `decision` (OD-01 to OD-13), `dependency`
- **Work type:** `type-build`, `type-test`, `type-governance`
- **Owner:** `owner-bitz`, `owner-primero`, `owner-ministry`, `owner-unicef`
- **Status:** `critical-path`, `blocked`

## Current status

- **D1 Inception Report v2.9 (final draft)** has been submitted for stakeholder approval. Written approval is pending.
- **G2 is the critical dependency:** Primero must supply the Lesotho test environment, credentials, field identifiers and service list. Until then, development runs against a mock API.
- **Open decisions** are tracked as issues:
  - OD-01: written UNICEF disposition of two-way updates and attachments
  - OD-09: official ABR ID rules
  - OD-02 to OD-04: Ministry rules for rejection feedback, corrections and anonymity
  - OD-05 to OD-13: safeguarding decisions and production authorisation

## Key documents

- [D1 Inception Report v2.9 — Markdown](01_inception/D1_INCEPTION_REPORT_OPENCHS_PRIMERO_V2.9_FINAL_DRAFT.md) · [Word](01_inception/D1_INCEPTION_REPORT_OPENCHS_PRIMERO_V2.9_FINAL_DRAFT.docx)
- [v2.9 consolidation register](01_inception/D1_V2.9_CONSOLIDATION_REGISTER.md)
- [Outstanding decisions](01_inception/INCEPTION_OUTSTANDING_DECISIONS.md) · [D1 acceptance readiness](01_inception/D1_ACCEPTANCE_READINESS.md)
- [Contract-aligned delivery plan](02_project_management/CONTRACT_ALIGNED_DELIVERY_PLAN.md)
- [OpenCHS–Primero integration context](05_technical_reference/OPENCHS_PRIMERO_INTEGRATION_CONTEXT.md) · [Primero CPIMS+ context](05_technical_reference/12_PRIMERO_CPIMS_CONTEXT.md)
- [Technical scope brief](07_source_documents/Lesotho_OpenCHS_Technical_Scope_Inception_Brief.pdf)

## Folder guide

| Folder | Contents |
|---|---|
| [01_inception](01_inception/README.md) | D1 inception report versions, annexes, revision records, QA and consistency audits |
| [02_project_management](02_project_management/README.md) | Delivery plan, decision document, checklists, update and validation records |
| [03_meetings](03_meetings/README.md) | Facilitation slides and notes, meeting reports (minutes and transcripts are kept locally, not in Git) |
| [04_templates](04_templates/README.md) | Capture forms, registers and the Workstream 1 workbook |
| [05_technical_reference](05_technical_reference/README.md) | OpenCHS architecture, Primero CPIMS+ context and integration reference |
| [07_source_documents](07_source_documents/README.md) | Technical scope brief and planning presentations (contracts are held outside this repository) |
| [08_archive](08_archive/README.md) | Superseded versions in dated folders |

`06_correspondence/` and the upstream `primero/` source clone exist locally only.

## Working rules

1. Keep the current report in `01_inception/`, and keep its Word copy aligned with the Markdown.
2. Move superseded versions into a dated folder under `08_archive/previous_versions/`.
3. Treat API documentation, example fields and URLs as references until they are verified on the Lesotho environment. Label evidence as Level 1 (development), Level 2 (simulated) or Level 3 (Lesotho). Only Level 3 evidence supports G4.
4. Use synthetic data in every non-production environment.
5. Do not mark access, testing, approval or go-live as complete without supporting evidence.
6. Before committing, check new files against the sensitive categories in `.gitignore`.
