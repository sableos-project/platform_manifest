# SableOS Platform Manifest

Authoritative SableOS operating-system source composition and release-input provenance.

This repository defines which exact upstream and Sable-owned revisions compose an OS build. When SableOS intentionally consumes independently built application APKs instead of rebuilding their external Gradle dependency graph inside AOSP, the provenance layer must also bind those exact trusted artifact inputs.

It does not own application implementation source, product semantics or host build tooling.

## Current reference targets

- Google Pixel 7 (`panther`) — PRIMARY development/runtime reference.
- Titan 2 — active R8 PORTABILITY target after Panther acceptance.

New validated builds must bind their actual current substrate/revisions; historical GrapheneOS `2026081300` and R5 migration identities remain evidence, not permanent current defaults.

## Current R8 composition model

```text
A1 disposable application qualification
        |
        v
A2 trusted standalone app build on ai-g732
        |
        v
exact trusted application freeze
        |
        v
B1 Android/Soong product integration
        |
        v
B2 Panther development image/runtime
        |
        v
B3 Titan 2 portability image/runtime
```

A complete build record must answer both:

```text
Which exact Git revisions composed the OS source tree?
Which exact trusted external application artifacts were consumed?
```

Do not imply every shipping APK was source-built inside AOSP when the architecture deliberately imports a sealed standalone artifact.

## Repository roles

- `platform_manifest` — exact OS source composition and release-input provenance.
- application repositories/workspaces — application source/build/test ownership.
- `platform_sable` — shared semantic/design/application architecture.
- `vendor_sable` — common imported modules and common app/product selection.
- `device_sable_<target>` — bounded target-specific integration/qualification.
- `build` — trusted application build, Android build, reconstruction and evidence tooling.
- `.github` — organization roadmap/trust/product policy.

## Current development train

```text
R5/R6  historical migration + launcher foundation
R7     Panther product/daily-driver evidence baseline
R8     A1/A2 application qualification + B1/B2/B3 dual-target integration
R9+    next coherent application/productivity tranche
```

## Trusted external application provenance

For every A2-built application accepted into a development image record at least:

```text
application source repository + commit
upstream/reuse source commit where applicable
trusted A2 build/toolchain identity
trusted APK SHA-256
package/application ID + version
permissions/components
DEX/JNI inner-content identities
native ABI / 16 KiB compatibility
product import/module
install partition/path
Soong signing/transformation behavior
```

The exact metadata storage may evolve, but it cannot remain host-private or implicit.

## Dual-target rule

Where compatible, Panther and Titan 2 should consume the same trusted common application artifacts and common `vendor_sable` composition with isolated target OUT_DIRs and bounded device adapters.

A Titan-specific display/keyboard adaptation does not justify a common application source fork.

## Production signing

Production AVB/OTA/application signing is deliberately deferred until Panther and Titan 2 development qualification is satisfactory.

The ThinkPad P50 is only a future signing-host candidate after Android building migrates to `ai-g732`. OptiPlex is not part of the current signing plan, and there is no active `sable-signer-01` yet.

Release provenance will later bind production signing/update identity separately from development/test signing.

## Bootstrap/reconstruction state

`docs/R5_R3_RECONSTRUCTION_PLAN.md` remains historical reconstruction evidence and is not the current R8 roadmap. Current architecture must not depend on the historical SableStart workspace copy or manually copied APKs.

## Revision policy

- development refs may move, but every validation run resolves exact commits;
- validated/release source composition pins exact revisions;
- trusted external app artifacts bind exact hashes and source/toolchain provenance;
- formal release definitions remain immutable evidence;
- branch names alone are never sufficient provenance.

See:

- [`docs/SOURCE_COMPOSITION_MODEL.md`](docs/SOURCE_COMPOSITION_MODEL.md)
- [`docs/MANIFEST_HIERARCHY.md`](docs/MANIFEST_HIERARCHY.md)
- [`docs/RELEASE_MANIFEST_POLICY.md`](docs/RELEASE_MANIFEST_POLICY.md)
- [`docs/DEVELOPMENT_MILESTONE_COMPOSITION.md`](docs/DEVELOPMENT_MILESTONE_COMPOSITION.md)
- [`docs/R5_R3_RECONSTRUCTION_PLAN.md`](docs/R5_R3_RECONSTRUCTION_PLAN.md)

The manifest/provenance layer encodes decided architecture. It must not invent application ownership or product behavior.
