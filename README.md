# NEXORA

## Brand asset authority

NEXORA owns its brand identity and official logo asset. This repository is the sole source of truth for the unchanged master artwork at `projects/NEXORA/assets/brand/NEXORA-Official-Logo.png`. Platform icons and other derivatives must be exported from that master and must never replace it.

TRADIX is a production tool, not a project archive or owner. It may temporarily hold NEXORA-specific working files only while an authorized development, test, build, or delivery task is active. At project completion, those temporary copies and records must be reviewed and removed from TRADIX. NEXORA must not depend on TRADIX at runtime or for continued access to its source, assets, data, or releases.

Offline-first, multilingual wellness PWA. Release locales: English, French, and Spanish.

## Source import

The verified source package is **NEXORA 0.5.4**. Its SHA-256 is:

`83b2b5fc464a5df1b5f1f8ef74b187962efdae0591a82ea28690a09eaa0a1f8e`

The package contains the application source and prototype media, but no logo master. The canonical logo remains in this repository at `projects/NEXORA/assets/brand/NEXORA-Official-Logo.png`. The import workflow must verify the exact archive checksum, run the Node.js test suite, merge the app source without overwriting the canonical logo, and remove the uploaded archive after a successful import.

The package excludes the redundant JPEG and duplicate PNG. Do not substitute a different ZIP or rename the package. A checksum mismatch intentionally stops the import.

## Current verification boundary

- Package integrity: verified.
- Automated Node.js tests: 27/27 passed locally.
- Physical iPad/iPhone Safari, background audio, accessibility, and production hosting: not yet verified.
- The three included ambience tracks are synthesized prototypes, not professionally mastered audio.
