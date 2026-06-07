# Scena Technical Overview

Scena is the Phoenix Engine motion artwork and video export surface. It combines metadata, cover art, visual effects, audio timing, and browser-local rendering into a release-ready visual presentation.

This document is a public technical overview. It explains behavior and architecture at a product level. It does not publish application source code or hidden internal effect details.

## 1. Overview

Scena handles:

- Song metadata layout.
- Cover artwork presentation.
- Template-based visual scene design.
- Backgrounds, overlays, particles, and opening/fade behavior.
- Audio-synchronized preview behavior.
- Video export using the current visual scene and mastered audio.

The canonical scene is designed around a 1920 x 1080 composition and scales from that base for export.

## 2. For Music Creators

Scena is designed for the visual presentation stage of a musical work.

It can combine:

- Cover art.
- Track and artist metadata.
- Motion backgrounds.
- Particle and overlay effects.
- Audio-reactive or timing-aware visual behavior.
- Finalis-mastered audio for video export.

The goal is not to replace a full video editing suite. The goal is to provide a focused motion artwork environment for music releases.

## 3. Visual Scene Model

A Scena scene can be understood as layered composition:

```text
Base frame
  -> Background
  -> Template layout
  -> Typography
  -> Particles / special effects
  -> Overlays
  -> Opening / fade behavior
  -> Export frame capture
```

For visual understanding, the scene can also be grouped into five practical layers:

| Layer | Contains | Purpose |
|-------|----------|---------|
| Foundation | Base frame, cover-derived background, gradients. | Establishes the visual atmosphere. |
| Layout | Template structure, artwork placement, metadata. | Defines how the music identity is presented. |
| Motion | Background movement, particles, audio-reactive timing. | Adds time-based energy and musical motion. |
| Finish | Overlays, fades, opening behavior, visual polish. | Creates the final cinematic surface. |
| Capture | Export frame capture and muxing. | Turns the browser scene into a deliverable video. |

The implementation uses a fixed design space so preview and export can share the same visual language.

## 4. Templates and Effects

Phoenix Engine v1.0 includes several template concepts:

| Template | Role |
|----------|------|
| Phoenix | Cinematic base layout. |
| Minimal | Typography-focused layout. |
| Classic | Artwork-forward classic presentation. |
| Scena | Signature Phoenix Engine scene style. |

Scena also includes visual effect modes such as Scena Galaxy, particle systems, overlays, opening effects, and background motion.

Some special visual behaviors are intentionally not documented in detail because they are part of the proprietary creative implementation.

## 5. Rendering Technology

Scena uses PixiJS for browser rendering. PixiJS provides GPU-accelerated canvas rendering suitable for layered visual scenes and responsive preview.

Hardware acceleration should remain enabled. Without hardware acceleration, preview smoothness and export behavior can degrade.

The visual composition is browser-local. It does not require server-side video rendering for normal use.

## 6. Audio Coupling

Scena can use audio-related context to drive visual behavior:

- Current playback time.
- Decoded audio buffer information.
- Analyzer data.
- Visual impact timing.
- Finalis-mastered audio for video export.

This coupling lets Scena align motion artwork with the musical structure while keeping the audio processing responsibility in Finalis.

## 7. Video Export

Scena video export has two public paths.

| Path | When Used | Requirement | Tradeoff |
|------|-----------|-------------|----------|
| GPU / WebCodecs | Preferred when browser encoder support is available. | WebCodecs support and suitable browser behavior. | Faster and more direct, but browser support varies. |
| CPU fallback | Used when WebCodecs is missing, unsuitable, or explicitly selected. | Frame capture plus local FFmpeg.wasm. | Broader compatibility, but slower and memory-sensitive. |

### GPU / WebCodecs Path

The preferred path uses browser WebCodecs when the required encoder features are available.

### CPU Fallback Path

The fallback path captures frames and uses local FFmpeg WebAssembly runtime for assembly and muxing. It is slower, but it provides an important compatibility path when WebCodecs is missing or unsuitable.

Both paths are browser-local and use the same local `/ffmpeg` runtime for muxing.

## 8. FFmpeg and Hosting Requirements

Scena video export uses a local-only FFmpeg runtime:

```text
/ffmpeg/ffmpeg-core.js
/ffmpeg/ffmpeg-core.wasm
/ffmpeg/ffmpeg-core.worker.js
```

No external FFmpeg CDN fallback is implemented in the public v1.0 release.

The host must also serve these public asset groups correctly:

- `/assets`
- `/img`
- `/worklets`
- `/wasm`
- `/ffmpeg`

Static assets must be available on the same origin and served with correct MIME types.

## 9. Browser and Performance Notes

Scena relies on:

- GPU-accelerated browser rendering.
- WebCodecs for the preferred video path.
- FFmpeg.wasm for muxing and CPU fallback export.
- Available browser memory for decoded audio, frame capture, and temporary export buffers.

Chrome and Edge desktop are the primary expected release targets. Firefox and Safari are best-effort until more release data is recorded. Long-form video export memory behavior is not formally guaranteed in v1.0.

## 10. Current Limitations

- Scena is not a general-purpose nonlinear video editor.
- Export is browser-local and memory-sensitive.
- CPU fallback export can be slow.
- iOS Safari is not currently included in the guaranteed support scope.
- Social preview validation depends on Basic authentication being removed from the public site.

## 11. Related Documents

- [Architecture Overview](./architecture-overview.md)
- [Export Guide](./export-guide.md)
- [Browser Support](./browser-support.md)
- [Known Issues](./known-issues.md)
