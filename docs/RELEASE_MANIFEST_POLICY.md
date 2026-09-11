# Manifest and release provenance policy

SableOS distinguishes moving development state from validated source compositions.

## Development

Development manifests may reference active branches while work is in progress. Their purpose is convenience and integration, not archival reproducibility.

## Validated build manifests

A validated build manifest must pin exact revisions for every Sable-owned project and must bind the upstream Android release/tag used as the substrate. It must also reference the device profile and corresponding validation record.

## Release manifests

A release manifest must be immutable after publication. Corrections require a new manifest identity rather than rewriting an existing validated release definition.

## Branches, tags, and manifests

- branches represent ongoing development;
- signed or otherwise protected tags identify component milestones;
- revision-pinned manifests identify complete OS source compositions.

The manifest is the authoritative answer to: which exact commits made this build?

## Current bootstrap state

The organization repositories were created on 2026-09-11 while the Panther Sable Start R3 compile/type-check gate was still in progress. The first validated Panther manifest will be created only after current source capture, repository migration, and clean reconstruction have all passed.
