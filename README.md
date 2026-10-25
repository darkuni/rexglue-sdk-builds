# ReXGlue SDK builds

Prebuilt [ReXGlue SDK](https://github.com/rexglue/rexglue-sdk) packages for the darkuni Xbox 360 static-recompilation projects. The game repos download these instead of compiling the SDK on every new project.

| Release | Asset |
|---|---|
| `sdk-v0.9.0` | `rexglue-sdk-v0.9.0-win-amd64-release.zip` (Windows x64, Release, clang, Tracy off) |

To build another SDK version: **Actions → Build ReXGlue SDK → Run workflow**, enter the tag.

Contains no game code or game data. ReXGlue is BSD-3-Clause (portions derived from Xenia, BSD); see `share/licenses` inside each package.
