# Phase 1: Project Scaffold and Deploy - Research

**Researched:** 2026-06-20
**Domain:** SvelteKit project initialization, Tailwind CSS, Vercel deployment
**Confidence:** HIGH

## Summary

This phase creates a greenfield SvelteKit 2 project with Tailwind CSS, applies Amplic branding (colors, typography, landing page), and deploys to Vercel. The stack is mature and well-documented. SvelteKit 2.66 runs on Svelte 5.56, Tailwind 4.3 uses the new CSS-first configuration, and `@sveltejs/adapter-vercel` 6.3 handles deployment.

**Primary recommendation:** Use `npx sv create` to scaffold, add Tailwind via the SvelteKit CLI addon, configure Amplic brand tokens in `app.css`, build minimal landing, deploy via Vercel Git integration.

<user_constraints>
## User Constraints (from CONTEXT.md)

### Locked Decisions
- **Framework:** SvelteKit 2 (Svelte 5)
- **Styling:** Tailwind CSS
- **Hosting:** Vercel (free tier), Vercel subdomain initially
- **Structure:** By feature (`/roadmap`, `/catalog`, `/dashboard`, `/progress`)
- **Branding:** Azul Profundo #0E1B33, Azul Amplic #2563EB, Cian Senal #06B6D4, Gris Claro #F4F6FA; Poppins/Montserrat headings, Inter body
- **Landing:** Minimal Amplic-branded with logo, tagline "Amplificamos datos en decisiones", "Entrar" button

### Claude's Discretion
- Landing page layout and design details

### Deferred Ideas (OUT OF SCOPE)
- Custom domain
</user_constraints>

<phase_requirements>
## Phase Requirements

| ID | Description | Research Support |
|----|-------------|------------------|
| CORE-01 | Usuario puede acceder a la plataforma desde cualquier dispositivo via URL (deploy en Vercel) | SvelteKit + adapter-vercel + Vercel Git integration provides this out of the box |
</phase_requirements>

## Architectural Responsibility Map

| Capability | Primary Tier | Secondary Tier | Rationale |
|------------|-------------|----------------|-----------|
| Project scaffold | Build tooling | -- | Vite + SvelteKit CLI |
| Styling/branding | Browser/Client | -- | Tailwind CSS utility classes |
| Landing page | Browser/Client | Frontend Server (SSR) | SvelteKit SSR renders, browser displays |
| Deployment | CDN/Static + Edge | -- | Vercel serves with edge functions for SSR |

## Standard Stack

### Core
| Library | Version | Purpose | Why Standard |
|---------|---------|---------|--------------|
| @sveltejs/kit | 2.66.0 | Full-stack framework | [VERIFIED: npm registry] |
| svelte | 5.56.3 | UI framework | [VERIFIED: npm registry] |
| tailwindcss | 4.3.1 | Utility CSS | [VERIFIED: npm registry] |
| @sveltejs/adapter-vercel | 6.3.4 | Vercel deployment adapter | [VERIFIED: npm registry] |

### Supporting
| Library | Version | Purpose | When to Use |
|---------|---------|---------|-------------|
| @fontsource/inter | latest | Body font | Self-hosted web font |
| @fontsource/poppins | latest | Heading font | Self-hosted web font |

### Alternatives Considered
| Instead of | Could Use | Tradeoff |
|------------|-----------|----------|
| @fontsource | Google Fonts CDN | fontsource = no external requests, better privacy/performance |

**Installation:**
```bash
npx sv create amplic-learn --template minimal --types ts
cd amplic-learn
npx sv add tailwindcss
npm install @fontsource/inter @fontsource/poppins
```

## Package Legitimacy Audit

| Package | Registry | Age | Downloads | Source Repo | slopcheck | Disposition |
|---------|----------|-----|-----------|-------------|-----------|-------------|
| @sveltejs/kit | npm | 4+ yrs | millions/wk | github.com/sveltejs/kit | [ASSUMED] | Approved - official Svelte org |
| svelte | npm | 8+ yrs | millions/wk | github.com/sveltejs/svelte | [ASSUMED] | Approved - official |
| tailwindcss | npm | 7+ yrs | millions/wk | github.com/tailwindlabs/tailwindcss | [ASSUMED] | Approved - official |
| @sveltejs/adapter-vercel | npm | 4+ yrs | high | github.com/sveltejs/kit | [ASSUMED] | Approved - official Svelte org |
| @fontsource/inter | npm | 4+ yrs | high | github.com/fontsource/fontsource | [ASSUMED] | Approved - well-known project |
| @fontsource/poppins | npm | 4+ yrs | high | github.com/fontsource/fontsource | [ASSUMED] | Approved |

**Packages removed due to slopcheck [SLOP] verdict:** none
**Packages flagged as suspicious [SUS]:** none

*slopcheck was not run. All packages tagged [ASSUMED] but are well-known ecosystem packages from official organizations.*

## Architecture Patterns

### System Architecture Diagram

```
User (mobile/desktop)
    |
    v
[Vercel Edge/CDN] --> serves SSR HTML + static assets
    |
    v
[SvelteKit App]
    +-- /           --> Landing page (Amplic branding)
    +-- /catalog    --> (Phase 3)
    +-- /dashboard  --> (Phase 4)
    +-- /roadmap    --> (Phase 7)
    +-- /progress   --> (Phase 4)
```

### Recommended Project Structure
```
amplic-learn/
├── src/
│   ├── routes/
│   │   ├── +page.svelte          # Landing page
│   │   └── +layout.svelte        # Global layout with fonts
│   ├── lib/
│   │   ├── components/           # Shared components
│   │   └── styles/               # Brand tokens if needed
│   └── app.css                   # Tailwind + brand CSS variables
├── static/
│   └── logo.svg                  # Amplic logo
├── svelte.config.js
├── tailwind.config.ts            # (Tailwind v4 uses CSS config, this may be minimal)
└── vite.config.ts
```

### Pattern 1: Tailwind v4 CSS-First Config
**What:** Tailwind 4 uses `@theme` in CSS instead of `tailwind.config.js` for custom values.
**When to use:** Always with Tailwind 4+.
**Example:**
```css
/* app.css */
@import "tailwindcss";
@import "@fontsource/inter/400.css";
@import "@fontsource/inter/500.css";
@import "@fontsource/poppins/600.css";
@import "@fontsource/poppins/700.css";

@theme {
  --color-azul-profundo: #0E1B33;
  --color-azul-amplic: #2563EB;
  --color-cian-senal: #06B6D4;
  --color-gris-claro: #F4F6FA;
  --font-heading: "Poppins", sans-serif;
  --font-body: "Inter", sans-serif;
}
```
[ASSUMED - based on Tailwind v4 CSS-first approach]

### Pattern 2: SvelteKit Adapter Vercel
**What:** Set adapter in svelte.config.js
**Example:**
```javascript
// svelte.config.js
import adapter from '@sveltejs/adapter-vercel';
export default { kit: { adapter: adapter() } };
```
[ASSUMED - standard SvelteKit pattern]

### Anti-Patterns to Avoid
- **Don't use `tailwind.config.js` for theme in v4:** Use `@theme` in CSS instead
- **Don't use adapter-auto for production:** Explicitly use adapter-vercel for predictable builds

## Don't Hand-Roll

| Problem | Don't Build | Use Instead | Why |
|---------|-------------|-------------|-----|
| Font loading | Manual @font-face | @fontsource packages | Handles weights, subsets, preloading |
| CSS reset/base | Custom reset | Tailwind preflight | Already included |
| Deploy config | Manual Vercel config | adapter-vercel | Handles edge cases, streaming, ISR |

## Common Pitfalls

### Pitfall 1: Tailwind v4 Config Confusion
**What goes wrong:** Trying to use `tailwind.config.js` with custom colors/fonts when v4 expects CSS `@theme`
**Why it happens:** Most tutorials online still show v3 patterns
**How to avoid:** Use `@theme` block in app.css for all custom values
**Warning signs:** Custom colors not working, theme values not appearing

### Pitfall 2: Vercel Build Failing on SvelteKit
**What goes wrong:** Build fails because adapter-auto doesn't resolve properly
**Why it happens:** Default scaffold uses adapter-auto
**How to avoid:** Replace with `@sveltejs/adapter-vercel` explicitly in svelte.config.js
**Warning signs:** "Cannot find adapter" errors in Vercel build logs

### Pitfall 3: Font Not Loading
**What goes wrong:** Fonts render as fallback system fonts
**Why it happens:** @fontsource imports missing or not imported in root layout
**How to avoid:** Import font CSS in app.css or +layout.svelte, verify with DevTools
**Warning signs:** FOUT or system font visible

## Code Examples

### Landing Page Structure
```svelte
<!-- src/routes/+page.svelte -->
<div class="min-h-screen bg-gris-claro flex flex-col items-center justify-center">
  <img src="/logo.svg" alt="Amplic" class="w-48 mb-8" />
  <h1 class="font-heading text-4xl font-bold text-azul-profundo mb-4">
    Amplic
  </h1>
  <p class="font-body text-lg text-azul-profundo/70 mb-8">
    Amplificamos datos en decisiones
  </p>
  <a
    href="/catalog"
    class="bg-azul-amplic text-white px-8 py-3 rounded-lg font-body font-medium
           hover:bg-azul-amplic/90 transition-colors"
  >
    Entrar
  </a>
</div>
```
[ASSUMED - illustrative pattern]

## State of the Art

| Old Approach | Current Approach | When Changed | Impact |
|--------------|------------------|--------------|--------|
| tailwind.config.js | @theme in CSS (v4) | 2025 | Simpler config, CSS-native |
| Svelte 4 reactive | Svelte 5 runes ($state, $derived) | 2024 | New reactivity model |
| adapter-auto | Explicit adapter-vercel | Ongoing | More predictable deploys |

## Assumptions Log

| # | Claim | Section | Risk if Wrong |
|---|-------|---------|---------------|
| A1 | Tailwind v4 uses @theme in CSS for custom tokens | Architecture Patterns | Would need tailwind.config.js instead - low risk, easy fix |
| A2 | `npx sv create` is the current SvelteKit scaffolding command | Standard Stack | Would need different init command |
| A3 | @fontsource packages work with simple CSS imports | Supporting stack | Might need different import approach |

## Open Questions

1. **Amplic Logo**
   - What we know: Brand uses specific colors and "amplification" visual concept
   - What's unclear: Does a logo SVG file exist already, or must one be created?
   - Recommendation: Use text-based logo initially, replace with SVG when available

## Environment Availability

| Dependency | Required By | Available | Version | Fallback |
|------------|------------|-----------|---------|----------|
| Node.js | SvelteKit | Yes | 24.17.0 | -- |
| npm | Package install | Yes | 11.13.0 | -- |
| git | Version control + Vercel | Yes | 2.54.0 | -- |
| Vercel CLI | Deploy (optional) | No | -- | Use Vercel Git integration (recommended) |

**Missing dependencies with no fallback:** None
**Missing dependencies with fallback:** Vercel CLI not installed, but Git integration is the recommended deploy method anyway.

## Validation Architecture

### Test Framework
| Property | Value |
|----------|-------|
| Framework | Playwright (SvelteKit default for e2e) + Vitest (unit) |
| Config file | None yet - Wave 0 |
| Quick run command | `npm run test:unit` |
| Full suite command | `npm run test` |

### Phase Requirements - Test Map
| Req ID | Behavior | Test Type | Automated Command | File Exists? |
|--------|----------|-----------|-------------------|-------------|
| CORE-01 | App accessible via URL, renders landing | smoke/e2e | `npx playwright test tests/landing.spec.ts` | No - Wave 0 |

### Sampling Rate
- **Per task commit:** `npm run build` (verifies compilation)
- **Per wave merge:** `npm run build && npx playwright test`
- **Phase gate:** Successful Vercel deploy + manual URL check

### Wave 0 Gaps
- [ ] `playwright.config.ts` - e2e test config
- [ ] `tests/landing.spec.ts` - verifies landing page renders
- [ ] Vitest config (comes with sv create)

## Security Domain

### Applicable ASVS Categories

| ASVS Category | Applies | Standard Control |
|---------------|---------|-----------------|
| V2 Authentication | No | N/A - no auth in Phase 1 |
| V3 Session Management | No | N/A |
| V4 Access Control | No | N/A |
| V5 Input Validation | No | No user input in Phase 1 |
| V6 Cryptography | No | N/A |

### Known Threat Patterns for SvelteKit + Vercel

| Pattern | STRIDE | Standard Mitigation |
|---------|--------|---------------------|
| XSS via server-rendered content | Tampering | SvelteKit auto-escapes by default |
| Dependency supply chain | Tampering | Use well-known packages only |

No significant security concerns for this phase (static landing page, no user input).

## Sources

### Primary (HIGH confidence)
- npm registry - verified current versions of all packages
- Environment probes - confirmed Node 24, npm 11, git available

### Secondary (MEDIUM confidence)
- Training knowledge of SvelteKit 2 / Svelte 5 / Tailwind v4 patterns

### Tertiary (LOW confidence)
- Tailwind v4 @theme syntax details (A1) - needs verification during implementation

## Metadata

**Confidence breakdown:**
- Standard stack: HIGH - versions verified on npm registry
- Architecture: HIGH - standard SvelteKit patterns, greenfield
- Pitfalls: MEDIUM - Tailwind v4 patterns based on training data

**Research date:** 2026-06-20
**Valid until:** 2026-07-20 (stable, mature stack)
