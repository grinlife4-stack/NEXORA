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


## Monetization and advertising policy

**Current product decision:** NEXORA is free to use, with clearly bounded, non-intrusive advertising present from the first public release.

- No mandatory subscription, paywall, account, or payment is introduced into the core experience.
- Advertising is permitted only in predefined, reserved UI placements. The initial limit is one visible ad placement per screen.
- Ads must be clearly labelled (for example, "Advertisement" or "Sponsored") and visually distinct from editorial and learning content.
- No interstitials, pop-ups, autoplay video, audio ads, forced rewarded ads, or ads that interrupt playback, lessons, exercises, meditation, or reading.
- Users must be able to dismiss or hide an ad where the format allows it.
- Contextual placement is preferred. Do not use personal data, mood/check-in entries, listening history, learning progress, or other sensitive behavioural profiles for ad targeting.
- Do not sell personal data or expose locally stored user data to advertisers.
- The advertising integration must be an optional, isolated module. The app's core features must continue to work when offline, when an ad provider is unavailable, or when the user declines optional network access. In those cases, the reserved ad slot may remain empty.
- No advertising SDK or remote service may become a mandatory dependency for storage, playback, learning, or other core functionality.
- Sponsored content must be disclosed and reviewed for relevance and safety. Advertising must not influence lesson ordering, educational conclusions, or wellbeing guidance.
- Any future change to ad frequency, formats, targeting, or data handling requires an explicit architecture decision and privacy review.

The initial implementation should define the placement contract and privacy boundary first. Selection of an ad network or sponsor is a separate decision and must not be assumed by the architecture.
