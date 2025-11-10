# HTML Kiosk Video Player

A single-file, browser-based kiosk video player with two modes: Loop and Thumbnail and configurable audio options. Designed for gallery/installations and unattended displays.

## Features

- Two modes:
  - Loop Mode: continuous video playback.
  - Thumbnail Mode: shows an image; first mouse move starts one playthrough, then returns to the image.
- Audio modes:
  - Mute (always), Manual unmute (per playthrough overlay), Unmute (always).
- Fullscreen-first experience with keyboard and mouse controls.
- Minimal UI (toolbar) that’s hidden by default; shown in Edit mode.

## Quick Start

1. Put your image and video files in the same folder as `videoplayer.html`.
2. Open `videoplayer.html` in a modern browser, or host it on a simple web server.
3. Press `E` to enter Edit mode; use the toolbar to switch modes and audio.
4. Press `F` to toggle Fullscreen mode.

## Configuration

Edit the constants at the top of the `<script>` block to point to your assets and defaults:

```js
const THUMBNAIL_PATH = "image.jpg"; 		// image path
const VIDEO_PATH = "video.mp4";				// video path
const DEFAULT_MODE = "loop";				// "loop" | "thumbnail"
const DEFAULT_AUDIO_MODE = "manual";		// "mute" | "manual" | "unmute"
```

Alternatively the thumbnail image and video can be loaded via Drag&Drop in the Edit mode. **Note:** File-URLs will not be stored in Local- or SessionStorage and discarded on reload.

## Controls

- Keyboard:
  - `E`: Toggle Edit mode (shows/hides toolbar and hint).
  - `F`: Toggle fullscreen.
- Mouse:
  - Double-click anywhere: Toggle fullscreen.
  - In Thumbnail Mode: first mouse move starts the video.
  - Unmute overlay (Manual mode only): click “Click to Unmute” to enable audio for the current playthrough.

## Behavior Details

- Loop Mode:
  - Video plays to end and immediately restarts.
  - In Manual audio mode, the unmute choice resets at each loop.
- Thumbnail Mode:
  - Shows the image until user moves the mouse; then plays the video once and returns to the image.
  - A short “autoplay suppression” window prevents accidental restarts immediately after toggling modes.
- Fullscreen:
  - The app requests fullscreen on image load and when video plays.
  - Some browsers require a user gesture to enter fullscreen.

## Browser Compatibility Notes

- Modern Chrome, Edge, Firefox, and Safari are supported.
- Autoplay with sound:
  - Browsers often block it without a prior user gesture. Use Manual mode (click overlay) or Unmute after interacting.

## Troubleshooting

- Video doesn’t play with sound:
  - This is likely autoplay policy. Use Manual audio mode and click the overlay, or interact (click/dblclick) before switching to Unmute.
- Fullscreen denied:
  - Provide a user gesture (double-click or press F).
- Video replays unexpectedly in Thumbnail Mode:
  - Mouse movement triggers playback. Ensure the cursor/device isn’t generating stray movements.
- Unmute-Overlay not visible:
  - It only appears when: Audio = Manual, video is on-screen, and not in Edit mode.

## File Structure

- `videoplayer.html` — self-contained app (HTML/CSS/JS). Place your media next to it or update the paths in the constants.
