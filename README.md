# AUDIOVIZOR

Real-time audio visualizer. Runs in the browser and as an Electron desktop app, turning
audio into GPU-rendered visuals that react to what's actually playing.

**[audiovizor.com](https://audiovizor.com)** · [Web app](https://audiovizor.com/app) · [Download for Windows](https://github.com/connorl953/audiovizor-releases/releases)

This repository hosts the release binaries and issue tracker. The application source is
private.

## What it does

- **16 built-in visual presets**, each a distinct scene with its own shader work
- **Adaptive quality scaling** across five tiers, so the renderer degrades rather than
  stutters on slower hardware
- **Video export** that re-renders offline rather than screen-capturing the preview
- **Beat-reactive** transitions and accents
- **Auto-update** on the desktop build

## How it works

**The visuals are shader work.** Roughly 1,200 lines of GLSL across dedicated shader files,
plus inline shader code in the scene components, running through three.js. The presets are
original compositions rather than ports — the one substantial borrowed piece is a
well-known simplex noise implementation, which carries its original attribution in the
source.

**Audio drives the shaders rather than accompanying them.** An FFT decomposes the incoming
signal into frequency bands, and those bands are bound to shader uniforms, so amplitude and
spectral distribution modulate the visuals frame by frame.

**The desktop build visualizes system audio.** It captures whatever the machine is playing —
any application, any source — through Electron's loopback audio capture, so there is no
virtual cable to install and no routing to configure. The web build uses microphone or tab
audio, within the limits the browser allows.

**Export is a separate offline render.** Rather than recording the live preview, the
exporter precomputes per-frame audio features for the whole track and re-renders each frame
deterministically. Output is therefore clean regardless of what the display was doing, and
identical run to run. Resolution and frame rate are configurable.

**Beat detection comes in two forms,** and they are not the same quality. The offline
analyzer used for export is a real onset-detection pipeline — spectral flux, autocorrelation
for tempo, and adaptive peak picking. The live analyzer used during playback is a much
simpler adaptive amplitude threshold. Exported video tracks the beat more accurately than
the live preview does.

## Download

Grab the latest installer from the
[Releases](https://github.com/connorl953/audiovizor-releases/releases) page.

**Windows:** download the `.exe` installer and run it. The app updates itself when new
versions ship.

**Browser:** no install — open the [web app](https://audiovizor.com/app).

## Requirements

| | |
|---|---|
| **GPU** | Any WebGL2-capable GPU. A discrete GPU gives the best results at the highest quality tier; integrated graphics are supported and drop to a lower tier automatically. |
| **Browser** | WebGL2 support required |
| **Desktop** | Windows 10/11 |

The renderer measures its own frame rate and steps down through five quality tiers rather
than dropping frames, so lower-end hardware gets a lower-fidelity render instead of a
stuttering one.

## Tiers

The free tier runs all presets with a 15-minute session limit and exports at 720p with a
watermark. Paid tiers remove the session limit, remove the watermark, raise the export
resolution ceiling, and enable live audio input and saved presets. Current pricing is on
[audiovizor.com](https://audiovizor.com).

## Links

- [Website](https://audiovizor.com)
- [Web app](https://audiovizor.com/app)
- [Releases](https://github.com/connorl953/audiovizor-releases/releases)
