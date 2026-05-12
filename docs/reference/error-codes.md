# Error Codes

Canonical errors returned by the Bluecom Auth service during the handshake.

| Code | HTTP | Cause | Fix |
|------|------|-------|-----|
| `UNKNOWN_PROVIDER` | 400 | `partnerCode` is unknown, inactive, or not of type `hmac` | Verify provisioning with Bluecom ops. Check that you're using the right environment's `partnerCode`. |
| `VERIFICATION_FAILED` | 401 | HMAC mismatch, expired timestamp, wrong secret, or malformed canonical string | Recompute the token. Check clock skew via NTP. Verify the secret matches the environment. |

## Debugging checklist

1. Is `timestamp` in **seconds**, not milliseconds?
2. Is the signed string exactly `userId:timestamp` — no spaces, no JSON?
3. Is the token **lowercase hex**?
4. Is `partnerSecret` from the correct environment (staging vs production)?
5. Is server time within ±5 minutes of UTC?
