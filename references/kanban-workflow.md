# 软件开发部 Kanban 工作流规范

## 一、角色职责

| 角色 | Profile | 主要任务 |
|------|---------|----------|
| 项目总监 | director | 需求分析、任务拆解、进度把控、代码审查 |
| 后端开发 | backend | API设计、数据库建模、业务逻辑 |
| 前端开发 | frontend | UI组件、交互逻辑、性能优化 |
| 全栈开发 | coder | 独立模块端到端交付 |
| 测试工程师 | tester | 用例设计、自动化测试、质量保障 |

---

## 二、项目目录结构规范

### 2.1 统一规范（所有部门）

```
F:/workspace/Hermes-Workspace/
└── Department/
    └── <部门名称>/
        └── Project/
            └── <项目名称>/                    # 每个项目一个目录
                ├── kanban-workspace/          # ← Kanban临时文件存放区
                ├── src/                       # 源代码
                ├── .git/                      # Git仓库
                └── README.md
```

**示例：软件开发部 - 消消乐小游戏项目**
```
F:\workspace\Hermes-Workspace\Department\Software-Development-Department\Project\Game-xiaoxiaole\
├── kanban-workspace\    # Kanban任务临时文件存放区
├── src\                 # 源代码目录
├── .git\                # Git仓库
└── README.md
```

### 2.2 目录用途说明

| 目录 | 用途 | 创建方式 |
|------|------|----------|
| `kanban-workspace/` | Kanban任务临时文件存储 | 手动创建 |
| `.worktrees/` | Git工作区隔离（自动管理） | kanban创建任务时自动生成 |
| `src/` | 源代码 | 开发时创建 |

### 2.3 关键规则

- **所有部门统一使用此结构**
- 部门目录位于 `Department/<部门名称>/Project/`
- `kanban-workspace/` 用于存储 Kanban 任务处理过程中的临时文件
- Git worktree 用于代码隔离开发
- 必须先初始化 Git 仓库再创建 Kanban 任务

---

## 三、任务状态流转

```
┌─────────┐   ┌───────┐   ┌────────┐   ┌──────────┐   ┌────────┐
│ triage  │ → │ todo  │ → │ ready  │ → │ running  │ → │ done   │
│ (待分类)│   │ (待规划)│   │ (就绪) │   │ (开发中) │   │ (完成) │
└─────────┘   └───────┘   └────────┘   └──────────┘   └────────┘
                    ↑                                      ↓
              ┌─────────┐                          ┌─────────────┐
              │ blocked │ ←─────────────────────────│ review      │
              │ (阻塞)  │                          │ (审查中)     │
              └─────────┘                          └─────────────┘
```

---

## 四、开发流程

### Step 1: 创建部门项目目录
```bash
mkdir -p "F:/workspace/Hermes-Workspace/Department/<部门名称>/Project"
```

### Step 2: 创建项目目录
```bash
mkdir -p "F:/workspace/Hermes-Workspace/Department/<部门名称>/Project/<项目名>/kanban-workspace"
```

### Step 3: 初始化Git并创建项目
```bash
cd "F:/workspace/Hermes-Workspace/Department/<部门名称>/Project/<项目名>"
git init
echo "# <项目名>" > README.md
git add .
git commit -m "Initial commit"

hermes project create --slug <项目名> --primary "F:/workspace/Hermes-Workspace/Department/<部门名称>/Project/<项目名>" --board software-dev "<显示名称>"
```

### Step 4: 需求入库（director）
```bash
hermes kanban --board software-dev create "需求标题" --body "需求描述" --triage --project <项目名>
```

### Step 5: 任务拆解（director）
```bash
hermes kanban decompose <task-id>
```

### Step 6: 并行开发（各角色）
- 各角色从 `ready` 领取任务
- Git worktree 自动创建在 `.worktrees/` 目录
- 临时文件存放在 `kanban-workspace/`
- 完成后提交 `request-review`

### Step 7: 代码审查（director）
```bash
hermes kanban request-changes <task-id>  # 需要修改
hermes kanban complete <task-id>         # 审查通过
```

### Step 8: 测试验证（tester）
```bash
hermes kanban complete <task-id>         # 测试通过
```

---

## 五、常用命令速查

### 项目管理
| 操作 | 命令 |
|------|------|
| 查看项目 | `hermes project list` |
| 查看项目详情 | `hermes project show <项目名>` |
| 绑定看板 | `hermes project bind-board <项目名> software-dev` |

### Kanban任务
| 操作 | 命令 |
|------|------|
| 查看看板 | `hermes kanban --board software-dev list` |
| 查看统计 | `hermes kanban --board software-dev stats` |
| 创建任务 | `hermes kanban create "标题" --body "描述" --assignee <角色> --project <项目名>` |
| 指定项目 | `--project <项目名>` |
| 领取任务 | `hermes kanban claim` |
| 请求审查 | `hermes kanban request-review <task-id>` |
| 完成任务 | `hermes kanban complete <task-id>` |
| 阻塞任务 | `hermes kanban block <task-id>` |
| 添加评论 | `hermes kanban comment <task-id> "评论内容"` |

---

## 六、工作流示例

### 创建消消乐小游戏项目
```bash
# 1. 创建部门项目目录
mkdir -p "F:/workspace/Hermes-Workspace/Department/Software-Development-Department/Project/Game-xiaoxiaole/kanban-workspace"

# 2. 初始化Git
cd "F:/workspace/Hermes-Workspace/Department/Software-Development-Department/Project/Game-xiaoxiaole"
git init
echo "# 消消乐小游戏" > README.md
git add . && git commit -m "Initial commit"

# 3. 创建项目
hermes project create --slug game-xiaoxiaole --primary "F:/workspace/Hermes-Workspace/Department/Software-Development-Department/Project/Game-xiaoxiaole" --board software-dev "消消乐小游戏"
```

### 添加任务到项目
```bash
# 创建后端任务
hermes kanban create "游戏API接口" --body "实现游戏开始、计分、排行榜接口" --assignee backend --project game-xiaoxiaole

# 创建前端任务
hermes kanban create "游戏UI界面" --body "实现消除动画、计分显示、重新开始按钮" --assignee frontend --project game-xiaoxiaole

# 创建依赖关系
hermes kanban link <后端任务id> <前端任务id>
```

---

## 七、常见问题

### Worktree 创建失败
**错误**: `git worktree add failed... fatal: invalid reference: HEAD`

**原因**: Git 仓库未初始化或没有提交。

**解决**:
```bash
cd /path/to/project
echo "# Project" > README.md
git add README.md
git commit -m "Initial commit"
```

### 任务一直停留在 ready
**原因**: Gateway 未运行。

**解决**: `hermes gateway start`

### 工作区路径不在 Git 仓库内
**错误**: `workspace path is not inside a git repo`

**解决**: 确保项目目录已初始化 Git 仓库后再创建任务。

---

## 八、配置示例

Director profile 需要启用 kanban 配置：
```yaml
# ~/.hermes/profiles/director/config.yaml
kanban:
  review_dispatch: true
  dispatch_interval_seconds: 30
```

---

## 九、部门项目目录结构汇总

```
F:/workspace/Hermes-Workspace/
└── Department/
    └── <部门名称>/
        ├── Project/                    # 项目根目录
        │   ├── Game-xiaoxiaole/        # 消消乐小游戏项目
        │   │   ├── kanban-workspace/   # Kanban临时文件
        │   │   ├── src/                # 源代码
        │   │   ├── .git/               # Git仓库
        │   │   └── README.md
        │   ├── Auth-System/            # 认证系统项目
        │   │   ├── kanban-workspace/
        │   │   ├── src/
        │   │   ├── .git/
        │   │   └── README.md
        │   └── ...
        └── kanban-workflow.md          # 工作流文档
```
