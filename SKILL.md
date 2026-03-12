---
name: telos
description: "TELOS (Telic Evolution and Life Operating System) — Reads and updates the user's personal life OS stored in ~/clawd/telos/. Provides missions, goals, beliefs, challenges, and wisdom as context for life-aligned AI assistance. Based on Daniel Miessler's PAI framework. Use when: (1) user mentions 'telos', 'setup telos', 'update telos', 'add to telos', 'my goals', 'my beliefs', 'my missions', 'telos status'; (2) user asks about personal decisions, career direction, investment choices, relationships, priorities, or life strategy — always check for telos context first; (3) user says 'help me fill telos', '引导我填 telos', or 'telos onboarding'."
---

# TELOS — Telic Evolution and Life Operating System

User's personal life OS. 20-file system capturing who they are across missions, goals, beliefs, challenges, and wisdom. Read at session start. Updated through guided workflows.

## Data Location

- **User data**: `~/clawd/telos/` (never committed to git)
- **Templates**: `assets/templates/` in this skill (20 files)
- **References**: `references/onboarding.md`, `references/update-workflow.md`

## Session Startup

At every MAIN SESSION start:
1. Check if `~/clawd/telos/TELOS.md` exists → read it as user context
2. If no TELOS.md but other files exist → read `MISSION.md` + `GOALS.md` + `BELIEFS.md`
3. No files → skip silently; suggest "setup telos" if user asks about personal topics

Absorb silently. Use this context throughout the session without announcing it.

## Trigger → Action Map

| Trigger | Action |
|---|---|
| "setup telos" / "telos onboarding" / "引导我填" | See `references/onboarding.md` — copy templates + guided Q&A |
| "update telos" / "add to telos" | See `references/update-workflow.md` |
| "add book [title]" | Append to `BOOKS.md` → ask for one-line insight |
| "learned [X]" / "add to learned" | Append to `LEARNED.md` → ask context/source |
| "add to wisdom" | Append to `WISDOM.md` |
| "telos status" | Read + summarize `STATUS.md` |
| "my goals / beliefs / missions" | Read relevant file, respond in context |
| "I was wrong about [X]" | Append to `WRONG.md` with date + lesson |

## Personal Analysis Context

When user asks about **personal decisions, investments, career, relationships, life priorities, or strategy** — always check telos first:

1. If telos files exist → read relevant sections before responding
2. Frame advice against their Goals (G#) and Beliefs (B#)
3. Flag if a suggested action conflicts with their stated Missions (M#)
4. Reference their Challenges (C#) and Strategies (S#) when relevant

Example: user asks "should I take this opportunity?" → read M#, G#, B# → advise through that lens.

## Numbering System

`M#` Missions · `G#` Goals · `C#` Challenges · `S#` Strategies · `B#` Beliefs · `FR#` Frames · `MO#` Models · `N#` Narratives · `P#` Problems · `TR#` Traumas · `I#` Ideas

Hierarchy: `M → G ← (blocked by) C ← (solved by) S` | `B` guides all | `P` drives `G`

## Update Rules (summary)

Full workflow: `references/update-workflow.md`
- Backup before every change: `cp FILE.md backups/FILE_TIMESTAMP.md`
- Append, never overwrite
- Log all changes to `updates.md`
