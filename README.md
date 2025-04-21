# NovelVision Agent Protocols

This repository defines the core protocols and operational standards for collaborative agent systems in the NovelVision AI infrastructure.

## Purpose

The NovelVision AI Agent Protocol System provides a structured framework for collaboration between different AI agents (Sora, Cursor, Cline, Gemini, Claude) and humans. It enables:

- Clear communication through standardized message formats
- Persistent memory across sessions and agents
- Structured task management and tracking
- Continuous improvement through feedback and learning

## Protocols

### 📡 CodeBridge

CodeBridge is the structured relay system used to pass clear, scoped, and modular instructions between humans and agents. It ensures that all participants have a shared understanding of the task, context, scope, and expected outcomes.

[Learn more about CodeBridge](docs/codebridge_protocol.md)

### 🧠 Task Manager

The Task Manager protocol tracks the full lifecycle and memory of all tasks across the system, using structured JSON + Markdown format. It provides a persistent memory system that can be accessed by any agent or human.

[Learn more about Task Manager](docs/taskmanager_protocol.md)

### 🔁 Feedback + Learning

The Feedback + Learning protocol tracks and evaluates the outcomes of completed tasks to extract protocol-level lessons, detect repeated failures, and evolve the system automatically over time.

[Learn more about Feedback + Learning](docs/feedback_learning.md)

## Getting Started

1. Review the protocol documentation in the `/docs` directory
2. Use the templates in the `/templates` directory for creating new tasks and CodeBridge messages
3. Check the current tasks in `task_log.json`
4. Follow the recovery playbook if you need to resume a task after a disruption

## Usage with MCP/Cursor

1. Reference the task ID and scratchpad path in your CodeBridge messages
2. Load the task scratchpad into the agent's context
3. Update the scratchpad with progress and notes
4. Document any errors or issues encountered
5. Evaluate the task outcome and suggest improvements

## Directory Structure

```
/Task Memory System/
├── README.md
├── agents-protocol-guide.md
├── task_log.json
├── task-memory-system-v1.md
├── full-architecture-recovery.md
├── /task_scratchpads/
│   └── (task-specific scratchpads)
├── /templates/
│   ├── .sorarules.example
│   ├── codebridge_template.md
│   ├── task_log.example.json
│   └── task_scratchpad_template.md
├── /docs/
│   ├── codebridge_protocol.md
│   ├── taskmanager_protocol.md
│   ├── feedback_learning.md
│   ├── recovery_playbook.md
│   └── agent_roles.md
```
