# Phoenix Engine Third-Party Notices

## FFmpeg WebAssembly Core

Phoenix Engine distributes a fixed-source browser FFmpeg WebAssembly runtime.

- Build repository: `teruyukishiraiwa/phoenix-engine-ffmpeg-build`
- License: `GPL-2.0-or-later`
- Runtime files: `/ffmpeg/ffmpeg-core.js`, `/ffmpeg/ffmpeg-core.wasm`, and `/ffmpeg/ffmpeg-core.worker.js`

The exact file sizes and SHA-256 hashes are recorded in `/ffmpeg/manifest.json` on the public site and summarized in `FFMPEG_SOURCE.md`.

Project repository:

<https://github.com/ffmpegwasm/ffmpeg.wasm>

GNU General Public License version 2:

<https://www.gnu.org/licenses/old-licenses/gpl-2.0.html>

## FFmpeg Browser Wrapper

Phoenix Engine also uses `@ffmpeg/ffmpeg` and `@ffmpeg/util`, which declare the MIT license. These wrapper packages are bundled into the Phoenix Engine application JavaScript.

Project repository:

<https://github.com/ffmpegwasm/ffmpeg.wasm>

## Other Browser Libraries

Phoenix Engine uses browser UI, rendering, and media libraries including React, PixiJS, Three.js, html-to-image, mp4-muxer, Framer Motion, and related tooling. These dependencies retain their respective upstream licenses.
