# Phase 2 Context: Data Model and User Switching

**Phase:** 2 — Data Model and User Switching
**Date:** 2026-06-20
**Decisions captured:** 6

## Domain

Sistema donde cada co-founder (Dharrell/Jose) elige su perfil, su progreso se persiste independientemente en localStorage, y el contenido se carga desde JSON estático. Base de datos para todo el tracking futuro.

## Canonical Refs

| Document | Path | Purpose |
|----------|------|---------|
| PROJECT.md | `.planning/PROJECT.md` | Project scope |
| Phase 1 SUMMARY | `.planning/phases/01-project-scaffold-and-deploy/01-01-SUMMARY.md` | Stack already built (SvelteKit 2, Tailwind 4, brand tokens) |
| Amplic Doc | `C:\Users\dharr\Documentos\2. Crecimiento\A M P L I C\Amplic Documento Oficial.docx` | Brand identity |

## Decisions

### User Selector
- **Decision:** Pantalla de selección estilo tarjetas (Claude's discretion). Al entrar (tras el PIN), el usuario ve dos tarjetas grandes "Dharrell" y "Jose" con avatar/inicial. Elige una y entra. Estética limpia alineada al branding Amplic (bg-gris-claro, acentos azul-amplic/cian-senal).
- Cada perfil tiene: nombre, identificador (id), y opcionalmente un color/avatar distintivo.

### Access Protection
- **Decision:** PIN simple de 4 dígitos compartido para abrir la app. Gate antes de la pantalla de selección de perfil.
- El PIN se valida client-side (es solo una barrera ligera, no seguridad real — herramienta interna de 2 personas).
- El PIN correcto se recuerda en localStorage para no pedirlo cada vez en el mismo dispositivo.

### Profile Memory
- **Decision:** Recordar último perfil usado en el dispositivo (Claude's discretion). Tras elegir perfil una vez, futuras visitas en ese dispositivo entran directo al último perfil. Debe haber forma de cambiar de perfil (botón "Cambiar usuario").

### Data Model (3 entities — from research)
- **Resource:** { id, area, title, type (video/curso/doc), url, duration, level (principiante/intermedio/avanzado) } — cargado desde JSON estático
- **PathNode / Area:** estructura del roadmap (áreas de IA: LLMs, Deep Learning, Computer Vision) — JSON estático
- **UserProgress:** { userId, resourceId, completed: bool, completedAt } — guardado en localStorage, independiente por usuario

### Persistence Strategy
- **localStorage** como única persistencia en v1. Keys namespaced por usuario (ej: `amplic:progress:dharrell`, `amplic:progress:jose`).
- Sin backend. Datos de contenido en archivos JSON estáticos en el proyecto (`src/lib/data/`).
- Un store de Svelte 5 (runes: `$state`) maneja el usuario activo y su progreso, sincronizado con localStorage.

### Directory Structure (feature-based)
- `src/lib/data/` — JSON estático (resources, areas)
- `src/lib/stores/` — user store, progress store
- `src/lib/types/` — TypeScript types (Resource, Area, UserProgress)
- `src/routes/` — pantalla PIN, selección de perfil

## Code Context

Phase 1 already built: SvelteKit 2 (Svelte 5 runes), Tailwind 4 with brand tokens in `src/app.css`, landing page at `/`. The "Entrar" button on landing links to `/catalog` (Phase 3). This phase adds the user/PIN gate and data layer that `/catalog` will consume.

## Deferred Ideas

- Sincronización cross-device (v2 — requeriría Supabase)
- Avatares con foto real (por ahora inicial/color)

---
*6 decisions | 2 deferred | Ready for planning*
