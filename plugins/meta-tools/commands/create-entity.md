---
description: Quick entity creation wizard for agents, commands, skills, or plugins
argument-hint: [agent|command|skill|plugin] [NAME]
---

# Create Entity

Interactive wizard for creating Claude Code entities (sub-agents, slash commands, skills, or plugins).

## Parse Arguments

Parse arguments from `$ARGUMENTS`:
- First argument: Entity type (`agent`, `command`, `skill`, or `plugin`)
- Second argument: Optional entity name
- If no arguments: Show interactive menu

## Instructions

### 1. Determine Entity Type

If entity type is not provided or is invalid:
1. Show a menu of options:
   - `agent` - Create a new sub-agent
   - `command` - Create a new slash command
   - `skill` - Create a new skill
   - `plugin` - Create a complete plugin package

2. Ask the user to choose one

3. Validate the choice

### 2. Get Entity Name (If Not Provided)

If name is not provided:
1. Ask the user for a name
2. Validate it's kebab-case
3. If not kebab-case, offer to convert it

### 3. Gather Requirements

Based on entity type, ask targeted questions:

**For Sub-Agent:**
- What is the agent's primary purpose?
- What tasks will it perform?
- Should it be invoked proactively or manually?
- What tools does it need? (or inherit all tools?)

**For Slash Command:**
- What should the command do?
- Does it need arguments? If yes, what kind?
- What tools should it have access to? (or allow all?)

**For Skill:**
- What specialized capability does it provide?
- When should Claude invoke it automatically?
- Does it need supporting files (scripts, templates)?

**For Plugin:**
- What is the plugin's purpose?
- What components should it include? (agents, commands, skills, MCP, hooks)
- Who is it for? (personal, team, public)
- Where should it be created? (current directory, ~/.claude/, etc.)

### 4. Delegate to Appropriate Meta-Agent

Based on entity type, delegate using the Task tool:

**For Agent:**
```
Use Task tool with subagent_type="meta-agent"
Pass all gathered requirements
```

**For Command:**
```
Use Task tool with subagent_type="meta-command"
Pass all gathered requirements
```

**For Skill:**
```
Use Task tool with subagent_type="meta-skill"
Pass all gathered requirements
```

**For Plugin:**
```
Use Task tool with subagent_type="meta-plugin"
Pass all gathered requirements
```

### 5. Report Results

After the meta-agent completes:
1. Summarize what was created
2. Show the file location(s)
3. Provide usage instructions
4. Offer next steps

## Examples

### Example 1: Create Agent (Interactive)
```
/create-entity agent
```
Wizard asks for name, purpose, tasks, tools, etc.

### Example 2: Create Agent (With Name)
```
/create-entity agent code-reviewer
```
Wizard asks for purpose, tasks, tools, etc. (name already provided).

### Example 3: Create Command
```
/create-entity command deploy
```
Wizard asks what the deploy command should do, whether it needs arguments, etc.

### Example 4: Create Skill
```
/create-entity skill excel-expert
```
Wizard asks about Excel capabilities, when to invoke, supporting files needed, etc.

### Example 5: Create Plugin
```
/create-entity plugin team-tools
```
Wizard asks about plugin purpose, components to include, target audience, etc.

### Example 6: Interactive (No Args)
```
/create-entity
```
Shows menu to choose entity type, then proceeds with wizard.

## Wizard Flow

```
/create-entity [type] [name]
    ↓
[If no type] → Show menu → Choose type
    ↓
[If no name] → Ask for name → Validate kebab-case
    ↓
Ask requirements questions based on type
    ↓
Delegate to meta-agent (meta-agent, meta-command, meta-skill, or meta-plugin)
    ↓
Meta-agent creates entity
    ↓
Report success and usage instructions
```

## Validation

Validate inputs:
- **Entity type**: Must be one of: agent, command, skill, plugin
- **Name**: Must be kebab-case (lowercase, hyphens, no spaces)
- **Requirements**: Ensure all necessary information is gathered

Offer to fix invalid inputs:
- Convert "My Agent" to "my-agent"
- Suggest alternatives for unclear requirements

## Interactive Experience

Make the wizard friendly and helpful:
1. **Clear questions**: Ask one thing at a time
2. **Examples**: Provide examples of good answers
3. **Defaults**: Offer sensible defaults when appropriate
4. **Validation**: Validate inputs and offer corrections
5. **Progress**: Show what step user is on
6. **Summary**: Summarize before creating

## Error Handling

Handle these cases:
- Invalid entity type: Show valid options
- Invalid name format: Offer to convert or ask again
- Missing requirements: Ask clarifying questions
- Meta-agent fails: Show error and suggest fixes
- File already exists: Ask whether to overwrite or choose new name

## Advanced Options

Consider asking about:
- **Scope**: Personal (~/.claude/) or project (.claude/)?
- **Documentation**: Generate example usage?
- **Testing**: Create test cases?
- **Git**: Commit the new files?

## Notes

- This command provides a user-friendly interface to the meta-agents
- It guides users through the creation process step-by-step
- It delegates actual creation to specialized meta-agents
- It ensures all necessary information is gathered before creating
- It validates inputs to prevent common mistakes
