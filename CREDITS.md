# Credits

Lunaris Client is maintained by [lIIusionator](https://github.com/lIIusionator).

## Method references

- **YURI / YuriHub** — the user-provided YURI 2.2.0 executable informed the Windows singleton signature, hash-table lookup, and original-value handling. [YuriHub](https://github.com/lIIusionator/YuriHub)
- **FFlags injector.ahk** — the user-provided AutoHotkey script informed direct offset lookup, value encoding, and the original fetch URLs. Its source did not identify an author.
- **theo's offsets** — the supplied [FFlags header](https://imtheo.lol/Offsets/FFlags.hpp) provides the offset catalog.
- **Prefixes-FFlags** — the supplied [prefix list](https://github.com/soulukr78/Prefixes-FFlags) is an optional source of name suggestions.

Lunaris adds its own interface, profiles, launch integration, update system,
graphics-last chunks, pacing, per-flag reporting, and conflict-aware Undo.

## Interface and libraries

The application uses Rust, Iced, tiny-skia, Serde, reqwest, Tokio, rfd, image,
RustCrypto SHA-2, dirs, windows-sys, winreg, and winresource. Dependencies retain
their own licenses; Lunaris's project license does not replace them.

The moon icon and native interface were created for Lunaris.

## Launcher integrations

Thanks to the Bloxstrap, Fishstrap, Froststrap, and AppleBlox projects for their
launcher interfaces. Integration references and the source links used for those
interfaces are listed in
[`packaging/launcher-references.md`](https://github.com/lIIusionator/Lunaris-Client/blob/main/packaging/launcher-references.md).

Roblox is developed by Roblox Corporation. Lunaris is an independent project.
