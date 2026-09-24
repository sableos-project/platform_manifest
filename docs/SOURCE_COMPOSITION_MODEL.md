# SableOS source composition model

Status: **current normative model — 2026-09-24**

SableOS is assembled from an Android substrate, Sable-owned source repositories,
vendor/BSP inputs and—where deliberately chosen—exact independently qualified
application/artifact inputs.

## Composition classes

1. **Android substrate** — AOSP/GrapheneOS/LineageOS or another qualified base.
2. **Sable-owned source** — common product/platform/apps plus bounded device adapters.
3. **Vendor/BSP inputs** — device kernel/vendor/ODM/firmware dependencies.
4. **Qualified external artifacts** — exact sealed APK/native/image inputs.

The composition layer records inputs; it does not absorb ownership from the
repositories/workflows that produced them.

## Current product roles

```text
panther       REFERENCE_FROZEN / Android 17 accepted reference
titan2        PORTABILITY / N0 active research
titan2-elite  PORTABILITY candidate / independent proof
q27           RESEARCH
bramble       historical reference
```

No current PRIMARY device is declared.

## Current HOME boundary

`org.sableos.launcher` / SableLauncher owns HOME.
Launcher3QuickStep owns Recents/Overview/task/gesture substrate only.
Historical SableStart composition is not the current product HOME model.

## Artifact composition

K1 registry v2 separates artifact identity from device-contact identity.
Artifact records can represent target-files, full images, GSI/system images,
system/product bundles or boot/recovery bundles.

A physical serial is not source/artifact composition.

## Validation

A composition is validated only when recorded source and artifact inputs can
produce/integrate the intended tree and pass the relevant build/product/runtime
gates.

A successful historical workspace build, standalone APK qualification or generic
GSI boot is never sufficient by itself to claim current product qualification.
