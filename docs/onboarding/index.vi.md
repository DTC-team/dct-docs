# Onboarding

Tính từ đầu tới cuối, đưa một đối tác mới từ trạng thái "đã ký hợp đồng" tới "sẵn sàng trên staging" mất **~5 ngày làm việc**.

## Lộ trình

1. **[Yêu cầu cấp quyền truy cập](request-access.md)** — gửi mẫu onboarding.
2. Bluecom cấp `partnerCode` và `partnerSecret` cho bạn.
3. Bluecom khởi tạo bản ghi đối tác và thêm domain của bạn vào allowlist CSP của iframe.
4. Bạn triển khai bắt tay (handshake) [Authentication](../integration/authentication.md) và điểm vào [Embedding](../integration/embedding.md).
5. Smoke test phối hợp trên **staging** → ký xác nhận → chuyển sang **production**.

[Danh sách kiểm tra](checklist.md) chi tiết theo dõi chủ sở hữu và thời gian xử lý cho từng bước. [Môi trường](environments.md) liệt kê hostname của staging và production.
