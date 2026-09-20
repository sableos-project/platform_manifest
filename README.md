# SableOS Platform Manifest

![Local CI](https://img.shields.io/badge/CI-local%20direct-active-2ea44f)
![R9 Launcher](https://img.shields.io/badge/R9%20launcher%20visual-PASS-2ea44f)
![Fresh Panther](https://img.shields.io/badge/fresh%20Panther%20build-IN%20PROGRESS-f0ad4e)
![Pixel 7](https://img.shields.io/badge/Pixel%207%20physical-PENDING-lightgrey)
![Titan 2](https://img.shields.io/badge/Titan%202-keyboard--first%20QUEUED-6f42c1)

## Current R9 release state

The active release train is R9. R8 established the shared application/product-composition foundation; R9 closes the Launcher3/Quickstep + Sable Start HOME architecture, proves a fresh source-bound Panther build, then moves to physical Pixel 7 acceptance before Titan 2 portability work.

Canonical cross-repository status: `sableos-project/.github/docs/CURRENT_RELEASE_STATUS.md`.

GitHub-hosted build CI is not the current release authority. Exact source/artifact provenance is now bound to local direct CI/build evidence from the controlled build machine.

Authoritative SableOS operating-system source composition and release-input provenance.

This repository defines which exact upstream and Sable-owned revisions compose an OS build. When SableOS intentionally consumes independently built application APKs instead of rebuilding their external Gradle dependency graph inside AOSP, the provenance layer must also bind those exact trusted artifact inputs.

It does not own application implementation source, product semantics or host build tooling.

Organization-wide security, quality, test, coverage, supply-chain and performance policy is defined in `sableos-project/.github/docs/SECURITY_QUALITY_ENGINEERING.md`.

## Current reference targets

- Google Pixel 7 (`panther`) — PRIMARY development/runtime reference.
- Titan 2 — keyboard-first N0 GSI portability target after Panther acceptance.
- Titan 2 Elite — second keyboard-first N0 GSI candidate; independent bootloader/recovery/GSI proof required.
- Zinwa Q27 — future integrated/full-QWERTY candidate after shipped-hardware qualification.

The active Panther R9 substrate is the exact signed GrapheneOS `2026081300` Android 17 release with audited Sable deltas. Future validated builds must still bind their exact manifest/source/artifact identities rather than relying on a mutable label.

## Current composition model

```text
R8 application/design foundation + trusted artifact freeze
        |
        v
R9 Launcher3/Quickstep + Sable Start visual closure
        |
        v
fresh source-bound Panther full build
        |
        v
physical Pixel 7 R9 acceptance
        |
        v
Titan 2 keyboard-first portability/GSI qualification
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
- `platform_sable` — shared semantic/design/application/security-quality architecture.
- `vendor_sable` — common imported modules and common app/product selection.
- `device_sable_<target>` — bounded target-specific integration/qualification.
- `build` — trusted application build, Android build, reconstruction and evidence tooling.
- `.github` — organization roadmap/trust/security-quality/product policy.

## Trusted external application provenance

For every A2-built application accepted into a development image record at least:

```text
application source repository + commit
upstream/reuse source commit where applicable
trusted A2 build/toolchain identity
canonical dependency/lock identity
trusted APK SHA-256
package/application ID + version
permissions/AppOps implications
exported components
DEX/JNI inner-content identities
native ABI / 16 KiB compatibility
security/static-analysis summary
coverage provenance where applicable
OWASP MASVS/MASTG evidence/exception references where applicable
SBOM/provenance identity where available
product import/module
install partition/path
Soong signing/transformation behavior
```

The exact metadata storage may evolve, but it cannot remain host-private or implicit.

A source/security check result is not itself an artifact identity. A trusted artifact identity is not itself image/runtime proof.

## Supply-chain and CI provenance

Accepted build definitions should make it possible to reconstruct:

```text
source commit(s)
dependency lock/verification state
accepted upstream revisions
CI/workflow revision
pinned toolchain identities
trusted artifact hashes
manifest/product composition
```

Mutable branch names, caches or unpinned third-party Actions are not sufficient provenance for a trusted transition. The hardened private pipeline requires immutable action/tool references, least-privilege workflow permissions and explicit dependency provenance.

## Dual-target rule

Where compatible, Panther, Titan 2, Titan 2 Elite and later Q27 should consume the same trusted common application artifacts and common `vendor_sable` composition with isolated target OUT_DIRs and bounded device adapters.

A Titan-specific display/keyboard adaptation does not justify a common application source fork.

Panther runtime/performance evidence does not automatically establish Titan 2 runtime/performance behavior.

## Reproducibility rule

Historical successful OUT directories are evidence, not hidden reconstruction inputs.

Repeatability requires fresh source/workspace/output construction from exact canonical Git/tool/dependency identities. Failed historical evidence is preserved rather than rewritten or deleted to make later results appear clean.

## Production signing

Production AVB/OTA/application signing is deliberately deferred until repeatable Panther and Titan 2 development qualification is satisfactory.

The ThinkPad P50 is only a future signing-host candidate after Android building migrates to `ai-g732`. OptiPlex is not part of the current signing plan, and there is no active `sable-signer-01` yet.

Release provenance will later bind production signing/update identity separately from development/test signing.

## Bootstrap/reconstruction state

`docs/R5_R3_RECONSTRUCTION_PLAN.md` remains historical reconstruction evidence and is not the current R8 roadmap. Current architecture must not depend on the historical SableStart workspace copy or manually copied APKs.

## Revision policy

- development refs may move, but every validation run resolves exact commits;
- validated/release source composition pins exact revisions;
- trusted external app artifacts bind exact hashes and source/toolchain/dependency provenance;
- formal release definitions remain immutable evidence;
- branch names alone are never sufficient provenance;
- security/coverage/performance summaries reference the exact source/build identity they describe;
- a planned assurance control is not represented as enforced until evidence exists.

See:

- [`docs/SOURCE_COMPOSITION_MODEL.md`](docs/SOURCE_COMPOSITION_MODEL.md)
- [`docs/MANIFEST_HIERARCHY.md`](docs/MANIFEST_HIERARCHY.md)
- [`docs/RELEASE_MANIFEST_POLICY.md`](docs/RELEASE_MANIFEST_POLICY.md)
- [`docs/DEVELOPMENT_MILESTONE_COMPOSITION.md`](docs/DEVELOPMENT_MILESTONE_COMPOSITION.md)
- [`docs/R5_R3_RECONSTRUCTION_PLAN.md`](docs/R5_R3_RECONSTRUCTION_PLAN.md)

The manifest/provenance layer encodes decided architecture. It must not invent application ownership, security exceptions or product behavior.
