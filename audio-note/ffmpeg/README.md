# ffmpeg bundle (vendored)

Unmodified npm build files, served from this folder so the app never loads code from a CDN.
They are used only when a recording needs splitting before transcription.

| File | Comes from | License |
| --- | --- | --- |
| `ffmpeg.js`, `814.ffmpeg.js` | `@ffmpeg/ffmpeg@0.12.15` → `dist/umd/` | MIT |
| `ffmpeg-core.js`, `ffmpeg-core.wasm` | `@ffmpeg/core@0.12.10` → `dist/umd/` (single-thread) | GPL-2.0-or-later |

The single-thread core is used on purpose: GitHub Pages cannot send the
`Cross-Origin-Opener-Policy` / `Cross-Origin-Embedder-Policy` headers that
`SharedArrayBuffer` and the multi-thread core (`@ffmpeg/core-mt`) need.

- `ffmpeg.js` loads its worker chunk `814.ffmpeg.js` from the same folder
  (webpack public path resolves next to the script), and the app passes
  absolute URLs for `coreURL` / `wasmURL`.
- The wasm file is ~32 MB. It is not precached by `sw.js`; the browser caches it
  on first use instead (runtime cache), so installing the PWA stays small.
