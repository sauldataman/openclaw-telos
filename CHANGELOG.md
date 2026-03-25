# Changelog

All notable changes to this project will be documented in this file.

Format: [Semantic Versioning](https://semver.org)

---

## [1.0.1] — 2026-03-25

### Security
- **REPO-03 fix**: `TRAUMAS.md` injection now requires explicit trigger phrases
  (`"my trauma"`, `"telos trauma"`, `"traumas"`) instead of any message containing
  the word "trauma". Prevents accidental injection of sensitive personal data in
  group chats or unrelated conversations.
  - Identified by: SlowMist Agent Security Review
  - Affected file: `hooks/telos-context.js`

---

## [1.0.0] — 2026-03-24

### Added
- Initial release of TELOS skill for OpenClaw
- 20 template files covering all life dimensions (MISSION, GOALS, BELIEFS, etc.)
- `scripts/init-telos.ts` — Initialize telos directory from templates
- `scripts/update-telos.ts` — Safe update with automatic backup and changelog
- `scripts/backup-telos.ts` — Full snapshot backup and restore system
- `hooks/telos-context.js` — OpenClaw hook for automatic context injection
  - `agent:bootstrap` — Loads MISSION + GOALS + BELIEFS at session start
  - `message:preprocessed` — Injects relevant files based on topic keywords
- `references/onboarding.md` — Guided setup workflow
- `references/update-workflow.md` — Update format rules
- `evals/evals.json` — Skill evaluation test cases
- Updated `SKILL.md` with File Index table, backup triggers, hook integration docs

### Architecture
- Zero external npm dependencies (pure Node.js built-ins + bun stdlib)
- Append-only file updates — no destructive overwrites
- `.gitignore` excludes all personal telos data from version control
- Paths hardcoded to `~/clawd/telos/` — no path traversal attack surface
