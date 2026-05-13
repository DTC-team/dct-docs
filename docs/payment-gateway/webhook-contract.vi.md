# Hợp đồng Webhook

!!! warning "Trạng thái: Bản nháp"
    Hợp đồng cấp trường bên dưới là **bản mặc định phía Bluecom**, lấy từ tích hợp tham chiếu NeoPay. Đây là điểm khởi đầu cho mọi đối tác mới; hình dạng cuối cùng sẽ được thương lượng và đóng băng theo từng nhà cung cấp trước khi vào certification sandbox.

## Request create-payment (Bluecom → Partner)

`POST {ApiUrl}/<partner-create-payment-path>`

| Trường | Kiểu | Ghi chú |
|-------|------|-------|
| `merchantCode` | string | Do đối tác cấp. |
| `orderId` | string | Order reference của Bluecom. Duy nhất mỗi lần attempt. |
| `amount` | integer | Đơn vị nhỏ nhất (VND không có đơn vị nhỏ → integer đồng). |
| `currency` | string | ISO 4217. |
| `description` | string | Hiển thị cho người dùng trên hosted page. |
| `returnUrl` | string | Do Bluecom sở hữu; phải tôn trọng cả khi thành công **và** khi huỷ. |
| `ipnUrl` | string | Endpoint IPN do Bluecom sở hữu. |
| `expiresAt` | string (ISO 8601) | Tuỳ chọn; đối tác có thể áp giới hạn của riêng mình. |
| `signature` | string | HMAC-SHA256 trên tập trường có thứ tự, hex chữ thường. |

Response (thành công):

```json
{
  "providerRef": "string",
  "redirectUrl": "https://...",
  "qrPayload": "string|null",
  "expiresAt": "2026-05-13T10:15:00Z"
}
```

Đúng một trong `redirectUrl` hoặc `qrPayload` phải có mặt.

## IPN (Partner → Bluecom)

`POST https://api.bluecom.*/api/payment/ipn`

| Trường | Kiểu | Ghi chú |
|-------|------|-------|
| `merchantCode` | string | |
| `orderId` | string | Echo `orderId` của Bluecom. |
| `providerRef` | string | Mã giao dịch phía đối tác. |
| `status` | enum | `SUCCESS` / `FAILED` / `EXPIRED` / `REFUNDED`. |
| `amount` | integer | Phải khớp create request. |
| `currency` | string | |
| `paidAt` | string (ISO 8601) | Bắt buộc khi `SUCCESS`. |
| `timestamp` | string (ISO 8601) | Chống replay. Bị từ chối nếu lệch > 5 phút. |
| `nonce` | string | Tuỳ chọn; dùng khi `timestamp` không đủ. |
| `signature` | string | Cùng scheme với create request. |

Bluecom ack `200 OK` body rỗng ngay sau khi verify chữ ký và persist IPN bền vững vào kho audit của Bluecom. Việc chuyển trạng thái đơn hàng sau đó diễn ra bất đồng bộ qua kênh giao tin cậy; đối tác không cần chờ.

## Browser return (Partner → Bluecom)

`GET https://api.bluecom.*/api/payment/result?...signed-fields...`

Cùng tập trường với IPN, mang qua query string. Dùng **chỉ** để redirect người dùng về Shop UI — không bao giờ dùng để chốt đơn hàng.

## Scheme chữ ký

Mặc định:

```
hex(hmac_sha256(secret, join("|", ordered_fields)))
```

Trong đó `ordered_fields` là phép nối lexicographic các trường không phải `signature` theo thứ tự được tài liệu hoá. Đối tác dùng scheme khác (RSA, separator khác, casing khác) phải công bố thuật toán chính xác; Bluecom sẽ implement theo nhưng sẽ không tự nghĩ ra.
