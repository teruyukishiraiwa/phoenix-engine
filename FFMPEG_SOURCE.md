# FFmpeg Core Source Information

Phoenix Engine v1.0 distributes a fixed-source single-thread FFmpeg WebAssembly runtime for browser video muxing and CPU fallback export.

## Distributed Runtime

- Build repository: `teruyukishiraiwa/phoenix-engine-ffmpeg-build`
- Workflow run: `26951274975`
- License: `GPL-2.0-or-later`
- Public runtime path: `/ffmpeg/`
- Integrity record: `/ffmpeg/manifest.json`

Runtime files:

| File | Bytes | SHA-256 |
|------|------:|---------|
| `ffmpeg-core.js` | 261807 | `2d4e4b575fe838006b07befb6dbc6a09038aa8cece2ad74cfe99f7c2e0e64d83` |
| `ffmpeg-core.wasm` | 36514015 | `bc217747b9422f0fc6afccb26296ad1327c363a2063fc18450a737304cd151d7` |
| `ffmpeg-core.worker.js` | 222 | `f6a68426aabf7c3d7252f558f34802098a1991b9349800dad376dd3cf45db72c` |

## Source Input Bundle

Phoenix Engine retains an offline source-input bundle containing the ffmpeg.wasm build repository plus FFmpeg and linked-library source archives resolved to immutable commits.

```text
ffmpeg-complete-source-inputs-2026-06-04T11-36-02-752Z.tar.gz
SHA-256: 9996dbf388a762116c4b478fef5be3c9d361c0323c0eee62bf4a352de334968f
```

The exact repositories, commits, licenses, archive sizes, and SHA-256 hashes are recorded in the source manifest distributed with the public site:

```text
/source/ffmpeg-source-manifest.json
```

## Upstream Snapshot

Phoenix Engine also retains the upstream ffmpeg.wasm release source archive:

```text
ffmpeg.wasm-v12.15-source.tar.gz
SHA-256: 930f51b2dc882da0810151b386eecdea12ac173aaf1b9dccc1d77d8dea02fb20
```

Upstream release:

<https://github.com/ffmpegwasm/ffmpeg.wasm/releases/tag/v12.15>

## Build Image

The Emscripten build image used for the fixed-source build is:

```text
emscripten/emsdk:3.1.40@sha256:c1e807a6e03ac5bd5b37bae2ace3c46c08579e2ddeb951037a3b8dac7067f2cc
```

## Verification Status

The fixed-source FFmpeg runtime was verified against the generated manifest and passed a browser CPU-export regression test using H.264 video and AAC audio.
