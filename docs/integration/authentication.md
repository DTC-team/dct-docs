# Authentication

Bluecom uses **HMAC-SHA256** as the partner SSO mechanism. Every Shop session begins with a signed handshake on the URL.

## Token contract

| Field | Type | Description |
|-------|------|-------------|
| `partnerCode` | string | Your provider ID, issued by Bluecom. URL query param. |
| `userId` | string | Stable identifier of the user in **your** system. The link key for their Shop account. |
| `timestamp` | integer | Unix epoch in **seconds** (not milliseconds). |
| `token` | string | `hex(HMAC-SHA256(partnerSecret, "${userId}:${timestamp}"))`. **Lowercase hex.** |

## Validation rules

- Timestamp must be within **±5 minutes** of server time, else `401 VERIFICATION_FAILED`.
- Signed string is exactly `userId:timestamp` — colon-separated, no spaces, no JSON.
- `token` is compared in constant time.
- `partnerCode` must be active and of type `hmac`, else `400 UNKNOWN_PROVIDER`.

## Security rules

1. **`partnerSecret` MUST live only on your backend.** Never embed it in app binaries, web bundles, or repo code.
2. **Mint the token immediately before opening the Shop URL.** The 5-minute window is short by design.
3. **`userId` must be stable per end user.** Changing it creates a new Shop account.
4. **HTTPS end-to-end.** Plain HTTP handshakes are rejected in production.

## Code samples

### Node.js

```ts
import crypto from "node:crypto";

const PARTNER_CODE = "acme-bank";
const PARTNER_SECRET = process.env.BLUECOM_PARTNER_SECRET!; // server-only

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

## Error responses

See [Reference › Error codes](../reference/error-codes.md).
