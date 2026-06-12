# Phoenix Engine v1.1 Release Notes

Status: **Unreleased**

Official site: <https://phxengine.static.jp/>

## Overview

Phoenix Engine v1.1 is a stabilization release for the browser-local motion artwork and precision audio finishing workflow introduced in v1.0.

## Reliability

- Chiaroscuro WebAssembly initialization now has a bounded failure path.
- Realtime playback can continue with a visible degraded-mode fallback.
- Chiaroscuro-enabled export stops explicitly if the requested processing cannot initialize.
- Chiaroscuro-disabled export no longer waits for the Chiaroscuro WebAssembly module.

## Finalis Session Identity

- A saved or loaded Phoenix Engine project name is shown as the Finalis session title.
- A Finalis preset name remains the fallback when no named project is active.
- Source file identity remains separate from the project/session identity.
- Project and source names are masked from Microsoft Clarity session capture.

## Release Engineering

- Public runtime assets are assembled through a reproducible allowlisted process.
- The release manifest records SHA-256 hashes for every published file except the manifest itself.
- Production-only social assets are excluded from the application runtime.
- The fixed-source local FFmpeg runtime remains unchanged.

## Compatibility

- Chrome and Edge desktop remain the primary targets.
- Firefox and Safari desktop remain best-effort pending final regression records.
- iOS Safari is not included in the guaranteed v1.1 support scope.
- CPU video export fallback remains available through the local FFmpeg WebAssembly runtime.

## Previous Release

Phoenix Engine v1.0.0 was initially released on **June 8, 2026 (JST)**.
