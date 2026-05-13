# Integration Checklist

Two columns: what **the partner gateway** must deliver, and what **Bluecom** builds on top. Both must be green before go-live.

## Partner deliverables

### 1. Specification & credentials
- [ ] API spec document (PDF / OpenAPI) for create-payment, query-payment, refund (if applicable), and IPN.
- [ ] Field-level signature spec: hash algorithm, ordered field list, secret-key placement.
- [ ] Sandbox `ApiUrl`, `MerchantCode`, `SecretKey`.
- [ ] Production `ApiUrl`, `MerchantCode`, `SecretKey` (delivered just before cutover).
- [ ] Test data: cards, test bank accounts, QR test payloads, simulated failure triggers.

### 2. Endpoints
- [ ] Create-payment endpoint returning **either** a `redirectUrl` (hosted page) **or** a `qrPayload` + `expiresAt`.
- [ ] Query-payment endpoint (for reconciliation and stuck-order recovery).
- [ ] IPN that POSTs to a Bluecom-owned URL on every terminal state.

### 3. WebView / iframe compatibility
- [ ] Hosted payment page allows being embedded by Bluecom domains (no blocking `X-Frame-Options` / `frame-ancestors`).
- [ ] Page is mobile-responsive (≥ 360 px).
- [ ] Page honours a `returnUrl` query parameter on success **and** cancel.
- [ ] No mandatory third-party cookies.

### 4. Security & operations
- [ ] Replay-safe IPN (timestamp or nonce inside the signed payload).
- [ ] Documented retry policy (interval, max attempts).
- [ ] Documented secret-rotation procedure.
- [ ] Static IP allow-list for outbound IPN (if available) — Bluecom will register.
- [ ] Support contact + SLA for sandbox and production incidents.

## Bluecom-side work

These items run in parallel and are owned by Bluecom. Listed for transparency so partners know what to expect.

- [ ] Provider adapter built against Bluecom's payment-service contract.
- [ ] Signing pipeline configured for the partner's ordered field set and algorithm.
- [ ] Configuration plumbed end-to-end across sandbox and production.
- [ ] Sales-channel policy updated so the new payment method is offered on the intended channels.
- [ ] Functional test pack covering: create-payment success/failure, IPN success/failure/replay/bad-signature, redirect handler, idempotent re-delivery.
- [ ] Reconciliation job using the partner's query-payment endpoint.
- [ ] Observability and runbook entry.

## Acceptance gate

An integration is "done" when, on the **sandbox** environment:

1. A user can complete a happy-path payment end-to-end inside the Bluecom Shop WebView.
2. A cancelled payment returns the user to the Shop with the correct state.
3. An expired payment is reaped without manual intervention.
4. IPN replay does not double-credit an order.
5. A tampered IPN (broken signature) is rejected and logged.
6. Reconciliation of a stuck order via query-payment converges to the correct state.
7. The full functional test pack passes against the new provider.
