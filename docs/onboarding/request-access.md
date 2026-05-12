# Request Access

Send the following to `integration@bluecom.com.vn`. Bluecom replies within 1 business day with credentials.

```
Legal entity:           <Company Ltd.>
Desired partnerCode:    <slug, lowercase, e.g. "acme-bank">
Production domain(s):   <https://app.acme.vn, https://m.acme.vn>
Embedding mode:         <iframe | webview | both>
Brand tokens:
  - Primary color:      <#RRGGBB or oklch(...)>
  - Logo URL:           <https://...>
Channel / currency:     <e.g. VND, default channel>
Tech contact (email):   <eng-lead@acme.vn>
Secret delivery:        <1Password account email | PGP key fingerprint>
Webhook URL (TBD):      <https://api.acme.vn/bluecom/webhook>
```

## Notes

- **Production domains** are used to build the iframe CSP `frame-ancestors` allowlist. List every host that will embed the Shop.
- **`partnerCode`** is permanent and user-visible in URLs — pick a clean, lowercase slug.
- **Secret delivery**: 1Password is preferred. PGP works if your team operates a managed keyring.
- **Webhook URL** is optional until the [payment return contract](../integration/payment-return.md) is finalized.
