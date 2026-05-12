# Onboarding

End-to-end, getting a new partner from "signed agreement" to "staging-ready" takes **~5 business days**.

## The path

1. **[Request access](request-access.md)** — submit the onboarding template.
2. Bluecom issues your `partnerCode` and `partnerSecret`.
3. Bluecom provisions your partner record and adds your domain to the iframe CSP allowlist.
4. You implement the [Authentication](../integration/authentication.md) handshake and [Embedding](../integration/embedding.md) entry.
5. Joint smoke test on **staging** → sign-off → switch to **production**.

The detailed [Checklist](checklist.md) tracks owners and lead times for each step. [Environments](environments.md) lists the staging vs production hostnames.
