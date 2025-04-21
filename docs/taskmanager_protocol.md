# 🧠 Task Manager Protocol

## Purpose
Tracks the full lifecycle and memory of all tasks across the system, using structured JSON + Markdown format.

## Structure
```
/Task Memory System/
├── task_log.json                      # global task list + metadata
└── task_scratchpads/
    ├── <task_id>.md                  # each task has its own working memory
```

## task_log.json fields
```json
{
  "task_id": "unique-id",
  "status": "planned | in_progress | complete | failed",
  "created_by": "Sora | Claude | Fabio",
  "agent": "Cursor | Cline | Manual",
  "context": "Frontend | Backend | Planning",
  "plan_file": "path to .md",
  "description": "What this task does",
  "notes": "Relevant side info",
  "created_at": "ISO8601 timestamp"
}
```

## task_scratchpad.md structure
```markdown
# Task: <task_id>

## ✅ Goal
<Human-readable goal>

## 📐 Structure Plan
- [ ] List subtasks

## 🧠 Notes / Lessons
- Error history, bugs, decisions

## 🛠 Status
PLANNED | IN PROGRESS | COMPLETE
```

## Recovery Pattern
- Restart any session by reloading the `.json` + `.md` into context
- No memory is assumed — **all recall is explicit**

## Best Practices
1. **Unique Task IDs**: Use kebab-case for task IDs (e.g., `bootstrap-agent-protocols`)
2. **Status Updates**: Keep the status field updated as the task progresses
3. **Detailed Notes**: Document errors, bugs, and decisions in the scratchpad
4. **Explicit References**: Always reference the task ID and scratchpad path in CodeBridge messages

## Examples
See the `/templates/task_log.example.json` and `/templates/task_scratchpad_template.md` files for template examples.
