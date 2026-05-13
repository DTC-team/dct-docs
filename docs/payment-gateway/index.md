# Payment Gateway Integration

This section is for **payment providers** who want to plug their gateway into the Bluecom eSIM platform so end-users can pay through it inside the Bluecom WebView / iframe checkout.

If you are a **partner app embedding Bluecom** and only need to be notified when a payment completes, you want [Integration → Payment Return](../integration/payment-return.md) instead.

## Who this is for

- Domestic VN gateways (QR-by-bank, card, wallet) — same class as our current reference integration **Neox / NeoPay**.
- International PSPs (card / APM) that expose either a **hosted payment page** (redirect/iframe) or a **server-to-server create-payment API** with a returned redirect URL.

## What Bluecom expects from your gateway

At minimum:

1. A **create-payment API** that accepts an order reference + amount + currency and returns either a redirect URL or QR payload.
2. A **server-to-server IPN / webhook** that fires on terminal payment states (`SUCCESS`, `FAILED`, `EXPIRED`, optionally `REFUNDED`).
3. A **deterministic signature scheme** (HMAC-SHA256 or RSA) over a documented field set, so Bluecom can verify both outgoing requests and incoming IPNs.
4. A **sandbox environment** with test credentials and test cards / test bank QR.

## How to read the rest of this section

| Page | Read if you want to know… |
|------|---------------------------|
| [Architecture](architecture.md) | Where your gateway sits in the Bluecom stack, request/IPN flow, WebView/iframe constraints. |
| [Checklist](checklist.md) | The concrete deliverables and what Bluecom will build on its side. |
| [Webhook Contract](webhook-contract.md) | Field-level spec for create-payment, IPN, and signature. *(Draft — finalised per partner.)* |
| [Testing & Go-Live](testing.md) | Sandbox flow, certification cases, production cutover. |
| [Timeline](timeline.md) | Expected duration for an end-to-end integration. |
