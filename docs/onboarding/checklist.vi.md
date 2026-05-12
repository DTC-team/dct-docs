# Danh sách kiểm tra tích hợp

| # | Bước | Chủ sở hữu | Thời gian xử lý |
|---|------|------------|-----------------|
| 1 | Gửi [yêu cầu onboarding](request-access.md) — pháp nhân, domains, brand tokens, email liên hệ | Đối tác | — |
| 2 | Bluecom cấp `partnerCode` và `partnerSecret` (chia sẻ qua 1Password hoặc email mã hóa PGP) | Bluecom | 1 ngày làm việc |
| 3 | Bluecom khởi tạo bản ghi đối tác (cấu hình auth, đối tác phân phối, kênh, theme class) và thêm domain của bạn vào allowlist CSP của iframe | Bluecom | 2 ngày làm việc |
| 4 | Đối tác triển khai bắt tay (handshake) [Authentication](../integration/authentication.md) ở backend và điểm vào [Embedding](../integration/embedding.md) ở frontend/app | Đối tác | — |
| 5 | Smoke test phối hợp trên **staging** → ký xác nhận → chuyển sang URL **production** | Cả hai | 1 ngày làm việc |

**Tổng: ~5 ngày làm việc từ lúc yêu cầu đến khi sẵn sàng trên staging.**

## Trước khi go-live

- [ ] `partnerSecret` chỉ tồn tại trên backend của bạn (không nằm trong app bundle hay repo).
- [ ] URL bắt tay được sinh mới mỗi lần mở Shop (không cache).
- [ ] HTTPS xuyên suốt.
- [ ] Domain production đã được xác nhận trong allowlist CSP của Bluecom (đối tác iframe).
- [ ] Đã xác thực `event.origin` trong listener postMessage (đối tác iframe).
- [ ] Đã nhận xác nhận smoke test từ đội vận hành Bluecom.
