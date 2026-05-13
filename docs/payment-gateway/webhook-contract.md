# Webhook Contract

!!! warning "Status: Draft"
    The field-level contract below is the **Bluecom-side default**, derived from the NeoPay reference integration. It is the starting point for every new partner; the final shape is negotiated and frozen per provider before sandbox certification.

## Create-payment request (Bluecom → Partner)

`POST {ApiUrl}/<partner-create-payment-path>`

| Field | Type | Notes |
|-------|------|-------|
| `merchantCode` | string | Issued by partner. |
| `orderId` | string | Bluecom order reference. Unique per attempt. |
| `amount` | integer | Minor units (VND has no minor units → integer dong). |
| `currency` | string | ISO 4217. |
| `description` | string | Shown to the user on the hosted page. |
| `returnUrl` | string | Bluecom-owned; must be honoured on success **and** cancel. |
| `ipnUrl` | string | Bluecom-owned IPN endpoint. |
| `expiresAt` | string (ISO 8601) | Optional; partner may enforce its own. |
| `signature` | string | HMAC-SHA256 over the ordered field list, lower-case hex. |

Response (success):

```json
{
  "providerRef": "string",
  "redirectUrl": "https://...",
  "qrPayload": "string|null",
  "expiresAt": "2026-05-13T10:15:00Z"
}
```

Exactly one of `redirectUrl` or `qrPayload` must be present.

## IPN (Partner → Bluecom)

`POST https://api.bluecom.*/api/payment/ipn`

| Field | Type | Notes |
|-------|------|-------|
| `merchantCode` | string | |
| `orderId` | string | Echoes Bluecom's `orderId`. |
| `providerRef` | string | Partner's transaction id. |
| `status` | enum | `SUCCESS` / `FAILED` / `EXPIRED` / `REFUNDED`. |
| `amount` | integer | Must match the create request. |
| `currency` | string | |
| `paidAt` | string (ISO 8601) | Required for `SUCCESS`. |
| `timestamp` | string (ISO 8601) | For replay protection. Rejected if > 5 min skew. |
| `nonce` | string | Optional; used if `timestamp` alone is insufficient. |
| `signature` | string | Same scheme as the create request. |

Bluecom acknowledges with `200 OK` and an empty body as soon as the signature is verified and the IPN is durably persisted to Bluecom's audit store. Order-state transition then happens asynchronously through reliable delivery; partners do not need to wait for it.

## Browser return (Partner → Bluecom)

`GET https://api.bluecom.*/api/payment/result?...signed-fields...`

Same field set as the IPN, transported as a query string. Used **only** to redirect the user back to the Shop UI — never to settle an order.

## Signature scheme

Default:

```
hex(hmac_sha256(secret, join("|", ordered_fields)))
```

Where `ordered_fields` is the lexicographic concatenation of the non-`signature` fields in a documented order. Partners using a different scheme (RSA, different separator, different casing) must publish the exact algorithm; Bluecom will implement against it but will not invent it.
