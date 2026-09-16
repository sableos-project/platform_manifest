# Development milestone source-composition requirements

Status: **normative source/input composition policy for the current development train.**

`platform_manifest` is the authority for the Android/Sable source composition of an OS build. The current R8 architecture additionally permits exact externally qualified application artifacts; those inputs must be bound by explicit release/build provenance rather than hidden as local files.

Historical Git history preserves the earlier detailed R5–R10 composition document.

## 1. Core rule

A complete build claim must be reconstructable from explicit inputs.

Do not depend on:

- manually copied source trees;
- host-only symlinks;
- untracked local manifests;
- uncommitted workspace files;
- branch tips without resolved commits;
- device repositories containing copied common app source;
- opaque APKs copied into the tree without source/workflow/hash provenance.

## 2. Complete input identity

A validated build records as applicable:

```text
platform_manifest commit
upstream/substrate manifest/tag/revisions
Sable source-project commits
target device/product/release/variant
vendor/BSP/generated inputs
qualified external application artifact records
build/toolchain/host identity
resulting artifact hashes
```

For release composition, also record signing/update provenance and device support level.

## 3. R5/R6 historical composition

R5/R6 established the migration/reconstruction and launcher-source principles:

- canonical SableStart source belongs in `packages_apps_SableStart`;
- no manual historical workspace copy is accepted as final composition;
- common launcher source must not be duplicated into a device repository;
- branch identity alone does not close reproducibility;
- manifest path collisions/overrides must be deliberate.

`R5_R3_RECONSTRUCTION_PLAN.md` remains preserved historical reconstruction guidance. Do not treat it as the current R8 roadmap.

## 4. R7 composition baseline

R7 makes product/default application and device build inputs explicit.

For source-built components record repository/path/revision/product owner. For vendor/prebuilt components record their actual provenance/hash rather than inventing a Git identity.

R7 product/build evidence reinforced that module discovery, install rules, product selection, PRODUCT_OUT, target-files/image membership and runtime are different claims.

## 5. R8 composition — ACTIVE

R8 is a consolidated application train:

```text
R8-A shared design/test foundation
R8-B Calculator + Convert
R8-C Games
R8-D Reader publication path
R8-D2 Reader text/accessibility path
R8-E Media
```

### 5.1 Source workstreams

Shared platform/design contracts belong in `platform_sable`.

Substantial application implementation belongs in an application-owned source repository/workspace once the boundary is stable. Do not place complete app implementations in `platform_sable`, `vendor_sable` or `device_sable_panther` merely to avoid creating/choosing the right owner.

### 5.2 Standalone-qualified application inputs

R8 application development may remain Cargo/Gradle/upstream-build owned until product integration.

Before an APK becomes an R8 product input, its freeze record must bind at least:

```text
source repo + commit
upstream/reuse repo + commit where applicable
qualification workflow/run
dependency/toolchain identity
package/application ID + version
APK SHA-256
permissions/exported components
native ABI/library inventory
accepted feature-policy boundary
```

The product build consumes the exact frozen input or explicitly records why/how it transforms it.

### 5.3 Reader inputs

Current initial qualification pins:

```text
vaachak-platform/vaachak-mobile
  5393503ec0695e87e0a9bc4567fec0fea110ea4d

vaachak-platform/vaachak-textreader
  50fca365baae9869264716569830690fb62029a7
```

These are separate provenance sources for one intended Sable Reader product. Do not model them as two required Sable Reader launcher applications merely because qualification occurs independently.

### 5.4 Product integration owner

`vendor_sable` owns common product selection/import of accepted applications. `device_sable_<target>` owns only actual target-specific adaptation.

Generated upstream/vendor product files remain substrate inputs and do not become the owner of Sable package policy.

### 5.5 Import mechanism

The exact Android 17 / GrapheneOS prebuilt application mechanism must be proven in the target tree. `android_app_import` is a candidate, not an assumed manifest/source rule.

The selected mechanism must make product provenance auditable:

```text
sealed APK
 -> Sable product module/import
 -> product selection
 -> PRODUCT_OUT
 -> target-files/image
```

## 6. R8 integration freeze

The manifest/build provenance record for the R8 image identifies the exact selected source projects **and** exact selected standalone application artifacts.

A workstream may be explicitly deferred. The freeze records what is actually included, not what the roadmap once hoped would be included.

Changing a frozen APK/source commit reopens the affected integration evidence.

## 7. Builder/source-root transition

The next R8 Panther image is planned on `ai-g732` after the storage/build migration gate passes.

The source composition must not depend on old ThinkPad absolute paths, manually copied outputs or hidden local-manifest state. The new host should reconstruct/check out from recorded composition plus the recorded external artifact freeze.

## 8. R9+

R9 is the next coherent productivity/application tranche, not the first Calculator milestone. New application/source repositories or artifact inputs follow the same ownership/provenance pattern as R8.

## 9. Release/source model

Development refs may point at active branches, but validation resolves exact commits. Validated/release manifests pin exact revisions and bind any qualified external inputs by exact hash/provenance.

A branch name is never a complete release identity.

## 10. Local manifests

Local manifests are bounded development tools only.

- inspect them during evidence gates;
- prevent accidental path ownership collisions;
- promote required composition into version control before a reconstruction/release claim;
- record temporary local-manifest contents/hashes when they materially affect a validation run.

## 11. Path ownership collisions

Before adding/replacing a project, verify the active upstream composition does not already own the target checkout path. Use deliberate manifest replacement/override semantics, not sync order.

## 12. Device expansion

Future devices reuse common Sable application/platform source and qualified artifacts where technically valid. Device repos are adapters, not app forks.

## 13. Reconstruction gate

A strong reconstruction proves:

1. documented clean/isolated source root;
2. exact intended manifest revision;
3. exact source project revisions;
4. no unexpected local-manifest/path override;
5. exact qualified external artifact inputs available and hash-verified;
6. target/product configuration resolved;
7. build executes under documented network/tool/storage policy;
8. outputs and hashes recorded;
9. runtime/device evidence binds back to the exact resulting image when that claim is in scope.

## 14. Documentation-before-composition

If a new repo, service, application ownership model, default-app replacement or external artifact class is not covered by current architecture, document it before encoding it in the manifest/product tree.

Composition records decided architecture; they must not silently create it.