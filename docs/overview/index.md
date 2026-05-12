# Overview

Bluecom eSIM Shop is an embeddable storefront that lets your users browse, purchase, and manage eSIM data plans without leaving your app.

## Who this is for

Technical integrators at partner organizations who have a signed agreement with Bluecom and have been issued a `partnerCode` and `partnerSecret`.

## Supported embedding modes

- **iframe** — desktop/responsive website embeds the Shop in an `<iframe>`.
- **WebView** — native mobile app embeds the Shop in a system WebView (iOS `WKWebView`, Android `WebView`).
- **Telegram Mini App** — see [Embedding › Telegram Mini App](../integration/embedding.md#telegram-mini-app).

## What you get out of the box

- HMAC-SHA256 SSO handshake — no end-user password required.
- Branded storefront keyed off your `partnerCode` (colors, logo).
- Cookie-backed 24-hour user session.
- postMessage tracking events for analytics wiring.

## What's next

Continue to [Architecture](architecture.md) for the high-level data flow, then move to [Onboarding](../onboarding/index.md).
