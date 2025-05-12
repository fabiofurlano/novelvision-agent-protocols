## Task Memory System (v1)

### Purpose
Tracks the lifecycle, scratch memory, and test notes for all tasks across the NovelVision AI codebase.

### File Structure
- `/task_memory/task_log.json`: Global task list and agent routing metadata
- `/task_memory/task_scratchpads/{task_id}.md`: Detailed plan and memory log per task

### Usage Pattern

**For Humans:**
1. Create or review a task idea
2.Ask Sora to generate a task ID and register it in task_log.json.
Then Sora will generate a CodeBridge message to instruct the AI coding tool (Cline/Cursor) to:

Create the corresponding .md scratchpad

Populate it with investigation logs, plans, and result tracking during the task lifecycle.
Humans should not write in the scratchpad — it is for AI agent use only.”

3. Use task ID with Cursor or other agents
4. Update `.md` file with outcomes, lessons, errors

**For Agents (Cursor, Cline, Cascade):**
1. Load `task_log.json` to discover planned tasks
2. Read `task_scratchpads/<task_id>.md` for detailed execution steps
3. Write back test outcomes, bugs, retries
4. Respect status in `task_log.json` (`planned`, `in_progress`, `failed`, `complete`)

### Example
### Example
task_id: "task-memory-system-v1" scratchpad: task_memory/task_scratchpads/task-memory-system-v1.md

pgsql
Copy
Edit

### Rule
These files must be **included in the current session context** or uploaded to an external memory layer (e.g., MCP) for GPTs to recall them.
