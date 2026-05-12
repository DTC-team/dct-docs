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

Bluecom adds languages on partner request. Contact `integrations@bluecom.vn`.
