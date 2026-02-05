# 🧠 How It Works

> *"The doctor said I wouldn't have so many nosebleeds if I kept my finger outta there."* — Ralph, on debugging

## Architecture

```mermaid
flowchart TD
    A[👤 YOU<br/>'Build feature X'] --> B[🎯 ORCHESTRATOR]
    
    B --> C[📋 Break down task<br/>into objectives]
    C --> D[🤖 Spawn specialist agents]
    D --> E[Research Agent]
    D --> F[Backend Agent]
    D --> G[Frontend Agent]
    D --> H[Testing Agent]
    D --> I[Security Agent]
    
    E --> J[📁 /memories/project-xxx/<br/>Shared memory for handoffs]
    F --> J
    G --> J
    H --> J
    I --> J
    
    J --> K[✅ Synthesize results]
    
    style A fill:#e1f5fe
    style B fill:#fff3e0
    style K fill:#c8e6c9
```

## Objective-Based Loops

> *"When I grow up, I'm going to Bovine University!"* — Ralph, setting objectives

Instead of fixed iteration counts, Wiggum uses **objectives**:

| ID | Objective | Status |
|----|-----------|--------|
| O1 | Handles null input | ✅ PASS |
| O2 | Validates required fields | ✅ PASS |
| O3 | Returns proper error format | 🔄 FAIL |

The loop continues until all objectives pass — not after N iterations.

| Approach | How it works |
|----------|--------------|
| ❌ Fixed iterations | "Review 3 times then give up" |
| ✅ **Objective-based** | "Keep going until tests pass, security is verified, and code review approves" |

## Iteration Flow

```mermaid
flowchart TB
    subgraph iter1["🔄 ITERATION 1"]
        A1[🔧 Backend Engineer<br/>writes auth module] --> B1[🔍 Code Reviewer<br/>evaluates objectives]
        B1 --> C1{All objectives<br/>pass?}
        C1 -->|"❌ 2/4 passed"| D1[O1: Null handling ✅<br/>O2: bcrypt ✅<br/>O3: JWT refresh ❌<br/>O4: Rate limiting ❌]
    end
    
    D1 --> iter2
    
    subgraph iter2["🔄 ITERATION 2"]
        A2[🔧 Backend Engineer<br/>reads review, fixes issues] --> B2[🔍 Code Reviewer<br/>re-evaluates]
        B2 --> C2{All objectives<br/>pass?}
        C2 -->|"✅ 4/4 passed"| D2[O1: Null handling ✅<br/>O2: bcrypt ✅<br/>O3: JWT refresh ✅<br/>O4: Rate limiting ✅]
    end
    
    D2 --> E[✅ COMPLETE]
    
    style iter1 fill:#fff3cd,stroke:#ffc107
    style iter2 fill:#d4edda,stroke:#28a745
    style E fill:#28a745,color:#fff
```

## Resumeable State

All state is persisted to `/memories/`. If a session ends mid-task, the next session can resume exactly where it left off. *"I remember my first thought ever!"*

## Memory Structure

> *"I eated the purple berries!"* — Ralph, on persisting state

When running a task, Wiggum creates:

```
/memories/project-{id}/
├── objectives/           # What "done" looks like
├── code/                 # Versioned implementations
├── evaluations/          # Pass/fail for each objective
└── loop-state/           # Resumeable state
```

## Agent Prompt Generation

Each agent gets a custom prompt with:
- **Mission** — What exactly to accomplish
- **Context** — What to read from previous agents
- **Constraints** — Technology/style requirements  
- **Output** — Where to write results
- **Quality standards** — What "good" looks like
