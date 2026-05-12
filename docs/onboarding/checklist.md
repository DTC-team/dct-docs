# Integration Checklist

| # | Step | Owner | Lead time |
|---|------|-------|-----------|
| 1 | Submit the [onboarding request](request-access.md) — legal entity, domains, brand tokens, contact email | Partner | — |
| 2 | Bluecom issues `partnerCode` and `partnerSecret` (1Password share or PGP-encrypted email) | Bluecom | 1 business day |
| 3 | Bluecom provisions your partner record (auth config, reseller, channel, theme class) and adds your domain to the iframe CSP allowlist | Bluecom | 2 business days |
| 4 | Partner implements the [Authentication](../integration/authentication.md) handshake on the backend and the [Embedding](../integration/embedding.md) entry on the frontend/app | Partner | — |
| 5 | Joint smoke test on **staging** → sign-off → switch to **production** entry URL | Both | 1 business day |

**Total: ~5 business days from request to staging-ready.**

## Before you go live

- [ ] `partnerSecret` lives only on your backend (not in app bundles or repos).
- [ ] Handshake URL is generated fresh on every Shop open (no caching).
- [ ] HTTPS end-to-end.
- [ ] Production domain confirmed in Bluecom's CSP allowlist (iframe partners).
- [ ] `event.origin` validation in postMessage listener (iframe partners).
- [ ] Smoke test sign-off received from Bluecom ops.
