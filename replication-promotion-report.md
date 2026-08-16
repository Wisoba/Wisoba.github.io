# RF physical replication / promotion validation

**Run:** `20260811T060144Z`

- Standby execution: **REFUSED** — permits cannot execute on a recovery/standby server.
- Promotion: **exercised**.
- A permit issued before promotion remained unconsumed on the standby.
- Issuance on the promoted server’s new timeline: **passed**.

This is a focused local physical-replication and promotion validation. It is not a complete high-availability or production-readiness claim.
