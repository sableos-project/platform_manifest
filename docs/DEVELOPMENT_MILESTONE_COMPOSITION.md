# Development milestone source-composition requirements

> **Current execution overlay — 2026-09-20:** R9 is the active milestone. The current Panther source substrate is GrapheneOS 2026081300 / Android 17 plus audited Sable deltas. R8 established the sealed first-party app/product foundation; R9 adds Launcher3/Quickstep-hosted Sable Start and requires fresh source-bound Panther output before physical acceptance.


Status: **normative source/input composition policy for the current development train.**

`platform_manifest` is the authority for Android/Sable source composition. R8 additionally permits trusted externally built application artifacts; those inputs must be bound by explicit provenance rather than hidden as local files.

Historical Git history preserves earlier R5–R10 composition detail.

## 1. Core rule

A complete build claim must be reconstructable from explicit inputs.

Do not depend on manually copied source trees, host-only symlinks, untracked local manifests, uncommitted workspace files, unresolved branch tips, device repos containing copied common app source, or opaque APKs without source/toolchain/hash provenance.

## 2. Complete input identity

A validated development build records as applicable:

```text
platform_manifest commit
upstream/substrate revisions
Sable source-project commits
target device/product/release/variant
vendor/BSP/generated inputs
trusted external application artifact records
build/toolchain/host identity
isolated target OUT_DIR identity
resulting artifact hashes
```

Formal release composition later adds production signing/update provenance and support level.

## 3. R5/R6 historical composition

R5/R6 established canonical SableStart ownership, no manual historical-workspace dependency, no common-launcher duplication into device repos, exact revision requirements and deliberate manifest path ownership.

`R5_R3_RECONSTRUCTION_PLAN.md` remains historical guidance, not the current R8 roadmap.

## 4. R7 composition baseline

R7 makes default-app/device build inputs explicit and reinforced that module discovery, install rules, product selection, PRODUCT_OUT, target-files/image membership and runtime are different claims.

## 5. R8 composition — ACTIVE

```text
R8-A shared design/test foundation
R8-B Calculator + Convert
R8-C Games
R8-D Reader publication path
R8-D2 Reader text/accessibility path
R8-E Media
```

### 5.1 A1 qualification

R8 application development may remain Cargo/Gradle/upstream-build owned. A1 qualification records source/upstream pins, workflow/dependency state, package/manifest state and qualification artifacts but does not by itself define the trusted product input.

### 5.2 A2 trusted external application input

Before an APK becomes an R8 product input, `ai-g732` produces the trusted standalone artifact from exact accepted source.

Its freeze record binds at least:

```text
source repo + exact commit
upstream/reuse repo + exact commit where applicable
trusted A2 build/toolchain identity
package/application ID + version
trusted APK SHA-256
permissions/exported components
classes*.dex identity
JNI .so identity
native ABI / 16 KiB compatibility
dependency/provenance inventory
accepted feature-policy boundary
```

The product build consumes this exact trusted input or explicitly records the intentional transformation.

### 5.3 Reader inputs

Current initial qualification pins:

```text
vaachak-platform/vaachak-mobile
  5393503ec0695e87e0a9bc4567fec0fea110ea4d

vaachak-platform/vaachak-textreader
  50fca365baae9869264716569830690fb62029a7
```

These are provenance sources for one intended Sable Reader product, not two required launcher apps.

### 5.4 Product integration owner

`vendor_sable` owns common imported-module definitions and common product selection of accepted applications. `device_sable_<target>` owns only actual target-specific adaptation.

Generated upstream/vendor product files remain substrate inputs and do not become the owner of Sable package policy.

### 5.5 B1 import mechanism

The exact Android 17 / GrapheneOS prebuilt mechanism must be proven in the target tree. `android_app_import` is preferred but not assumed.

The selected mechanism must make provenance auditable:

```text
trusted frozen APK
 -> Sable module/import
 -> certificate/signing transformation
 -> JNI/dexpreopt/uses-library behavior
 -> product selection
 -> PRODUCT_OUT
 -> later target-files/image/runtime
```

## 6. R8 integration freeze

The R8 build provenance record identifies exact selected source projects and exact A2 trusted application artifacts.

A workstream may be explicitly deferred. Changing a frozen artifact/source commit reopens affected downstream integration evidence.

## 7. Panther and Titan 2 composition

Panther is the primary R8 development/runtime target. Titan 2 is the second R8 PORTABILITY target.

Where technically compatible both should consume:

```text
same trusted common R8 application artifacts
same common vendor_sable product composition
separate target-specific adapter source
separate target OUT_DIR / build evidence
```

A Titan-specific keyboard/layout/BSP adapter does not justify a common application fork.

## 8. Builder/source-root transition

A2/B1/B2/B3 are planned on `ai-g732` after storage/build migration passes.

Composition must not depend on old ThinkPad absolute paths, manually copied outputs or hidden local-manifest state. The trusted builder should reconstruct/check out from recorded source composition plus the recorded trusted external artifact freeze.

## 9. Production signing — deferred

Production signing is not part of R8 development composition closure.

Production app keys, AVB, OTA signing, `sign_target_files_apks`, key custody and signed-output provenance are defined later only after Panther and Titan 2 development qualification is satisfactory.

The ThinkPad P50 is only a future signing-host candidate. OptiPlex is not part of the current signing plan and no active `sable-signer-01` exists.

## 10. R9+

R9 is the next coherent productivity/application tranche, not first Calculator. New application/source repositories or trusted external artifacts follow the same ownership/provenance pattern.

## 11. Local manifests/path ownership

Local manifests remain bounded development tools. Inspect them, prevent collisions, promote required composition into version control before reconstruction/release claims and never rely on sync order for path ownership.

## 12. Reconstruction gate

A strong reconstruction proves:

1. documented clean/isolated source root;
2. exact intended manifest/source revisions;
3. no unexpected local-manifest/path override;
4. exact trusted external app inputs available/hash-verified;
5. target/product configuration resolved;
6. build executes under documented network/tool/storage policy;
7. outputs/hashes recorded;
8. runtime evidence binds back to the exact image when in scope.

## 13. Documentation-before-composition

If a new repo, service, app ownership model, default-app replacement, device adapter or external artifact class is not covered by current architecture, document it before encoding it into the manifest/product tree.

Composition records decided architecture; it must not silently create it.
