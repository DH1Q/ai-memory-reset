# Claude Code Adapter

Claude Code supports local file read/write, so this skill runs in **Mode A (Automatic Archive & Overwrite)**.

## Setup (30 Seconds)

1. Copy `SKILL.md` into your global or project skills folder:
   ```bash
   mkdir -p ~/.claude/skills/ai-memory-reset
   cp SKILL.md ~/.claude/skills/ai-memory-reset/SKILL.md
   ```
2. Start Claude Code in any workspace and say:
   > `Clean up my memory` (or `一键清理记忆`)

## Target Files Audited
By default, Claude Code will inspect your `CLAUDE.md` / `MEMORY.md` in the current project or `~/.claude/CLAUDE.md`. Backups are automatically written to `memory_archive/YYYY-MM-DD_HHmm_memory_backup.md`.

## Rollback
Say:
> `Rollback memory` (or `回退记忆`)
