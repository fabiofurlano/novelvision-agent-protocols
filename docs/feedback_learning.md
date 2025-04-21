# 🔁 Feedback + Learning Protocol

## Purpose
Track and evaluate the outcomes of completed tasks to extract protocol-level lessons, detect repeated failures, and evolve CodeBridge + TaskManager automatically over time.

## Evaluation Block
Add this block to every task_scratchpad.md:

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

## Protocol Memory File
Store learnings globally in:
- `/protocol_lessons.md`
- OR `/memory/auto-lessons.json`

Example:
```json
{
  "lesson_id": "L003",
  "pattern": "agent skipped Firebase auth detection",
  "suggested_change": "Require auth check verification in all frontend CodeBridge relays",
  "applied_to": ["implement-frontend-refactor"]
}
```

## Usage
- Auto-check `protocol_lessons` before generating CodeBridge
- Warn agent/human about prior issues with similar scope
- Gemini/Sora may rewrite protocol automatically to reflect lessons

## Benefits
- Durable learning across crashes and restarts
- Prevents repeated mistakes
- Enables self-healing protocol improvements

## Best Practices
1. **Honest Evaluation**: Be honest about the outcome of the task
2. **Concrete Issues**: List specific failures and issues
3. **Actionable Improvements**: Suggest concrete changes to prevent reoccurrence
4. **Apply Lessons**: Check for relevant lessons before starting a new task
