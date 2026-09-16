# Manifest and release provenance policy

Status: **normative release-input provenance policy.**

SableOS distinguishes moving development state from validated/release input compositions.

## Development

Development manifests may reference active branches while work is in progress. Every validation/build record still resolves the actual revisions it consumed.

Development application qualification may happen outside the Android source manifest. That is allowed only when the resulting product input is later represented by an exact artifact/source provenance record.

## Validated build composition

A validated build composition binds:

```text
exact upstream/substrate identity
exact Sable source-project revisions
exact target device/product/release/variant
vendor/BSP/generated input identity
exact qualified external application artifact inputs, if any
build/toolchain/host identity
resulting artifact hashes
validation record
```

A source manifest alone is not a complete build-input identity when externally qualified APKs are consumed.

## Qualified application artifact record

For every standalone-built application accepted into a validated/release build, bind at least:

```text
source repository + exact commit
upstream/reuse source + exact commit where applicable
qualification workflow/run
build variant/toolchain/dependency identity
application/package ID + version
APK SHA-256
permissions/exported components
native ABI/library inventory
product module/import + install path
signing or build-time transformation behavior
```

The exact storage format for this metadata may evolve, but it must be immutable/reviewable with the validated build definition.

## Release manifests

A release manifest/provenance definition is immutable after publication. Corrections produce a new release identity rather than rewriting an existing validated definition.

Historical input records remain available even after a source repo/app is replaced in later releases.

## Branches, tags, manifests and artifacts

- branches represent moving development;
- protected/signed tags may identify component milestones;
- revision-pinned manifests identify complete OS source compositions;
- sealed artifact records identify exact external build inputs;
- release records bind the source composition and artifact inputs to final signed outputs.

A branch name, package name or filename alone is never sufficient release provenance.

## Build-host transition

The next R8 Panther integration image is intended for `ai-g732` after its storage/source/toolchain migration is sealed. The host transition does not change source ownership; it is part of the build-environment identity recorded with the validated output.

Do not carry host-private ThinkPad paths/local copies into release provenance.

## Current bootstrap/history note

The organization was originally bootstrapped during R3/R5 SableStart migration/reconstruction work. Those historical plans/evidence remain audit records, but the current R8 release-input model includes independently qualified application artifacts in addition to revision-pinned OS source.

## Governing question

The complete release provenance must answer:

> Which exact source revisions, qualified external inputs, build environment, product target and signing identity produced this exact released artifact?

If that cannot be answered without consulting an untracked developer workspace, the release provenance is incomplete.