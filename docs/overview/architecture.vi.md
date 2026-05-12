# Kiến trúc

Shop được khởi tạo từ một URL đã ký. **Backend** của đối tác giữ secret và ký bắt tay (handshake); **app/frontend** của đối tác không bao giờ thấy secret.

```mermaid
sequenceDiagram
    participant U as Người dùng cuối
    participant PA as App / Site của đối tác
    participant PB as Backend của đối tác
    participant S as Bluecom Shop
    participant AU as Bluecom Auth

    U->>PA: Tap "Buy eSIM"
    PA->>PB: Request handshake token
    PB->>PB: HMAC-SHA256(partnerSecret, "userId:timestamp")
    PB-->>PA: { token, userId, timestamp }
    PA->>S: Open Shop URL with partnerCode + token + userId + timestamp
    S->>AU: POST /provider/signin
    AU->>AU: Verify HMAC (±5min window)
    AU-->>S: Session cookie (httpOnly, 24h)
    S-->>U: Renders branded storefront
```

## Ranh giới tin cậy

| Thành phần | Giữ secret? | Giao tiếp với |
|-----------|---------------|----------|
| Backend của đối tác | **Có** | Chỉ app của đối tác |
| App/frontend của đối tác | Không | Backend của đối tác, URL của Shop |
| Bluecom Shop (browser/webview) | Không | Bluecom Auth |
| Bluecom Auth | Xác thực HMAC | Nội bộ |

Xem [Authentication](../integration/authentication.md) để biết hợp đồng token đầy đủ.
