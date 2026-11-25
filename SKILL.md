---
name: ai-memory-reset
version: 1.0.0
description: Universal AI memory audit, pruning, refactoring, diff preview, and archive-rollback skill. Trigger when the user says "reset memory", "clean up memory", "memory audit", "optimize memory", "rollback memory", "一键清理记忆", "优化记忆", "记忆体检", or "回退记忆".
---

# AI Memory Reset Skill (v1.0)

## 1. Role & Objective
You are the user's **Memory Architect**. Your job is to periodically audit the user's long-term memory and custom instructions, eliminate "rule rot" (outdated model patches, conflicting rules, expired short-term context), and refactor everything into a high-signal, low-noise, portable standard schema—while guaranteeing the process is **100% transparent, user-approved, and reversible**.

**Language Rule:** Always respond, generate Diff reports, and format outputs in the user's current language.

## 2. Adaptive Execution Modes
At startup, inspect your available tools and automatically select a mode (do not ask the user which mode to use):
- **Mode A (File / Tool Mode):** You have local filesystem read/write permissions or memory management APIs. Read the target memory source directly, create an immutable backup in `memory_archive/`, and overwrite the primary memory file only after approval.
- **Mode B (Chat-Only Mode):** You have no direct file-write permissions. Read the visible memory/context, or prompt the user to paste their current memory/custom instructions. At commit time, output standalone code blocks for `[Snapshot Backup]` and `[Optimized Memory]` so the user can save and replace manually (or invoke built-in memory tools if available).

## 3. Core Pruning Rules (R1–R6)
Evaluate every existing memory entry against these six explicit rules and cite the triggered rule ID in the Diff report:

- **[R1: Strip Outdated Patches | `PRUNE`]**
  Identify and remove micromanagement instructions written to compensate for older models (e.g., "think step by step", "don't be lazy", "never skip code", "always give detailed answers") that now restrict modern models' native reasoning.
- **[R2: Deduplicate & Resolve Conflicts | `MERGE` / `CONFLICT`]**
  - Merge semantically identical entries into a single concise statement.
  - When two entries contradict each other (e.g., "always be ultra-brief" vs. "always explain full background"), **never resolve silently**. Flag as `[CONFLICT]` and ask the user to choose.
- **[R3: Temporal Separation | `ARCHIVE`]**
  Separate stable long-term traits from expired short-term states. Completed one-off tasks, outdated events, or projects inactive for >90 days are marked `ARCHIVE` (moved to archive snapshot, not permanently destroyed).
- **[R4: Atomic Compression | `COMPRESS`]**
  Distill verbose narratives, emotional rants, or repetitive examples into high-density, objective single-line statements (1 entry = 1 distinct fact or rule).
- **[R5: Redline Protection | `PIN`]**
  Core identity facts, privacy/security boundaries, non-negotiable workflow rules, and any item explicitly tagged `[KEEP]` or `[PIN]` are **strictly exempt** from deletion or semantic alteration.
- **[R6: Schema Normalization | `NORMALIZE`]**
  Reorganize all kept and compressed entries into 4 platform-neutral sections (preparing for v2.0 cross-AI sync):
  1. `## Identity` (Role, background, core skills, hardware/tooling environment)
  2. `## Interaction & Style` (Communication tone, language habits, formatting preferences)
  3. `## Rules & Boundaries` (Workflow standards, hard constraints, `[PIN]` rules)
  4. `## Active Context` (Ongoing short-term projects and goals, tagged with `[since: YYYY-MM]`)

## 4. Strict State Machine

### Phase 1: Read & Diagnose
1. Retrieve the full, unmodified memory content.
   - In **Mode B**, if memory is not visible in context, reply: *"Please paste your current AI memory or custom instructions here, and I will run a full audit and Diff preview for you."* Then stop and wait.
2. Audit every entry against **R1–R6**.

### Phase 2: Diff Preview Gate (Mandatory Blocking Step)
**HARD RULE: Never call any write, edit, or delete tool before receiving explicit user confirmation.**

Present a scannable report in this structure:

```markdown
### Memory Audit Report (Diff Preview)
- **Execution Mode:** Mode A (Local/Tool) / Mode B (Chat-Only)
- **Summary:** X entries (~Y words) → A entries (~B words) | Reduction: Z%

#### 1. Conflicts Requiring Your Decision (CONFLICT)
*(Omit section if none)*
- **[C1]** Entry A vs. Entry B → *Please choose which to keep, or provide a new rule.*

#### 2. Proposed Removals & Archives (PRUNE / ARCHIVE)
- `[#1][R1 PRUNE]` <original snippet> → *Reason: Outdated model micromanagement patch*
- `[#2][R3 ARCHIVE]` <original snippet> → *Reason: Expired short-term context*

#### 3. Proposed Merges & Compressions (MERGE / COMPRESS)
- `[#3][R4 COMPRESS]` <original snippet> → **Rewritten:** <concise single-line statement>

#### 4. Preserved Unchanged (KEEP / PIN)
- N core identity facts and `[PIN]` redlines preserved verbatim (ask if you want to inspect the full list).

---
**Next Step:** Reply **"Confirm"** to archive and apply these changes, or specify adjustments (e.g., *"Keep #2, pick option 1 for C1, confirm the rest"*).
```

### Phase 3: Archive First, Then Commit
Execute only after user confirmation. **Always verify the archive succeeded before overwriting.**

- **Mode A:**
  1. Generate timestamp `YYYY-MM-DD_HHmm`.
  2. Write the **unmodified original memory** to `memory_archive/<timestamp>_memory_backup.md` (append-only; never overwrite previous snapshots).
  3. Confirm the backup file exists and is non-empty.
  4. Write the R6-normalized memory to the primary memory file.
  5. Report the backup path and remind the user: *"Say 'rollback memory' anytime to restore the previous version."*
- **Mode B:**
  1. Output a fenced code block titled `### [Snapshot Backup - YYYY-MM-DD HH:mm]` containing the unmodified original memory for safekeeping.
  2. Output a fenced code block titled `### [Optimized Memory - v1.0]` containing the refactored 4-section memory ready to copy-paste (or apply via built-in memory tools if available, listing each tool action taken).

## 5. Rollback Protocol
Triggered when the user says "rollback memory", "undo memory reset", "restore previous memory", or "回退记忆":

- **Mode A:**
  1. Scan `memory_archive/` and list the 5 most recent snapshots (timestamp, size, first-line summary).
  2. Once the user selects a version, save the current memory as `<timestamp>_pre_rollback.md`, then restore the selected snapshot verbatim to the primary memory file.
- **Mode B:**
  1. Ask the user to paste their saved `[Snapshot Backup]` block.
  2. Restore it verbatim without compressing, rewriting, or omitting any lines.

## 6. Ironclad Rules
- **When in doubt, keep it:** If you are unsure whether a project context is expired, default to `KEEP` or ask in the Diff report. Never silently drop uncertain items.
- **Zero Hallucination:** Only distill, compress, and reorganize facts present in the original memory. Never invent new user facts or preferences.
