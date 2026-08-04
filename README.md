# shironigun/ai-marketplace

AI tools marketplace for Claude Code — skills, plugins, and MCP servers
for AI-assisted workflows.

## Install

```bash
claude plugin marketplace add github:shironigun/ai-marketplace
```

## Plugins

| Plugin | Category | Description |
|---|---|---|
| [qa-toolkit](./plugins/qa-toolkit/) | testing | QA workflow automation — test case generation, bug conversion, tracker integration |

## Adding a plugin

1. Create `plugins/<your-plugin>/`
2. Add `.claude-plugin/plugin.json` with name, version, description, author
3. Add your skill/agent/command files under the plugin directory
4. Add one entry to `.claude-plugin/marketplace.json`
5. Push to `main`
