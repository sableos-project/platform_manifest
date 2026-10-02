# Development milestone composition

Status: **current normative composition policy — 2026-10-02**

## Current baseline

R8/R9 established the accepted Panther reference. Panther is now frozen.
K1/K2 generalized artifact identity and deployment boundaries without enabling
Titan-family mutation.

Current composition direction:

```text
common Sable source + qualified artifacts
        |
        +-- Panther frozen target-files reference
        |
        +-- Titan 2 active N1D/C3B systemimage/GSI engineering composition
        |
        +-- Titan 2 Elite independent future composition
        |
        +-- Q27 research only
```

## Source composition

Every participating project is recorded by exact revision and checkout path.
Do not depend on copied source trees, host-only symlinks, untracked local
manifests, uncommitted workspace changes or unresolved branch tips.

The Android substrate may differ by device, but common Sable application and
semantic source does not fork merely because the SoC, display or keyboard
changes.

## External artifact composition

When product integration consumes independently qualified APK/native artifacts,
the composition record binds at least:

- owning source repository and exact commit;
- upstream revision where applicable;
- trusted builder/toolchain identity;
- artifact package/module identity;
- whole-artifact hash;
- native inner-content hashes where applicable;
- product integration evidence.

## K1 artifact kinds

The composition layer recognizes explicit artifact classes rather than assuming
every target produces Panther-style target-files.

```text
target-files
full-device-images
gsi-system-image
system-product-bundle
boot-recovery-bundle
```

A Titan N1D/C3B systemimage/GSI record also binds the exact stock/vendor basis it expects.

## Device composition

### Panther

REFERENCE_FROZEN. The accepted R9 image source/artifact remains historical
release evidence. Later docs/tooling commits do not become new Panther image
sources automatically.

### Titan 2

N1D/C3B active engineering integration. Preserve the qualified stock
kernel/vendor/ODM/firmware boundary while the Graphene/AOSP-derived Sable
userspace and minimal Treble compatibility peel are built and qualified.
RestlessOS remains a compatibility reference, not the product runtime baseline.

### Titan 2 Elite

Independent PORTABILITY candidate. Do not inherit Titan 2 stock, AVB, partition,
input, display, camera or telephony claims.

### Q27

RESEARCH only until shipped-hardware evidence supports promotion.

## Launcher composition

Launcher3/Launcher3QuickStep is the canonical Sable first-party HOME runtime,
Recents/Overview/task/gesture substrate and host for Sable Start
presentation/state source.

Standalone SableLauncher is retired from the current product architecture.

```text
THIRD_PARTY_HOME_SELECTION_ALLOWED=YES
FORCE_SABLE_HOME_AFTER_USER_SELECTION=NO
```

## Release closure

A composition becomes a validated build definition only when exact source and
artifact inputs are bound and the corresponding build/product/runtime gates
pass. A successful historical workspace build is evidence, not a hidden input.
