# Môi trường

Bluecom vận hành hai môi trường tách biệt. Thông tin xác thực và dữ liệu không dùng chéo giữa hai bên.

| Môi trường | Hostname | Mục đích |
|------------|----------|----------|
| Staging | `<TBD: staging>` | Phát triển tích hợp, smoke test, ký xác nhận phối hợp |
| Production | `<TBD: production>` | Lưu lượng người dùng cuối thực tế |

## Thông tin xác thực

Mỗi môi trường có `partnerCode` / `partnerSecret` riêng. Secret staging được cấp tại bước 2 của onboarding; secret production được cấp khi ký xác nhận (bước 5 của onboarding).

## Chuyển môi trường

Dùng chung một đường code cho cả hai môi trường và chuyển đổi qua biến môi trường:

```bash
BLUECOM_SHOP_HOST=https://<staging-host>
BLUECOM_PARTNER_SECRET=<staging secret>
```

Không hard-code hostname hay secret vào client bundle. Xem [Authentication › Security rules](../integration/authentication.md#security-rules).
