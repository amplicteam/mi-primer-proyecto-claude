# Feature Landscape

**Domain:** Personal AI learning roadmap/course tracker (2-person team)
**Researched:** 2026-06-20

## Table Stakes

Features that make this useful at all. Without these, it's just a list of links.

| Feature | Why Expected | Complexity | Notes |
|---------|--------------|------------|-------|
| Resource catalog per topic area | Core unit of content — videos, courses, docs organized by AI area | Low | JSON/data file with title, URL, type, area |
| Checkbox completion per resource | Minimum viable tracking — "did I do this?" | Low | Per-user boolean state |
| Progress bar per area | Visual feedback on how far along each topic area is | Low | Derived: completed/total per area per user |
| Two user profiles with independent progress | The whole point — Dharrell and Jose track separately | Low | Simple user selector, no auth needed (just pick name) |
| Responsive web layout | Must work on phone and laptop | Low | Standard CSS, no native app |
| Dashboard with overall progress | At-a-glance view: where am I across all areas? | Low | Aggregate of per-area progress |
| Persistent state | Progress must survive page refresh | Low | localStorage or simple DB |
| Area/topic organization | Resources grouped by LLMs, Deep Learning, CV, ML Fundamentals | Low | Static structure, defined in data |

## Differentiators

Nice-to-haves that make it genuinely enjoyable to use vs a spreadsheet.

| Feature | Value Proposition | Complexity | Notes |
|---------|-------------------|------------|-------|
| Visual roadmap with connected nodes | Makes learning path feel like a journey, shows dependencies | Medium | Library like React Flow or simple SVG/CSS nodes |
| Learning streak tracker | Motivation — "I've studied 5 days in a row" | Low | Track last-completed date, calculate streak |
| Time/hours estimate per resource | Helps plan study sessions — "I have 30 min, what can I do?" | Low | Manual metadata per resource |
| Side-by-side comparison view | See Dharrell vs Jose progress at a glance | Low | Simple dual-column or toggle view |
| Notes per resource | Jot down key takeaways while learning | Medium | Text field per resource per user, needs more storage |
| Resource difficulty tags | Know what's beginner vs advanced at a glance | Low | Metadata field |
| "Currently learning" indicator | Quick resume — what was I working on? | Low | Track last-active resource per user |
| Suggested next resource | Based on completion, suggest what to do next | Low | Simple logic: next incomplete in sequence |
| Weekly/monthly progress stats | "This week you completed 3 resources" | Medium | Needs timestamp tracking on completions |

## Anti-Features

Things to deliberately NOT build. Critical for a 2-person internal tool.

| Anti-Feature | Why Avoid | What to Do Instead |
|--------------|-----------|-------------------|
| User authentication / login system | Only 2 fixed users, auth adds complexity for zero value | Simple name selector (click "Dharrell" or "Jose") |
| Badges / achievements / gamification | Over-engineering for 2 people who already have business motivation | Streak counter is enough motivation |
| Leaderboard / competition features | Could create unhealthy dynamics between co-founders | Side-by-side view without ranking |
| YouTube API integration | OAuth complexity, quota limits, maintenance burden | Manual curation with direct links |
| Video player embedding | Copyright issues, layout complexity, just link out | Open in new tab links |
| Admin panel / CMS | 2 users = 2 developers, edit data files directly | Resources defined in code/JSON, update via git push |
| Comments / social features | They sit next to each other, just talk | Notes field per resource is sufficient |
| Search functionality | With ~50-100 curated resources, browsing by area is faster | Good category organization |
| Email notifications / reminders | Over-engineering, they can bookmark the site | None needed |
| Mobile app | Responsive web covers this | Standard responsive CSS |
| Multi-language support | Both speak Spanish and English, pick one UI language | Spanish UI with English resource titles |
| Analytics / telemetry | Internal tool, no need to track usage patterns | Dashboard progress stats are enough |

## Feature Dependencies

```
Resource catalog (data model) --> Everything else depends on this
  --> Checkbox completion --> Progress bar per area --> Dashboard
  --> User profiles --> Per-user state for all above
  --> Visual roadmap (needs area/topic structure)

Timestamp tracking on completions --> Streak tracker
                                  --> Weekly/monthly stats
```

## MVP Recommendation

**Phase 1 — Core (ship in days, not weeks):**
1. Resource catalog organized by 4 AI areas
2. User selector (Dharrell / Jose)
3. Checkbox completion per resource per user
4. Progress bar per area
5. Simple dashboard with overall completion %
6. localStorage persistence

**Phase 2 — Polish:**
1. Visual roadmap with connected nodes
2. Streak tracker
3. "Currently learning" indicator
4. Time estimates per resource

**Defer indefinitely:**
- Notes per resource (use a separate note-taking app)
- Weekly/monthly stats (premature until there's enough data)
- Any backend/database (localStorage is fine for 2 users on their own devices; consider JSON export/import for backup)

## Key Insight

This is NOT a SaaS product. It's a personal tool for 2 motivated co-founders. Every feature decision should pass the test: "Is this faster than a Google Sheet?" If a feature doesn't clearly beat the spreadsheet experience, skip it. The visual roadmap and per-person progress tracking are the two things that make this worth building as a web app instead of using a spreadsheet.

## Sources

- Project requirements from PROJECT.md
- Domain knowledge of learning platforms (Roadmap.sh, freeCodeCamp, Coursera progress tracking patterns)
- Out-of-scope decisions already validated by stakeholders in PROJECT.md
