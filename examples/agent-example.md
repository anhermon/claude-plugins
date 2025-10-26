# Example: Creating a Sub-Agent

This example shows how to use the meta-tools plugin to create a sub-agent.

## Simple Creation (Just Ask)

The easiest way to create a sub-agent is to simply ask Claude:

```
Create a sub-agent for reviewing Python code
```

The **meta-agent** will automatically:
1. Fetch the latest sub-agent documentation
2. Ask you clarifying questions about:
   - Specific tasks the agent should perform
   - Tools it needs
   - Whether it should be proactive
3. Generate the agent configuration
4. Write it to `~/.claude/agents/python-code-reviewer.md`
5. Provide usage instructions

## Using the Interactive Wizard

Alternatively, use the `/create-entity` command:

```bash
/create-entity agent python-code-reviewer
```

This wizard will guide you through:
1. Purpose of the agent
2. Primary tasks
3. Required tools
4. Proactive vs manual invocation
5. Output format preferences

## Result

You'll get a properly formatted agent file like:

```yaml
---
name: python-code-reviewer
description: Use proactively for reviewing Python code quality, style, and best practices
tools: Read, Grep, Glob
color: Blue
---

# Purpose

You are a Python code review specialist...

## Instructions

When invoked, follow these steps:
1. Read the Python code files
2. Check for PEP 8 compliance
3. Identify potential bugs
4. Suggest improvements
...
```

## Using the Agent

Once created, the agent can be used:

**Proactively** (if configured):
```
Review this Python file for issues
```

**Manually**:
```
Use the python-code-reviewer agent to analyze app.py
```

## Customization

After creation, you can edit the agent file to:
- Add more specific instructions
- Adjust tool permissions
- Refine the description for better delegation
- Add domain-specific best practices

Location: `~/.claude/agents/python-code-reviewer.md`
