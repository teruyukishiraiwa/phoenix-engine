# Phoenix Engine v1.0 Release Notes

Release date: **June 8, 2026 (JST)**

Official site: <https://phxengine.static.jp/>

## Overview

Phoenix Engine v1.0 introduces an integrated browser-local workflow for motion artwork and precision audio finishing.

## Scena

- 1920x1080 canonical visual scene design.
- Phoenix, Minimal, Classic, and Scena templates.
- Scena Galaxy visual effect mode.
- Background, overlay, opening effect, and particle controls.
- Browser-local video export with GPU/WebCodecs preferred path.
- CPU-only video export fallback using local FFmpeg WebAssembly runtime.

## Finalis

- Local audio import and browser-based playback.
- Input trim, Chroma, Prism, Apex, and Ether processing chain.
- Precision Spectrum, stereo scope, input and output metering.
- Oracle local reference comparison and custom references.
- WAV export and final export analysis.
- Finalis preset import/export.

## Public Release Notes

- FFmpeg uses a same-origin local bundle only.
- External FFmpeg CDN fallback is not used.
- Public YouTube URL analysis is disabled.
- CPU fallback remains available for video export compatibility.
- Safari is best-effort until physical-device verification is recorded.
