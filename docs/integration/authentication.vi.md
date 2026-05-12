# Authentication

Bluecom dùng **HMAC-SHA256** làm cơ chế SSO cho đối tác. Mỗi phiên Shop bắt đầu bằng một bắt tay (handshake) đã ký trên URL.

## Hợp đồng token

| Trường | Kiểu | Mô tả |
|--------|------|-------|
| `partnerCode` | string | ID nhà cung cấp của bạn, do Bluecom cấp. Truyền qua URL query param. |
| `userId` | string | Định danh ổn định của người dùng trong hệ thống **của bạn**. Là khóa liên kết tới tài khoản Shop của họ. |
| `timestamp` | integer | Unix epoch tính bằng **giây** (không phải mili-giây). |
| `token` | string | `hex(HMAC-SHA256(partnerSecret, "${userId}:${timestamp}"))`. **Hex chữ thường.** |

## Quy tắc kiểm tra

- `timestamp` phải nằm trong khoảng **±5 phút** so với giờ máy chủ, nếu không sẽ trả về `401 VERIFICATION_FAILED`.
- Chuỗi được ký là chính xác `userId:timestamp` — phân tách bằng dấu hai chấm, không khoảng trắng, không JSON.
- `token` được so sánh theo thời gian hằng số (constant time).
- `partnerCode` phải đang hoạt động và có kiểu `hmac`, nếu không sẽ trả về `400 UNKNOWN_PROVIDER`.

## Quy tắc bảo mật

1. **`partnerSecret` BẮT BUỘC chỉ tồn tại trên backend của bạn.** Không nhúng vào binary ứng dụng, bundle web, hoặc mã nguồn repo.
2. **Tạo `token` ngay trước khi mở URL Shop.** Cửa sổ 5 phút được thiết kế ngắn có chủ đích.
3. **`userId` phải ổn định cho mỗi người dùng cuối.** Thay đổi giá trị này sẽ tạo ra tài khoản Shop mới.
4. **HTTPS đầu-cuối.** Handshake qua HTTP thuần sẽ bị từ chối ở môi trường Production.

## Mã ví dụ

### Node.js

```ts
import crypto from "node:crypto";

const PARTNER_CODE = "acme-bank";
const PARTNER_SECRET = process.env.BLUECOM_PARTNER_SECRET!; // chỉ dùng ở server

export function buildShopUrl(userId: string): string {
  const timestamp = Math.floor(Date.now() / 1000);
  const token = crypto
    .createHmac("sha256", PARTNER_SECRET)
    .update(`${userId}:${timestamp}`)
    .digest("hex");

  const params = new URLSearchParams({
    partnerCode: PARTNER_CODE,
    userId,
    timestamp: String(timestamp),
    token,
  });
  return `https://<shop-host>/?${params.toString()}`;
}
```

### C# (.NET 8+)

```csharp
using System.Security.Cryptography;
using System.Text;
using System.Web;

public static class BluecomShopUrlBuilder
{
    private const string PartnerCode = "acme-bank";
    private static readonly string PartnerSecret =
        Environment.GetEnvironmentVariable("BLUECOM_PARTNER_SECRET")!;

    public static string Build(string userId)
    {
        var timestamp = DateTimeOffset.UtcNow.ToUnixTimeSeconds();
        var payload = $"{userId}:{timestamp}";

        using var hmac = new HMACSHA256(Encoding.UTF8.GetBytes(PartnerSecret));
        var hash = hmac.ComputeHash(Encoding.UTF8.GetBytes(payload));
        var token = Convert.ToHexString(hash).ToLowerInvariant();

        var qs = HttpUtility.ParseQueryString(string.Empty);
        qs["partnerCode"] = PartnerCode;
        qs["userId"] = userId;
        qs["timestamp"] = timestamp.ToString();
        qs["token"] = token;

        return $"https://<shop-host>/?{qs}";
    }
}
```

## Phản hồi lỗi

Xem [Reference › Error codes](../reference/error-codes.md).
