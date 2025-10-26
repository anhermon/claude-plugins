# Example: Creating a Slash Command

This example shows how to use the meta-tools plugin to create a slash command.

## Simple Creation (Just Ask)

The easiest way to create a slash command is to simply ask Claude:

```
Create a slash command that runs tests and opens a browser with coverage
```

The **meta-command** agent will automatically:
1. Fetch the latest slash command documentation
2. Study existing command patterns
3. Generate a natural language prompt (not a bash script!)
4. Write it to `~/.claude/commands/test-with-coverage.md`
5. Show usage examples

## Using the Interactive Wizard

Alternatively, use the `/create-entity` command:

```bash
/create-entity command test-with-coverage
```

This wizard will guide you through:
1. What the command should do
2. Whether it needs arguments
3. What tools it should use
4. Expected workflow

## Result

You'll get a properly formatted command file like:

```yaml
---
description: Run tests with coverage and open browser report
---

# Test with Coverage

Run the project's test suite with coverage reporting and automatically open the coverage report in a browser.

## Instructions

1. Use the Bash tool to run the test command with coverage
2. Generate the coverage HTML report
3. Open the coverage report in the default browser
4. Display a summary of the test results

## Example

`/test-with-coverage`
```

## Using the Command

Once created, use it like:

```bash
/test-with-coverage
```

Claude will:
1. Run the tests with coverage
2. Generate the HTML report
3. Open it in your browser
4. Show you a summary

## Key Difference from Scripts

Remember: Slash commands are **prompts**, not scripts!

❌ **Wrong** (writing bash code):
```markdown
```bash
pytest --cov=. --cov-report=html
open htmlcov/index.html
```
```

✅ **Correct** (natural language instructions):
```markdown
Use the Bash tool to:
1. Run pytest with coverage options: `--cov=.` and `--cov-report=html`
2. Open the coverage report in the browser: `htmlcov/index.html`
3. Display the test results summary to the user
```

## Customization

After creation, you can edit the command to:
- Add argument handling
- Refine the workflow
- Add error handling instructions
- Include more detailed examples

Location: `~/.claude/commands/test-with-coverage.md`
