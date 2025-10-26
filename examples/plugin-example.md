# Example: Creating a Plugin

This example shows how to use the meta-tools plugin to create a complete plugin package.

## Simple Creation (Just Ask)

The easiest way to create a plugin is to simply ask Claude:

```
Create a plugin for our team's Git workflow tools
```

The **meta-plugin** agent will automatically:
1. Fetch the latest plugin documentation
2. Ask what components to include (agents, commands, skills, etc.)
3. Generate PLUGIN.md manifest
4. Create README documentation
5. Create all components
6. Provide installation instructions

## Using the Interactive Wizard

Alternatively, use the `/create-entity` command:

```bash
/create-entity plugin git-workflow-tools
```

This wizard will guide you through:
1. Plugin purpose and use case
2. What components to include
3. Target audience (personal, team, public)
4. Distribution method

## Example: Git Workflow Plugin

Let's create a plugin that includes:
- Agent for reviewing commits
- Command for deploying
- Skill for Git best practices

The meta-plugin agent will create:

```
git-workflow-tools/
├── PLUGIN.md              # Plugin manifest
├── README.md              # Documentation
├── agents/
│   └── commit-reviewer.md # Reviews commit quality
├── commands/
│   ├── deploy.md          # Deploy to staging/production
│   └── release.md         # Create a release
└── skills/
    └── git-expert/
        └── SKILL.md       # Git best practices
```

## PLUGIN.md Example

```yaml
---
name: git-workflow-tools
version: 1.0.0
description: Complete Git workflow toolkit with review, deployment, and best practices
author: Your Team
repository: https://github.com/yourteam/git-workflow-tools
---

# Git Workflow Tools

A comprehensive plugin for managing Git workflows with commit reviews, automated deployments, and best practice guidance.

## Features

- Automated commit message review
- One-command deployment to staging/production
- Release automation
- Git best practices skill

## Installation

\`\`\`bash
/plugin install git-workflow-tools
\`\`\`
...
```

## Installation After Creation

Once created, you can:

### 1. Test Locally

```bash
/plugin install /path/to/git-workflow-tools
```

### 2. Publish to Git Repository

```bash
cd git-workflow-tools
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/yourteam/git-workflow-tools
git push -u origin main
```

### 3. Share with Team

Team members can install with:

```bash
/plugin marketplace add yourteam/git-workflow-tools
/plugin install git-workflow-tools
```

Or direct install:

```bash
/plugin install https://github.com/yourteam/git-workflow-tools
```

## Using the Plugin

After installation, all components are available:

**Agent** (proactive or manual):
```
Review my last commit for quality
```

**Commands**:
```bash
/deploy staging
/deploy production
/release v1.2.0
```

**Skill** (automatic):
```
How should I structure my Git branches?
```
(Git-expert skill automatically loads)

## Components Example

### commit-reviewer.md (Agent)
```yaml
---
name: commit-reviewer
description: Use proactively to review Git commits for quality, convention adherence, and best practices
tools: Read, Bash, Grep
color: Blue
---

# Purpose

You are a Git commit review specialist...
```

### deploy.md (Slash Command)
```yaml
---
description: Deploy to staging or production environment
argument-hint: [staging|production]
---

# Deploy

Deploy the current branch to the specified environment.

Parse `$ARGUMENTS` to determine target environment...
```

### git-expert/SKILL.md (Skill)
```yaml
---
name: git-expert
description: Git best practices and workflow guidance. Use when discussing Git strategies, branching, or commit practices.
---

# Instructions

You are an expert in Git best practices...
```

## Updating the Plugin

To update:

1. Modify plugin files
2. Update version in PLUGIN.md
3. Commit and push to git
4. Users update with:

```bash
/plugin update git-workflow-tools
```

## Best Practices for Plugins

**DO**:
- Create focused plugins with clear purpose
- Include comprehensive README
- Version your plugins (semver)
- Test all components before publishing
- Document all features and usage

**DON'T**:
- Create monolithic plugins (split into focused ones)
- Forget to update version numbers
- Skip documentation
- Include untested components

## Distribution Strategies

**Personal Use**:
```
Create in ~/.claude/plugins/
Test locally
Use for your own workflows
```

**Team Use**:
```
Create in team repository
Team members add marketplace
Install and share updates via git
```

**Public Use**:
```
Create in public GitHub repo
Submit to community marketplaces
Open source license
Accept contributions
```

## Customization

After creation:
- Edit any component files
- Add new components
- Update documentation
- Adjust for specific needs

All plugin files are standard markdown - easy to edit and version control!
