# NovelVision Agent Protocols

This repository defines the core protocols and operational standards for collaborative agent systems in the NovelVision AI infrastructure.

---

## 📡 Protocol 1: CodeBridge

**Purpose:**
CodeBridge is the structured relay system used to pass clear, scoped, and modular instructions between humans and agents (e.g., Sora → Cursor, Claude → Gemini).

### ✅ Format:
Each CodeBridge message must contain the following fields:

```markdown
# 📡 CodeBridge Message: <short title>

## 🔗 Linked Task
- task_id: <task_id>
- scratchpad: <file path to .md scratchpad>

## 🎯 Objective
<What the agent must do — clearly defined, without ambiguity>

## 🧠 Context
<Essential background: architecture, constraints, memory notes>

## 🔍 Scope
<What files, folders, or modules the agent may touch>

## 🧪 Tests / Validation
<What questions to answer, what behavior to verify>

## 🧾 Output Format
<Expected return format: plan, .sorarules, diagnostic list, etc.>
```

### 🛠 Usage
- Relay to coding agents via live message or `.md`
- May be bundled with `.sorarules` files or task references
- Used to keep planning and execution synchronized

---

## 🧠 Protocol 2: Task Manager System

**Purpose:**
Tracks the full lifecycle and memory of all tasks across the system, using structured JSON + Markdown format.

### 📁 Structure
```
/task_memory/
├── task_log.json                      # global task list + metadata
└── task_scratchpads/
    ├── <task_id>.md                  # each task has its own working memory
```

### 🧱 task_log.json fields:
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

### 📝 task_scratchpad.md structure
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

### 🔁 Recovery Pattern
- Restart any session by reloading the `.json` + `.md` into context
- No memory is assumed — **all recall is explicit**

---

## 🔁 Protocol 3: Feedback + Learning

**Purpose:**
Track and evaluate the outcomes of completed tasks to extract protocol-level lessons, detect repeated failures, and evolve CodeBridge + TaskManager automatically over time.

### 📊 Evaluation Block (to add in every task_scratchpad.md):
```markdown
## ✅ Evaluation

### Outcome:
success | partial | failed

### Score:
X/10 (manual or AI-detected)

### Issues:
- List concrete failures

### Improvements Suggested:
- List protocol changes or reminders to prevent reoccurrence
```

### 📚 Protocol Memory File
Store learnings globally in:
- `/protocol_lessons.md`
- OR `/memory/auto-lessons.json`

### Example:
```json
{
  "lesson_id": "L003",
  "pattern": "agent skipped Firebase auth detection",
  "suggested_change": "Require auth check verification in all frontend CodeBridge relays",
  "applied_to": ["implement-frontend-refactor"]
}
```

### 🔁 Usage
- Auto-check `protocol_lessons` before generating CodeBridge
- Warn agent/human about prior issues with similar scope
- Gemini/Sora may rewrite protocol automatically to reflect lessons

### 🧠 Benefits
- Durable learning across crashes and restarts
- Prevents repeated mistakes
- Enables self-healing protocol improvements

---

## 🔧 Agent Integration

### Cursor, Gemini, Cline, Claude:
- Agents must check task_log.json for available work
- Each task includes a plan_file `.md` with memory and structure
- When finished, agents write back test notes or plan outputs into the scratchpad
- CodeBridge messages may be referenced in the scratchpad or sent live

---

## 🧭 Recommended Repo Structure

```plaintext
/docs/
  codebridge_protocol.md
  taskmanager_protocol.md
  feedback_learning.md
  recovery_playbook.md
  agent_roles.md

/templates/
  .sorarules.example
  codebridge_template.md
  task_log.example.json
  task_scratchpad_template.md

/memory/
  task_log.json
  task_scratchpads/
    <task_id>.md
  auto-lessons.json

README.md
```

---

Next step: Assign repo creation to Cline via CodeBridge.

