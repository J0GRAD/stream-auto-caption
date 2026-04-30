# stream auto caption

Automated script to layer a real time caption overlay over a livestream.

Built with the Web Speech API for near-zero latency. No server, installations, or dependencies required. Minimal single HTML file setup for OBS.

---

## Setup

### 1. Grant microphone access

Open `index.html` in Chrome at least once and allow microphone access when prompted. This only needs to be done once.

### 2. Add to OBS

- In OBS, add a new **Browser Source**
- Check **Local file** and point it to `index.html`
- Check **Allow transparency**
- Set width/height to match your canvas resolution (e.g. 1920x1080)
- Freely position the source over your scene

---

## Configuration

All tweakable settings are at the top of `index.html` inside the `CONFIG` block. Do not edit anything below it.

| Variable            | Default                                          | Description                                                                 |
| ------------------- | ------------------------------------------------ | --------------------------------------------------------------------------- |
| `INACTIVITY_TIMER`  | `3`                                              | Seconds of silence before the display clears                                |
| `CHAR_LIMIT`        | `80`                                             | Character threshold for a forced line reset                                 |
| `FINAL_CLEAR_DELAY` | `0`                                              | Seconds to hold text after a phrase finalizes before clearing (0 = instant) |
| `FONT_SIZE`         | `'36px'`                                         | Size of the caption text                                                    |
| `FONT_FAMILY`       | `'Helvetica Neue', Helvetica, Arial, sans-serif` | Font stack                                                                  |
| `FONT_WEIGHT`       | `500`                                            | Font weight                                                                 |
| `TEXT_COLOR`        | `'#FFD700'`                                      | Caption text color                                                          |
| `OUTLINE_COLOR`     | `'#000000'`                                      | Text outline color                                                          |
| `OUTLINE_WEIGHT`    | `1.5`                                            | Text outline thickness in px                                                |
| `POSITION_BOTTOM`   | `'60px'`                                         | Distance from the bottom of the screen                                      |
| `LETTER_SPACING`    | `'0.02em'`                                       | Letter spacing                                                              |

---

## How it works

- Captions render instantly from interim speech results; display does not wait for a phrase to finalize
- When a phrase finalizes, the line clears after `FINAL_CLEAR_DELAY` seconds
- If a phrase runs long without a natural break, `CHAR_LIMIT` forces a reset
- If you stop speaking, `INACTIVITY_TIMER` clears the display after the set number of seconds
- Recognition restarts automatically if it drops, no manual intervention needed

---

## Requirements

- **Chrome** (or any Chromium-based browser) — Web Speech API is not supported in Firefox or Safari
- OBS Studio with Browser Source support

---

## Planned features

- Volume-based dynamic styling — whisper for quiet speech, all caps for loud
- Speaker diarization
