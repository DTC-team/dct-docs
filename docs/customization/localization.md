# Localization

## Supported languages

| Code | Language | Default |
|------|----------|---------|
| `vi` | Vietnamese | ✓ |
| `en` | English | |

## Selecting a language

Pass `?locale=vi` or `?locale=en` on the [Shop URL](../integration/embedding.md#entry-url). The URL parameter overrides the user's cookie preference.

## Fallback

If `locale` is omitted, the Shop uses the cookie from a prior session, then falls back to `vi`.

## Adding a language

Bluecom adds languages on partner request. Contact `integration@bluecom.com.vn`.

## Lead times

| Request | Bluecom turnaround |
|---------|---------------------|
| Enable an already-translated language for your `partnerCode` | **1 business day** |
| String tweak in an existing language (copy fix, brand wording) | **2 business days** |
| Add a brand new language (full translation pass + QA) | **10 business days** |
