---
phase: quick
plan: 260622-bly
type: execute
wave: 1
depends_on: []
files_modified:
  - amplic-learn/src/app.css
  - amplic-learn/src/lib/assets/logo.svg
  - amplic-learn/src/lib/assets/favicon.svg
  - amplic-learn/src/app.html
  - amplic-learn/src/lib/actions/motion.ts
  - amplic-learn/src/routes/+page.svelte
  - amplic-learn/src/routes/perfil/+page.svelte
  - amplic-learn/src/routes/(app)/+layout.svelte
  - amplic-learn/src/lib/components/NavBar.svelte
  - amplic-learn/src/routes/(app)/dashboard/+page.svelte
  - amplic-learn/src/routes/(app)/catalog/+page.svelte
  - amplic-learn/src/routes/(app)/roadmap/+page.svelte
  - amplic-learn/src/lib/components/ResourceRow.svelte
  - amplic-learn/src/lib/components/ProfileCard.svelte
  - amplic-learn/src/lib/components/ProgressBar.svelte
autonomous: false
requirements: [REDESIGN-01]

must_haves:
  truths:
    - "All pages render with the 3-color palette — no gradients, blobs, or emojis in UI"
    - "New monogram-A logo and matching favicon appear (Svelte default favicon gone)"
    - "Typography uses a distinctive display face + Inter body across all headings"
    - "Scroll/inView animations run on landing and key sections via the motion action"
  artifacts:
    - path: "amplic-learn/src/app.css"
      provides: "3-color palette + editorial typography tokens"
      contains: "@theme"
    - path: "amplic-learn/src/lib/actions/motion.ts"
      provides: "Svelte use:action animation helpers"
      exports: ["fadeInOnScroll"]
    - path: "amplic-learn/src/lib/assets/logo.svg"
      provides: "Monogram A + Amplic wordmark"
    - path: "amplic-learn/src/lib/assets/favicon.svg"
      provides: "Monogram A favicon"
  key_links:
    - from: "amplic-learn/src/routes/+page.svelte"
      to: "amplic-learn/src/lib/actions/motion.ts"
      via: "use:fadeInOnScroll"
      pattern: "use:fadeInOnScroll"
    - from: "amplic-learn/src/app.html"
      to: "amplic-learn/src/lib/assets/favicon.svg"
      via: "link rel=icon"
      pattern: "favicon"
---

<objective>
Complete visual redesign of amplic-learn toward an "invisible school" editorial aesthetic
(Stripe docs meets Linear): clean, confident, $5K-perceived. Replace the chaotic 7-color
palette + cliché bar logo + Poppins/Inter pairing + dark gradients/blobs/emojis with a
disciplined 3-color system, a monogram-A logo, an editorial display face, and tasteful
Motion-driven scroll animations.

Purpose: The current UI reads templated and unprofessional, undermining the goal of selling
AI services under the Amplic brand. A coherent, distinctive design raises perceived quality.

Output: Updated design tokens, new logo + favicon, a reusable motion action, and every page
and shared component restyled to the new system.
</objective>

<execution_context>
@$HOME/.claude/get-shit-done/workflows/execute-plan.md
@$HOME/.claude/get-shit-done/templates/summary.md
</execution_context>

<context>
@.planning/STATE.md
@./CLAUDE.md
@.claude/skills/frontend-design/SKILL.md

# Current design tokens (to be replaced)
@amplic-learn/src/app.css

<interfaces>
<!-- Motion is installed (motion v12.40.0). Use motion/mini vanilla API with Svelte use:action. -->
Pattern for amplic-learn/src/lib/actions/motion.ts:
```typescript
import { animate, inView } from "motion/mini";
export function fadeInOnScroll(node: HTMLElement) {
  inView(node, () => { animate(node, { opacity: [0, 1], y: [24, 0] }, { duration: 0.6 }); });
}
```

Current palette (app.css @theme) uses 8 colors: azul-profundo, azul-amplic, cian-senal,
gris-claro, violeta, naranja, esmeralda, rosa. Components reference these via Tailwind
classes (e.g. bg-azul-profundo, text-cian-senal, bg-violeta).

NavBar uses emoji link labels (📊📚🗺️) and 3 colored bars as a mini-logo.
Landing (+page.svelte) uses a 4-stop gradient background + 3 blur blobs + 🚀 emoji CTA.
(app)/+layout.svelte wraps content in a dark gradient background.
ProfileCard color comes from userStore.activeProfile.color (per-user accent) — keep that
data-driven accent but ensure it reads cleanly against the new neutral surfaces.
</interfaces>
</context>

<tasks>

<task type="auto">
  <name>Task 1: Establish the new design system — tokens, logo, favicon, motion action</name>
  <files>amplic-learn/src/app.css, amplic-learn/src/lib/assets/logo.svg, amplic-learn/src/lib/assets/favicon.svg, amplic-learn/src/app.html, amplic-learn/src/lib/actions/motion.ts</files>
  <action>
    Define the 3-color palette in app.css @theme: an ink/dark (e.g. near-black), a warm
    surface (off-white/paper), and a single accent. Name tokens semantically (--color-ink,
    --color-surface, --color-accent plus 1-2 muted neutrals for borders/secondary text).
    Remove the 8 legacy color tokens. Set typography: import a distinctive display face via
    @fontsource (a serif or grotesk — pick one already on npm, e.g. @fontsource/fraunces or
    @fontsource/space-grotesk; install if needed) for --font-heading, keep Inter for
    --font-body. Drop Poppins. Set body background to the surface token, default text to ink.

    Create a new logo.svg: a clean monogram "A" mark + "Amplic" wordmark in the display face
    style (single-color, ink). Replace favicon.svg with a standalone monogram-A mark (no Svelte
    default). Wire the favicon in app.html (link rel="icon" href to the favicon asset). Remove
    any leftover Svelte branding.

    Create amplic-learn/src/lib/actions/motion.ts exporting fadeInOnScroll (and optionally a
    staggered variant) using motion/mini inView+animate per the interface pattern. Respect
    prefers-reduced-motion by skipping animation when set.
  </action>
  <verify>
    <automated>cd amplic-learn && npm run build</automated>
  </verify>
  <done>Build succeeds; app.css has exactly 3 brand colors + neutrals, no Poppins/legacy tokens; logo.svg and favicon.svg are the new monogram; motion.ts exports fadeInOnScroll.</done>
</task>

<task type="auto">
  <name>Task 2: Apply the new system to landing, profile, app shell, and navbar</name>
  <files>amplic-learn/src/routes/+page.svelte, amplic-learn/src/routes/perfil/+page.svelte, amplic-learn/src/routes/(app)/+layout.svelte, amplic-learn/src/lib/components/NavBar.svelte, amplic-learn/src/lib/components/ProfileCard.svelte</files>
  <action>
    Landing (+page.svelte): remove the 4-stop gradient and all 3 blur blobs; use a flat surface
    background with ink typography and the editorial display face for the headline. Remove the
    🚀 emoji from the CTA — use a clean text button (accent or ink). Apply use:fadeInOnScroll to
    the headline/CTA block. Drop the brightness-0 invert hack — use the ink logo directly.

    Profile (perfil/+page.svelte) and ProfileCard.svelte: restyle to the neutral surface +
    editorial type. Keep each profile's data-driven accent color, but as a small accent
    (avatar/ring), not a full card fill — ensure contrast on the new surface.

    App shell ((app)/+layout.svelte): replace the dark gradient background with the flat
    surface/ink scheme used app-wide.

    NavBar.svelte: remove emoji from link labels (📊📚🗺️) — text-only labels, optionally with
    lucide-svelte icons (already a dep). Replace the 3 colored bars mini-logo with the new
    monogram-A. Recolor active/hover states to the ink/accent system instead of white/10 on dark.
  </action>
  <verify>
    <automated>cd amplic-learn && npm run build && grep -rL "📊\|📚\|🗺️\|🚀\|blur-3xl\|brightness-0 invert" src/routes/+page.svelte src/lib/components/NavBar.svelte</automated>
  </verify>
  <done>Build passes; landing has no gradient/blobs/emoji; navbar has no emoji and uses the monogram; layout uses flat surface; profile accents read cleanly.</done>
</task>

<task type="auto">
  <name>Task 3: Apply the new system to dashboard, catalog, roadmap, and remaining components</name>
  <files>amplic-learn/src/routes/(app)/dashboard/+page.svelte, amplic-learn/src/routes/(app)/catalog/+page.svelte, amplic-learn/src/routes/(app)/roadmap/+page.svelte, amplic-learn/src/lib/components/ResourceRow.svelte, amplic-learn/src/lib/components/ProgressBar.svelte</files>
  <action>
    Dashboard: restyle cards to the editorial surface (subtle borders over heavy shadows on
    dark). Recolor chart.js datasets (doughnut/bars) to the 3-color palette — accent + neutrals,
    no violeta/naranja/esmeralda/rosa. Apply use:fadeInOnScroll to card sections.

    Catalog (+page.svelte) and ResourceRow.svelte: neutral surface, editorial headings, accent
    used sparingly for active/CTA states. No emojis; use lucide-svelte icons if iconography is
    needed.

    Roadmap (+page.svelte): align Svelte Flow node/edge styling and surrounding chrome with the
    new palette and type. Keep Svelte Flow functional; restyle node cards to ink/surface/accent.

    ProgressBar.svelte: recolor track + fill to neutral track + accent fill (or the per-user
    accent where progress is user-scoped). Remove any legacy color references.

    Final sweep: grep the whole src tree for legacy color tokens and emojis; replace any
    stragglers so nothing references the removed palette.
  </action>
  <verify>
    <automated>cd amplic-learn && npm run build && grep -rn "azul-amplic\|cian-senal\|azul-profundo\|violeta\|naranja\|esmeralda\|rosa\|font-heading.*Poppins\|📊\|📚\|🗺️" src/ || echo "no legacy references"</automated>
  </verify>
  <done>Build passes; dashboard/catalog/roadmap/components use the new system; chart colors use the palette; no legacy color tokens or emojis remain in src/.</done>
</task>

<task type="checkpoint:human-verify" gate="blocking">
  <what-built>Complete visual redesign applied across all pages and components, plus new logo/favicon and scroll animations.</what-built>
  <how-to-verify>
    1. Run `cd amplic-learn && npm run dev` and open the local URL.
    2. Landing: confirm flat surface, editorial headline, no gradient/blobs, text-only CTA, fade-in animation on scroll/load.
    3. Browser tab: confirm the favicon is the new monogram-A (not the Svelte default).
    4. Profile, dashboard, catalog, roadmap, navbar: confirm the 3-color palette, no emojis, consistent editorial type, monogram logo in navbar.
    5. Confirm charts and progress bars use the new palette and Svelte Flow roadmap still works.
  </how-to-verify>
  <resume-signal>Type "approved" or describe visual issues to fix.</resume-signal>
</task>

</tasks>

<verification>
- `npm run build` succeeds.
- No legacy color tokens (azul-amplic, cian-senal, azul-profundo, violeta, naranja, esmeralda, rosa) or Poppins remain in src/.
- No emojis or blur blobs or gradient backgrounds in UI.
- Favicon is the new monogram; logo updated everywhere.
- fadeInOnScroll wired on landing.
</verification>

<success_criteria>
Every page (landing, perfil, dashboard, catalog, roadmap) and shared component renders in the
3-color editorial system with the new logo/favicon and motion animations, build passes, and the
human verification checkpoint is approved.
</success_criteria>

<output>
Create `.planning/quick/260622-bly-redesign-visual-completo-de-amplic-learn/260622-bly-SUMMARY.md` when done.
</output>
