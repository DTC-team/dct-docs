# Lộ trình

Một payment gateway mới được tích hợp **end-to-end trong vòng một tháng**, với giả định đối tác cung cấp spec đầy đủ, sandbox hoạt động ổn định và một kỹ sư đối tác trả lời nhanh các câu hỏi. Lịch dưới đây là track chuẩn mà Bluecom cam kết.

## End-to-end: 4 tuần làm việc

| Tuần | Giai đoạn | Đảm trách | Tiêu chí kết thúc |
|------|-----------|-----------|--------------------|
| **Tuần 1** | Trước tích hợp + triển khai adapter | Đối tác + Backend Bluecom | Đã nhận spec, đã cấp credentials sandbox, adapter provider và pipeline ký đã vào chỗ, unit tests xanh. |
| **Tuần 2** | Đấu nối WebView / iframe + E2E happy-path sandbox | Backend + Frontend Bluecom | Shop UI render được redirect/QR của đối tác; một giao dịch thực hoàn tất end-to-end trên sandbox; đơn hàng chuyển `PAID`. |
| **Tuần 3** | Edge case & certification | QA Bluecom + đối tác | Toàn bộ [cổng acceptance](checklist.md#cong-acceptance) pass: cancel, expiry, replay, sai chữ ký, đối soát. |
| **Tuần 4** | Hardening trước production + cutover production | Bluecom + vận hành đối tác | Idempotency được verify dưới tải, observability và runbook sẵn sàng, đã thay credentials production, canary trên một kênh bán hàng lưu lượng thấp, rollout dần. |

Đây là track chuẩn. Phần lớn gateway nội địa VN đi theo khuôn NeoPay đều nằm gọn trong khung này mà không bị trượt.

## Baseline tham chiếu: NeoPay

NeoPay là baseline đã được chứng minh. Nền tảng Bluecom — abstraction dịch vụ thanh toán, pipeline ký, kho audit, handler IPN idempotent, job đối soát, chính sách kênh bán hàng — đều đã có sẵn từ tích hợp đó; nhờ vậy một provider mới hoàn tất trong bốn tuần thay vì xây từ đầu.

## Điều gì có thể kéo dài lịch (cộng thêm 1–2 tuần mỗi mục)

- Scheme ký riêng hoặc không có tài liệu, phải reverse-engineering với sandbox.
- Hosted payment page **không thể** nhúng — buộc phải thiết kế lại luồng checkout của Shop cho nhà cung cấp đó.
- Không có endpoint query-payment — Bluecom phải xây fallback polling cho đối soát.
- Đa tiền tệ / settlement FX không khớp mô hình Ordering hiện tại.
- Rà soát compliance (thay đổi phạm vi PCI, phê duyệt SBV / NHNN nếu mở rail thanh toán mới cho một kênh có quản lý).
