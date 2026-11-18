# NEXORA Architecture Decisions

**Status:** Accepted  
**Date:** 2026-11-18  
**Baseline:** NEXORA 0.5.4 (must remain unchanged)

## Product architecture boundaries

The following are excluded from the product's mandatory core:

- User accounts or mandatory registration.
- A permanently running application server.
- Mandatory subscriptions or payment gates.
- Mandatory dependence on third-party APIs or remote services.

The application must remain useful on-device and support offline operation for locally available features and media. Optional distribution, content acquisition, or update mechanisms must not become runtime requirements for the core experience.

## Personal data and privacy

- Personal information, preferences, favorites, listening history, progress, and playback position are stored locally on the user's device.
- No account-based synchronization or remote personal-data store is assumed.
- Data export/import and recovery must be considered as part of storage design. Any protected export must use encryption and must not silently upload data.
- Network access must not be required to read or update locally stored personal data.

## Release and change-control policy

- NEXORA 0.5.4 is the immutable baseline for this development cycle.
- Do not edit, overwrite, or replace baseline source files in place.
- All implementation work must occur on a separate feature branch.
- A candidate release may replace the baseline only after automated regression tests and practical device testing pass.
- Failed or incomplete work remains isolated on its branch; the baseline remains recoverable.

## Current development priority

The next engineering phase is limited to two foundational areas:

1. Local data storage, integrity, migration, and recovery.
2. Audio playback, playback state, offline media, and iOS device behavior.

New decorative features or broad feature expansion are out of scope until these foundations are reliable.

## Decision review

These decisions may be changed only through an explicit architecture decision update, not by accidental dependency additions during implementation.
