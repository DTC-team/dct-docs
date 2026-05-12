# Partner Dashboard

Bluecom provisions every partner an account on the **Bluecom Marketplace** — a web dashboard for monitoring your integration end-to-end. You get the credentials during [onboarding](../onboarding/checklist.md) step 3.

## Access

| What | Value |
|------|-------|
| URL | `<TBD: marketplace host>` |
| Auth | Email + password (Better Auth) |
| Account provisioning | Bluecom ops creates one admin account per partner; you invite teammates via **Members** |
| Recommended browsers | Chromium-based, Firefox, Safari (latest 2 versions) |

## What's inside

The sidebar maps to the operational surfaces of your integration.

| Section | What it shows | Who uses it |
|---------|---------------|-------------|
| **Dashboard** | Pending payments, eSIM stock, activated and in-use counts; revenue/cost/profit by period (7/30/90 days, by quarter); leaderboards (top countries, products, members) | Business owner, ops lead |
| **Products** | Catalog of plans available to your channel — country, data, duration, price | Product, support |
| **eSIM** | Per-unit eSIM inventory and lifecycle state | Ops, support |
| **Insurance** | Travel insurance add-ons (if enabled on your channel) | Product |
| **Customers** | End users who came through your `partnerCode` | Support, CX |
| **Orders** | Order list and per-order detail (status, payment, fulfilment, activation) | Support, finance |
| **Distribution log** | Audit trail of eSIM provisioning and delivery | Ops |
| **Members** | Manage your team's marketplace accounts | Admin |
| **Storefront** | Storefront configuration tied to your `partnerCode` | Admin |
| **Webview Insights** | Funnel and revenue from the embedded Shop — see below | Growth, analytics |

Top bar shows your current **Balance** and currency. Top-ups are arranged with Bluecom ops.

## Webview Insights — the integration view

Built specifically for partners running the embedded Shop. The page exposes the funnel from your traffic, not Bluecom's overall traffic.

**Funnel stages:**

1. **Phiên truy cập** — Sessions opened (handshake succeeded).
2. **Ý định mua** — Purchase intent (`shop.purchase_intent` event).
3. **Đơn đã thanh toán** — Paid orders.
4. **Đã kích hoạt** — Activated eSIMs.

**Derived rates:** intent rate, conversion rate, activation rate.

**Revenue panel:** total orders and revenue broken down by currency.

**Traffic chart:** sessions over time, comparable to the period selector.

The same `partnerCode` powers the Shop handshake and the Webview Insights filter — so what you see is exactly what your users did.

## Day-2 self-serve

- Invite a teammate → **Members** → Invite.
- Switch language (UI is `vi` / `en`) → top-right user menu.
- Export an order list → **Orders** → filter → Export (CSV).
- Check whether a specific user reached payment → **Customers** → search → order history.

For anything not exposed in the UI, see [Support](support.md).
