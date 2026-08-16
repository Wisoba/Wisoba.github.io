# PCC → RF complete authority-chain experiment

**Run:** `20260811T060102Z-ed28adcf`  
**Duration:** 10.412 seconds  
**Outcome:** **20 / 20 expected results**.

PCC is an optional correspondence-evidence boundary. The experiment tests that malformed, stale, or mismatched PCC evidence does not create authority in RF; a complete faithful chain is permitted once; replay, drift, and revocation are then refused by RF’s own checks.

| Result group | Cases | Expected / actual |
|---|---:|---|
| PCC correspondence mismatch | 7 | all REFUSED |
| PCC evidence / certificate mismatch | 2 | all REFUSED |
| RF certificate / permit binding failure | 6 | all REFUSED |
| Faithful complete chain | 1 | PERMITTED_ONCE |
| Replay, state drift, and revocation after evidence | 4 | all REFUSED |

The 15 pre-authority refusal variants cover row correspondence, trigger/function correspondence, privilege, row-level security, dependency topology, runtime context, environment identity, snapshot coherence signature, certificate content address, certificate signature, package identity, action binding, rehearsal artifact binding, execution-role binding, and certificate freshness.

The one faithful chain committed and consumed its permit. The post-authority checks then refused permit replay, target change after PCC before issuance, journal change after permit before execution, and midflight verifier revocation.

## Boundary

`ESTABLISHED` is scoped correspondence evidence, not safety or execution authority. RF independently verifies the separately signed, digest-bound certificate; locks and rebinds live state through its append-only row/DDL journal; executes one exact stored action; and consumes the permit once.
