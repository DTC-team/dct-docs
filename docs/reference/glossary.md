# Glossary

| Term | Meaning |
|------|---------|
| **`partnerCode`** | Your provider identifier issued by Bluecom. Equals `providerId` in the Auth service. |
| **`partnerSecret`** | Shared HMAC key. **Server-only.** Rotated by request to Bluecom ops. |
| **Handshake** | The HMAC-signed `{token, userId, timestamp}` tuple plus `partnerCode`, passed as URL params on the Shop entry URL. |
| **Channel** | A pricing/payment configuration attached to your reseller record inside Bluecom. |
| **Reseller** | Bluecom's internal term for a partner. |
| **Entry URL** | The root Shop URL with the handshake parameters. See [Embedding](../integration/embedding.md#entry-url). |
| **Mini App** | A Telegram WebApp embedding of the Shop. See [Embedding › Telegram Mini App](../integration/embedding.md#telegram-mini-app). |
