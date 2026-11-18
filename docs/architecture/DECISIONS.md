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

**Current product decision:** NEXORA is free to use, with relevant, curated, non-intrusive advertising. Advertising must support the product's wellbeing and quality-of-life focus rather than turn the interface into an ad-heavy environment.

### Permitted advertising surfaces

- An app-open advertisement may be presented on eligible launches/entries. It must be clearly labelled, must not delay access when no ad is ready, and must provide a clear exit. A short close-delay may be used only when the selected ad format, platform rules, and provider policy explicitly permit it; target 2–5 seconds where permitted, never force a delay that the format or policy does not allow. No autoplay sound.
- Limited, predefined contextual placements may appear on the home, discovery, and recommendation surfaces. Keep the interface visually quiet, with at most one visible ad placement per screen as the initial design constraint.
- A clearly labelled curated offers area may present relevant services, experiences, and products. Users may save or revisit offers they find useful.
- Direct sponsorships and network-supplied ads are both possible, subject to the same relevance, verification, disclosure, and privacy rules.

### Ad-free experiences

- Meditation sessions and active relaxation exercises.
- Audio playback and guided listening.
- Lessons, learning, reading, and study sessions.
- Sleep and rest experiences.
- Private records and personal-history detail views where an advertisement would expose, overlap, or distract from sensitive information.

The progress overview/review area is eligible for one quiet, clearly labelled contextual ad placement, provided it does not overlap progress charts, personal records, or controls. Ad selection must not use the user's progress, history, goals, check-ins, or other personal data. No ad may interrupt an active session, playback, lesson, exercise, meditation, or reading.

### Relevance and advertiser quality

- Ads and sponsored offers must fit NEXORA's defined areas: health and wellbeing, relaxation, sleep, nutrition and cooking, physical activity, personal care, relevant travel and hospitality, and quality-of-life experiences.
- Unrelated products and services (for example, industrial tools unrelated to the product's subject) are not eligible.
- Health-related claims, products, and services require additional scrutiny. Do not accept unsubstantiated treatment claims, misleading health promises, unlicensed services, or prohibited/high-risk products.
- Sponsored content must be clearly distinguished from NEXORA's own editorial, educational, and wellbeing content. Advertisers must not influence educational conclusions or wellbeing guidance.
- Users should be able to dismiss or hide ads where the format supports it, and report irrelevant or inappropriate advertising.

### Privacy, frequency, and technical boundaries

- Contextual relevance may use the current content category or page, but must not use personal data, mood/check-in entries, listening history, learning progress, health information, or sensitive behavioural profiles for ad targeting.
- Do not sell personal data or expose locally stored user data to advertisers.
- Avoid repetitive delivery of the same creative. Frequency caps and placement rules must be configurable and tested against retention, user complaints, and revenue rather than optimized for impressions alone.
- No interstitial may interrupt an active task or appear unexpectedly over content. App-open ads are a distinct, explicitly permitted entry surface and must follow the constraints above.
- The advertising integration must be an optional, isolated module. Core features must continue to work offline, when an ad provider is unavailable, or when the user declines optional network access. In those cases, ad placements remain empty.
- No advertising SDK or remote service may become a mandatory dependency for storage, playback, learning, or other core functionality.
- Any future change to ad frequency, formats, targeting, or data handling requires an explicit architecture decision and privacy review.

The initial implementation must define placement contracts, ad-free routes, advertiser acceptance criteria, and privacy boundaries before integrating an ad network. Selection of an ad network or sponsor is a separate decision and must not be assumed by the architecture.
