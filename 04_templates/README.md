# Lesotho Child Helpline 116 / OpenCHS — Workstream 1 templates

These editable templates were created from the supplied **Lesotho Child Helpline 116 / OpenCHS — Workstream 1 Inception** facilitator workbook.

The pack includes the eight live-capture worksheets, the decision/action/open-issues registers, and the final inception close-out checklist described in the workbook. Word files are provided for facilitated completion; `Workstream_1_Inception_Capture_Workbook.xlsx` provides a consolidated structured-capture option.

## Files

1. Stakeholder / Responsibility Matrix
2. Referral Lifecycle Capture
3. ABR ID Requirements
4. Field-Mapping Worksheet
5. API / Environment Matrix
6. API Contract Capture
7. Reliability, Logging and Support Controls
8. UAT and Acceptance Matrix
9. Decision Register
10. Action Register
11. Open Issues Register
12. Inception Close-out Checklist
13. Workstream 1 Risk Record — Primero Sandbox Access
14. Potential Sponsor Escalation Email — Primero Sandbox Risk

The templates intentionally leave unconfirmed values blank or marked for confirmation. Do not place credentials, secrets, or sensitive child-protection data in the templates.

The earlier pack was partially prefilled from `SESSION_1_MEETING_REPORT_DRAFT.md` and the supplied Session 1 minutes PDFs. The Session 1 minutes were used as the current baseline where they resolve an earlier draft note, including the manual referral trigger, perpetrator details in the payload, optional ABR ID, one-way follow-up updates, direct district routing in principle, and the parallel emergency phone path. Remaining conflicts, missing API details, sandbox prerequisites and approval questions are marked for confirmation.

Earlier technical templates included candidate references from prior integration documentation. The token and case paths are now upstream-documented references; `abr_id` and the placeholder sandbox URL remain unconfirmed. Deployment compatibility must still be validated before implementation or testing.

## Current evidence update

Updated 26 October 2026 from Sessions 1–2 and [Isaiah’s response](../06_correspondence/ISAIAH_RESPONSE_SOURCE_2026-10-26.md). All 14 Word forms and the 12-sheet capture workbook now distinguish received documentation/contact evidence from pending approvals and live access. Earlier direct district-routing assumptions are retained as history, with Session 2’s service-based routing and Ministry distribution as the current working position.

The token and case paths are now documented upstream references, rather than unsupported candidate paths. Actual deployment compatibility, configured payloads, `abr_id`, example URLs and validation rules remain unconfirmed. Country SOPs, paper forms, use cases and pathways feed demo configuration; field definitions/lookups follow setup. Earlier annotations are preserved in the dated archive and, where relevant, in form capture-history notes.

Use [D1 v0.4](../01_inception/DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO.md) and [the completion inventory](../01_inception/INCEPTION_COMPLETION_INVENTORY.md) for current status. The workbook mirrors the main tables of forms 01–12. Risk and escalation forms 13–14 remain separate. Dates and proposed owners are not commitments unless explicitly confirmed.

## Token and template detail update

Forms **05, 06, 07, 08, 10 and 12**, and their workbook sheets, now prefill the available token details: POST issuance, bearer response header, username/password request structure, 60-minute lifetime, renewal with a valid token and DELETE invalidation of the current token. The API contract links directly to the upstream operation pages. Operational controls and UAT scenarios are marked as proposed or pending where agreement or execution is still required.

The action register also records the unified referral form as shared in Session 2, with review still pending. The separate case-management SOP receipt remains unconfirmed. Existing template action IDs are retained; they are not a renumbering of the minutes' action register.

The selected SSO/backend flow, actual base URL, credentials, permissions, renewal timing, expiry recovery and network controls remain Pending. No token was issued and no live authentication test was run. See the [update and validation record](../02_project_management/update_records/TEMPLATE_TOKEN_UPDATE_2026-10-26.md) for the exact changes and remaining questions.
