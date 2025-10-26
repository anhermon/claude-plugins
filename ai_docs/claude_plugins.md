# Claude Code Plugins Documentation

## Overview

Claude Code now supports plugins: custom collections of slash commands, agents, MCP servers, and hooks that install with a single command. This was announced on October 9, 2025, and is available in public beta for all Claude Code users.

## What Plugins Include

Plugins are a lightweight way to package and share any combination of:

- **Slash commands**: Create custom shortcuts for frequently-used operations
- **Subagents**: Install purpose-built agents for specialized development tasks
- **MCP servers**: Connect to tools and data sources through the Model Context Protocol
- **Hooks**: Customize Claude Code's behavior at key points in its workflow

## Installation & Access

Plugins can be installed directly using the `/plugin` command, both in terminal and VS Code environments.

## Marketplace System

Instead of a centralized app store controlled by Anthropic, anyone can create and host a marketplace from a simple Git repository. This decentralized, developer-first approach lowers the barrier to entry for distributing powerful tools.

### Using Marketplaces

1. Add a repository source: `/plugin marketplace add user-or-org/repo-name`
2. Explore and install desired plugins via the `/plugin` menu

## Use Cases

Common plugin use cases include:

- **Enforcing standards**: Engineering leaders can maintain consistency across their team by using plugins to ensure specific hooks run for code reviews or testing workflows
- **Supporting users**: Open source maintainers can provide slash commands that help developers use their packages correctly
- **Sharing workflows**: Developers can share productivity-boosting workflows like debugging setups, deployment pipelines, or testing harnesses
- **Connecting tools**: Teams can connect internal tools and data sources through MCP servers

## Plugin Structure

A plugin is a Git repository with a specific structure that contains:
- Slash commands (in `.claude/commands/`)
- Subagents (in `.claude/subagents/`)
- MCP server configurations
- Hooks

## Technical Implementation

Plugins install with a single command and can include any combination of the four components listed above. The decentralized marketplace approach allows anyone to host and distribute plugins through Git repositories.

## Significance

This represents a significant evolution of Claude Code from a standalone tool into an extensible platform with community-driven development.
