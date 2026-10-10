# Her Little Universe ✦

A mobile-first, privacy-respecting gift site for Ash, made by Ojas. The experience is client-side by default; the tiny Express API is optional and intentionally stores no data. The new **Tiny Rage Room / Ojas Punching Bag** is integrated into the same universe.

## Requirements

- Node.js 20+ (tested source target: Node 22)
- npm 10+
- Internet access for the first dependency installation

## Install and run

From the project root:

```bash
npm install
cp .env.example .env
npm run dev
```

Frontend: `http://localhost:5173`  
Optional API: `http://localhost:8787/api/health`

Run only the frontend (the site and all games work without the API):

```bash
npm run dev:client
```

## Production build and start

```bash
npm run build
npm start
```

The frontend build is written to `client/dist`; the API build is written to `server/dist`. The Express server does not serve the frontend bundle, so deploy `client/dist` to a static host and deploy `server/dist` separately only if you want the health/config endpoints. The frontend does not depend on the API.

## Deploy

### Static frontend

Deploy `client/dist` to any static host (for example, Netlify, Cloudflare Pages, or Vercel). Set the build command to `npm run build -w client` and the output directory to `client/dist` when deploying from the repository root. No frontend environment variables are required.

### Optional API

Deploy the `server` workspace to a Node host. Build with `npm run build -w server`, start with `npm run start -w server`, and configure:

- `PORT` — host-provided port (defaults to `8787` locally)
- `CLIENT_ORIGIN` — exact frontend origin allowed by CORS (defaults to `http://localhost:5173`)

The API exposes only `GET /api/health` and `GET /api/config`. No database, auth, tracking, or write endpoint exists.

## Personalize it

Edit **`client/src/config/giftConfig.ts`** first. It centralizes:

- recipient/sender nicknames and opening copy
- the complete letter, reasons jar, jokes, and memory placeholders
- visibility flags for each room
- punching bag combo timing, thresholds, shop/boss toggles, and 40 reactions

Replace the placeholder memory title/message with a real shared memory before gifting. Keep images optional; no photos are needed for the world to look complete. The letter uses the requested affectionate draft and can be edited paragraph-by-paragraph in the config.

## The Ojas Punching Bag

- Tap the bag or the large BONK button; keyboard users can focus the bag and press Enter/Space.
- Three modes: Normal Chaos, Combo Challenge, and the configurable Silly Boss Fight.
- One fictional bonk-buck per hit; optional cosmetic shop; unlocked/equipped cosmetics and points are saved in that browser's localStorage only.
- Sound starts off. When enabled, a tiny synthesized tone is created only in response to a user action; no audio files or third-party sound assets are loaded.
- Reduced visual effects and optional vibration are available in settings. Vibration is used only after the user enables it and only if the browser exposes `navigator.vibrate`.
- Scores, modes, mood selections, and play activity are not sent to a server.

## Privacy and limitations

- No analytics, ads, third-party trackers, location, camera, microphone, account, or notification features.
- The sound toggle in the overall site header is decorative in this first implementation; the punching room has the actual synthesized sound toggle. (Remove the header toggle if you want no misleading control.)
- Google Fonts are loaded remotely by CSS for the visual style. For a fully offline / no-third-party-request deployment, remove the `@import` line in `client/src/styles/global.css` and use the system font fallbacks.
- The tiny star-catching activity is intentionally relaxed and has no timer or penalty.
- This environment may not have network access for installing npm dependencies. Do not interpret source generation as a successful build: run the commands above on a networked machine and fix any environment-specific issues before publishing.
