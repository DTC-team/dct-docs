# Architecture

The Shop boots from a signed URL. The partner's **backend** holds the secret and signs the handshake; the partner's **app/frontend** never sees the secret.

```mermaid
sequenceDiagram
    participant U as End User
    participant PA as Partner App / Site
    participant PB as Partner Backend
    participant S as Bluecom Shop
    participant AU as Bluecom Auth

    U->>PA: Tap "Buy eSIM"
    PA->>PB: Request handshake token
    PB->>PB: HMAC-SHA256(partnerSecret, "userId:timestamp")
    PB-->>PA: { token, userId, timestamp }
    PA->>S: Open Shop URL with partnerCode + token + userId + timestamp
    S->>AU: POST /provider/signin
    AU->>AU: Verify HMAC (±5min window)
    AU-->>S: Session cookie (httpOnly, 24h)
    S-->>U: Renders branded storefront
```

## Trust boundary

| Component | Holds secret? | Talks to |
|-----------|---------------|----------|
| Partner backend | **Yes** | Partner app only |
| Partner app/frontend | No | Partner backend, Shop URL |
| Bluecom Shop (browser/webview) | No | Bluecom Auth |
| Bluecom Auth | Verifies HMAC | Internal |

See [Authentication](../integration/authentication.md) for the full token contract.
