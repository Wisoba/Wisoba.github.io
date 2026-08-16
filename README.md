# PINCR public evidence record — revision 7

**Status:** internally source- and package-verified revision-7 candidate, ready for partner-owned staging.

This record describes the current Recoverability Firewall (RF) candidate. Its shipped enforcement scope is **transactional PostgreSQL migrations with visible SQL**. It is not broad production certification, and it does not claim Kubernetes enforcement.

## What is in this record

- [10-million-row RF runtime report](runtime-10m-report.md): the corrected maintained-commitment measurement.
- [PCC-to-RF authority-chain report](pcc-rf-authority-report.md): optional correspondence evidence passed to RF, where RF still independently decides authority.
- [RF physical-replication and promotion report](replication-promotion-report.md): standby refusal and issuance after promotion.
- [PCC real-Kubernetes experiment](pcc-kubernetes-report.md): a separate two-cluster evidence experiment, not an RF Kubernetes product claim.
- [PCC Kubernetes false-green audit](pcc-kubernetes-false-green-report.md): four real server-side divergence cases refused after the package repair.

## Revision-7 release record

- RF package: `0.3.0`; kernel revision: `7`.
- Current source-suite record: **404/404 cases passed**, with zero failures, errors, or skips. The canonical release gate also passed **390 tests + 14 adversarial subtests**, with zero skips.
- Bounded hostile-schedule model: **0 false authorizations in 512 checked schedules** for the shipped journal-checkpoint protocol.
- PostgreSQL physical-replication and promotion run: standby execution refused; promotion exercised; post-promotion issuance passed.
- PCC is an optional, separately signed correspondence boundary. A PCC result is not itself safety or execution authority: RF separately verifies it, binds current state through its journal, executes one stored action, and consumes the permit once.

## 10M runtime headline

Run `20260816T040246Z` reconciled 10,000,000 rows using the exact-data oracle in **57.434 seconds**. That full pass is deliberately outside authorization and the final execution lock. The maintained exact-state lookup was **1.683 ms**; resident exact-data apply p50 was **22.246 ms**; the uncontended final lock-window proxy was **12.670 ms**. See the runtime report for methods and limits.

## Important boundaries

- The 10M measurement is a warm-buffer, uncontended local run with one sample at 10M rows. It is not a concurrency benchmark, production tail-latency measurement, or SLO.
- The lock-window proxy includes uncontended acquisition and excludes the final commit tail; it is not presented as exact lock dwell.
- RF currently refuses opaque or non-transactional operations. HTTP, queues, files, email, and other external effects remain outside its database proof boundary.
- PCC’s Kubernetes work is evidence that a separately scoped compiler can collect and falsify specific Kubernetes claims. It does not make RF a Kubernetes enforcement product or establish Kubernetes-wide transactional coherence.
- Any partner deployment needs partner-controlled staging, its own trust configuration, and evaluation of its actual workloads.
- A separate closure-aware scheduler experiment preserved authority integrity but regressed throughput by 83.2% and timed out 15 application operations. It is not recommended by default pending diagnosis and repeated evidence.

All reports are intentionally concise public records. `SHA256SUMS` binds the files in this directory.
