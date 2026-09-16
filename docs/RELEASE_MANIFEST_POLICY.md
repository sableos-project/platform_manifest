# Manifest and release provenance policy

Status: **normative development/release-input provenance policy.**

SableOS distinguishes moving development state, validated development-image inputs and later production release/signing state.

## Development source composition

Development manifests may reference active branches while work is in progress. Every validation/build record still resolves the actual revisions it consumed.

Standalone application qualification may happen outside the Android source manifest. That is allowed only when the trusted artifact later consumed by the product is represented by exact source/toolchain/artifact provenance.

## R8 trusted application input

R8 has two application-build stages:

```text
A1 GitHub/disposable qualification
 -> A2 trusted standalone build on ai-g732
 -> exact trusted application freeze
```

A1 artifacts are evidence, not automatically trusted product binaries.

For every A2-built application accepted into Panther/Titan 2 development images, bind at least:

```text
source repository + exact commit
upstream/reuse source + exact commit where applicable
trusted A2 build/toolchain/dependency identity
application/package ID + version
trusted APK SHA-256
permissions/exported components
classes*.dex identity
JNI .so identity
native ABI / 16 KiB compatibility
product module/import + install path
Soong signing/transformation behavior
```

## Validated development-image composition

A validated development build binds:

```text
exact upstream/substrate identity
exact Sable source revisions
exact target device/product/release/variant
vendor/BSP/generated inputs
exact trusted external application inputs
build/toolchain/host identity
isolated target OUT_DIR identity
resulting artifact hashes
validation record
```

A source manifest alone is not a complete input identity when sealed standalone APKs are consumed.

## Panther and Titan 2

Where compatible, the R8 Panther and Titan 2 development builds should consume the same frozen common app artifacts and common product integration. Device-specific differences are recorded as bounded target adapters/exceptions.

Each target retains separate build/output/runtime evidence.

## Production signing — deferred

Production signing is not part of R8 development composition closure.

Only after Panther and Titan 2 development qualification is satisfactory should a release-signing workstream define production application keys, AVB hierarchy, OTA signing, `sign_target_files_apks`, key custody/backup/recovery/rotation, offline signing-host policy and signed-output provenance.

The ThinkPad P50 is a future signing-host candidate only. OptiPlex is not part of the current signing plan. No host should be called `sable-signer-01` until commissioned.

Development/test signing identity used for engineering images is recorded separately and must not be presented as production signing provenance.

## Formal release manifests

A future formal release manifest/provenance definition is immutable after publication. Corrections produce a new release identity rather than rewriting an existing validated definition.

Historical input records remain available even after an application/source implementation is replaced.

## Branches, tags, manifests and artifacts

- branches represent moving development;
- protected/signed tags may identify component milestones;
- revision-pinned manifests identify OS source compositions;
- sealed artifact records identify exact trusted external build inputs;
- development-image records bind source/artifacts/host/target/runtime evidence;
- future release records additionally bind production signing/update outputs.

A branch name, package name or filename alone is never sufficient provenance.

## Build-host transition

R8 trusted application and Android development builds move to `ai-g732` after storage/source/toolchain migration is sealed. The host transition does not change source ownership; it becomes part of the build-environment identity.

Do not carry host-private ThinkPad paths/local copies into validated build provenance.

## Governing questions

For a development image:

> Which exact source revisions, trusted external inputs, build environment and product target produced this exact image?

For a future production release:

> Which exact approved development/release candidate plus production signing identities produced this exact released artifact?

If either answer depends on an untracked developer workspace, provenance is incomplete.
