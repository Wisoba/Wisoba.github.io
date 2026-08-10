# Corrected RF kernel runtime benchmark

Run: `20260805T051035Z`

This is an uncontended, warm-buffer local benchmark. It is not the
Gate 7 concurrent-load availability benchmark and does not establish
busy-production readiness.

## Measured conclusion

- Exact-data permits use the transactional-journal checkpoint; their
  final authorization does not rescan application rows under the
  execution lock.
- The isolated exact-data fingerprint remains the off-path digest
  reference and is reported separately from apply.
- The schema-only resident-connection p50 stayed row-independent at
  22.681–22.681 ms.
- Issuance includes signing plus independent verifier attestation;
  execution includes envelope, governance, closure, journal and
  runtime-identity checks.

| Rows | Native p50 | Schema RF p50 (resident) | Exact-data RF p50 (resident) | Schema lock-window proxy | Exact lock-window proxy |
|---:|---:|---:|---:|---:|---:|
| 10,000,000 | 2.204 ms | 22.681 ms | 31.577 ms | 12.770 ms | 15.228 ms |

## Isolated phases (p50)

| Rows | Revision preflight | Catalog closure | Schema fingerprint | Exact-data fingerprint | Uncontended lock transaction |
|---:|---:|---:|---:|---:|---:|
| 10,000,000 | 0.141 ms | 0.361 ms | 0.394 ms | 40180.133 ms | 0.264 ms |

## Interpretation boundary

- `native` runs the identical marker + add-column + drop-column SQL.
- `resident` keeps one executor connection but still performs the
  required revision preflight for every permit.
- `lock-window proxy` begins at the consumption timestamp immediately
  before lock acquisition and ends at the kernel result timestamp.
  It includes uncontended acquisition and excludes the final commit
  tail, so it is not represented as exact lock dwell.
- `live binding issuance` includes production state binding,
  immutable permit insert, Ed25519 signing, and independent
  verifier attestation. It is not the shadow rehearsal duration.
- Full distributions and PostgreSQL function attribution are in
  `results.json`.
- Samples in this run: 1 at 10,000,000 rows. The emitted p95/p99
  values are diagnostic maxima at these sample counts, not
  production tail-latency estimates or SLO evidence.
- `results.json` binds SHA-256 hashes of the exact source files used;
  `SHA256SUMS` protects the two human/machine-readable artifacts.
