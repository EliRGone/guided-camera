# Product Camera (PWA)

A single-page progressive web app that opens your phone's camera, draws a
centered bounding-box guide for framing product photos, and saves JPEGs to
your phone's Downloads folder. Add it to your home screen and it behaves
like a regular app — fullscreen, with its own icon.

## What's in here

```
ProductCameraPWA/
├── index.html          ← the whole app (HTML + CSS + JS in one file)
├── manifest.json       ← PWA manifest (name, icons, display mode)
├── service-worker.js   ← makes the app installable + offline-capable
├── icons/
│   ├── icon-192.png
│   ├── icon-512.png
│   └── icon-512-maskable.png
└── README.md           ← this file
```

You don't need to install anything to use the app — but you do need to host
it somewhere that serves over HTTPS, because phones won't grant camera
access to insecure pages. GitHub Pages is free and gives you HTTPS
automatically.

## Deploy it on GitHub Pages

The whole process takes ~5 minutes.

### 1. Create a new GitHub repository

Go to <https://github.com/new>, give the repo a name (e.g. `product-camera`),
keep it **Public**, and click **Create repository**.

### 2. Upload the files

The easiest way is right in the browser:

1. On the new repo's page, click **uploading an existing file**.
2. Drag the entire contents of this `ProductCameraPWA/` folder onto the
   upload area — `index.html`, `manifest.json`, `service-worker.js`, and
   the `icons/` folder.
3. Scroll down and click **Commit changes**.

If you prefer the command line:

```bash
cd ProductCameraPWA
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/<your-username>/product-camera.git
git push -u origin main
```

### 3. Turn on GitHub Pages

1. In the repo, click **Settings** (top right of the repo nav).
2. In the left sidebar click **Pages**.
3. Under **Source**, pick **Deploy from a branch**.
4. Under **Branch**, pick `main` and folder `/ (root)`. Click **Save**.
5. Wait ~1 minute. The page will refresh and show a URL like
   `https://<your-username>.github.io/product-camera/`. That's your app.

### 4. Install it on your phone

1. On the phone, open the URL above in **Chrome** (Android) or **Safari** (iPhone).
2. Grant camera permission when prompted.
3. Add it to your home screen:
   - **Android (Chrome):** an "Install app" banner usually appears at the
     bottom. Tap it. If not, tap the three-dot menu → **Install app** (or
     **Add to Home screen**).
   - **iPhone (Safari):** tap the Share button (square with up arrow) →
     **Add to Home Screen**.
4. From now on, tap the icon on your home screen. It opens fullscreen with
   no browser chrome — just the camera and the guide box.

## Using the app

- **Shutter button** (white circle, bottom center) — takes the photo. The
  JPEG is saved to your Downloads folder.
- **Flip icon** (right side) — switches between back and front camera.
- **Gear icon** (left side) — opens settings to change the box's size and
  aspect ratio (square, portrait, landscape).

Your size/shape preferences are remembered between visits.

## Tweaking the look

All styling lives at the top of `index.html` in the `<style>` block. A few
things you might want to change:

- `--box-size` (default `80vmin`) — how big the guide box is. Higher = bigger.
- `--box-aspect` (default `1`) — width / height. `1` = square, `0.8` = portrait.
- `--accent` (default `#ffc640`) — the warm yellow on the corner brackets.
- `--dim` (default `rgba(0,0,0,0.55)`) — how strongly the area outside the
  box is dimmed.

After changing files, commit and push again — GitHub Pages rebuilds
automatically (give it ~30 seconds). On the phone, you may need to close
the installed app and reopen it to pick up the new version (the service
worker caches assets).

## Troubleshooting

- **Camera permission denied** — go to the browser's site settings for
  your Pages URL and re-enable Camera, then reload.
- **Black screen, no preview** — make sure you're on HTTPS (the URL starts
  with `https://`). Phones block camera access on plain `http://`.
- **Install option doesn't appear** — make sure all four files
  (`index.html`, `manifest.json`, `service-worker.js`, plus the icons)
  were uploaded and that the page loads without errors. On Android Chrome,
  you can also force-add via the three-dot menu.
- **The app doesn't update after I pushed changes** — service workers
  cache aggressively. Close all instances of the app, then reopen. Or in
  Chrome → Site settings → Clear & reset.

## Limitations vs. a native app

- No access to the system camera shutter button or hardware shortcuts.
- Photos go to Downloads, not directly into the Photos/Gallery album.
- On iOS, some camera features (torch/zoom/exposure controls) aren't
  available through the browser.

If any of those become important later, the original
[`ProductCameraApp/`](../ProductCameraApp/) folder has the equivalent
native Android version ready to build in Android Studio.
