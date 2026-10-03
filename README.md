# SableOS Platform Manifest

Status: **current composition authority — 2026-10-02**

Pixel 7 / Panther R9 is physically accepted and frozen as the touch-first
reference after the final Sable Hub V1 closure. Active development is now split
between the Pixel reference lane and the keyboard-first/Treble portability lane.

```text
panther       REFERENCE_FROZEN / accepted R9 Hub V1 image
titan2        N1D/C3B E3 active build engineering / public build+flash still fail-closed
titan2-elite  PORTABILITY candidate / independent baseline required
q27           RESEARCH / future candidate
```

Current private integration image authority:

```text
R9_PANTHER_ACCEPTED_SOURCE=edf62e5bb08372a1395841d6cc5d78d3148a7695
R9_PANTHER_TARGET_FILES_SHA256=a0b359613c4f30e9a834fba212e0b044a97d63ed0537c59471c31b99b627d285
R9_PANTHER_HUB_V1_CLOSURE=MERGED_PR_110
R10_KEYBOARD_FIRST_DESIGN_V1=MERGED_PR_108
PUBLIC_BUILD_FOUNDATION=MERGED
PUBLIC_BUILD_SELF_TEST=MERGED
```

This repository owns exact OS source composition and trusted external-artifact
provenance. It does not own application implementation, device runtime policy or
deployment transport.

## Release lanes

SableOS now separates release identity from device-portability reality:

```text
PIXEL_REFERENCE_LANE
  Devices: Pixel / Panther first
  Substrate: latest qualified Sable/Graphene-derived Pixel baseline
  Artifact class: target-files / full-device image
  Claim: strongest Sable reference image

TREBLE_PORTABILITY_LANE
  Devices: Titan 2 first; Titan 2 Elite independently; Q27 future research
  Substrate: Graphene/AOSP-derived Sable userspace plus bounded Treble compatibility
  Artifact class: systemimage/GSI engineering first; later bounded product/system_ext only if proven
  Claim: portable Sable userspace on preserved vendor/kernel/firmware, not production security ownership
```

Titan-family builds must not be forced to track the latest Pixel Android release
before vendor/kernel/HAL compatibility is proven. The current Titan 2 canonical
engineering lane is N1D/C3B on Android 16 / SDK 36, with a Graphene/AOSP base,
minimal Treble scaffold and a fail-closed compatibility-peel process. The full
RestlessOS runtime stack is not the Sable product baseline.

See [`docs/TREBLE_PORTABILITY_STRATEGY.md`](docs/TREBLE_PORTABILITY_STRATEGY.md).

## Titan 2 C3B checkpoint

Current private integration authority is `aimindseye/sableos@26d11bed93ef4eab924fc63100113bd94e8ae88b`.
The first Sable-composed Titan 2 E3 image is being built from
`caf98dde723d07a071d95aaa1ef27d578d3208d8`.

```text
C3B_E1_SYSTEMIMAGE=PASS
C3B_E2_SOURCE_ADMISSION=PASS
C3B_E3_STATUS=BUILD_RUNNING_NOT_YET_SEALED
C3B_RUNTIME_PATCH_ALLOWLIST_COUNT=0
PUBLIC_TITAN_BUILD_IMAGE=NO
PUBLIC_TITAN_FLASH=NO
```

Parallel product work is P1-P4 (Sable Start, Keyboard provisioning,
SetupWizard2 integration preparation, Weather closure) with one batched
ai-g732 qualification after P4. P5 Sable Reader v2 remains design/scope work.

## Composition record

A build record must answer:

```text
which exact source revisions composed the OS?
which exact external application/artifact inputs were consumed?
which device/vendor/firmware basis was used?
which artifact kind was produced?
which exact hashes identify the result?
```

K1 artifact registry v2 means release composition may bind different artifact
classes explicitly:

```text
target-files
full-device-images
gsi-system-image
system-product-bundle
boot-recovery-bundle
```

Panther R9 uses the qualified target-files/full-image path. Titan 2 N1D/C3B may
bind a Sable systemimage/GSI engineering artifact to an exact stock kernel/vendor/ODM/firmware
basis. Those are different claims and must not be mislabeled.

Titan 2 N0 is retained as historical precursor documentation. Current canonical
engineering is N1D/C3B; no public Titan 2 `build-image`, signing or flash path is
enabled until that lane publishes and qualifies a public composition contract.

## Repository roles

- `platform_manifest` — exact source/artifact composition.
- `platform_sable` — common semantic/design/portability contracts.
- `vendor_sable` — common product composition.
- `device_sable_<target>` — bounded device adaptation.
- `build` — CI/build/artifact/deployment contracts.
- `treble_restlessos` — compatibility/reference fork; useful for known-fix discovery, not Sable runtime/product authority.
- application repositories — implementation/tests/dependencies.

## Current product composition note

Sable Hub V1 is the accepted communications surface:

```text
Priority | Messages | Email | People
```

Hub is an aggregator and interaction surface; it is not a claim to own every
provider database/account. Manifest composition must preserve the owning source
application/service boundaries.

## Publication

Reusable source should progressively move into `sableos-project` after
provenance/licensing/privacy review. The private integration repository remains
the release/integration authority during that transition.

Mutable branch names alone are never release provenance.
