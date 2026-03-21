# AP-XR.Studio


█████╗ ██████╗       ██╗  ██╗██████╗    ███████╗████████╗██╗   ██╗██████╗ ██╗ ██████╗
██╔══██╗██╔══██╗      ╚██╗██╔╝██╔══██╗   ██╔════╝╚══██╔══╝██║   ██║██╔══██╗██║██╔═══██╗
███████║██████╔╝       ╚███╔╝ ██████╔╝   ███████╗   ██║   ██║   ██║██║  ██║██║██║   ██║
██╔══██║██╔═══╝        ██╔██╗ ██╔══██╗   ╚════██║   ██║   ██║   ██║██║  ██║██║██║   ██║
██║  ██║██║           ██╔╝ ██╗██║  ██║   ███████║   ██║   ╚██████╔╝██████╔╝██║╚██████╔╝
╚═╝  ╚═╝╚═╝           ╚═╝  ╚═╝╚═╝  ╚═╝   ╚══════╝   ╚═╝    ╚═════╝ ╚═════╝ ╚═╝ ╚═════╝


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
| [MediaPipe Hands](https://mediapipe.dev) | latest | Hand landmark detection |
| [MediaPipe Camera Utils](https://mediapipe.dev) | latest | Webcam management |
| [MediaPipe Drawing Utils](https://mediapipe.dev) | latest | Hand skeleton overlay |
| [JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono) | — | UI font |
| [Bebas Neue](https://fonts.google.com/specimen/Bebas+Neue) | — | Display font |

All libraries loaded from CDN — no `package.json`, no bundler.

---

## 🔒 Privacy

- Camera feed is processed **entirely in the browser** using on-device AI
- No video data is ever uploaded to any server
- No analytics, no tracking, no cookies

---

## 📄 License

MIT — free to use, modify, and deploy.

---

*Built with Three.js + MediaPipe · AP-XR.Studio*