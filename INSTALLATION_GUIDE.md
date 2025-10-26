# Installation & Testing Guide

## Quick Installation

### Method 1: Local Installation (Testing)

```bash
# From within Claude Code, run:
/plugin marketplace add /Users/angelhermon/workspace/claude-plugins
```

Or using relative path if you're in the directory:
```bash
/plugin marketplace add ./
```

Then install the plugin:
```bash
/plugin install meta-tools
```

### Method 2: GitHub Installation (After Publishing)

```bash
# Add marketplace
/plugin marketplace add angelhermon/claude-plugins

# Install plugin
/plugin install meta-tools
```

## Verifying Installation

After installation, verify the components were installed:

### Check Agents
```bash
ls ~/.claude/agents/meta-*
```

Should show:
- meta-agent.md
- meta-command.md
- meta-plugin.md
- meta-skill.md

### Check Commands
```bash
ls ~/.claude/commands/spawn.md ~/.claude/commands/create-entity.md
```

Should show both files.

### Check Skills
```bash
ls ~/.claude/skills/meta-creator/
```

Should show SKILL.md

## Testing Components

### Test 1: Meta-Creator Skill (Automatic Invocation)

Simply ask Claude:
```
Create a sub-agent for testing code
```

**Expected**: The meta-agent should be automatically invoked via the meta-creator skill.

### Test 2: Slash Command - /create-entity

```bash
/create-entity
```

**Expected**: Interactive wizard appears asking what type of entity to create.

### Test 3: Slash Command - /spawn

```bash
/spawn --help
```

Or try spawning a new session:
```bash
/spawn Test new feature --agent code-reviewer
```

**Expected**: New terminal window opens with Claude Code.

### Test 4: Direct Agent Usage

```
Use the meta-command agent to create a slash command for running tests
```

**Expected**: meta-command agent is invoked and creates a test command.

### Test 5: Create Different Entity Types

**Create an Agent:**
```
Create a sub-agent that helps write documentation
```

**Create a Command:**
```
Create a slash command to deploy to production
```

**Create a Skill:**
```
Create a skill for Python best practices
```

**Create a Plugin:**
```
Create a plugin package for our team's workflow tools
```

## Troubleshooting

### Issue: Marketplace file not found

**Error:**
```
Marketplace file not found at /path/.claude-plugin/marketplace.json
```

**Solution:**
Make sure you're adding the marketplace from the correct path:
```bash
# Use absolute path
/plugin marketplace add /Users/angelhermon/workspace/claude-plugins

# Or if you're in the repo directory
/plugin marketplace add ./
```

### Issue: Plugin not found in marketplace

**Error:**
```
Plugin 'meta-tools' not found in marketplace
```

**Solution:**
1. Verify marketplace.json exists:
   ```bash
   cat .claude-plugin/marketplace.json
   ```

2. Check the marketplace was added:
   ```bash
   /plugin marketplace list
   ```

3. Reinstall marketplace:
   ```bash
   /plugin marketplace remove claude-plugins-marketplace
   /plugin marketplace add /Users/angelhermon/workspace/claude-plugins
   ```

### Issue: Components not appearing after install

**Problem:** Agents, commands, or skills not showing up in ~/.claude/

**Solution:**
1. Check plugin installation:
   ```bash
   /plugin list
   ```

2. Verify plugin.json exists:
   ```bash
   cat plugins/meta-tools/.claude-plugin/plugin.json
   ```

3. Reinstall plugin:
   ```bash
   /plugin uninstall meta-tools
   /plugin install meta-tools
   ```

4. Restart Claude Code

### Issue: Agents not being invoked proactively

**Problem:** Asking to create something but meta-agents don't activate

**Solution:**
1. Be more explicit:
   ```
   Create a sub-agent for code reviews
   Create a slash command for deployment
   Create a skill for React
   ```

2. Or use the slash command:
   ```bash
   /create-entity agent my-agent
   ```

3. Verify meta-creator skill was installed:
   ```bash
   ls ~/.claude/skills/meta-creator/SKILL.md
   ```

## Directory Structure After Installation

```
~/.claude/
├── agents/
│   ├── meta-agent.md
│   ├── meta-command.md
│   ├── meta-plugin.md
│   └── meta-skill.md
├── commands/
│   ├── spawn.md
│   └── create-entity.md
└── skills/
    └── meta-creator/
        └── SKILL.md
```

## Uninstalling

To uninstall the plugin:

```bash
/plugin uninstall meta-tools
```

To remove the marketplace:

```bash
/plugin marketplace remove claude-plugins-marketplace
```

## Publishing to GitHub

Once tested locally, publish to GitHub:

```bash
# Initialize git (if not done)
git add .
git commit -m "Complete meta-tools plugin with marketplace"

# Create GitHub repo and push
git remote add origin https://github.com/angelhermon/claude-plugins.git
git branch -M main
git push -u origin main
```

Then users can install with:

```bash
/plugin marketplace add angelhermon/claude-plugins
/plugin install meta-tools
```

## Advanced Testing

### Test Marketplace JSON

Validate the marketplace.json:
```bash
cat .claude-plugin/marketplace.json | jq .
```

### Test Plugin JSON

Validate the plugin.json:
```bash
cat plugins/meta-tools/.claude-plugin/plugin.json | jq .
```

### Test Component Files

**Agents:**
```bash
head -20 plugins/meta-tools/agents/meta-agent.md
```

**Commands:**
```bash
head -20 plugins/meta-tools/commands/spawn.md
```

**Skills:**
```bash
head -20 plugins/meta-tools/skills/meta-creator/SKILL.md
```

## Success Criteria

Installation is successful when:

- ✅ Marketplace added without errors
- ✅ Plugin installed without errors
- ✅ 4 meta-agents in ~/.claude/agents/
- ✅ 2 slash commands in ~/.claude/commands/
- ✅ 1 skill in ~/.claude/skills/
- ✅ meta-creator skill automatically invokes when creating
- ✅ /spawn and /create-entity commands work
- ✅ Can create agents, commands, skills, and plugins

## Support

If you encounter issues:

1. Check this guide's troubleshooting section
2. Verify all JSON files are valid
3. Ensure file paths are correct
4. Restart Claude Code
5. Open an issue at: https://github.com/angelhermon/claude-plugins/issues
