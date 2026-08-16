# PCC Kubernetes false-green adversarial audit

**Run:** `20260811T040820Z-92a1c9b6`  
**Package:** `1.3.0`  
**Expectation mode:** closed.

The audit intentionally replays four cases where a real Kubernetes server-side oracle found behavioral divergence that package `1.2` had not completely represented. Under package `1.3`, all four cases were refused; no false green remained in this set.

| Real divergence class | PCC result | False green | Expected |
|---|---|---|---|
| Namespace selector / admission context | REFUSED | no | yes |
| LimitRange admission defaults | REFUSED | no | yes |
| ServiceAccount admission defaults | REFUSED | no | yes |
| RBAC permission outside the prior fixed query list | REFUSED | no | yes |

This is evidence of package repair and fail-closed behavior for these four discovered cases. It does not prove completeness for Kubernetes generally: unmodeled controllers, webhooks, quotas, scheduling, networking, storage, cloud-provider behavior, and other excluded semantics require explicit package coverage before they can support a production claim.
