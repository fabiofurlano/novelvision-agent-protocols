# 🤖 Agent Roles

## Purpose
This document defines the roles and responsibilities of different agents in the NovelVision AI ecosystem.

## Agent Types

### Sora
- **Role**: Planning and coordination
- **Responsibilities**:
  - Create and manage tasks
  - Generate CodeBridge messages
  - Evaluate task outcomes
  - Extract protocol-level lessons
  - Evolve protocols over time

### Cursor
- **Role**: Code implementation and debugging
- **Responsibilities**:
  - Implement features based on CodeBridge instructions
  - Debug issues and document solutions
  - Update task scratchpads with progress
  - Provide feedback on implementation challenges

### Cline
- **Role**: Repository management and documentation
- **Responsibilities**:
  - Create and manage GitHub repositories
  - Implement file structures and templates
  - Document protocols and best practices
  - Maintain consistency across the codebase

### Gemini
- **Role**: Analysis and optimization
- **Responsibilities**:
  - Analyze code for performance issues
  - Suggest optimizations and improvements
  - Review and validate implementations
  - Provide feedback on architectural decisions

### Claude
- **Role**: Documentation and knowledge management
- **Responsibilities**:
  - Create and maintain documentation
  - Extract knowledge from conversations
  - Organize and structure information
  - Provide context and background for tasks

## Collaboration Workflow
1. **Task Creation**: Sora or human creates a task in `task_log.json`
2. **Task Planning**: Sora creates a scratchpad with the task structure
3. **Implementation**: Cursor or other agent implements the task based on CodeBridge instructions
4. **Evaluation**: Sora or human evaluates the outcome and extracts lessons
5. **Iteration**: Process repeats with improvements based on feedback

## Best Practices
1. **Clear Handoffs**: Use CodeBridge for clear handoffs between agents
2. **Documentation**: Document all decisions and progress in the task scratchpad
3. **Feedback Loop**: Provide feedback on the process to improve future iterations
4. **Role Respect**: Respect the roles and responsibilities of each agent
