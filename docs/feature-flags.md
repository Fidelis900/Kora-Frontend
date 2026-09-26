# Feature Flags

Kora uses environment-backed feature flags to control optional application features. Flags are defined in [`lib/featureFlags.ts`](../lib/featureFlags.ts) and can be configured locally through `.env.local`.

---

## Flag Reference

| Flag | Environment variable | Default | Purpose |
| :--- | :--- | :---: | :--- |
| `mock-data` | `NEXT_PUBLIC_ENABLE_MOCK_DATA` | `false` | Use static mock invoice data instead of live Soroban/indexer data. |
| `devtools` | `NEXT_PUBLIC_ENABLE_DEVTOOLS` | `false` | Show React Query developer tools. |
| `comparison` | `NEXT_PUBLIC_ENABLE_COMPARISON` | `false` | Enable the invoice comparison bar in the marketplace. |
| `onboarding-tour` | `NEXT_PUBLIC_ENABLE_ONBOARDING_TOUR` | `true` | Enable the guided onboarding tour for new users. |
| `batch-actions` | `NEXT_PUBLIC_ENABLE_BATCH_ACTIONS` | `false` | Enable batch cancel/repay actions in the SME dashboard. |
| `kyb-mint-gate` | `NEXT_PUBLIC_ENABLE_KYB_MINT_GATE` | `false` | Require KYB/KYC business verification before reaching the invoice minting step. |
| `secondary-market` | `NEXT_PUBLIC_ENABLE_SECONDARY_MARKET` | `false` | Enable the secondary-market P2P trading route. |
| `category-taxonomy-preview` | `NEXT_PUBLIC_ENABLE_CATEGORY_TAXONOMY_PREVIEW` | `false` | Enable the category taxonomy preview feature. |

---

## Local Configuration

Feature flags are configured through environment variables. Create or update `.env.local` in the repository root.

For boolean flags, set the environment variable to the string `"true"` to enable it:

```dotenv
NEXT_PUBLIC_ENABLE_COMPARISON=true
NEXT_PUBLIC_ENABLE_BATCH_ACTIONS=true
```

> **Note:** For most flags, any value other than `"true"` leaves the flag disabled.

### Exceptions
The onboarding tour is an exception: it is enabled unless `NEXT_PUBLIC_ENABLE_ONBOARDING_TOUR` is explicitly set to `"false"`. For example:

```dotenv
NEXT_PUBLIC_ENABLE_ONBOARDING_TOUR=false
```

disables the onboarding tour.

---

## Runtime Overrides

In development, feature flags can also be overridden at runtime through the feature-flag override system in `lib/featureFlags.ts`.

* Runtime overrides are stored in browser `localStorage` and take precedence over environment values.
* Runtime overrides are **not** available in production.

---

## Source of Truth

The complete list of supported flags is defined by `FLAG_ENV_MAP` in `lib/featureFlags.ts`. When adding a new feature flag, make sure to update both that mapping and this documentation.
