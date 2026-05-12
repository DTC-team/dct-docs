# Thuật ngữ

| Term | Ý nghĩa |
|------|---------|
| **`partnerCode`** | Định danh nhà cung cấp do Bluecom cấp cho bạn. Tương đương `providerId` trong Auth service. |
| **`partnerSecret`** | Khóa HMAC dùng chung. **Chỉ lưu ở phía server.** Được luân chuyển khi yêu cầu bộ phận vận hành Bluecom. |
| **Handshake** | Bộ ba `{token, userId, timestamp}` được ký HMAC, kèm `partnerCode`, truyền qua tham số URL trên Entry URL của Shop. |
| **Channel** | Cấu hình giá/thanh toán gắn với hồ sơ reseller của bạn trong Bluecom. |
| **Reseller** | Thuật ngữ nội bộ của Bluecom dùng để chỉ đối tác. |
| **Entry URL** | URL gốc của Shop kèm các tham số handshake. Xem [Nhúng](../integration/embedding.md#entry-url). |
| **Mini App** | Bản nhúng Shop dưới dạng Telegram WebApp. Xem [Nhúng › Telegram Mini App](../integration/embedding.md#telegram-mini-app). |
