# 🔄 Recovery Playbook

## Purpose
This playbook provides guidance for recovering from session crashes, context loss, or other disruptions in the agent workflow.

## Recovery Steps

### 1. Identify the Task
- Check `task_log.json` to find the task ID and status
- Locate the corresponding scratchpad file in `task_scratchpads/<task_id>.md`

### 2. Load Context
- Load the task scratchpad into the agent's context
- Review the task goal, structure plan, and notes
- Check for any linked resources or references

### 3. Assess Status
- Determine the current status of the task (PLANNED, IN PROGRESS, COMPLETE, FAILED)
- Review any error history or bugs documented in the scratchpad
- Check for any pending subtasks or action items

### 4. Resume Work
- Continue from the last documented step
- Update the scratchpad with new progress
- If necessary, create a new CodeBridge message to relay instructions

### 5. Document Recovery
- Add a note in the scratchpad about the recovery
- Document any lessons learned from the disruption
- Update the task status if needed

## Best Practices
1. **Regular Updates**: Frequently update the scratchpad with progress
2. **Explicit State**: Document the current state and next steps clearly
3. **Checkpoints**: Create clear checkpoints in the workflow
4. **Error Documentation**: Document errors and recovery attempts in detail

## Example Recovery Note
```markdown
## 🔄 Recovery Note (2025-04-22)
Session crashed during implementation of feature X.
- Last completed step: Created component structure
- Next step: Implement event handlers
- Known issues: None documented
```
