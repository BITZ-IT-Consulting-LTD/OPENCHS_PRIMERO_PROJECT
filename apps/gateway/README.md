# BITZ Integration Gateway

The D3 outbound REST API client (contract item 70). It receives authorised referral operations from OPENCHS and sends them to the Primero CPIMS+ API of the Lesotho deployment. It calls Primero directly; there is no OpenFN or X-Road in the path.

> Planned layout only. No code yet.

## Planned layout

```
gateway/
├── auth/            # JWT client, token renewal, least-privilege service account     (#37)
├── mapping/         # versioned field and service mapping, disclosure rules           (#38)
├── operations/      # Create Referral and Send Update against the stored UUID         (#39, #40)
├── ledger/          # transaction ledger: case, referral, operation, idempotency key, UUID (#39, #42)
├── queue/           # persistent queue, failure classification, retries 1/5/30/120 min (#41)
├── reconciliation/  # resolve uncertain outcomes before any further create attempt    (#42)
├── audit/           # metadata-only, tamper-evident audit log                         (#43)
├── admin/           # restricted queue dashboard, alerts, controlled manual retry     (#44)
├── config/          # per-environment settings (no secrets in Git)
└── tests/
    ├── unit/
    ├── contract/    # against the mock Primero API                                    (#45)
    └── mock_primero/
```

## Design references

- Design and interface specification: #36
- D1 Inception Report v2.9, Sections 6.1–6.7 and Annex B ([report](../../01_inception/D1_INCEPTION_REPORT_OPENCHS_PRIMERO_V2.9_FINAL_DRAFT.md))
- Lesotho verification (G3): #47

## Evidence levels

| Level | Meaning |
|---|---|
| 1 | Development (unit tests) |
| 2 | Simulated integration (mock Primero API) |
| 3 | Verified on the Lesotho CPIMS+ test environment. Only this level supports G4 |
