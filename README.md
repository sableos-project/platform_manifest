# SableOS Platform Manifest

Authoritative multi-repository source composition for SableOS.

This repository defines which exact upstream and Sable-owned revisions compose a SableOS build. It is the source-composition authority for the project. Application code, device implementation code, and host build tooling live in their dedicated repositories.

## Current reference target

The primary development reference is Google Pixel 7 (`panther`) on the validated GrapheneOS `2026081300` Android 17 substrate work.

The repository is being bootstrapped while the existing Panther Sable Start source migration/build/reconstruction gates close. No manifest here should yet be described as reproducing the validated Panther build until the multi-repository migration and clean reconstruction gate pass.

The current R5-R3 audit found that the repository still contains policy/documentation only and does not yet contain an operational `default.xml`/common/device/release manifest hierarchy. The exact audit result and reconstruction acceptance plan are recorded in:

- [`docs/R5_R3_RECONSTRUCTION_PLAN.md`](docs/R5_R3_RECONSTRUCTION_PLAN.md)

Manifest integration is therefore the next composition change after the read-only historical-workspace audit establishes the current upstream/local-manifest/path-collision state.

## Repository roles

- `platform_manifest`: exact revisions composing a build.
- `packages_apps_SableStart`: common Sable Start launcher and shell.
- `platform_sable`: common semantic contracts, services, adapters, and shared product/design contracts.
- `vendor_sable`: common Android product integration/default-package composition.
- `device_sable_<target>`: bounded target-specific integration and qualification.
- `build`: source bootstrap, build orchestration, reconstruction, and validation.
- `.github`: current organization-wide development-plan/policy documentation while the future central `sableos` project repository transition is incomplete.

## Current development train

The active internal milestones are R5 migration/reconstruction, R6 real Sable Start, R7 daily-driver phone qualification, R8 shared design/customization, R9 first Sable utilities, and R10+ deliberate replacement/expansion.

These milestone labels are **not** product versions. Their source-composition requirements are defined in:

- [`docs/DEVELOPMENT_MILESTONE_COMPOSITION.md`](docs/DEVELOPMENT_MILESTONE_COMPOSITION.md)

## Revision policy

Development manifests may follow active development refs where appropriate, but every build/validation record must resolve them to exact commits. Validated and release manifests must pin exact revisions. Branch names alone are never sufficient release provenance.

A validated source composition should bind upstream identity, exact Sable revisions, device profile, build configuration, and the validation record corresponding to the resulting artifact.

See:

- [`docs/SOURCE_COMPOSITION_MODEL.md`](docs/SOURCE_COMPOSITION_MODEL.md)
- [`docs/MANIFEST_HIERARCHY.md`](docs/MANIFEST_HIERARCHY.md)
- [`docs/RELEASE_MANIFEST_POLICY.md`](docs/RELEASE_MANIFEST_POLICY.md)
- [`docs/DEVELOPMENT_MILESTONE_COMPOSITION.md`](docs/DEVELOPMENT_MILESTONE_COMPOSITION.md)
- [`docs/R5_R3_RECONSTRUCTION_PLAN.md`](docs/R5_R3_RECONSTRUCTION_PLAN.md)

The manifest should encode decided architecture. If a new Sable repository, default application, shared service, or device-specific source project is needed, document its ownership before introducing it into source composition.