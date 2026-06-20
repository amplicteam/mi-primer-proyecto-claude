# Walking Skeleton — Amplic AI Learning Hub

**Phase:** 1
**Generated:** 2026-06-20

## Capability Proven End-to-End

A user can open the Vercel URL on any device and see the Amplic-branded landing page with the tagline and an "Entrar" button.

## Architectural Decisions

| Decision | Choice | Rationale |
|---|---|---|
| Framework | SvelteKit 2 (Svelte 5) | Low learning curve, excellent DX, SSR built-in |
| Styling | Tailwind CSS 4 (CSS-first @theme) | Utility-first, fast prototyping, brand tokens via CSS |
| Fonts | @fontsource/inter + @fontsource/poppins | Self-hosted, no external CDN dependency |
| Deployment target | Vercel (adapter-vercel) | Free tier, Git integration, zero-config SSR |
| Directory layout | Feature-folders under src/routes/* (/catalog, /dashboard, /roadmap, /progress) | Scales with phase additions |
| Data layer | localStorage + static JSON (no backend) | Simplest persistence for 2-user app |

## Stack Touched in Phase 1

- [x] Project scaffold (SvelteKit, Vite, TypeScript, Tailwind)
- [x] Routing — landing page at /
- [ ] Database — N/A for Phase 1 (localStorage starts Phase 2)
- [x] UI — landing page with Amplic branding and "Entrar" button
- [x] Deployment — live on Vercel via Git integration

## Out of Scope (Deferred to Later Slices)

- User switching / profiles (Phase 2)
- Resource catalog and content (Phase 3+)
- Progress tracking (Phase 4)
- Visual roadmap with Svelte Flow (Phase 7)
- Custom domain
- Authentication (not needed — 2-person tool)

## Subsequent Slice Plan

- Phase 2: User can select their profile and data persists per user
- Phase 3: User can browse and mark resources as complete
- Phase 4: User can see progress bars and dashboard
- Phase 7: User can view interactive visual roadmap
