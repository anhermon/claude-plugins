---
description: Execute a prompt with AI model and return results (supports Claude, Gemini, Codex)
argument-hint: MODEL PROMPT [--timeout MS] [--dir PATH] [--background]
---

# Prompt - Execute with AI Model

Execute a single prompt with a specific AI model and return the results to the current session.

**Supports:** Claude (all versions), Gemini, OpenAI/Codex

**Key Features:**
- Intelligent model detection (supports aliases like `sonnet-4.5`, `opus-4`, `gpt-4`)
- Multi-model support (Claude, Gemini, Codex)
- Returns results to current session
- Background execution support
- For interactive sessions, use `/spawn` instead

## Parse Arguments

Parse arguments from `$ARGUMENTS`:
- `MODEL`: Required - AI model to use (supports aliases, full IDs, or CLI types)
- `PROMPT`: Required - The prompt/task to execute
- `--timeout MS`: Optional - Timeout in milliseconds (default: 120000)
- `--dir PATH`: Optional - Working directory (default: current directory)
- `--background`: Optional - Run in background mode

**Model Specification Options:**
- **Aliases:** `sonnet-4.5`, `opus-4`, `haiku-3.5`, `gpt-4`, `gemini-2.0`
- **Full IDs:** `claude-sonnet-4-5-20250929`, `gemini-2.0-flash-exp`
- **CLI types:** `claude`, `gemini`, `codex` (uses default model)

## Instructions

### 1. Validate Arguments

Check that required arguments are provided:
- Model specification is present
- Prompt is non-empty
- Timeout is positive integer (if specified)
- Directory exists (if specified)

If validation fails:
```
Error: Missing required arguments

Usage: /prompt MODEL PROMPT [OPTIONS]

Examples:
  /prompt sonnet-4.5 "What is the capital of France?"
  /prompt gemini "Search for React best practices"
  /prompt gpt-4 "Generate a Python function"
  /prompt claude-opus-4-20250514 "Deep code analysis" --timeout 300000
```

### 2. Execute Prompt

**Decision: Same Context vs Separate Context**

- If you just need to run a CLI command and capture output: Use **Bash tool directly** (same context)
- If you need isolated execution with separate context: Use **Task tool** with `general-purpose` agent

**Option A: Direct Execution (Recommended for most cases)**

Use Bash tool to execute CLI commands directly:

**Steps:**
1. Parse the MODEL parameter to determine CLI type (`claude`, `gemini-cli`, or `codex`)
2. Resolve model aliases to full IDs if needed (e.g., `sonnet-4.5` → `claude-sonnet-4-5-20250929`)
3. Construct the appropriate command
4. Change to the working directory (if specified)
5. Execute the command with the specified timeout

**Command Construction:**
- For Claude: `claude --model [model-id] "[prompt]"` or just `claude "[prompt]"`
- For Gemini: `gemini-cli --model [model-id] "[prompt]"` or `gemini-cli "[prompt]"`
- For Codex: `codex --model [model-id] "[prompt]"` or `codex "[prompt]"`

**Execution:**
```bash
cd [working-directory] && [cli-command]
```

Use the Bash tool with appropriate timeout setting.

**Option B: Isolated Execution (When separate context needed)**

If the task requires isolated context, use the Task tool:

```
Task(
  subagent_type="general-purpose",
  description="Execute [model] prompt",
  prompt="Execute the following prompt with [model]:

  Prompt: [user's prompt]
  Working Directory: [directory]

  Use Bash tool to run: [cli-command]"
)
```

**When to use each:**
- Direct Bash: Quick commands, output capture, same-context execution
- Task tool: Complex tasks requiring isolated context or multiple steps

### 3. Handle Response

Process the command output and format for user:

**If Successful:**
```
✓ Executed with [model]

Output:
[model output]

Completed in [execution time]
```

**If Failed:**
```
✗ Execution failed with [model]

Error: [error message]

Suggestion: [remediation steps]
```

**If CLI Not Found:**
```
✗ [model] CLI not found

Installation instructions:
[model-specific installation steps]
```

## Examples

### Example 1: Simple Question with Alias
```bash
/prompt sonnet-4.5 "What is the capital of France?"
```

### Example 2: Code Review with Full Model ID
```bash
/prompt claude-opus-4-20250514 "Review app.py for security issues" --dir /path/to/project
```

### Example 3: Research Task with Gemini
```bash
/prompt gemini "Find the latest best practices for React hooks in 2025"
```

### Example 4: Code Generation with GPT-4
```bash
/prompt gpt-4 "Generate a Python function to parse CSV files"
```

### Example 5: Long Task with Timeout
```bash
/prompt opus-4 "Analyze this entire codebase" --timeout 600000
```

### Example 6: Background Execution
```bash
/prompt haiku-3.5 "Run all tests and generate coverage report" --background
```

### Example 7: Using Different Model Aliases
```bash
# All Claude aliases work
/prompt sonnet-4.5 "Explain quantum computing"
/prompt opus-4 "Deep analysis of architecture"
/prompt haiku-3.5 "Quick summary of changes"
```

### Example 8: Compare Models
```bash
# Run same prompt with different models
/prompt sonnet-4.5 "Explain async/await"
/prompt gemini "Explain async/await"
/prompt gpt-4 "Explain async/await"
```

## Model-Specific Notes

### Claude Code
- Best for: Code review, complex reasoning, detailed explanations
- CLI: `claude`
- Supports: Multiple model versions via --model flag
- Strengths: Deep code analysis, security review, architectural guidance

### Gemini CLI
- Best for: Research, web search, quick information retrieval
- CLI: `gemini-cli`
- Supports: Google's Gemini models
- Strengths: Current information, search integration, fast responses

### ChatGPT Codex
- Best for: Code generation, completion, refactoring
- CLI: `codex`
- Supports: OpenAI's Codex models
- Strengths: Code synthesis, pattern recognition, quick prototypes

## Advanced Usage

### Parallel Execution

Execute multiple prompts in parallel:
```bash
/prompt sonnet-4.5 "Task 1" --background
/prompt gemini "Task 2" --background
/prompt gpt-4 "Task 3" --background
```

### Sequential Pipeline

Chain execution results:
```bash
# Step 1: Generate code with GPT-4
/prompt gpt-4 "Generate a REST API in Python"

# Step 2: Review with Claude Opus
/prompt opus-4 "Review the generated API code for issues"

# Step 3: Research with Gemini
/prompt gemini "Find best practices for the identified issues"
```

### Model Comparison Workflow

Execute the same prompt with different models to compare:
```bash
/prompt sonnet-4.5 "Explain dependency injection" --background
/prompt opus-4 "Explain dependency injection" --background
/prompt gemini "Explain dependency injection" --background
/prompt gpt-4 "Explain dependency injection" --background
```

## Error Handling

The command handles these error scenarios:

**Missing Arguments:**
- Shows usage help
- Lists required parameters
- Provides examples

**Invalid Model:**
- Lists valid model options
- Suggests closest match
- Shows installation status of each CLI

**CLI Not Installed:**
- Provides installation instructions
- Links to documentation
- Suggests alternative models

**Execution Timeout:**
- Returns partial results if available
- Suggests increasing timeout
- Recommends background execution

**Permission Errors:**
- Checks directory permissions
- Suggests solutions
- Validates file access

## Best Practices

1. **Choose the Right Model:**
   - Claude for complex reasoning and code review
   - Gemini for research and current information
   - Codex for code generation and completion

2. **Set Appropriate Timeouts:**
   - Simple queries: 60-120 seconds
   - Code analysis: 2-5 minutes
   - Large tasks: 5-10 minutes

3. **Use Background Mode:**
   - For tasks > 2 minutes
   - When running parallel tasks
   - For non-blocking workflows

4. **Validate Results:**
   - Review generated code before execution
   - Verify information from multiple sources
   - Test code in isolated environment

5. **Handle Errors Gracefully:**
   - Check CLI availability first
   - Set reasonable timeouts
   - Have fallback strategies

## Troubleshooting

### "Model CLI not found"
- Install the required CLI tool
- Verify it's in your PATH
- Try using the full path to CLI

### "Command timeout"
- Increase timeout value
- Use background execution
- Break task into smaller chunks

### "Permission denied"
- Check directory permissions
- Verify file access rights
- Run with appropriate privileges

### "API rate limit"
- Wait and retry
- Use different API key
- Switch to alternative model

### "Unexpected output format"
- Add output format instructions to prompt
- Parse stderr for warnings
- Verify CLI version

## Notes

- The command contains the logic to execute CLI tools
- By default, uses Bash tool directly for same-context execution
- For separate context/isolation, can use Task tool with general-purpose agent
- API keys must be configured for each CLI
- Results can be piped to files using shell redirection
- Background tasks can be monitored via process ID
- Execution logs are stored in `.claude/logs/` (if configured)

## Related Commands

- `/spawn`: Launch new interactive Claude Code session in terminal window
- `/create-entity`: Create new agents, commands, skills, or plugins
- For interactive sessions, use `/spawn` instead of `/prompt`

## Command vs Spawn

**Use `/prompt` when:**
- You want a single answer returned to current session
- Comparing outputs from different models
- Integrating results into current workflow
- Running background tasks that report back

**Use `/spawn` when:**
- You want a new interactive terminal session
- Working on multiple tasks in parallel
- Need a persistent separate context
- Want to use different agents simultaneously

## References

- [Claude Code CLI](https://docs.claude.com/en/docs/claude-code/quickstart)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [OpenAI Codex](https://openai.com/codex)
- [Sub-Agent Documentation](https://docs.claude.com/en/docs/claude-code/sub-agents)
