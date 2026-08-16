# Corrected RF kernel runtime benchmark

**Run:** `20260816T040246Z`
**Environment:** PostgreSQL 16.14; `fsync=on`; `shared_buffers=128MB`; kernel revision 7.

This is an uncontended, warm-buffer local benchmark. It is not a concurrent-load availability benchmark and does not establish busy-production readiness.

## Measured result

Exact-data permits use a transactional-journal checkpoint. Their final authorization does **not** rescan application rows under the execution lock. The isolated full-scan oracle, maintained-commitment lookup, and apply path are therefore reported separately.

| Rows | Native p50 | Schema RF p50 (resident) | Exact-data RF p50 (resident) | Schema lock-window proxy | Exact lock-window proxy |
|---:|---:|---:|---:|---:|---:|
| 10,000,000 | 4.135 ms | 23.473 ms | 22.246 ms | 16.663 ms | 12.670 ms |

## Isolated phases (p50)

| Rows | Revision preflight | Catalog closure | Schema fingerprint | Exact reconciliation | Maintained exact lookup | Uncontended lock transaction |
|---:|---:|---:|---:|---:|---:|---:|
| 10,000,000 | 0.405 ms | 1.006 ms | 1.332 ms | 57,433.798 ms | 1.683 ms | 1.174 ms |

## Method and interpretation limits

- `native` runs the identical marker + add-column + drop-column SQL.
- `resident` retains one executor connection while still performing the required revision preflight for every permit.
- `lock-window proxy` begins at the consumption timestamp immediately before lock acquisition and ends at the kernel result timestamp. It includes uncontended acquisition and excludes the final commit tail; it is not exact lock dwell.
- Live-binding issuance includes production-state binding, immutable permit insertion, Ed25519 signing, and independent verifier attestation. It is not shadow-rehearsal duration.
- There was one sample at 10M rows. Diagnostic p95/p99 maxima at that sample count are not production tail-latency estimates or SLO evidence.

The product claim supported here is narrow: exact state can be reconciled outside the authorization window, then checked through a fresh maintained commitment before a single-use permit is issued and applied.
