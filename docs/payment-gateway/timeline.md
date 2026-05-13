# Timeline

A new payment gateway is integrated **end-to-end within one calendar month**, assuming the partner provides a complete spec, a working sandbox, and a responsive engineer for Q&A. The schedule below is the standard track that Bluecom commits to.

## End-to-end: 4 working weeks

| Week | Phase | Owner | Exit criteria |
|------|-------|-------|---------------|
| **Week 1** | Pre-integration + adapter implementation | Partner + Bluecom backend | Spec received, sandbox credentials issued, provider adapter and signing pipeline in place, unit tests green. |
| **Week 2** | WebView / iframe wiring + sandbox happy-path E2E | Bluecom backend + frontend | Shop UI renders the partner redirect/QR; one real payment completes end-to-end in sandbox; order transitions to `PAID`. |
| **Week 3** | Edge cases & certification | Bluecom QA + partner | The full [acceptance gate](checklist.md#acceptance-gate) passes: cancel, expiry, replay, bad-signature, reconciliation. |
| **Week 4** | Pre-production hardening + production cutover | Bluecom + partner ops | Idempotency verified under load, observability and runbook in place, production credentials rotated in, canary on a low-volume sales channel, gradual rollout. |

This is the standard track. Most domestic VN gateways that follow a NeoPay-shaped contract land inside it without overruns.

## Reference baseline: NeoPay

NeoPay is the proven baseline. The Bluecom platform — payment-service abstraction, signing pipeline, audit store, idempotent IPN handler, reconciliation jobs, sales-channel policy — is already in place from that integration, which is why a new provider lands in four weeks rather than starting from scratch.

## What can extend the schedule (add 1–2 weeks each)

- Bespoke or undocumented signing scheme that requires reverse-engineering against the sandbox.
- Hosted payment page **cannot** be embedded — forces a redesign of the Shop checkout flow for that provider.
- No query-payment endpoint — Bluecom must build a polling fallback for reconciliation.
- Multi-currency / FX settlement that doesn't fit the current Ordering model.
- Compliance review (PCI scope change, SBV / NHNN approval if a new payment rail is introduced for a regulated channel).
