# Nhúng

URL của Shop luôn là **root**. Việc định tuyến giữa các view dành cho `iframe` và `WebView` được quyết định tự động.

## URL khởi đầu

```
https://<shop-host>/?partnerCode=<code>&userId=<id>&timestamp=<unix>&token=<hex>
                    [&locale=vi|en]
                    [&returnUrl=<url-encoded>]
```

| Tham số | Bắt buộc | Ghi chú |
|---------|----------|---------|
| `partnerCode`, `userId`, `timestamp`, `token` | có | Xem [Authentication](authentication.md). |
| `locale` | không | `vi` (mặc định) hoặc `en`. Ghi đè cookie. |
| `returnUrl` | không | Chuyển hướng sau khi thanh toán. Xem [Payment return](payment-return.md) — **hợp đồng đang xác định**. |

Deep-link tới các route bên trong **không được hỗ trợ ở v1**. Luôn mở root.

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

Domain Production của bạn phải nằm trong allowlist `frame-ancestors` của `CSP` Bluecom (đăng ký trong quá trình onboarding).

## WebView native

### iOS (Swift / WKWebView)

```swift
let url = URL(string: shopUrl)! // lấy từ backend của bạn
let config = WKWebViewConfiguration()
config.websiteDataStore = .default() // cookie được lưu lại
let webView = WKWebView(frame: view.bounds, configuration: config)
webView.load(URLRequest(url: url))
```

### Android (Kotlin / WebView)

```kotlin
webView.settings.javaScriptEnabled = true
webView.settings.domStorageEnabled = true
CookieManager.getInstance().setAcceptThirdPartyCookies(webView, true)
webView.loadUrl(shopUrl) // lấy từ backend của bạn
```

### Yêu cầu

- Bật JavaScript và DOM storage.
- Bật cookie; `WebView` phải chấp nhận `sameSite=none; secure; partitioned`.
- HTTPS ở Production.

## Telegram Mini App

Dành cho đối tác xây dựng Telegram Bot Mini App:

- Mở Shop làm URL của Mini App với chỉ `?partnerCode=<code>` — handshake `token/userId/timestamp` **không** được sử dụng.
- Shop đọc `window.Telegram.WebApp.initData` (payload đã ký của Telegram) làm thông tin xác thực thay cho `HMAC`.
- Trường `start_param` của Mini App có thể mang `partnerCode` như một phương án dự phòng.
- Tất cả các mục khác (giao diện, phiên, theo dõi, payment return) áp dụng nguyên trạng.

Phối hợp với đội vận hành Bluecom để đăng ký domain bot và bật xác minh `initData`.
