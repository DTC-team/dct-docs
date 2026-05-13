# Danh sách kiểm tra tích hợp

Chia hai cột: phần **partner gateway** phải bàn giao, và phần **Bluecom** xây dựng bên trên. Cả hai đều phải xanh trước khi go-live.

## Hạng mục đối tác bàn giao

### 1. Spec & credentials
- [ ] Tài liệu spec API (PDF / OpenAPI) cho create-payment, query-payment, refund (nếu có) và IPN.
- [ ] Spec chữ ký cấp trường: thuật toán hash, thứ tự trường, vị trí secret key.
- [ ] Sandbox `ApiUrl`, `MerchantCode`, `SecretKey`.
- [ ] Production `ApiUrl`, `MerchantCode`, `SecretKey` (chỉ bàn giao ngay trước cutover).
- [ ] Test data: thẻ, tài khoản ngân hàng test, payload QR test, trigger giả lập lỗi.

### 2. Endpoints
- [ ] Endpoint create-payment trả về **hoặc** một `redirectUrl` (hosted page) **hoặc** một `qrPayload` + `expiresAt`.
- [ ] Endpoint query-payment (phục vụ đối soát và khôi phục đơn hàng treo).
- [ ] IPN POST tới URL do Bluecom sở hữu khi giao dịch vào trạng thái cuối.

### 3. Tương thích WebView / iframe
- [ ] Hosted payment page cho phép Bluecom nhúng (không có `X-Frame-Options` / `frame-ancestors` chặn).
- [ ] Trang responsive cho mobile (≥ 360 px).
- [ ] Trang tôn trọng query parameter `returnUrl` cả khi thành công **và** khi huỷ.
- [ ] Không bắt buộc third-party cookies.

### 4. Bảo mật & vận hành
- [ ] IPN an toàn trước replay (timestamp hoặc nonce nằm trong payload đã ký).
- [ ] Tài liệu hoá retry policy (interval, số lần tối đa).
- [ ] Tài liệu hoá quy trình xoay secret.
- [ ] Allow-list IP cố định cho IPN gửi đi (nếu có) — Bluecom sẽ đăng ký.
- [ ] Đầu mối hỗ trợ + SLA cho sandbox và production.

## Phần Bluecom thực hiện

Các hạng mục này chạy song song và do Bluecom đảm trách. Liệt kê ở đây để đối tác hình dung phạm vi.

- [ ] Adapter provider xây trên contract dịch vụ thanh toán của Bluecom.
- [ ] Pipeline ký được cấu hình theo tập trường có thứ tự và thuật toán của đối tác.
- [ ] Cấu hình được nối end-to-end qua sandbox và production.
- [ ] Chính sách kênh bán hàng được cập nhật để mở phương thức thanh toán mới trên các kênh mục tiêu.
- [ ] Bộ functional test phủ: create-payment success/failure, IPN success/failure/replay/sai chữ ký, redirect handler, redelivery idempotent.
- [ ] Job đối soát dùng endpoint query-payment của đối tác.
- [ ] Observability và mục runbook.

## Cổng acceptance

Một tích hợp được xem là "xong" khi, trên môi trường **sandbox**:

1. Người dùng có thể hoàn tất một thanh toán happy-path end-to-end trong Bluecom Shop WebView.
2. Thanh toán bị huỷ đưa người dùng về Shop đúng trạng thái.
3. Thanh toán hết hạn được dọn dẹp tự động, không cần thao tác tay.
4. Replay IPN không cộng kép đơn hàng.
5. IPN bị giả mạo (sai chữ ký) bị từ chối và được log lại.
6. Đối soát một đơn hàng "treo" qua query-payment hội tụ về đúng trạng thái.
7. Toàn bộ bộ functional test pass với nhà cung cấp mới.
