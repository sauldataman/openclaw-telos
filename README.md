# openclaw-telos

**TELOS** (Telic Evolution and Life Operating System) — A personal life OS plugin for [OpenClaw](https://openclaw.ai).

Captures who you are across missions, goals, beliefs, challenges, and wisdom. Gives your AI a persistent understanding of *you* — so it can give life-aligned advice, not just generic answers.

Based on [Daniel Miessler's PAI Framework](https://github.com/danielmiessler/Personal_AI_Infrastructure).

---

## What It Does

| Feature | Description |
|---|---|
| 📁 **20 Templates** | Full TELOS file set — fill at your own pace |
| 🧭 **Guided Onboarding** | Step-by-step Q&A to fill your core files (Missions → Goals → Beliefs) |
| 🔄 **Update Workflow** | Add books, lessons, wisdom anytime — auto-backup + changelog |
| 🧠 **Session Context** | AI reads your TELOS at session start, knows your missions and goals throughout |
| 💡 **Personal Analysis** | When you ask about decisions, career, or investments — AI cross-references your telos |

---

## Quick Start

### 1. Install

```bash
openclaw skills install ./telos.skill
```

Or clone and install from source:
```bash
git clone https://github.com/sauldataman/openclaw-telos.git
openclaw skills install ./openclaw-telos/telos.skill
```

### 2. Initialize

In OpenClaw, say:
```
setup telos
```

This copies all 20 templates to `~/clawd/telos/` and walks you through filling the core files.

### 3. Start Filling

The AI will guide you through:
1. **Missions** — What are you ultimately trying to achieve?
2. **Goals** — Specific objectives supporting your missions
3. **Beliefs** — Core beliefs that guide your decisions

Everything else (WISDOM, LEARNED, MODELS, etc.) you fill gradually over time.

### 4. Use It

Once set up, the AI automatically:
- Reads your telos at session start
- References your goals and beliefs when advising on decisions
- Flags conflicts between suggestions and your stated missions

Trigger updates anytime:
```
add this book to telos — The Psychology of Money by Morgan Housel
I learned something, add to telos — [what you learned]
add to my wisdom — [principle or insight]
update my goals
telos status
```

---

## File Structure

```
~/clawd/telos/              ← Your personal data (never shared)
├── TELOS.md                ← Master overview (start here)
├── MISSION.md              ← M0, M1, M2...
├── GOALS.md                ← G0, G1, G2...
├── BELIEFS.md              ← B0, B1, B2...
├── CHALLENGES.md           ← C0, C1...
├── STRATEGIES.md           ← S0, S1...
├── FRAMES.md               ← FR0, FR1...
├── MODELS.md               ← MO0, MO1...
├── NARRATIVES.md           ← N0, N1...
├── PROBLEMS.md             ← P0, P1...
├── PREDICTIONS.md
├── PROJECTS.md
├── TRAUMAS.md              ← TR0, TR1...
├── IDEAS.md                ← I0, I1...
├── BOOKS.md
├── MOVIES.md
├── STATUS.md
├── LEARNED.md
├── WISDOM.md
├── WRONG.md
├── updates.md              ← Append-only changelog
└── backups/                ← Auto-created timestamped backups
```

### Priority Guide

Start with these, fill the rest over time:

| Priority | Files |
|---|---|
| ⭐⭐⭐ Core (fill first) | TELOS.md or MISSION.md + GOALS.md + BELIEFS.md |
| ⭐⭐ Important | CHALLENGES.md, STRATEGIES.md, STATUS.md |
| ⭐ Accumulate over time | WISDOM.md, LEARNED.md, BOOKS.md, MODELS.md, FRAMES.md, WRONG.md |
| Optional | TRAUMAS.md, PREDICTIONS.md, MOVIES.md, NARRATIVES.md, PROBLEMS.md |

---

## Numbering System

All entries use cross-referenceable prefixes:

```
M#   Missions      G#   Goals         C#   Challenges
S#   Strategies    B#   Beliefs       FR#  Frames
MO#  Models        N#   Narratives    P#   Problems
TR#  Traumas       I#   Ideas
```

Relationships:
```
MISSIONS (M#)
    └─ supported by → GOALS (G#)
                          └─ blocked by → CHALLENGES (C#)
                                              └─ solved by → STRATEGIES (S#)

BELIEFS (B#)  → guide all decisions
PROBLEMS (P#) → drive GOALS
MODELS (MO#)  → shape understanding
```

---

## Update Rules

The skill enforces a safe update workflow:

1. **Always backup first** — auto-creates `~/clawd/telos/backups/FILE_TIMESTAMP.md`
2. **Append, never overwrite** — preserves history
3. **Log every change** — appended to `~/clawd/telos/updates.md`

---

## Privacy

- `~/clawd/telos/` is **never committed to git** by default
- Add `telos/` to your `.gitignore`
- Templates in this repo contain no personal data

---

## Compatibility

- **OpenClaw** — Primary target (`.skill` install format)
- **Claude Code / PAI** — Compatible with Daniel Miessler's PAI framework structure; templates can be used directly in `~/.claude/PAI/USER/TELOS/`

---

## Credits

- **Original concept**: [Daniel Miessler](https://github.com/danielmiessler) — [Personal_AI_Infrastructure](https://github.com/danielmiessler/Personal_AI_Infrastructure)
- **OpenClaw adaptation**: K ([@imnoobk](https://twitter.com/imnoobk)) + 猴爪

---

## License

MIT — see [LICENSE](LICENSE)

---

*"Most people don't believe they have valuable contributions to make. They've never asked who they are, what they're about, and have never articulated or written it down."*

— Daniel Miessler
