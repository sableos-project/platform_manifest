# Development milestone composition

Status: **current normative composition policy — 2026-09-24**

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
        +-- Titan 2 future N0 GSI/system composition
        |
        +-- Titan 2 Elite independent N0 composition
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

A Titan N0 GSI record also binds the exact stock/vendor basis it expects.

## Device composition

### Panther

REFERENCE_FROZEN. The accepted R9 image source/artifact remains historical
release evidence. Later docs/tooling commits do not become new Panther image
sources automatically.

### Titan 2

PORTABILITY/N0 active research. Initial Sable work should preserve stock
kernel/vendor/ODM/firmware unless evidence requires otherwise.

### Titan 2 Elite

Independent PORTABILITY candidate. Do not inherit Titan 2 stock, AVB, partition,
input, display, camera or telephony claims.

### Q27

RESEARCH only until shipped-hardware evidence supports promotion.

## Launcher composition

SableLauncher is the current Sable HOME product. Launcher3QuickStep is retained
for Recents/Overview/task/gesture substrate and is not HOME eligible.
SableStart is historical presentation/source context.

## Release closure

A composition becomes a validated build definition only when exact source and
artifact inputs are bound and the corresponding build/product/runtime gates
pass. A successful historical workspace build is evidence, not a hidden input.
