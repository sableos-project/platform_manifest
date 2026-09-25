# SableOS Platform Manifest

Status: **current composition authority — 2026-09-25**

Pixel 7 / Panther R9 is physically accepted and frozen as the touch-first
reference after the final Sable Hub V1 closure. Active development is now the
common keyboard-first/Titan portability line.

```text
panther       REFERENCE_FROZEN / accepted R9 Hub V1 image
titan2        PORTABILITY / N0 active research
titan2-elite  PORTABILITY candidate / independent baseline required
q27           RESEARCH / future candidate
```

Current private integration image authority:

```text
R9_PANTHER_ACCEPTED_SOURCE=edf62e5bb08372a1395841d6cc5d78d3148a7695
R9_PANTHER_TARGET_FILES_SHA256=a0b359613c4f30e9a834fba212e0b044a97d63ed0537c59471c31b99b627d285
R9_PANTHER_HUB_V1_CLOSURE=MERGED_PR_110
R10_KEYBOARD_FIRST_DESIGN_V1=MERGED_PR_108
```

This repository owns exact OS source composition and trusted external-artifact
provenance. It does not own application implementation, device runtime policy or
deployment transport.

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

## Repository roles

- `platform_manifest` — exact source/artifact composition.
- `platform_sable` — common semantic/design/portability contracts.
- `vendor_sable` — common product composition.
- `device_sable_<target>` — bounded device adaptation.
- `build` — CI/build/artifact/deployment contracts.
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
