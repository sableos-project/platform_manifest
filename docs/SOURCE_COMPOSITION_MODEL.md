# SableOS source composition model

Status: **current normative model — 2026-10-02**

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
titan2        N1D/C3B active engineering integration
titan2-elite  PORTABILITY candidate / independent proof
q27           RESEARCH
bramble       historical reference
```

No current PRIMARY device is declared.

## Current HOME boundary

Launcher3/Launcher3QuickStep is the canonical **Sable first-party HOME runtime**
and Recents/Overview/task/gesture substrate. It hosts Sable Start
presentation/state source.

Standalone `org.sableos.launcher` / SableLauncher is retired from the current
product architecture.

```text
THIRD_PARTY_HOME_SELECTION_ALLOWED=YES
FORCE_SABLE_HOME_AFTER_USER_SELECTION=NO
```

Manifest composition records Sable first-party defaults; it must not reinterpret
a user's later Android HOME selection as a composition change.

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
