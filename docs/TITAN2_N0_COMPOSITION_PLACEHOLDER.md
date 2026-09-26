# Titan 2 N0 composition placeholder

Status: **placeholder only — 2026-09-26**

This document creates the public composition placeholder for the first bounded
Titan 2 SableOS N0 experiment. It does not enable a public build, signing flow,
flash flow or production reproducibility claim.

```text
DEVICE=titan2
RELEASE=N0
COMPOSITION_STATUS=PLACEHOLDER_ONLY
PUBLIC_DEVICE_REPO=sableos-project/device_sable_titan2
PUBLIC_DEVICE_REPO_STATUS=ABSENT
PRIVATE_INTEGRATION_SKELETON=EXPECTED
BUILD_IMAGE_PUBLIC=NO
SIGNING_PUBLIC=NO
FLASH_PUBLIC=NO
FIRST_SABLE_ARTIFACT=ABSENT
FIRST_SABLE_BOOT=NOT_RUN
```

## Exact stock basis to bind before artifact work

The first N0 experiment must bind the Sable artifact to an exact stock firmware,
vendor, ODM and firmware basis. Public docs must use normalized facts and hashes;
raw firmware, partition images, serials, IMEI/MEID/ICCID, calibration data and
signed OTA query strings must remain outside public source.

Current Titan 2 research facts available from the device research repository:

```text
DEVICE_FAMILY=Titan 2
RETAIL_VARIANT=US retail handset
FASTBOOT_PRODUCT=g71v78c2k_dfl_tee
STOCK_BASELINE=Android 16 V01.00.13
SOC_FAMILY=MediaTek MT6878
USERSpace_ABI=arm64-only
TREBLE=YES
VENDOR_API=34
VNDK=34
KERNEL=Linux 6.1.145 / Android 14-derived branch
DYNAMIC_PARTITIONS=YES
VIRTUAL_AB=YES
SUPER_BYTES=9663676416
FASTBOOTD=YES
FASTBOOT_BOOT=NO
DSU=NO_ON_TESTED_STOCK_BUILD
RECOVERY_PATH=vendor_boot recovery vendor ramdisk
AVB_UNLOCKED_STATE=orange after unlock
```

This placeholder must not be converted into a release manifest until the exact
public/private source revisions, proprietary inputs and artifact hashes are
known.

## Artifact candidates

The first Titan 2 N0 artifact type remains an experimental decision.

```text
gsi-system-image
  Candidate when the stock vendor/odm/kernel stack can boot a Sable system image
  with a bounded AVB and data policy.

generated-super-image
  Candidate when logical partition sizing or dynamic partition composition makes
  a single system image insufficient.

bounded system/product/system_ext bundle
  Candidate when Sable userspace requires a bounded product/system_ext payload
  while preserving the stock kernel/vendor/odm basis.
```

Do not choose based only on a community recipe. The decision must be based on
super/LP metadata, free space, AVB handling, restore evidence and whether first
Sable deployment requires a userdata wipe.

## Publication gates

Before this placeholder can become a real public N0 composition record:

```text
PUBLIC_DEVICE_REPO_EXISTS=YES
PRIVATE_DEVICE_SKELETON_EXISTS=YES
TITAN2_N0_ARTIFACT_TYPE_DECIDED=YES
STOCK_FIRMWARE_BASIS_HASHED=YES
PROPRIETARY_INPUT_BOUNDARY_DOCUMENTED=YES
AVB_STRATEGY_DOCUMENTED=YES
USERDATA_POLICY_DOCUMENTED=YES
RESTORE_PLAN_VERIFIED=YES
BUILD_IMAGE_PUBLIC=YES_OR_EXPLICITLY_PRIVATE_ONLY
```

## Fail-closed build boundary

`sableos-project/build` remains authoritative for public command behavior.
Titan-family `build-image` and flash paths must remain fail-closed until this
placeholder is replaced by a qualified composition record and device adapter.

Expected current behavior:

```bash
bash sable.sh titan2 N0 build-image
```

```text
SABLE_BUILD_IMAGE=FAIL_CLOSED
```

## E3/N0 deployment boundary

First E3/N0 deployment may begin only after:

1. a real Titan 2 artifact exists;
2. its artifact kind is recorded;
3. its stock firmware/vendor basis is recorded;
4. restore evidence is reachable;
5. serial-bound commands are used;
6. destructive-data behavior is explicit; and
7. the deployment adapter rejects unsupported artifact kinds.

Until then, Titan 2 N0 remains a composition placeholder, not a build target.
