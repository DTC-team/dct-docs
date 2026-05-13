# Tích hợp Payment Gateway

Mục này dành cho **các nhà cung cấp cổng thanh toán** muốn kết nối gateway của mình vào nền tảng eSIM Bluecom, để người dùng cuối có thể thanh toán qua gateway đó ngay trong WebView / iframe checkout của Bluecom.

Nếu bạn là **Đối tác đang nhúng Bluecom** và chỉ cần được thông báo khi một giao dịch thanh toán hoàn tất, hãy xem [Tích hợp → Trả về thanh toán](../integration/payment-return.md).

## Đối tượng phù hợp

- Gateway nội địa Việt Nam (QR ngân hàng, thẻ, ví) — cùng loại với tích hợp tham chiếu hiện tại của chúng tôi là **Neox / NeoPay**.
- PSP quốc tế (thẻ / APM) cung cấp **hosted payment page** (redirect/iframe) hoặc **API tạo thanh toán server-to-server** trả về redirect URL.

## Yêu cầu Bluecom đặt ra với gateway của bạn

Tối thiểu:

1. Một **API tạo thanh toán** nhận order reference + amount + currency và trả về redirect URL hoặc QR payload.
2. Một **IPN / Webhook server-to-server** kích hoạt khi giao dịch chuyển sang trạng thái cuối (`SUCCESS`, `FAILED`, `EXPIRED`, tuỳ chọn `REFUNDED`).
3. Một **scheme ký dữ liệu xác định** (HMAC-SHA256 hoặc RSA) trên một tập trường được tài liệu hoá, để Bluecom có thể verify cả request gửi đi lẫn IPN nhận về.
4. Một **môi trường sandbox** kèm credentials test và thẻ test / QR ngân hàng test.

## Đọc tiếp gì

| Trang | Đọc khi bạn cần biết… |
|------|---------------------------|
| [Kiến trúc](architecture.md) | Vị trí gateway trong stack Bluecom, luồng request/IPN, ràng buộc WebView/iframe. |
| [Danh sách kiểm tra](checklist.md) | Các hạng mục bàn giao cụ thể và phần Bluecom sẽ làm. |
| [Hợp đồng Webhook](webhook-contract.md) | Spec chi tiết cấp trường cho create-payment, IPN, và chữ ký. *(Bản nháp — chốt theo từng đối tác.)* |
| [Kiểm thử & Go-Live](testing.md) | Luồng sandbox, các case certification, cutover production. |
| [Lộ trình](timeline.md) | Thời gian dự kiến cho một tích hợp end-to-end. |
