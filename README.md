# ⚽ Copa 2026 AI — PWA

Offline-capable Progressive Web App for World Cup 2026 player face recognition.

## Features
- Works 100% offline after first load
- Installable on Android, iOS, and desktop (Add to Home Screen)
- Player bank stored locally on the device
- Connects to your Google Colab backend when online

## File structure
```
copa2026-app/
├── index.html      ← entire app (HTML + CSS + JS)
├── sw.js           ← service worker (makes it offline)
├── manifest.json   ← PWA config (name, icon, theme color)
├── icon-192.png    ← app icon (you need to add this)
├── icon-512.png    ← app icon large (you need to add this)
└── README.md
```

## How to deploy on GitHub Pages (free hosting)

### Step 1 — Create a GitHub account
1. Go to https://github.com and click "Sign up"
2. Choose a free account

### Step 2 — Create a new repository
1. Click the "+" button → "New repository"
2. Name it: `copa2026-app`
3. Set it to **Public**
4. Check "Add a README file"
5. Click "Create repository"

### Step 3 — Upload your files
1. In your new repository, click "Add file" → "Upload files"
2. Drag and drop ALL files from this folder:
   - index.html
   - sw.js
   - manifest.json
   - icon-192.png
   - icon-512.png
3. Scroll down, click "Commit changes"

### Step 4 — Enable GitHub Pages
1. Click "Settings" (top of your repository)
2. Scroll down to "Pages" in the left menu
3. Under "Source", select "Deploy from a branch"
4. Under "Branch", select "main" and "/ (root)"
5. Click "Save"
6. Wait ~2 minutes, then your app is live at:
   `https://YOUR_USERNAME.github.io/copa2026-app`

### Step 5 — Install on your phone
1. Open the link above in Chrome (Android) or Safari (iOS)
2. Android: tap the "Install" banner or browser menu → "Add to Home Screen"
3. iOS: tap the Share button → "Add to Home Screen"
4. The app icon appears on your home screen and works offline!

## Add your own icon
- Create a square image (at least 512×512px) with a football/soccer ball
- Save it as `icon-192.png` (192×192px) and `icon-512.png` (512×512px)
- Free tool: https://favicon.io or https://realfavicongenerator.net

## Connecting to Colab backend
When your device is online, the app can call your FastAPI backend.
In `index.html`, find the `simulateScan()` function and replace it with a real
`fetch()` call to your `/recognize` endpoint.

Example:
```js
const res = await fetch('https://your-api.railway.app/recognize', {
  method: 'POST',
  body: formData   // FormData with the photo
});
const result = await res.json();
```

## Offline storage
Player data is saved in `localStorage` — it stays on the device even when offline.
When online, you can sync with your Colab/FastAPI database.
