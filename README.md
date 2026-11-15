<p align="center"><img src="assets/lunaris.png" width="96" alt="Lunaris moon icon"></p>
<h1 align="center">Lunaris Client</h1>
<p align="center">Your flags. Your launcher. One native desktop app.</p>

[**Download the latest release**](https://github.com/lIIusionator/Lunaris-Client/releases/latest)

Lunaris is a Roblox companion built with Rust and Iced. Manage profiles, switch
launchers, and apply supported Windows live flags from a compact native app.
No Chromium or HTML frontend is required.

The public channel contains downloads, documentation, credits, and release
notes. New application source and injection-core changes are developed locally
and are not included in the public release documentation bundle.

## Downloads

| Platform | Status |
| --- | --- |
| Windows x64 | 0.16.0: Setup, portable ZIP, and automatic updates |
| macOS ARM64 | No 0.16.0 build yet; the shared frontend remains an unsigned preview |
| Linux | Planned; no 0.16.0 build available |

Use Setup for a per-user installation, or extract the Windows ZIP and open
`Lunaris.exe`. See the [download page](https://github.com/lIIusionator/Lunaris-Client/releases/latest)
for release assets.

## What's in 0.16.0

- Full per-flag logs, with applied/requested, already-matching/requested,
  skipped, batch-error, unattempted, and cancelled totals at the end of every batch.
- Selectable monospace log previews with Expand, Collapse, Copy all, and Export.
- A Settings tab with Credits and License buttons.
- Smooth button hover feedback and an animated injecting/waiting indicator.
  Reduced motion is available.
- Offset-load success reported separately from optional prefix-list errors.
- Windows method checks based on the running client, without a fixed Roblox
  version allowlist.
- Graphics-last chunks and mandatory per-flag pacing for Apply and Undo.
- Cleanup of proven obsolete update caches while preserving profiles, settings,
  active downloads, and recovery backups.

See [release notes](CHANGELOG.md) for changes and verification limits.

## Verification

Local Windows validation passed **97 tests with 0 failures**; one opt-in live
test was filtered from that suite. A separate authorized live check exercised
Singleton, hybrid, and direct Offsets with three flags each and immediate Undo.
Four native minimum-size previews were checked. These results do not establish
gameplay effects or long-session stability.

The verified 0.16.0 Windows packages use GNU/MinGW. Package checks cover versions,
SHA-256 checksums, ZIP contents, and isolated native startup. No MSVC, macOS, or
Linux artifact was built for this version. The installer installation and
uninstallation flow was not smoke-tested.

## Quick start

1. Choose Fishstrap, Bloxstrap, Froststrap, Roblox, or a custom launcher in Roblox.
2. Import or paste flags, choose a preset, and review the saved values. Stack
   imports merges new values; disable it when you want to replace the list.
3. Open Roblox through your selected launcher, then use Check Roblox to see its
   process ID.
4. Choose the live method in Settings and press Apply live. Stop cancels between
   operations; Undo live restores changes that still match Lunaris's last write.
5. Open Logs for every requested flag's result and the final totals. Expand the
   preview for more room, or copy/export the session.

Saving flags for a later launch is separate from applying live values. Roblox
may ignore local flags outside its allowlist. Lunaris opens the installed client
and does not install, replace, or re-sign Roblox.

## Live methods

Singleton reads the running client's registry. Offsets loads addresses from the
same supplied AHK feed at startup and works independently of a Singleton scan.
Optional offset assistance uses fetched addresses checked against Singleton.

Both methods use sorted chunks, 50 ms between writes, and pauses between batches
or rendering categories. Missing or incompatible targets are logged and skipped;
removing a version allowlist does not guarantee every future Roblox layout.
Readback tests do not establish gameplay effects or long-session stability.

## Updates

Lunaris checks public releases and stages verified downloads. Restart when ready
to install an update. Version 0.15.1 or newer can use this update channel without
a GitHub login. Saved flags, profiles, and settings are preserved.

## License and credits

Official 0.16.0 binaries are free to use under the proprietary binary-use notice.
See [LICENSE](LICENSE) and [CREDITS.md](CREDITS.md), also linked from Settings.
Third-party components retain their own licenses.

[Report an issue](https://github.com/lIIusionator/Lunaris-Client/issues)
