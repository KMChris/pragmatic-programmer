# Pragmatic Programmer

A repository-level engineering workflow for coding agents. The plugin adds one skill, `pragmatic-programmer`, that guides the agent through inspecting an existing codebase, making a focused change, validating it with the strongest checks the project offers, reviewing the diff, and recording a checkpoint commit with a short English message. It ends with a brief report backed by the evidence it gathered.

## What it contains and runs

- One Agent Skill: `skills/pragmatic-programmer/SKILL.md`, with a decision checklist in `skills/pragmatic-programmer/references/`.
- No hooks, MCP servers, scripts, or external dependencies. The plugin itself runs nothing and makes no network requests.
- The skill tells the agent to work in your repository with its usual tools: read files, edit them, run the project's own build and test commands, and create a git commit on the current branch after each completed task. Your agent's normal permission prompts still apply to each of these actions.

## Install in Claude Code

Install it from Claude's plugin directory once it is listed there, or from this repository's marketplace:

```shell
claude plugin marketplace add KMChris/pragmatic-programmer
claude plugin install pragmatic-programmer@pragmatic-programmer
```

Claude selects the skill on its own for matching repository tasks. You can also call it explicitly as `/pragmatic-programmer:pragmatic-programmer`.

## Examples

- "Add input validation to the signup form and cover it with tests." The agent finds the form and its test setup, implements the change, runs the tests, reviews the diff, and commits.
- "The nightly export job fails on empty files. Fix it." The agent reproduces the failure, fixes the cause, adds a regression test, and reports what it verified.
- "Rename the `UserStore` class to `AccountStore` across the project." The agent makes the rename consistently, runs the build and tests, and records one checkpoint commit.

## Notes

Inspired by the book *The Pragmatic Programmer*. This project is not affiliated with its authors or publisher, nor with Anthropic.

## License

MIT. See [LICENSE](LICENSE).
