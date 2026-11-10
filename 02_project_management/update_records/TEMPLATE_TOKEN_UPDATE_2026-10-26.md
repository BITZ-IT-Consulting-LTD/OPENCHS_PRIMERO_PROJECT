# Token and template detail update

**Recorded:** 26 October 2026  
**Status:** Documentation update; deployment confirmation and test execution Pending

Isaiah's supplied response and the upstream API pages fill several authentication discovery fields. The existing templates retain their approval and test gates.

| Template | Information filled or corrected | Still required |
|---|---|---|
| [05 API environment matrix](../../04_templates/05_api_environment_matrix.docx) | Primero provisions credentials when ready; SSO preference; 60-minute JWT and token access-package row | Actual site URL, selected backend flow, secure handover, account permissions and connectivity |
| [06 API contract capture](../../04_templates/06_api_contract_capture.docx) | Issuance request structure, response/header, lifetime, valid-token renewal, current-token invalidation and documented token responses | Applicable release, selected flow, approved account, renewal timing, expiry recovery and deployed behaviour |
| [07 Reliability controls](../../04_templates/07_reliability_logging_support_controls.docx) | Token lifecycle baseline; proposed secret handling and bounded failure-recovery controls | Approved procedure, secret custodian, storage/rotation, concurrency, redaction and operational evidence |
| [08 UAT matrix](../../04_templates/08_uat_acceptance_matrix.docx) | More specific issuance/renewal/expiry test; proposed invalidation and failure/access/redaction scenarios | Provisioned test accounts, expected deployed errors, approved criteria and executed evidence |
| [10 Action register](../../04_templates/10_action_register.docx) | Authentication action now asks for remaining decisions; referral form sharing recorded complete per Session 2, review pending; SOP owner corrected to Hopolang/Ministry subject to confirmation | SOP receipt, versioned form review, approved mapping and dated authentication decisions |
| [12 Close-out checklist](../../04_templates/12_inception_closeout_checklist.docx) | Available token evidence and shared-form status prefilled beside open gates | Full business/technical approval and test evidence; checkboxes remain unchecked |

The [capture workbook](../../04_templates/Workstream_1_Inception_Capture_Workbook.xlsx) mirrors these six main tables. All 12 existing evidence footers now use the organised source-record path. Other main tables retain their content. Existing action IDs are retained and are separate from the minutes' IDs.

## Evidence and remaining decisions

- [Isaiah response source record](../../06_correspondence/ISAIAH_RESPONSE_SOURCE_2026-10-26.md): 60-minute expiry, issue/reissue endpoint, SSO preference with username/password alternative, Primero credential provisioning, unspecified applicable network/security controls and the demo/alternative environment approach. The response's sent date was not supplied.
- [Upstream token POST documentation](https://github.com/primeroIMS/primero/blob/development_v2/app/controllers/api/v2/docs/tokens/post.md): issue/renew with POST `/api/v2/tokens`; a valid token can be used instead of credentials; the bearer token is returned in the Authorization response header. Other unexpired tokens remain valid. Username/password schema and 200/401 examples are documented.
- [Upstream token DELETE documentation](https://github.com/primeroIMS/primero/blob/development_v2/app/controllers/api/v2/docs/tokens/delete.md): invalidate the token supplied in Authorization; 200 response with an empty object. Error response details are unfinished upstream.
- Session 2, 9 October 2026: workflow sharing (minutes A-003) and referral-form sharing (minutes A-004) recorded complete. This does not establish a separately supplied SOP, approved field rules or a configured payload.

The API pages are on the moving `development_v2` branch. They do not establish the deployed Lesotho version. Confirm the backend authentication choice separately from user SSO, and agree renewal timing, expired/invalidated-token recovery, permissions and secure handling. No OAuth grant or separate refresh-token mechanism is assumed.

All new controls and UAT scenarios are proposed until approved. No credentials or real tokens were entered, no live API request was made, and no UAT scenario was executed. Inception inventory status totals remain unchanged.

## Preservation and verification

Pre-update files are preserved under [the dated archive](../../08_archive/previous_versions/2026-10-26_before_token_template_update/). The Word forms and workbook are checked for readable rendering, archive integrity and exact table alignment. Detailed results are recorded in [the validation record](TEMPLATE_TOKEN_VALIDATION_2026-10-26.json).
