# Embedding

The Shop URL is always the **root**. Routing between iframe and WebView views is decided automatically.

## Entry URL

```
https://<shop-host>/?partnerCode=<code>&userId=<id>&timestamp=<unix>&token=<hex>
                    [&locale=vi|en]
                    [&returnUrl=<url-encoded>]
```

| Param | Required | Notes |
|-------|----------|-------|
| `partnerCode`, `userId`, `timestamp`, `token` | yes | See [Authentication](authentication.md). |
| `locale` | no | `vi` (default) or `en`. Overrides cookie. |
| `returnUrl` | no | Post-checkout redirect. See [Payment return](payment-return.md) — **contract TBD**. |

Deep-linking to inner routes is **not supported in v1**. Always open the root.

## iframe (desktop web)

```html
<iframe
  src="https://<shop-host>/?partnerCode=...&userId=...&timestamp=...&token=..."
  width="100%"
  height="800"
  allow="payment; clipboard-write"
  style="border: 0;"
></iframe>
```

Your production domain(s) must be in Bluecom's CSP `frame-ancestors` allowlist (submitted during onboarding).

## Native WebView

### iOS (Swift / WKWebView)

```swift
let url = URL(string: shopUrl)! // from your backend
let config = WKWebViewConfiguration()
config.websiteDataStore = .default() // cookies persist
let webView = WKWebView(frame: view.bounds, configuration: config)
webView.load(URLRequest(url: url))
```

### Android (Kotlin / WebView)

```kotlin
webView.settings.javaScriptEnabled = true
webView.settings.domStorageEnabled = true
CookieManager.getInstance().setAcceptThirdPartyCookies(webView, true)
webView.loadUrl(shopUrl) // from your backend
```

### Requirements

- JavaScript and DOM storage enabled.
- Cookies enabled; the WebView must accept `sameSite=none; secure; partitioned`.
- HTTPS in production.

## Telegram Mini App

For partners building a Telegram Bot Mini App:

- Open the Shop as the Mini App URL with `?partnerCode=<code>` only — handshake `token/userId/timestamp` are **not** used.
- The Shop reads `window.Telegram.WebApp.initData` (Telegram's signed payload) as the auth credential instead of HMAC.
- The Mini App `start_param` may carry `partnerCode` as a fallback.
- All other sections (theming, session, tracking, payment return) apply unchanged.

Coordinate with Bluecom ops to register your bot domain and enable `initData` verification.
