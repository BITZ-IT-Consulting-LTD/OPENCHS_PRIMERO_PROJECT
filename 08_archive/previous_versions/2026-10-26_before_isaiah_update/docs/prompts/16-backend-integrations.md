# Prompt 17: Backend Integrations — Primero CPIMS+

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
