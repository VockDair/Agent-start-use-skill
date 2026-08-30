# Agent Start Use Skill（初始化调校）

指导 Hermes Agent 完成结构化、对话式的初始化配置流程，涵盖文件管理、部门创建与 Kanban 团队配置、Obsidian 知识库和会话归档。

## 目的

确保新的 Hermes Agent 实例能够正确配置以下七大模块：
1. Agent 命名和用户偏好设置
2. 标准化文件管理规范
3. 部门创建与 Kanban 团队配置
4. Obsidian 知识库集成
5. 工作习惯协议
6. 会话归档配置

## 核心组件

### Step 1: Agent 命名
- 设置 Agent 显示名称和用户称呼
- 存储在 memory 中用于个性化交互

### Step 2: 文件管理规范
- 建立工作区根目录和子目录结构
- **部门项目结构：**
  - `F:/workspace/Hermes-Workspace/Department/<部门名称>/Project/<项目名>/`
  - Kanban 工作区：`<项目名>/kanban-workspace/`
  - Git worktree 自动创建在 `.worktrees/`

### Step 3: 部门创建与 Kanban 团队配置（可选）
**仅当用户确认需要时执行。**

5 步流程：
1. **建立 Profile 角色** — 创建 director/backend/frontend/coder/tester 各独立 Profile
2. **创建部门** — 建立部门物理目录 `<workspace>/Department/<部门名称>/Project/`
3. **角色入职部门** — 在 memory 中记录部门架构，配置 director 的 kanban 权限
4. **建立部门流程** — 文档化协作规范至 WORKFLOW.md
5. **配置 Kanban 与工作区** — 初始化看板，设置默认工作区，启动 Gateway

### Step 4: Obsidian 知识库
- 创建 Memory-hub、Collect-hub、Knowledge-hub
- 建立知识提炼流程

### Step 5: 工作习惯
- 文档化交互协议
- 在 memory 中存储行为规则

### Step 6: 验证与总结
- 生成初始化完成报告

## 关键特性

- ✅ 交互式执行，每步需用户确认
- ✅ 不可自动执行任务
- ✅ Step 3 完全可选（无部门计划则跳过）
- ✅ 支持 Windows/Linux/macOS
- ✅ 集成 Git worktree 支持

## 相关文件

- `SKILL.md` — 主技能文档（含详细步骤）
- `references/kanban-workflow.md` — Kanban 工作流详细规范
- `references/templates.md` — SOUL.md 角色模板
- `references/conversation-script.md` — 对话脚本

## 使用方法

触发方式："初始化调校" 或类似请求。

始终先展示完整计划（Step 0），等待用户明确批准后再执行。

## 版本历史

- v0.5.0 — 每步添加详细功能描述；Step 3 拆分为 5 个子步骤；新增会话归档配置
- v0.4.0 — 修正部门目录路径（Software-Development-Department）
- v0.3.0 — 新增 Kanban 项目目录规范和团队配置步骤
- v0.2.0 — 初始版本
