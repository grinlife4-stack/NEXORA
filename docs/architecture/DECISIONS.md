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

## Advertiser acceptance and rejection taxonomy

**Status:** Accepted product policy  
**Scope:** This section is the authoritative subject-matter reference for accepting or rejecting advertisers, products, and services. It complements the placement, privacy, disclosure, and safety requirements above; it does not replace them.

### Purpose and governing principle

NEXORA is a space for relaxation, health, beauty, comfort, recreation, and human growth. Advertising must fit that identity and the audience's context. NEXORA is not a general-purpose marketplace or directory of every product and service.

The governing question is:

**Does this product or service have a natural connection to everyday life, health, beauty, comfort, recreation, or human development?**

Commercial value, advertiser preference, and the personal interests of the product's creators do not override this principle.

### Permitted subject areas

Advertising may be accepted in these broad areas:

1. Health and physical care.
2. Hygiene and personal care.
3. Beauty, cosmetics, and skincare.
4. Clothing, fashion, footwear, bags, and accessories.
5. Sports, fitness, and sports equipment.
6. Food, healthy nutrition, and suitable food products.
7. Cooking, kitchen equipment, and related products.
8. Travel, tourism, hotels, and accommodation.
9. Pets, veterinary care, pet products, and pet food.
10. Home, furniture, interior design, and household appliances.
11. Real estate and living environments, including apartments, towers, houses, and villas.
12. Health-oriented buildings, residences, and accommodation.
13. Education, books, arts, and personal development.
14. Culture, entertainment, and recreational activities.
15. Relaxation, comfort, and quality-of-life services.
16. Practical technology and smart products connected to everyday life.
17. Environmental products and sustainable living.
18. Family, social, and care services.
19. Transport and urban experiences connected to everyday life.

These categories are expandable. A new subject may be included when its natural connection to NEXORA's identity is clear.

### Prohibited subject areas

Do not accept advertising for:

1. Gambling, betting, or lotteries.
2. Tobacco and related products.
3. Alcoholic beverages.
4. Weapons and dangerous products.
5. Fast food and clearly unhealthy food products.
6. Deceptive, misleading, or materially unsubstantiated promotions.
7. Political, party, or election advertising.
8. General administrative and organizational services.
9. General industrial and manufacturing services.
10. Factory and workshop machinery and equipment.
11. Specialized construction and industrial tools.
12. General-purpose administrative, organizational, and industrial software.
13. Commercial or professional services with no natural connection to the permitted NEXORA subject areas.

### Boundary for specialized products and services

A product is not prohibited merely because it is technical or specialized. It may be accepted when its direct, intended use is clearly connected to a permitted subject area. Examples include medical equipment, rehabilitation and sports equipment, assistive technology for older people, practical smart-home products, and veterinary services.

By contrast, general industrial machinery, factory equipment, workshop tools, unrelated construction tools, and generic office or PDF/scanning software are outside NEXORA's advertising scope. A technical product should not be admitted merely because it is useful to some businesses or personally interesting to the creators.

### Application

Classify the actual advertised product or service, not just the advertiser's industry label. If an offer spans both permitted and prohibited areas, assess the specific advertised item and its presentation. If its fit with NEXORA is unclear, do not accept it until the relevance is established.

Passing this subject-matter test does not automatically approve an advertisement. All existing requirements for truthful claims, advertiser suitability, disclosure, privacy, placement eligibility, and platform/provider compliance still apply.

**Final rule:** NEXORA accepts advertising that naturally serves the everyday lives, health, beauty, comfort, recreation, or development of its audience. General industrial and administrative advertising, and unrelated commercial promotions, are rejected. The category list may grow, but the product identity must not drift.

## Advertising revenue allocation policy

**Status:** Accepted product/business decision  
**Scope:** Allocation of net advertising revenue received by NEXORA.

### Calculation basis

The allocation percentages apply to net advertising revenue actually received, after deducting directly attributable collection and advertising-network fees, applicable taxes, refunds, and other unavoidable direct transaction costs. Uncollected amounts are not distributable revenue.

### Allocation

Allocate the resulting net amount as follows:

| Allocation | Share |
|---|---:|
| Founder and product owner | 60% |
| NEXORA advertising, promotion, and market development | 30% |
| Product development and improvement | 10% |
| **Total** | **100%** |

There is no separate reserve allocation in this model. The founder/product-owner share is not restricted to a particular internal use. The marketing allocation is intended to attract and retain suitable users and grow awareness of NEXORA. The product-development allocation is intended for improvements to the application and its content and experience.

### Operating principles

- These percentages are applied to net receipts, not gross advertiser spend or quoted contract value.
- Marketing and product-development allocations must be tracked separately and used for their stated purposes.
- The allocation does not authorize increasing ad volume, weakening advertiser acceptance rules, or compromising user privacy and experience to raise revenue.
- This is the approved financial allocation policy; it does not imply that revenue collection, accounting, or budget-disbursement functionality has already been implemented.
- Any change to these percentages or the calculation basis requires an explicit decision update.


## Financial operations and revenue custody policy

**Status:** Accepted operating policy  
**Scope:** Revenue accounting, custody, allocation, authorization, and audit controls for NEXORA advertising and direct sponsorship income.

### Revenue recognition and ledger

- Record income as **pending** when reported by an advertising network or advertiser but not yet irrevocably settled and available to NEXORA.
- Record income as **received** only after the funds or digital assets have arrived at a controlled destination and the relevant payment/network confirmation requirements have been met.
- Calculate the 60/30/10 allocation only from net revenue actually received, using the approved calculation basis in the Advertising revenue allocation policy.
- Maintain an append-only transaction ledger with, at minimum: unique record ID, source/provider, campaign or contract reference, asset/currency, amount, network/rail, transaction ID or bank reference, timestamps, gross amount, direct fees, applicable tax/refund adjustments, net received amount, allocation amounts, status, and reconciliation notes.
- Pending, disputed, reversed, frozen, or unconfirmed balances must never be represented as available cash or spendable budget.
- Reconcile provider statements, on-chain transactions, bank receipts, fees, and the internal ledger. Preserve source records and correction history; do not silently overwrite entries.

### Dedicated revenue wallet and custody

- NEXORA may use a dedicated self-custody wallet solely for verified NEXORA business receipts. Do not mix personal transfers, trading deposits, unrelated income, or third-party funds into this wallet.
- A wallet address is specific to an asset and blockchain network. Maintain an explicit allowlist of accepted asset/network combinations; never assume that the same address format or ticker means the same network.
- Before publishing a receiving address to a provider, verify the provider's supported asset and network, wallet compatibility, ownership/control, deposit minimum, confirmation requirements, and any memo/tag requirement.
- Test each new asset/network route with a small permitted transaction before relying on it for material receipts.
- Keep recovery material offline and under the owner's exclusive control. Never place recovery phrases or private keys in email, cloud storage, chat, source control, analytics, or application logs. Never send them to NEXORA agents, advertisers, payment providers, or support personnel.
- The wallet provider/software and any associated services must explicitly permit the owner's actual residence, business use, and intended activity. Do not misstate residence, beneficial ownership, or identity, and do not use another person's account as a substitute for the real owner.
- A self-custody wallet is a technical custody tool; it does not remove sanctions, tax, licensing, or payment-provider obligations.
- The initial software wallet is a transitional operational choice, not a claim of institutional-grade custody. Establish exposure limits and review migration to stronger custody controls as balances grow.

### Allocation and budget controls

- Maintain separate ledger sub-accounts for: (1) 60% founder/product owner, (2) 30% marketing and market development, and (3) 10% product development and improvement.
- The 60% owner allocation is payable to the verified beneficial owner. The system has no authority to spend or redirect this allocation.
- The 30% marketing allocation may be spent by the system only within a separately approved policy envelope: eligible NEXORA marketing purposes, approved countries/channels, per-transaction and cumulative budget limits, approved counterparties/payment destinations, campaign duration limits, and required evidence of delivery.
- The system may negotiate and prepare standard marketing or reciprocal-promotion arrangements within that envelope. It must not create debt, personal guarantees, open-ended future obligations, exclusivity, or long-term commitments. Any such commitment requires explicit owner approval and legally valid authority.
- The 10% product-development allocation remains under the owner's control. The owner may withdraw or reallocate it. The system may spend from it only after a specific, recorded authorization defining amount, purpose, recipient, and expiry or completion condition. Authorization must be revocable for unspent amounts.
- Unused marketing and development allocations carry forward between accounting periods. An allocation is not a requirement to spend the full amount.
- The system must not transfer funds, sign contracts, or make external payment commitments merely because an allocation exists. Technical authorization, provider permission, and legally valid authority are separate prerequisites.

### Payment execution and audit

- Every outgoing payment requires a ledger entry, purpose, approved budget source, destination verification, amount/asset/network, transaction reference, and authorization record.
- Enforce spending limits before transaction signing or payment submission. Fail closed if balances, authorization, destination, provider status, or network details cannot be verified.
- Changes to wallet addresses, payout instructions, provider accounts, or authorized counterparties require independent verification and an audit record. Do not accept address changes solely from an email or chat message.
- Agents may prepare recommendations, draft contracts, reconcile records, and propose transactions. They must not receive seed phrases/private keys or unrestricted signing authority.
- Keep a complete audit trail for approvals, denials, budget changes, contract drafts, payment attempts, completed payments, reversals, and reconciliation corrections.
- Do not claim that a payment, wallet integration, automated marketing authority, bank account, or legal representative arrangement is implemented until it has been separately built, tested, and lawfully authorized.

### Implementation status boundary

This policy defines the approved financial operating model. It does not establish that NEXORA has a registered legal entity, an approved advertising provider, a compliant payout route, a selected wallet provider, a bank account, or implemented payment/ledger automation. Provider eligibility and legal availability must be verified for the owner's actual residence and beneficial ownership before any production revenue is routed.
