# AP-XR.Studio

**Hand Gesture Voxel Editor** — Build 3D sculptures with your bare hands in the browser.

---

## ✨ Features

- **Hand Gesture Control** — Uses MediaPipe AI for real-time hand tracking via webcam
- **Voxel Building** — Place and erase 3D voxels on a grid using natural gestures
- **AR Background Mode** — Remove the scene background and place voxels in your live camera feed
- **6 Camera Views** — ISO, Front, Back, Left, Right, Top with smooth transitions
- **7 Colors** — Cycle through a curated palette using gestures or UI swatches
- **Screenshot & Video Recording** — Capture your creations directly to an in-app gallery
- **Mouse / Touch Support** — Full fallback controls without camera
- **100-step Undo** — Never lose your work
- **Zero dependencies to install** — Pure HTML/CSS/JS, loads Three.js and MediaPipe from CDN

---

## 🤟 Gesture Reference

| Gesture | Action |
|---|---|
| ☝️ POINT | Move the ghost voxel cursor |
| 🤌 PINCH | Place or erase a voxel |
| ✊ FIST + drag | Orbit the camera |
| ✌️ PEACE (hold 0.9s) | Cycle color |
| 🤟 THREE (hold 0.9s) | Toggle Build / Erase mode |
| 🖐 PALM (hold 0.9s) | Next camera view |
| 🤙 PINKY (hold 0.9s) | Undo last action |

---

## ⌨️ Keyboard Shortcuts

| Key | Action |
|---|---|
| `A` | Build mode |
| `D` | Erase mode |
| `H` | Start hand-cam |
| `Z` | Undo |
| `V` | Next view |
| `F` | Flip camera (front ↔ back) |
| `B` | Toggle AR background |
| `R` | Start / stop recording |
| `S` | Save screenshot |
| `G` | Open gallery |
| `M` | Load demo sculpture |
| `C` | Clear all voxels |
| `Esc` | Close gallery |

---

## 📁 Project Structure

```
ap-xr-studio/
├── index.html      ← Entire app (self-contained)
└── README.md       ← This file
```

---

## 🔧 Tech Stack

| Library | Version | Purpose |
|---|---|---|
| [Three.js](https://threejs.org) | r128 | 3D rendering |
| [MediaPipe Hands](https://mediapipe.dev) | 0.4.1675469240 (pinned) | Hand landmark detection |
| [MediaPipe Camera Utils](https://mediapipe.dev) | 0.3.1675466862 (pinned) | Webcam management |
| [MediaPipe Drawing Utils](https://mediapipe.dev) | 0.3.1675466124 (pinned) | Hand skeleton overlay |
| [JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono) | — | UI font |
| [Bebas Neue](https://fonts.google.com/specimen/Bebas+Neue) | — | Display font |

All runtime libraries load from CDN by exact pinned version — no bundler, and still no app-side `package.json`. The `package.json` in this repo is dev-only (runs the test suite below) and is never loaded by the browser.

---

## 🔒 Privacy

- Camera feed is processed **entirely in the browser** using on-device AI
- No video data is ever uploaded to any server
- No analytics, no tracking, no cookies

---

## 🧪 Tests

`gesture.js` — the code that turns 21 MediaPipe hand landmarks into a named
gesture (PINCH / FIST / POINT / PEACE / THREE / PALM / PINKY) — is a pure
function with no DOM or Three.js dependency, extracted from the page's
inline script into its own file so the *exact* code the browser runs is also
unit-tested in Node:

```bash
npm test
```

**12 tests**, including the finger-up/down threshold with its jitter margin,
every named gesture, the pinch-distance threshold, and a check that every
possible finger-combination returns a defined gesture string rather than
`undefined` (which would otherwise crash the `GICONS[g]` lookup used for the
on-screen gesture icon). `car.js`-equivalent heavier logic — Three.js scene
setup, voxel placement, recording — isn't unit tested here; it's exercised by
running the app.

## 🔧 Fixes in this pass

- **CDN scripts were unpinned** (Three.js was already pinned to r128, but
  MediaPipe's 3 scripts — and the model file URL in `locateFile`— were not).
  All pinned now, so a future MediaPipe release can't silently change
  hand-tracking behavior underneath you.
- **Minor material leak on voxel removal**: each voxel's dark edge outline
  is a child `LineSegments` with its own cloned material (correct — needed
  so disposing one voxel's material doesn't break others sharing the same
  color). That child material was never disposed when the voxel was removed
  (undo, erase, clear-all, and the demo-rebuild all go through this path).
  Fixed to dispose it alongside the parent mesh's material.
- **Stale comment removed**: a leftover comment claimed the `#bm` (DEMO)
  button had been "removed" in favor of `#bgal`; both buttons actually exist
  and are correctly wired — the comment was just confusing, not a bug.
- **`gesture.js` extracted** from the inline script so gesture classification
  has test coverage (see above) instead of being unverified beyond manual
  testing.

### Intentionally left as-is

`user-scalable=no` is still in the viewport meta tag. On the other vanilla-JS
projects in this portfolio that was a pure accessibility regression and got
removed; here it's load-bearing — the canvas has its own two-finger pinch
handler (`touchstart`/`touchmove` with `e.touches.length === 2`) for zooming
the 3D camera, and letting the browser's native pinch-to-zoom-the-page fire
at the same time would fight that gesture. Worth revisiting with a more
surgical fix (e.g. `touch-action: none` scoped tightly enough to keep page
zoom everywhere else) if this becomes a real accessibility complaint.

## 📄 License

MIT — free to use, modify, and deploy.

---

*Built with Three.js + MediaPipe · AP-XR.Studio*
