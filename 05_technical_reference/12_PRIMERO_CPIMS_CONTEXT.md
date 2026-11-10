# 12: Primero CPIMS+ Integration

## Current Lesotho evidence recorded on 26 October 2026

This technical material contains prior design examples and implementation descriptions. The current inception evidence is [D1 v0.4](../01_inception/DRAFT_INCEPTION_REPORT_D1_OPENCHS_PRIMERO.md) and [Isaiah’s response](../06_correspondence/ISAIAH_RESPONSE_SOURCE_2026-10-26.md). These do not verify the OpenCHS runtime or a live Primero connection.

- Upstream API v2 documentation is received. Token, case-create/update and referral paths are documented, but the Lesotho deployed release, configured schemas and operation sequence remain Pending.
- Documented bearer JWTs expire after 60 minutes. SSO is preferred where an identity provider exists; username/password is an alternative. Unattended backend authentication and specific network controls require confirmation.
- A configured demo is preferred; a primerodev.org site is a proposed alternative. No actual URL, credentials or committed access date is supplied.
- Country SOPs, paper forms, use cases and referral pathways are configuration inputs. Configured field definitions/lookups follow demo setup; ABR rules must be defined with the use case.
- Isaiah Amutavi Osotsi is the Primero technical contact. Active agency representatives should participate in child-journey UAT; named signatories remain Pending.
- Session 2’s working model is service-based routing with Ministry-side distribution. Direct district/caseworker selection in older examples is unconfirmed. Status write-back is Deferred; duplicate prevention and retry recovery remain Pending.

Example URLs, `abr_id`, sample mappings, validation patterns, and architectural refactors below remain discovery/design material unless explicitly approved. Isaiah reports no rate limits; operating limits and retry policies still require agreement.


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
