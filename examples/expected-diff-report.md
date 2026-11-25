# Expected Diff Preview Report (Sample Output)

Running `SKILL.md` on `examples/dirty-memory-sample.md` should produce a report similar to this:

---

### Memory Audit Report (Diff Preview)
- **Execution Mode:** Mode B (Chat-Only)
- **Summary:** 14 entries (~215 words) → 6 entries (~78 words) | Reduction: ~64%

#### 1. Conflicts Requiring Your Decision (CONFLICT)
- **[C1][R2 CONFLICT]**
  - *Entry A:* "Always keep your answers ultra-short, under 3 sentences."
  - *Entry B:* "Every time I ask a technical question, please explain the full historical background and give at least 3 detailed analogies."
  - → *Please reply which style you prefer (or specify a rule like: default concise, expand only when asked).*

#### 2. Proposed Removals & Archives (PRUNE / ARCHIVE)
- `[#1][R1 PRUNE]` "Please always think step by step before answering any question." → *Reason: Outdated model micromanagement patch.*
- `[#2][R1 PRUNE]` "Never be lazy and never omit code with '// rest of code here'." → *Reason: Outdated model patch.*
- `[#3][R1 PRUNE]` "Please make sure your answers are thorough and never skip details." → *Reason: Generic filler patch; also conflicts with conciseness preference.*
- `[#4][R3 ARCHIVE]` "Currently preparing for the May 2025 Product Hunt launch of my Pomodoro timer app (launch completed May 18, 2025)." → *Reason: Completed one-off event (>90 days old).*
- `[#5][R3 ARCHIVE]` "Remind me to buy a birthday cake for Mike on March 12, 2025." → *Reason: Expired one-off reminder.*

#### 3. Proposed Merges & Compressions (MERGE / COMPRESS)
- `[#6][R2 MERGE + R4 COMPRESS]` Merged 3 entries ("hate robotic intros", "stop starting with Great question/Certainly", "don't give generic advice, be direct") → **Rewritten:** `No filler intros ("Sure!", "Great question!"); lead directly with concrete, concise answers.`

#### 4. Preserved Unchanged (KEEP / PIN)
- 4 core entries preserved verbatim:
  - Identity: Solo indie developer & product designer (Shanghai), SwiftUI & TypeScript.
  - Hardware: Mac mini M4 (24GB RAM).
  - `[PIN]` Never execute destructive shell commands (`rm -rf`, `git push --force`) without explicit confirmation.
  - Active Context: Building Folio (local-first markdown note app with Tauri + React) `[since: 2026-10]`.

---
**Next Step:** Reply **"Confirm"** to archive and apply these changes, or specify adjustments (e.g., *"For C1, default concise and expand only on deep dives; confirm the rest"*).
