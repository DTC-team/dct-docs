# Kiểm thử & Go-Live

## Các giai đoạn sandbox

1. **Smoke** — một thanh toán thành công, được verify trên monitoring dashboard của Bluecom và trong webhook audit log.
2. **Functional matrix** — đầy đủ các dòng trong [cổng acceptance](checklist.md#cong-acceptance).
3. **Soak** — 24 giờ traffic rate thấp liên tục trên sandbox để lộ các bug idempotency và lệch đồng hồ.

## Các test case bắt buộc

| Case | Kết quả mong đợi |
|------|-----------------|
| Happy path | Đơn hàng → `PAID`, chỉ phát đúng một event chốt đơn. |
| Người dùng huỷ trên hosted page | Đơn hàng → `CANCELLED`, người dùng được đưa về Shop. |
| Người dùng bỏ dở (đóng WebView) | Đơn hàng tự hết hạn sau `expiresAt` của đối tác. |
| IPN gửi hai lần | Đơn hàng chỉ chuyển trạng thái một lần; IPN thứ hai chỉ ack. |
| IPN sai chữ ký | Trả `4xx`, mục trong webhook audit log được đánh dấu sai. |
| IPN có timestamp cũ (> 5 phút) | Bị từ chối. |
| Đối soát đơn hàng "treo" | Query-payment hội tụ trạng thái mà không cần thao tác vận hành tay. |
| Refund (nếu hỗ trợ) | Đơn hàng → `REFUNDED`. |

## Go-live

- Đối tác bàn giao credentials production qua kênh bảo mật ngoài băng (không phải email plain text).
- Bluecom xoay credentials vào kho cấu hình production không downtime.
- Canary trên một kênh bán hàng lưu lượng thấp trong 48 giờ.
- Rollout dần ra các kênh còn lại khi error rate < 0.1 % và backlog đối soát = 0.
- Mục runbook được công bố trong Bluecom Operations.
