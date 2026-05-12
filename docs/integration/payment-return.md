# Payment Return

!!! warning "Status: TBD"
    The contract for notifying the partner app when a user completes or abandons a payment is being finalized. Final spec, payload shape, and signature scheme will be published **before any partner ships to production**.

## Confirmed direction

| Channel | Purpose |
|---------|---------|
| **Server-side webhook** | Source of truth for reconciliation. Partner-registered URL receives signed order-event POSTs. |
| **postMessage** | UX nicety for iframe partners — fire-and-forget UI update. |
| **Deep-link `returnUrl`** | For native WebView partners with a URL scheme (e.g. `acme://payment-result`). |

## What to prepare now

- Register a webhook URL during [onboarding](../onboarding/request-access.md) (field `Webhook URL`). Bluecom will activate it once the contract ships.
- If you're embedding via WebView, reserve a URL scheme for payment return now.
- Plan idempotency on your side — order events may be redelivered.

Subscribe to release notes for the final spec.
