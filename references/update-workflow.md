# TELOS Update Workflow

## Before Any Update

```bash
# 1. Create timestamped backup
TIMESTAMP=$(date +%Y%m%dT%H%M%S)
cp ~/clawd/telos/FILENAME.md ~/clawd/telos/backups/FILENAME_${TIMESTAMP}.md
```

## Per-File Format Rules

| File | Format |
|---|---|
| BOOKS.md | `- *Title* by Author — [one-line insight]` |
| LEARNED.md | `## Lesson\n\n[Description]\n\n*Date: YYYY-MM-DD · Source: [book/experience/conversation]*` |
| BELIEFS.md | `## B#: [Statement]\n\n**Evidence:** ...\n**Implications:** ...\n**Confidence:** High/Medium/Low` |
| GOALS.md | `## G#: [Title]\n\n**Supports:** M#\n**Target:** YYYY-MM-DD\n**Milestones:**\n- [ ] ...` |
| WISDOM.md | `> [Quote or principle]\n\n[Source / context]` |
| WRONG.md | `## [Period] — [What I Believed]\n\n**What happened:** ...\n**Lesson:** ...` |

## After Update

Append to `~/clawd/telos/updates.md`:
```
## YYYY-MM-DD HH:MM
- [FILENAME.md] Brief description of what changed
```

## Batch Interview Extraction

When the user says "extract from this conversation/interview into telos":
1. Identify all telos-relevant content (beliefs, lessons, books, goals, challenges)
2. Group by file type
3. Run update workflow once per file (backup → append → log)
4. Report summary: "Added 2 beliefs, 1 book, 3 lessons"
