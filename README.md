# shironigun/ai-marketplace

AI tools marketplace for Claude Code — skills, plugins, and MCP servers
for AI-assisted workflows.

## Install

```bash
claude plugin marketplace add shironigun/ai-marketplace
```

## Plugins

| Plugin | Category | Description |
|---|---|---|
| [qa-toolkit](./plugins/qa-toolkit/) | testing | QA workflow automation — test case generation, bug conversion, tracker integration |
| [targetcrm-bug-suite](./plugins/targetcrm-bug-suite/) | bug-tracking | File Bugs and Defects on the TargetCRM ADO project in Mahmood Ahmad's QA house style |
| [release-notes-suite](./plugins/release-notes-suite/) | release-management | Build the engineering release inventory (harvester) and write dealer-facing release notes (releaser) |
| [ui-testing](./plugins/ui-testing/) | testing | UI test case authoring (buggy → ADO) and Playwright UI script generation (tester) |
| [api-testing](./plugins/api-testing/) | testing | API test case authoring and Playwright + TypeScript script generation (api-tester) plus bug triage (api-bugger) |

## Adding a plugin

1. Create `plugins/<your-plugin>/`
2. Add `.claude-plugin/plugin.json` with name, version, description, author
3. Add your skill/agent/command files under the plugin directory
4. Add one entry to `.claude-plugin/marketplace.json`
5. Push to `main`
