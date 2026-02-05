---
description: Orchestrate a multi-agent team to complete a complex development task
---

# Multi-Agent Development Task

## Objective
${{task_description:Describe the feature or system to build (e.g., "Build a user authentication system with JWT tokens, password reset, and OAuth2 support")}}

## Project Context
${{project_type:What type of project is this? (e.g., "Web API", "Full-stack app", "CLI tool")}}

## Constraints
${{constraints:Any technical constraints? (e.g., "Use PostgreSQL", "Must work with existing Express app", "Node.js 18+")}}

---

## Instructions for Orchestrator

1. **Initialize Project Memory**
   - Create project structure at `/memories/project-{slug}/`
   - Set up orchestrator state and task queue

2. **Decompose the Task**
   - Break down into specialized sub-tasks
   - Identify agent types needed (research, backend, frontend, testing)
   - Determine dependencies between tasks

3. **Load Skills**
   - Copy relevant skills from `.github/skills/` to project memory
   - Customize skills for this specific project

4. **Execute Sequentially**
   - Run research tasks first
   - Run implementation tasks based on dependency order
   - Verify each agent's output before proceeding

5. **Synthesize Results**
   - Combine all agent outputs into cohesive deliverable
   - Present complete solution to user

---

## Example Task Queue

```markdown
| ID | Type | Task | Dependencies | Status |
|----|------|------|--------------|--------|
| 001 | research | Research authentication best practices | none | pending |
| 002 | backend | Design API endpoints | 001 | pending |
| 003 | backend | Implement auth service | 002 | pending |
| 004 | frontend | Design login/register components | 002 | pending |
| 005 | testing | Write integration tests | 003, 004 | pending |
```

---

Execute now using the @Orchestrator agent.
