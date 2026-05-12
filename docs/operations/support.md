# Support

| Channel | Contact |
|---------|---------|
| Onboarding & business | `integrations@bluecom.vn` |
| Technical / production incidents | `<TBD ops contact>` |
| Status page | `<TBD>` |

## What to include in an incident report

- `partnerCode` and environment (staging / production).
- Timestamp (with timezone) of the failed request.
- `userId` (your system) involved, if any.
- HTTP status and error code from the response.
- Browser/WebView user-agent (for client-side issues).

This shortens triage significantly — Bluecom can correlate against `auth_provider_configs` and the auth service logs.
