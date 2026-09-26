# SableOS Platform Manifest

Status: **current composition authority — 2026-09-26**

Pixel 7 / Panther R9 is physically accepted and frozen as the touch-first
reference after the final Sable Hub V1 closure. Active development is now split
between the Pixel reference lane and the keyboard-first/Treble portability lane.

```text
panther       REFERENCE_FROZEN / accepted R9 Hub V1 image
titan2        N0_A16 / Treble portability lane / build target strategy pending
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
  Devices: Titan 2, Titan 2 Elite, Q27 and future Unihertz/MediaTek targets
  Substrate: stock-vendor-compatible AOSP/Treble userspace
  Artifact class: gsi-system-image first, then bounded system/product/system_ext only if proven
  Claim: portable Sable userspace on preserved vendor/kernel/firmware
```

Titan-family builds must not be forced to track the latest Pixel Android release
before vendor/kernel/HAL compatibility is proven. For Titan 2 N0 the first
planned identity is `TITAN2_N0_A16`: Android 16 / SDK 36 / stock-vendor-bound /
GSI-first.

See [`docs/TREBLE_PORTABILITY_STRATEGY.md`](docs/TREBLE_PORTABILITY_STRATEGY.md).

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

Panther R9 uses the qualified target-files/full-image path. Titan-family N0 may
bind a Sable GSI/system artifact to an exact stock kernel/vendor/ODM/firmware
basis. Those are different claims and must not be mislabeled.

Titan 2 N0 is currently moving from placeholder to strategy-bound build-target
work. No public Titan 2 `build-image`, signing or flash path is enabled.

## Repository roles

- `platform_manifest` — exact source/artifact composition.
- `platform_sable` — common semantic/design/portability contracts.
- `vendor_sable` — common product composition.
- `device_sable_<target>` — bounded device adaptation.
- `build` — CI/build/artifact/deployment contracts.
- `treble_restlessos` — planned upstream-tracking RestlessOS fork for common Treble work, tracked by issue #8.
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
