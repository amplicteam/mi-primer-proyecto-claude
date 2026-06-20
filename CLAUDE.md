<!-- GSD:project-start source:PROJECT.md -->
## Project

**Amplic AI Learning Hub**

Una plataforma web interactiva estilo "curso" que funciona como roadmap de aprendizaje de Inteligencia Artificial para los co-founders de Amplic (Dharrell y Jose). Cada uno tiene su propio perfil con tracking de progreso individual. El objetivo final: dominar IA para vender servicios y productos de IA a empresas bajo la marca Amplic.

**Core Value:** **Aprendizaje estructurado y trackeable de IA para dos personas**, con rutas claras de principiante a avanzado, recursos curados, y visibilidad del progreso de cada co-founder.
<!-- GSD:project-end -->

<!-- GSD:stack-start source:research/STACK.md -->
## Technology Stack

## Recommended Stack
### Core Framework
| Technology | Version | Purpose | Why |
|------------|---------|---------|-----|
| SvelteKit | 2.x (Svelte 5) | Full-stack framework | Smallest bundle size, best DX for small interactive apps, built-in routing, server endpoints for API. Up to 70% smaller bundles than Next.js. Perfect fit for a 2-user dashboard app where simplicity matters. |
| TypeScript | 5.x | Type safety | Svelte 5 has first-class TS support. Prevents bugs in progress tracking logic. |
### Database / Persistence
| Technology | Version | Purpose | Why |
|------------|---------|---------|-----|
| Supabase | Latest | User progress, resource catalog | Free tier (500MB, unlimited API) is more than enough for 2 users. Real PostgreSQL means proper relational data (users, resources, progress). Row Level Security gives per-user data isolation trivially. Hosted -- no server to manage. |
### Visualization
| Technology | Version | Purpose | Why |
|------------|---------|---------|-----|
| @xyflow/svelte (Svelte Flow) | 1.x | Interactive roadmap nodes | Same team as React Flow (industry standard for node UIs), built from scratch for Svelte. Drag, zoom, pan, custom node components all built-in. MIT licensed. Nodes are just Svelte components so styling/interactivity is native. |
### Hosting
| Technology | Version | Purpose | Why |
|------------|---------|---------|-----|
| Vercel | - | Deployment | First-class SvelteKit adapter. Free tier handles this scale trivially. Auto-deploys from GitHub. Edge functions for API routes. |
### Styling
| Technology | Version | Purpose | Why |
|------------|---------|---------|-----|
| Tailwind CSS | 4.x | Utility-first styling | Fast prototyping, responsive by default, works perfectly with Svelte components. No design system needed for 2 users. |
### Supporting Libraries
| Library | Version | Purpose | When to Use |
|---------|---------|---------|-------------|
| @supabase/supabase-js | 2.x | Supabase client SDK | All data reads/writes |
| chart.js + svelte-chartjs | 4.x | Dashboard stats/charts | Progress bars, completion charts on dashboard |
| lucide-svelte | Latest | Icons | UI icons throughout |
| date-fns | 3.x | Date formatting | Streak calculations, "last studied" timestamps |
## Alternatives Considered
| Category | Recommended | Alternative | Why Not |
|----------|-------------|-------------|---------|
| Framework | SvelteKit | Next.js (React) | Overkill for 2-user app. Larger bundles, more boilerplate. React Flow exists but Svelte Flow is equally capable with less code. |
| Framework | SvelteKit | Astro | Astro is content-first/static. This app needs interactivity (checkboxes, progress, node interactions). Astro's island architecture adds friction for a fully interactive dashboard. |
| Database | Supabase | Firebase/Firestore | NoSQL is wrong model -- resources belong to areas, progress belongs to users. Relational data fits PostgreSQL naturally. Firebase's pricing model (per-read) is riskier long-term. |
| Database | Supabase | JSON files | Cannot persist files on Vercel's serverless. Would need a separate server or git-based workflow. Supabase free tier is simpler. |
| Database | Supabase | SQLite (Turso) | Viable but Supabase gives you auth, realtime, and a dashboard for free. Less setup. |
| Visualization | Svelte Flow | D3.js | D3 is low-level. Would need to build node layout, connections, zoom, pan from scratch. Svelte Flow gives all of this out of the box. |
| Visualization | Svelte Flow | vis.js / cytoscape.js | Not Svelte-native. Would require wrapper components and fight the framework. Svelte Flow nodes ARE Svelte components. |
| Styling | Tailwind CSS | Component library (shadcn-svelte) | Adds complexity. For 2 users, custom Tailwind styling is faster than learning a component library's API. Consider shadcn-svelte only if you want polished UI fast. |
| Hosting | Vercel | Netlify | Both work. Vercel has slightly better SvelteKit support via official adapter. |
## Do NOT Use
| Technology | Why Not |
|------------|---------|
| Redux / state management library | Svelte 5 runes ($state, $derived) handle all state natively. No external state management needed. |
| NextAuth / Auth.js | 2 fixed users. Use Supabase simple email auth or even just a PIN/password gate. No OAuth needed. |
| Prisma / Drizzle ORM | Supabase client SDK handles all queries. Adding an ORM is unnecessary indirection for this data model. |
| Docker / self-hosting | Vercel free tier handles everything. No need for infrastructure management. |
| MongoDB | Relational data (users -> progress -> resources -> areas). PostgreSQL is the right model. |
## Installation
# Create project
# Select: SvelteKit, TypeScript, Tailwind CSS
# Core dependencies
# Dashboard/UI
# Dev
## Data Model (Supabase)
## Key Architecture Decisions
## Sources
- [Svelte Flow](https://svelteflow.dev/) - Official documentation
- [xyflow GitHub](https://github.com/xyflow/xyflow) - React Flow + Svelte Flow monorepo
- [Supabase](https://supabase.com/) - Backend as a Service with PostgreSQL
- [SvelteKit docs](https://svelte.dev/docs/kit) - Official framework documentation
- [Supabase vs Firebase comparison](https://supabase.com/alternatives/supabase-vs-firebase)
<!-- GSD:stack-end -->

<!-- GSD:conventions-start source:CONVENTIONS.md -->
## Conventions

Conventions not yet established. Will populate as patterns emerge during development.
<!-- GSD:conventions-end -->

<!-- GSD:architecture-start source:ARCHITECTURE.md -->
## Architecture

Architecture not yet mapped. Follow existing patterns found in the codebase.
<!-- GSD:architecture-end -->

<!-- GSD:skills-start source:skills/ -->
## Project Skills

| Skill | Description | Path |
|-------|-------------|------|
| frontend-design | Guidance for distinctive, intentional visual design when building new UI or reshaping an existing one. Helps with aesthetic direction, typography, and making choices that don't read as templated defaults. | `.claude/skills/frontend-design/SKILL.md` |
<!-- GSD:skills-end -->

<!-- GSD:workflow-start source:GSD defaults -->
## GSD Workflow Enforcement

Before using Edit, Write, or other file-changing tools, start work through a GSD command so planning artifacts and execution context stay in sync.

Use these entry points:
- `/gsd-quick` for small fixes, doc updates, and ad-hoc tasks
- `/gsd-debug` for investigation and bug fixing
- `/gsd-execute-phase` for planned phase work

Do not make direct repo edits outside a GSD workflow unless the user explicitly asks to bypass it.
<!-- GSD:workflow-end -->



<!-- GSD:profile-start -->
## Developer Profile

> Profile not yet configured. Run `/gsd-profile-user` to generate your developer profile.
> This section is managed by `generate-claude-profile` -- do not edit manually.
<!-- GSD:profile-end -->
