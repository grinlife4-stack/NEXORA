# NEXORA Brand Asset Ownership and Development Boundary

**Status:** Approved project boundary  
**Decision date:** 2026-11-19

## Ownership and authoritative master

NEXORA owns its brand identity and official logo asset. This repository, `grinlife4-stack/NEXORA`, is the sole authoritative location for the official master artwork:

- **Path:** `projects/NEXORA/assets/brand/NEXORA-Official-Logo.png`
- **Original Git blob SHA in TRADIX:** `7f2a39590db755077b0a903cf93056121e0ef1b5`

The master artwork must remain unchanged. Derivatives are permitted only as technical exports for platform requirements (for example, app icons, PWA icons, and responsive placements). Derivatives may adjust dimensions, format, or transparent padding as required, but must preserve the artwork, wordmark, colors, proportions, and composition. A derivative is never a replacement for the master.

## TRADIX development role

TRADIX may retain a working copy of the official logo in its development workspace:

`projects/NEXORA/assets/brand/NEXORA-Official-Logo.png`

That copy exists only to support NEXORA-related design, development, build, testing, packaging, and delivery work performed with TRADIX tooling. It is a development copy, not an independent master and not a transfer of brand ownership.

TRADIX must not become a runtime dependency for NEXORA. NEXORA's application, release packages, and deployed product must resolve the logo from NEXORA-owned project assets. No production app should load the logo from a TRADIX URL or require a TRADIX checkout at runtime.

## Synchronization and change control

1. The NEXORA repository is the canonical source for the master artwork.
2. A TRADIX working copy must be copied from the NEXORA canonical file, not independently redrawn or recreated.
3. Record the canonical file hash when updating the TRADIX working copy.
4. If the two copies differ, the NEXORA master wins; do not silently overwrite or promote the TRADIX copy.
5. Any proposed artwork change requires explicit approval by the NEXORA owner. Technical exports do not authorize artwork changes.
6. Keep this rule in both repositories so developers and agents encounter the same boundary regardless of entry point.

## Source-package reconciliation

The NEXORA 0.5.4 package's JPEG and PNG were compared at decoded-pixel level: both are 784×1168 RGB images with zero per-channel difference. The JPEG was therefore a redundant duplicate, not a distinct artwork version. It has been removed.

The corrected source archive contains no logo master at all. This avoids maintaining multiple copies of the same brand asset. The application continues to reference the canonical path above. During import, the repository workflow injects the canonical master into the temporary test workspace, then merges the application source without overwriting the repository-owned master.

The existing PWA/app icons remain technical derivatives. They are not additional master artworks.

## Non-goals

This decision does not merge NEXORA into TRADIX, transfer NEXORA's identity or IP to TRADIX, make TRADIX the product owner, or create a runtime, account, data, or operational dependency between the projects.
