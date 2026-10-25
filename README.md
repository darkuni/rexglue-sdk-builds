# ReXGlue SDK builds

Prebuilt [ReXGlue SDK](https://github.com/rexglue/rexglue-sdk) packages for the darkuni Xbox 360 static-recompilation projects. The game repos download these instead of compiling the SDK on every new project.

| Release | Asset |
|---|---|
| `sdk-v0.9.0` | `rexglue-sdk-v0.9.0-win-amd64-release.zip` - stock v0.9.0 (Windows x64, Release, clang, Tracy off) |
| `sdk-v0.9.0-p1` | `rexglue-sdk-v0.9.0-p1-win-amd64-release.zip` - v0.9.0 + `patches/0001` |
| `sdk-v0.9.0-p2` | `rexglue-sdk-v0.9.0-p2-win-amd64-release.zip` - v0.9.0 + earlier XMA patches (superseded) |
| `sdk-v0.9.0-p3` | `rexglue-sdk-v0.9.0-p3-win-amd64-release.zip` - v0.9.0 + XMA decoder from xenia-canary |

## Patches
`patches/*.patch` are applied in name order on top of the upstream tag. Bump `PATCH_LEVEL` in the workflow when they change.

- `0001-xma-decoder-from-xenia-canary-451f915.patch` - replaces the XMA decode path (Work, Decode, Consume, packet/frame walking, buffer swap, loop handling, output ring setup, context write-back) with xenia-canary's `xma_context_new.cc` at commit 451f915 (2026-10-24), adapted to ReXGlue. Matches Xenia in never flushing the FFmpeg decoder on context clear/release; `xma_flush_decoder_on_release=true` restores the SDK's flush on release. Supersedes the p1/p2 patches (their fixes are included). Target: periodic clicking in OutRun Online Arcade races.

To build another SDK version: **Actions → Build ReXGlue SDK → Run workflow**, enter the tag.

Contains no game code or game data. ReXGlue is BSD-3-Clause (portions derived from Xenia, BSD); see `share/licenses` inside each package.
