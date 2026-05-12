# Integration

Four things to wire up:

1. **[Authentication](authentication.md)** — sign the HMAC handshake on your backend.
2. **[Embedding](embedding.md)** — open the Shop in an iframe, WebView, or Telegram Mini App.
3. **[Session lifecycle](session-lifecycle.md)** — how the 24-hour cookie behaves and what to do on expiry.
4. **[Payment return](payment-return.md)** — notify your app when the user finishes (or abandons) checkout. **Contract TBD.**

## Mental model

> Your **backend** mints a short-lived signed URL. Your **frontend** opens it. The Shop verifies the signature, issues a session cookie, and renders.

The Shop is self-contained inside the iframe/WebView. You do not call any Bluecom API directly during normal operation — events come back via [tracking events](../operations/tracking-events.md) and (eventually) the payment webhook.
