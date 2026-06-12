# Changelog

## v1.1.0 - Unreleased

### User-Facing Changes

- Prevent indefinite waits when Chiaroscuro WebAssembly cannot be loaded or initialized.
- Keep realtime playback available through a visible degraded-mode fallback.
- Stop Chiaroscuro-enabled audio export with an explicit error when the requested processing cannot initialize.
- Allow Chiaroscuro-disabled audio export to proceed without loading its WebAssembly module.
- Show the saved or loaded Phoenix Engine project name as the Finalis session title.
- Keep the Finalis preset name as the session fallback only when no named project is active.

### Engineering and Release Changes

- Separate production-only social assets from the public application runtime.
- Repair dynamic DSP benchmark parameter delivery and deterministic failure reporting.
- Add reproducible release assembly with allowlisted operational files and SHA-256 verification.
- Normalize product version reporting to Phoenix Engine v1.1 / SemVer 1.1.0.

## v1.0.0 - 2026-06-08 JST

Initial public release of Phoenix Engine.

### Included

- Scena motion artwork surface.
- Finalis precision audio finishing surface.
- Local audio import and browser-based playback.
- Precision Spectrum, stereo scope, loudness and peak metering.
- WAV export with final export analysis.
- Browser-local video export with GPU/WebCodecs preferred path.
- CPU-only video export fallback using local FFmpeg WebAssembly runtime.
- Local-only FFmpeg bundle; no external FFmpeg CDN fallback.
- Public YouTube URL analysis disabled.
- Open Graph, X/Twitter Card, favicon, and release metadata.

### Release Notes

The release target is the site root at <https://phxengine.static.jp/>.
