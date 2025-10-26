# Claude Plugins Marketplace - Architecture

## Overview

This repository serves as a decentralized plugin marketplace for Claude Code, providing a collection of meta-tools for creating and managing Claude Code extensions (sub-agents, slash commands, skills, and complete plugins).

## Architecture Components

### 1. Plugin Marketplace Structure

```
claude-plugins/
├── README.md                      # Marketplace documentation
├── ARCHITECTURE.md                # This file
├── plugins/                       # Available plugins
│   ├── meta-tools/               # Meta tool plugin
│   │   ├── PLUGIN.md            # Plugin manifest
│   │   ├── agents/              # Sub-agents for creation
│   │   │   ├── meta-agent.md
│   │   │   ├── meta-command.md
│   │   │   ├── meta-skill.md
│   │   │   └── meta-plugin.md
│   │   ├── commands/            # Slash commands
│   │   │   ├── spawn.md
│   │   │   └── create-entity.md
│   │   └── skills/              # Skills
│   │       └── meta-creator/    # Unified meta skill
│   │           └── SKILL.md
│   └── [other-plugins]/
├── ai_docs/                      # Documentation for AI
│   ├── claude_plugins.md
│   ├── claude_skills.md
│   └── claude_skills_detailed.md
└── examples/                     # Example configurations
```

### 2. Meta-Tools Plugin

The flagship plugin providing tools to create Claude Code extensions.

#### Components

**A. Sub-Agents**

1. **meta-agent**: Creates new sub-agents
   - Tools: Write, Read, WebFetch, Grep, Glob
   - Fetches latest sub-agent documentation
   - Generates complete agent configurations

2. **meta-command**: Creates new slash commands
   - Tools: Write, Read, Grep, Glob
   - Fetches latest slash command documentation
   - Generates properly formatted command files

3. **meta-skill**: Creates new skills
   - Tools: Write, Read, WebFetch, Grep, Glob
   - Fetches latest skills documentation
   - Generates SKILL.md with proper frontmatter

4. **meta-plugin**: Creates complete plugins
   - Tools: Write, Read, WebFetch, Grep, Glob, Bash
   - Orchestrates creation of plugin packages
   - Generates PLUGIN.md manifests

**B. Skills**

1. **meta-creator**: Unified skill for all meta operations
   - Proactively invoked when user wants to create:
     - Sub-agents
     - Slash commands
     - Skills
     - Plugins
   - Delegates to appropriate meta-agent
   - Ensures latest documentation is used

**C. Slash Commands**

1. **/spawn**: Launches new Claude Code sessions
   - Syntax: `/spawn [TASK] [--agent AGENT_TYPE] [--model MODEL]`
   - Opens new terminal with Claude Code
   - Optionally starts with specific agent/model

2. **/create-entity**: Quick entity creation
   - Syntax: `/create-entity [agent|command|skill|plugin] [name]`
   - Interactive prompts for details
   - Delegates to appropriate meta-agent

### 3. Plugin Installation Flow

```
User → /plugin marketplace add angelhermon/claude-plugins
     → /plugin install meta-tools
     → Meta-tools plugin installed to ~/.claude/
     → Agents, commands, and skills become available
```

### 4. Key Design Decisions

#### Proactive Agent Usage

All meta-agents are configured to be proactively used:
- `description` field includes "Use proactively when..."
- Claude automatically delegates without explicit invocation
- Users can still invoke manually if needed

#### Documentation Fetching

All meta-agents fetch the latest documentation:
- Sub-agent docs: https://docs.claude.com/en/docs/claude-code/sub-agents
- Slash command docs: https://docs.claude.com/en/docs/claude-code/slash-commands
- Skills docs: https://docs.claude.com/en/docs/claude-code/skills
- Plugins docs: https://www.anthropic.com/news/claude-code-plugins

This ensures created entities follow current best practices.

#### Skill-First Approach

The meta-creator skill serves as the primary entry point:
- Model-invoked (Claude decides when to use it)
- Composable with other skills
- Delegates to specialized agents when needed

#### Decentralized Distribution

Following Anthropic's philosophy:
- No centralized app store
- Git-based distribution
- Anyone can fork and customize
- Easy team sharing

### 5. Data Flow

```
User Request
    ↓
Meta-Creator Skill (if relevant)
    ↓
Determine Entity Type
    ↓
┌─────────┬──────────┬──────────┬──────────┐
│ Agent   │ Command  │ Skill    │ Plugin   │
│ Needed  │ Needed   │ Needed   │ Needed   │
└────┬────┴────┬─────┴────┬─────┴────┬─────┘
     │         │          │          │
     ↓         ↓          ↓          ↓
meta-agent meta-command meta-skill meta-plugin
     │         │          │          │
     └─────────┴──────────┴──────────┘
                    ↓
          Fetch Latest Docs
                    ↓
          Generate Configuration
                    ↓
          Write to ~/.claude/
                    ↓
              Verify & Report
```

### 6. Tool Access Strategy

Each meta-agent has minimal, focused tool access:

- **Read**: Examine existing configurations
- **Write**: Create new configurations
- **Grep/Glob**: Find examples and patterns
- **WebFetch**: Fetch latest documentation
- **Bash**: Execute verification commands (meta-plugin only)

### 7. Verification Strategy

After creation, each meta-agent verifies:
1. File was written successfully
2. Frontmatter is valid YAML
3. Required fields are present
4. File is in correct location
5. (For plugins) Test installation works

### 8. Extension Points

The marketplace is designed for easy extension:

1. **Add New Plugins**: Create new plugin directories
2. **Customize Meta-Tools**: Fork and modify meta-agents
3. **Share Workflows**: Package common patterns as plugins
4. **Team Standards**: Create org-specific meta-agents

## Integration with Claude Code

### Global Installation
```bash
# Add marketplace
claude /plugin marketplace add angelhermon/claude-plugins

# Install meta-tools plugin
claude /plugin install meta-tools

# Verify installation
claude /plugin list
```

### Project-Specific Installation
```bash
cd your-project
claude /plugin install meta-tools --project
```

## Security Considerations

1. **Read-Only Fetching**: Documentation fetching uses WebFetch (read-only)
2. **Validated Writes**: All writes go to ~/.claude/ or .claude/ only
3. **YAML Validation**: Frontmatter is validated before writing
4. **Tool Restrictions**: Each agent has minimal tool access
5. **No External Execution**: No arbitrary code execution

## Future Enhancements

1. **Plugin Templates**: Pre-built plugin templates
2. **Testing Framework**: Automated testing for created entities
3. **Version Management**: Track plugin versions
4. **Dependency Resolution**: Handle plugin dependencies
5. **Update Notifications**: Alert when documentation changes
6. **Community Contributions**: Accept pull requests for new plugins

## Maintenance

### Keeping Documentation Current

Meta-agents automatically fetch latest docs, but we should:
1. Periodically verify doc URLs are current
2. Update ai_docs/ with latest information
3. Test generated entities against current Claude Code
4. Update examples when APIs change

### Testing Strategy

1. **Manual Testing**: Create test entities regularly
2. **Integration Testing**: Install plugin in fresh environment
3. **Documentation Review**: Compare against official docs monthly
4. **Community Feedback**: Monitor issues and PRs

## References

- [Claude Code Sub-Agents](https://docs.claude.com/en/docs/claude-code/sub-agents)
- [Claude Code Slash Commands](https://docs.claude.com/en/docs/claude-code/slash-commands)
- [Claude Code Skills](https://docs.claude.com/en/docs/claude-code/skills)
- [Claude Code Plugins](https://www.anthropic.com/news/claude-code-plugins)
- [Anthropic Skills Repository](https://github.com/anthropics/skills)
