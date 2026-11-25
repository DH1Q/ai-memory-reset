# AI Memory Reset（AI 记忆重置与体检技能）

> **给你的 AI 长期记忆做一次定期“垃圾回收”。**  
> 零代码依赖、纯 Markdown 驱动。全平台通用（Claude Code / OpenClaw / Cursor / ChatGPT / Claude / Gemini）。

[English Documentation (README.md)](./README.md)

---

## 为什么需要它？

重度使用 AI 一段时间后，你的记忆库和自定义指令几乎必然出现**“规则腐烂”**：
- 以前为了给旧模型兜底写的保姆级补丁（“请一步步思考”“不要偷懒”“严禁省略代码”），放到新模型上反而限制了它的原生推理上限。
- 不同时期加进去的规则互相打架（一边要求“极简回答”，一边要求“每次展开完整背景”）。
- 早就结束的旧项目上下文还留在记忆里，持续污染新对话。

**AI Memory Reset** 是一个通用技能：只需说一句**“一键清理记忆”**，它就会按显式规则为你的记忆做体检、输出 **Diff 对比清单**，等你确认后再**先归档、后覆写**，随时可一键回退。

### 效果对比示例
| 指标 | 清理前 | 清理后 |
| :--- | :--- | :--- |
| 记忆条目 | 18 条杂乱堆叠的规则与笔记 | **8 条高信噪比原子化记忆** |
| 过时模型补丁 | 5 条冗余微操指令 | **0 条（R1 自动剔除）** |
| 规则冲突 | 2 处隐藏矛盾 | **R2 主动揪出并交由用户二选一** |
| 过期短期项目 | 3 个已完结旧任务 | **R3 移入归档快照，不污染活跃区** |
| 数据结构 | 无分类流水账 | **4 分区中立标准结构（R6，兼容 2.0 同步）** |

---

## 核心机制

1. **双模自动适配：**
   - **Mode A（本地 Agent / 带文件工具环境）：** 自动读取记忆文件，在 `memory_archive/` 下生成时间戳只读归档，再覆写主文件。
   - **Mode B（网页端纯对话环境）：** 自动降级为输出 `[Snapshot Backup]` 原备份块 + `[Optimized Memory]` 重构记忆块，供用户留档与复制替换。
2. **6 条显式修剪规则（R1–R6）：**
   - `R1 PRUNE`：剥离过时的旧模型保姆级补丁。
   - `R2 MERGE / CONFLICT`：合并重复项；遇到矛盾**严禁静默覆盖**，必须交由用户裁决。
   - `R3 ARCHIVE`：将超 90 天未活跃或已完结的短期上下文移入归档。
   - `R4 COMPRESS`：将冗长叙述提炼为高密度单行陈述句。
   - `R5 PIN`：核心身份、安全红线及标注 `[PIN]` / `[KEEP]` 的条目绝对豁免。
   - `R6 NORMALIZE`：重排进 4 个标准分区（`Identity` / `Interaction & Style` / `Rules & Boundaries` / `Active Context`）。
3. **强阻断 Diff 确认门：** 收到用户明确“确认执行”前，绝不修改任何文件或记忆。
4. **先归档、后覆写 & 一键回退：** 随时说一句“回退记忆”，即可恢复到清理前的任意历史快照。

---

## 30 秒快速上手

按你常用的环境选择接入方式：

- **Claude Code：** 将 `SKILL.md` 放入 `~/.claude/skills/ai-memory-reset/SKILL.md` → [查看指南](./adapters/claude-code.md)
- **OpenClaw / 本地 Agent：** 直接挂载 `SKILL.md` 到技能目录 → [查看指南](./adapters/openclaw.md)
- **Cursor / Windsurf：** 添加为 Rules 或 Slash Command → [查看指南](./adapters/cursor-windsurf.md)
- **网页端（ChatGPT / Claude / Gemini）：** 复制 `SKILL.md` 发送给 AI，然后说“一键清理记忆” → [查看指南](./adapters/web-chat.md)

---

## 先用沙盒样本试跑（零风险）

不放心直接跑自己的真实记忆？仓库内置了演练样本：
1. 打开 [`examples/dirty-memory-sample.md`](./examples/dirty-memory-sample.md)。
2. 加载 `SKILL.md` 后，把样本发给 AI 说：“用记忆重置技能给这份样本做个体检”。
3. 对照 [`examples/expected-diff-report.md`](./examples/expected-diff-report.md) 查看预期效果。

---

## 路线图（Roadmap）

- [x] **v1.0：** 核心修剪规则（R1–R6）、Diff 预览确认门、Mode A/B 双模降级、归档与一键回退。
- [ ] **v2.0：** **跨平台一键同步记忆** — 基于 R6 的 4 分区中立结构，实现 Claude、ChatGPT、Gemini 与本地 Agent 之间的记忆一键同步。（欢迎提 Issue 投票你最想支持的平台！）

---

## 开源协议

[MIT License](./LICENSE)
