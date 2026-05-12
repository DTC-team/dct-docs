# Tích hợp

Bốn việc cần kết nối:

1. **[Authentication](authentication.md)** — ký bắt tay (handshake) `HMAC` ở backend của bạn.
2. **[Embedding](embedding.md)** — mở Shop trong `iframe`, `WebView`, hoặc Telegram Mini App.
3. **[Session lifecycle](session-lifecycle.md)** — cookie 24 giờ hoạt động ra sao và cần làm gì khi hết hạn.
4. **[Payment return](payment-return.md)** — thông báo cho ứng dụng của bạn khi người dùng hoàn tất (hoặc bỏ dở) thanh toán. **Hợp đồng đang xác định.**

## Mô hình tư duy

> **Backend** của bạn tạo một URL đã ký với thời hạn ngắn. **Frontend** của bạn mở URL đó. Shop xác minh chữ ký, cấp cookie phiên (session), và hiển thị nội dung.

Shop là một khối khép kín bên trong `iframe`/`WebView`. Trong vận hành bình thường, bạn không gọi trực tiếp bất kỳ API nào của Bluecom — các sự kiện được trả về qua [tracking events](../operations/tracking-events.md) và (sau này) qua webhook thanh toán.
