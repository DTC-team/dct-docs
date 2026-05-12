# Đa ngôn ngữ

## Ngôn ngữ được hỗ trợ

| Mã | Ngôn ngữ | Mặc định |
|----|----------|----------|
| `vi` | Tiếng Việt | ✓ |
| `en` | Tiếng Anh | |

## Chọn ngôn ngữ

Truyền `?locale=vi` hoặc `?locale=en` trên [URL của Shop](../integration/embedding.md#entry-url). Tham số URL sẽ ghi đè tùy chọn lưu trong cookie của người dùng.

## Cơ chế fallback

Nếu thiếu `locale`, Shop sử dụng cookie từ phiên trước, sau đó fallback về `vi`.

## Thêm ngôn ngữ

Bluecom bổ sung ngôn ngữ theo yêu cầu của đối tác. Liên hệ `integration@bluecom.com.vn`.

## Thời gian xử lý

| Yêu cầu | Thời gian xử lý của Bluecom |
|---------|------------------------------|
| Bật một ngôn ngữ đã dịch sẵn cho `partnerCode` của đối tác | **1 ngày làm việc** |
| Chỉnh sửa chuỗi trong ngôn ngữ hiện có (sửa nội dung, từ ngữ thương hiệu) | **2 ngày làm việc** |
| Thêm ngôn ngữ hoàn toàn mới (dịch toàn bộ + QA) | **10 ngày làm việc** |
