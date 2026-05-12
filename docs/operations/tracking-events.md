# Tracking Events

For iframe embeds, the Shop emits `window.parent.postMessage(...)` on key lifecycle moments. Use these to wire your own analytics.

## Event catalog

| Event | When | Payload |
|-------|------|---------|
| `shop.ready` | First render after handshake | `{ type, partnerCode, userId }` |
| `shop.error` | Unrecoverable error (auth, network) | `{ type, code, message }` |
| `shop.purchase_intent` | User clicks "Buy" on a plan | `{ type, sku, price, currency }` |
| `shop.close_request` | User taps the close affordance | `{ type }` |
| `shop.payment_success` | Order paid | `{ type, orderId, sku, amount, currency }` — pending [payment return](../integration/payment-return.md) finalization |

## Listener example

```ts
window.addEventListener("message", (event) => {
  // ALWAYS validate origin against your configured Shop host
  if (event.origin !== "https://<shop-host>") return;

  const msg = event.data;
  if (msg?.type === "shop.close_request") {
    document.getElementById("bluecom-iframe")?.remove();
  }
  // handle other events
});
```

!!! danger "Validate `event.origin`"
    Always check `event.origin` against your configured Shop hostname before trusting the payload. Otherwise any page can forge events.

## Native WebView

The same events will be exposed via the WebView's JavaScript bridge (`window.webkit.messageHandlers` on iOS, `Android.postMessage` on Android). Bridge contract will be published alongside the [payment return](../integration/payment-return.md) spec.
