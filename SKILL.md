---
name: agent-start-use
description: "Guides Hermes Agent onboarding setup with file management, Kanban project standards, Obsidian knowledge base, and session archiving."
version: 0.5.0
author: Hermes Agent + Boss
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [onboarding, setup, personalization, initialization, preferences, 初始化调校, kanban, department-standards]
    related_skills: [hermes-agent, obsidian, kanban-team-setup]
---

# Agent Start Use

Guides new Hermes Agent users through a structured, conversational onboarding process covering five core personalization areas. Runs interactively — never auto-executes without explicit user approval.

## When to Use

- User says "初始化调校" or similar onboarding requests
- A new Hermes Agent user wants to personalize their session from scratch
- User asks to set up naming, file management, knowledge base, or working habits
- First-time session configuration or re-onboarding after a profile reset

Don't use for: one-off preference changes (use memory directly), technical Hermes troubleshooting (use `hermes-agent` skill), or batch automation (use `cronjob`).

## Procedure

### Step 0 — Discovery & Planning (MANDATORY first action)

**功能描述：**
初始化调校的第一步是"先规划，后执行"。在修改任何配置之前，必须先向用户展示完整的实施方案，让用户了解：
- 整个调校过程包含哪些步骤
- 每步要做什么、为什么要做
- 需要用户提供什么信息
- 数据会存储在哪里
- 有没有前置条件（比如需要安装Obsidian）

**为什么重要：** 避免盲目操作导致配置错误，让用户有完整的知情权和决策权。

**Inputs required from user:** 无（此步骤由Agent主导）

**Actions:**
1. 生成一份完整的计划文档
2. 询问用户确认

---

### Step 1 — Agent Naming

**功能描述：**
这一步设置Agent的身份标识。配置完成后：
- Agent在对话中会用自己的名字自称（如"我是艾莉丝"）
- 知道如何称呼用户（如"Boss"）
- 每次会话都会加载这些信息，保持一致性

**为什么重要：** 建立个性化的人设，让对话更有温度，也方便后续记忆系统记录用户偏好。

**Inputs required from user:**
- Agent英文名（如 Alice, Orion）
- Agent中文名（如 艾莉丝，星野）
- 用户希望如何被称呼（如 Boss, 主人, 名字）

**Actions (after approval):**
1. Save to memory via `memory` tool:
   - `target: "user"`, content: `Agent英文名 <name>，中文名 <name-cn>`
   - `target: "user"`, content: `用户称呼为 <address>`
2. Confirm with user: *"已记录：我是<中文名>（<英文名>），今后称呼您为<address>。"*

---

### Step 2 — File Management Standards

**功能描述：**
建立统一的文件管理规范，确保所有临时文件、输出结果、项目代码都有固定的存放位置：

| 目录 | 用途 | 示例路径 |
|------|------|----------|
| `Chat/` | Agent对话临时文件和输出（三级结构） | `D:/WorkSpace/Hermes-workspace/Chat/<日期>-<会话主题>/<内容名>/` |
| `Department/` | 各部门项目目录 | `D:/WorkSpace/Hermes-workspace/Department/Software-Development-Department/` |
| `Tools/` | 工作工具（图片处理、脚本等） | `D:/WorkSpace/Hermes-workspace/Tools/` |
| `Sessions/` | Agent会话归档（自动清理） | `D:/WorkSpace/Hermes-workspace/Sessions/` |
| `kanban-workspace/` | Kanban任务临时文件 | `Department/<部门>/Project/<项目>/kanban-workspace/` |

**Chat/ 三级结构规范：**
```
Chat/
├── <日期>-<会话主题>/                    # 第一级：会话主题目录
│   ├── <内容名>/                        # 第二级：会话中的具体内容
│   │   ├── temp/                        # 临时文件（草稿、中间结果）
│   │   └── output/                      # 最终产物（报告、图表、文档等）
│   ├── <内容名2>/
│   │   ├── temp/
│   │   └── output/
│   └── ...
└── ...
```

- **第一级 `<日期>-<会话主题>`**：格式 `YYYYMMDD-会话主题`，如 `20260925-即兴创作歌曲`
- **第二级 `<内容名>`**：会话中具体创作/处理的对象名称，如歌曲名 A/B、项目名等
- **temp/**：对话过程中产生的草稿、中间结果
- **output/**：任务完成后的最终输出文件

**为什么重要：** 
- 避免文件散落各处难以查找
- 方便后续检索和历史追溯
- 支持多部门协作时保持结构清晰
- Git版本控制更整洁（只追踪代码，不追踪临时文件）
- Chat 三级结构让资源管理器中查看整齐顺眼

**Inputs required from user:**
- Default workspace root path (e.g., `D:\WorkSpace\Hermes-workspace`)
- Whether to create subdirectories (`Chat/`, `Department/`, `Tools/`, `Sessions/`)
- Optional: alternative paths per section

**Actions (after approval):**

1. Create base workspace directories:
   ```bash
   terminal(command="mkdir -p <workspace>/Chat <workspace>/Department <workspace>/Tools <workspace>/Sessions")
   ```

2. **Create Department directory structure:**
   ```bash
   mkdir -p "<workspace>/Department/<部门名称>/Project"
   ```

3. Save file structure convention to memory via `memory`:
   - Chat 三级结构：`<workspace>/Chat/<日期>-<会话主题>/<内容名>/temp` 和 `output/`
   - **Dept projects: `<workspace>/Department/<部门名称>/Project/<项目名>/`**
   - **Kanban workspace: `<workspace>/Department/<部门名称>/Project/<项目名>/kanban-workspace/`**
   - Tools: `<workspace>/Tools/` — 存储工作工具（如图片处理工具）
   - Sessions: `<workspace>/Sessions/` — Agent会话归档目录

4. **部门项目目录规范（已集成）:**
   - 所有部门统一使用此结构
   - `kanban-workspace/` 用于Kanban任务临时文件存放
   - Git worktree自动创建在 `.worktrees/` 目录
   - 示例：`D:/WorkSpace/Hermes-workspace/Department/Software-Development-Department/Project/Game-xiaoxiaole/kanban-workspace/`

5. Configure session auto-archive:
   ```bash
   hermes config set sessions.auto_archive true
   hermes config set sessions.auto_archive_days 3
   hermes config set sessions.archive_dir "<workspace>/Sessions"
   ```

6. Verify directories exist and report back.

---

### Step 3 — 部门创建与 Kanban 团队配置 (Optional, for Development Teams)

**功能描述：**
为软件开发部门配置完整的多Agent协作体系。配置完成后：
- 各角色拥有独立的 Profile 和 SOUL.md，职责清晰
- 部门目录结构标准化，项目有序管理
- 角色"入职"部门，形成完整的组织架构
- Kanban 看板实现任务分配、状态跟踪、依赖管理
- Gateway 自动调度任务，各角色并行开发
- Worktree 隔离保证不同角色不会互相干扰代码

**为什么重要：**
- 模拟真实企业团队协作流程
- 大项目可拆分为多个子任务并行处理
- 代码隔离避免冲突，便于版本管理
- 任务状态可视化，便于追踪进度

**谁需要此步骤：** 只有计划进行软件开发、需要多Agent协作的用户才需要。纯个人使用可跳过。

**Prerequisites:** Hermes Agent gateway running.

**Inputs required from user:**
- 部门名称（如 Software-Development-Department）
- 部门展示名称（如 软件开发部）
- 团队角色列表（由用户自定义，如需要的话）
- Board 名称（由用户自定义）

---

#### 3.1 建立 Profile 角色

**交互流程：**

1. **询问用户需要哪些角色**
   ```
   请告诉我您的团队需要哪些角色？（多个角色用逗号分隔）
   例如：项目经理、后端开发、前端开发、测试工程师、全栈开发
   ```

2. **用户输入角色后，动态创建 Profile**
   ```bash
   # 示例：假设用户输入了 "pm、后端、前端、测试"
   hermes profile create pm --clone-from default
   hermes profile create backend --clone-from default
   hermes profile create frontend --clone-from default
   hermes profile create tester --clone-from default
   ```

3. **收集每个角色的职责描述**
   - 逐一询问每个角色的核心职责
   - 用于生成对应的 SOUL.md

4. **为每个 Profile 创建 SOUL.md**
   ```
   # 示例：后端开发角色
   ~/.hermes/profiles/backend/SOUL.md
   
   ## 核心职责
   - API设计、数据库建模、业务逻辑
   - 性能优化、接口安全
   - ...（根据用户输入定制）
   ```

5. **配置 director 角色（如有）的 Kanban 权限**
   ```bash
   cat >> ~/.hermes/profiles/director/config.yaml << 'EOF'
   
   kanban:
     review_dispatch: true
     dispatch_interval_seconds: 30
   EOF
   ```

**注意：**
- 如果用户没有定义 director/项目经理角色，可不配置自动调度权限
- 角色数量不限，由用户根据实际需求决定
- 每个角色的 SOUL.md 内容由用户自定义

---

#### 3.2 创建部门

创建部门的物理目录结构，作为部门所有项目的根目录：

```bash
# 创建部门目录（包含Project子目录）
mkdir -p "<workspace>/Department/<部门名称>/Project"

# 创建部门工作流文档（根据用户定义的角色动态生成）
cat > "<workspace>/Department/<部门名称>/README.md" << 'EOF'
# <部门展示名称>

## 部门职责
- 负责软件产品的规划、开发、测试和交付
- 协调多Agent协作，确保项目按时高质量完成

## 目录结构
```
<Project>/
├── kanban-workspace/    # Kanban任务临时文件
├── src/                 # 源代码
├── .git/                # Git仓库
└── README.md
```

## 团队成员
<% roles.each do |role| %>
- <%= role.name %>: <%= role.description %>
<% end %>
EOF
```

---

#### 3.3 角色入职部门

为每个角色创建部门专属的记忆和配置，明确其归属关系：

```bash
# 保存部门架构信息到memory
hermes config set memory.<部门名称>_department "部门：<部门展示名称>，目录：<workspace>/Department/<部门名称>/"

# 保存角色列表
hermes config set memory.<部门名称>_roles "director/backend/frontend/coder/tester"

# 为director配置Kanban权限
cat >> ~/.hermes/profiles/director/config.yaml << 'EOF'

kanban:
  review_dispatch: true
  dispatch_interval_seconds: 30
EOF
```

**角色入职确认：**
- 每个角色Profile都加载部门的通用规则
- director 拥有 Kanban 调度和审查权限
- 其他角色通过 Kanban 工具领取任务

---

#### 3.4 建立部门流程

文档化部门的协作流程和工作规范：

```bash
# 创建部门工作流文档（根据用户定义的角色动态生成）
cat > "<workspace>/Department/<部门名称>/WORKFLOW.md" << 'EOF'
# <部门展示名称> 工作流程

## 角色职责
| 角色 | 职责 |
|------|------|
<% roles.each do |role| %>
| <%= role.name %> | <%= role.description %> |
<% end %>

## 任务流转
```
需求 → director拆解 → Kanban看板
     → 各角色并行开发
     → director审查 → tester验收 → 完成
```

## 沟通协议
- 任务依赖通过 `kanban link` 建立
- 代码审查通过 `request-review` / `request-changes` 流程
- 问题升级路径：角色 → director → Boss
EOF
```

**注意：** 表格内容根据用户实际定义的角色动态生成，不是预置的固定模板。

---

#### 3.5 配置 Kanban 与 Kanban 工作区目录

初始化 Kanban 系统，设置看板和工作区目录：

```bash
# 初始化 Kanban 数据库
hermes kanban init

# 创建看板
hermes kanban boards create <board-slug> --name "<部门展示名称>"

# 切换到新看板
hermes kanban boards switch <board-slug>

# 设置默认工作区（指向部门Project目录）
hermes kanban boards set-default-workdir <board-slug> "<workspace>/Department/<部门名称>/Project"
```

**Kanban 工作区结构：**
```
<workspace>/Department/<部门名称>/Project/
├── <项目名>/
│   ├── kanban-workspace/      # Kanban任务临时文件存放
│   ├── src/                   # 源代码（开发时创建）
│   ├── .git/                  # Git仓库
│   ├── .worktrees/            # Git worktree（自动管理）
│   │   ├── t_<task-id>-<role1>/
│   │   ├── t_<task-id>-<role2>/
│   │   └── ...
│   └── README.md
└── ...
```

**启动 Gateway 自动调度：**
```bash
hermes gateway start
```

Gateway 启动后，dispatcher 会：
- 每 30 秒轮询一次 `ready` 状态的任务
- 自动分配给对应角色的 Profile
- 创建 Git worktree 隔离开发环境
- 管理任务状态流转

---

**Teams workflow:**
```
Boss → director（分析需求、拆解任务）
    ↓
director 写入 Kanban 看板
    ↓
各角色领取任务并行开发
    ↓
director 代码审查 → tester 验收测试
```

**注意：** 如果用户没有定义 director 或 tester 角色，对应步骤可省略。

---

### Step 4 — Obsidian Knowledge Base Setup

**功能描述：**
创建三级知识管理体系，作为Agent的"外部大脑"：

| 层级 | 目录 | 用途 | 内容类型 |
|------|------|------|----------|
| 记忆区 | Memory-hub | 日常对话提炼的经验、洞察 | 简短笔记、待办事项 |
| 收藏区 | Collect-hub | 从记忆区整理出的有价值资料 | 分类整理的资料、参考文档 |
| 知识区 | Knowledge-hub | 完整体系化的深度知识 | 主题研究、方法论、知识库 |

**为什么重要：**
- 突破Agent记忆容量限制，长期保存重要知识
- 支持知识的沉淀、整理、复用
- 形成"经验→资料→知识"的进化链条
- Obsidian支持双向链接，构建知识网络

**谁需要此步骤：** 希望Agent有长期记忆、需要积累知识的用户。纯一次性任务可跳过。

**Prerequisites:** Obsidian installed on the user's machine. If not found, note the gap and proceed optionally.

**Inputs required from user:**
- Obsidian vault root path (e.g., `D:\mdhub`)
- Names for the three vaults (defaults: Memory-hub, Collect-hub, Knowledge-hub)

**Actions (after approval):**
1. Create vault directories:
   ```bash
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

### Step 5 — Working Habits & Protocols

**功能描述：**
建立用户和Agent之间的"交互契约"，明确：
- 用户何时需要Agent先分析再行动
- 什么情况下Agent可以自主执行
- 如何沟通需求更高效

**为什么重要：**
- 避免Agent过度执行用户不想要的操作
- 减少反复确认的摩擦成本
- 建立稳定的协作模式
- 新会话自动继承行为规则

**谁需要此步骤：** 所有用户都需要。这是基础协作规范。

**No file system changes needed.** Purely behavioral rules stored in memory.

**Actions (after approval):**
1. Save working habit rules via `memory`:
   - Content: `工作习惯：用户所有需求先整理问题分析和解决方案，必要时联网调研。未经用户明确指令（如"开始处理""继续工作"）前不得擅自执行任务。`
2. Optionally create a `.hermes.md` or `AGENTS.md` in the workspace root to persist these rules project-wide.

---

### Step 6 — Verification & Summary

**功能描述：**
完成所有配置后，生成一份完整的初始化报告，让用户一目了然地看到：
- 所有配置项的状态（已创建✓/已跳过）
- 关键路径和参数
- 下一步建议

**为什么重要：**
- 让用户确认配置正确
- 提供快速参考手册
- 便于后续问题排查

**Outputs:**
1. 控制台输出格式化报告
2. 可选：保存报告到 `<workspace>/Chat/初始化报告-YYYY-MM-DD.md`

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
    - 三级结构：<workspace>/Chat/<日期>-<会话主题>/<内容名>/temp + output
  Department目录：[路径]\Department\ （已创建 ✓）
  部门项目目录：[路径]\Department\<部门名称>\Project\ （已创建 ✓）
  Kanban工作区规范：<workspace>/Department/<部门名称>/Project/<项目名>/kanban-workspace/
  Tools目录：[路径]\Tools\ （已创建 ✓）— 工作工具存储
  Sessions目录：[路径]\Sessions\ （已创建 ✓）— 会话归档

三、部门创建与 Kanban 团队配置（如已设置）
  部门：<部门展示名称>
  部门目录：<workspace>/Department/<部门名称>/
  角色：<用户自定义的角色列表>
  Board: <board-slug>
  状态：✓ 已配置

四、Obsidian资料库
  根目录：[路径]
  记忆区：[路径]\Memory-hub\ （已创建 ✓）
  收藏区：[路径]\Collect-hub\ （已创建 ✓）
  知识区：[路径]\Knowledge-hub\ （已创建 ✓）

五、办事习惯
  已保存至记忆库 ✓

六、Agent会话配置
  归档目录：[路径]\Sessions\
  自动归档：已开启（3天后）✓
  保留天数：90天

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
- **Git initialization.** Kanban worktree mode requires git repo to be initialized with at least one commit before tasks can be created.
- **Department naming.** Use proper department names (e.g., "Software-Development-Department", not "Sofware-...").
- **User-defined roles.** Role names and quantities are defined by the user, not pre-set defaults.
- **Optional team setup.** If user doesn't need a development team, skip Step 3 entirely.

## Verification

- [ ] User confirmed the Step 0 plan before any changes were made
- [ ] All directory structures exist and are verified via `terminal`
- [ ] Memory entries are readable back via `memory` (implicit — they were just written)
- [ ] Kanban workspace structure documented in memory
- [ ] Final summary was presented to the user
- [ ] No task was executed without explicit user authorization ("开始"/"继续"/etc.)
