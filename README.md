# SableOS Platform Manifest

## Current composition direction — 2026-09-24

Pixel 7 / Panther R9 is physically accepted and frozen as the touch-first
reference. Active development moves to keyboard-first portability while keeping
one common Sable product core.

```text
panther       REFERENCE_FROZEN
titan2        PORTABILITY / N0 ACTIVE
titan2-elite  PORTABILITY CANDIDATE / N0 PENDING
q27           RESEARCH / FUTURE PRODUCT CANDIDATE
```

This repository owns exact OS source composition and trusted external-artifact
provenance. It does not own application implementation or device-specific
runtime policy.

## Composition rule

A complete build record answers:

```text
which exact source revisions composed the OS?
which exact trusted application artifacts were consumed?
which device/vendor/firmware basis was used?
which artifact kind was produced?
```

For Panther, that artifact may be full target-files/full-device images.

For Titan-family N0 work, the manifest may instead bind a Sable GSI/system image
to an exact stock kernel/vendor/ODM/firmware basis. That distinction must be
explicit; a GSI build is not mislabeled as a full device-owned OS build.

## Repository roles

- `platform_manifest` — exact source/artifact composition.
- `platform_sable` — common semantic/design/portability contracts.
- `vendor_sable` — common product composition.
- `device_sable_<target>` — bounded target adaptation.
- `build` — trusted CI/build/artifact/deployment tooling.
- application repos — implementation source/tests/dependencies.

## Source publication

Reusable source should progressively move into `sableos-project` after
provenance/licensing/privacy review. The private integration repository remains
the release/integration authority during that transition; do not model it as a
permanent monolithic public source tree.

## Device independence

Common Sable application source must not fork merely because a target uses a
different SoC, physical keyboard, display aspect ratio or vendor BSP.

Every device/release build resolves exact revisions. Mutable branch names alone
are not release provenance.
