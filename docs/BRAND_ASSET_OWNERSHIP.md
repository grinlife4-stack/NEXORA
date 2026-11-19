# NEXORA Brand Asset Ownership and Temporary Tooling Boundary

**Status:** Approved project boundary  
**Decision date:** 2026-11-19

## Ownership and authoritative master

NEXORA owns its brand identity and official logo asset. This independent repository, `grinlife4-stack/NEXORA`, is the sole authoritative location for the unchanged master artwork:

- **Path:** `projects/NEXORA/assets/brand/NEXORA-Official-Logo.png`
- **Git blob SHA:** `7f2a39590db755077b0a903cf93056121e0ef1b5`

The master artwork must remain unchanged. Platform icons and other derivatives may adjust dimensions, format, or transparent padding only as required, while preserving the artwork, wordmark, colors, proportions, and composition. A derivative is never a replacement for the master.

## TRADIX role and temporary-file rule

TRADIX is a production tool. It is not NEXORA's owner, parent, permanent workspace, archive, or runtime dependency.

During an active, authorized NEXORA task, TRADIX may temporarily process or hold only the working files necessary for that task. Those files are temporary operational copies, not authoritative assets.

At NEXORA project completion, issue a specific **TRADIX review-and-cleanup** task:
1. Identify every NEXORA-specific file, copy, document, package, setting, cache, and temporary record remaining in TRADIX.
2. Verify that every required authoritative asset, source file, decision, and record is safely stored in NEXORA's own repository or approved project-owned location.
3. Verify that NEXORA has no runtime or operational dependency on TRADIX.
4. Remove NEXORA-specific temporary artifacts from TRADIX.
5. Retain only generic, reusable tools and capabilities that contain no NEXORA-specific project material.
6. Produce a cleanup report listing what was removed, what generic tooling remains, and any exception requiring owner approval.

Do not delete an item until its required authoritative copy and integrity have been verified. Do not preserve a NEXORA-specific copy in TRADIX merely for convenience after the authorized task is complete.

## Application and release boundary

- NEXORA application source and releases resolve the logo from NEXORA-owned project assets.
- NEXORA runtime must not load the logo or any required resource from a TRADIX URL, checkout, service, or filesystem.
- Delivery artifacts must include the assets required to run independently.
- NEXORA must remain exportable and operable if TRADIX is unavailable, replaced, or removed.

## Change control

1. NEXORA's canonical master is authoritative.
2. Any temporary tooling copy must originate from the NEXORA master.
3. Verify byte identity when a working copy is created or refreshed.
4. If a mismatch is found, stop; the NEXORA master remains authoritative.
5. Only the NEXORA owner may approve changes to the artwork.
6. Generic tooling may be reused across projects, but project-specific assets, records, data, and secrets must not be retained or shared.

## Source-package reconciliation

The NEXORA 0.5.4 package's JPEG and PNG were compared at decoded-pixel level: both are 784×1168 RGB images with zero per-channel difference. The JPEG was redundant and removed.

The corrected source archive contains no logo master. The application references the canonical path in this repository. The existing PWA/app icons are technical derivatives, not additional master artworks.

## Non-goals

This decision does not merge NEXORA into TRADIX, transfer NEXORA's identity or IP to TRADIX, make TRADIX the product owner, or create a permanent runtime, account, data, or operational dependency.
