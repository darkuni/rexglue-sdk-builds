# ReXGlue SDK builds

Prebuilt [ReXGlue SDK](https://github.com/rexglue/rexglue-sdk) packages for the darkuni Xbox 360 static-recompilation projects. The game repos download these instead of compiling the SDK on every new project.

| Release | Asset |
|---|---|
| `sdk-v0.9.0` | `rexglue-sdk-v0.9.0-win-amd64-release.zip` - stock v0.9.0 (Windows x64, Release, clang, Tracy off) |
| `sdk-v0.9.0-p1` | `rexglue-sdk-v0.9.0-p1-win-amd64-release.zip` - v0.9.0 + `patches/0001` |
| `sdk-v0.9.0-p2` | `rexglue-sdk-v0.9.0-p2-win-amd64-release.zip` - v0.9.0 + earlier XMA patches (superseded) |
| `sdk-v0.9.0-p3` | `rexglue-sdk-v0.9.0-p3-win-amd64-release.zip` - v0.9.0 + XMA decoder from xenia-canary (didn't help; archived) |
| `sdk-v0.9.0-p4` | `rexglue-sdk-v0.9.0-p4-win-amd64-release.zip` - stock v0.9.0 decoder + `xma_trace` diagnostics only |
| `sdk-v0.9.0-p5` | `rexglue-sdk-v0.9.0-p5-win-amd64-release.zip` - **XMA stream start/end skip honoured** (fixes OutRun's race clicking) + `xma_trace` |

## Patches
`patches/*.patch` are applied in name order on top of the upstream tag; `*.ffmpeg.patch` files apply inside the `thirdparty/FFmpeg` submodule. `patches/archive/` is not applied. Bump `PATCH_LEVEL` in the workflow when they change.

- `0001-xma-stream-skip-and-trace.patch` - XMA contexts drop the encoder-delay / end-padding samples flagged in each frame header (start/end skip), as the console's XMA hardware does (`xma_honor_stream_skip`, default on). Plus `xma_trace` diagnostics.
- `0002-wmapro-export-xma-stream-skip.ffmpeg.patch` - FFmpeg's WMA Pro/XMA decoder parsed those start/end skip fields and discarded them ("no idea what these are for"); it now exports them as frame metadata (`xma_start_skip`, `xma_end_skip`).

### Why
OutRun Online Arcade loops its engine sound (`ICS_116`, 25 encoded frames) by re-submitting the same XMA buffer. Frame 0 carries start skip = 512 (one whole warm-up frame). Ignoring it made every pass 12,800 samples with a 133-sample silent gap instead of a seamless 12,288 - a click every 0.384 s during races, in Xenia too. Verified with an offline harness driving `XmaContext` directly: with the fix each pass is exactly 12,288 samples, no gaps, seams within normal sample-to-sample variation.

Archived (`patches/archive/`): xenia-canary decoder swap (p3), no effect on the clicking.

To build another SDK version: **Actions → Build ReXGlue SDK → Run workflow**, enter the tag.

Contains no game code or game data. ReXGlue is BSD-3-Clause (portions derived from Xenia, BSD); see `share/licenses` inside each package.
