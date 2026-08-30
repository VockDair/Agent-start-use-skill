# Agent Initialization Conversation Script

This file contains the actual conversation flow that the agent follows during initialization. Each section contains the exact prompts and responses.

---

## Phase 1: Introduction & Consent

**Agent says:**
```
您好！我是 Hermes Agent 的初始化助手。我将引导您完成六项个性化设置：

1. **命名** — 为 Agent 取一个名字，设定您的称呼
2. **文件管理** — 建立规范的工作区目录结构（Chat、Department、Tools、Sessions）
3. **部门创建与 Kanban 团队配置** — 配置多 Agent 协作体系（可选）
4. **Obsidian 资料库** — 搭建三级知识管理系统
5. **办事习惯** — 设定协作规则
6. **会话归档** — 配置自动归档和存储路径

请确认以下方案：

---
【初始化方案】

### Step 1: Agent 命名
- 您需要提供：Agent 英文名、中文名、希望被如何称呼
- 存储位置：Hermes 记忆库（每次对话自动加载）

### Step 2: 文件管理规范
- 您需要提供：默认工作区路径
- 将创建：Chat/（日常对话）、Department/（部门任务）、Tools/（工作工具）、Sessions/（会话归档）
- 存储位置：文件系统 + 记忆库

### Step 3: 部门创建与 Kanban 团队配置（可选）
- 您需要提供：部门名称、展示名称、团队角色列表
- 将创建：部门目录、Profile 角色、Kanban 看板、工作流文档
- 存储位置：文件系统 + 记忆库 + config.yaml
- 前提：需要 Hermes Gateway 运行中
- **注意：如无开发团队计划可跳过此步骤**

### Step 4: Obsidian 资料库
- 您需要提供：Obsidian 库根目录
- 将创建：Memory-hub（记忆区）、Collect-hub（收藏区）、Knowledge-hub（知识区）
- 存储位置：文件系统 + 记忆库
- 前提：需已安装 Obsidian

### Step 5: 办事习惯
- 设定：先分析后执行、需明确指令才能行动
- 存储位置：记忆库

### Step 6: 会话归档配置
- 配置：自动归档开关、归档目录、保留天数
- 存储位置：Hermes config.yaml

---
确认后请回复「开始」，或提出修改意见。
```

---

## Phase 2: Step-by-Step Execution

### Step 1: 命名

**Agent 提问:**
```
【Step 1: 命名】

请告诉我：
1. 您希望我给 Agent 取什么英文名？（例如 Alice、Orion）
2. 中文名？（例如 艾莉丝、星野）
3. 您希望我如何称呼您？（例如 Boss、主人、您的名字）
```

**Agent 确认后说:**
```
已记录：
- Agent 名：{中文名}（{英文名}）
- 称呼您为：{称呼}

后续对话中我会使用这些称呼。
```

---

### Step 2: 文件管理

**Agent 提问:**
```
【Step 2: 文件管理规范】

请告诉我您的默认工作区路径（例如 F:\workspace\Hermes-Workspace）。
我将在此目录下创建：
- Chat/ — 日常对话临时文件
- Department/ — 部门/群组任务文件
- Tools/ — 工作工具（图片处理等）
- Sessions/ — Agent会话归档目录
```

**Agent 执行后确认:**
```
已创建目录结构：
{工作区路径}\Chat\
{工作区路径}\Department\
{工作区路径}\Tools\
{工作区路径}\Sessions\

文件管理约定：
• 日常对话 → Chat\日期-主题\Temp\ 和 output\
• 部门任务 → Department\部门名\Project\项目名\temp\ 和 output\
• 工作工具 → Tools\
• 会话归档 → Sessions\（自动归档，3天后）
```

**配置会话归档:**
```
【Step 2 续: 会话归档配置】

已配置以下会话归档设置：
• 自动归档：已开启
• 归档目录：{工作区路径}\Sessions\
• 归档周期：3天后自动归档
• 保留天数：90天

此设置已写入 Hermes config.yaml。
```

---

### Step 3: 部门创建与 Kanban 团队配置（可选）

**Agent 询问用户是否需要此步骤:**
```
【Step 3: 部门创建与 Kanban 团队配置】（可选）

此步骤用于配置多 Agent 协作体系。如果您不需要开发团队，可以跳过。

如需要，请告诉我：
1. 部门名称（如 Software-Development-Department）
2. 部门展示名称（如 软件开发部）
3. 团队角色列表（多个角色用逗号分隔，如 director、backend、frontend、tester）
```

**如果用户跳过:**
```
已记录：跳过部门创建与 Kanban 团队配置。
如需后续配置，可随时告诉我。
```

**如果用户需要:**

**Agent 执行后确认:**
```
【Step 3: 部门创建与 Kanban 团队配置】

已完成以下配置：

1. 部门目录：
   {工作区路径}\Department\{部门名称}\Project\

2. Profile 角色（已创建独立 Profile）：
   - director：项目总监，负责需求分析、任务拆解、代码审查
   - backend：后端开发
   - frontend：前端开发
   - tester：测试工程师
   （根据用户输入定制）

3. Kanban 看板：
   - Board 名称：{board-slug}
   - 默认工作区：{工作区路径}\Department\{部门名称}\Project\
   - Gateway 调度：已启动（每30秒轮询 ready 状态任务）

4. 工作流文档：
   {工作区路径}\Department\{部门名称}\WORKFLOW.md

5. Git worktree 支持：
   - 每个任务自动创建独立 worktree 目录 .worktrees/t_<task-id>-<role>/
   - 确保不同角色代码隔离

此设置已写入 Hermes config.yaml 和 memory。
```

---

### Step 4: Obsidian 资料库

**Agent 提问:**
```
【Step 4: Obsidian 资料库】

请告诉我您的 Obsidian 库根目录路径（例如 D:\mdhub）。
我将创建三个子库：
• Memory-hub（记忆区）— 第二记忆仓
• Collect-hub（收藏区）— 资料收藏
• Knowledge-hub（知识区）— 结构化知识

知识流向：记忆区 → 收藏区 → 知识区
```

**Agent 执行后确认:**
```
已创建 Obsidian 库目录：
{路径}\Memory-hub\
{路径}\Collect-hub\
{路径}\Knowledge-hub\

已为每个库创建 README 说明其用途。
```

---

### Step 5: 办事习惯

**Agent 说:**
```
【Step 5: 办事习惯】

已记录以下工作协议：
• 所有需求先整理问题分析和解决方案
• 必要时联网查询收集资料
• 未经您明确指令（"开始处理"、"继续工作"等），不擅自执行任务

此规则已存入记忆库，将在每次对话中生效。
```

---

## Phase 3: 完成报告

**Agent 输出:**
```
═══════════════════════════════════
  Agent 初始化调校完成报告
═══════════════════════════════════

一、命名设置
  Agent名：{中文名}（{英文名}）
  用户称呼：{称呼}

二、文件管理规范
  默认工作区：{路径}
  Chat目录：已创建 ✓
  Department目录：已创建 ✓
  Tools目录：已创建 ✓ — 工作工具存储
  Sessions目录：已创建 ✓ — 会话归档

三、部门创建与 Kanban 团队配置（如已设置）
  部门：{部门展示名称}
  部门目录：{工作区路径}\Department\{部门名称}\
  角色：{用户自定义的角色列表}
  Board: {board-slug}
  状态：✓ 已配置

四、Obsidian资料库
  根目录：{路径}
  记忆区：已创建 ✓
  收藏区：已创建 ✓
  知识区：已创建 ✓

五、办事习惯
  已保存至记忆库 ✓

六、Agent会话配置
  归档目录：{路径}\Sessions\
  自动归档：已开启（3天后）✓
  保留天数：90天

═══════════════════════════════════

初始化完成！今后每次对话我都会遵循这些约定。
如有需要可随时调整。
```

---

## Notes for Implementation

- Always wait for explicit "开始" or similar approval before executing any step
- After Step 0 (plan presentation), do NOT proceed without user confirmation
- Each step should be presented as a question, then executed only after answer
- Memory entries should be written immediately after each step's approval
- Directory creation should be verified with `terminal` commands
- If Obsidian is not installed, note it but continue with other steps
- If user skips Step 3 (Kanban), proceed directly to Step 4
- The working habits rule is critical: model it by not acting until explicitly told to start
- Session archive config is part of Step 2 (file management), not a separate step
