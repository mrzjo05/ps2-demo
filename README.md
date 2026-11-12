# PS2 demo — iToF × stereo RGB (Lichtblick web)

**View:** https://mrzjo05.github.io/ps2-demo/

Plays a sensor recording (MCAP) in Lichtblick running in the browser. Nothing to install.

- Press ▶ at the bottom to play (loop playback is on).
- **Live** tab: the two stereo cameras, iToF depth, a sync table on the shared PTP timebase, IMU and microphone plots, and events.
- **3D Cloud** tab: the stereo RGB point cloud and the iToF point cloud (cyan) in one frame. Drag with the left button to rotate, the right button to pan, and scroll to zoom.
- Microphone audio plays only after you press "Enable sound" in the audio panel (browser policy).
- Chrome or Edge is recommended (H.264 is decoded with WebCodecs).

## Contents

| Path | What it is |
|---|---|
| `index.html` | Entry page — a header (logo, telelian.com link) above `app/`, which it opens with the recording and layout |
| `assets/telelian-logo.png` | Logo |
| `app/` | Lichtblick web build |
| `app/extensions/` | Extensions loaded at startup: Cloudini (decompresses point clouds) and the demo panels (sync table, events, audio) |
| `data/` | Recording (MCAP, about 10 s). Point clouds are Cloudini-compressed at 5 mm. GitHub Pages serves this file gzipped, which breaks Range requests, so the app reads it from raw.githubusercontent.com. Log times were rewritten to the sensor exposure stamps, so video, point clouds and iToF change together for the same instant (iToF depth is paired with the camera frame closest in exposure). |
| `layouts/PS2-Demo-v4.json` | Panel layout |

## Source and licenses

- **Lichtblick** (MPL-2.0): based on https://github.com/lichtblick-suite/lichtblick v1.29.1. The modified source is branch `hsb/1.29.1-web-demo` of https://github.com/mrzjo05/lichtblick (46a5baed = `hsb/1.29.1-hsb.3` c091044d + `source/lichtblick-bundled-extensions.patch`), built with `yarn web:build:prod`.
  - Changes: a read-only loader for `.foxe` files served next to the app, dark theme by default, a 1-byte Range probe for servers that do not expose Accept-Ranges (raw.githubusercontent.com), and waiting up to 100 ms (instead of 10 ms) for a decoded H.264 frame so video does not fall behind with hardware decoders.
  - Full license text: `LICENSES/lichtblick.MPL-2.0.txt`.
- **Cloudini Foxglove converter extension**: extension code MIT (`LICENSES/cloudini-foxglove-cloudini-converter.MIT.txt`), the bundled Cloudini library Apache-2.0 (`LICENSES/cloudini.Apache-2.0.txt`). Source: https://github.com/facontidavide/cloudini/releases/tag/1.3.1
- **Demo panel extension (`hsb-panels-*.foxe`) and the recording**: Telelian. Published only for viewing this demo.
