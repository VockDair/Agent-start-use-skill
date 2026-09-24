# Agent Start Use Skill

Guides Hermes Agent onboarding setup with file management, Kanban project standards, Obsidian knowledge base, and session archiving.

## Purpose

Ensures new Hermes Agent instances are properly configured with:
1. Agent naming and user preferences
2. Standardized file management structure
3. Department creation and Kanban team setup
4. Obsidian knowledge base integration
5. Working habit protocols
6. Session archiving configuration

## Key Components

### Step 1: Agent Naming
- Sets agent display name and user address
- Stored in memory for personalized interactions

### Step 2: File Management Standards
- Establishes workspace root and subdirectories
- **Chat/ three-level structure:**
  - `Chat/<date>-<session-theme>/<content-name>/temp/` — temporary files (drafts, intermediates)
  - `Chat/<date>-<session-theme>/<content-name>/output/` — final outputs (reports, charts, docs)
  - Level 1 `<date>-<session-theme>`: format `YYYYMMDD-session-theme`, e.g., `20260925-song-creation`
  - Level 2 `<content-name>`: specific object in the session, e.g., song names A/B
- **Department project structure:**
  - `D:/WorkSpace/Hermes-workspace/Department/<department>/Project/<project>/`
  - Kanban workspace: `<project>/kanban-workspace/`
  - Git worktree auto-created in `.worktrees/`

### Step 3: Department Creation & Kanban Team Setup (Optional)
**Execute only when user confirms need.**

5-step process:
1. **Establish Profile Roles** — Create director/backend/frontend/coder/tester profiles
2. **Create Department** — Build directory structure `<workspace>/Department/<name>/Project/`
3. **Role Onboarding** — Persist department structure to memory, configure director kanban permissions
4. **Establish Workflow** — Document collaboration rules in WORKFLOW.md
5. **Configure Kanban & Workspace** — Initialize board, set default workdir, start gateway

### Step 4: Obsidian Knowledge Base
- Creates Memory-hub, Collect-hub, Knowledge-hub
- Establishes knowledge refinement pipeline

### Step 5: Working Habits
- Documents interaction protocols
- Stores behavioral rules in memory

### Step 6: Verification & Summary
- Generates initialization completion report

## Key Features

- ✅ Interactive execution, requires user confirmation at each step
- ✅ Never auto-execute tasks
- ✅ Step 3 fully optional (skip if no department plans)
- ✅ Supports Windows/Linux/macOS
- ✅ Integrated Git worktree support

## Related Files

- `SKILL.md` — Main skill documentation (with detailed steps)
- `references/kanban-workflow.md` — Detailed Kanban workflow
- `references/templates.md` — SOUL.md role templates
- `references/conversation-script.md` — Conversation scripts

## Usage

Trigger with: "初始化调校" or similar onboarding requests.

Always presents full plan first (Step 0), then awaits explicit user approval before executing.

## Version History

- v0.6.0 — Chat/ directory updated to three-level structure (<date>-<session-theme>/<content-name>/temp+output); workspace path changed to D:/WorkSpace/Hermes-workspace
- v0.5.0 — Added detailed functional descriptions to each step; split Step 3 into 5 sub-steps; added session archiving
- v0.4.0 — Fixed department directory path (Software-Development-Department)
- v0.3.0 — Added Kanban project directory standards and team setup step
- v0.2.0 — Initial release
