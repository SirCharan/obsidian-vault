---
title: "Start Here - Your Second Brain"
type: guide
tags:
  - guide
---

# Welcome to Your Second Brain

This vault has been set up as a complete Personal Knowledge Management (PKM) system optimized for your meeting-heavy founder workflow. Here's everything you need to know.

---

## How This Vault is Organized (PARA Method)

| Folder | Purpose | Examples |
|--------|---------|---------|
| **1-Projects/** | Active projects with deadlines | Stocky, Timelock, Fuze, Fundraising |
| **2-Areas/** | Ongoing responsibilities | Leadership, Product, Hiring, Partnerships |
| **3-Resources/** | Reference material by topic | DeFi, Crypto-Markets, AI-ML |
| **4-Archive/** | Completed/inactive items | Move finished projects here |
| **People/** | Notes on key contacts | Auto-generated from your meetings |
| **MOCs/** | Maps of Content (index pages) | Stocky MOC, Fundraising MOC |
| **Meetings/** | Uncategorized meeting notes | 1-on-1, Strategy, External, Interviews |
| **Daily/** | Daily notes | One per day, linked to meetings & tasks |
| **Templates/** | Reusable templates | Meeting Note, Person, Project, etc. |

**Rule of thumb:** If it has a deadline, it's a **Project**. If it's ongoing, it's an **Area**. If it's reference, it's a **Resource**. If it's done, it's **Archive**.

---

## Install These Plugins (One-Time Setup)

Go to **Settings > Community Plugins > Browse** and install:

### Must-Have

| Plugin | Why You Need It |
|--------|----------------|
| **Templater** | Powers all templates (date functions, auto-fill). After installing: Settings > Templater > Template Folder = `Templates` |
| **Dataview** | Makes your MOCs and Person notes dynamic — auto-populates meeting lists, task rollups |
| **Tasks** | Enables `- [ ] #task` checkboxes with due dates across your vault |
| **Calendar** | Visual calendar in the sidebar — click any day to open/create a daily note |
| **Periodic Notes** | Auto-creates daily notes. Settings: Daily Note Folder = `Daily`, Template = `Templates/Daily Note.md` |

### Nice-to-Have

| Plugin | Why |
|--------|-----|
| **Advanced Tables** | Tab-to-navigate markdown tables |
| **Obsidian Git** | Auto-backup your vault to a git repo |
| **Smart Connections** | AI-powered "related notes" suggestions |

### Enable Core Plugins

Go to **Settings > Core Plugins** and enable:
- **Daily Notes** (set folder to `Daily/`)
- **Graph View** (already enabled)
- **Quick Switcher** (Cmd+O to jump to any note)
- **Backlinks** (see what links to the current note)
- **Tags** (tag pane in sidebar)

---

## Daily Workflow

### Morning (2 min)
1. **Cmd+O** → Open today's Daily Note (auto-created by Periodic Notes)
2. Write your 1-3 focus items for the day
3. Review tasks due today (auto-populated by Dataview)

### During Meetings
- Granola captures everything automatically
- Notes sync to your vault via the migration script or plugin

### End of Day (5 min)
1. Open your Daily Note
2. Fill in the "End of Day Review" section
3. Process any new Granola meeting notes (review summaries, check action items)

---

## Weekly Review Workflow (15-20 min)

1. Create a new note from `Templates/Weekly Review.md`
2. Review completed tasks (auto-populated)
3. Review open tasks — reprioritize or defer
4. Scan this week's meeting notes — any patterns or insights?
5. Update MOCs if new themes emerged
6. Archive completed projects

---

## How Wikilinks Work

- Type `[[` to create a link to any note
- `[[Person Name]]` links to their Person note
- `[[Stocky]]` links to the Stocky MOC
- Links create connections visible in **Graph View** (click the graph icon)
- **Backlinks** (right sidebar) show every note that links to the current one

---

## How Granola Notes Were Migrated

Your 209 Granola meeting notes have been imported:
- **Recent notes (last 3 months):** AI-enriched with summaries, action items, key insights, and atomic ideas
- **Older notes:** Basic import with content and auto-categorization
- **People notes:** Auto-created for contacts with 2+ meetings
- **MOCs:** Auto-generated for Stocky, Timelock, Fuze, Fundraising, and Monad

Check `_REVIEW_CATEGORIZATION.md` for any notes that need manual re-categorization.

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| **Cmd+O** | Quick Switcher (jump to any note) |
| **Cmd+P** | Command Palette |
| **Cmd+E** | Toggle edit/preview mode |
| **Cmd+Click** | Open link in new tab |
| **Cmd+Shift+F** | Search entire vault |
| `[[` | Start a wikilink |
| `#` | Start a tag |

---

## Tips for Founders

1. **Link aggressively.** Every person, project, and concept should be a `[[wikilink]]`. The Graph View rewards this.
2. **Use tags for status.** `#active`, `#blocked`, `#done` on action items.
3. **Weekly review is non-negotiable.** This is where patterns emerge and insights compound.
4. **Don't over-organize.** PARA gives you 4 buckets. If unsure, put it in Meetings/ and sort later.
5. **Trust the search.** Cmd+Shift+F finds anything. You don't need perfect folders.

---

*This vault was set up by an automated migration tool. For questions or to re-run the migration, see the `brain/` directory in your tooling workspace.*
