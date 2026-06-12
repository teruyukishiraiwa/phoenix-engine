# Browser Support

Phoenix Engine v1.1 is a browser-local media application. Browser support depends on Web Audio, AudioWorklet, WebAssembly, PixiJS rendering, and video export capabilities.

## Primary Targets

- Chrome desktop: primary target.
- Edge desktop: primary target.

## Best-Effort Targets

- Firefox desktop: basic app behavior is expected, but video export behavior may differ.
- Safari desktop: best-effort until physical-device verification is recorded.

## Not Guaranteed in v1.1

- iOS Safari is not included in the guaranteed support scope.
- Long-form video export is not formally guaranteed.

## Feature Notes

- WAV export depends primarily on Web Audio and OfflineAudioContext.
- GPU video export depends on WebCodecs support.
- CPU video export fallback depends on local FFmpeg WebAssembly runtime and available browser memory.
- Hardware acceleration should remain enabled for smooth Scena preview and analyzer visuals.
