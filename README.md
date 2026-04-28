# QR → AR Floating Poster

A browser-based AR demo. Scan a QR code with your phone, point the camera at a printable marker, and a 3D poster floats above it — tracked in real time to the marker's position and orientation.

Built with [A-Frame](https://aframe.io) + [AR.js](https://ar-js-org.github.io/AR.js-Docs/). No app install required — runs in mobile Safari / Chrome over HTTPS.

## Live demo

Hosted on GitHub Pages. Open the landing page on a desktop, scan the QR with your phone, then aim your phone at the HIRO marker shown on screen (or printed from `marker.html`).

## Files

- `index.html` — landing page with a QR code (dynamically generated to point at the deployed `ar.html`) and a marker preview.
- `ar.html` — the AR experience. Activates the camera and renders a 3D scene anchored to the HIRO marker.
- `marker.html` — printable A4/Letter poster with QR + marker side-by-side.
- `poster-art.svg` — the texture used for the floating poster in the AR scene.
- `.nojekyll` — disables Jekyll on GitHub Pages so all files are served as-is.

## Local testing

You need HTTPS for camera access on a phone. Easiest options:

```bash
# Serve over plain HTTP for desktop testing
npx serve .

# To test on a phone, use a tunnel that gives you HTTPS:
npx localtunnel --port 3000
# or: ngrok http 3000
```

## Deploying

1. `git init && git add . && git commit -m "init"`
2. Create a GitHub repo and push.
3. In repo settings → Pages → deploy from `main` / root.
4. The site is live at `https://<user>.github.io/<repo>/`.

## How tracking works

AR.js detects the HIRO fiducial marker (a high-contrast black square with a known interior pattern) in each camera frame, solves a PnP problem to recover its 3D pose relative to the camera, then A-Frame uses that pose as a transform for the child scene graph. So everything inside `<a-marker>` lives in the marker's coordinate frame — translate, rotate, animate freely, and it stays locked to the printed marker as you move your phone.
