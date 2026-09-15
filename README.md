# AUDIOVIZOR

Real-time audio visualizer. Runs in the browser and as a native Windows application, turning
live system audio into GPU-rendered visuals with no setup beyond pressing play.

**[audiovizor.com](https://audiovizor.com)** · [Web app](https://audiovizor.com/app) · [Download for Windows](https://github.com/connorl953/audiovizor-releases/releases)

This repository hosts the release binaries and issue tracker. The application source is private.

## What it does

- **15+ reactive presets** — distinct visual systems, each responding to a different aspect of
  the signal
- **Beat detection** driving transitions and accents in time with the music
- **1080p60 video export** for finished clips
- **Auto-update** on the Windows build

## How it works

The visual layer is a **GLSL shader pipeline targeting 144fps**, with every preset written as
fragment shader work so the CPU stays out of the render path.

Audio drives the shaders rather than merely accompanying them. A **Web Audio FFT** decomposes
the incoming signal into frequency bands, and those bands are bound directly to shader uniforms —
so amplitude, spectral distribution, and beat events modulate the visual parameters frame by
frame. What you see is a function of what is playing, not a loop timed to it.

On Windows, the native build captures system audio through **WASAPI loopback**, which taps the
audio device's render stream directly. That means it visualizes whatever the machine is playing —
any application, any source — with no virtual cable, no routing configuration, and no stereo-mix
device. The browser build visualizes microphone or tab audio within the limits the browser
permits.

Export renders at **1080p60** rather than capturing the live preview, so exported video is clean
regardless of what the display was doing during playback.

## Download

Grab the latest installer from the [Releases](https://github.com/connorl953/audiovizor-releases/releases)
page.

**Windows:** download the `.exe` installer and run it. The app updates itself when new versions
ship.

**Browser:** no install — open the [web app](https://audiovizor.com/app).

## System requirements

A **dedicated GPU is required.** The shader pipeline targets 144fps at full resolution, and
integrated graphics will not sustain it.

| | |
|---|---|
| **GPU** | Dedicated graphics — NVIDIA RTX series, Apple M-series, or equivalent |
| **OS** | Windows 10/11 for the native build; any modern browser for the web build |
| **Browser** | WebGL2 support required |

Lower-end hardware will run the web build at reduced frame rates.

## Links

- [Website](https://audiovizor.com)
- [Web app](https://audiovizor.com/app)
- [Releases](https://github.com/connorl953/audiovizor-releases/releases)
