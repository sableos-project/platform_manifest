# R5-R3 — Panther clean manifest reconstruction plan

Status: **normative plan; manifest integration and reconstruction execution are not yet closed.**

This document records the R5-R3 audit result and the exact acceptance boundary for moving from the successful R5-R2 direct migrated-checkout build to a normal `repo`-managed reconstruction.

## 1. Current audit result

At the audit baseline, `sableos-project/platform_manifest` `main` resolves to:

```text
5fb58b19cd83693068c63ba670042cfa20f911e2
```

The repository currently contains organization CI configuration, `README.md`, and policy/documentation under `docs/`. It does **not** yet contain the operational manifest hierarchy described by `docs/MANIFEST_HIERARCHY.md`:

```text
default.xml
manifests/common/sable.xml
manifests/devices/panther.xml
releases/panther/<id>.xml
```

Therefore the current repository cannot yet reconstruct the validated Panther source tree and cannot yet place `packages_apps_SableStart` at `packages/apps/SableStart` through normal `repo init` / `repo sync` semantics.

This is an expected bootstrap gap, not an R5-R2 regression.

## 2. Upstream substrate identity

The validated Panther reference substrate is GrapheneOS `2026081300` / Android 17.

The upstream GrapheneOS manifest at tag `2026081300` exists and declares, among other pinned source-composition data:

```text
GrapheneOS manifest tag: refs/tags/2026081300
AOSP default revision:   refs/tags/android-17.0.0_r1
```

R5-R3 must preserve the exact upstream project revisions represented by that upstream release manifest rather than reconstructing an approximation from current branch tips.

The final R5-R3 evidence must record the exact upstream manifest identity actually consumed.

## 3. Sable Start identity that must enter the manifest

Canonical repository:

```text
https://github.com/sableos-project/packages_apps_SableStart.git
```

Canonical Android checkout path:

```text
packages/apps/SableStart
```

Sealed migration revision:

```text
commit 059d5d23e4186bbd3119180433a5e6206b7d95bd
tree   c00fd741c401fdd1421e8971bfb82f01c4b7c7da
```

Validated source invariant:

```text
source_count=12
src/com/sable/start/ui/SableMetroPreviewActivity.kt
SHA256=dde4196f82ea4357cfdef5a78fe0d9824971d93e52ee6886923c6be245f1f249
```

Known-good APK identity from both the prior R3B build and the R5-R2 exact migrated-checkout build:

```text
1b35cd8a6ee90bfac6108babce160a040c5315dec88e7b0c6ae9c9b968b757ef
```

## 4. Required manifest semantics

The manifest integration must encode a Sable-owned remote and an exact project mapping equivalent in meaning to:

```xml
<remote name="sableos" fetch="https://github.com/sableos-project/" />

<project
    name="packages_apps_SableStart"
    path="packages/apps/SableStart"
    remote="sableos"
    revision="059d5d23e4186bbd3119180433a5e6206b7d95bd" />
```

Exact formatting may follow the final hierarchy, but the repository, path, and revision semantics are fixed for this R5 baseline.

R5-R3 must prove that no other active project or local manifest entry populates the same checkout path.

## 5. Preferred hierarchy

For the first clean Panther reconstruction, use the hierarchy already documented by this repository:

```text
default.xml
manifests/
    upstream/
        grapheneos-2026081300.xml
    common/
        sable.xml
    devices/
        panther.xml
releases/
    panther/
        <validated-id>.xml
```

Recommended intent:

- `manifests/upstream/grapheneos-2026081300.xml` preserves the exact GrapheneOS `2026081300` source-composition manifest used as the substrate;
- `manifests/common/sable.xml` owns common Sable projects, beginning with `packages_apps_SableStart` for R5;
- `manifests/devices/panther.xml` owns only genuinely Panther-specific Sable projects when such projects are required;
- `default.xml` is the active development composition entry point;
- `releases/panther/<validated-id>.xml` becomes the revision-pinned validated composition after the reconstruction gate passes.

A host-private `.repo/local_manifests` overlay may be used only for a bounded experiment and does not close R5-R3. The closure manifest must be version-controlled in this repository.

## 6. R5-R3A — read-only historical-workspace audit

Before mutating manifest composition, capture the current historical workspace's actual `repo` state read-only.

Required observations:

```text
workspace path
.repo/manifest.xml target/link identity
manifest repository URL + branch/tag + commit
repo manifest -r output hash
presence and contents/hashes of .repo/local_manifests/*
project(s) resolving to packages/apps/SableStart, if any
whether an upstream project already owns packages/apps/SableStart
current GrapheneOS/substrate manifest identity
```

This audit must not edit source, sync, reset projects, clean outputs, contact a device, or change Git history.

R5-R3A result vocabulary:

```text
PASS    exact current composition and collision state captured
FAIL    contradictory/unsafe composition discovered
BLOCKED required repo metadata is missing/unreadable
```

## 7. R5-R3B — manifest integration

If R5-R3A confirms the expected GrapheneOS `2026081300` baseline and no checkout-path collision, integrate the operational manifest files through a normal reviewed Git change.

The integration change must prove before merge/use:

- XML parseability;
- exact SableStart project path/revision;
- exact upstream release binding;
- no duplicate active project path for `packages/apps/SableStart`;
- no dependency on a host-private local manifest;
- no unrelated source-composition changes hidden in the same commit.

Manifest integration is a Git/source-composition mutation and is separate from merely auditing the current state.

## 8. R5-R3C — clean reconstruction

Use a new source root separate from the historical Panther workspace. Do not path-swap or copy the historical `packages/apps/SableStart` tree into it.

The reconstruction gate must record explicit authorization for network acquisition and build-output mutation separately.

### Acquisition phase

Network may be enabled only when explicitly authorized for this phase.

Required sequence:

```text
create/use dedicated empty reconstruction root
repo init using sableos-project/platform_manifest at an exact commit
repo sync required source projects
resolve repo manifest -r
record every relevant Sable revision
verify packages/apps/SableStart Git remote + HEAD + tree
verify source count and PreviewActivity SHA-256
verify no local-manifest override/path collision
seal acquisition/source identity
```

A reconstruction cannot be called clean if it silently reuses the historical workspace's manually supplied application directory.

### Build phase

After acquisition is complete, external network creation must be denied according to the reviewed build gate.

Use a fresh isolated output directory rather than cleaning the historical workspace.

Target build configuration remains the validated Panther baseline unless a separately documented change is made:

```text
TARGET_PRODUCT=panther
TARGET_RELEASE=cur
TARGET_BUILD_VARIANT=user
module=SableStart
```

Build evidence must prove the checkout at `packages/apps/SableStart` is the manifest-managed repository/revision recorded above.

## 9. Artifact acceptance

Required package checks:

```text
module build result = success
APK is a valid ZIP/APK
AndroidManifest.xml present
classes.dex / expected dex inventory present
package = org.sableos.start
versionCode = 38
versionName = 17
targetSdkVersion = 37
```

Strongest expected result:

```text
APK_SHA256=1b35cd8a6ee90bfac6108babce160a040c5315dec88e7b0c6ae9c9b968b757ef
```

If the hash differs, R5-R3 does not automatically fail, but the difference must be explained by exact source/tool/config provenance before any equivalence claim is made. A differing unexplained hash is `UNKNOWN`, not `PASS` for artifact equivalence.

## 10. Post-build integrity

Record:

- manifest-managed SableStart worktree clean state;
- exact SableStart HEAD/tree unchanged;
- source hash invariant unchanged;
- reconstruction manifest/repositories not mutated by the build;
- historical workspace untouched;
- no clean/clobber/delete unless separately authorized.

## 11. Evidence bundle

Suggested evidence directory:

```text
/tmp/SABLESTART_R5_R3_RECONSTRUCTION_<timestamp>
```

At minimum preserve:

```text
gate_report.txt
platform_manifest_identity.txt
upstream_manifest_identity.txt
resolved_manifest.xml
local_manifest_inventory.txt
project_path_inventory.txt
sablestart_source_identity.txt
build_environment.txt
build.log
apk_inventory.txt
SHA256SUMS.txt
```

Hash the evidence inventory itself and record the final seal.

## 12. Closure statement

Only after all required R5-R3 phases pass may the project claim:

```text
SABLESTART_R5_R3_MANIFEST_RECONSTRUCTION=PASS
```

The bounded meaning is:

> A new Panther source root, reconstructed from the version-controlled SableOS manifest composition and exact upstream/Sable revisions, supplied the canonical SableStart repository at `packages/apps/SableStart` and successfully built the expected SableStart artifact without historical-workspace source substitution.

This still does not by itself prove a complete signed production OS release, HOME-role adoption, or new R6 behavior.

## 13. Next boundary after R5-R3

After clean reconstruction closes:

1. record the accepted/merged reachable SableStart source identity;
2. close the migration/source-integration decision for PR #1;
3. record the validated Panther manifest identity;
4. treat the organization repositories as the canonical starting point for R6;
5. convert the proven reconstruction/build procedure into the trusted `sable-builder-01` C2/C3 CI gates rather than inventing a different CI build path.
