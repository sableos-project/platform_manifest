# Development milestone source-composition requirements

Status: **normative source-composition policy for the R5–R10+ development train.**

`platform_manifest` is the authoritative place to describe which repositories/revisions form a complete SableOS source composition. A milestone is not reproducible merely because the relevant component commit exists somewhere on GitHub.

This document complements `MANIFEST_HIERARCHY.md`, `SOURCE_COMPOSITION_MODEL.md`, and `RELEASE_MANIFEST_POLICY.md`.

## 1. Core rule

A complete build claim must be reconstructable from explicit source-composition data.

Do not depend on:

- manually copied source trees;
- host-only symlinks;
- ad hoc local manifest entries that are not captured in the project composition;
- uncommitted workspace files;
- branch tips that can move without an exact recorded revision;
- device repositories containing copied common application source.

Development may temporarily use a bounded migration mechanism to prove source equivalence, but the migration is not complete until normal manifest composition can reconstruct the intended tree.

## 2. Development milestone labels versus manifests

`R5`, `R6`, `R7`, `R8`, `R9`, and `R10+` are development milestones, not source manifest version numbers.

For a milestone closure, record:

- exact manifest repository commit;
- exact relevant Sable component commits;
- exact upstream/substrate manifest/tag/revision;
- target device/product/release/variant;
- any allowed local manifest fragment, preferably checked into an appropriate project repository rather than remaining host-private;
- vendor/BSP inputs that are not represented as normal Git projects;
- resulting artifact hashes.

A public/semantic SableOS release should use an immutable revision-pinned manifest according to `RELEASE_MANIFEST_POLICY.md`.

## 3. R5 — migration/reconstruction closure

R5 exists to cross the boundary from historically validated local workspace source to canonical organization repositories.

For Sable Start, R5 must establish:

```text
sableos-project/packages_apps_SableStart
  -> exact validated source commit
  -> manifest project at packages/apps/SableStart
  -> successful build from reconstructed checkout
```

Current sealed migration source identity:

```text
commit 059d5d23e4186bbd3119180433a5e6206b7d95bd
tree   c00fd741c401fdd1421e8971bfb82f01c4b7c7da
```

The final manifest must not require the historical authoritative workspace copy to remain present merely to build Sable Start.

### 3.1 R5 manifest requirements

Before R5 reconstruction closure:

- define the canonical manifest project name/path for `packages_apps_SableStart`;
- pin/refer to the accepted commit according to development/release manifest policy;
- ensure no duplicate project also populates `packages/apps/SableStart`;
- ensure no local symlink substitutes a different tree;
- ensure `repo sync`/checkout semantics place the repository at the expected Android path;
- capture exact upstream substrate composition used around it;
- perform a fresh or sufficiently isolated reconstruction build gate that proves the manifest source is actually consumed.

### 3.2 Migration PR timing

A source migration PR may remain open while build/reconstruction is being proven. Do not rewrite a sealed source commit solely to absorb unrelated documentation changes when the merge model can preserve the source identity.

Once accepted, the exact merged/reachable source identity and manifest revision must be recorded.

## 4. R6 — Sable Start functional milestone

R6 modifies `packages_apps_SableStart` after migration closure.

Source-composition requirements:

- R6 feature commits belong in the canonical Sable Start repository, not only the Panther workspace;
- Panther/device repositories must not receive a forked launcher copy;
- exact R6 validation should record Sable Start commit and complete manifest identity;
- if R6 requires no new common platform/vendor/device source, do not create artificial cross-repository changes;
- if a shared Android adapter is genuinely required, place it in the documented owning common repository and pin both changes together for validation.

R6 runtime fixture applications (for example user-installed Maps/Weather) are not necessarily manifest projects/product defaults and must not be added to the product manifest merely because they were used for testing.

## 5. R7 — daily-driver composition

R7 is the point at which default application/product composition becomes explicit.

The manifest/product combination must make it possible to identify the selected source implementation for baseline apps that are source-built as part of SableOS.

For each source-built default app, record:

- repository/project name;
- checkout path;
- exact revision;
- upstream provenance;
- product inclusion owner (`vendor_sable` or appropriate product definition);
- device-specific exception, if any.

For a prebuilt/proprietary/vendor-supplied component, do not invent a Git revision. Record the actual provenance/version/hash through the appropriate vendor/provenance mechanism.

### 5.1 No blanket upstream assumption

Do not model R7 as "AOSP apps" or "Graphene apps" globally unless every relevant component actually follows that rule and the product documentation intentionally chooses it.

Phone, Messaging, Browser, Camera, Files, Clock, Calculator, etc. can have different upstream/ownership decisions.

## 6. R8 — common Sable design/customization source

R8 common design/theme contracts belong in `platform_sable` or another intentionally created common Sable project if the architecture evolves.

Manifest rules:

- one canonical source project for the common contract;
- application repositories consume it through the normal Android build dependency model;
- no per-device copy of shared design source;
- no local host overlay used as the canonical theme source;
- R8 validation pins both the common contract and consuming Sable application revisions.

If Sable customization persistence requires a new common service/package, it needs its own documented source ownership/project path before manifest integration.

## 7. R9 — new Sable application repositories

The first intended native utility is Sable Calculator.

Before adding a new Sable app to the manifest/product:

1. create/identify its canonical repository;
2. document package name and Android checkout path;
3. document build module name;
4. establish license and source ownership;
5. establish the initial source commit;
6. add the manifest project at a non-conflicting path;
7. add product inclusion only after the app's own build gate is ready;
8. pin the exact revision for milestone/release validation.

Suggested naming should remain consistent with existing Android repository conventions, e.g. a future canonical repository may follow a `packages_apps_<Name>` pattern, but the exact repository must be intentionally created rather than assumed by code/scripts before it exists.

Do not store Calculator source in `platform_sable`, `vendor_sable`, or `device_sable_panther` merely to avoid creating the proper repository.

## 8. R10+ — application replacement

Replacing an inherited application affects composition and often product roles/privileges.

A replacement manifest/product change should explicitly model:

```text
old source/package inclusion
new source/package inclusion
role/default-handler transition
permission/allowlist transition
data migration compatibility
rollback revision
```

Do not delete the old source reference and its rollback knowledge before the new application is qualified.

Historical release manifests remain immutable evidence even if the current product no longer uses the component.

## 9. Complete build identity

For milestone evidence, record at least:

```text
platform_manifest commit
upstream/default manifest identity
Sable project commit(s)
target product
release
build variant
OUT_DIR/build configuration where relevant
artifact hashes
```

For formal release composition also record signing/update provenance and device support level.

## 10. Working branches versus exact revisions

A branch name is useful for development, but branch identity alone does not close reproducibility.

Bad closure statement:

```text
built from main
```

Better:

```text
platform_manifest=<sha>
packages_apps_SableStart=<sha>
platform_sable=<sha>
vendor_sable=<sha>
device_sable_panther=<sha>
upstream_manifest/tag=<exact identity>
```

When a build uses a branch, resolve and record its exact commit at build time.

## 11. Local manifests

Local manifests are acceptable as bounded development tools only when their role is explicit.

Rules:

- inspect them during evidence gates;
- do not let an unknown local manifest silently override a canonical project path;
- promote required composition into version-controlled Sable manifest data before claiming clean reconstruction;
- capture hashes/contents if a temporary local manifest is part of a specific validation run;
- do not treat host-private local manifest state as a release manifest.

## 12. Path ownership collisions

Before introducing a Sable project, verify that no upstream project already owns the same checkout path in the active composition.

For replacements/overrides, use deliberate manifest semantics and document why the replacement is necessary.

Do not rely on sync order to decide which repository wins a path collision.

## 13. Device expansion

Future devices such as Bramble or other targets should compose the same common Sable app/platform repositories where semantically compatible.

A new device should add a bounded `device_sable_*` adapter/project and any truly device-specific vendor inputs, not duplicate the Sable Start/Calculator/common-theme repositories.

A common Sable product release may pin different upstream substrate/device revisions per target while retaining common Sable component versions where valid.

## 14. Reconstruction gate

A strong reconstruction gate should prove:

1. start from a documented clean/new source root or equivalently isolated checkout state;
2. use the intended manifest source/revision;
3. sync/checkout the required repositories without manual source copying;
4. verify project paths/revisions;
5. verify no unexpected local-manifest/path override;
6. build the target/module/image according to the milestone claim;
7. hash outputs;
8. record exact source identities;
9. compare expected behavior/artifacts where applicable.

A successful build from a historical workspace that still contains manually migrated source does not by itself close this gate.

## 15. Documentation-before-composition rule

If a new repository, default application, shared service, or device-specific source project is required but not covered by the current architecture, document ownership and purpose before adding it to the manifest.

The manifest should encode decided architecture, not become the place where architecture is accidentally invented.

## 16. Milestone composition checklist

Before closing any R6+ milestone, answer:

- Which exact complete manifest/source composition produced the tested build?
- Which Sable repositories changed for the milestone?
- Are those changes in their canonical repositories?
- Are any source paths supplied by manual copies/symlinks/local host state?
- Are default applications represented accurately as source-built, prebuilt, or user-installed/test fixtures?
- Can another clean checkout identify the same revisions?
- Are device-specific differences bounded to device/vendor projects?
- Does the artifact/evidence bind back to these exact revisions?

If those questions cannot be answered from version-controlled data and evidence, the composition claim is not closed.