# Notion Reorganization Plan

## Current Problems

1. **4-level hierarchy is too deep**: Topic Groupings → Topics → Projects → Tasks adds cognitive overhead
2. **Confusion between ongoing and finite**: "Guitar" and "Shambhala 2025" are fundamentally different but treated similarly
3. **Documents vs Knowledge overlap**: Book notes (like Atomic Habits) are reference material but belong contextually under interests
4. **Multiple archive databases**: Suggests the system has been reworked multiple times without cleanup
5. **Scattered views**: Multiple views of the same databases spread across Home Dashboard

## Core Distinctions

| Type | Description | Examples | Completable? |
|------|-------------|----------|--------------|
| **Interest** | Ongoing area of life/hobby | Guitar, DJ, Habit Formation, 3D Modeling | Never |
| **Project** | Finite goal with tasks | Shambhala 2025, Game Jam, specific learning goals | Yes |
| **Task** | Action item within a project | "Book restaurant", "Fix bug in auth" | Yes |
| **Log** | Record of activity/experience | Date nights, practice sessions, workouts | N/A (it happened) |
| **Document** | Life admin reference | Insurance, Tax, How-tos, Resumes | N/A |

**Key insight**: Book notes and learnings live under their relevant Interest (not in Documents). Documents = life admin only.

## Tasks vs Logs

| | Tasks | Logs |
|---|-------|------|
| Feeling | Obligation, pressure | Accomplishment, pride |
| Direction | Forward-looking | Backward-looking |
| Goal | Empty the list | Fill the list |
| Mindset | "What do I need to do?" | "What have I done?" |

**Tasks** are for project work - discrete actions you complete and move on from.

**Logs** are for ongoing engagement - records of activity you want to look back on. They function as a "Done List" which is motivational rather than anxiety-inducing.

Examples of Logs:
- Date nights with relationship reflections
- Guitar practice sessions (what you worked on)
- Creative sessions (drawing, DJ sets, writing)
- Workouts, meditation, reading

## Task → Log Workflow

Some tasks naturally lead to logs. For these, use **task templates with a "Create Log" button**.

```
Task: "Plan date night" (created from template)
       ↓ plan the date
       ↓ date happens
       ↓ click "Create Log" button in task
Log:  "Date: [name]" (created with date pre-filled)
       ↓ add notes, reflections
Task: ✓ marked complete
```

**Which tasks get the button?**
- Date night planning → Yes (creates Date log)
- Practice reminders → Maybe (if you want to log practice)
- "Fix auth bug" → No (just a task, no log needed)

**Button behavior:**
- Creates new Log entry in Logs database
- Pre-fills: Date, Interest (if known), Type
- Optionally marks the Task complete

**Task templates with buttons:**
- 📅 Date Night Planning
- 🎸 Practice Session (optional)
- Other recurring activities worth logging

## Proposed Structure

```
Interests (top-level pages, fully customizable)
    └── Guitar (page)
            └── Notes, resources, tabs, whatever
            └── [Linked view: Projects where Interest = Guitar]
            └── [Linked view: Logs where Interest = Guitar] ← practice history!
    └── Habit Formation (page)
            └── Atomic Habits (book notes - stays here)
            └── Methods, reflections
            └── Habit tracking database
    └── Relationship (page)
            └── Notes, love languages, reflections
            └── [Linked view: Logs where Type = Date] ← date history!
    └── DJ (page)
    └── 3D Modeling (page)
    └── etc.

Projects (flat database, central location)
    └── Properties:
        - Name
        - Interest (relation, optional)
        - Status (Active / Complete / On Hold)
        - Tasks (relation)
    └── Views:
        - All Projects
        - Active Projects
        - By Interest (grouped)

Tasks (flat database)
    └── Properties:
        - Name
        - Project (relation)
        - Due Date
        - Complete (checkbox)

Logs (flat database - "Done List")
    └── Properties:
        - What (title)
        - Date
        - Interest (select) - Guitar, Relationship, DJ, etc.
    └── Views:
        - "Done This Week" - all recent logs (motivational Done List)
        - "Guitar Log" - filtered by Interest
        - "Date History" - filtered by Interest = Relationship
        - "By Year" - for annual review

Documents (life admin reference, unchanged)
    └── Insurance, Tax, How-tos, etc.
```

## Key Principles

1. **Interests are top-level pages** - not database entries. This allows full customization of each interest's page layout.

2. **Projects are a flat database** with an optional relation to Interest. Grouping by interest happens through views, not hierarchy.

3. **Linked views on Interest pages** let you see related projects/tasks without nesting. The Guitar page shows Guitar projects, but those projects live in the central Projects database.

4. **No forced hierarchy** - a project without an interest is fine. It just lives in the main Projects list.

5. **Book notes stay contextual** - Atomic Habits lives under Habit Formation because that's where you'd look for it. Documents is for life admin only.

6. **Logs are separate from Tasks** - Tasks are obligations (forward-looking, empty the list). Logs are records of engagement (backward-looking, fill the list). Date nights, practice sessions, and workouts are Logs, not Tasks.

7. **Logs link to Interests** - Each Interest page can show its activity history via linked views. "What have I done with Guitar this year?" becomes easy to answer.

## Home Page Design

The home page serves as a clean jumping-off point:

```
┌─────────────────────────────────────────────────────────┐
│  🏠 Home                                                │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  📋 TASKS                    ✅ DONE THIS WEEK          │
│  ┌─────────────────────┐     ┌─────────────────────┐    │
│  │ □ Fix auth bug      │     │ ❣️ Date: Raku        │    │
│  │ □ Book dentist      │     │ 🎸 Guitar: scales    │    │
│  │ □ Review PR         │     │ 🎨 Drew for 1hr      │    │
│  │ □ Plan date night   │     │ 🏋️ Gym: legs         │    │
│  └─────────────────────┘     └─────────────────────┘    │
│                                                         │
│  🎯 INTERESTS (jump into something)                     │
│  ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐           │
│  │ 🎸     │ │ 🎨     │ │ 💛     │ │ 🎧     │           │
│  │Guitar  │ │Sketching│ │Relat.  │ │ DJ     │           │
│  └────────┘ └────────┘ └────────┘ └────────┘           │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

**Tasks**: What needs doing (forward-looking, obligations)
**Done This Week**: What you've accomplished (backward-looking, motivational)
**Interests**: Quick access to dive into something

## What This Eliminates

- Topic Groupings database (not needed)
- The "Topics" database (replaced by Interest pages)
- Milestones database (was already being removed)
- Multiple scattered views (consolidate)
- Date entries mixed into Tasks (move to Logs)

## Migration Steps (TBD)

1. [ ] Create "📦 Databases" page to house all databases
2. [ ] Create/move databases into Databases page:
   - [ ] Projects (simplify: remove Topic relation, add Interest relation)
   - [ ] Tasks (keep existing, clean up properties)
   - [ ] Logs (new database)
3. [ ] Create new Interest pages at top level
4. [ ] Move content from old Topic database entries into new Interest pages
5. [ ] Migrate "Date:" entries from Tasks to Logs
6. [ ] Create Task templates with "Create Log" buttons:
   - [ ] Date Night Planning template
   - [ ] Other log-worthy task templates as needed
7. [ ] Add linked views to each Interest page (Projects + Logs)
8. [ ] Update Home Dashboard to reflect new structure (Tasks + Done This Week + Interests)
9. [ ] Clean up old databases (Topic Groupings, Topics, archives)
10. [ ] Hide/tuck away Databases page in sidebar

## Open Questions

(None remaining)

## Resolved Decisions

- **Task → Log workflow**: Use button on specific task templates (not all tasks). Button creates Log entry with pre-filled fields.
- **Logs don't have "Planned" status**: Tasks handle the planning phase. Logs are only created after the activity happens (via button).
- **Topic Groupings**: Removed. Interests are top-level pages. If grouping is needed, nest Interest pages under a parent page.
- **Database location**: All databases live in a dedicated "📦 Databases" page, accessed via linked views elsewhere.
- **Interest linking**: Use Select property (not relation) for simplicity. Logs and Projects have an "Interest" dropdown. Add new options as needed when creating new Interest pages.

```
📦 Databases (page - hidden or tucked in sidebar)
    └── Projects (database) - has Interest select property
    └── Tasks (database)
    └── Logs (database) - has Interest select property
```
