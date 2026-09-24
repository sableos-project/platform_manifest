# Manifest and release provenance policy

Status: **current normative policy — 2026-09-24**

## Exact identity

Every validated build records exact source revisions. Development branches may
move, but validation evidence resolves the exact commits it consumed.

When independently built artifacts enter the product, source manifests alone are
not complete provenance. Bind the exact artifact identity as well.

## Artifact provenance

For each accepted external artifact record at least:

```text
source repository + exact commit
upstream pin if reused
toolchain/build environment
package/module identity
artifact kind
artifact hash(es)
build evidence
```

K1 registry v2 recognizes multiple artifact kinds, including target-files,
full-device images, GSI system images, system/product bundles and boot/recovery
bundles.

## Device/vendor basis

Non-Pixel N0 artifacts must additionally identify the exact stock/vendor basis
on which they rely when applicable. A Sable GSI plus stock vendor/firmware is
not provenance-equivalent to a fully owned target-files build.

## Panther

Panther R9 is frozen reference evidence. Its accepted image remains bound to its
exact source/artifact identity.

## Titan family

Titan 2 and Titan 2 Elite use independent source/vendor/firmware evidence.
Common app/product revisions may match, but device-specific inputs and acceptance
do not inherit across the family.

## Branches, tags and release manifests

- branches are mutable development references;
- tags identify named source points;
- revision-pinned manifests identify exact source compositions;
- artifact records identify exact external/generated inputs;
- physical evidence identifies actual runtime qualification.

No one layer substitutes for another.

## Production signing

Production application keys, AVB signing hierarchy, OTA signing/update service,
key custody and signed-output provenance remain a later program. Development
provenance must already be sufficient to answer which approved source/artifacts
produced a candidate before production signing is introduced.
