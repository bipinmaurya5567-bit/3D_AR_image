# 🎾 Tennis Ball AR — Web Augmented Reality Experience

A lightweight, browser-based **Augmented Reality (AR)** web app that overlays an animated 3D tennis ball model onto a real-world image target — no app install required.

---

## 📸 Demo

> Point your phone camera at the tennis ball target image and watch the 3D model come to life — spinning in real time!

---

## 🗂️ Project Structure

```
3D image/
├── index.html           # Main application entry point (frontend)
├── Tennis ball.glb      # 3D tennis ball model (GLTF Binary format)
├── targets-boll.mind    # MindAR compiled image target file
└── README.md            # Project documentation
```

---

## 🛠️ Tech Stack

| Technology | Version | Role |
|---|---|---|
| [A-Frame](https://aframe.io/) | `1.4.0` | WebXR / 3D scene framework |
| [MindAR](https://hiukim.github.io/mind-ar-js-doc/) | `1.2.5` | Image-based AR tracking |
| GLTF / GLB | — | 3D model format for the tennis ball |
| HTML5 / CSS3 / Vanilla JS | — | UI, loading screen, hints |

> **No backend server is required.** This is a fully client-side application.

---

## ✨ Features

- 📷 **Image Target AR** — Detects a tennis ball image and anchors the 3D model on it
- 🌀 **3D Animation** — The model continuously rotates 360° on the Y-axis (3-second loop)
- ⏳ **Loading Screen** — Animated spinner shown while the AR engine initializes
- 💡 **On-screen Hint** — Displays a prompt guiding the user after the scene loads
- 📱 **Mobile Friendly** — Responsive viewport, optimized for smartphone cameras

---

## 🚀 Getting Started

### Prerequisites

- A modern mobile or desktop browser with **camera access** (Chrome, Safari, Firefox)
- No Node.js, no build tools, no installation required

### Running Locally

Since the app uses `fetch` for loading `.mind` and `.glb` assets, you need to serve it over HTTP (not `file://`).

**Option 1 — VS Code Live Server**
1. Install the [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) extension
2. Right-click `index.html` → **Open with Live Server**

**Option 2 — Python HTTP Server**
```bash
# Python 3
python -m http.server 8080
```
Then open `http://localhost:8080` in your browser.

**Option 3 — Node.js `serve`**
```bash
npx serve .
```

### Deploying to the Web

This project can be hosted on any static hosting provider:

| Platform | Command / Steps |
|---|---|
| [GitHub Pages](https://pages.github.com/) | Push to a `gh-pages` branch or enable Pages in Settings |
| [Netlify](https://netlify.com) | Drag & drop the project folder |
| [Vercel](https://vercel.com) | `npx vercel` from the project root |
| [Firebase Hosting](https://firebase.google.com/docs/hosting) | `firebase deploy` after init |

> ⚠️ **HTTPS is required** for camera access on mobile browsers. All platforms above provide free SSL.

---

## 🎯 How It Works

### 1. Image Target Detection
The file `targets-boll.mind` is a pre-compiled MindAR target descriptor created from a tennis ball reference image. When the camera detects this image, MindAR returns the 3D pose (position + orientation).

### 2. A-Frame Scene
An A-Frame scene is configured with the `mindar-image` component:
```html
<a-scene mindar-image="imageTargetSrc: ./targets-boll.mind; autoStart: true;">
```

### 3. 3D Model Anchoring
The GLB model is attached to `<a-entity mindar-image-target="targetIndex: 0">`, which pins the model to the detected target:
```html
<a-gltf-model
  src="#tennis-ball"
  position="0 0 0.1"
  scale="3 3 3"
  animation="property: rotation; to: 0 360 0; loop: true; dur: 3000; easing: linear"
/>
```

### 4. Loading & UX Flow
```
Page Load → AR Engine Initializes → 3s Fade Delay → Loading Screen Hides → Hint Appears
```

---

## 📁 Assets

| File | Description |
|---|---|
| `Tennis ball.glb` | Binary GLTF 3D model (~65 KB) of a tennis ball |
| `targets-boll.mind` | MindAR compiled image target (~301 KB) |

### Regenerating the `.mind` Target File
If you change the target image, recompile it using the [MindAR Image Target Compiler](https://hiukim.github.io/mind-ar-js-doc/tools/compile):
1. Upload your new reference image
2. Download the generated `.mind` file
3. Replace `targets-boll.mind` in the project root

---

## 📱 Usage Instructions

1. Open the hosted URL on your phone
2. Allow camera permission when prompted
3. Wait for the **"Loading AR..."** screen to disappear
4. Point your camera at a **tennis ball image** (the same one used as the target)
5. Watch the 3D tennis ball model appear and spin! 🎾

---

## 🔧 Customization

### Change the 3D Model
Replace `Tennis ball.glb` with any `.glb` or `.gltf` file and update the asset reference in `index.html`:
```html
<a-asset-item id="tennis-ball" src="./your-model.glb"></a-asset-item>
```

### Adjust Scale & Position
Modify the `scale` and `position` attributes on the `<a-gltf-model>` element:
```html
<a-gltf-model scale="3 3 3" position="0 0 0.1" ...>
```

### Change Animation Speed
Adjust `dur` (duration in milliseconds) in the `animation` attribute:
```html
animation="property: rotation; to: 0 360 0; loop: true; dur: 2000; easing: linear"
```

---

## 🌐 Browser Compatibility

| Browser | AR Support |
|---|---|
| Chrome (Android) | ✅ Full support |
| Safari (iOS 14.5+) | ✅ Full support |
| Firefox (Android) | ✅ Full support |
| Desktop Chrome | ✅ (webcam required) |
| Samsung Internet | ✅ Full support |

---

## 📄 License

This project is open source. Feel free to use and modify it for personal or commercial projects.

---

## 🙏 Acknowledgements

- [A-Frame](https://aframe.io/) by Mozilla — Web VR/AR framework
- [MindAR.js](https://github.com/hiukim/mind-ar-js) by hiukim — Efficient image tracking in the browser
