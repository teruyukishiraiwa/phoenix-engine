# Known Issues

This document tracks known limitations for Phoenix Engine v1.1.

## Browser Compatibility

- Safari desktop support is best-effort until physical-device verification is recorded.
- iOS Safari is not currently part of the guaranteed support scope.
- Firefox behavior should be validated separately, especially around video export.

## Video Export

- Long-form export memory behavior is not formally guaranteed.
- CPU-only video export can be slow because it runs in the browser and uses FFmpeg WebAssembly.
- GPU export depends on browser WebCodecs support and may fall back to CPU export.

## Support

If you encounter an issue, include browser version, operating system, reproduction steps, and whether the issue occurs with a short local audio file.
