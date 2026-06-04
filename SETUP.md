# BP Tracker — Setup Guide

## What you have
- `index.html` — the app
- `manifest.json` — PWA install config
- `sw.js` — service worker (offline support)
- `SETUP.md` — this file

---

## Step 1 — Get your Google OAuth Client ID

1. Go to https://console.cloud.google.com/
2. Create a new project (name it anything — "BP Tracker" works)
3. Go to **APIs & Services → OAuth consent screen**
   - User type: External
   - Fill in app name ("BP Tracker") and your email — click Save
4. Go to **APIs & Services → Credentials**
   - Click **Create Credentials → OAuth Client ID**
   - Application type: **Web application**
   - Name: BP Tracker
   - Under **Authorized JavaScript origins**, add:
     - `https://YOUR_GITHUB_USERNAME.github.io`
     - `http://localhost` (for local testing)
   - Click Create
5. Copy the **Client ID** (looks like: `123456789-abc.apps.googleusercontent.com`)

---

## Step 2 — Add your Client ID to the app

Open `index.html` and find this line near the bottom:

```
const GOOGLE_CLIENT_ID = 'YOUR_GOOGLE_CLIENT_ID';
```

Replace `YOUR_GOOGLE_CLIENT_ID` with the Client ID you copied.

---

## Step 3 — Enable Google Drive API

1. In Google Cloud Console → **APIs & Services → Library**
2. Search for **Google Drive API** → Enable it

---

## Step 4 — Deploy to GitHub Pages

1. Go to https://github.com and create a new repository
   - Name: `bp-tracker` (or anything you like)
   - Set to **Public** (required for free GitHub Pages)
2. Upload all 4 files: `index.html`, `manifest.json`, `sw.js`, `SETUP.md`
3. Go to **Settings → Pages**
   - Source: **Deploy from a branch**
   - Branch: `main` → `/root` → Save
4. Your app will be live at:
   `https://YOUR_GITHUB_USERNAME.github.io/bp-tracker/`

---

## Step 5 — Install on your iPhone

1. Open Safari on your iPhone
2. Go to `https://YOUR_GITHUB_USERNAME.github.io/bp-tracker/`
3. Tap the **Share** button (box with arrow)
4. Tap **Add to Home Screen**
5. Tap **Add** — it installs like a native app

---

## How Drive sync works

- Tap **Connect Drive** in the app header
- Sign in with your Google account
- The app creates a file called `bp_tracker_data.json` in your Drive
- Every change you make syncs automatically (2-second debounce)
- Open the app on any device, connect Drive — your data loads instantly

---

## Notes

- Data is stored in your Google Drive, not shared with anyone
- The app works offline — readings save locally and sync when back online
- The `bp_tracker_data.json` file in Drive is plain JSON — you can open it anytime
