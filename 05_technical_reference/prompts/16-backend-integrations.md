# Prompt 17: Backend Integrations — Primero CPIMS+

## Current Lesotho evidence recorded on 26 October 2026

This technical material contains prior design examples and implementation descriptions. The current inception evidence is [D1 v0.4](../../01_inception/DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO.md) and [Isaiah’s response](../../06_correspondence/ISAIAH_RESPONSE_SOURCE_2026-10-26.md). These do not verify the OpenCHS runtime or a live Primero connection.

- Upstream API v2 documentation is received. Token, case-create/update and referral paths are documented, but the Lesotho deployed release, configured schemas and operation sequence remain Pending.
- Documented bearer JWTs expire after 60 minutes. SSO is preferred where an identity provider exists; username/password is an alternative. Unattended backend authentication and specific network controls require confirmation.
- A configured demo is preferred; a primerodev.org site is a proposed alternative. No actual URL, credentials or committed access date is supplied.
- Country SOPs, paper forms, use cases and referral pathways are configuration inputs. Configured field definitions/lookups follow demo setup; ABR rules must be defined with the use case.
- Isaiah Amutavi Osotsi is the Primero technical contact. Active agency representatives should participate in child-journey UAT; named signatories remain Pending.
- Session 2’s working model is service-based routing with Ministry-side distribution. Direct district/caseworker selection in older examples is unconfirmed. Status write-back is Deferred; duplicate prevention and retry recovery remain Pending.

Example URLs, `abr_id`, sample mappings, validation patterns, and architectural refactors below remain discovery/design material unless explicitly approved. Isaiah reports no rate limits; operating limits and retry policies still require agreement.


## Goal
Build the Primero CPIMS+ integration for automated child protection case referrals.

## Context
Refer to CONTEXT.md Sections 5.8 (ReferralQueue, IntegrationLog), 7.6 (Primero Integration), and the full `OPENCHS_PRIMERO_INTEGRATION_CONTEXT.md`.

## Instructions

1. **Create app structure:**
```
backend/apps/integrations/
├── __init__.py
├── apps.py
├── tasks.py
└── primero/
    ├── __init__.py
    ├── client.py
    ├── auth.py
    ├── mappers.py
    └── exceptions.py
```

2. **Exceptions (`exceptions.py`)**:
   - `PrimeroAPIError` (base): message, status_code, response_data
   - `PrimeroAuthError`, `PrimeroNotFoundError`, `PrimeroValidationError`, `PrimeroServerError`, `PrimeroRateLimitError`

3. **Auth (`auth.py`)**:
   - `PrimeroAuth` class:
     - `CACHE_KEY = 'primero_jwt_token'`
     - `get_token()`: check Django cache first, if expired call `_fetch_token()`
     - `_fetch_token()`: POST to `/api/v2/tokens` with `{user: {user_name, password}}`, cache token with expiry
     - `invalidate_token()`: DELETE token endpoint, clear cache

4. **Client (`client.py`)**:
   - `PrimeroAPIClient` class:
     - `_make_request(method, endpoint, data, params, retry_auth=True)`: unified request handler with status code mapping to custom exceptions, auto-retry on 401 once after token refresh
     - `create_case(case_data)`: POST `/api/v2/cases`
     - `get_case(case_id)`, `list_cases(params)`, `update_case(case_id, case_data)`
     - `get_forms()`, `get_lookups()`

5. **Mappers (`mappers.py`)**:
   - `PrimeroCaseMapper` class:
     - `map_call_to_case(call)` → returns Primero v2 payload dict
     - `PROTECTION_CONCERNS_MAP`: map OpenCHS concern codes to Primero codes
     - `RISK_LEVEL_MAP`: map OpenCHS risk levels to Primero levels
     - Extract child demographics from Call model
     - Include referral_source='child_helpline_116', module_id='primeromodule-cp'

6. **Tasks (`tasks.py`)**:
   - `process_referral_async(referral_queue_id)`:
     - Get ReferralQueue by ID
     - If status not pending, return
     - Set status='processing'
     - Build payload via `PrimeroCaseMapper.map_call_to_case()`
     - Call `PrimeroAPIClient.create_case()`
     - On success: update ReferralQueue status='completed', store primero_case_id
     - On failure: increment retry_count, compute next_retry_at from delays [60,300,1800,7200], log to IntegrationLog
     - If max retries exceeded: status='failed', alert admin

7. **Celery Beat Schedule** (add to settings):
   - `process-pending-referrals`: every 5 minutes, calls task that finds ReferralQueue with status='pending' and next_retry_at <= now

## Acceptance Criteria
- PrimeroAuth caches JWT tokens and refreshes before expiry
- PrimeroAPIClient handles all HTTP status codes with correct exceptions
- Mapper produces valid Primero v2 case payload
- Celery task retries with exponential backoff
- IntegrationLog captures full request/response on every attempt
