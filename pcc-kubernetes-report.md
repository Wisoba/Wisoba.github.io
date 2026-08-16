# PCC real-Kubernetes A/B falsification experiment

**Run:** `20260811T015521Z-eedd4541`  
**Package:** PCC package `1.3.0`; core compiler unchanged for the Kubernetes experiment.  
**Environment:** two independently initialized kind clusters, Kubernetes 1.36.1, with separate cluster CAs and separate ephemeral Ed25519 attestors.

This is **PCC evidence**, not a Recoverability Firewall Kubernetes enforcement claim. The unchanged proof-context compiler collected live Kubernetes resource evidence, signed it, and compared an API-applied clone against an independently initialized cluster.

## Recorded result

- **12 / 12** scenarios completed in **190.233 seconds**.
- Baseline clone: **29 / 29 obligations discharged**, `ESTABLISHED`.
- Eleven declared mutations: all **REFUSED** at the predicted subject or causal expansion.
- Dependency-expansion cases grew the compiled slice to 31 or 32 obligations when a relevant service account, ConfigMap, or Secret appeared only in the clone.
- **24 / 24** detached snapshot signatures reverified independently.
- **12 / 12** contract IDs and **12 / 12** bundle IDs recomputed independently.

The refused mutation set covered deployment strategy, immutable image digest, mutable tag, ConfigMap data, Secret data, RBAC rule removal, admission expression, admission-binding removal, and three dependency-expansion cases (service account, ConfigMap, Secret).

## Collection boundary

For each API collection the observer obtains a resource version, then rereads with `resourceVersionMatch=Exact` and refuses if the version differs. The resulting signed token is an **exact collection vector**, not a Kubernetes-wide ACID snapshot across heterogeneous API collections.

## What this does not establish

It does not establish that the package covers every production Kubernetes dimension or recovery claim; cross-resource transactional coherence beyond its signed vector; production trust roots; resistance to compromise of the API server, host, observer, or signer; equivalence under live traffic or external controllers; or immutable live state after evidence expires. RF’s present shipped enforcement domain remains transactional PostgreSQL migrations.
