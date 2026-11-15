# Launcher integration references

Primary source inspected 2026-11-14. Lunaris interoperates with installed launchers; no launcher source, binaries, icons or branding are copied into Lunaris. Download links go to official project releases.

## Windows

| Launcher | Launch home / settings | Discovery | Flag file |
| --- | --- | --- | --- |
| Bloxstrap | `-player` / `-settings` | HKCU or HKLM `Software\Microsoft\Windows\CurrentVersion\Uninstall\Bloxstrap`, `InstallLocation`; default `%LOCALAPPDATA%\Bloxstrap\Bloxstrap.exe` | `<install root>\Modifications\ClientSettings\ClientAppSettings.json` |
| Fishstrap | `-player` / `-settings` | Same uninstall-key convention with `Fishstrap`; default `%LOCALAPPDATA%\Fishstrap\Fishstrap.exe` | `<install root>\Modifications\ClientSettings\ClientAppSettings.json` |
| Froststrap | `-player` / `-settings` | Uninstall key, then `%LOCALAPPDATA%\Froststrap\current\Froststrap.exe` and legacy `%LOCALAPPDATA%\Froststrap\Froststrap.exe` | Current layout: `%APPDATA%\Froststrap\Modifications\ClientSettings\ClientAppSettings.json`. Existing legacy layouts are detected. |
| Roblox | Exact installed `RobloxPlayerBeta.exe`, no home arguments | Uninstall location or newest existing player under `%LOCALAPPDATA%\Roblox\Versions\version-*` | That player directory's `ClientSettings\ClientAppSettings.json` |

All three bootstrappers accept a `roblox:` or `roblox-player:` URI as the first argument. Lunaris constructs `roblox://experiences/start?placeId=<positive decimal ID>` and passes it as one argument to the exact selected application. Current Roblox player itself receives the same URI directly, as in Bloxstrap's launch implementation. No shell command string, default protocol handler lookup, or registry writes are used.

Froststrap 2.x uses `--player` and `--settings`, and its compatibility shim maps the older single-hyphen forms to those options. The latest implementation separates its install root and roaming configuration root. Older releases have also used `<install root>\ClientSettings`; Lunaris prefers this file only when it already exists and a modern layout was not detected. Custom paths are supported; unknown applications do not receive guessed flag configuration locations.

- [Bloxstrap argument parser](https://github.com/bloxstraplabs/bloxstrap/blob/main/Bloxstrap/LaunchSettings.cs)
- [Bloxstrap install discovery](https://github.com/bloxstraplabs/bloxstrap/blob/main/Bloxstrap/App.xaml.cs)
- [Bloxstrap paths](https://github.com/bloxstraplabs/bloxstrap/blob/main/Bloxstrap/Paths.cs)
- [Bloxstrap Roblox launch implementation](https://github.com/bloxstraplabs/bloxstrap/blob/main/Bloxstrap/Bootstrapper.cs)
- [Fishstrap argument parser](https://github.com/fishstrap/fishstrap/blob/main/Bloxstrap/LaunchSettings.cs)
- [Fishstrap flag manager](https://github.com/fishstrap/fishstrap/blob/main/Bloxstrap/FastFlagManager.cs)
- [Fishstrap install discovery](https://github.com/fishstrap/fishstrap/blob/main/Bloxstrap/App.xaml.cs)
- [Froststrap current arguments](https://github.com/Froststrap/Froststrap/blob/main/Froststrap/Cli/FroststrapCliCommand.cs)
- [Froststrap legacy argument compatibility](https://github.com/Froststrap/Froststrap/blob/main/Froststrap/Cli/LegacyArgs.cs)
- [Froststrap current paths](https://github.com/Froststrap/Froststrap/blob/main/Froststrap.Core/Paths.cs)
- [Froststrap flag manager](https://github.com/Froststrap/Froststrap/blob/main/Froststrap/FastFlagManager.cs)

## macOS

Lunaris discovers `/Applications` and `~/Applications` bundles for Roblox, AppleBlox and Froststrap. It uses `/usr/bin/open -a <exact bundle>` and adds a validated game URI if specified. AppleBlox home Play sends its supported `appleblox://launch` shortcut; opening AppleBlox settings omits that shortcut. AppleBlox owns its launch-time flag configuration: its launch code rewrites the selected Roblox bundle's `Contents/MacOS/ClientSettings/ClientAppSettings.json`. Lunaris therefore does not claim direct writes to that file persist through AppleBlox launch. Froststrap's shared flags live at `~/Library/Application Support/Froststrap/Modifications/ClientSettings/ClientAppSettings.json`.

- [AppleBlox flag writer](https://github.com/AppleBlox/appleblox/blob/main/frontend/src/windows/main/ts/roblox/fflags.ts)
- [AppleBlox installation selection](https://github.com/AppleBlox/appleblox/blob/main/frontend/src/windows/main/ts/roblox/path-manager.ts)
- [AppleBlox launch shortcut](https://github.com/AppleBlox/appleblox/blob/980ea714ddb8908ed8b390411f89c01d1bca20f6/frontend/src/windows/main/ts/roblox/utils.ts#L110-L113)
- [Froststrap platform paths](https://github.com/Froststrap/Froststrap/blob/main/Froststrap.Core/Paths.cs)

Launch plans and discovery layouts are fixture-tested; native launcher update/game flows and macOS execution require separate installed-app verification.

## Roblox FastFlag scope

Local `ClientAppSettings.json` flags are subject to Roblox's allowlist. Unsupported flags can be retained in a user profile for portability but do not become effective merely because a launcher writes them. Runtime memory modification has a separate compatibility and enforcement risk; a successful file write is not evidence of an in-game effect.

- [Roblox local FastFlag allowlist announcement](https://devforum.roblox.com/t/allowlist-for-local-client-configuration-via-fast-flags/3966569)
- [Roblox staff clarification on memory modification](https://devforum.roblox.com/t/allowlist-for-local-client-configuration-via-fast-flags/3966569/271)
