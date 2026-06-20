# Summary: Phase 1 Plan 01 — Project Scaffold and Deploy

**Phase:** 01-project-scaffold-and-deploy
**Plan:** 01
**Completed:** 2026-06-20
**Status:** Complete

## What Was Built

Scaffolded the SvelteKit project with Amplic branding and deployed it live to Vercel via GitHub integration.

### Task 1: Scaffold SvelteKit with Tailwind and brand config ✓
- Created SvelteKit 2 (Svelte 5) project `amplic-learn/` using `npx sv create --template minimal --types ts`
- Added Tailwind CSS 4 via `@tailwindcss/vite` plugin (CSS-first `@theme` approach)
- Installed `@sveltejs/adapter-vercel` and configured it in `vite.config.ts` (this scaffold puts adapter in vite.config.ts, not svelte.config.js)
- Installed self-hosted fonts: `@fontsource/inter` (400, 500) + `@fontsource/poppins` (600, 700)
- Configured `src/app.css` with `@theme` block defining the 4 Amplic brand colors and 2 font families
- Created `src/lib/assets/logo.svg` — amplification mark (ascending bars in brand colors) + "AMPLIC" wordmark
- Built landing page `src/routes/+page.svelte` with logo, "AI Learning Hub" heading, tagline "Amplificamos datos en decisiones", and "Entrar" button linking to /catalog
- `npm run build` passes with zero errors; adapter-vercel confirmed in output

### Task 2: Deploy to Vercel ✓
- Initialized git repo inside `amplic-learn/`
- Created private GitHub repo `amplicteam/amplic-learn` and pushed
- User imported the repo into Vercel; SvelteKit auto-detected; deployed successfully
- Landing page confirmed live showing correct Amplic branding (verified via deploy preview screenshot)

## Brand Tokens Applied

| Token | Value |
|-------|-------|
| --color-azul-profundo | #0E1B33 |
| --color-azul-amplic | #2563EB |
| --color-cian-senal | #06B6D4 |
| --color-gris-claro | #F4F6FA |
| --font-heading | Poppins |
| --font-body | Inter |

## Key Decisions / Deviations

- **Adapter location:** The current Svelte CLI scaffold configures the adapter in `vite.config.ts` rather than `svelte.config.js` (no svelte.config.js generated). Plan assumed svelte.config.js — adapted accordingly.
- **Scaffold method:** Used `npx sv create` non-interactively (`--no-install --no-add-ons`) after the interactive version hung. Added Tailwind/adapter manually via npm + config edits rather than `sv add` (which also hung interactively).
- **Deploy method:** GitHub integration (user's choice) instead of Vercel CLI — gives auto-deploy on push.

## Files Created/Modified

- `amplic-learn/vite.config.ts` — adapter-vercel + tailwindcss plugin
- `amplic-learn/src/app.css` — Tailwind import + @theme brand tokens + font imports
- `amplic-learn/src/routes/+layout.svelte` — imports app.css
- `amplic-learn/src/routes/+page.svelte` — Amplic landing page
- `amplic-learn/src/lib/assets/logo.svg` — Amplic logo
- `amplic-learn/package.json` — added tailwindcss, @tailwindcss/vite, adapter-vercel, fontsource fonts

## Repo

- GitHub: https://github.com/amplicteam/amplic-learn (private)
- Vercel: deployed (URL pending capture)

## Requirements Satisfied

- **CORE-01**: Plataforma web desplegada online accesible desde cualquier dispositivo ✓
