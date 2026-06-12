# Export Guide

Phoenix Engine provides browser-local export paths for audio and video.

## WAV Export

Finalis WAV export renders the current mastering chain in the browser and downloads a local WAV file.

In v1.1, a Chiaroscuro-enabled export stops with an explicit error if the requested WebAssembly processing cannot initialize. When Chiaroscuro is disabled, export does not require that module.

Recommended checks:

- Confirm local audio playback first.
- Review final export analysis after export.
- Check true peak and sample peak against the selected delivery profile.

## Video Export

Scena video export uses the visual scene plus mastered audio.

### GPU / WebCodecs Path

This is the preferred path when the browser supports the required WebCodecs features.

### CPU Fallback Path

CPU-only export captures frames and uses the local FFmpeg WebAssembly runtime for assembly and muxing. It is slower, but it is retained for compatibility.

## Practical Limits

For v1.1, keep initial export tests short. Long-form export memory behavior is still under review and is not a formal guarantee.

## FFmpeg

Phoenix Engine uses a local `/ffmpeg` runtime. The app does not fall back to an external FFmpeg CDN.
