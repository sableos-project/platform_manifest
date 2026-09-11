# Source composition model

SableOS is assembled from an Android upstream substrate plus Sable-owned repositories. The manifest layer defines composition; it does not absorb source ownership from the repositories it references.

## Layers

1. Upstream Android substrate: GrapheneOS/AOSP/LineageOS or another explicitly qualified base.
2. Sable common product repositories: applications, semantic services, product integration.
3. Device adapter repositories: only target-specific integration that cannot remain common.
4. External vendor/BSP inputs: versioned and hash-bound when redistribution is not permitted.
5. Build tooling: host-side bootstrap, validation, and artifact production.

## Device principle

A new device must reuse common Sable repositories unless a target-specific difference is technically required. Device repositories are adapters, not complete OS forks.

## Initial device roles

- `panther`: primary Android 17 / GrapheneOS product-development reference.
- `bramble`: future legacy-hardware portability experiment, not a current production-security target.
- MediaTek/QWERTY targets: future second portability axis once Panther architecture is stable.

## Validation principle

A manifest becomes a validated build definition only after a clean reconstruction from the manifest produces the expected source identities and passes the corresponding build and runtime gates.
