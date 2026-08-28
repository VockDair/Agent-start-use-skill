# Agent Start Use（Agent 启动向导）

Hermes Agent 的技能，用于引导新用户完成初始化配置和个性化设置。

## 概述

**Agent Start Use** 通过结构化的对话流程，引导新用户完成五项核心个性化设置：

1.**Agent 命名** — 设定 Agent 名字和您的称呼
2.**文件管理** — 建立规范的工作区目录结构（Chat、Department、Tools、Sessions）
3.**Obsidian 知识库** — 搭建三级知识管理系统
4.**办事习惯** — 设定协作规则和权限协议
5.**会话归档配置** — 设置自动归档和存储路径

该 Skill 采用交互式运行，**不会在未经您明确同意的情况下擅自执行** — 从一开始就践行"不批准不动手"的原则。

## 功能特性

- ✅ 分步骤引导设置，每一步都有清晰说明
- ✅ 强制规划阶段，任何操作前必须获得确认
- ✅ 自动保存偏好到记忆库，跨会话持久化
- ✅ 自动创建并验证目录结构
- ✅ 生成 Obsidian 知识库框架
- ✅ 建立工作协议规则
- ✅ 支持跨平台（Linux、macOS、Windows）

## 安装方法

### 方法一：手动安装

1. 下载此仓库或克隆：
   ```bash
   git clone https://github.com/your-org/agent-start-use.git
   ```

2. 将 Skill 目录复制到 Hermes 技能文件夹：
   ```bash
   cp -r agent-start-use ~/.hermes/skills/productivity/
   ```

3. 重启 Hermes Agent 或重载技能：
   ```bash
   hermes skills reload
   ```

### 方法二：通过 Hermes CLI 安装

如果此 Skill 已发布到 Hermes 技能注册表：
```bash
hermes skills install official/productivity/agent-start-use
```

## 使用方法

### 触发 Skill

说出以下任意短语即可启动初始化：
- **"初始化调校"**（中文触发词）
- "Help me set up my agent"
- "Guide me through onboarding"
- "Start fresh configuration"

### 执行流程

1. **Step 0 — 规划阶段**：Agent 展示完整设置方案，列出所有步骤、所需输入和存储位置
2. **Step 1 — 命名设置**：设定 Agent 名字和用户称呼
3. **Step 2 — 文件管理**：创建规范的工作区目录（含 Tools、Sessions）
4. **Step 3 — Obsidian 设置**：构建三级知识库
5. **Step 4 — 办事习惯**：保存交互协议到记忆库
6. **Step 5 — 会话配置**：设置自动归档和归档目录
7. **Step 6 — 验证报告**：生成完成报告

### 示例会话

```
用户: 初始化调校

Agent: 您好！我是 Hermes Agent 的初始化助手...
       [展示完整初始化方案]
       
用户: 开始

Agent: 【Step 1: 命名】请告诉我...
       [收集偏好并保存到记忆]
       
用户: Alice / 艾莉丝 / Boss

Agent: 已记录：我是艾莉丝（Alice），今后称呼您为 Boss。
       [继续后续步骤...]

═══════════════════════════════════
  Agent 初始化调校完成报告
═══════════════════════════════════
...
```

## 工作流程图

```
┌─────────────────────────────────────────────────────────────┐
│                    Step 0: 规划阶段                          │
│  展示完整方案 → 等待用户确认                                  │
└──────────────────────────┬──────────────────────────────────┘
                           │ 用户说"开始"
                           ▼
┌─────────────────────────────────────────────────────────────┐
│              Step 1: Agent 命名                              │
│  收集：英文名、中文名、用户称呼                               │
│  存储：记忆库（跨会话持久化）                                  │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│            Step 2: 文件管理                                  │
│  创建：Chat/、Department/、Tools/、Sessions/ 目录                    │
│  存储：文件系统 + 记忆库约定                                   │
│  额外：配置 sessions.auto_archive + archive_dir                      │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│            Step 3: Obsidian 知识库                           │
│  创建：Memory-hub、Collect-hub、Knowledge-hub                 │
│  存储：文件系统 + 记忆库约定                                   │
│  前提：需安装 Obsidian                                        │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│            Step 4: 办事习惯                                  │
│  保存：先分析后执行、需批准才能行动                            │
│  存储：记忆库                                                │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│            Step 5: 会话归档配置                              │
│  配置：sessions.auto_archive + archive_dir                   │
│  存储：Hermes config.yaml                                   │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│              Step 6: 验证报告                                │
│  生成包含所有设置的完成报告                                    │
└─────────────────────────────────────────────────────────────┘
```

## 目录结构

初始化完成后，您的工作区将按如下结构组织：

```
工作区根目录/
├── Chat/                          # 日常对话文件
│   └── YYYY-MM-DD-主题/
│       ├── Temp/                  # 临时文件
│       └── output/                # 产出物
│
├── Department/                    # 部门/团队任务文件
│   └── 部门名/
│       └── Project/
│           └── 项目类型-名称/
│               ├── temp/          # 临时文件
│               └── output/        # 产出物
│
├── Tools/                         # 工作工具（图片处理等）
│
└── Sessions/                      # Agent会话归档（自动归档）
    └── <日期>-<会话ID>/           # 归档的会话文件

Obsidian 库/
├── Memory-hub/                    # 记忆区 — 日常经验和洞察
├── Collect-hub/                   # 收藏区 — 资料收藏
└── Knowledge-hub/                 # 知识区 — 结构化知识
```

## 记忆条目

Skill 会向 Hermes 记忆库保存以下条目：

| 条目 | 内容 |
|------|------|
| Agent 名 | `Agent英文名 <name>，中文名 <name-cn>` |
| 用户称呼 | `用户称呼为 <address>` |
| 工作区路径 | `默认工作区：<path>` |
| 文件约定 | Chat/Department/Tools/Sessions 目录结构 |
| Obsidian 路径 | 库根目录和三个子库路径 |
| 知识流向 | `记忆区 → 收藏区 → 知识区` |
| 工作习惯 | 先分析后执行、需批准才能行动 |
| 会话归档 | `Sessions 归档目录：<path>\Sessions，自动归档：3天` |

---

## 跨 Agent 兼容性

本 Skill 遵循 **[agentskills.io](https://agentskills.io)** 开放标准，同一份 `SKILL.md` 可在多个主流 AI Agent 平台运行。

### 已验证兼容的 Agent 平台

| Agent 平台 | 兼容性 | 路径 |
|-----------|--------|------|
| **Hermes Agent** | ✅ 原生支持 | `~/.hermes/skills/` |
| **Claude Code** | ✅ 原生支持 | `~/.claude/skills/` |
| **OpenAI Codex** | ✅ 原生支持 | `~/.agents/skills/` |
| **OpenClaw** | ✅ 原生支持 | `~/.agents/skills/` |
| **Vercel skills.sh** | ✅ 原生支持 | `~/.skills/` |
| **LobeHub** | ✅ 原生支持 | 通过 `.well-known/skills/index.json` |
| **Cursor** | ⚠️ 需转换脚本 | 自动生成 `.cursorrules` |
| **Aider** | ⚠️ 需转换脚本 | 自动生成 `CONVENTIONS.md` |

### 配置共享目录

在 Hermes 的 `config.yaml` 中添加外部技能目录：

```yaml
skills:
  external_dirs:
    - ~/.agents/skills/      # 共享技能库
    - ~/.claude/skills/      # Claude Code 技能
```

### 注意事项

- ✅ Hermes 专有字段（`metadata.hermes.*`）会被其他 Agent 忽略，安全无影响
- ✅ 核心技能格式跨平台通用，无需重复编写
- ⚠️ 部分 Hermes 专用工具在其他 Agent 中不可用，但基础功能仍生效

---

## 前置要求

- **Hermes Agent** 已安装并运行
- **Obsidian**（可选）— 仅 Step 3 需要；如未安装可跳过
- **基本终端访问权限** — 用于执行目录创建命令

## 注意事项

### 用户须知
- ✅ 仔细审阅 Step 0 的方案后再确认
- ✅ 提供绝对路径（如 `F:\workspace\Hermes-Workspace`）
- ✅ 如需 Step 3 的知识库功能，请确保已安装 Obsidian

### 技能作者须知
- ⚠️ 未经用户明确批准绝不擅自执行
- ⚠️ 使用 `terminal` 命令验证目录创建是否成功
- ⚠️ 记忆条目保持简洁（一条记忆一个事实）
- ⚠️ Windows 上使用正斜杠（如 `C:/Users/...`）

## 相关 Skills

- [`hermes-agent`](https://hermes-agent.nousresearch.com/docs) — Hermes Agent 核心配置
- [`obsidian`](../note-taking/obsidian) — 读取和编辑 Obsidian 笔记
- [`weekly-review-planning`](../productivity/weekly-review-planning) — 定期维护知识库

## 许可证

MIT License — 详见 [LICENSE](LICENSE)

## 作者

Hermes Agent

## 支持

- Hermes Agent 文档：https://hermes-agent.nousresearch.com/docs
- GitHub Issues：[创建 Issue](../../issues)

---

<div align="center">

**用 ❤️ 为 Hermes Agent 社区打造**

</div>
