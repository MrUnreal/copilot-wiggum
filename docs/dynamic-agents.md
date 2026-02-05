# 🤖 Dynamic Agents

> *"I bent my wookiee."* — Ralph, on code refactoring

Unlike traditional setups with preset agent types, Wiggum **generates agents on-the-fly** based on what each task needs.

## Any Specialist You Need

> *"That's where I saw the leprechaun. He told me to burn things."* — Ralph, on specialist selection

The orchestrator spawns whatever expert the task requires:

| Common Agents | Specialized Agents |
|---------------|-------------------|
| Research Analyst | Data Pipeline Engineer |
| API Architect | ML Ops Specialist |
| Database Architect | Accessibility Expert |
| Frontend Engineer | Localization Specialist |
| Backend Engineer | Compliance Analyst |
| QA Engineer | DevRel Writer |
| Security Engineer | Cost Optimization Analyst |
| Code Reviewer | ... anything the task needs |

## Agent Prompt Generation

Each dynamically-generated agent receives:

- **Mission** — What exactly to accomplish
- **Context** — What to read from previous agents
- **Constraints** — Technology/style requirements  
- **Output** — Where to write results
- **Quality standards** — What "good" looks like

## Example

```
@Orchestrator Build a real-time chat system with WebSocket support
```

The orchestrator might spawn:
1. **Research Agent** — Investigate WebSocket libraries
2. **Backend Engineer** — Build the socket server
3. **Frontend Engineer** — Create the chat UI
4. **Security Engineer** — Audit the implementation
5. **QA Engineer** — Write integration tests
6. **Code Reviewer** — Final review loop

Each agent is created with a tailored prompt — no preset configurations needed.
