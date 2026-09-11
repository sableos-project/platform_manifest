# SableOS Platform Manifest

Authoritative multi-repository source composition for SableOS.

This repository defines which exact upstream and Sable-owned revisions compose a SableOS build. It is the source-composition authority for the project. Application code, device implementation code, and host build tooling live in their dedicated repositories.

## Current reference target

The primary development reference is Google Pixel 7 (`panther`) on the exact GrapheneOS `2026081300` Android 17 substrate.

The repository is being bootstrapped while the existing Panther Sable Start R3 build/runtime evidence is closed. No manifest here should yet be described as reproducing the validated Panther build until the multi-repository migration and clean reconstruction gate pass.

## Repository roles

- `platform_manifest`: exact revisions composing a build.
- `packages_apps_SableStart`: common Sable Start launcher and shell.
- `platform_sable`: common semantic contracts, services, and adapters.
- `vendor_sable`: common Android product integration.
- `device_sable_<target>`: bounded target-specific integration.
- `build`: source bootstrap, build orchestration, and validation.
- `sableos`: project architecture, ADRs, roadmap, and validation documentation.

## Revision policy

Development manifests may follow active development refs. Validated and release manifests must pin exact revisions. Branch names alone are never sufficient release provenance.

A validated source composition should bind upstream identity, exact Sable revisions, device profile, build configuration, and the validation record corresponding to the resulting artifact.

See `docs/SOURCE_COMPOSITION_MODEL.md` and `docs/RELEASE_MANIFEST_POLICY.md`.
