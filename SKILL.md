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
| "setup telos" / "telos onboarding" / "引导我填" | Run `bun ${CLAUDE_SKILL_DIR}/scripts/init-telos.ts` then see `references/onboarding.md` |
| "update telos" / "add to telos" | Run update script (see below) — respond conversationally, not mechanically |
| "add book [title]" | Acknowledge the book, reflect on the insight, then append to `BOOKS.md` |
| "learned [X]" / "add to learned" | Engage with the lesson first, then append to `LEARNED.md` |
| "add to wisdom" | Discuss the principle, then append to `WISDOM.md` |
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

## Update Workflow

When updating telos, the conversation matters as much as the data. Follow this order:

1. **Engage first** — Acknowledge what the user shared. Reflect on the insight, ask a follow-up, or connect it to their existing telos context. This is a life framework, not a database — treat additions as meaningful moments.
2. **Execute** — Run the update script: `bun ${CLAUDE_SKILL_DIR}/scripts/update-telos.ts <file> "<content>" "<description>"`
3. **Confirm briefly** — Mention it's backed up and logged. Don't dump execution logs.
4. **Suggest connections** — After adding to one file, suggest related files that might benefit. ("This connects to your B0 about compounding — want to add a related strategy?")

Full format rules: `references/update-workflow.md`

The tone should feel like a thoughtful conversation partner recording insights together, not a CLI tool reporting status.
