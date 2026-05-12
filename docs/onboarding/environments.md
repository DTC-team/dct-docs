# Environments

Bluecom operates two isolated environments. Credentials and data do not cross between them.

| Environment | Hostname | Purpose |
|-------------|----------|---------|
| Staging | `<TBD: staging>` | Integration development, smoke tests, joint sign-off |
| Production | `<TBD: production>` | Live end-user traffic |

## Credentials

Each environment has its own `partnerCode` / `partnerSecret`. The staging secret is issued during onboarding step 2; the production secret is issued at sign-off (onboarding step 5).

## Switching

Use the same code path in both environments and switch via an environment variable:

```bash
BLUECOM_SHOP_HOST=https://<staging-host>
BLUECOM_PARTNER_SECRET=<staging secret>
```

Do not hard-code hostnames or secrets in client bundles. See [Authentication › Security rules](../integration/authentication.md#security-rules).
