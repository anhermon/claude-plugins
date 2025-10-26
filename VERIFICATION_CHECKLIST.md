# Verification Checklist

## Pre-Installation Verification

### ✅ Repository Structure
- [x] `.claude-plugin/marketplace.json` exists
- [x] `plugins/meta-tools/.claude-plugin/plugin.json` exists
- [x] All agent files in `plugins/meta-tools/agents/`
- [x] All command files in `plugins/meta-tools/commands/`
- [x] Skill file in `plugins/meta-tools/skills/meta-creator/`
- [x] README.md documentation complete
- [x] LICENSE file present
- [x] .gitignore properly configured

### ✅ JSON Validation

```bash
# Validate marketplace.json
cat .claude-plugin/marketplace.json | jq .

# Validate plugin.json
cat plugins/meta-tools/.claude-plugin/plugin.json | jq .
```

Both should parse without errors.

### ✅ File Count

Expected files:
- **Agents**: 4 (meta-agent, meta-command, meta-skill, meta-plugin)
- **Commands**: 2 (spawn, create-entity)
- **Skills**: 1 (meta-creator)
- **Config**: 2 JSON files (marketplace.json, plugin.json)
- **Docs**: 10+ markdown files

## Installation Test

### Step 1: Add Marketplace

```bash
/plugin marketplace add /Users/angelhermon/workspace/claude-plugins
```

**Expected Output:**
```
✓ Added marketplace: claude-plugins-marketplace
```

### Step 2: Verify Marketplace

```bash
/plugin marketplace list
```

**Expected:** Should show "claude-plugins-marketplace"

### Step 3: Install Plugin

```bash
/plugin install meta-tools
```

**Expected Output:**
```
✓ Installing plugin: meta-tools
✓ Installed agents: meta-agent, meta-command, meta-skill, meta-plugin
✓ Installed commands: spawn, create-entity
✓ Installed skills: meta-creator
✓ Plugin installed successfully
```

### Step 4: Verify Installation

```bash
# Check agents
ls ~/.claude/agents/meta-*

# Check commands
ls ~/.claude/commands/{spawn,create-entity}.md

# Check skills
ls ~/.claude/skills/meta-creator/SKILL.md
```

All files should exist.

## Functional Testing

### Test 1: Meta-Creator Skill (Automatic)

**Test:**
```
Create a sub-agent for code reviews
```

**Expected:**
- Meta-creator skill is invoked (you might see a brief message)
- meta-agent is delegated to
- Questions are asked about the agent
- Agent file is created at `~/.claude/agents/code-reviewer.md`

**Verify:**
```bash
ls ~/.claude/agents/code-reviewer.md
cat ~/.claude/agents/code-reviewer.md | head -20
```

---

### Test 2: /create-entity Command

**Test:**
```bash
/create-entity
```

**Expected:**
- Interactive menu appears
- Options: agent, command, skill, plugin
- Can select and proceed through wizard

---

### Test 3: /spawn Command

**Test:**
```bash
/spawn Review code in main.py
```

**Expected:**
- New terminal window opens
- Claude Code starts
- (Optional) Task is provided to Claude

Note: May not work on all systems due to terminal emulator differences.

---

### Test 4: Create Slash Command

**Test:**
```
Create a slash command to run tests with coverage
```

**Expected:**
- meta-command agent is invoked
- Questions about command details
- Command file created at `~/.claude/commands/test-coverage.md`

**Verify:**
```bash
cat ~/.claude/commands/test-coverage.md
```

---

### Test 5: Create Skill

**Test:**
```
Create a skill for React best practices
```

**Expected:**
- meta-skill agent is invoked
- Questions about the skill
- Skill directory created at `~/.claude/skills/react-patterns/`
- SKILL.md created inside

**Verify:**
```bash
ls ~/.claude/skills/react-patterns/
cat ~/.claude/skills/react-patterns/SKILL.md
```

---

### Test 6: Create Plugin

**Test:**
```
Create a plugin for Git workflow automation
```

**Expected:**
- meta-plugin agent is invoked
- Questions about components to include
- Plugin directory created
- PLUGIN.md manifest created
- All specified components created

**Verify:**
```bash
ls -R /path/to/created/plugin/
```

---

## Component Verification

### Agents Verification

For each agent, verify:

```bash
# Check frontmatter is valid
head -10 ~/.claude/agents/meta-agent.md

# Should show:
# ---
# name: meta-agent
# description: ...
# tools: ...
# color: ...
# ---
```

All 4 agents should have:
- ✅ Valid YAML frontmatter
- ✅ Proactive description ("Use proactively when...")
- ✅ Tools specified or omitted
- ✅ Color set
- ✅ Instructions section
- ✅ WebFetch calls to latest documentation

### Commands Verification

For each command, verify:

```bash
# Check frontmatter
head -10 ~/.claude/commands/spawn.md

# Should show:
# ---
# description: ...
# argument-hint: ... (if applicable)
# ---
```

Both commands should have:
- ✅ Valid YAML frontmatter
- ✅ Clear description
- ✅ Natural language instructions (NOT bash scripts)
- ✅ Usage examples

### Skill Verification

```bash
# Check skill frontmatter
head -20 ~/.claude/skills/meta-creator/SKILL.md

# Should show:
# ---
# name: meta-creator
# description: ...
# ---
```

Skill should have:
- ✅ Valid YAML frontmatter
- ✅ Description with "when to use"
- ✅ Instructions section
- ✅ When to Use section
- ✅ Examples section

## Documentation Verification

### README.md
- ✅ Installation instructions
- ✅ Feature list
- ✅ Usage examples
- ✅ Component descriptions

### ARCHITECTURE.md
- ✅ Technical design
- ✅ Data flow diagrams
- ✅ Component relationships

### INSTALLATION_GUIDE.md
- ✅ Step-by-step installation
- ✅ Troubleshooting section
- ✅ Verification steps

### Examples
- ✅ agent-example.md
- ✅ command-example.md
- ✅ skill-example.md
- ✅ plugin-example.md

## Error Testing

### Test Invalid Marketplace Path

```bash
/plugin marketplace add /invalid/path
```

**Expected:** Error message about marketplace not found

### Test Duplicate Installation

```bash
/plugin install meta-tools
# (already installed)
```

**Expected:** Message about already installed or reinstallation prompt

### Test Uninstall and Reinstall

```bash
/plugin uninstall meta-tools
ls ~/.claude/agents/meta-*
# Should show: No such file or directory

/plugin install meta-tools
ls ~/.claude/agents/meta-*
# Should show: All 4 agents
```

## Final Checklist

Before marking as complete:

- [ ] Marketplace.json valid and correct
- [ ] Plugin.json valid and correct
- [ ] All 4 agents present and formatted correctly
- [ ] All 2 commands present and formatted correctly
- [ ] 1 skill present and formatted correctly
- [ ] Marketplace installation successful
- [ ] Plugin installation successful
- [ ] Components copied to ~/.claude/ correctly
- [ ] Meta-creator skill automatically invokes
- [ ] Can create agents via meta-agent
- [ ] Can create commands via meta-command
- [ ] Can create skills via meta-skill
- [ ] Can create plugins via meta-plugin
- [ ] /spawn command works
- [ ] /create-entity command works
- [ ] All documentation complete
- [ ] README accurate
- [ ] Examples helpful
- [ ] No errors in logs

## Success Criteria

✅ **Installation Success:**
- Marketplace added without errors
- Plugin installed without errors
- All components in correct locations

✅ **Functional Success:**
- Can create agents automatically
- Can create commands automatically
- Can create skills automatically
- Can create plugins automatically
- Slash commands work
- Meta-creator skill routes correctly

✅ **Quality Success:**
- All files properly formatted
- YAML frontmatter valid
- Documentation complete
- Examples working

## Known Limitations

1. **/spawn command**: May not work on all terminal emulators
2. **WebFetch**: Requires internet connection for documentation fetching
3. **Proactive invocation**: Requires clear, explicit language

## Support

If any test fails, check:
1. JSON syntax with `jq`
2. File permissions
3. Claude Code version compatibility
4. Log files for errors

Report issues at: https://github.com/angelhermon/claude-plugins/issues
