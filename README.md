# NEXORA

## Brand asset authority

The official NEXORA logo master is owned and maintained in this repository at `projects/NEXORA/assets/brand/NEXORA-Official-Logo.png`. This repository is the sole source of truth for the master artwork. The master is preserved unchanged; platform icons and other derivatives must be exported from it and must not replace it.

TRADIX may keep a working copy in its own development workspace for design, build, test, and packaging tasks. That copy is not a second authority and does not transfer ownership or make NEXORA dependent on TRADIX. NEXORA releases must consume the logo from their own project assets, not from a TRADIX URL or checkout.

Offline-first, multilingual wellness PWA. Release locales: English, French, and Spanish.

## Source import

The verified source package is **NEXORA 0.5.4**. Its SHA-256 is:

`83b2b5fc464a5df1b5f1f8ef74b187962efdae0591a82ea28690a09eaa0a1f8e`

To import it, upload the exact file `NEXORA-0.5.4-source-package.zip` to the repository root on the `main` branch. The GitHub Actions workflow `Import NEXORA 0.5.4 source` will verify the checksum, inspect the archive, run the Node.js test suite, merge the app source into `projects/NEXORA/`, preserve the canonical logo already stored in this repository, and commit the source. The archive intentionally contains no duplicate logo master. The uploaded archive is removed after a successful import.

The corrected package removes the redundant JPEG and duplicate PNG from the archive. The logo master remains only at `projects/NEXORA/assets/brand/NEXORA-Official-Logo.png`. Do not substitute a different ZIP or rename the package. A checksum mismatch intentionally stops the import.

## Current verification boundary

- Package integrity: verified.
- Automated Node.js tests: 27/27 passed locally.
- Physical iPad/iPhone Safari, background audio, accessibility, and production hosting: not yet verified.
- The three included ambience tracks are synthesized prototypes, not professionally mastered audio.
