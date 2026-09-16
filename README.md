# SableOS Platform Manifest

Authoritative SableOS operating-system source composition and release-input provenance.

This repository defines which exact upstream and Sable-owned revisions compose an OS build. When SableOS intentionally consumes independently qualified application APKs instead of rebuilding their external Gradle dependency graph inside AOSP, the manifest/release provenance layer must also bind those exact sealed artifact inputs.

It does not own application implementation source, product semantics or host build tooling.

## Current reference target

Google Pixel 7 (`panther`) on the Android 17 / GrapheneOS-derived development line remains the PRIMARY reference target.

Historical reconstruction work was rooted in the GrapheneOS `2026081300` substrate and R5 SableStart migration. New builds must bind their actual current substrate/revisions rather than treating that historical identity as permanently current.

The next R8 Panther integration build is planned on the migrated `ai-g732` trusted builder environment after its storage/source/toolchain transition is sealed.

## Current R8 composition model

R8 separates application qualification from OS integration:

```text
Process A
  independent Rust/Kotlin/upstream app qualification
  -> exact APK/native artifact freeze

Process B
  platform_manifest source identity
  + exact qualified external artifact identities
  + vendor_sable product integration
  + device_sable_panther bounded adapter
  -> trusted Panther image build
```

A release/build record must therefore be able to answer both:

```text
Which exact Git revisions composed the OS source tree?
Which exact externally-qualified artifacts were consumed by that source tree?
```

Do not imply every shipping APK was source-built inside AOSP when the accepted architecture deliberately imported a sealed standalone artifact.

## Repository roles

- `platform_manifest` — exact OS source composition and release-input provenance.
- `packages_apps_SableStart` — Sable Start launcher/shell source.
- `platform_sable` — shared Sable semantic/design/application architecture contracts.
- application repositories/workspaces — standalone source/build/test ownership for Sable applications.
- `vendor_sable` — common product package/integration selection of qualified inputs.
- `device_sable_<target>` — bounded target-specific integration/qualification.
- `build` — source assembly, Android build, reconstruction and evidence tooling.
- `.github` — organization current-state/roadmap/trust/product policy.

## Current development train

```text
R5/R6  historical migration + launcher foundation
R7     Panther product/daily-driver evidence baseline
R8     shared design + native application qualification/integration   ACTIVE
R9+    next coherent application/productivity tranche
```

R8 is no longer design-only, and R9 is no longer the first Calculator milestone.

See [`docs/DEVELOPMENT_MILESTONE_COMPOSITION.md`](docs/DEVELOPMENT_MILESTONE_COMPOSITION.md).

## Source versus external artifact provenance

### Source projects

Revision-pinned manifest data identifies the Android/Sable source projects actually checked out into the build tree.

### Qualified external application inputs

When a product consumes a sealed standalone APK, the corresponding build/release record must bind at least:

```text
application source repository + commit
upstream/reuse source commit where applicable
qualification workflow/run
APK SHA-256
package/application ID + version
permissions/components
native ABI/library inventory
product import/module
install partition/path
signing/transformation behavior
```

The exact storage/representation may evolve, but the provenance cannot be host-private or implicit.

## Bootstrap/reconstruction state

`docs/R5_R3_RECONSTRUCTION_PLAN.md` is preserved as the historical reconstruction plan from the early organization migration. It remains useful until every relevant historical reconstruction claim is closed, but it is not the current R8 roadmap.

The current architecture must not depend on the historical workspace copy of SableStart or on manually copied application APKs.

## Revision policy

- development refs may move, but every validation run resolves them to exact commits;
- validated/release source composition pins exact revisions;
- external qualified artifacts bind exact hashes and source/workflow provenance;
- release definitions are immutable evidence;
- branch names alone are never sufficient provenance.

See:

- [`docs/SOURCE_COMPOSITION_MODEL.md`](docs/SOURCE_COMPOSITION_MODEL.md)
- [`docs/MANIFEST_HIERARCHY.md`](docs/MANIFEST_HIERARCHY.md)
- [`docs/RELEASE_MANIFEST_POLICY.md`](docs/RELEASE_MANIFEST_POLICY.md)
- [`docs/DEVELOPMENT_MILESTONE_COMPOSITION.md`](docs/DEVELOPMENT_MILESTONE_COMPOSITION.md)
- [`docs/R5_R3_RECONSTRUCTION_PLAN.md`](docs/R5_R3_RECONSTRUCTION_PLAN.md)

The manifest/provenance layer encodes decided architecture. It must not become the place where application ownership or product behavior is accidentally invented.