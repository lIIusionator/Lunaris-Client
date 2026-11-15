# Lunaris Client 0.16.0

## Fixed

- Separate successful offset loading from an unavailable optional prefix list. Startup reports the address count and source version; a prefix-list 404 does not imply the offsets failed to load.
- Restore the AHK offset method's bare-name lookup, module-base-plus-RVA addressing, and value-based encoding. Both original fetch URLs are unchanged.
- Preserve bare flag names beginning with `Int` during lookup instead of incorrectly stripping those letters. Standard `DFInt`, `SFInt`, and `FInt` aliases still resolve normally.
- Remove the fixed Roblox-build lock. Singleton discovers and validates the running registry instead of requiring a specific executable hash and address table.

## Changed

- Add a result for every requested flag and finish each batch with applied/requested, already-matching/requested, skipped, batch-error, unattempted, and cancelled totals.
- Make logs a readable monospace text preview with expand/collapse controls.
- Rename Access to Settings, with Credits and License buttons.
- Add animated button hover feedback and an injecting/waiting indicator, with reduced-motion support.
- Clear proven obsolete update caches after upgrading. Active/newer downloads, failed-update recovery files, user profiles, and settings are retained; locked caches can be retried later.
- Include updated credits and the proprietary binary-use notice in Settings and the distribution packages. New core development is kept local; the public channel carries release downloads and documentation.
- Keep sorting and pacing around both methods: general flags first, then graphics, textures, and lighting; 50 ms between writes and 300 ms between categories or batches of 25 writes.
- Apply and Undo always use pacing, including when an older settings file disabled it.
- Keep original-value capture, process-lifetime checks, write readback, cancellation, and conflict-aware Undo.

## Verification

- Live Windows x64 test: Singleton, hybrid, and direct Offsets each wrote and read back three flags (FPS, Air responsiveness, and a boolean), then immediately restored all three originals. Hybrid confirmed all three fetched addresses were used. The temporary client was closed.
- Four native previews checked at the minimum 800 × 600 window size: compact logs, expanded logs, Settings, and the injecting indicator.
- Final local GNU Windows automated suite: **97 passed, 0 failed**, with one separate opt-in live test filtered out. Coverage includes the bare-`Int` name regression, every-flag reporting, final totals, read-only log selection, long log retention, hover interpolation, reduced motion, byte-width Undo, updater rollback, and cache cleanup. The earlier three-method live check above is separate from this final automated run.

## Packages and compatibility

Local Windows x64 GNU/MinGW artifacts include Setup, the portable ZIP, and the
raw executable/checksum used by the in-app updater. Package versions, SHA-256
sidecars, ZIP contents, and isolated native startup were checked. Installer
installation/uninstallation was not smoke-tested for this release.
No 0.16.0 MSVC artifact has been built.

No macOS 0.16.0 archive has been built or native-tested yet. The shared frontend
remains an unsigned preview; the legacy macOS live-memory, signing,
virtual-display, and AppleBlox-preparation backend has not been ported. Linux
has no 0.16.0 build and remains reserved for a future release.

Live methods depend on the current registry layout or offset feed. Missing or incompatible targets remain skipped. Readback tests do not establish gameplay effects or long-session stability. Lunaris does not install or replace Roblox.
