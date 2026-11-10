# Lesotho OpenCHS–Primero Project

Documentation-only repository for planning and delivering the integration of the Lesotho Child Helpline 116 / OpenCHS environment with Primero CPIMS+.

## Repository purpose

This repository is the controlled documentation baseline for:

- Inception and requirements
- Integration decisions
- OpenCHS-to-Primero data mapping
- ABR ID and referral workflow definition
- API, authentication, retry, offline queue, idempotency, and audit requirements
- Testing, UAT, training, handover, and go-live planning

The repository does not currently contain the OpenCHS application source code. Statements describing implementation must be verified against the actual OpenCHS and Primero environments before being treated as completed work.

## Key documents

- `Lesotho_OpenCHS_Technical_Scope_Inception_Brief.pdf` — source technical scope and contractual workstreams
- `Lesotho_OpenCHS_Implementation_Timeline_Presentation.pptx` — original 14-week implementation timeline
- `docs/DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO.md` — D1 inception baseline
- `docs/CONTRACT_ALIGNED_DELIVERY_PLAN.md` — contract dates, milestone schedule, acceptance gates, dependencies, and payment controls
- `docs/OPENCHS_PRIMERO_FIRST_MEETING_DECISION_DOCUMENT.md` — first-meeting decisions and questions
- `docs/OPENCHS_PRIMERO_TWO_WEEK_PROJECT_CHECKLIST.md` — delivery checklist
- `docs/FOURTEEN_WEEK_IMPLEMENTATION_SLIDE_NOTES.md` — slide notes for the original 14-week plan
- `docs/docs/platform/reference/OPENCHS_PRIMERO_INTEGRATION_CONTEXT.md` — technical integration context
- `docs/context/12_PRIMERO_CPIMS_CONTEXT.md` — integration architecture context

## Documentation status rules

- `Draft` means the content requires review or approval.
- `Proposed` means a design option has been suggested but not approved.
- `TBD` means the required information is not yet available.
- `Implemented` must only be used after verification in the relevant source or environment.

## Working approach

1. Record decisions in the decision document and action register.
2. Keep the requirements and field mapping under version control.
3. Mark unresolved external dependencies as blockers.
4. Do not promote draft assumptions into production requirements without owner approval.
5. Update the README when the repository structure or delivery baseline changes.

## Current delivery baseline

The commercial delivery baseline is the contract-aligned plan: 1 July 2026 to 28 February 2027, with milestone targets in August 2026, October 2026, November 2026, and February 2027. The 14-week and two-week materials are retained as technical planning references; they are not the commercial schedule unless formally approved as a rebaseline.
