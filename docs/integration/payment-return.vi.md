# Payment Return

!!! warning "Trạng thái: Đang xác định"
    Hợp đồng để thông báo cho ứng dụng đối tác khi người dùng hoàn tất hoặc bỏ dở thanh toán đang được hoàn thiện. Đặc tả cuối cùng, cấu trúc payload, và cơ chế chữ ký sẽ được công bố **trước khi bất kỳ đối tác nào triển khai lên Production**.

## Hướng đã xác nhận

| Kênh | Mục đích |
|------|----------|
| **Webhook phía máy chủ** | Nguồn sự thật cho đối soát. URL do đối tác đăng ký sẽ nhận các POST sự kiện đơn hàng đã ký. |
| **postMessage** | Tiện ích trải nghiệm cho đối tác dùng `iframe` — cập nhật UI kiểu fire-and-forget. |
| **Deep-link `returnUrl`** | Dành cho đối tác `WebView` native có URL scheme (ví dụ `acme://payment-result`). |

## Cần chuẩn bị trước

- Đăng ký URL Webhook trong [onboarding](../onboarding/request-access.md) (trường `Webhook URL`). Bluecom sẽ kích hoạt khi hợp đồng được phát hành.
- Nếu bạn nhúng qua `WebView`, hãy giữ sẵn một URL scheme cho payment return ngay từ bây giờ.
- Lên kế hoạch xử lý idempotency ở phía bạn — sự kiện đơn hàng có thể được gửi lại.

Theo dõi release notes để nhận đặc tả cuối cùng.
