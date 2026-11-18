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

**Current product decision:** NEXORA is free to use, with relevant, curated, non-intrusive advertising. Advertising must support the product's wellbeing and quality-of-life focus. The product is not opposed to advertising volume by itself; the unacceptable cases are irrelevant advertising and cluttered, intrusive, or visually noisy placements.

### Permitted advertising surfaces

- An app-open advertisement may be presented on eligible launches/entries. It must be clearly labelled, must not delay access when no ad is ready, and must provide a clear exit. A short close-delay may be used only when the selected ad format, platform rules, and provider policy explicitly permit it; target 2–5 seconds where permitted, never force a delay that the format or policy does not allow. No autoplay sound.
- Contextual placements may appear on home, discovery, recommendation, and other eligible browsing surfaces. There is no arbitrary fixed numerical cap as a product principle; the practical limit is whether the page remains visually calm, readable, useful, and easy to navigate. Side placements are acceptable when relevant and discreet, but must never become crowded, repetitive, obstructive, or visually dominant.
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


### Algorithmic advertising selection

NEXORA should use a contextual recommendation engine rather than random ad rotation or unrestricted behavioural profiling. Its purpose is to select the most relevant, useful, trustworthy advertisement for an eligible placement while preserving user privacy and a calm product experience.

#### Permitted selection signals

The engine may use:
- The current page, feature, or content category (for example, sleep, nutrition, travel, exercise, or personal care).
- Broad interest categories explicitly selected or edited by the user.
- Direct, optional feedback on advertisements, such as save, like, hide, or report. These preference signals must remain local to the device unless the user separately and explicitly chooses an export mechanism.
- Ad-level information needed to assess suitability, such as category, declared claims, advertiser verification status, freshness, placement eligibility, and prior display frequency.

A click alone must not be treated as proof of preference or used to build a sensitive profile. The user must be able to reset or disable personalized ad preferences; contextual ads based only on the current page category may remain available where permitted.

#### Prohibited selection signals

The engine must not inspect, infer from, or use:
- Mood check-ins, stress or wellbeing entries, health information, sleep records, or private journal content.
- Meditation, lesson, reading, or listening history; completion rates; progress; goals; or personal playback data.
- Sensitive traits or vulnerability inferences, including inferred illness, emotional state, or personal hardship.
- Cross-app tracking, third-party identity graphs, or personal data obtained from unrelated services.

The fact that a user is viewing a progress overview does not authorize targeting based on their progress data. Only the broad page category may be used for contextual placement there.

#### User-declared needs, conflict avoidance, and prohibited ad categories

Ad relevance must account for a user's explicitly declared preferences and exclusions so that a technically related advertisement does not conflict with the user's stated needs. Relevance is not merely a match to the page category.

- Users may optionally declare broad needs, interests, and ad exclusions (for example, avoiding fast food or food promotions while following a dietary plan). These settings are stored and evaluated locally on the device.
- Treat declared exclusions as hard filters: do not show an advertisement that conflicts with them, even if it is contextually relevant or commercially valuable.
- Never infer a dietary plan, health condition, weight goal, or other sensitive need from check-ins, journals, listening behaviour, progress, or other private app records. Do not use such information to target ads.
- The purpose of a declared need is to protect the user from conflicting or unwanted promotions, not to exploit that need for more persuasive targeting.
- Fast-food advertising and promotions for clearly low-quality, nutritionally poor food products are prohibited. This restriction applies regardless of placement, advertiser payment, or predicted revenue.
- Food-related promotions that are eligible must meet NEXORA's quality and wellbeing standards and must not undermine an explicitly declared dietary preference or exclusion.
- Advertisements must not use shame, body-image pressure, fear, or unsupported weight-loss and health claims.
- Users must be able to edit, clear, or disable these optional preferences at any time. No account or remote profile is required.

When there is uncertainty about whether an advertisement conflicts with a declared preference or meets the food-quality standard, exclude it until it can be reviewed. Commercial value never overrides a user-declared exclusion or a prohibited-category rule.

#### Ranking and decision logic

For each eligible placement, the engine should:
1. Apply hard eligibility filters first: permitted page, advertiser and product acceptance, required disclosures, privacy rules, and platform/provider policy.
2. Exclude ads already hidden or reported by the user, ineligible creatives, and ads blocked by frequency caps.
3. Rank the remaining candidates using contextual relevance, user-selected broad interests, advertiser/content quality, freshness, diversity, and repetition controls.
4. Return no ad when no candidate meets the minimum quality and relevance threshold. Filling every slot is not a goal.
5. Record only the minimum operational information needed for frequency control and aggregate evaluation. Do not create a personal behavioural dossier.

The ranking objective must balance relevance, usefulness, trust, diversity, and user experience. It must not optimize click-through rate or revenue alone, and must never reward misleading claims, excessive repetition, or interruption of an active experience.

#### User-level ad frequency and fatigue management

The recommendation engine must account for each user's recent advertising exposure, not only the number of placements available on a page. Relevant ads are not automatically acceptable in unlimited volume.

- Apply configurable per-user frequency controls across eligible placements, including app-open and in-page ads, using the minimum operational counters needed. Do not use sensitive personal information to calculate these limits.
- Consider recent ad count, time since the last ad, repeated creatives or advertisers, dismissals, hides, and reports as signals of possible ad fatigue.
- Reduce, pause, or suppress further ads when exposure becomes excessive or the user repeatedly dismisses or hides them. Never increase ad pressure merely because a user does not click.
- Avoid showing the same creative or advertiser repeatedly within a short period. Rotate among eligible, high-quality alternatives where appropriate.
- Preserve ad-free routes and never interrupt an active meditation, audio session, lesson, reading, exercise, or sleep experience, regardless of frequency allowance.
- Let users control or reset optional ad preferences. Frequency management must remain privacy-preserving and must not require an account or remote behavioural profile.
- Evaluate frequency rules against user complaints, dismissals, retention, perceived relevance, and revenue together. Revenue or impressions must not override user experience.
- If no suitable ad remains within the user's frequency allowance, show no ad.

The exact thresholds and cooldown windows should be configurable and validated through testing; do not hard-code arbitrary limits before observing real usage.

#### User control and offline behaviour

- Ad preference controls must be understandable and optional.
- Save, like, hide, and report actions must have clear meanings and must not be disguised as navigation controls.
- Personal ad preference signals should be stored locally and included in local export/import only when the user chooses to include them.
- If the device is offline, the ad provider is unavailable, or no eligible ad passes the filters, the placement remains empty and the core app continues normally.
- The recommendation engine must be isolated from the storage, audio, learning, and wellbeing core. It must not introduce mandatory accounts, remote profiles, or always-on server dependencies.

This policy defines the selection architecture; it does not mean an ad-ranking engine, tracking system, or ad-network integration has already been implemented. Implementation requires a separate, testable change on the feature branch and must not modify the immutable 0.5.4 baseline.
