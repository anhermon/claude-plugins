# Claude Code Plugins Marketplace

A decentralized marketplace for Claude Code plugins, featuring the **Meta-Tools** plugin for creating Claude Code extensions with the latest best practices.

## 🚀 Quick Start

### Add This Marketplace

```bash
/plugin marketplace add angelhermon/claude-plugins
```

### Install Meta-Tools Plugin

```bash
/plugin install meta-tools
```

That's it! You now have a complete toolkit for creating Claude Code extensions.

## 📦 Available Plugins

### Meta-Tools v1.0.0

**The complete meta-creation toolkit for building Claude Code extensions.**

#### What's Included

- **🤖 5 Meta-Agents**: Specialized agents for creating sub-agents, slash commands, skills, plugins, and executing prompts with different AI models
- **🎨 1 Unified Skill**: Intelligent routing to appropriate creation tools
- **⚡ 3 Slash Commands**: Spawn new sessions, interactive entity creation, and multi-model execution
- **📚 Auto Documentation**: Fetches latest official Claude Code docs

#### Features

✨ **Proactive**: Agents automatically activate when you need to create extensions
📚 **Current**: Always uses latest official documentation from Anthropic
🔧 **Best Practices**: Follows official guidelines and recommendations
🎯 **Easy**: Just describe what you want, agents handle the details
🚀 **Complete**: Create any type of Claude Code extension

#### Quick Examples

```bash
# Create a sub-agent (just ask!)
"Create a sub-agent for code reviews"

# Create a slash command (just ask!)
"Create a slash command to deploy to staging"

# Create a skill (just ask!)
"Create a skill for React best practices"

# Create a plugin (just ask!)
"Create a plugin for our team's Git workflow"

# Use slash commands
/spawn Review the auth code --agent security-reviewer
/create-entity agent my-agent

# Execute prompts with different AI models
/execute-with-model --model claude "Review this code"
/execute-with-model --model gemini "Find React best practices"
/execute-with-model --model codex "Generate a REST API"
```

[**→ Full Meta-Tools Documentation**](plugins/meta-tools/PLUGIN.md)

---

## 🎯 What Are Claude Code Plugins?

Plugins are lightweight packages that can include any combination of:

- **Slash Commands**: Custom shortcuts for frequently-used operations
- **Sub-Agents**: Purpose-built agents for specialized development tasks
- **MCP Servers**: Connections to tools and data sources
- **Hooks**: Customizations to Claude Code's behavior
- **Skills**: Model-invoked capabilities that Claude uses automatically

### Why Use Plugins?

✅ **One-Command Install**: `/plugin install plugin-name`
✅ **Decentralized**: Anyone can host a marketplace
✅ **Shareable**: Easy team and community distribution
✅ **Composable**: Mix and match plugins
✅ **Version Control**: Git-based distribution

## 🏗️ Architecture

This marketplace follows Anthropic's decentralized plugin architecture:

```
claude-plugins/ (this repository)
├── README.md                    # This file
├── ARCHITECTURE.md              # Technical architecture
├── plugins/                     # Available plugins
│   └── meta-tools/             # Meta-creation toolkit
│       ├── PLUGIN.md           # Plugin manifest
│       ├── agents/             # Meta-agents
│       │   ├── meta-agent.md
│       │   ├── meta-command.md
│       │   ├── meta-skill.md
│       │   └── meta-plugin.md
│       ├── commands/           # Slash commands
│       │   ├── spawn.md
│       │   └── create-entity.md
│       └── skills/             # Skills
│           └── meta-creator/
│               └── SKILL.md
├── ai_docs/                    # Documentation for AI
└── examples/                   # Example configurations
```

## 🛠️ Using Meta-Tools

### Creating Sub-Agents

Just ask Claude to create one:

```
Create a sub-agent for security code reviews
```

The **meta-agent** will:
1. Fetch latest sub-agent documentation
2. Ask clarifying questions
3. Generate the agent configuration
4. Write to `~/.claude/agents/`
5. Provide usage instructions

### Creating Slash Commands

Just ask Claude to create one:

```
Create a slash command for committing and pushing in one step
```

The **meta-command** agent will:
1. Fetch latest slash command documentation
2. Study existing command patterns
3. Generate the command file
4. Write to `~/.claude/commands/`
5. Show usage examples

### Creating Skills

Just ask Claude to create one:

```
Create a skill for Excel spreadsheet work
```

The **meta-skill** agent will:
1. Fetch latest skills documentation
2. Generate SKILL.md with proper frontmatter
3. Set up model-invoked triggering
4. Write to `~/.claude/skills/`
5. Explain how it will be triggered

### Creating Plugins

Just ask Claude to create one:

```
Create a plugin with our team's code review tools
```

The **meta-plugin** agent will:
1. Fetch latest plugin documentation
2. Ask what components to include
3. Generate PLUGIN.md and README
4. Create all components
5. Provide installation instructions

### Interactive Creation

Use the wizard-style command:

```bash
/create-entity
```

Guides you through creating any type of entity with questions and validation.

### Spawning New Sessions

Work on multiple tasks in parallel:

```bash
/spawn Optimize database queries --agent performance-reviewer
```

Opens a new terminal with Claude already focused on the task!

### Executing with Different AI Models

Delegate tasks to different AI models based on their strengths:

```bash
# Use Claude for deep code analysis
/execute-with-model --model claude "Review this Python code for security issues"

# Use Gemini for research and current information
/execute-with-model --model gemini "What are the latest TypeScript features in 2025?"

# Use Codex for code generation
/execute-with-model --model codex "Generate a FastAPI application with authentication"
```

Run tasks in parallel or compare outputs from different models!

## 📚 Documentation

- [**Architecture Overview**](ARCHITECTURE.md) - Technical design and data flow
- [**Meta-Tools Plugin**](plugins/meta-tools/PLUGIN.md) - Complete plugin documentation
- [**Claude Code Plugins**](ai_docs/claude_plugins.md) - Plugins overview
- [**Claude Code Skills**](ai_docs/claude_skills.md) - Skills overview
- [**Skills Detailed**](ai_docs/claude_skills_detailed.md) - Skills deep dive

## 🎓 Learning Resources

### Official Anthropic Documentation

- [Sub-Agents](https://docs.claude.com/en/docs/claude-code/sub-agents)
- [Slash Commands](https://docs.claude.com/en/docs/claude-code/slash-commands)
- [Skills](https://docs.claude.com/en/docs/claude-code/skills)
- [Plugins](https://www.anthropic.com/news/claude-code-plugins)
- [Example Skills](https://github.com/anthropics/skills)

### Understanding Extension Types

**When to use each:**

| Type | User-Invoked | Model-Invoked | Use Case |
|------|-------------|---------------|----------|
| **Sub-Agent** | Manual or Proactive | No | Specialized, reusable AI functionality |
| **Slash Command** | Manual (`/command`) | No | Frequently-used workflows |
| **Skill** | No | Automatic | Expertise Claude invokes when relevant |
| **Plugin** | N/A (container) | N/A | Package multiple components |

## 🔧 Advanced Usage

### Creating Your Own Marketplace

1. Create a Git repository
2. Add plugins to `plugins/` directory
3. Share the repository URL
4. Users add with: `/plugin marketplace add your-username/your-repo`

### Contributing to This Marketplace

1. Fork this repository
2. Create your plugin in `plugins/your-plugin-name/`
3. Follow the plugin structure (see meta-tools example)
4. Submit a pull request

### Customizing Meta-Tools

1. Install the plugin
2. Copy agents to your local `~/.claude/agents/`
3. Modify as needed
4. Your local versions take precedence

## 🚀 Roadmap

- [ ] Additional plugins for specific workflows
- [ ] Plugin templates and starter kits
- [ ] Testing framework for plugins
- [ ] Plugin dependency management
- [ ] Automatic update notifications
- [ ] Community plugin contributions

## 🤝 Contributing

Contributions welcome! This marketplace is community-driven.

### Ways to Contribute

1. **Create Plugins**: Add new plugins to the marketplace
2. **Improve Meta-Tools**: Enhance existing meta-agents
3. **Documentation**: Improve docs and examples
4. **Bug Reports**: Open issues for problems
5. **Feature Requests**: Suggest improvements

### Contribution Guidelines

1. Follow existing plugin structure
2. Include comprehensive documentation
3. Test thoroughly before submitting
4. Follow Anthropic's official guidelines
5. Use clear, descriptive names

## 📋 Requirements

- Claude Code CLI (latest version)
- Internet connection (for documentation fetching)
- Git (for marketplace operations)

## 🐛 Troubleshooting

### Plugin Installation Fails

**Issue**: `/plugin install meta-tools` doesn't work

**Solution**:
1. Ensure marketplace is added: `/plugin marketplace add angelhermon/claude-plugins`
2. Check spelling: `meta-tools` (with hyphen)
3. Try direct install: `/plugin install https://github.com/angelhermon/claude-plugins/plugins/meta-tools`

### Meta-Agents Not Working

**Issue**: Agents aren't being invoked when creating entities

**Solution**:
1. Be explicit: "Create a sub-agent for X"
2. Use `/create-entity` for interactive creation
3. Restart Claude Code to pick up new agents
4. Check agents installed: `ls ~/.claude/agents/`

### Documentation Fetch Fails

**Issue**: Meta-agents can't fetch latest docs

**Solution**:
1. Check internet connection
2. Agents fall back to built-in knowledge
3. Can still create entities, just may not have absolute latest docs

## 📄 License

MIT License - See LICENSE file for details

## 🙏 Credits

Created by Angel Hermon

Built following Anthropic's official Claude Code documentation and best practices.

## 📧 Support

- **Issues**: [GitHub Issues](https://github.com/angelhermon/claude-plugins/issues)
- **Discussions**: [GitHub Discussions](https://github.com/angelhermon/claude-plugins/discussions)
- **Documentation**: This repository

---

**✨ Start creating Claude Code extensions with ease using Meta-Tools!**

```bash
# Get started in 2 commands:
/plugin marketplace add angelhermon/claude-plugins
/plugin install meta-tools

# Then just ask Claude to create what you need!
"Create a sub-agent for testing"
"Create a slash command for deployment"
"Create a skill for React"
"Create a plugin for our team"
```

**Happy building! 🚀**
