# NEXORA 0.5.4+ — Storage and Audio Engineering Plan

**Status:** Gate 0 verified; implementation has not started  
**Working branch:** `architecture/0.5.4-storage-audio`  
**Protected baseline:** `0.5.4`

## Gate 0 — Source and baseline verification

Before changing application code:

- Import or otherwise identify the exact 0.5.4 source tree.
- Record the archive SHA-256 and verify archive integrity.
- Record the baseline commit and source version.
- Run the existing test suite without modifying the baseline.
- Inventory every current read/write path for preferences, favorites, recents, progress, and playback state.
- Inventory the current audio element, source selection, event handling, service worker, and cache behavior.

**Exit condition:** exact baseline identity and a reproducible baseline test result are recorded.

## Workstream A — Local storage

### A1. Storage audit and model

Separate and document the data domains:

- Preferences and interface settings.
- Favorites and saved items.
- Recent listening history.
- Program/session progress.
- Playback queue and resume position.
- Downloaded-media metadata and integrity state.

Do not migrate blindly. Select the persistence mechanism after inspecting the actual 0.5.4 code and data shapes. IndexedDB is the leading candidate for structured records and media metadata; small, non-critical preferences may remain in a simpler store if that is demonstrably safer.

### A2. Reliability

Implement and test:

- Versioned schema and explicit migrations.
- Atomic writes where supported by the chosen store.
- Validation of records read from storage.
- Graceful handling of quota errors, unavailable storage, and corrupt records.
- Idempotent migration and safe retry after interrupted migration.
- No silent deletion or reset on parse/storage errors.

### A3. User-controlled recovery

Define local export/import for user data. Validate imported data before applying it. Provide an encrypted export option for personal data; keep keys and recovery instructions under user control. Do not add cloud backup or account sync as a hidden substitute.

## Workstream B — Audio engine

### B1. Playback state model

Use one authoritative playback state model for:

- Idle, loading, playing, paused, ended, and error states.
- Current item, current source, duration, and playback position.
- Queue and next/previous behavior.
- Resume position and completion updates.

UI controls must reflect actual media events rather than optimistic button state.

### B2. Playback behavior

Implement and verify:

- Play, pause, seek, and resume.
- Restore last position after app restart.
- Correct handling of source changes and language changes.
- Audio focus interruptions, phone calls, headphone disconnects, and output changes where the platform exposes those events.
- Background and lock-screen controls on supported iOS versions/devices.
- Clear error handling for missing, truncated, unsupported, or unreadable media.

Use platform-native browser audio capabilities first. Do not introduce a third-party playback API or remote streaming dependency into the core.

### B3. Offline media

- Play bundled or explicitly downloaded local media without network access.
- Track download state and file integrity locally.
- Never treat an external source URL as a required playback dependency after a licensed asset is available locally.
- Do not expose unapproved or rights-unverified media in the catalogue.

## Verification matrix

| Area | Required evidence |
|---|---|
| Baseline | Existing 0.5.4 tests pass unchanged |
| Persistence | Data survives reload and app restart |
| Migration | Old records migrate once without loss |
| Recovery | Export validates and can be restored |
| Corruption | Invalid records fail safely; no silent wipe |
| Offline | Local catalogue and media work with network disabled |
| Playback | Controls follow native media events |
| Resume | Position restores within an agreed tolerance |
| Interruptions | Playback state recovers correctly after interruption |
| iOS background | Tested on a physical iPad/iPhone; no simulator-only claim |
| Regression | Existing features and translations remain intact |

## Release gate

Do not merge into `main` or replace 0.5.4 until:

1. All automated tests pass.
2. Storage migration and recovery tests pass.
3. Offline tests pass.
4. Physical iOS playback/background tests pass.
5. A QA report records device, OS version, test results, known limitations, and candidate version.

A passing static check is not proof of real iOS background playback.


## Gate 0 results — 2026-11-18

Gate 0 is complete for the recovered source archive:

- Exact SHA-256 matched the digest expected by the existing source-import workflow.
- ZIP integrity passed.
- Application version file reports `0.5.4`.
- Existing Node smoke suite: 27 passed, 0 failed.
- Detailed findings are recorded in `docs/qa/BASELINE-0.5.4-VERIFICATION.md`.

### Confirmed implementation baseline

- Storage is currently synchronous `localStorage`; IndexedDB, schema migrations, export/import, and explicit corruption recovery are absent.
- Audio uses one HTMLAudioElement and three local WAV files.
- Playback position is not persisted.
- Media Session metadata/actions are not implemented.
- Physical iOS background and Lock Screen behavior remain unverified.

The next implementation task is a storage adapter with explicit initialization and migration while preserving current UI call semantics. Audio resume persistence and Media Session support follow after storage reliability is established.

**No application source files have been changed.**
