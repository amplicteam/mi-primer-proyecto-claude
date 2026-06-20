# Project Research Summary

**Project:** Amplic AI Learning Hub
**Domain:** Personal AI learning roadmap / course tracker (2-person team)
**Researched:** 2026-06-20
**Confidence:** HIGH

## Executive Summary

The Amplic AI Learning Hub is a personal learning tracker for two co-founders (Dharrell and Jose) studying AI topics. This is NOT a SaaS product. The two features that justify building a web app are the visual node-based roadmap and independent per-person progress tracking. Everything else should be ruthlessly simple.

The recommended approach is a SvelteKit client-side app with static JSON data files and localStorage for progress persistence. SvelteKit was chosen over React/Next.js because Svelte has a gentler learning curve for a beginner-intermediate team, produces less boilerplate, and handles state natively with runes -- no external state library needed. Svelte Flow provides the interactive roadmap visualization. No backend server or database is needed for v1.

The primary risks are all forms of over-engineering: building auth for 2 users, building a CMS for ~100 resources, complex progress tracking beyond checkboxes, and spending weeks on the roadmap visualization before content and tracking work. The mitigation is strict phasing -- ship a working list-based tracker in days, then layer the visual roadmap on top.

## Key Findings

### Recommended Stack

**Core technologies:**
- **SvelteKit 2.x (Svelte 5):** Full-stack framework -- smallest bundles, gentlest learning curve, native state management via runes
- **Svelte Flow (@xyflow/svelte 1.x):** Interactive node graph -- same team as React Flow, nodes are native Svelte components
- **TypeScript 5.x:** Type safety for progress tracking and data models
- **Tailwind CSS 4.x:** Rapid styling without a design system
- **Vercel:** Zero-config deployment with official SvelteKit adapter

**Resolved conflict:** STACK research recommended SvelteKit + Svelte Flow. ARCHITECTURE research used React (React Flow, .tsx, hooks). Resolution: **SvelteKit wins.** The team is beginner-intermediate level, Svelte learning curve is lower, boilerplate is minimal, and Svelte Flow is production-ready.

**Resolved conflict:** STACK recommended Supabase. ARCHITECTURE recommended localStorage + JSON (no backend). Resolution: **localStorage + JSON for v1.** 2 users on their own devices do not need a database. Supabase is the documented upgrade path for cross-device sync.

### Expected Features

**Must have (table stakes):**
- Resource catalog organized by 4 AI areas (LLMs, Deep Learning, CV, ML Fundamentals)
- User selector (Dharrell / Jose) -- no auth, just pick a name
- Checkbox completion per resource per user
- Progress bar per area
- Dashboard with overall completion percentage
- localStorage persistence
- Responsive web layout

**Should have (differentiators):**
- Visual roadmap with connected nodes (the killer feature vs a spreadsheet)
- Currently learning indicator
- Time/hours estimate per resource
- Side-by-side progress comparison view

**Defer (v2+):**
- Notes per resource
- Weekly/monthly stats
- Streak tracker (risk of demotivating)
- Any backend/database

### Architecture Approach

Pure client-side SvelteKit app. Resources and learning paths defined in static JSON files imported at build time. User progress stored in localStorage keyed by user ID. All computed values derived from raw completion records -- never stored. No API calls, no server.

**Major components:**
1. **UserSwitcher** -- Select active user, sets context consumed by all child components
2. **Roadmap** -- Svelte Flow node graph showing learning areas with completion-colored nodes
3. **ResourceList** -- Filterable resource catalog with checkboxes per area
4. **Dashboard** -- Aggregate stats: completion percentage, hours spent, current resource
5. **ProgressBar** -- Per-area completion derived from raw completion data

### Critical Pitfalls

1. **Over-engineering auth** -- Use a simple user selector (2 buttons). If you are reading JWT docs, stop.
2. **Building a CMS** -- Resources live in JSON files. Edit and redeploy. No admin panel.
3. **Complex progress tracking** -- Binary checkboxes only. No quiz scores, no spaced repetition.
4. **Roadmap visualization over substance** -- Build working list+checkboxes BEFORE the node graph.
5. **Not deploying until ready** -- Deploy hello-world to Vercel on day one.

## Implications for Roadmap

### Phase 1: Foundation and Core Tracking
**Rationale:** Everything depends on the data model and basic interaction loop. Deploy immediately.
**Delivers:** A working app that beats a spreadsheet for tracking progress.
**Addresses:** Resource catalog, user selector, checkboxes, progress bars, dashboard, persistence -- all table stakes.
**Avoids:** Over-engineering auth (Pitfall 1), complex backend (Pitfall 8), perfect taxonomy (Pitfall 7), not deploying early (Pitfall 10).

### Phase 2: Visual Roadmap
**Rationale:** Primary differentiator but depends on having content and tracking working first.
**Delivers:** Interactive node graph per area with completion-colored nodes, click-to-expand resource lists.
**Uses:** Svelte Flow for the node graph, learning-paths.json for node positions and edges.
**Avoids:** Visualization over substance (Pitfall 4). Only start after Phase 1 is deployed and in use.

### Phase 3: Polish and Quality of Life
**Rationale:** Refinements based on actual usage of Phases 1-2.
**Delivers:** Currently learning indicator, time estimates, side-by-side comparison, responsive polish.
**Avoids:** Demotivating comparisons (Pitfall 6) -- show individual progress positively, no rankings.

### Phase Ordering Rationale

- Data model and progress tracking are dependencies for everything else
- Deploying Phase 1 first gets real usage data before investing in the visual roadmap
- Svelte Flow integration is medium complexity and benefits from stable underlying data
- Phase 3 is deliberately vague -- let actual usage inform what to polish

### Research Flags

Phases likely needing deeper research during planning:
- **Phase 2:** Svelte Flow integration patterns, custom node components, responsive behavior on mobile. Newer library with fewer tutorials than React Flow.

Phases with standard patterns (skip research-phase):
- **Phase 1:** Standard SvelteKit app with localStorage. Well-documented, no unknowns.
- **Phase 3:** Standard UI polish. No research needed.

## Confidence Assessment

| Area | Confidence | Notes |
|------|------------|-------|
| Stack | HIGH | SvelteKit and Svelte Flow well-documented with official docs |
| Features | HIGH | Derived from project requirements, clear anti-features defined |
| Architecture | HIGH | localStorage + JSON for 2 users is a solved pattern |
| Pitfalls | HIGH | Universal small-project anti-patterns, well-documented |

**Overall confidence:** HIGH

### Gaps to Address

- **Svelte Flow mobile responsiveness:** Node graphs on small screens need testing. May need list fallback.
- **localStorage backup:** JSON export/import for backup should be considered.
- **Content curation:** The real work is curating quality AI resources -- a human task, not technical.

## Sources

### Primary (HIGH confidence)
- [Svelte Flow docs](https://svelteflow.dev/) -- API, custom nodes, examples
- [SvelteKit docs](https://svelte.dev/docs/kit) -- Framework reference
- localStorage Web API -- Universal browser support

### Secondary (MEDIUM confidence)
- [xyflow GitHub](https://github.com/xyflow/xyflow) -- Svelte Flow maturity
- [Supabase](https://supabase.com/) -- Upgrade path docs
- Domain patterns from Roadmap.sh, freeCodeCamp

---
*Research completed: 2026-06-20*
*Ready for roadmap: yes*
