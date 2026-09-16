# Source and build-input composition model

Status: **normative composition architecture.**

SableOS is assembled from an Android upstream substrate, Sable-owned source repositories, vendor/BSP inputs, and—where intentionally chosen—exact independently qualified application artifacts. The composition layer records what the build consumes; it does not absorb ownership from the repositories/workflows that produced those inputs.

## Layers

1. **Upstream Android substrate** — GrapheneOS/AOSP/LineageOS or another explicitly qualified base.
2. **Sable common source** — shared platform contracts, Sable Start and other source-built common components.
3. **Qualified standalone application inputs** — exact sealed APK/native artifacts whose canonical build graph remains Cargo/Gradle/upstream-owned.
4. **Common product integration** — `vendor_sable` product selection/import rules.
5. **Device adapters** — only target-specific integration that cannot remain common.
6. **External vendor/BSP inputs** — versioned/hash-bound when normal source redistribution is not available.
7. **Build tooling** — host-side assembly/build/reconstruction/evidence tooling.

## Source project identity

For every source project that participates in the OS tree, record the exact project/revision and checkout path through the appropriate manifest/provenance mechanism.

Do not rely on branch names, copied source, host-only symlinks or untracked local manifests for validated/release composition.

## Qualified external application identity

If the image consumes a standalone-qualified APK, record at least:

```text
source repository + commit
upstream/reuse repository + commit where applicable
qualification workflow/run
APK SHA-256
package/application ID + version
permissions/components
native ABI/library inventory
dependency/provenance inventory
product module/import
install partition/path
signing/transformation model
```

The artifact record complements source composition; it does not pretend the APK was rebuilt inside AOSP.

## Product integration principle

A qualified application becomes a SableOS product input only after its exact import/module semantics, product selection and install/image path are proven in the target Android tree.

`android_app_import` is currently a candidate mechanism, not a composition guarantee.

## Device principle

A new device reuses common Sable source and qualified application inputs unless a target-specific difference is technically required. Device repositories are adapters, not complete OS/app forks.

## Current target roles

- `panther`: PRIMARY Android 17 / GrapheneOS-derived product-development reference.
- `bramble`: future legacy-hardware portability/regression target, not a current production-security claim.
- MediaTek/QWERTY targets: future portability/research axis after common boundaries are stable.

## Validation principle

A composition becomes a validated build definition only when the recorded source and external artifact inputs can reconstruct/integrate the intended tree and pass the corresponding build/product/runtime gates.

A successful historical workspace build does not by itself prove the current composition. A standalone APK qualification PASS does not by itself prove product/image integration.