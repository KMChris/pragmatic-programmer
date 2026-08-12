# Pragmatic Programmer

[![skills.sh](https://skills.sh/b/KMChris/pragmatic-programmer)](https://skills.sh/KMChris/pragmatic-programmer)

`pragmatic-programmer` is a repository-level engineering workflow for coding agents. It guides an agent through repository inspection, focused implementation, testing, documentation, diff review, and a checkpoint commit without tying the workflow to a single host.

The distribution contains one canonical Agent Skill at `plugins/pragmatic-programmer/skills/pragmatic-programmer/SKILL.md`. Claude Code, Codex, and Google Antigravity all load that same file through their native plugin manifests.

## Recommended install with npx skills

Install the skill from this public GitHub repository with the open `skills` CLI. The interactive flow detects supported coding agents installed on the machine and asks where the skill should be installed:

```shell
npx skills@latest add KMChris/pragmatic-programmer
```

To install globally for a specific agent without prompts, pass its agent ID. Common IDs include `claude-code`, `codex`, `cursor`, `github-copilot`, `gemini-cli`, and `antigravity`:

```shell
npx skills@latest add KMChris/pragmatic-programmer --global --agent <agent-id> --yes
```

## Requirements

- A coding agent with filesystem and terminal access
- Git for checkpoint commits
- The command-line client or desktop application for the selected host

## Alternative installs

### Claude Code

Add the public GitHub repository as a marketplace, then install the plugin:

```shell
claude plugin marketplace add KMChris/pragmatic-programmer
claude plugin install pragmatic-programmer@pragmatic-programmer
```

For a development-only session from a local clone, load the plugin directory directly:

```shell
claude --plugin-dir <repo-root>/plugins/pragmatic-programmer
```

Claude can select the skill automatically. You can also invoke it explicitly as `/pragmatic-programmer:pragmatic-programmer`.

### Codex

Register the repository marketplace:

```shell
codex plugin marketplace add KMChris/pragmatic-programmer
```

Restart the Codex desktop app, open the Plugins Directory, select the `Pragmatic Programmer` marketplace, and install `pragmatic-programmer`. Invoke the installed skill as `$pragmatic-programmer` or describe a matching repository task and let Codex select it automatically.

### Google Antigravity

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
LICENSE
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

## License

Released under the [MIT License](LICENSE). Copyright (c) 2026 Krzysztof Mizgała.
