# NEONDROP 🎮

A sleek, modern, neon-styled Tetris game — playable in any browser. No dependencies, no build step, just one `index.html` file.

**[▶ Play it live](#)** _(your GitHub Pages URL will go here)_

## Features

- Full Tetris gameplay: 7-bag randomizer, ghost piece, hold, 3-piece next queue, hard/soft drop, wall kicks
- Progressive levels and scoring (single / double / triple / Tetris)
- Synth sound effects (no audio files) with mute toggle
- Local high-score saving (browser `localStorage`)
- Keyboard, on-screen, and swipe controls — works on desktop and mobile
- Dark neon UI with glowing tetrominoes

## Controls

| Key | Action |
|-----|--------|
| ← → | Move |
| ↑ / X | Rotate CW |
| Z | Rotate CCW |
| ↓ | Soft drop |
| Space | Hard drop |
| C / Shift | Hold |
| P | Pause |
| M | Mute |
| R | Restart |

On mobile: swipe to move, tap to rotate, swipe down to drop, or use the on-screen buttons.

## Run locally

Just open `index.html` in any browser. (No server needed.)

## Deploy to GitHub Pages

1. Create a new repository on GitHub (e.g. `neondrop`).
2. From this folder, run:

   ```bash
   git init
   git add index.html README.md
   git commit -m "NEONDROP — neon Tetris"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/neondrop.git
   git push -u origin main
   ```

3. On GitHub: **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: `main` / `/ (root)` → Save**.
4. Wait ~1 minute. Your game will be live at:

   ```
   https://YOUR_USERNAME.github.io/neondrop/
   ```

Replace `YOUR_USERNAME` with your GitHub username.

---

Built with vanilla HTML/CSS/JS. MIT licensed — do whatever you like with it.
