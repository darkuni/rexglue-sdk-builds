# ReXGlue SDK builds

Prebuilt [ReXGlue SDK](https://github.com/rexglue/rexglue-sdk) packages for the darkuni Xbox 360 static-recompilation projects. The game repos download these instead of compiling the SDK on every new project.

| Release | Asset |
|---|---|
| `sdk-v0.9.0` | `rexglue-sdk-v0.9.0-win-amd64-release.zip` - stock v0.9.0 (Windows x64, Release, clang, Tracy off) |
| `sdk-v0.9.0-p1` | `rexglue-sdk-v0.9.0-p1-win-amd64-release.zip` - v0.9.0 + `patches/0001` |
| `sdk-v0.9.0-p2` | `rexglue-sdk-v0.9.0-p2-win-amd64-release.zip` - v0.9.0 + earlier XMA patches (superseded) |
| `sdk-v0.9.0-p3` | `rexglue-sdk-v0.9.0-p3-win-amd64-release.zip` - v0.9.0 + XMA decoder from xenia-canary (didn't help; archived) |
| `sdk-v0.9.0-p4` | `rexglue-sdk-v0.9.0-p4-win-amd64-release.zip` - stock v0.9.0 decoder + `xma_trace` diagnostics only |

## Patches
`patches/*.patch` are applied in name order on top of the upstream tag (`patches/archive/` is not applied). Bump `PATCH_LEVEL` in the workflow when they change.

- `0001-xma-trace-loop-config.patch` - diagnostics only, no behaviour change. `xma_trace=true` logs each XMA context's buffers and loop registers when they change, every loop jump taken, and any loop_end that falls inside a frame (a loop the decoder will miss).

Archived: the xenia-canary decoder swap (p3) and the p1/p2 fixes did not change OutRun's race clicking. An offline harness running the stock decoder on OutRun's engine loop (`ICS_116`) showed the clip loops seamlessly via the loop registers (loop_start=32, loop_end=39729, subframe_end=3, skip=4) but gains a silent padding frame per pass when replayed without them.

To build another SDK version: **Actions → Build ReXGlue SDK → Run workflow**, enter the tag.

Contains no game code or game data. ReXGlue is BSD-3-Clause (portions derived from Xenia, BSD); see `share/licenses` inside each package.
