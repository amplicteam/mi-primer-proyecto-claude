<!-- GSD:project-start source:PROJECT.md -->
## Project

**Amplic AI Learning Hub**

Una plataforma web interactiva estilo "curso" que funciona como roadmap de aprendizaje de Inteligencia Artificial para los co-founders de Amplic (Dharrell y Jose). Cada uno tiene su propio perfil con tracking de progreso individual. El objetivo final: dominar IA para vender servicios y productos de IA a empresas bajo la marca Amplic.

**Core Value:** **Aprendizaje estructurado y trackeable de IA para dos personas**, con rutas claras de principiante a avanzado, recursos curados, y visibilidad del progreso de cada co-founder.
<!-- GSD:project-end -->

<!-- GSD:stack-start source:research/STACK.md -->
## Stack

SvelteKit 2.x (Svelte 5) + TypeScript, Supabase (PostgreSQL), Svelte Flow, Tailwind CSS 4.x, Vercel. Libs: @supabase/supabase-js, chart.js, lucide-svelte, date-fns.

**Do NOT use:** Redux (use runes), NextAuth (2 fixed users), Prisma/Drizzle (use Supabase SDK), Docker, MongoDB.
<!-- GSD:stack-end -->

<!-- GSD:conventions-start source:CONVENTIONS.md -->
<!-- GSD:conventions-end -->

<!-- GSD:architecture-start source:ARCHITECTURE.md -->
<!-- GSD:architecture-end -->

<!-- GSD:skills-start source:skills/ -->
## Project Skills

| Skill | Description | Path |
|-------|-------------|------|
| frontend-design | Guidance for distinctive, intentional visual design when building new UI or reshaping an existing one. Helps with aesthetic direction, typography, and making choices that don't read as templated defaults. | `.claude/skills/frontend-design/SKILL.md` |
<!-- GSD:skills-end -->

<!-- GSD:workflow-start source:GSD defaults -->
## GSD Workflow — Smart Activation

GSD is powerful but expensive (~40-100k tokens per orchestrated task). Use it surgically:

**REQUIRE GSD** (always worth the token cost):
- `/gsd-execute-phase` — new roadmap phases, multi-file features with logic/data/API changes
- `/gsd-debug` — production bugs, complex multi-system issues
- `/gsd-quick --full` — only when the task has real ambiguity AND touches critical paths (auth, data, payments)

**SKIP GSD — work directly** (the plan is already clear or the work is mechanical):
- Visual/CSS/branding changes (styling, colors, typography, layout tweaks)
- Applying a design that was already discussed and approved in conversation
- Doc updates, README changes, copy edits
- Single-file fixes where the solution is obvious
- Installing deps, config changes, env setup
- Continuation of work that was already planned in a prior GSD run

**Decision rule:** If you can describe every file change before touching code, skip GSD and just do it. If you need to discover the approach or coordinate across unfamiliar systems, use GSD.

When skipping GSD, still commit atomically and update STATE.md if the change is significant.
<!-- GSD:workflow-end -->



<!-- GSD:profile-start -->
<!-- GSD:profile-end -->
