---
name: telos
description: "TELOS (Telic Evolution and Life Operating System) — Reads, updates, and backs up the user's personal life OS stored in ~/clawd/telos/. Provides missions, goals, beliefs, challenges, and wisdom as context for life-aligned AI assistance. Based on Daniel Miessler's PAI framework. Use when: (1) user mentions 'telos', 'setup telos', 'update telos', 'add to telos', 'my goals', 'my beliefs', 'my missions', 'telos status'; (2) user asks about personal decisions, career direction, investment choices, relationships, priorities, or life strategy — always check for telos context first; (3) user says 'help me fill telos', '引导我填 telos', or 'telos onboarding'; (4) user says 'backup telos', 'restore telos', 'telos backups', 'telos history', or 'list telos snapshots'."
---

# TELOS — Telic Evolution and Life Operating System

User's personal life OS. 20-file system capturing who they are across missions, goals, beliefs, challenges, and wisdom. Read at session start. Updated through guided workflows.

## Data Location

- **User data**: `~/clawd/telos/` (never committed to git)
- **Templates**: `assets/templates/` in this skill (20 files)
- **References**: `references/onboarding.md`, `references/update-workflow.md`

## Context Loading

Telos files are loaded **on-demand** — only read what's relevant to the current conversation. Never load everything at once.

### File Index

Use this index to decide which files to read. Each file captures a different dimension of the user's life context:

| File | Contains | Load when the conversation touches... |
|---|---|---|
| MISSION.md | M# — ultimate life purposes | direction, meaning, "why am I doing this", major decisions |
| GOALS.md | G# — specific objectives with timelines | planning, priorities, "should I do X", progress, deadlines |
| BELIEFS.md | B# — core convictions guiding decisions | values, principles, "what do you think about", worldview |
| CHALLENGES.md | C# — current obstacles | frustration, being stuck, blockers, "I can't seem to" |
| STRATEGIES.md | S# — approaches to challenges/goals | how to tackle something, methodology, "what's my plan for" |
| PROBLEMS.md | P# — problems in the world to solve | entrepreneurship, impact, "what problem should I work on" |
| PROJECTS.md | Active initiatives | work, side projects, "what am I working on" |
| NARRATIVES.md | N# — talking points, self-story | pitching, introducing yourself, "how do I explain what I do" |
| FRAMES.md | FR# — mental perspectives | reframing, alternative viewpoints, "how should I think about" |
| MODELS.md | MO# — how things work | decision-making, analysis, cause-and-effect reasoning |
| PREDICTIONS.md | Future bets with confidence levels | forecasting, trends, "what do you think will happen" |
| WISDOM.md | Accumulated principles and quotes | advice, life lessons, "what's your take on" |
| LEARNED.md | Specific lessons from experience | reflecting, "what have I learned about", mistakes made |
| WRONG.md | Things the user was wrong about | intellectual humility, updating beliefs, "I changed my mind" |
| BOOKS.md | Influential books | reading, recommendations, "what should I read" |
| MOVIES.md | Influential films | media, culture, recommendations |
| TRAUMAS.md | TR# — formative experiences | deep personal context, patterns, "why do I always" |
| IDEAS.md | I# — ideas worth capturing | brainstorming, "I just thought of", creative exploration |
| STATUS.md | Current life snapshot | "where am I right now", life audit, quarterly review |
| TELOS.md | Master overview with all sections | "show me my telos", full context needed, onboarding |

### Loading Rules

1. Check if `~/clawd/telos/` exists. If not, skip silently.
2. Read the user's message. Identify which life dimensions it touches (use the "Load when" column).
3. Read only those files. Usually 1-3 files, rarely more than 4.
4. Absorb silently — use the context to inform your response without announcing it.
5. If a file is empty (only template content), skip it.
6. For major life decisions, load the core trio: MISSION.md + GOALS.md + BELIEFS.md.
7. If no telos directory exists and the user asks about personal topics, suggest "setup telos."

The goal: every response to a personal question should be informed by the user's own stated values, not generic advice. But unrelated conversations (coding, factual questions, etc.) should not trigger any telos loading.

## Trigger → Action Map

| Trigger | Action |
|---|---|
| "setup telos" / "telos onboarding" / "引导我填" | Run `bun {baseDir}/scripts/init-telos.ts` then see `references/onboarding.md` |
| "update telos" / "add to telos" | Run update script (see below) — respond conversationally, not mechanically |
| "add book [title]" | Acknowledge the book, reflect on the insight, then append to `BOOKS.md` |
| "learned [X]" / "add to learned" | Engage with the lesson first, then append to `LEARNED.md` |
| "add to wisdom" | Discuss the principle, then append to `WISDOM.md` |
| "telos status" | Read + summarize `STATUS.md` |
| "my goals / beliefs / missions" | Read relevant file, respond in context |
| "I was wrong about [X]" | Append to `WRONG.md` with date + lesson |
| "backup telos" | Run `bun {baseDir}/scripts/backup-telos.ts backup` |
| "restore telos" / "restore telos from [name]" | Run `bun {baseDir}/scripts/backup-telos.ts restore <name>` |
| "list telos backups" / "telos snapshots" | Run `bun {baseDir}/scripts/backup-telos.ts list` |
| "telos history [file]" / "show beliefs history" | Run `bun {baseDir}/scripts/backup-telos.ts history <file>` |
| "restore beliefs from [version]" | Run `bun {baseDir}/scripts/backup-telos.ts restore-file <file> <ver>` |

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
2. **Execute** — Run the update script: `bun {baseDir}/scripts/update-telos.ts <file> "<content>" "<description>"`
3. **Confirm briefly** — Mention it's backed up and logged. Don't dump execution logs.
4. **Suggest connections** — After adding to one file, suggest related files that might benefit. ("This connects to your B0 about compounding — want to add a related strategy?")

Full format rules: `references/update-workflow.md`

The tone should feel like a thoughtful conversation partner recording insights together, not a CLI tool reporting status.
