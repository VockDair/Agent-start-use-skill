# Agent Start Use

A Hermes Agent skill for guided onboarding and personalization setup.

## Overview

**Agent Start Use** guides new Hermes Agent users through a structured, conversational onboarding process covering five core personalization areas:

1. **Agent Naming** — Set agent display name and user address
2. **File Management** — Establish organized workspace directory structure (Chat, Department, Tools, Sessions)
3. **Obsidian Knowledge Base** — Create a three-tier knowledge system
4. **Working Habits** — Define interaction protocols and permissions
5. **Session Archiving** — Configure auto-archive and storage path

The skill runs interactively and **never auto-executes** without explicit user approval — modeling the "don't act without permission" principle from day one.

## Features

- ✅ Step-by-step guided setup with clear explanations
- ✅ Mandatory planning phase before any execution
- ✅ Automatic memory persistence for all preferences
- ✅ Directory creation and verification
- ✅ Obsidian vault structure generation
- ✅ Working protocol establishment
- ✅ Cross-platform support (Linux, macOS, Windows)

## Installation

### Method 1: Manual Installation

1. Download this repository or clone it:
   ```bash
   git clone https://github.com/VockDair/Agent-start-use-skill.git
   ```

2. Copy the skill directory to your Hermes skills folder:
   ```bash
   cp -r agent-start-use ~/.hermes/skills/productivity/
   ```

3. Restart Hermes Agent or reload skills:
   ```bash
   hermes skills reload
   ```

### Method 2: Via Hermes CLI

If this skill is published to the Hermes skills registry:
```bash
hermes skills install official/productivity/agent-start-use
```

## Usage

### Trigger the Skill

Say any of these phrases to start the initialization:
- **"初始化调校"** (Chinese trigger)
- "Help me set up my agent"
- "Guide me through onboarding"
- "Start fresh configuration"

### What Happens

1. **Step 0 — Planning**: Agent presents a complete setup plan with all steps, required inputs, and storage locations
2. **Step 1 — Naming**: Set agent name and user address
3. **Step 2 — File Management**: Create organized workspace directories (including Tools and Sessions)
4. **Step 3 — Obsidian Setup**: Build three-tier knowledge base
5. **Step 4 — Working Habits**: Save interaction protocols to memory
6. **Step 5 — Session Configuration**: Configure auto-archive and archive directory
7. **Step 6 — Verification**: Generate completion report

### Example Session

```
User: 初始化调校

Agent: 您好！我是 Hermes Agent 的初始化助手...
       [presents full initialization plan]
       
User: 开始

Agent: 【Step 1: 命名】请告诉我...
       [collects preferences and saves to memory]
       
User: Alice / 艾莉丝 / Boss

Agent: 已记录：我是艾莉丝（Alice），今后称呼您为 Boss。
       [continues through all steps...]

═══════════════════════════════════
  Agent 初始化调校完成报告
═══════════════════════════════════
...
```

## Workflow Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                    Step 0: Planning                         │
│  Present full setup plan → Wait for user approval           │
└──────────────────────────┬──────────────────────────────────┘
                           │ User says "开始"
                           ▼
┌─────────────────────────────────────────────────────────────┐
│              Step 1: Agent Naming                           │
│  Collect: English name, Chinese name, user address          │
│  Store: Memory (persists across sessions)                   │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│            Step 2: File Management                          │
│  Create: Chat/, Department/, Tools/, Sessions/ directories  │
│  Store: Filesystem + Memory convention                      │
│  Extra: Configure sessions.auto_archive + archive_dir       │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│            Step 3: Obsidian Knowledge Base                  │
│  Create: Memory-hub, Collect-hub, Knowledge-hub             │
│  Store: Filesystem + Memory convention                      │
│  Prerequisite: Obsidian installed                           │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│            Step 4: Working Habits                           │
│  Save: Analysis-first, approval-required protocols          │
│  Store: Memory                                              │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│            Step 5: Session Archive Configuration            │
│  Configure: sessions.auto_archive + archive_dir             │
│  Store: Hermes config.yaml                                  │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│              Step 6: Verification                           │
│  Generate completion report with all settings               │
└─────────────────────────────────────────────────────────────┘
```

## Directory Structure

After initialization, your workspace will be organized as:

```
Workspace Root/
├── Chat/                          # Daily conversation files
│   └── YYYY-MM-DD-topic/
│       ├── Temp/                  # Temporary files
│       └── output/                # Outputs and artifacts
│
├── Department/                    # Department/team task files
│   └── team-name/
│       └── Project/
│           └── project-type-name/
│               ├── temp/          # Temporary files
│               └── output/        # Outputs and artifacts
│
├── Tools/                         # Working tools (image processing, etc.)
│
└── Sessions/                      # Agent session archive (auto-archive)
    └── <date>-<session-id>/       # Archived session files

Obsidian Vault/
├── Memory-hub/                    # Daily insights & experiences
├── Collect-hub/                   # Collected resources
└── Knowledge-hub/                 # Structured knowledge
```

## Memory Entries

The skill saves these entries to Hermes memory:

| Entry | Content |
|-------|---------|
| Agent name | `Agent英文名 <name>，中文名 <name-cn>` |
| User address | `用户称呼为 <address>` |
| Workspace path | `默认工作区：<path>` |
| File conventions | Chat/Department/Tools/Sessions directory structure |
| Obsidian paths | Vault root and three sub-directories |
| Knowledge flow | `记忆区 → 收藏区 → 知识区` |
| Working habits | Analysis-first, approval-required rules |
| Session archive | `Sessions archive directory: <path>\Sessions, auto-archive: 3 days` |

---

## Cross-Agent Compatibility

This skill follows the **[agentskills.io](https://agentskills.io)** open standard, meaning the same `SKILL.md` works across multiple AI agent platforms.

### Verified Compatible Agent Platforms

| Agent Platform | Compatibility | Path |
|---------------|---------------|------|
| **Hermes Agent** | ✅ Native support | `~/.hermes/skills/` |
| **Claude Code** | ✅ Native support | `~/.claude/skills/` |
| **OpenAI Codex** | ✅ Native support | `~/.agents/skills/` |
| **OpenClaw** | ✅ Native support | `~/.agents/skills/` |
| **Vercel skills.sh** | ✅ Native support | `~/.skills/` |
| **LobeHub** | ✅ Native support | Via `.well-known/skills/index.json` |
| **Cursor** | ⚠️ Conversion script needed | Auto-generates `.cursorrules` |
| **Aider** | ⚠️ Conversion script needed | Auto-generates `CONVENTIONS.md` |

### Configuring Shared Directory

Add external skill directories to Hermes' `config.yaml`:

```yaml
skills:
  external_dirs:
    - ~/.agents/skills/      # Shared skill library
    - ~/.claude/skills/      # Claude Code skills
```

### Notes

- ✅ Hermes-specific fields (`metadata.hermes.*`) are safely ignored by other agents
- ✅ Core skill format is cross-platform compatible — no need to rewrite
- ⚠️ Some Hermes-specific tools may not be available in other agents, but core functionality works

---

## Prerequisites

- **Hermes Agent** installed and running
- **Obsidian** (optional) — required only for Step 3; can be skipped if not installed
- **Basic terminal access** — for directory creation commands

## Pitfalls & Best Practices

### For Users
- ✅ Review the Step 0 plan carefully before confirming
- ✅ Provide absolute paths (e.g., `F:\workspace\Hermes-Workspace`)
- ✅ Ensure Obsidian is installed before Step 3 if you want the knowledge base

### For Skill Authors
- ⚠️ Never auto-execute without explicit user approval
- ⚠️ Verify directory creation with `terminal` commands
- ⚠️ Keep memory entries concise (one fact per entry)
- ⚠️ Use forward slashes in terminal commands on Windows

## Related Skills

- [`hermes-agent`](https://hermes-agent.nousresearch.com/docs) — Core Hermes Agent configuration
- [`obsidian`](../note-taking/obsidian) — Read/write notes in Obsidian vaults
- [`weekly-review-planning`](../productivity/weekly-review-planning) — Regular knowledge base maintenance

## License

MIT License — see [LICENSE](LICENSE) for details.

## Author

Hermes Agent

## Support

- Hermes Agent Documentation: https://hermes-agent.nousresearch.com/docs
- GitHub Issues: [Create an issue](https://github.com/VockDair/Agent-start-use-skill/issues)

---

<div align="center">

**Built with ❤️ for the Hermes Agent community**

</div>
