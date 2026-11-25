# AI Memory Reset (`ai-memory-reset`)

> **Garbage collection for your AI's long-term memory.**  
> Zero dependencies. Pure Markdown. Works with Claude Code, Cursor, OpenClaw, ChatGPT, Claude, and Gemini.

[中文文档 (README_ZH.md)](./README_ZH.md)

---

## Why?

After months of heavy AI usage, your memory bank and custom instructions inevitably suffer from **Rule Rot**:
- Outdated "babysitting patches" written for older models (*"think step by step"*, *"don't be lazy"*, *"never omit code"*) that now bottleneck newer models.
- Contradictory rules added months apart (*"be ultra-brief"* vs. *"always explain full background"*).
- Dead project context from last year polluting every new conversation.

**AI Memory Reset** is a universal skill that audits, prunes, and normalizes your AI memory on demand—with a mandatory **Diff Preview Gate** and **Archive/Rollback** safety net.

### Before vs. After (Real Example)
| Metric | Before Audit | After Audit |
| :--- | :--- | :--- |
| Memory Entries | 18 messy rules & notes | **8 high-signal atomic entries** |
| Outdated Model Patches | 5 redundant instructions | **0 (Pruned via R1)** |
| Rule Conflicts | 2 hidden contradictions | **Surfaced & resolved via R2** |
| Expired Context | 3 finished projects | **Safely archived via R3** |
| Structure | Unsorted text dump | **4-section portable schema (R6)** |

---

## How It Works

1. **Adaptive Mode Detection:** Automatically detects whether it is running in a local Agent with file access (**Mode A**) or a web chat UI (**Mode B**).
2. **6 Explicit Pruning Rules (`R1–R6`):**
   - `R1 PRUNE`: Strips outdated model micromanagement patches.
   - `R2 MERGE / CONFLICT`: Merges duplicates; flags contradictions for user decision.
   - `R3 ARCHIVE`: Separates expired short-term context (>90 days) into archive snapshots.
   - `R4 COMPRESS`: Turns verbose paragraphs into atomic single-line statements.
   - `R5 PIN`: Strictly protects core identity, security boundaries, and `[PIN]` rules.
   - `R6 NORMALIZE`: Reorganizes into 4 neutral sections (`Identity`, `Interaction & Style`, `Rules & Boundaries`, `Active Context`).
3. **Diff Preview Gate:** Nothing is modified until you review the Diff report and reply **Confirm**.
4. **Archive First, Rollback Anytime:** Always saves a timestamped snapshot before writing. Say *"rollback memory"* to revert.

---

## Quick Start (30 Seconds)

Choose your environment:

- **Claude Code:** Copy `SKILL.md` to `~/.claude/skills/ai-memory-reset/SKILL.md` → [Guide](./adapters/claude-code.md)
- **OpenClaw / Local Agents:** Drop `SKILL.md` into your agent's skills directory → [Guide](./adapters/openclaw.md)
- **Cursor / Windsurf:** Add as a Rule or Slash Command → [Guide](./adapters/cursor-windsurf.md)
- **Web Chat (ChatGPT / Claude / Gemini):** Paste `SKILL.md` into a chat and say `"Clean up my memory"` → [Guide](./adapters/web-chat.md)

---

## Try It Safely First (Dry-Run Sandbox)

Don't test on your real memory first. Use the built-in test fixture:
1. Open [`examples/dirty-memory-sample.md`](./examples/dirty-memory-sample.md).
2. Feed it to your AI with `SKILL.md` loaded and say: *"Run a memory audit on this sample."*
3. Compare the output against [`examples/expected-diff-report.md`](./examples/expected-diff-report.md).

---

## Roadmap

- [x] **v1.0:** Core pruning rules (`R1–R6`), Diff Preview Gate, Mode A/B auto-fallback, Archive & Rollback.
- [ ] **v2.0:** **One-Click Cross-AI Memory Sync** — Export/import adapters based on the R6 4-section standard schema to keep Claude, ChatGPT, Gemini, and local Agents in sync. *(Open an Issue to suggest your favorite AI platform!)*

---

## License

[MIT](./LICENSE)
