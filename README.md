# AR Badminton 🏸

Browser-based augmented reality badminton game using webcam hand tracking. No downloads, no installs — just open and play.

**Live demo:** [https://ar-badminton.pages.dev](https://ar-badminton.pages.dev)

---

## How to Play

### Setup
1. Open the game in **Chrome or Edge** (desktop)
2. Allow **webcam permission** when prompted
3. Make sure you have **good lighting** — hand tracking needs to see your hand clearly
4. Click **Solo Rally** (vs AI) or **2 Player** (two people, same webcam)

### Controls
Your hand IS the racket. Move your hand in front of the webcam to control the player.

| Hand Position | Swing Speed | Shot Type | What It Does |
|---------------|-------------|-----------|--------------|
| **High** | **Fast** | **Smash** | Steep downward shot — hard to return |
| **High** | **Slow** | **Drop** | Soft shot that barely clears the net |
| **Low** | Any | **Clear** | High deep arc to the back of the court |
| **Mid** | **Fast** | **Drive** | Flat fast shot across the court |

### Gameplay
- Move your hand **left/right** to position on the court
- Move your hand **up/down** on screen to move forward/back on the court
- When the shuttlecock comes to your side, **move your hand near it** to hit
- The **red target circle** on the court shows where the shuttle will land
- A **magnetism system** gently pulls the shuttle toward your hand when it's close
- First to **11 points** wins
- The AI gets smarter as you score more

### Tips
- Start with your hand in the **center of the screen**
- Don't swing wildly — steady positioning beats speed
- Watch the **landing target** to anticipate where to move
- The shot type indicator shows what shot you played (Smash/Drop/Clear/Drive)

---

## Tech Stack

- **MediaPipe Hands** — real-time hand landmark detection via webcam
- **Canvas 2D** — perspective court rendering with sprite-based players
- **Web Audio API** — procedural sound effects (racket thwack, crowd, net hit)
- **Zero dependencies** — everything loaded via CDN, single HTML file + sprite sheet

---

## Deploy

### Option 1: Cloudflare Pages (recommended)

```bash
npm install -g wrangler
wrangler login
wrangler pages project create ar-badminton --production-branch main
wrangler pages deploy . --project-name ar-badminton
```

### Option 2: Any static file server

The game is just `index.html` + `sprites/sheet.png`. Host on any static server:

```bash
# Python
python3 -m http.server 8080

# Node
npx serve .

# Netlify
netlify deploy --prod --dir .

# GitHub Pages
# Just push to a repo and enable Pages in Settings → Pages → Deploy from branch
```

> **Note:** Must be served over HTTPS (or localhost) for webcam access to work.

### Option 3: GitHub Pages

1. Push to a GitHub repo
2. Go to **Settings → Pages**
3. Set source to **Deploy from a branch → main → / (root)**
4. Your game will be live at `https://<username>.github.io/<repo-name>/`

---

## Project Structure

```
├── index.html          # Entire game (single file)
├── sprites/
│   └── sheet.png       # Player sprite sheet (2 rows × 4 poses)
└── README.md
```

### Sprite Sheet Layout (1536×1024, 384×512 per cell)

| | Idle | Forehand | Backhand | Smash |
|---|---|---|---|---|
| **Row 1** (back view) | Player ready | Player forehand | Player backhand | Player smash |
| **Row 2** (front view) | Opponent ready | Opponent forehand | Opponent backhand | Opponent smash |

---

## Features

- **Webcam AR** — your camera feed as the background
- **Hand tracking** — MediaPipe detects your hand position in real-time
- **4 shot types** — Smash, Drop, Clear, Drive based on hand height + speed
- **AI opponent** — gets progressively harder, uses varied shot selection
- **2 Player mode** — two hands on the same webcam
- **Perspective court** — indoor badminton hall with proper markings
- **Sprite characters** — animated player poses that change on each shot
- **Landing predictor** — target shows where the shuttle will land
- **Magnetism assist** — shuttle curves toward your hand for easier rallies
- **Procedural audio** — different sounds for smash, drop, net hit, scoring
- **Score to 11** — with streak counter and shot type callouts
