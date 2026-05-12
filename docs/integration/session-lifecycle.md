# Session Lifecycle

The Shop issues an `httpOnly`, `secure`, `sameSite=none`, `partitioned` cookie on successful handshake.

| Property | Value |
|----------|-------|
| Lifetime | **24 hours** |
| Auto-refresh inside window | Yes (API tokens refreshed transparently) |
| After expiry | Shop redirects to its own `/sign-in` — a dead-end for partner-embedded users |

## Recommended partner behavior (v1)

> Open the Shop with a **freshly generated handshake URL** every time the user enters the Shop UI in your app. Do not cache the URL or rely on persisted sessions across app launches.

## Roadmap

A `shop.auth_expired` event (postMessage for iframe, JS bridge for WebView) will let partner hosts re-handshake without user-visible disruption. No date committed.
