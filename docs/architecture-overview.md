# Phoenix Engine Architecture Overview

Phoenix Engine is a browser-based environment for motion artwork and precision audio finishing.

Initial public release: **June 8, 2026 (JST)**

Current documented version: **v1.1.0 (unreleased)**

Official site: <https://phxengine.static.jp/>

Phoenix Engine is proprietary software. This repository documents public product behavior, release information, support guidance, and third-party notices. It does not publish application source code.

## 1. Product Model

Phoenix Engine v1.1 is organized around two integrated surfaces.

| Surface | Role |
|---------|------|
| **Scena** | Motion artwork, visual scene design, preview, and video export. |
| **Finalis** | Browser-local audio finishing, metering, reference comparison, WAV export, and final export analysis. |

A Phoenix Engine project can preserve Scena and Finalis state together. The audio file itself is not embedded in the project file, so the user may need to relink the original local audio file when reopening a saved project.

In Finalis, the active project name is the primary session identity. When no named project is active, the current Finalis preset name is used as a fallback. The source filename remains a separate value.

## 2. System Flow

The product can be understood as a browser-local finishing and presentation pipeline.

```text
Local audio + artwork + metadata
          |
          v
+---------------------+       +----------------------+
| Finalis             |       | Scena                |
| audio finishing     |       | motion artwork       |
| metering            |       | visual scene design  |
| reference checks    |       | preview              |
+----------+----------+       +----------+-----------+
           |                             |
           | mastered audio context      | visual scene frames
           +-------------+---------------+
                         |
                         v
              WAV export / video export
```

For music creators, this means the same project can move from audio finishing to visual presentation without leaving the browser. For engineers, this means the app depends on browser media capabilities rather than a server-side rendering or mastering backend.

## 3. For Music Creators

Phoenix Engine is intended to support the final presentation stage of a musical work.

- Scena turns track metadata, artwork, and motion design into a visual scene for video-ready presentation.
- Finalis provides local audio finishing, metering, reference comparison, and export checks.
- The two surfaces can work together so a video export can use a mastered audio buffer while preserving the visual identity of the work.

The app is not a DAW, multitrack editor, recorder, or cloud mastering service. It is designed as a browser-local environment for finishing and presenting a musical release.

## 4. Browser-Local Processing

Phoenix Engine is designed around local browser processing.

- Local audio files are selected by the user.
- Playback, metering, DSP, WAV export, preview, and browser-local video export run in the browser.
- Phoenix Engine v1.1 does not require uploading local audio to a Phoenix Engine server for normal use.
- Public YouTube URL analysis is disabled.
- The public app does not call the previously audited Cobalt API for YouTube reference analysis.

## 5. Technology Stack

Phoenix Engine uses modern browser media technologies.

| Technology | Main Area | Role |
|------------|-----------|------|
| React | App shell | Application UI and state orchestration. |
| Web Audio API | Finalis / export | Audio playback, routing, metering, and offline rendering. |
| AudioWorklet | Finalis | Realtime audio processing and analyzer streams. |
| WebAssembly | Finalis / export | Selected DSP and FFmpeg runtime components. |
| PixiJS | Scena | GPU-accelerated visual scene rendering. |
| WebCodecs | Scena export | Preferred path for browser-local video encoding when available. |
| FFmpeg.wasm | Video export | Local browser muxing and CPU fallback video export. |

A simplified dependency map is:

```text
Finalis: Web Audio -> AudioWorklet -> WASM-assisted processing -> WAV export
Scena:   PixiJS -> frame capture / WebCodecs -> FFmpeg.wasm muxing -> video export
Shared:  browser storage -> project / preset state
```

## 6. Export Architecture

Phoenix Engine provides browser-local export paths.

| Export | Primary Owner | Browser Technology | Output |
|--------|---------------|--------------------|--------|
| WAV export | Finalis | OfflineAudioContext / WAV encoding | Audio file |
| GPU video export | Scena | PixiJS / WebCodecs / FFmpeg.wasm | Video file |
| CPU video fallback | Scena | Frame capture / FFmpeg.wasm | Video file |

### WAV Export

Finalis can render the current audio finishing chain in the browser and download a WAV file. Final Export Analysis then reports loudness, peak, and safety information for the exported audio.

### Video Export

Scena video export uses the current visual scene and mastered audio.

- The preferred video path uses WebCodecs when supported by the browser.
- The CPU fallback path captures frames and assembles video through FFmpeg.wasm.
- Both video paths rely on the local `/ffmpeg` runtime for muxing.

## 7. Public Deployment Requirements

The public app expects static assets to be served from the same origin.

Required same-origin paths include:

- `/assets`
- `/img`
- `/worklets`
- `/wasm`
- `/ffmpeg`

The host must serve JavaScript and WebAssembly with correct MIME types. Static files must be served directly before any single-page-app fallback rewrite.

HTTPS is expected for the public release.

## 8. FFmpeg Runtime and Transparency

Phoenix Engine v1.1 uses a local-only FFmpeg WebAssembly runtime. It does not fall back to an external FFmpeg CDN.

Runtime hashes and source information are documented in:

- [FFmpeg Source Information](../FFMPEG_SOURCE.md)
- [Third-Party Notices](../THIRD_PARTY_NOTICES.md)

The public FFmpeg runtime is expected to match `/ffmpeg/manifest.json` on the official site.

## 9. Current Limitations

- Chrome and Edge desktop are the primary expected release targets.
- Firefox and Safari are best-effort until more release data is recorded.
- iOS Safari is not included in the guaranteed support scope for v1.1.
- Long-form video export memory behavior is not formally guaranteed.

## 10. Reading Order

For more detail:

- [Finalis Technical Overview](./finalis-technical-overview.md)
- [Scena Technical Overview](./scena-technical-overview.md)
- [Browser Support](./browser-support.md)
- [Export Guide](./export-guide.md)
- [Known Issues](./known-issues.md)
