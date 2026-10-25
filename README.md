# ReXGlue SDK builds

Prebuilt [ReXGlue SDK](https://github.com/rexglue/rexglue-sdk) packages for the darkuni Xbox 360 static-recompilation projects. The game repos download these instead of compiling the SDK on every new project.

| Release | Asset |
|---|---|
| `sdk-v0.9.0` | `rexglue-sdk-v0.9.0-win-amd64-release.zip` - stock v0.9.0 (Windows x64, Release, clang, Tracy off) |
| `sdk-v0.9.0-p1` | `rexglue-sdk-v0.9.0-p1-win-amd64-release.zip` - v0.9.0 + `patches/0001` |
| `sdk-v0.9.0-p2` | `rexglue-sdk-v0.9.0-p2-win-amd64-release.zip` - v0.9.0 + `patches/0001`-`0002` |

## Patches
`patches/*.patch` are applied in name order on top of the upstream tag. Bump `PATCH_LEVEL` in the workflow when they change.

- `0001-xma-port-canary-decoder-fixes.patch` - ports four xenia-canary XMA fixes (aee0871 split frame header counted, 6bef1fb drain partial frame, 7015473 sub-stream skip chain, 2372a54 sample rounding). Did not fix OutRun's clicks on its own.
- `0002-xma-keep-decoder-state-on-clear-and-trace.patch` - clearing an XMA context no longer flushes the FFmpeg decoder (matches Xenia; the SDK's flush clicked whenever a game cleared/refilled a context, e.g. OutRun every 0.384 s). `xma_flush_decoder_on_clear=true` restores the old behaviour; `xma_trace=true` logs context clear/release/swap/loop events.

To build another SDK version: **Actions → Build ReXGlue SDK → Run workflow**, enter the tag.

Contains no game code or game data. ReXGlue is BSD-3-Clause (portions derived from Xenia, BSD); see `share/licenses` inside each package.
