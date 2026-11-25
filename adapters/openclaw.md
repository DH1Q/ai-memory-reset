# OpenClaw & Local Agent Adapter

Local file-based agents with filesystem tools run this skill in **Mode A**.

## Setup

1. Place `SKILL.md` in your agent's `skills/ai-memory-reset/` directory.
2. Ensure your agent has read/write access to your workspace memory file (e.g., `MEMORY.md`, `USER.md`, or `memory/`).
3. Trigger anytime via chat or a periodic cron reminder:
   > `Run a memory audit` / `一键清理记忆`

## Recommended Schedule
Set a lightweight monthly reminder (every 30–60 days) to prompt you: *"Time for a 2-minute memory audit?"* — keep the actual execution interactive so you always review the Diff Preview Gate.
