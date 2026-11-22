# apps

A small collection of web apps that run entirely in the browser and can be installed as PWAs.

Live: https://jeonghyoan.github.io/apps/

## Apps

| App | What it does |
| --- | --- |
| [audio-note](./audio-note/) | Free audio transcription & summaries via Groq free API (PWA) |
| [clean-pdf](./clean-pdf/) | Ad-free PDF viewer that opens files on your device only (PWA) |

## audio-note

Free audio transcription & summaries via Groq free API (PWA).

- Transcribes several recordings at once with Groq Whisper (`whisper-large-v3-turbo` by default, `whisper-large-v3` for accuracy).
- Every transcript line carries a `[MM:SS]` timestamp from Whisper's segment data, so a note can be checked against the recording.
- Turns each transcript into one "notes" tab next to the transcript: general notes, meeting notes or class notes. Long transcripts are summarized section by section and the sections are joined as they are (no lossy re-compression), and anything misheard or unclear is collected once at the end under "다시 들어볼 구간" with its timestamp.
- Multiple API keys can be added. A per-minute 429 keeps the selected model, retrying on another key or after a short wait before it falls back to the lighter model. Keys stay in the browser's `localStorage` and go only to the Groq API.
- Works offline as an installed app shell, in light or dark mode.

Open: https://jeonghyoan.github.io/apps/audio-note/

Bring your own Groq API key from https://console.groq.com/keys.

## clean-pdf

Ad-free PDF viewer that opens files on your device only (PWA).

- Opens local PDFs in the browser; files are read on the device and never uploaded.
- Continuous scroll or single page, table of contents, thumbnails, text search with highlights, text selection, zoom, rotation, and dark mode.
- Tools: images to PDF, PDF to images, merge, extract or reorder pages, compress, page numbers, watermark, sign or draw, sticky notes, and unlocking password-protected PDFs.
- Recent documents are kept on the device and reopen from the home menu; works offline once installed.

Open: https://jeonghyoan.github.io/apps/clean-pdf/

## Structure

```
index.html            app launcher
audio-note/
  index.html          the app (single file)
  manifest.json       PWA manifest
  sw.js               offline cache (never caches Groq API calls)
  icon-*.png          app icons
clean-pdf/
  index.html          the app (single file)
  manifest.json       PWA manifest
  sw.js               offline cache
  pdf*.js             PDF engine, bundled locally
  icon-*.png          app icons
```

## Local use

Serve the folder over HTTP, for example:

```
python3 -m http.server 8000
```

Then open http://localhost:8000/. Service workers need `http://localhost` or https.

## License

MIT
