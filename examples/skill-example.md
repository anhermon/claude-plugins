# Example: Creating a Skill

This example shows how to use the meta-tools plugin to create a skill.

## Simple Creation (Just Ask)

The easiest way to create a skill is to simply ask Claude:

```
Create a skill that helps with React component best practices
```

The **meta-skill** agent will automatically:
1. Fetch the latest skills documentation
2. Generate a SKILL.md file with proper frontmatter
3. Set up model-invoked triggering conditions
4. Create supporting files if needed
5. Write to `~/.claude/skills/react-patterns/SKILL.md`
6. Explain how it will be triggered

## Using the Interactive Wizard

Alternatively, use the `/create-entity` command:

```bash
/create-entity skill react-patterns
```

This wizard will guide you through:
1. What specialized capability the skill provides
2. When it should be automatically invoked
3. Whether it needs supporting files (scripts, templates)
4. Best practices to include

## Result

You'll get a skill directory structure like:

```
~/.claude/skills/react-patterns/
├── SKILL.md
├── templates/
│   ├── component-template.tsx
│   └── hook-template.ts
└── examples/
    └── best-practices.md
```

With SKILL.md containing:

```yaml
---
name: react-patterns
description: React component patterns and best practices. Use when creating or reviewing React components.
---

# Instructions

You are an expert in React best practices and modern component patterns.

When this skill is invoked, you should:

1. Analyze React component code for modern patterns
2. Suggest improvements following React best practices
3. Recommend appropriate hooks for the use case
4. Ensure proper TypeScript typing
5. Verify accessibility standards

## When to Use

This skill should be invoked when:
- Creating new React components
- Reviewing existing React code
- Discussing React patterns and architecture
- Helping with React hooks implementation
- Optimizing React component performance

## Capabilities

This skill provides:
- Modern React patterns (hooks, composition)
- TypeScript best practices for React
- Performance optimization techniques
- Accessibility guidelines
- Testing strategies for components
...
```

## How It Works

**Model-Invoked (Automatic)**:

Unlike slash commands, skills are automatically invoked by Claude when relevant!

```
User: "Help me create a modal component in React"

Claude automatically loads react-patterns skill → Provides expert guidance
```

No need to explicitly invoke it!

## Composability

Skills can work together:

```
User: "Create a secure React form component"

Claude automatically loads:
- react-patterns skill (for React best practices)
- security-scanner skill (for security checks)
- accessibility-expert skill (for a11y)

Result: Comprehensive guidance from multiple expertise areas!
```

## Supporting Files

The skill can include:

- **Templates**: Ready-to-use code templates
- **Scripts**: Helper scripts for common tasks
- **Data**: Reference data, lookup tables
- **Documentation**: Additional guides

All accessible to Claude when the skill is invoked.

## Customization

After creation, you can:
- Add more templates
- Include executable Python/Bash scripts
- Add reference documentation
- Refine triggering conditions
- Split large SKILL.md into multiple files

Location: `~/.claude/skills/react-patterns/`

## Testing

To test if the skill is working:

```
Create a React component for a user profile card
```

If the skill is properly configured, Claude will automatically use it and you'll notice React-specific expertise in the response!
