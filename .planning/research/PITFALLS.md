# Domain Pitfalls

**Domain:** AI Learning Platform / Personal Course Tracker
**Researched:** 2026-06-20

## Critical Pitfalls

Mistakes that cause rewrites or abandonment.

### Pitfall 1: Over-Engineering Authentication and User Management

**What goes wrong:** Building a full auth system (JWT, OAuth, password reset, email verification) for a platform with exactly 2 fixed users. Weeks spent on infrastructure that adds zero learning value.
**Why it happens:** Tutorials and boilerplate projects assume multi-user SaaS. Developers follow patterns blindly.
**Consequences:** Delayed launch by weeks. Complex state management. Deployment headaches with token refresh, session expiry. The platform never ships.
**Prevention:** Use a simple hardcoded user selector or basic PIN. No passwords, no OAuth. Two buttons: "Dharrell" / "Jose". Store progress keyed by user ID in the database.
**Detection:** If you're reading docs about JWT tokens or bcrypt for this project, stop.
**Phase:** Phase 1 (foundation). Decide this on day one.

### Pitfall 2: Building a CMS Instead of a Learning Platform

**What goes wrong:** Spending all effort on admin panels to add/edit/delete resources, drag-and-drop reordering, rich text editors, image uploads -- instead of actually curating content and tracking progress.
**Why it happens:** "The system should be updatable" gets interpreted as "build a full CMS." For 2 users managing ~50-100 resources, this is massive over-engineering.
**Consequences:** Months building CRUD interfaces nobody uses. The actual learning experience (the product) gets neglected.
**Prevention:** Resources live in a JSON/YAML file or simple database seed. To add a resource, edit the file and redeploy. A code-level update takes 2 minutes and is perfectly adequate for 2 users.
**Detection:** If you're building an admin dashboard before the learning dashboard, priorities are inverted.
**Phase:** Phase 1. Define the content model as static data first.

### Pitfall 3: Complex Progress Tracking That Drifts From Reality

**What goes wrong:** Building elaborate tracking (time spent, quiz scores, spaced repetition, AI-assessed comprehension) when users just need "did I watch this video? yes/no." The complexity discourages honest tracking -- users stop updating because it's tedious.
**Why it happens:** Inspiration from platforms like Coursera/Duolingo that have teams of engineers. Feature envy.
**Consequences:** Users mark things done to clear notifications rather than because they learned. Progress bars become meaningless. Motivation drops because the tracking feels like homework.
**Prevention:** Start with binary completion (done/not done) per resource. A checkbox. That is the MVP. Add richer tracking only if the simple version feels insufficient after weeks of use.
**Detection:** If the progress model has more than 3 states (not started, in progress, complete), it's probably too complex for v1.
**Phase:** Phase 1-2. Ship binary tracking first.

### Pitfall 4: Roadmap Visualization Over Substance

**What goes wrong:** Spending weeks on a beautiful interactive node graph (D3.js, React Flow, custom SVG) for the "roadmap visual tipo mapa con nodos conectados" before the content and tracking work. The visualization becomes the project instead of the learning.
**Why it happens:** Visual roadmaps look impressive in mockups. They're fun to build. But they're hard to build well and even harder to make responsive.
**Consequences:** Complex drag/zoom/pan interactions that break on mobile. Hours debugging SVG rendering. The actual content behind the nodes is an afterthought.
**Prevention:** Phase 1: simple ordered list/cards grouped by area. Phase 2: add a basic visual map using a proven library only after content and tracking are solid. A well-organized list with progress indicators is more useful than a buggy interactive graph.
**Detection:** If you're importing D3.js before you have 10 resources with working checkboxes, reprioritize.
**Phase:** Phase 2-3. Visual roadmap is a differentiator, not table stakes.

## Moderate Pitfalls

### Pitfall 5: Stale Resource Links and Content Rot

**What goes wrong:** YouTube videos get deleted, courses change URLs, documentation restructures. Links break silently. Users click a resource and hit a 404.
**Prevention:** Keep resources in a single data file so broken links are easy to audit. Include a "last verified" date. Periodically (monthly) click through resources. Do NOT build automated link checking for v1 -- just make manual checking easy.
**Phase:** Phase 2. Add "last verified" metadata after initial content is loaded.

### Pitfall 6: Motivation Features That Backfire

**What goes wrong:** Adding streaks, daily goals, or comparative progress (showing one founder is ahead of the other) creates pressure and guilt rather than motivation. Missed streaks are demotivating. Comparisons breed resentment.
**Prevention:** Show individual progress without comparison. No streaks -- show total completed, not consecutive days. Frame progress positively ("12 of 30 resources completed") not negatively ("18 remaining").
**Phase:** Phase 2. Design dashboard stats carefully.

### Pitfall 7: Trying to Organize Content Perfectly Before Starting

**What goes wrong:** Spending weeks debating taxonomy: should "Transformers" go under LLMs or Deep Learning? Should prompt engineering be its own area? Analysis paralysis on categorization prevents shipping.
**Prevention:** Use the 4 areas already defined in PROJECT.md. Accept that some resources span multiple areas. Tag with a primary area and ship. Reorganize later based on actual usage.
**Detection:** If you've spent more than 1 hour on content organization without writing any code, stop and ship the imperfect version.
**Phase:** Phase 1. Use the existing area structure as-is.

### Pitfall 8: Choosing a Complex Backend for Simple Data

**What goes wrong:** Setting up PostgreSQL, Prisma, migrations, Docker for storing ~100 resources and ~200 completion records (100 resources x 2 users). The data model is trivially simple.
**Prevention:** Use a serverless database (Supabase, Firebase, or even localStorage + JSON export for backup). The total data for this project fits in a single JSON file. Pick the simplest persistence that supports two users accessing from different devices.
**Phase:** Phase 1. Database decision is day-one.

## Minor Pitfalls

### Pitfall 9: Premature Mobile App Aspirations

**What goes wrong:** Building with React Native or Flutter "in case we want a mobile app later" instead of just making a responsive web app.
**Prevention:** Already correctly scoped as out-of-scope in PROJECT.md. A responsive web app with good mobile CSS is sufficient. PWA (add to home screen) covers the mobile use case.
**Phase:** N/A -- already handled.

### Pitfall 10: Not Deploying Until "It's Ready"

**What goes wrong:** Building locally for weeks. When deployment finally happens, environment issues (env vars, CORS, database connections) eat days.
**Prevention:** Deploy a hello-world to Vercel/Netlify in Phase 1, day one. Every feature ships to production immediately. Continuous deployment from the start.
**Phase:** Phase 1, literally first task.

### Pitfall 11: Scope Creep Into Social/Collaborative Features

**What goes wrong:** "What if we add comments on resources?" "What if we can share notes?" "What about a chat?" Two users do not need in-app collaboration. They sit next to each other (or use WhatsApp).
**Prevention:** If a feature requires real-time sync, WebSockets, or notification systems, it's out of scope. Communicate about learning through existing channels.
**Phase:** All phases. Constant vigilance.

## Phase-Specific Warnings

| Phase Topic | Likely Pitfall | Mitigation |
|-------------|---------------|------------|
| Foundation/Setup | Over-engineering auth (#1), complex backend (#8) | Simplest possible: user selector + serverless DB |
| Content Loading | Perfect taxonomy (#7), building CMS (#2) | JSON file, 4 areas from PROJECT.md, edit-and-redeploy |
| Progress Tracking | Complex tracking states (#3) | Binary checkboxes only |
| Visual Roadmap | Visualization over substance (#4) | Lists first, visual map in later phase |
| Dashboard/Stats | Demotivating comparisons (#6) | Individual progress, positive framing |
| Ongoing Maintenance | Content rot (#5) | "Last verified" dates, easy-to-audit data file |

## Sources

- Training data: patterns from failed learning platform projects, common over-engineering mistakes in small-team tools
- PROJECT.md: project scope and constraints directly inform pitfall severity
- Confidence: HIGH for pitfalls 1-4 (universal small-project anti-patterns), MEDIUM for 5-6 (domain-specific), HIGH for 7-11 (well-documented scope creep patterns)
