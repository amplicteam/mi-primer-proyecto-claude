# Phase 1 Context: Project Scaffold and Deploy

**Phase:** 1 — Project Scaffold and Deploy
**Date:** 2026-06-20
**Decisions captured:** 6

## Domain

Create the SvelteKit project structure, apply Amplic branding, and deploy to Vercel so the app is accessible via URL from any device.

## Canonical Refs

| Document | Path | Purpose |
|----------|------|---------|
| Amplic Documento Oficial | `C:\Users\dharr\Documentos\2. Crecimiento\A M P L I C\Amplic Documento Oficial.docx` | Brand identity, colors, typography, tone |
| PROJECT.md | `.planning/PROJECT.md` | Project scope and goals |
| Research SUMMARY | `.planning/research/SUMMARY.md` | Stack and architecture decisions |

## Decisions

### Project Structure
- **Organization:** By feature — each area has its own folder (`/roadmap`, `/catalog`, `/dashboard`, `/progress`)
- **Framework:** SvelteKit 2 (Svelte 5) as recommended by research

### Visual Identity (Amplic Branding)
- **Color palette:**
  - Azul Profundo `#0E1B33` — fondos sólidos, titulares, base
  - Azul Amplic `#2563EB` — enlaces, destacados, CTAs
  - Cian Señal `#06B6D4` — acentos puntuales (nunca domina, solo señala)
  - Gris Claro `#F4F6FA` — fondos suaves, respiro y limpieza
- **Typography:** Poppins or Montserrat for headings (geometric, bold), Inter for body text (clean, legible)
- **Design concept:** "Amplificación" — barras/ondas ascendentes, mucho espacio en blanco, color como señal
- **Tone:** Cercana pero profesional, moderna, basada en evidencia
- **Principle #04:** "La calidad también se ve y se siente; debe ser atractiva de usar"

### Hosting
- **Platform:** Vercel (free tier)
- **Domain:** Vercel subdomain initially (e.g., amplic-learn.vercel.app)
- **Custom domain:** Deferred to later — can be added anytime

### Landing Page
- **Decision:** Claude's discretion — recommend a minimal Amplic-branded landing with logo, tagline "Amplificamos datos en decisiones", and a clean "Entrar" button leading to the user selector. Aligns with brand principle of being "estético y accesible."

### Tech Stack (from research)
- **SvelteKit 2** (Svelte 5) — framework
- **Tailwind CSS** — styling
- **Svelte Flow** (@xyflow/svelte) — roadmap visualization (Phase 7)
- **localStorage** — persistence (no backend for v1)
- **Vercel** — hosting with SvelteKit adapter

## Code Context

No existing code to reuse. Greenfield project.

## Deferred Ideas

(None from this discussion)

---
*6 decisions | 0 deferred | Ready for planning*
