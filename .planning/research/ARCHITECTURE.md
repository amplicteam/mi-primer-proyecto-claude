# Architecture Patterns

**Domain:** Interactive AI Learning Platform (2 users, curated resources)
**Researched:** 2026-06-20

## Recommended Architecture

**Single-page app with file-based data.** No backend server, no database. All data lives in JSON files committed to the repo, with localStorage as the runtime layer for per-user progress.

Why: 2 fixed users, ~50-200 curated resources, no auth complexity, deployed on Vercel/Netlify. A database is overkill. JSON files are editable by hand (easy to add/remove resources), version-controlled, and zero-cost.

```
src/
  components/        # UI components
    Roadmap.tsx       # Visual node graph
    Dashboard.tsx     # Stats and progress overview
    ResourceList.tsx  # Filterable resource catalog
    ProgressBar.tsx   # Per-area progress
    UserSwitcher.tsx  # Toggle between Dharrell/Jose
  data/
    resources.json    # All curated resources
    learning-paths.json  # Path definitions with node connections
  hooks/
    useProgress.ts    # Read/write progress from localStorage
    useStats.ts       # Compute dashboard statistics
  types/
    index.ts          # TypeScript interfaces
  pages/
    index.tsx         # Main app entry
```

### Component Boundaries

| Component | Responsibility | Communicates With |
|-----------|---------------|-------------------|
| `UserSwitcher` | Select active user (Dharrell/Jose) | Sets userId in context, all components react |
| `Roadmap` | Render visual node map of learning areas | Reads learning-paths.json, reads progress via useProgress |
| `ResourceList` | Show resources for selected area, mark complete | Reads resources.json, writes progress via useProgress |
| `Dashboard` | Show stats: % complete, hours, streak | Reads progress via useStats |
| `ProgressBar` | Per-area completion percentage | Reads progress via useProgress |

### Data Flow

```
resources.json (static)  ----+
learning-paths.json (static) +---> React App ---> Render UI
localStorage (per-user)  ----+         |
                                       v
                              User clicks checkbox
                                       |
                                       v
                              useProgress.ts writes to localStorage
                                       |
                                       v
                              All dependent components re-render
```

**No API calls. No server. Pure client-side.**

## Data Model

### resources.json

```typescript
interface Resource {
  id: string;              // "llm-prompt-eng-101"
  title: string;           // "Prompt Engineering Guide"
  type: "video" | "course" | "doc" | "article";
  url: string;             // External link
  area: AreaId;            // "llms" | "deep-learning" | "computer-vision" | "ml-fundamentals"
  pathNodeId: string;      // Which roadmap node this belongs to
  estimatedMinutes: number; // For dashboard stats
  source: string;          // "YouTube" | "Anthropic" | "Coursera" etc.
  order: number;           // Display order within node
}
```

### learning-paths.json

```typescript
interface LearningPath {
  id: AreaId;
  title: string;            // "LLMs y Prompting"
  description: string;
  nodes: PathNode[];
  edges: Edge[];             // Connections between nodes for visual graph
}

interface PathNode {
  id: string;               // "prompting-basics"
  title: string;            // "Fundamentos de Prompting"
  description: string;
  position: { x: number; y: number }; // For roadmap visualization
  level: "beginner" | "intermediate" | "advanced";
}

interface Edge {
  from: string;  // PathNode id
  to: string;    // PathNode id
}
```

### Progress (localStorage)

```typescript
// Key: `amplic-progress-${userId}`
interface UserProgress {
  userId: "dharrell" | "jose";
  completed: Record<string, CompletionEntry>; // resourceId -> entry
  lastActive: string; // ISO date
  streakDays: number;
}

interface CompletionEntry {
  completedAt: string; // ISO date
}
```

**Why localStorage, not a database:**
- Only 2 users on their own devices
- Data size is tiny (<50KB even with hundreds of resources)
- Zero infrastructure cost
- If a device is lost, re-checking boxes is trivial for this scale

**Optional upgrade path:** If they ever want cross-device sync, add a simple JSON file on a Supabase/Firebase row. But don't build this until needed.

## Patterns to Follow

### Pattern 1: Derived State via Hooks

All computed values (progress percentages, streak, hours) are derived from the raw completion records. Never store computed values.

```typescript
function useStats(userId: string) {
  const { completed } = useProgress(userId);
  const resources = useResources();
  
  const byArea = useMemo(() => {
    return areas.map(area => {
      const areaResources = resources.filter(r => r.area === area.id);
      const done = areaResources.filter(r => completed[r.id]);
      return {
        area: area.id,
        total: areaResources.length,
        completed: done.length,
        percent: Math.round((done.length / areaResources.length) * 100),
        hoursSpent: done.reduce((sum, r) => sum + r.estimatedMinutes, 0) / 60,
      };
    });
  }, [completed, resources]);
  
  return byArea;
}
```

### Pattern 2: User Context at the Top

Single React context provides the active user. All child components consume it.

```typescript
const UserContext = createContext<{ userId: string; setUserId: (id: string) => void }>();
```

No routing per user. Just a toggle/dropdown at the top of the page.

### Pattern 3: Static Data Import

Resources and paths are imported as static JSON at build time. No fetching, no loading states for content data.

```typescript
import resources from '../data/resources.json';
import paths from '../data/learning-paths.json';
```

## Anti-Patterns to Avoid

### Anti-Pattern 1: Building a Backend
**What:** Adding an API server, database, auth system
**Why bad:** Massive overhead for 2 users. Adds hosting costs, complexity, failure modes.
**Instead:** localStorage + static JSON. Upgrade only when there's a real need.

### Anti-Pattern 2: Over-Engineering the Roadmap Visualization
**What:** Building a custom graph rendering engine from scratch
**Why bad:** Time sink. Bugs with positioning, zooming, responsiveness.
**Instead:** Use React Flow for the node graph. It handles positioning, edges, zoom, pan, and is well-maintained.

### Anti-Pattern 3: Dynamic Resource Management UI
**What:** Building an admin panel to add/edit/delete resources
**Why bad:** Only 2 users who are also the developers. Editing JSON is faster.
**Instead:** Edit resources.json directly. Redeploy. Takes 2 minutes.

## Roadmap Visualization Approach

Use **React Flow** for the interactive node graph:
- Nodes = learning topics (e.g., "Prompting Basics", "RAG", "Transformers")
- Edges = prerequisites/suggested order
- Node color/opacity reflects completion status
- Click a node to expand its resource list

Each area (LLMs, Deep Learning, CV) is a separate graph/tab.

## Suggested Build Order

1. **Data model + JSON files** - Define resources.json and learning-paths.json structure, populate with initial content
2. **User context + progress hook** - localStorage read/write, user switching
3. **Resource list with checkboxes** - Core interaction: browse and mark complete
4. **Progress bars per area** - Visual feedback on completion
5. **Roadmap visualization** - React Flow node graph with completion status
6. **Dashboard with stats** - Hours, percentages, streak calculation
7. **Polish** - Responsive design, transitions, deploy

This order ensures each step is usable and testable before adding the next layer. The roadmap visualization (step 5) is the flashiest feature but depends on having the data model and progress system working first.

## Scalability Considerations

Not a concern. This app serves 2 people with <200 resources. The architecture is intentionally simple. If it ever needs to scale (unlikely), the upgrade path is:

1. Move progress to Supabase (free tier) for cross-device sync
2. Move resources.json to a CMS if non-technical editors need access (they don't)
3. Add real auth if more users join (they won't for this use case)

## Sources

- React Flow: established library for node-based UIs (HIGH confidence, widely used)
- localStorage API: standard Web API, universal browser support (HIGH confidence)
- Vercel/Netlify static hosting: standard for React SPAs (HIGH confidence)
