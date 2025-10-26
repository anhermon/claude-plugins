# Claude Code Skills - Detailed Documentation

## Overview

Skills are modular capabilities that extend Claude's functionality through organized folders containing instructions, scripts, and resources. Each Skill consists of a SKILL.md file with instructions that Claude reads when relevant, plus optional supporting files like scripts and templates.

## SKILL.md Format Structure

A SKILL.md file requires YAML frontmatter and Markdown content with the following structure:

```markdown
---
name: your-skill-name
description: Brief description of what this Skill does and when to use it
---

# Instructions

[Detailed instructions for Claude on how to use this skill]

## When to Use

[Describe when Claude should invoke this skill]

## Examples

[Provide usage examples]

## Best Practices

[Include best practices specific to this skill]
```

## Required Fields

### YAML Frontmatter

- **name**: `your-skill-name` (kebab-case identifier)
- **description**: Brief description that helps Claude decide when to use the skill. Should include both what the skill does AND when to use it.

### Markdown Content

- **Instructions**: Detailed step-by-step instructions for Claude
- **Examples**: Usage examples to guide Claude
- **Best Practices**: Domain-specific best practices (optional but recommended)

## Storage Locations

### Personal Skills (Available across all projects)
**Location**: `~/.claude/skills/`

Each skill is a directory containing at minimum a `SKILL.md` file.

### Project Skills (Shared with team)
**Location**: `.claude/skills/` within your project

Project skills take precedence over personal skills when names conflict.

## Key Characteristics

### Model-Invoked (Not User-Invoked)

- Skills are **autonomously invoked** by Claude based on context
- Unlike slash commands which require explicit user invocation (`/command`)
- Claude decides when to use them based on your request and the Skill's description

### Composable

- Multiple skills can be active simultaneously
- Claude automatically identifies which skills are relevant
- Skills stack together seamlessly

### Minimal Loading

- When a skill matches, Claude loads only the minimal information needed
- Keeps Claude fast while accessing specialized expertise
- For large skills, split content into separate files and reference them

## Advanced Features

### Executable Code

Skills can include executable code for tasks where traditional programming is more reliable than token generation.

### File References

Skills can reference additional files within their directory structure:
- Scripts (Python, Bash, etc.)
- Templates
- Data files
- Configuration files

### Context Optimization

When the SKILL.md file becomes large:
- Split content into separate files and reference them
- Keep mutually exclusive contexts in separate paths
- This reduces token usage by loading only relevant content

## Best Practices

1. **Clear Description**: Include both what the skill does and when to use it in the description
2. **Single Responsibility**: Each skill should have a focused purpose
3. **Minimal Files**: Only include files that are necessary
4. **Context Separation**: Keep mutually exclusive contexts separate to reduce token usage
5. **Examples**: Include concrete examples to guide Claude
6. **Version Control**: Keep skills in git for team sharing

## Integration with Code Execution Tool

Skills require the **Code Execution Tool beta** which provides:
- Secure environment for running skill code
- Sandboxed execution
- Resource limits

## Cross-Platform Support

Skills work across:
- Claude Code CLI
- Claude Code Web
- Claude apps
- Anthropic API

Same skill format everywhere - build once, use everywhere.

## Creating Skills

### Interactive Creation

Use the built-in "skill-creator" skill:
- Provides interactive guidance
- Asks about your workflow
- Generates the folder structure automatically

### Manual Creation

1. Create a directory: `~/.claude/skills/your-skill-name/`
2. Create `SKILL.md` with frontmatter and instructions
3. Add any supporting files (optional)
4. Claude will automatically discover and use the skill

## Official Resources

- Documentation: https://docs.claude.com/en/docs/claude-code/skills
- Example Skills: https://github.com/anthropics/skills
- Skills for MS Office: Excel, PowerPoint, Word, PDFs
- Agent Skills: https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills
