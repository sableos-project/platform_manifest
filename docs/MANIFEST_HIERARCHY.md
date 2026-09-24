# SableOS manifest hierarchy

Status: **current structural model — 2026-09-24**

The manifest layer defines source composition. It does not own application,
device or build-tool implementation.

Conceptual hierarchy:

```text
default.xml / active development composition

manifests/common/
    common Sable platform/application projects

manifests/devices/
    panther.xml
    titan2.xml             when real device-owned source exists
    titan2-elite.xml       when independently justified
    q27.xml                only after RESEARCH promotion

releases/<device>/
    exact revision-pinned validated compositions
```

Do not create a device manifest merely because a device is being researched.
Create one when there is actual source composition that belongs to that device.

## Common layer

The common layer may reference reusable Sable platform/application repositories,
including the current standalone SableLauncher source once publication/migration
is complete.

Historical SableStart composition remains history; it is not the current HOME
ownership model.

## Device layer

Device manifests contain only bounded target-specific integration such as
product/device trees, overlays or vendor/BSP bindings that cannot remain common.

## Release layer

A validated release manifest pins exact revisions and must correspond to exact
artifact/build evidence. Formal published release identities are immutable;
corrections create a new identity.

## Current roles

```text
panther       frozen accepted reference
titan2        active N0 portability research
titan2-elite  independent candidate
q27           research
```

Bramble is historical reference only.

The manifest hierarchy must not imply support that the runtime/evidence layer has
not established.
