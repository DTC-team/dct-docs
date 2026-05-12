# Tổng quan

Bluecom eSIM Shop là một storefront có thể nhúng, cho phép người dùng của bạn duyệt, mua và quản lý các gói dữ liệu eSIM mà không cần rời khỏi ứng dụng.

## Dành cho ai

Các kỹ sư tích hợp tại tổ chức đối tác đã ký thỏa thuận với Bluecom và đã được cấp `partnerCode` cùng `partnerSecret`.

## Các chế độ nhúng được hỗ trợ

- **iframe** — website desktop/responsive nhúng Shop trong một thẻ `<iframe>`.
- **WebView** — ứng dụng mobile native nhúng Shop trong WebView của hệ thống (iOS `WKWebView`, Android `WebView`).
- **Telegram Mini App** — xem [Nhúng › Telegram Mini App](../integration/embedding.md#telegram-mini-app).

## Bạn nhận được gì sẵn có

- Bắt tay (handshake) SSO bằng HMAC-SHA256 — không yêu cầu mật khẩu từ người dùng cuối.
- Storefront được thương hiệu hóa theo `partnerCode` của bạn (màu sắc, logo).
- Phiên người dùng 24 giờ dựa trên cookie.
- Sự kiện theo dõi qua postMessage để kết nối với hệ thống phân tích.

## Bước tiếp theo

Tiếp tục đến [Kiến trúc](architecture.md) để xem luồng dữ liệu tổng thể, sau đó chuyển sang [Onboarding](../onboarding/index.md).
