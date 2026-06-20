# Technology Stack

**Project:** Amplic AI Learning Hub
**Researched:** 2026-06-20

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

```bash
# Create project
npx sv create amplic-learning-hub
# Select: SvelteKit, TypeScript, Tailwind CSS

# Core dependencies
npm install @xyflow/svelte @supabase/supabase-js

# Dashboard/UI
npm install chart.js svelte-chartjs lucide-svelte date-fns

# Dev
npm install -D @sveltejs/adapter-vercel
```

## Data Model (Supabase)

```sql
-- Areas (LLMs, Deep Learning, Computer Vision, etc.)
create table areas (
  id uuid primary key default gen_random_uuid(),
  name text not null,
  description text,
  sort_order int,
  color text -- for roadmap node styling
);

-- Resources (videos, courses, docs)
create table resources (
  id uuid primary key default gen_random_uuid(),
  area_id uuid references areas(id),
  title text not null,
  url text,
  type text check (type in ('video', 'course', 'doc', 'article')),
  estimated_minutes int,
  sort_order int
);

-- User progress (per user, per resource)
create table progress (
  user_id text not null, -- 'dharrell' or 'jose'
  resource_id uuid references resources(id),
  completed boolean default false,
  completed_at timestamptz,
  primary key (user_id, resource_id)
);

-- Roadmap node positions (for Svelte Flow)
create table roadmap_nodes (
  id uuid primary key default gen_random_uuid(),
  area_id uuid references areas(id),
  x float not null,
  y float not null,
  parent_node_id uuid references roadmap_nodes(id)
);
```

## Key Architecture Decisions

1. **Svelte 5 runes for state** -- $state() for progress tracking, $derived() for computed stats. No external state library.
2. **Supabase RLS for user isolation** -- Simple policy: `user_id = current_setting('app.user_id')` or just filter client-side (2 users, trust is implicit).
3. **Static roadmap layout stored in DB** -- Node positions in `roadmap_nodes` table, editable via Svelte Flow's drag-and-drop, persisted to Supabase.
4. **Content as data, not code** -- Resources live in the database, not hardcoded. Add/remove via Supabase dashboard or a simple admin page.

## Sources

- [Svelte Flow](https://svelteflow.dev/) - Official documentation
- [xyflow GitHub](https://github.com/xyflow/xyflow) - React Flow + Svelte Flow monorepo
- [Supabase](https://supabase.com/) - Backend as a Service with PostgreSQL
- [SvelteKit docs](https://svelte.dev/docs/kit) - Official framework documentation
- [Supabase vs Firebase comparison](https://supabase.com/alternatives/supabase-vs-firebase)
