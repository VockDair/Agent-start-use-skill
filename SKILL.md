---
name: agent-start-use
description: "Guides Hermes Agent onboarding setup."
version: 0.1.0
author: Hermes Agent
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [onboarding, setup, personalization, initialization, preferences, 初始化调校]
    related_skills: [hermes-agent, obsidian]
---

# Agent Start Use

Guides new Hermes Agent users through a structured, conversational onboarding process covering four core personalization areas. Runs interactively — never auto-executes without explicit user approval.

## When to Use

- User says "初始化调校" or similar onboarding requests
- A new Hermes Agent user wants to personalize their session from scratch
- User asks to set up naming, file management, knowledge base, or working habits
- First-time session configuration or re-onboarding after a profile reset

Don't use for: one-off preference changes (use memory directly), technical Hermes troubleshooting (use `hermes-agent` skill), or batch automation (use `cronjob`).

## Procedure

### Step 0 — Discovery & Planning (MANDATORY first action)

Before touching any tool, present a **single summary document** covering:
1. What each step does and why it matters
2. Required inputs (what the user must provide)
3. Where data will be stored (memory, filesystem, Obsidian)
4. Estimated effort per step
5. Any prerequisites (e.g., Obsidian installed for Step 3)

Ask: *"以上为初始化方案，请确认后回复「开始」或提出修改意见。"*

**Never proceed past Step 0 without explicit approval.**

---

### Step 1 — Agent Naming

**Purpose:** Set agent display name and user address — makes the session feel personalized.

**Inputs required from user:**
- Agent English name (e.g., Alice, Orion)
- Agent Chinese name (e.g., 艾莉丝，星野)
- How user wants to be addressed (e.g., Boss, 主人, name)

**Actions (after approval):**
1. Save to memory via `memory` tool:
   - `target: "user"`, content: `Agent英文名 <name>，中文名 <name-cn>`
   - `target: "user"`, content: `用户称呼为 <address>`
2. Confirm with user: *"已记录：我是<中文名>（<英文名>），今后称呼您为<address>。"*

---

### Step 2 — File Management Standards

**Purpose:** Establish a clean, organized workspace so all temporary files and outputs have consistent, predictable locations.

**Inputs required from user:**
- Default workspace root path (e.g., `F:\workspace\Hermes-Workspace`)
- Whether to create the two subdirectories (`Chat/` and `Department/`)
- Optional: alternative paths per section

**Actions (after approval):**
1. Create workspace directories:
   ```
   terminal(command="mkdir -p <workspace>/Chat <workspace>/Department")
   ```
2. Save file structure convention to memory via `memory`:
   - Chat temp: `<workspace>/Chat/<日期-对话主题>/Temp/`
   - Chat output: `<workspace>/Chat/<日期-对话主题>/output/`
   - Dept temp: `<workspace>/Department/<部门名称>/Project/<项目类型-名称>/temp/`
   - Dept output: `<workspace>/Department/<部门名称>/Project/<项目类型-名称>/output/`
3. Verify directories exist and report back.

---

### Step 3 — Obsidian Knowledge Base Setup

**Purpose:** Create a three-tier personal knowledge system (Memory → Collection → Knowledge) to serve as Hermes's secondary memory warehouse.

**Prerequisites:** Obsidian installed on the user's machine. If not found, note the gap and proceed optionally.

**Inputs required from user:**
- Obsidian vault root path (e.g., `D:\mdhub`)
- Names for the three vaults (defaults: Memory-hub, Collect-hub, Knowledge-hub)

**Actions (after approval):**
1. Create vault directories:
   ```
   terminal(command="mkdir -p <vault-root>/Memory-hub <vault-root>/Collect-hub <vault-root>/Knowledge-hub")
   ```
2. Create a README in each vault explaining its purpose:
   - `Memory-hub/README.md`: 第二记忆仓 — 从日常对话提炼的经验与洞察
   - `Collect-hub/README.md`: 资料收藏仓 — 从记忆区提炼整理的有价值资料
   - `Knowledge-hub/README.md`: 结构化知识仓 — 完整体系化的深度知识
3. Set `OBSIDIAN_VAULT_PATH` convention in memory:
   - Content: `Obsidian库根目录：<vault-root>；记忆区：<vault-root>/Memory-hub；收藏区：<vault-root>/Collect-hub；知识区：<vault-root>/Knowledge-hub`
4. Document the knowledge refinement pipeline in memory: `记忆区 → 收藏区 → 知识区`

---

### Step 4 — Working Habits & Protocols

**Purpose:** Establish the interaction contract between user and agent — how requests are handled and when action is authorized.

**No file system changes needed.** Purely behavioral rules stored in memory.

**Actions (after approval):**
1. Save working habit rules via `memory`:
   - Content: `工作习惯：用户所有需求先整理问题分析和解决方案，必要时联网调研。未经用户明确指令（如"开始处理""继续工作"）前不得擅自执行任务。`
2. Optionally create a `.hermes.md` or `AGENTS.md` in the workspace root to persist these rules project-wide.

---

### Step 5 — Verification & Summary

After all four steps complete, produce a final summary report:

```
═══════════════════════════════════
  Agent 初始化调校完成报告
═══════════════════════════════════

一、命名设置
  Agent名：[中文名]（[英文名]）
  用户称呼：[称呼]

二、文件管理规范
  默认工作区：[路径]
  Chat目录：[路径]\Chat\ （已创建 ✓）
  Department目录：[路径]\Department\ （已创建 ✓）

三、Obsidian资料库
  根目录：[路径]
  记忆区：[路径]\Memory-hub\ （已创建 ✓）
  收藏区：[路径]\Collect-hub\ （已创建 ✓）
  知识区：[路径]\Knowledge-hub\ （已创建 ✓）

四、办事习惯
  已保存至记忆库 ✓

═══════════════════════════════════
```

---

## Pitfalls

- **Don't auto-execute.** Every step requires explicit user confirmation after the planning phase. The "don't act without permission" rule is foundational — model it from day one.
- **Don't assume paths exist.** Always verify with `terminal` after `mkdir`, and report errors clearly.
- **Don't skip Step 0.** Presenting the full plan upfront prevents confusion and lets the user catch issues early.
- **Obsidian prerequisite.** If Obsidian isn't installed, still create the directories but note the gap — don't block the rest of setup.
- **Memory density.** Keep memory entries concise (one fact per entry). Don't bloat the memory store with procedural text.
- **Windows path separators.** Use forward slashes in `terminal` commands; native Windows paths use backslashes but MSYS bash translates them.

## Verification

- [ ] User confirmed the Step 0 plan before any changes were made
- [ ] All directory structures exist and are verified via `terminal`
- [ ] Memory entries are readable back via `memory` (implicit — they were just written)
- [ ] Final summary was presented to the user
- [ ] No task was executed without explicit user authorization ("开始"/"继续"/etc.)
