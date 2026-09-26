# Treble portability strategy

Status: **strategy accepted / implementation gated**

This document records the SableOS strategy for keyboard-first and MediaTek /
Treble devices such as Titan 2, Titan 2 Elite and future Unihertz candidates.

## Decision

SableOS uses two release lanes:

```text
PIXEL_REFERENCE_LANE
  latest qualified Pixel/Sable baseline
  strongest Sable image and UX reference
  target-files/full-device-image artifact classes

TREBLE_PORTABILITY_LANE
  stock-vendor-compatible Treble userspace
  preserved vendor/kernel/firmware basis
  gsi-system-image first for N0
  no Pixel-equivalent security claim until proven
```

Titan-family devices should not be forced onto the latest Pixel Android release
before vendor, VNDK, HAL, kernel and firmware compatibility are proven. Vendor
lag is treated as part of the product architecture, not as an exceptional case.

## Titan 2 N0 identity

The first Titan 2 build target is:

```text
DEVICE=titan2
MILESTONE=N0
IDENTITY=TITAN2_N0_A16
ANDROID_RELEASE=16
PLATFORM_SDK=36
ARTIFACT_KIND=gsi-system-image
PRIMARY_ARTIFACT=system.img
STOCK_VENDOR_KERNEL_FIRMWARE=PRESERVED
FLASH_PUBLIC=NO
E3_DEPLOYMENT=BLOCKED_UNTIL_ARTIFACT_PREFLIGHT
```

## RestlessOS role

RestlessOS is a reference and future fork source, not the first Titan 2 N0
substrate.

```text
FIRST_TITAN2_N0_SUBSTRATE=AOSP16_CLEAN_GSI
RESTLESSOS_ROLE=REFERENCE_AND_FUTURE_FORK
RESTLESSOS_FIRST_BOOT_DEPENDENCY=NO
RESTLESSOS_COMPARISON_PHASE=AFTER_AOSP16_SYSTEM_IMG_EXISTS
```

Reasoning:

- A clean AOSP16 GSI isolates the first variable: whether stock Titan 2 vendor,
  kernel and firmware accept a system-only Sable userspace candidate.
- RestlessOS adds useful Treble compatibility work, but also adds additional
  policy, compatibility and hardening toggles that should not be introduced
  before the first stock-vendor compatibility baseline is understood.
- No GrapheneOS or RestlessOS branding, endorsement, security posture or release
  claim is inherited by SableOS.

## Planned RestlessOS fork

Create exactly one public upstream-tracking fork/mirror:

```text
REPOSITORY=sableos-project/treble_restlessos
UPSTREAM=cawilliamson/treble_restlessos
TRACKING_ISSUE=sableos-project/platform_manifest#8
```

Do not create per-device RestlessOS forks.

Branch model:

```text
upstream/android-16.2
upstream/android-17.0
sable/android-16.2
sable/android-17.0
sable/titan2-n0-a16
```

Rules:

- `upstream/*` branches are fast-forward mirrors only.
- `sable/android-*` branches contain reviewed common Sable Treble changes.
- `sable/titan2-*` branches are temporary device experiment branches.
- `platform_manifest` pins exact commits; mutable branch names are not release
  provenance.
- Prebuilt RestlessOS images are not Sable release artifacts.
- All downstream deltas require reason, risk and rollback notes.

## Substrate fallback order

```text
1. AOSP android-16.0.0_r4 / gsi_arm64-userdebug
2. Another qualified AOSP Android 16 GSI/release branch if r4 does not qualify
3. RestlessOS android-16.2 only after the clean AOSP16 baseline is understood
4. Android 17 Treble lane only after Titan 2 stock firmware/vendor basis supports it
```

## Artifact policy

Titan-family N0 can only advance after a build record answers:

```text
which exact source revisions composed the OS?
which exact stock firmware/vendor basis was used?
which artifact class was produced?
which output hashes identify the artifact?
which deployment gate remains closed or open?
```

Successful build does not authorize flash. E3 deployment remains blocked until
artifact preflight covers sparse/logical size, AVB handling, restore path and
userdata-wipe policy.
