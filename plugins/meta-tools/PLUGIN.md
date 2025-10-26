---
name: meta-tools
version: 1.0.0
description: Complete meta-creation toolkit for building Claude Code extensions (agents, commands, skills, plugins)
author: Angel Hermon
repository: https://github.com/angelhermon/claude-plugins
---

# Meta-Tools Plugin

A comprehensive toolkit for creating Claude Code extensions with the latest best practices and automatic documentation fetching.

## Features

- **🤖 Meta-Agents**: Specialized agents for creating sub-agents, slash commands, skills, and plugins
- **🎯 Unified Skill**: Single meta-creator skill that intelligently routes to appropriate creation tool
- **⚡ Slash Commands**: Convenient commands for spawning new sessions and interactive entity creation
- **📚 Latest Documentation**: All meta-agents fetch the latest official Claude Code documentation
- **✨ Proactive Usage**: Agents automatically activate when you need to create extensions
- **🔧 Best Practices**: Follows official Anthropic guidelines and recommendations

## Installation

### From Marketplace

```bash
/plugin marketplace add angelhermon/claude-plugins
/plugin install meta-tools
```

### Direct Installation

```bash
/plugin install https://github.com/angelhermon/claude-plugins/plugins/meta-tools
```

## Components

### 🤖 Meta-Agents

#### meta-agent
**Purpose**: Creates new Claude Code sub-agents

**Proactive Trigger**: Automatically invoked when you want to create a new sub-agent

**Features**:
- Fetches latest sub-agent documentation from Claude docs
- Studies existing agent examples
- Generates properly formatted agent configurations
- Selects minimal necessary tools
- Writes to `~/.claude/agents/` or `.claude/agents/`

**Usage**: Just ask Claude to create a sub-agent, and this agent will handle it!

---

#### meta-command
**Purpose**: Creates new Claude Code slash commands

**Proactive Trigger**: Automatically invoked when you want to create a new slash command

**Features**:
- Fetches latest slash command documentation
- Studies existing command patterns
- Generates natural language prompts (not bash scripts!)
- Handles argument parsing
- Writes to `~/.claude/commands/` or `.claude/commands/`

**Usage**: Ask Claude to create a slash command, and this agent takes over!

---

#### meta-skill
**Purpose**: Creates new Claude Code skills

**Proactive Trigger**: Automatically invoked when you want to create a new skill

**Features**:
- Fetches latest skills documentation
- Generates proper SKILL.md format
- Creates supporting files if needed
- Sets up model-invoked triggering
- Writes to `~/.claude/skills/` or `.claude/skills/`

**Usage**: Request a skill creation, and this agent handles it!

---

#### meta-plugin
**Purpose**: Creates complete Claude Code plugin packages

**Proactive Trigger**: Automatically invoked when you want to create a new plugin

**Features**:
- Fetches latest plugin documentation
- Plans multi-component plugin structure
- Generates PLUGIN.md manifest
- Creates README documentation
- Writes all components
- Provides installation instructions

**Usage**: Ask to create a plugin, and this agent orchestrates it!

---

#### sub-agent-executor
**Purpose**: Executes prompts in new AI model sessions (Claude Code, Gemini CLI, ChatGPT Codex)

**Proactive Trigger**: Use when delegating tasks to different AI models

**Features**:
- Supports multiple AI model CLIs (claude, gemini-cli, codex)
- Executes prompts in isolated sessions
- Handles timeouts and background execution
- Provides model-specific installation instructions
- Returns structured output with status and results

**Usage**: Ask Claude to execute a prompt with a specific model!

---

### 🎨 Skills

#### meta-creator
**Purpose**: Unified routing skill for all meta-creation needs

**Model-Invoked**: Claude automatically uses this when you need to create any extension

**Features**:
- Intelligent routing to appropriate meta-agent
- Helps users decide which type of extension to create
- Coordinates multi-component creation
- Provides guidance and best practices

**Triggers**:
- User wants to create something for Claude Code
- User asks "how do I create a..."
- User mentions "I need a command/agent/skill/plugin for..."
- User wants to extend Claude Code capabilities

---

### ⚡ Slash Commands

#### /spawn
**Purpose**: Launch new Claude Code CLI instance in separate terminal

**Usage**:
```bash
/spawn [TASK] [--agent AGENT_TYPE] [--model MODEL]
```

**Examples**:
```bash
/spawn                                    # Fresh session
/spawn Review the auth code               # With task
/spawn --agent code-reviewer              # With specific agent
/spawn Fix bug.py --agent debugger        # Task + agent
/spawn --model claude-sonnet-4-5          # Specific model
```

**Features**:
- Opens new terminal window
- Starts in same working directory
- Optional task, agent, or model specification
- Cross-platform support (macOS, Linux, Windows)

---

#### /create-entity
**Purpose**: Interactive wizard for creating Claude Code entities

**Usage**:
```bash
/create-entity [agent|command|skill|plugin] [NAME]
```

**Examples**:
```bash
/create-entity                            # Interactive menu
/create-entity agent                      # Create agent (asks for name)
/create-entity agent code-reviewer        # Create agent with name
/create-entity command deploy             # Create slash command
/create-entity skill excel-expert         # Create skill
/create-entity plugin team-tools          # Create plugin
```

**Features**:
- Interactive question-and-answer wizard
- Input validation (kebab-case, etc.)
- Delegates to appropriate meta-agent
- Friendly user experience
- Comprehensive requirement gathering

---

#### /execute-with-model
**Purpose**: Execute a prompt with a specific AI model (claude, gemini, or codex)

**Usage**:
```bash
/execute-with-model --model [claude|gemini|codex] [OPTIONS] PROMPT
```

**Examples**:
```bash
/execute-with-model --model claude "What is the capital of France?"
/execute-with-model --model gemini --timeout 300000 "Search for React best practices"
/execute-with-model --model codex --dir /path/to/project "Review this code"
/execute-with-model --model claude --background "Analyze entire codebase"
```

**Features**:
- Execute prompts in isolated AI model sessions
- Support for Claude Code, Gemini CLI, and ChatGPT Codex
- Configurable timeouts and working directories
- Background execution for long-running tasks
- Model-specific flags support
- Comprehensive error handling

---

## Use Cases

### 1. Creating Sub-Agents

**Scenario**: You want a specialized agent for security reviews

**How to Use**:
```
Just ask: "Create a sub-agent for security code reviews"

The meta-agent will:
- Fetch latest documentation
- Ask clarifying questions
- Generate the agent configuration
- Write to ~/.claude/agents/security-reviewer.md
- Provide usage instructions
```

---

### 2. Creating Slash Commands

**Scenario**: You frequently deploy to production and want a shortcut

**How to Use**:
```
Just ask: "Create a slash command for deploying to production"

The meta-command agent will:
- Fetch latest documentation
- Study existing command patterns
- Generate the command prompt
- Write to ~/.claude/commands/deploy.md
- Show usage examples
```

---

### 3. Creating Skills

**Scenario**: You work with Excel files and want Claude to be better at it

**How to Use**:
```
Just ask: "Create a skill for Excel spreadsheet work"

The meta-skill agent will:
- Fetch latest documentation
- Generate SKILL.md with proper frontmatter
- Set up model-invoked triggering
- Write to ~/.claude/skills/excel-expert/
- Explain how it will be triggered
```

---

### 4. Creating Plugins

**Scenario**: You want to package your team's code review tools

**How to Use**:
```
Just ask: "Create a plugin for our team code review workflow"

The meta-plugin agent will:
- Fetch latest documentation
- Ask what components to include
- Generate PLUGIN.md and README.md
- Create all components
- Provide installation instructions
```

---

### 5. Spawning New Sessions

**Scenario**: You want to work on a different task in parallel

**How to Use**:
```bash
/spawn Optimize the database queries --agent performance-reviewer
```

Opens a new terminal with Claude already focused on optimization!

---

### 6. Interactive Entity Creation

**Scenario**: You're not sure what type of extension you need

**How to Use**:
```bash
/create-entity
```

Wizard walks you through choosing the right type and creating it!

---

### 7. Executing Tasks with Different AI Models

**Scenario**: You want to compare how different models approach a problem or delegate to model-specific strengths

**How to Use**:
```bash
# Use Claude for deep code analysis
/execute-with-model --model claude "Review this code for security vulnerabilities"

# Use Gemini for research
/execute-with-model --model gemini "Find latest React best practices"

# Use Codex for code generation
/execute-with-model --model codex "Generate a REST API in Python"
```

Benefits:
- Leverage model-specific strengths
- Run multiple tasks in parallel with different models
- Compare outputs for consensus building
- Isolate long-running tasks in background sessions

---

## Configuration

No configuration needed! The plugin works out of the box.

All meta-agents automatically fetch the latest documentation from:
- Sub-agents: https://docs.claude.com/en/docs/claude-code/sub-agents
- Slash commands: https://docs.claude.com/en/docs/claude-code/slash-commands
- Skills: https://docs.claude.com/en/docs/claude-code/skills
- Plugins: https://www.anthropic.com/news/claude-code-plugins

## Troubleshooting

### Meta-agents not being invoked proactively

**Issue**: You asked to create something but the meta-agent didn't activate

**Solution**: Try being more explicit:
- "Create a sub-agent for X"
- "Generate a slash command for Y"
- "Make a skill for Z"

Or use the /create-entity command for interactive creation.

### Documentation fetch fails

**Issue**: Meta-agent can't fetch latest docs

**Solution**: Check internet connection. The agents will fall back to built-in knowledge if fetch fails.

### Created entity not working

**Issue**: Entity was created but doesn't work as expected

**Solution**: Check the created file for:
- Valid YAML frontmatter
- Correct file location
- Proper naming (kebab-case)
- Restart Claude Code to pick up new entities

## Examples

### Example 1: Create a Testing Agent

**Request**:
```
Create a sub-agent that helps me write unit tests for Python code
```

**What Happens**:
1. meta-agent is invoked
2. Fetches latest sub-agent docs
3. Studies existing examples
4. Creates `~/.claude/agents/python-test-writer.md`
5. Reports success with usage instructions

**Result**: New agent available for test writing!

---

### Example 2: Create a Git Command

**Request**:
```
Create a slash command that commits and pushes with one command
```

**What Happens**:
1. meta-command is invoked
2. Fetches latest slash command docs
3. Studies existing patterns
4. Creates `~/.claude/commands/git-ship.md`
5. Shows usage examples

**Result**: `/git-ship` command ready to use!

---

### Example 3: Create a React Skill

**Request**:
```
Create a skill for React component best practices
```

**What Happens**:
1. meta-skill is invoked
2. Fetches latest skills docs
3. Creates `~/.claude/skills/react-patterns/SKILL.md`
4. Sets up auto-invocation triggers

**Result**: Skill automatically loads when working with React!

---

### Example 4: Package Team Tools

**Request**:
```
Create a plugin with our code review agent and commands
```

**What Happens**:
1. meta-plugin is invoked
2. Fetches latest plugin docs
3. Asks what components to include
4. Creates complete plugin structure
5. Generates PLUGIN.md and README

**Result**: Shareable plugin package ready for team!

---

## Best Practices

### When to Use Each Meta-Agent

- **meta-agent**: For reusable, specialized AI functionality
- **meta-command**: For frequently-used manual workflows
- **meta-skill**: For automatic expertise Claude should invoke
- **meta-plugin**: For packaging multiple components together

### Tips for Success

1. **Be Specific**: Provide clear requirements when asking for creation
2. **Review Output**: Always review generated configurations
3. **Iterate**: Created entities can be manually edited and improved
4. **Follow Patterns**: Study generated examples to learn best practices
5. **Share**: Package useful creations as plugins for your team

### Leveraging Proactive Features

- Let meta-agents activate automatically - just describe what you want
- Use the unified meta-creator skill for guidance
- Try /create-entity for interactive, wizard-style creation
- Use /spawn for parallel work on different tasks

## Contributing

This plugin is part of the claude-plugins marketplace.

To contribute:
1. Fork the repository
2. Make improvements
3. Submit a pull request

## Version History

### 1.0.0 (2025-10-25)
- Initial release
- Four meta-agents (agent, command, skill, plugin)
- Unified meta-creator skill
- Two slash commands (spawn, create-entity)
- Automatic documentation fetching
- Proactive agent invocation
- Comprehensive examples and documentation

## License

MIT License - See repository for details

## Support

- **Issues**: https://github.com/angelhermon/claude-plugins/issues
- **Documentation**: https://github.com/angelhermon/claude-plugins
- **Examples**: See examples/ directory in repository

---

**✨ Happy creating! The meta-tools plugin makes extending Claude Code easy and follows the latest best practices!**
