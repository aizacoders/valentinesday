# Valentine's Day Celebration

A romantic, responsive Nuxt page to celebrate Valentine's Day with a photo area, smooth animations, love notes, and an Adelaide countdown.

## Features

- Responsive layout with romantic styling and smooth floating hearts.
- Photo area for 2-4 memories and a hero collage.
- Adelaide (Australia/Adelaide) countdown to February 14.
- English love quotes with easy customization.

## Quick Start

```bash
pnpm install
pnpm dev
```

Open `http://localhost:3000`.

## Customize

- Replace hero photos and placeholders in `app/pages/index.vue`.
- Update the countdown UI in `app/components/CountdownTimer.vue`.
- Adjust theme and animations in `app/assets/css/main.css`.
- Add your romance music at `public/audio/romance.mp3`.

## Production

```bash
pnpm build
pnpm preview
```

## Deploy to GitHub Pages (Project Pages)

1. In GitHub, go to Settings → Pages and set Source to GitHub Actions.
2. Make sure the workflow runs on your default branch (e.g., `main`).
3. The site will be available at `https://<user>.github.io/<repo>/`.

If you want to preview the build locally with a project base URL:

```bash
NUXT_APP_BASE_URL=/<repo>/ pnpm build
```
