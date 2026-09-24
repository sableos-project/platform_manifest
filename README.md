# SableOS Platform Manifest

Status: **current composition authority — 2026-09-24**

Pixel 7 / Panther R9 is physically accepted and frozen. Active development is
the common keyboard-first/Titan portability line.

```text
panther       REFERENCE_FROZEN / accepted R9
titan2        PORTABILITY / N0 active research
titan2-elite  PORTABILITY candidate / independent baseline required
q27           RESEARCH / future candidate
```

This repository owns exact OS source composition and trusted external-artifact
provenance. It does not own application implementation, device runtime policy
or deployment transport.

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

## Launcher composition

Current HOME is standalone `org.sableos.launcher` / SableLauncher.
Launcher3QuickStep remains a Recents/task/gesture substrate. Historical
`packages_apps_SableStart` content is not the current HOME product authority.

## Publication

Reusable source should progressively move into `sableos-project` after
provenance/licensing/privacy review. The private integration repository remains
the release/integration authority during that transition.

Mutable branch names alone are never release provenance.
