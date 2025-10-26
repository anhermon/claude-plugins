# Claude Skills Documentation

## Overview

Anthropic introduced Claude Skills in October 2025. Skills are folders that include instructions, scripts, and resources that Claude can load when needed. These skills can be used across Claude apps, Claude Code, and Anthropic's API.

## Key Features

### What Skills Do

- Skills make Claude better at specialized tasks like working with Excel or following organization brand guidelines
- Claude only accesses a skill when it's relevant to the task at hand
- When a skill matches, it loads only the minimal information and files needed—keeping Claude fast while accessing specialized expertise

### Key Characteristics

- **Composable**: Skills stack together with Claude automatically identifying which are needed
- **Portable**: Use the same format everywhere - across Claude apps, Claude Code, and API
- **Build once, use everywhere**: Skills can be built once and used across all Claude platforms
- **Can include executable code**: For tasks where traditional programming is more reliable than token generation

## How to Create Skills

Skills are simple to create:
1. Create a folder with a `SKILL.md` file
2. Include YAML frontmatter and instructions in the `SKILL.md` file
3. The "skill-creator" skill provides interactive guidance, asking about your workflow and generating the folder structure automatically

## Skill Structure

A skill is a folder containing:
- `SKILL.md`: Main configuration file with YAML frontmatter and instructions
- Additional resources: Scripts, data files, templates, etc.
- Executable code (optional): For tasks requiring programmatic approaches

## Integration with Claude Code

Skills work seamlessly within Claude Code environments:
- Desktop/CLI versions
- Web version (introduced October 2025 with Anthropic-managed cloud infrastructure)
- Skills require the Code Execution Tool beta for secure execution

## Proactive Usage

Claude automatically:
- Identifies when a skill is relevant to the current task
- Loads only the minimal information needed
- Uses multiple skills together when appropriate

## Examples and Resources

Anthropic created skills for:
- Reading and generating professional Excel spreadsheets with formulas
- PowerPoint presentations
- Word documents
- Fillable PDFs

Additional resources:
- Agent Skills documentation
- Claude Skills Cookbook

## Technical Requirements

- Skills require the Code Execution Tool beta
- This provides the secure environment needed to run skill code
- Skills can be distributed through Claude Code plugins or used independently
