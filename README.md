# NEXORA

## Brand asset authority

The official NEXORA logo master is owned and maintained in this repository at `projects/NEXORA/assets/brand/NEXORA-Official-Logo.png`. This repository is the sole source of truth for the master artwork. The master is preserved unchanged; platform icons and other derivatives must be exported from it and must not replace it.

TRADIX may keep a working copy in its own development workspace for design, build, test, and packaging tasks. That copy is not a second authority and does not transfer ownership or make NEXORA dependent on TRADIX. NEXORA releases must consume the logo from their own project assets, not from a TRADIX URL or checkout.

Offline-first, multilingual wellness PWA. Release locales: English, French, and Spanish.

## Source import

The verified source package is **NEXORA 0.5.4**. Its SHA-256 is:

`55483d73738ba24fcdea1de78b9f757628866a689f794656e9213b2e9cfb3673`

To import it, upload the exact file `NEXORA-0.5.4-source-package.zip` to the repository root on the `main` branch. The GitHub Actions workflow `Import NEXORA 0.5.4 source` will verify the checksum, inspect the archive, run the Node.js test suite, extract the complete `projects/NEXORA/` tree, and commit the source. The uploaded archive is removed after a successful import.

Do not substitute a different ZIP or rename the package. A checksum mismatch intentionally stops the import.

## Current verification boundary

- Package integrity: verified.
- Automated Node.js tests: 27/27 passed locally.
- Physical iPad/iPhone Safari, background audio, accessibility, and production hosting: not yet verified.
- The three included ambience tracks are synthesized prototypes, not professionally mastered audio.
