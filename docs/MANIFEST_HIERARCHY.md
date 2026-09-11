# SableOS manifest hierarchy

SableOS uses one common manifest layer plus device-specific manifest files. The manifest repository defines source composition; it does not own application, device, or build-tool implementation.

Recommended hierarchy:

```text
default.xml
manifests/common/sable.xml
manifests/devices/panther.xml
manifests/devices/bramble.xml
releases/panther/<release>.xml
releases/bramble/<validation>.xml
```

## Roles

`default.xml`
- active development entry point;
- includes the common Sable layer and the selected development target composition.

`manifests/common/sable.xml`
- Sable-owned projects shared across devices;
- packages/apps/SableStart;
- common Sable platform/services;
- vendor/sable common integration.

`manifests/devices/<target>.xml`
- target-specific Sable adapter projects;
- only device-specific repos required for that target;
- no copies of common Sable applications or semantics.

`releases/<target>/<id>.xml`
- immutable or revision-pinned complete source composition for a validated build/release;
- exact Sable project revisions;
- exact upstream revisions or release tag binding;
- target/support-level metadata recorded in adjacent documentation.

## Composition rule

Conceptually:

```text
upstream substrate
    + common Sable manifest
    + one device manifest
    = development source tree
```

A validated build adds an exact revision-pinned release manifest.

## Initial target model

- Panther: PRIMARY; GrapheneOS 2026081300 / Android 17 reference.
- Bramble: future PORTABILITY profile; exact Android 16/LineageOS substrate to be qualified before manifest creation.

The first Panther manifest is not considered validated until the organization-based multi-repository checkout reproduces the already-qualified SableStart build and subsequent runtime gates.
