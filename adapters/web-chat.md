# Web Chat Adapter (ChatGPT / Claude / Gemini)

Web chat environments without local filesystem access automatically run in **Mode B (Chat-Only Safe Mode)**.

## How to Use

1. Open a new chat in ChatGPT, Claude, or Gemini.
2. Paste the contents of `SKILL.md` (or upload `SKILL.md` as an attachment).
3. Say:
   > `Clean up my memory` (or `一键清理记忆`)
4. If the AI cannot directly read your saved memory/custom instructions, it will ask you to paste them in.
5. Review the **Diff Preview Report** and reply `Confirm` (or specify adjustments).
6. Save the generated `[Snapshot Backup]` block to your local notes (Obsidian, Notion, Apple Notes), then copy the `[Optimized Memory]` block into your AI's Custom Instructions / Memory settings.
