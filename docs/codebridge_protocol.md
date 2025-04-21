# 📡 CodeBridge Protocol

## Purpose
CodeBridge is the structured relay system used to pass clear, scoped, and modular instructions between humans and agents (e.g., Sora → Cursor, Claude → Gemini).

## Format
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

## Usage
- Relay to coding agents via live message or `.md`
- May be bundled with `.sorarules` files or task references
- Used to keep planning and execution synchronized

## Best Practices
1. **Be Specific**: Clearly define the objective without ambiguity
2. **Provide Context**: Include essential background information
3. **Define Scope**: Specify what files, folders, or modules the agent may touch
4. **Set Validation Criteria**: Define what questions to answer or behavior to verify
5. **Specify Output Format**: Define the expected return format

## Examples
See the `/templates/codebridge_template.md` file for a template example.
