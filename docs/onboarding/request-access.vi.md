# Yêu cầu cấp quyền truy cập

Gửi nội dung sau tới `integration@bluecom.com.vn`. Bluecom phản hồi kèm thông tin xác thực trong vòng 1 ngày làm việc.

```
Pháp nhân:              <Công ty TNHH ABC>
partnerCode mong muốn:  <slug, chữ thường, ví dụ "acme-bank">
Domain production:      <https://app.acme.vn, https://m.acme.vn>
Chế độ nhúng:           <iframe | webview | cả hai>
Brand tokens:
  - Màu chủ đạo:        <#RRGGBB hoặc oklch(...)>
  - Logo URL:           <https://...>
Kênh / tiền tệ:         <ví dụ VND, kênh mặc định>
Liên hệ kỹ thuật (email): <eng-lead@acme.vn>
Phương thức bàn giao secret: <email tài khoản 1Password | PGP key fingerprint>
Webhook URL (chưa xác định): <https://api.acme.vn/bluecom/webhook>
```

## Ghi chú

- **Domain production** được dùng để xây allowlist `frame-ancestors` của CSP iframe. Liệt kê mọi host sẽ nhúng Shop.
- **`partnerCode`** là cố định và người dùng cuối nhìn thấy được trong URL — hãy chọn một slug gọn gàng, chữ thường.
- **Phương thức bàn giao secret**: ưu tiên 1Password. PGP cũng được nếu đội của bạn vận hành keyring có quản lý.
- **Webhook URL** là tùy chọn cho tới khi [hợp đồng payment return](../integration/payment-return.md) được chốt.
