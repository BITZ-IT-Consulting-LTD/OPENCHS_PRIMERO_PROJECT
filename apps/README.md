# Applications

| App | Path | Role | Status |
|---|---|---|---|
| **OPENCHS** | [`openchs/`](openchs/README.md) | Child Helpline 116 case management. Hosts the D2 referral features: **Refer to CPIMS+**, the optional ABR ID, validation, technical status and **Send Update** | Placeholder. Will be added as a git submodule pointing at the OpenCHS repository |
| **BITZ Integration Gateway** | [`gateway/`](gateway/README.md) | D3 outbound REST API client between OPENCHS and Primero CPIMS+ | Planned layout only; no code yet |

```
OPENCHS  →  BITZ Integration Gateway  →  Primero CPIMS+ API (Lesotho)
```

**Rules for this repository (it is public):**
- No real child data in code, fixtures or tests. Use synthetic data only.
- No credentials, tokens, `.env` files or certificates. Secrets come from the environment's secret store.
- Upstream Primero source is not vendored here. It stays local in `primero/`, which is git-ignored.
