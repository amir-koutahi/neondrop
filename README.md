# NEONDROP 🎮

A sleek, modern, neon-styled Tetris game with competitive modes, optional accounts, and a global leaderboard. One `index.html` file, no build step.

**Live:** `https://amir-koutahi.github.io/neondrop/`

## Features

- **Four modes:** Marathon (endless), Sprint 40 (clear 40 lines fastest), Ultra 2:00 (max score in 2 min), and Blitz (fast from the start)
- Smooth, hardware-friendly rendering (pre-rendered sprites + cached background — no per-frame lag)
- Full gameplay: 7-bag randomizer, ghost piece, hold, next queue, wall kicks, hard/soft drop
- Synth sound effects with mute
- **Optional sign-in** with a **global leaderboard** per mode, plus a "My Games" view
- Works without a backend too — falls back to local profiles saved in the browser
- Keyboard, on-screen, and swipe controls (desktop + mobile)

## Controls

| Key | Action |
|-----|--------|
| ← → | Move |
| ↑ / X | Rotate CW |
| Z | Rotate CCW |
| ↓ | Soft drop |
| Space | Hard drop |
| C / Shift | Hold |
| P | Pause · M | Mute · R | Restart |

On mobile: swipe to move, tap to rotate, swipe down to drop, or use the on-screen buttons.

## Accounts + leaderboard (optional)

The game works immediately in **local mode** (profiles and scores save on the device). To enable **real sign-in and a shared global leaderboard**, connect a free Firebase project — it takes about 5 minutes.

### 1. Create the Firebase project
1. Go to <https://console.firebase.google.com> → **Add project** (any name) → create it.
2. In the project, open **Build → Authentication → Get started**, pick **Google** as a sign-in provider, and enable it.
3. Open **Build → Firestore Database → Create database** → start in **production mode** → pick a region.

### 2. Get your web config
1. Click the gear icon → **Project settings**.
2. Scroll to **Your apps** → click the **`</>`** (Web) icon → register an app (any nickname).
3. Copy the `firebaseConfig` values it shows you.

### 3. Paste it into the game
Open `index.html` and find the `FIREBASE_CONFIG` block near the bottom. Fill it in:

```js
const FIREBASE_CONFIG = {
  apiKey: "AIza...",
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-project",
  appId: "1:...:web:..."
};
```

(These web keys are safe to commit — they're public client identifiers, not secrets.)

### 4. Allow your site to sign in
In **Authentication → Settings → Authorized domains**, add `amir-koutahi.github.io`.

### 5. Set Firestore security rules
In **Firestore → Rules**, paste this (anyone can read the leaderboard; only signed-in users can submit their own scores):

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /scores/{doc} {
      allow read: if true;
      allow create: if request.auth != null
        && request.resource.data.uid == request.auth.uid;
      allow update, delete: if false;
    }
  }
}
```

### 6. (Leaderboard sorting index)
The first time you open the leaderboard for a mode, Firestore may log a link in the browser console to **create an index** (it needs one for `mode` + `score`/`timeMs`). Click that link → **Create index** → wait a minute. Do it once per query and the leaderboard is fully live.

That's it — push the updated `index.html` and sign-in + the global board are working.

## Run locally

Open `index.html` in any browser. (Google sign-in needs the page served over http/https and the domain authorized; local mode works from a file directly.)

## Deploy / update on GitHub Pages

From the project folder:

```bash
git add index.html README.md
git commit -m "Update NEONDROP"
git push
```

Pages redeploys automatically within a minute.

---

Built with vanilla HTML/CSS/JS + Firebase (optional). MIT licensed.
