# Testing & Go-Live

## Sandbox phases

1. **Smoke** — one successful payment, verified on the Bluecom monitoring dashboard and in the webhook audit log.
2. **Functional matrix** — every row in the [acceptance gate](checklist.md#acceptance-gate).
3. **Soak** — 24 h continuous low-rate traffic against sandbox to surface idempotency and clock-skew bugs.

## Required test cases

| Case | Expected result |
|------|-----------------|
| Happy path | Order → `PAID`, single settlement event emitted. |
| User cancels on the hosted page | Order → `CANCELLED`, user returned to the Shop. |
| User abandons (closes WebView) | Order auto-expires after the partner's `expiresAt`. |
| IPN delivered twice | Order transitions once; second IPN is ack-only. |
| IPN with bad signature | `4xx` rejection, entry flagged in the webhook audit log. |
| IPN with stale timestamp (> 5 min) | Rejected. |
| Reconciliation of a stuck order | Query-payment converges state without manual ops. |
| Refund (if supported) | Order → `REFUNDED`. |

## Go-live

- Partner delivers production credentials via an out-of-band secure channel (not plaintext email).
- Bluecom rotates credentials into the production configuration store with no downtime.
- Canary on one low-volume sales channel for 48 h.
- Gradual rollout to remaining channels once error rate < 0.1 % and reconciliation backlog = 0.
- Runbook entry published in Bluecom Operations.
