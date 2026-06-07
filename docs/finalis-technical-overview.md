# Finalis Technical Overview

Finalis is the Phoenix Engine audio finishing surface. It is designed for browser-local mastering decisions, realtime monitoring, WAV export, and final export analysis.

This document is a public technical overview. It explains behavior and architecture at a product level. It does not publish application source code or detailed DSP implementation formulas.

## 1. Overview

Finalis handles:

- Local audio import and browser-based playback.
- Realtime audio processing.
- Input and output metering.
- Spectrum and stereo field monitoring.
- Local reference comparison.
- WAV export.
- Final Export Analysis.
- Finalis preset storage and import/export.

Finalis is intended to support listening and verification. It is not positioned as a fully automatic mastering replacement.

## 2. For Music Creators

Finalis helps answer practical release questions:

- Is the input level appropriate before processing?
- Is the low end focused and controlled?
- Is the spectrum balanced against a useful reference?
- Is the stereo field coherent?
- Is the limiter controlling peaks without hiding important musical motion?
- Does the exported WAV satisfy the selected delivery profile?

The interface combines listening controls, meters, spectral views, and final export analysis so decisions can be made with both ears and measurement feedback.

## 3. Signal Flow Concept

The Finalis signal flow can be understood as:

```text
Input
  -> Input metering
  -> Chroma
  -> Prism
  -> Apex
  -> Ether
  -> Analysis / monitoring
  -> Output
```

This diagram is conceptual. It is intended to explain the public behavior rather than expose implementation internals.

## 4. Processing Stages and Listening Meaning

| Stage | Technical Role | What the Creator Listens / Watches For |
|-------|----------------|------------------------------------------|
| Input metering | Confirms level after input trim. | Whether the source is entering the chain too quietly or too hot. |
| Chroma | Target-guided spectral dynamics. | Whether broad tonal contour is moving toward the intended reference character. |
| Prism | Low-end, stereo focus, tilt, and spectral contour control. | Weight, center stability, low-end width, and tonal posture. |
| Apex | Nonlinear clipping and density control. | Loudness density, transient shape, and whether clipping remains musical. |
| Ether | Final limiting and delivery metering. | Peak safety, gain reduction behavior, loudness, and stereo correlation. |
| Analysis / monitoring | Spectrum, stereo, loudness, and final export checks. | Whether decisions survive measurement and rendered-file verification. |

## 5. Processing Modules

### Chroma

Chroma is a target-guided spectral dynamics stage. It can use Oracle target curves or custom reference data to help shape broad spectral balance without treating the goal as a generic flat response.

### Prism

Prism focuses on low-end control, stereo focus, tilt, air, and spectral contour shaping. It is intended to help the user judge weight, center stability, and tonal contour.

### Apex

Apex is a nonlinear clipping and density-control stage. It is designed to increase usable level and density while giving the user control over clipping character and protection behavior.

### Ether

Ether is the final limiting and monitoring stage. It handles lookahead limiting, ceiling behavior, loudness-related telemetry, true peak awareness, gain reduction, and correlation information.

### Oracle

Oracle provides reference comparison using local factory targets and user-created custom references. Public YouTube URL analysis is disabled in v1.0, and the public app does not use the previously audited Cobalt API.

## 6. Metering and Analysis

Finalis includes several monitoring layers.

| Feature | Purpose |
|---------|---------|
| Input Meter | Shows peak level after input trim and before the processing chain. |
| Loudness / Peak metering | Supports level and delivery decisions. |
| Precision Spectrum | Shows mix, mid, and side spectral behavior. |
| Stereo Scope | Helps judge width and phase behavior. |
| Final Export Analysis | Verifies the exported WAV after rendering. |

Final Export Analysis is important because it checks the rendered output, not just the realtime monitoring state.

## 7. Realtime Monitoring vs Final Export Analysis

| Area | Realtime Monitoring | Final Export Analysis |
|------|---------------------|-----------------------|
| Timing | During playback and adjustment. | After rendered export. |
| Purpose | Decision support while listening. | Verification of the actual exported file. |
| Typical use | Adjust tone, density, width, and safety margin. | Confirm loudness, true peak, sample peak, and hotspot timing. |
| Risk it reduces | Mixing or mastering blind spots during playback. | Assuming realtime meters exactly represent the delivered file. |

For release decisions, realtime monitoring should guide adjustments, while Final Export Analysis should confirm the rendered result.

## 8. Export and Quality

Finalis WAV export uses offline browser rendering. The export path is designed to use a higher quality mode than realtime preview when appropriate.

Publicly relevant quality concepts:

- Realtime preview is optimized for responsive monitoring.
- Realtime high quality raises processing quality while preserving interactivity.
- Export high quality is used for offline rendering.

Delivery profiles help interpret exported audio safety:

| Profile | Intended meaning |
|---------|------------------|
| Transparent | Minimal policy constraint. |
| Streaming Safe | Conservative codec-safe target. |
| Aggressive | Higher-density target with less conservative margin. |

## 9. Browser Technologies

Finalis depends on:

- Web Audio API for playback, routing, and rendering.
- AudioWorklet for realtime processing and analyzer streams.
- OfflineAudioContext for WAV export rendering.
- WebAssembly for selected processing components.
- Browser storage for presets and local configuration.

These requirements make modern desktop browsers the primary target for v1.0.

## 10. Privacy and Local Processing

Local audio files are selected by the user and processed in the browser. Finalis does not require uploading local audio to a Phoenix Engine server for normal playback, analysis, or WAV export.

Public YouTube URL analysis is disabled. No Cobalt API request is part of the public Finalis runtime.

## 11. Presets and Project State

Finalis presets store mastering-related settings, reference information, and export-related state. Phoenix Engine project files are broader: they preserve Scena and Finalis state together, but they do not embed the audio file itself.

This separation allows a user to reuse Finalis settings while keeping full project state as a separate concept.

## 12. Current Limitations

- Finalis is single-source audio oriented.
- It is not a DAW, multitrack editor, recorder, or cloud mastering service.
- Long-form export memory behavior is not formally guaranteed.
- Safari support is best-effort until physical-device verification is recorded.
- Browser performance depends heavily on CPU single-thread behavior for realtime audio work.

## 13. Related Documents

- [Architecture Overview](./architecture-overview.md)
- [Export Guide](./export-guide.md)
- [Browser Support](./browser-support.md)
- [Known Issues](./known-issues.md)
