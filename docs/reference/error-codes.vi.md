# Mã lỗi

Các lỗi chuẩn được Bluecom Auth service trả về trong quá trình bắt tay (handshake).

| Code | HTTP | Nguyên nhân | Cách khắc phục |
|------|------|-------------|----------------|
| `UNKNOWN_PROVIDER` | 400 | `partnerCode` không xác định, không hoạt động, hoặc không thuộc loại `hmac` | Xác minh việc cấp phát với bộ phận vận hành Bluecom. Kiểm tra bạn đang dùng đúng `partnerCode` của môi trường tương ứng. |
| `VERIFICATION_FAILED` | 401 | HMAC không khớp, `timestamp` hết hạn, sai secret, hoặc chuỗi canonical sai định dạng | Tính lại token. Kiểm tra lệch giờ qua NTP. Xác minh secret khớp với môi trường. |

## Danh sách kiểm tra khi gỡ lỗi

1. `timestamp` đang ở đơn vị **giây**, không phải mili-giây?
2. Chuỗi được ký có đúng là `userId:timestamp` — không có khoảng trắng, không phải JSON?
3. Token đã ở dạng **hex chữ thường** chưa?
4. `partnerSecret` có đúng môi trường (staging hay production) không?
5. Thời gian máy chủ có nằm trong khoảng ±5 phút so với UTC không?
