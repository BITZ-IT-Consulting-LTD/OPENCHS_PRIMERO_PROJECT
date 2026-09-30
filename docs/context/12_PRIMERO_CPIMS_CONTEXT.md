# 12: Primero CPIMS+ Integration

## Current Implementation State

### Implemented

- Primero client/auth/mapper code under `backend/apps/integrations/primero`
- referral and telephony fields reference Primero concepts
- call form has Primero-specific UI fields

### Partially implemented

- Primero exists as a concrete integration slice
- some workflow integration hooks exist

### Missing

- Primero expressed through the generic integration framework
- tenant-specific Primero credential/config model
- async job orchestration with retries and logs

## Required Refactor

Primero should become a configured `IntegrationProvider` rather than a special-case integration path.

## Primero Mapping Requirements

### Provider configuration

- `IntegrationProvider.code = "PRIMERO_CPIMS"`
- credentials stored via `IntegrationCredential`
- field mappings stored via `IntegrationMapping`
- retry policy stored via `IntegrationRetryPolicy`

### Job types

- `push_referral`
- `pull_case_status`
- `sync_lookup`
- `verify_connection`

## APIs To Add Or Change

- `POST /api/v1/integrations/providers/primero/test-connection/`
- `POST /api/v1/integrations/providers/primero/sync-lookups/`
- `POST /api/v1/referrals/<id>/dispatch/` should internally resolve provider and enqueue integration job

## Events

### Consume

- `REFERRAL_CREATED`
- `REFERRAL_DISPATCHED` follow-up status syncs

### Emit

- `INTEGRATION_JOB_SUCCEEDED`
- `INTEGRATION_JOB_FAILED`
- `REFERRAL_COMPLETED`

## Frontend Changes Required

- move Primero-specific settings into generic integration admin with provider-specific form sections
- keep Primero fields on call/referral screens only where business flow genuinely requires them

## Permissions

- `integrations.manage_primero`
- `integrations.view_primero_logs`

## Tests To Write

- Primero provider credential resolution
- Primero payload mapping
- Primero retry behavior
- sync lookup job writes logs and statuses

## Production Concerns

- SSL verification should default on
- all outbound payloads must pass consent/data-sharing policy evaluation first
