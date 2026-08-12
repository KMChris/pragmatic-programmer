# Pragmatic Programmer

`pragmatic-programmer` is a repository-level engineering workflow for coding agents. It guides an agent through repository inspection, focused implementation, testing, documentation, diff review, and a checkpoint commit without tying the workflow to a single host.

The distribution contains one canonical Agent Skill at `plugins/pragmatic-programmer/skills/pragmatic-programmer/SKILL.md`. Claude Code, Codex, and Google Antigravity all load that same file through their native plugin manifests.

## Requirements

- A coding agent with filesystem and terminal access
- Git for checkpoint commits
- The command-line client or desktop application for the selected host

## Claude Code

Add this repository as a local marketplace, then install the plugin:

```shell
claude plugin marketplace add <repo-root>
claude plugin install pragmatic-programmer@pragmatic-programmer
```

For a development-only session, load the plugin directory directly:

```shell
claude --plugin-dir <repo-root>/plugins/pragmatic-programmer
```

Claude can select the skill automatically. You can also invoke it explicitly as `/pragmatic-programmer:pragmatic-programmer`.

## Codex

Register the repository marketplace:

```shell
codex plugin marketplace add <repo-root>
```

Restart the Codex desktop app, open the Plugins Directory, select the `Pragmatic Programmer` marketplace, and install `pragmatic-programmer`. Invoke the installed skill as `$pragmatic-programmer` or describe a matching repository task and let Codex select it automatically.

## Google Antigravity

Install the shared plugin directory with the Antigravity CLI:

```shell
agy plugin install <repo-root>/plugins/pragmatic-programmer
```

For manual installation, copy `plugins/pragmatic-programmer` into one of Antigravity's plugin locations:

- Workspace: `.agents/plugins/` or `_agents/plugins/`
- Global: `~/.gemini/config/plugins/`

Antigravity discovers the skill under the `pragmatic-programmer` plugin namespace.

## Package layout

```text
.claude-plugin/marketplace.json
.agents/plugins/marketplace.json
plugins/pragmatic-programmer/
  .claude-plugin/plugin.json
  .codex-plugin/plugin.json
  plugin.json
  skills/pragmatic-programmer/
    SKILL.md
    agents/openai.yaml
    references/decision-checklist.md
```

## Validation

From the repository root, run the checks available for the installed hosts:

```shell
claude plugin validate .
claude plugin validate ./plugins/pragmatic-programmer
agy plugin validate ./plugins/pragmatic-programmer
uvx --from "git+https://github.com/agentskills/agentskills.git#subdirectory=skills-ref" skills-ref validate ./plugins/pragmatic-programmer/skills/pragmatic-programmer
python <codex-home>/skills/.system/plugin-creator/scripts/validate_plugin.py ./plugins/pragmatic-programmer
```

The `uvx` command runs the reference Agent Skills validator in an isolated tool environment. The plugin itself contains no MCP servers, hooks, runtime scripts, or external dependencies.
