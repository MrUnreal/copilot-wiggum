<p align="center">
  <img src="assets/logo.png" alt="Copilot Wiggum" width="300">
</p>

<h1 align="center">🚔 Copilot Wiggum</h1>

<p align="center">
  <strong>Multi-Agent Orchestrator for GitHub Copilot</strong><br>
  <em>"I'm helping!"</em>
</p>

<p align="center">
  <a href="#-quick-start">Quick Start</a> •
  <a href="#-how-it-works">How It Works</a> •
  <a href="#-usage">Usage</a> •
  <a href="#-agent-types">Agent Types</a>
</p>

---

## 🍩 What is this?

Copilot Wiggum is a **multi-agent orchestration system** for GitHub Copilot. It breaks down complex tasks into specialized sub-tasks, delegates them to expert agents, and synthesizes the results.

Think of it as Chief Wiggum managing a squad of specialist officers — each one handles their part, and the chief brings it all together.

## ⚡ Quick Start

### 1. Copy to your repo

```bash
# Clone this repo
git clone git@github.com:MrUnreal/copilot-wiggum.git

# Copy the .github folder to your project
cp -r copilot-wiggum/.github your-project/
```

### 2. Structure

```
your-project/
└── .github/
    ├── agents/
    │   └── orchestrator.agent.md    # The orchestrator agent
    ├── skills/
    │   ├── research-skill.md        # Research specialist guidelines
    │   ├── backend-skill.md         # Backend specialist guidelines
    │   ├── frontend-skill.md        # Frontend specialist guidelines
    │   ├── testing-skill.md         # Testing specialist guidelines
    │   └── security-skill.md        # Security specialist guidelines
    ├── prompts/
    │   └── multi-agent-task.prompt.md   # Reusable prompt template
    └── copilot-instructions.md      # Auto-applied instructions
```

### 3. Use it

In VS Code with GitHub Copilot Chat, type:

```
@Orchestrator Build a REST API for a blog with posts and comments
```

That's it! The orchestrator will:
1. Break down the task
2. Spawn specialized agents (research, backend, frontend, etc.)
3. Coordinate via shared memory
4. Synthesize the final result

## 🧠 How It Works

```
┌─────────────────────────────────────────────────────────────┐
│                     YOU                                      │
│              "Build feature X"                               │
└─────────────────────┬───────────────────────────────────────┘
                      ▼
┌─────────────────────────────────────────────────────────────┐
│                 ORCHESTRATOR                                 │
│  • Breaks down task into objectives                         │
│  • Creates memory structure                                 │
│  • Spawns specialist agents                                 │
│  • Tracks progress until objectives met                     │
└─────────────────────┬───────────────────────────────────────┘
                      ▼
┌──────────┬──────────┬──────────┬──────────┬────────────────┐
│ Research │ Backend  │ Frontend │ Testing  │ Security       │
│  Agent   │  Agent   │  Agent   │  Agent   │  Agent         │
└────┬─────┴────┬─────┴────┬─────┴────┬─────┴────┬───────────┘
     │          │          │          │          │
     └──────────┴──────────┴──────────┴──────────┘
                      ▼
              /memories/project-xxx/
              (Shared memory for handoffs)
```

### Objective-Based Loops

Instead of fixed iteration counts, Wiggum uses **objectives**:

```markdown
| ID | Objective                    | Status |
|----|------------------------------|--------|
| O1 | Handles null input           | ✅ PASS |
| O2 | Validates required fields    | ✅ PASS |
| O3 | Returns proper error format  | 🔄 FAIL |
```

The loop continues until all objectives pass — not after N iterations.

### Resumeable State

All state is persisted to `/memories/`. If a session ends mid-task, the next session can resume exactly where it left off.

## 📖 Usage

### Option 1: Invoke the Agent

```
@Orchestrator <your complex task>
```

### Option 2: Use the Prompt Template

Open `.github/prompts/multi-agent-task.prompt.md` and fill in:
- Task description
- Project type
- Constraints

### Example Tasks

```
@Orchestrator Build a user authentication system with JWT tokens

@Orchestrator Create a dashboard with charts showing sales data

@Orchestrator Refactor the payment module to use Stripe

@Orchestrator Add comprehensive tests for the user service
```

## 🤖 Agent Types

| Agent | Specialty |
|-------|-----------|
| **Research** | Best practices, architecture, technology evaluation |
| **Backend** | API design, server logic, database schemas |
| **Frontend** | UI components, user flows, responsive design |
| **Testing** | Unit tests, integration tests, test strategies |
| **Security** | Auth, authorization, vulnerability analysis |

Each agent has a skill file in `.github/skills/` that defines its behavior.

## 🔧 Customization

### Add Your Own Agent Type

1. Create `.github/skills/your-agent-skill.md`
2. Define responsibilities, output format, quality standards
3. The orchestrator will automatically use it

### Modify Skill Definitions

Edit any file in `.github/skills/` to match your team's standards:
- Code style preferences
- Technology stack
- Testing requirements
- Documentation format

## 📝 Memory Structure

When running a task, Wiggum creates:

```
/memories/project-{id}/
├── objectives/           # What "done" looks like
├── code/                 # Versioned implementations
├── evaluations/          # Pass/fail for each objective
└── loop-state/           # Resumeable state
```

## 🚀 Requirements

- VS Code with GitHub Copilot extension
- GitHub Copilot Chat enabled
- Access to custom agents feature (`.github/agents/`)

## 📜 License

MIT — Do what you want with it.

---

<p align="center">
  <em>"Bake 'em away, toys!"</em>
</p>
