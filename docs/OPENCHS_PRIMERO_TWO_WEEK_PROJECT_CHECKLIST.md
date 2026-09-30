# OpenCHS–Primero Integration
## Two-Week Project Delivery Checklist

**Project:** Lesotho Child Helpline 116 / OpenCHS integration with Primero CPIMS+  
**Project manager:** ____________________  
**Start date:** ____________________  
**Target decision/go-live date:** ____________________  
**Version:** 0.1

### Status key

- ☐ Not started
- ◐ In progress
- ☑ Complete
- ⚠ Blocked
- N/A Not applicable to MVP

---

## 1. Project Mobilisation

| Status | Checklist item | Owner | Due date | Evidence/notes |
|---|---|---|---|---|
| ☐ | Project sponsor confirmed |  |  |  |
| ☐ | Business owner confirmed |  |  |  |
| ☐ | OpenCHS technical lead confirmed |  |  |  |
| ☐ | Primero technical lead confirmed |  |  |  |
| ☐ | MGYSD operational representative confirmed |  |  |  |
| ☐ | UNICEF programme representative confirmed |  |  |  |
| ☐ | Data protection/security owner confirmed |  |  |  |
| ☐ | Infrastructure/network owner confirmed |  |  |  |
| ☐ | UAT sign-off authority confirmed |  |  |  |
| ☐ | Daily project meeting scheduled |  |  |  |
| ☐ | Decision register created |  |  |  |
| ☐ | Risk and issue register created |  |  |  |
| ☐ | Change-control process agreed |  |  |  |

## 2. Scope and MVP Confirmation

| Status | Checklist item | Owner | Due date | Evidence/notes |
|---|---|---|---|---|
| ☐ | Primero CPIMS+ confirmed as receiving system |  |  |  |
| ☐ | Primero version confirmed |  |  |  |
| ☐ | Outbound-only or bi-directional scope decided |  |  |  |
| ☐ | Two-week MVP scope approved |  |  |  |
| ☐ | Deferred features documented |  |  |  |
| ☐ | Critical success criteria approved |  |  |  |
| ☐ | Go/no-go decision criteria approved |  |  |  |
| ☐ | No unapproved scope additions accepted |  |  |  |

## 3. Environment and Access Readiness

| Status | Checklist item | Owner | Due date | Evidence/notes |
|---|---|---|---|---|
| ☐ | OpenCHS source repository available |  |  |  |
| ☐ | OpenCHS development environment available |  |  |  |
| ☐ | OpenCHS test/UAT environment available |  |  |  |
| ☐ | Primero sandbox URL received |  |  |  |
| ☐ | Primero UAT URL received |  |  |  |
| ☐ | Primero production URL received or scheduled |  |  |  |
| ☐ | API credentials received through a secure channel |  |  |  |
| ☐ | Separate test and production credentials confirmed |  |  |  |
| ☐ | Network/firewall/VPN access tested |  |  |  |
| ☐ | TLS/SSL certificate requirements confirmed |  |  |  |
| ☐ | Production secret-storage approach confirmed |  |  |  |
| ☐ | Backup and rollback access confirmed |  |  |  |

## 4. Business Referral Workflow

| Status | Checklist item | Owner | Due date | Evidence/notes |
|---|---|---|---|---|
| ☐ | Referral initiation point defined |  |  |  |
| ☐ | Referral eligibility criteria approved |  |  |  |
| ☐ | Authorized referral roles defined |  |  |  |
| ☐ | Supervisor approval requirement decided |  |  |  |
| ☐ | Consent and legal-basis requirements approved |  |  |  |
| ☐ | No-ABR-ID process approved |  |  |  |
| ☐ | Referral correction process approved |  |  |  |
| ☐ | Referral cancellation process approved |  |  |  |
| ☐ | Re-referral rules approved |  |  |  |
| ☐ | Rejected-referral process approved |  |  |  |
| ☐ | Primero outage process approved |  |  |  |
| ☐ | Operator-visible referral statuses agreed |  |  |  |

## 5. ABR ID Requirements

| Status | Checklist item | Owner | Due date | Evidence/notes |
|---|---|---|---|---|
| ☐ | ABR meaning formally confirmed |  |  |  |
| ☐ | ABR owner confirmed |  |  |  |
| ☐ | ABR creation point confirmed |  |  |  |
| ☐ | ABR manual/generated/source-system rule confirmed |  |  |  |
| ☐ | ABR mandatory/optional rule confirmed |  |  |  |
| ☐ | ABR length confirmed |  |  |  |
| ☐ | ABR character set confirmed |  |  |  |
| ☐ | ABR prefix and structure confirmed |  |  |  |
| ☐ | ABR uniqueness rule confirmed |  |  |  |
| ☐ | ABR check-digit rule confirmed or explicitly deferred |  |  |  |
| ☐ | Valid sample ABR values received |  |  |  |
| ☐ | Invalid sample ABR values received |  |  |  |
| ☐ | ABR validation rules approved for implementation |  |  |  |

## 6. API and Authentication Contract

| Status | Checklist item | Owner | Due date | Evidence/notes |
|---|---|---|---|---|
| ☐ | API specification received |  |  |  |
| ☐ | API version confirmed |  |  |  |
| ☐ | Authentication endpoint confirmed |  |  |  |
| ☐ | Authentication request format confirmed |  |  |  |
| ☐ | Token response format confirmed |  |  |  |
| ☐ | Token lifetime confirmed |  |  |  |
| ☐ | Token refresh process confirmed |  |  |  |
| ☐ | Required headers confirmed |  |  |  |
| ☐ | Case-creation endpoint confirmed |  |  |  |
| ☐ | Success response confirmed |  |  |  |
| ☐ | Validation-error response confirmed |  |  |  |
| ☐ | Timeout and rate-limit behaviour confirmed |  |  |  |
| ☐ | API connectivity test passed |  |  |  |

## 7. Data Mapping and Privacy

| Status | Checklist item | Owner | Due date | Evidence/notes |
|---|---|---|---|---|
| ☐ | OpenCHS case/call source fields identified |  |  |  |
| ☐ | Primero target fields identified |  |  |  |
| ☐ | Mandatory fields identified |  |  |  |
| ☐ | Optional fields identified |  |  |  |
| ☐ | ABR target field confirmed |  |  |  |
| ☐ | Child identity mapping approved |  |  |  |
| ☐ | Age/date-of-birth mapping approved |  |  |  |
| ☐ | Sex/gender code mapping approved |  |  |  |
| ☐ | Location mapping approved |  |  |  |
| ☐ | Risk-level mapping approved |  |  |  |
| ☐ | Protection-concern lookup values confirmed |  |  |  |
| ☐ | Referral-source value confirmed |  |  |  |
| ☐ | Free-text sharing rules approved |  |  |  |
| ☐ | Phone-number sharing rules approved |  |  |  |
| ☐ | Call-recording sharing rules approved |  |  |  |
| ☐ | Consent/legal-basis field mapping approved |  |  |  |
| ☐ | Data minimisation review completed |  |  |  |
| ☐ | Mapping document signed off |  |  |  |

## 8. ABR and Referral User Interface

| Status | Checklist item | Owner | Due date | Evidence/notes |
|---|---|---|---|---|
| ☐ | ABR field added/configured |  |  |  |
| ☐ | Referral action added/configured |  |  |  |
| ☐ | Mandatory-field validation implemented |  |  |  |
| ☐ | Invalid-ABR error message implemented |  |  |  |
| ☐ | Referral permission restriction implemented |  |  |  |
| ☐ | Duplicate referral prevention implemented |  |  |  |
| ☐ | Pending status displayed |  |  |  |
| ☐ | Processing status displayed |  |  |  |
| ☐ | Completed status displayed |  |  |  |
| ☐ | Failed status and explanation displayed |  |  |  |
| ☐ | Manual retry control restricted to authorized users |  |  |  |
| ☐ | UI tested on supported browsers/devices |  |  |  |

## 9. Integration Implementation

| Status | Checklist item | Owner | Due date | Evidence/notes |
|---|---|---|---|---|
| ☐ | Primero API client implemented |  |  |  |
| ☐ | JWT token caching implemented |  |  |  |
| ☐ | Token refresh on expiry implemented |  |  |  |
| ☐ | Secure credential configuration implemented |  |  |  |
| ☐ | Confirmed payload mapper implemented |  |  |  |
| ☐ | Referral persisted before transmission |  |  |  |
| ☐ | Durable offline queue implemented |  |  |  |
| ☐ | Retryable and non-retryable errors separated |  |  |  |
| ☐ | Retry/back-off policy implemented |  |  |  |
| ☐ | Maximum retries implemented |  |  |  |
| ☐ | Failed referral escalation implemented |  |  |  |
| ☐ | Idempotency/transaction key implemented |  |  |  |
| ☐ | Duplicate response reconciliation implemented |  |  |  |
| ☐ | Referral status endpoint or equivalent implemented |  |  |  |
| ☐ | Manual retry mechanism implemented |  |  |  |

## 10. Audit, Security, and Operations

| Status | Checklist item | Owner | Due date | Evidence/notes |
|---|---|---|---|---|
| ☐ | Integration attempts are auditable |  |  |  |
| ☐ | Initiating user is recorded |  |  |  |
| ☐ | Transaction/reference ID is recorded |  |  |  |
| ☐ | Timestamp and endpoint are recorded |  |  |  |
| ☐ | Retry history is recorded |  |  |  |
| ☐ | Sensitive request fields are redacted |  |  |  |
| ☐ | Sensitive response fields are redacted |  |  |  |
| ☐ | Integration logs have role-based access |  |  |  |
| ☐ | SSL verification is enabled |  |  |  |
| ☐ | Credentials are not stored in source code |  |  |  |
| ☐ | Monitoring owner assigned |  |  |  |
| ☐ | Queue monitoring procedure documented |  |  |  |
| ☐ | Incident escalation path documented |  |  |  |

## 11. Testing Checklist

| Status | Test | Expected result | Owner | Evidence/notes |
|---|---|---|---|---|
| ☐ | Valid ABR ID | Accepted |  |  |
| ☐ | Invalid ABR ID | Submission blocked with clear message |  |  |
| ☐ | Missing mandatory field | Submission blocked |  |  |
| ☐ | Unauthorized referral attempt | Access denied and logged |  |  |
| ☐ | Successful authentication | Token received and securely handled |  |  |
| ☐ | Expired token | Token refreshed and request retried once |  |  |
| ☐ | Successful case creation | Primero case ID stored |  |  |
| ☐ | Primero validation rejection | Referral marked failed with actionable error |  |  |
| ☐ | Network timeout | Referral retained and retry scheduled |  |  |
| ☐ | Primero server error | Retry performed according to policy |  |  |
| ☐ | Maximum retries exceeded | Escalation generated |  |  |
| ☐ | Duplicate submission | Only one Primero case created |  |  |
| ☐ | Uncertain timeout after creation | Existing case reconciled |  |  |
| ☐ | Manual retry | Authorized retry succeeds or records failure |  |  |
| ☐ | Audit-log access | Only authorized users can view logs |  |  |
| ☐ | Existing OpenCHS regression | Existing workflows remain functional |  |  |

## 12. UAT Checklist

| Status | Checklist item | Owner | Due date | Evidence/notes |
|---|---|---|---|---|
| ☐ | UAT scenarios approved |  |  |  |
| ☐ | UAT users and roles prepared |  |  |  |
| ☐ | Test data prepared and approved |  |  |  |
| ☐ | UAT environment stable |  |  |  |
| ☐ | Happy-path referral passed |  |  |  |
| ☐ | Invalid-data scenario passed |  |  |  |
| ☐ | API-unavailable scenario passed |  |  |  |
| ☐ | Retry scenario passed |  |  |  |
| ☐ | Duplicate-prevention scenario passed |  |  |  |
| ☐ | Status visibility scenario passed |  |  |  |
| ☐ | Audit evidence reviewed |  |  |  |
| ☐ | Defects classified by severity |  |  |  |
| ☐ | Critical defects closed |  |  |  |
| ☐ | UAT sign-off completed |  |  |  |

## 13. Training and Handover

| Status | Checklist item | Owner | Due date | Evidence/notes |
|---|---|---|---|---|
| ☐ | Operator guide prepared |  |  |  |
| ☐ | ABR and referral workflow training completed |  |  |  |
| ☐ | Referral-status training completed |  |  |  |
| ☐ | Failed-referral escalation training completed |  |  |  |
| ☐ | Technical administrator guide prepared |  |  |  |
| ☐ | Queue-monitoring training completed |  |  |  |
| ☐ | Retry and troubleshooting training completed |  |  |  |
| ☐ | Credential-management procedure handed over |  |  |  |
| ☐ | Support contacts distributed |  |  |  |
| ☐ | Backup and rollback procedure handed over |  |  |  |
| ☐ | Known limitations and deferred scope handed over |  |  |  |

## 14. Production Readiness and Go-Live

| Status | Checklist item | Owner | Due date | Evidence/notes |
|---|---|---|---|---|
| ☐ | Production API endpoint confirmed |  |  |  |
| ☐ | Production credentials loaded securely |  |  |  |
| ☐ | Production connectivity tested |  |  |  |
| ☐ | Production configuration reviewed |  |  |  |
| ☐ | Database migration/configuration backed up |  |  |  |
| ☐ | Rollback procedure tested or rehearsed |  |  |  |
| ☐ | Monitoring enabled |  |  |  |
| ☐ | Support coverage scheduled |  |  |  |
| ☐ | Go-live communication issued |  |  |  |
| ☐ | Business owner approval received |  |  |  |
| ☐ | Technical owner approval received |  |  |  |
| ☐ | Data protection/security approval received |  |  |  |
| ☐ | Go decision recorded |  |  |  |

## 15. Go / Conditional Go / No-Go Review

### Go

- ☐ End-to-end referral test passed.
- ☐ No unresolved critical defects.
- ☐ ABR rules approved.
- ☐ API contract confirmed.
- ☐ Idempotency verified.
- ☐ Sensitive-data controls verified.
- ☐ UAT signed off.
- ☐ Support owner confirmed.

### Conditional go

- ☐ Only minor defects remain.
- ☐ Workarounds documented.
- ☐ Risks accepted in writing.
- ☐ Monitoring active.
- ☐ Rollback available.

### No-go triggers

- ☐ API contract unresolved.
- ☐ ABR rules unresolved.
- ☐ Duplicate prevention unverified.
- ☐ Sensitive-data controls incomplete.
- ☐ No UAT sign-off.
- ☐ No accountable support owner.

**Final decision:** Go / Conditional go / No-go  
**Decision date:** ____________________  
**Decision authority:** ____________________  
**Signature:** ____________________

## 16. Outstanding Actions and Risks

| ID | Action/risk | Impact | Owner | Deadline | Status | Escalation |
|---|---|---|---|---|---|---|
| R/A-001 |  |  |  |  |  |  |
| R/A-002 |  |  |  |  |  |  |
| R/A-003 |  |  |  |  |  |  |
| R/A-004 |  |  |  |  |  |  |
| R/A-005 |  |  |  |  |  |  |

## Source Documents

- `Lesotho_OpenCHS_Technical_Scope_Inception_Brief.pdf`
- `Lesotho_OpenCHS_Implementation_Timeline_Presentation.pptx`
- `docs/docs/platform/reference/OPENCHS_PRIMERO_INTEGRATION_CONTEXT.md`
- `docs/context/12_PRIMERO_CPIMS_CONTEXT.md`
