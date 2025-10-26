---
description: Launch a new Claude Code CLI instance in a new terminal window
argument-hint: [TASK] [--agent AGENT_TYPE] [--model MODEL]
---

# Spawn New Claude Code Session

Launch a new Claude Code CLI instance in a separate terminal window, optionally with a specific task, agent, or model.

## Parse Arguments

Parse arguments from `$ARGUMENTS`:
- `TASK`: Optional task description to start with (everything before flags)
- `--agent AGENT_TYPE`: Optional agent to start with
- `--model MODEL`: Optional model to use (supports aliases and full IDs)

**Model Specification Options:**
- Full model IDs: `claude-sonnet-4-5-20250929`, `claude-opus-4-20250514`
- Shorthand aliases: `sonnet-4.5`, `opus-4`, `haiku-3.5`
- CLI type only: `claude` (uses default model)

If no arguments provided, launch a fresh Claude Code session.

## Instructions

1. **Parse the arguments** to extract:
   - Task description (if any)
   - Agent type (if --agent flag present)
   - Model (if --model flag present)

2. **Resolve model alias to full ID** (if model specified):

   Apply the same intelligent model detection used in sub-agent-executor:

   **Claude Model Aliases:**
   - `sonnet-4.5` or `claude-sonnet-4-5-20250929` → `claude-sonnet-4-5-20250929`
   - `sonnet-3.7` or `claude-3-7-sonnet-20250219` → `claude-3-7-sonnet-20250219`
   - `sonnet-3.5` or `claude-3-5-sonnet-20241022` → `claude-3-5-sonnet-20241022`
   - `opus-4` or `claude-opus-4-20250514` → `claude-opus-4-20250514`
   - `opus-3` or `claude-3-opus-20240229` → `claude-3-opus-20240229`
   - `haiku-3.5` or `claude-3-5-haiku-20241022` → `claude-3-5-haiku-20241022`
   - `haiku-3` or `claude-3-haiku-20240307` → `claude-3-haiku-20240307`

   **Detection Rules:**
   - If model contains `sonnet-4.5` or `sonnet-4-5`: Use `claude-sonnet-4-5-20250929`
   - If model contains `sonnet-3.7` or `sonnet-3-7`: Use `claude-3-7-sonnet-20250219`
   - If model contains `opus-4`: Use `claude-opus-4-20250514`
   - If model contains `haiku-3.5` or `haiku-3-5`: Use `claude-3-5-haiku-20241022`
   - If model is already a full ID (contains date suffix): Use as-is
   - If model is unrecognized: Show error with available options

3. **Determine the current shell** by checking `$SHELL` environment variable

4. **Construct the Claude Code command:**
   - Base: `claude`
   - If agent specified: Add agent invocation
   - If model specified: Add `--model [resolved-model-id]`
   - If task specified: Add task as quoted argument

5. **Launch in new terminal window:**
   - **macOS**: Use `osascript` to open new Terminal or iTerm2 window
   - **Linux**: Use `gnome-terminal`, `konsole`, or `xterm` depending on availability
   - **Windows**: Use `start` command with `cmd` or `powershell`

6. **Report success** to the user with details of what was launched:
   - Terminal window ID
   - Working directory
   - Resolved model (if alias was used)
   - Full command executed

## Examples

### Example 1: Fresh Session
```
/spawn
```
Opens a new terminal with a fresh Claude Code session.

### Example 2: With Task
```
/spawn Review the authentication code
```
Opens new terminal and starts Claude with the task "Review the authentication code".

### Example 3: With Specific Agent
```
/spawn --agent code-reviewer
```
Opens new terminal and starts with the code-reviewer agent active.

### Example 4: With Task and Agent
```
/spawn Fix the bug in user.py --agent debugging-specialist
```
Opens new terminal with debugging-specialist agent and the task "Fix the bug in user.py".

### Example 5: With Specific Model (Full ID)
```
/spawn --model claude-3-7-sonnet-20250219
```
Opens new terminal with the specified model.

### Example 6: With Model Alias (Shorthand)
```
/spawn --model sonnet-4.5
```
Opens new terminal with Sonnet 4.5 (automatically resolves to `claude-sonnet-4-5-20250929`).

### Example 7: Everything Combined
```
/spawn Optimize the database queries --agent performance-reviewer --model opus-4
```
Opens new terminal with performance-reviewer agent, Opus 4 model (resolves to `claude-opus-4-20250514`), and the optimization task.

### Example 8: Multiple Aliases
```bash
# All of these work and resolve correctly:
/spawn --model sonnet-4.5 "Review code"
/spawn --model opus-4 "Deep analysis"
/spawn --model haiku-3.5 "Quick task"
```

## Platform-Specific Commands

### macOS (Terminal.app)
```applescript
osascript -e 'tell application "Terminal" to do script "cd \"$(pwd)\" && claude [args]"'
```

### macOS (iTerm2)
```applescript
osascript -e 'tell application "iTerm" to create window with default profile command "cd \"$(pwd)\" && claude [args]"'
```

### Linux (gnome-terminal)
```bash
gnome-terminal -- bash -c "cd $(pwd) && claude [args]; exec bash"
```

### Linux (konsole)
```bash
konsole -e bash -c "cd $(pwd) && claude [args]; exec bash"
```

### Windows (PowerShell)
```powershell
start powershell -Command "cd '$(pwd)'; claude [args]"
```

## Error Handling

Handle these cases gracefully:
- No terminal emulator available: Inform user and suggest alternatives
- Invalid agent specified: Show available agents
- Invalid model specified: Show available models
- Command construction fails: Show the command that would have run

## Notes

- The new session starts in the same working directory as the current session
- Environment variables from the current session may not transfer
- Each session is independent with its own context
- Useful for parallel work on different tasks
